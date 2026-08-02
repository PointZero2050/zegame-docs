# Écart de portage à arbitrer — le facilitateur perd son périmètre de communautés

> Rédigé par Claude (instance pile neuve), 2026-08-02, après confrontation du portage à
> [caracterisation-auth-roles-autorisations.md](caracterisation-auth-roles-autorisations.md).
> **Décision produit demandée à Boris.** Aucun code n'est modifié tant qu'elle n'est pas prise.

## 1. Ce que fait la source

Dans `zegame-app`, le facilitateur (`role: dff`) a des pouvoirs **bornés à une liste explicite
de communautés**, portée par une table de jonction `dffs {user_id, community_id}` :

- `roles(:edit, :update, :destroy) { user.is_admin? or user.dff_community_ids.include?(challenge.community_id) }`
  — un facilitateur de la communauté A ne peut pas toucher un objet de la communauté B ;
- deux garde-fous d'intégrité côté `User` : `keep_only_good_communities` (retaille les
  communautés d'un DFF à son périmètre) et `ensure_dff_communities` (vide le périmètre si le
  rôle n'est plus `dff`) ;
- la caractérisation le formule explicitement : « **Un DFF de la communauté A ne doit jamais
  agir sur un objet de la communauté B** » (§7.2).

État réel en production : 4 facilitateurs, **une communauté chacun**.

## 2. Ce que fait mon portage

J'ai supprimé la table `dffs` et fait de `facilitateur` un **rôle global**, sans périmètre.
Documenté dans l'inventaire comme « la notion de facilitateur par communauté est remplacée par
le rôle global » — formulation qui présentait un **élargissement de pouvoirs** comme une simple
simplification. C'est l'écart le plus significatif du portage à ce jour, et il n'aurait pas été
détecté sans la caractérisation.

**Portée actuelle du problème : nulle en pratique, réelle en principe.** Le rôle n'est
aujourd'hui lu qu'à un seul endroit (`Gestion::BaseController` → accès à l'espace de gestion des
événements), et les contrôleurs du jeu ne sont pas encore portés. Rien n'est cassé ; mais si je
porte les contrôleurs sur cette base, **chaque facilitateur pourra éditer les expériences,
parcours et compétences de tous les Mondes**, ce que la source interdit.

## 3. Pourquoi j'ai dévié (et pourquoi ce n'était pas à moi de trancher)

Deux raisons se sont enchaînées sans que j'en mesure l'effet cumulé :

1. Boris a indiqué que les **cinq créateurs d'événements** seraient facilitateurs ou
   administrateurs. Pour la billetterie, un rôle global suffit : un événement n'appartient à
   aucune communauté.
2. La table `dffs` référençait des communautés dont le portage n'était pas encore fait.

J'ai donc optimisé pour le besoin du moment (les événements) en supprimant un mécanisme qui
sert **au jeu**, pas aux événements. Le besoin réel diffère selon l'objet : le site est global,
le jeu est scopé.

## 4. Trois options

| Option | Description | Conséquence |
|---|---|---|
| **A. Rôle global partout** (état actuel) | Un facilitateur peut tout éditer dans tous les Mondes | Le plus simple. Acceptable si les facilitateurs sont peu nombreux et de confiance — c'est le cas aujourd'hui (4 personnes). Diverge de la source : à assumer explicitement, pas à subir |
| **B. Restaurer le périmètre** | Porter `dffs` et ses deux garde-fous ; `facilitateur` redevient scopé | Fidélité totale. Coût : une table, deux callbacks, et chaque règle d'autorisation du jeu doit tester le périmètre |
| **C. Hybride (ma recommandation)** | Rôle global pour le **site** (événements, inscriptions, abonnés) ; périmètre par communauté pour les **objets du jeu** (Challenge, Journey, Skill) | Correspond au besoin réel : la billetterie est transverse, le jeu est cloisonné. Coût proche de B, sans compliquer la gestion des événements |

## 5. Recommandation

**Option C**, à mettre en œuvre **avant** le portage des contrôleurs du jeu — après, chaque
règle écrite sur l'hypothèse d'un rôle global devra être reprise.

Question complémentaire pour Boris, qui conditionne le choix : les facilitateurs du Festival
seront-ils rattachés à des **Mondes** distincts (auquel cas le cloisonnement a un sens fort), ou
travailleront-ils tous sur le même périmètre (auquel cas l'option A suffit et il faut alors
supprimer la notion, pas la laisser en jachère) ?

## 6. Autres points de la caractérisation, déjà vérifiés conformes

- Patron « auto-validation Marelle » : les 5 copies sont portées, avec double écriture et
  idempotence. Testé de bout en bout — 12 Oméga attribués, rejeu sans effet, et le
  `create!` direct avec `validated_at` donne bien **zéro** Oméga (preuve que `on_change`
  ignore la création, comme dans la source).
- Les 5 vérifications de parité de `caracterisation-progression-omega.md` §8 passent.
- Recommandation retenue pour plus tard : faire du patron Marelle **un concern partagé**
  (`MarelleValidatable`) plutôt que 5 copies — à faire au portage des contrôleurs, le risque
  de correction partielle étant avéré dans l'historique du projet.
