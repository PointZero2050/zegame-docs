# Analyse d'impact — les Guides passent dans Intuition, et gagnent un historique

> **Claude (portable), 2026-08-20.** Demandée par
> [`guides-intuition-metaparcours-badges.md`](guides-intuition-metaparcours-badges.md) §6
> (« Avant implémentation, compléter la matrice ») et par son en-tête (« doit faire l'objet
> d'une analyse d'impact avant portage »). Établie sur `pointzero-app` à `6a48967`, code lu,
> pas supposé.
>
> **Amendement Codex — 2026-08-20, arbitrage Boris.** La partie badges du §2.4 est remplacée
> par la décision canonique de
> [`guides-intuition-metaparcours-badges.md`](guides-intuition-metaparcours-badges.md) :
> **Présence choisie** devient le seuil Communication à la confirmation du Profil, et
> **Première clé de discernement** le seuil Intuition au premier échange Guide complet. Le
> constat technique sur le seuil livré **Dialogue ouvert** reste valide et impose la migration
> non destructive décrite ci-dessous.

## 1. La conclusion d'abord

L'amendement contient **deux chantiers de tailles très différentes**, et les mélanger ferait
attendre le petit derrière le grand :

| | Ce que c'est | Coût | Risque |
|---|---|---:|---|
| **A. Le déménagement** | Les Guides quittent Communication pour Intuition ; les deux métaparcours se réordonnent | **faible** — config + deux conditions de lecture | **faible**, et surtout REVERSIBLE |
| **B. L'historique multiple** | Une table de conversations, archivage, suppression par fil, titres | **moyen** — table, routes, droits, export | **plus faible qu'attendu** : mesuré, il n'y a **rien à migrer** (§3.3) |

**Recommandation : livrer A maintenant, instruire B.** A ne dépend pas de B. La séquence
visible par le Joueur — Communication qui commence par le Profil, Intuition qui commence par
les Guides — est ce que Boris et Codex viennent de décider ; elle n'a pas besoin d'attendre
une refonte du stockage.

## 2. Chantier A — le déménagement

### 2.1. Ce qui existe déjà et qu'il ne faut PAS refaire

L'événement que Codex recommande de créer (`first_guide_exchange_completed_at`, §4.2)
**existe déjà** : le marqueur `m0-dialogue-guides`, posé par `GuidesController#creer` — donc
après un échange réellement abouti, jamais sur une visite. Il est idempotent par construction
(`MarqueurDAttention` a une contrainte d'unicité sur `[user_id, cle]`).

Ajouter une colonne `first_guide_exchange_completed_at` dupliquerait cet état dans une seconde
source, avec le risque classique de divergence. **La doctrine du dépôt s'y oppose** : un état
se lit, il ne se stocke pas. Le marqueur change de territoire, pas de nature.

### 2.2. Les deux lignes qui portent tout le déménagement

`app/services/monde_0_etats.rb`, résolveur d'activation :

```ruby
when "communication" then marqueurs.key?("m0-dialogue-guides")   # ← devient faux
when "intuition"     then cles_assimilees.positive?              # ← devient incomplet
```

Cible :

```ruby
# Communication commence quand le Joueur choisit ce qu'il rend visible
# (Codex §3.2), puis entre réellement en relation.
when "communication" then marqueurs.key?("m0-visibilite-confirmee") ||
                          espace_du_seuil_rejoint?
# Intuition commence au premier échange abouti avec un Guide (Codex §3.1),
# sans retirer l'ancienne porte : un joueur venu par les clés garde la sienne.
when "intuition" then marqueurs.key?("m0-dialogue-guides") || cles_assimilees.positive?
```

⚠️ **Le second terme n'est pas décoratif.** Sans lui, tout joueur ayant assimilé des clés
sans avoir parlé aux Guides verrait sa carte Intuition s'éteindre — un territoire acquis se
reprendrait. C'est la même exigence de monotonie que pour Imagination. Depuis l'arbitrage du
24 août, son prédicat doit reconnaître la première Graine canonique du Joueur, y compris la
Graine de l'Appel dans un fil `ChallengesUser` ; l'ancien
`Graine.au_moins_une_de_fresque?` limité au fil `User` ne suffit plus.

Symétriquement pour Communication : un joueur ayant dialogué avec les Guides mais rien
configuré verrait sa carte s'éteindre.

**Mesuré en production, et le chiffre est décisif :**

```text
joueurs ayant dialogué avec un Guide      : 0
…dont aucune confirmation de visibilité   : 0   ← personne ne perdrait Communication
joueurs ayant assimilé des clés Intuition : 0
…dont aucun dialogue Guide                : 0   ← personne ne perdrait Intuition
```

**Aucun joueur réel n'est affecté par la bascule.** Les deux `||` de compatibilité restent
à écrire — ils ne protègent personne aujourd'hui, ils protègent le joueur de demain qui
entrera par une porte plutôt que l'autre. Mais aucune reprise de données n'est nécessaire.

### 2.3. Les destinations à réordonner

`config/monde_0.yml`. Structure cible, d'après Codex §3.1 et §3.2 :

| Territoire | Base | Destinations, dans l'ordre |
|---|---|---|
| **Communication** | Profil communautaire | Espace d'échange · Annuaire |
| **Intuition** | Guides | Point Zéro (clés) · Ressources · Événements — ~~Observatoire~~ hors M0 |

Les conditions correspondantes existent **toutes déjà**, posées ces deux derniers jours :
`visibilite_confirmee`, `espace_du_seuil_rejoint`, et le marqueur des Guides. Aucune
condition nouvelle n'est à écrire pour A.

**Une seule réserve reste à lever avant de toucher le YAML :**

1. ~~**L'Observatoire n'existe pas**~~ — **tranché par Boris le 20 août : « pas un sujet
   M0 »**. Il sort de la liste M0 (Guides · Point Zéro · Ressources externes · Événements) et
   reste dans la ventilation cible de Codex pour les Mondes suivants. Sans cette décision, il
   aurait de toute façon été refusé par le résolveur : une destination sans `chemin` n'est pas
   accessible (garde du 19 août).
2. **Les libellés sont éditoriaux, donc à Codex.** La carte Communication s'intitule
   aujourd'hui « Rencontre les deux guides du Jeu » avec l'accroche qui va avec ; sa base
   devient le Profil. Le titre, l'accroche, le CTA et le badge de la carte doivent être
   réécrits — **je ne les invente pas**. Idem pour Intuition, dont la base passe de la
   Ressourcerie aux Guides.

### 2.4. Ce que le déménagement ne touche PAS

- **Pas de double sceau.** L’audit ne trouve aucun détenteur réel de **Dialogue ouvert** : il peut
  sortir du catalogue actif. Si un détenteur apparaissait avant la bascule, l’ancien sceau vaudrait
  équivalence du seuil Intuition et empêcherait l’affichage simultané du nouveau.
- **Aucun Oméga.** Les entrées du catalogue des seuils ne portent aucun montant ; le banc doit
  conserver cette garantie structurelle.
- **Clé conservée.** La première clé devient une étape avec Trace, pas un second seuil Intuition.
  Auditer ses détenteurs avant de le sortir du catalogue actif ou de le conserver comme acquis
  historique hors constellation.
- **Première grammaire acquise.** Il reste conditionné aux dix clés, mais relève désormais des
  accomplissements d'appropriation plutôt que du seuil d'entrée dans Intuition.
- **Aucune donnée.** `GuideMessage`, `GuideAppel`, `AutorisationLlm` sont inchangés.
- **La pastille.** Elle est déjà transversale (`_pastille_guides`), rendue par le layout : elle
  ne dépend d'aucun territoire. Son déplacement est donc **déjà fait**, sans le savoir.

Le portage doit donc auditer `config/seuils.yml`, `GuidesController`, `Monde0Etats` et l'événement
de confirmation du Profil dans une même livraison. Il doit distinguer lecture d'un état existant,
affichage d'un badge, équivalence historique et comptage dans la constellation.

## 3. Chantier B — l'historique multiple

### 3.1. L'état des lieux, mesuré

`GuideMessage` : `id · user_id · role · voix · contenu · created_at · updated_at`.
**Un seul fil par joueur**, matérialisé par le scope `fil_de(user)` — il n'y a pas de
colonne de conversation.

**En production : 0 ligne, 0 joueur.** (4 lignes en préprod, toutes issues de bancs.)
Personne n'a jamais parlé aux Guides sur l'application réelle.

Six consommateurs, tous à revoir : `guides_controller`, `guide_reponse` (la fenêtre de
mémoire `messages_pour_api`), `centre_de_personnalisation` (le geste de suppression),
`guides/new`, `_pastille_guides`, et trois bancs.

### 3.2. Ce que la cible exige, et ce que ça coûte

| Exigence Codex | Impact réel |
|---|---|
| Historique de conversations | table `guide_conversations` + FK sur `guide_messages` (nullable puis NOT NULL après reprise) |
| Titre automatique modifiable | colonne `titre`, et **un appel LLM de plus** si le titre est généré — à chiffrer dans `PlafondLlm` |
| Archivage ≠ suppression | `archivee_le` (nullable) — un archivage n'efface rien |
| Suppression par fil | la route actuelle `DELETE /guide/fil` efface **tout** ; elle devient `DELETE /guide/conversations/:id`, et l'ancienne doit rester (« tout effacer ») |
| Bascule dans le même fil | **déjà acquis** — le rôle `bascule` existe et la césure ne part jamais au modèle |
| Sources publiques | `GuideReponse` peut demander des citations dans le texte ; aucun champ séparé ne sait aujourd’hui identifier les documents réellement mobilisés. Un affichage structuré exige un futur suivi de citations côté serveur. |

### 3.3. Les trois points durs, qui ne sont pas techniques

1. ~~**La migration du fil existant**~~ (Codex §5.1) — **ce point dur n'existe pas.**
   Aucun fil à reprendre : zéro ligne en production. La migration se réduit à créer la table.
   C'est le même cadeau que « zéro consentement en production » pour la Personnalisation le
   18 août : la cible peut être construite proprement, sans compromis d'héritage. **Écrire
   quand même la reprise idempotente** — entre cette analyse et le portage, quelqu'un aura
   peut-être parlé à un Guide.
2. **La suppression de compte.** `User has_many :guide_messages, dependent: :delete_all` —
   c'est le correctif d'un défaut RÉEL trouvé le 18 août (une clé étrangère bloquait la
   suppression d'un compte). La table de conversations devra recevoir le même traitement, et
   **le banc de suppression de compte devra être rejoué**, sinon on réintroduit exactement le
   défaut qu'on a corrigé.
3. **L'export et la politique de conservation.** Codex demande d'aligner « export, suppression
   du compte, sauvegardes et journalisation ». L'export n'existe pas aujourd'hui ; la
   politique de rotation des sauvegardes est une dette déjà ouverte (passation). **Ces deux
   points ne sont pas un préalable au déménagement A**, mais ils sont un préalable à
   l'activation de l'historique multiple.

### 3.4. Le piège à nommer

Codex §2.2 : « La bulle est un raccourci vers le même système, jamais une seconde
messagerie. » C'est le risque principal du chantier B, et il est architectural : la page et la
bulle doivent lire et écrire **le même modèle**, sinon on obtient deux fils qui divergent.
Le critère d'acceptation 2 de Codex le dit ; il se vérifie par un banc qui **écrit dans l'une
et relit dans l'autre**, pas par une revue de code.

## 4. Ce qui était à décider — trois réponses de Boris, 20 août

| Question | Réponse |
|---|---|
| L'Observatoire dans le sous-menu Intuition | **« Pas un sujet M0 »** — retiré. La liste M0 devient Guides · Point Zéro · Ressources externes · Événements |
| Le titre automatique des conversations | **Généré** (LLM) — voir §4.1, il a un coût et une condition |
| La conservation d'une conversation | **Illimitée jusqu'à suppression par le Joueur**, « comme une interface LLM habituelle » — voir §4.2 |
| Les libellés des cartes Communication et Intuition | **toujours ouvert — Codex**, seul blocage du chantier A |

### 4.1. Le titre généré : une dépense, et une règle de dégradation

Un titre généré, c'est **un appel LLM de plus par conversation neuve**. Trois conséquences à
tenir dès la conception, sans quoi elles se découvriront en production :

1. il compte dans `PlafondLlm` — le plafond de 20 $/jour est **partagé préprod/production**,
   et son relèvement est une décision reportée (passation) ;
2. **le titre ne doit JAMAIS bloquer la conversation.** Si l'appel échoue, si le plafond est
   atteint ou si le modèle tarde, la conversation s'ouvre quand même avec un titre dérivé du
   premier message. Un titre est un confort ; le dialogue est le service ;
3. il se génère **une fois**, à la première réponse, jamais à chaque message — et il reste
   modifiable à la main (Codex §2.1), donc une régénération écraserait un choix du Joueur.

### 4.2. La conservation : la décision CONFIRME ce qui existe

« Illimitée jusqu'à suppression par le Joueur » est exactement la politique déjà arrêtée par
Codex le 18 août (`9a37aed` : conservation sans expiration propre pendant la durée du compte,
suppression à la main du Joueur ou avec son compte). **Rien à construire de ce côté** : le
code l'applique déjà — `DELETE /guide/fil` pour le geste volontaire, et
`has_many :guide_messages, dependent: :delete_all` pour la suppression du compte.

Le seul ajout du chantier B est la **granularité** : supprimer *une* conversation plutôt que
tout le fil. L'ancienne route reste — « tout effacer » doit rester possible en un geste.

## 5. Ce que je propose

1. **Livrer A** dès que Codex fournit les libellés — c'est désormais le **seul** blocage, les
   trois autres décisions étant prises. Deux conditions, un YAML, les bancs de la carte qui
   suivent dans la même livraison. Une demi-journée, réversible.
2. **B est moins cher qu'annoncé.** Sans reprise de données, il redevient un chantier
   ordinaire : une table, des routes, des droits, des bancs. Il reste soumis aux quatre
   décisions du §4 et il n'est pas urgent — le fil unique fonctionne. Mais l'argument « c'est
   risqué » ne tient plus, et **la fenêtre est maintenant** : chaque semaine de plus est une
   chance qu'un vrai joueur écrive dans l'ancien modèle et fasse renaître la reprise.
3. **La vérification de compatibilité est faite** (§2.2) : personne n'est affecté. À refaire
   juste avant la bascule si des semaines passent — un chiffre ne vaut que daté.
