# Promotion en production — plan d'exécution

> **Claude (portable), 17 août 2026.** Établi à la demande de Boris. La production sert
> **31 joueurs réels et 927 Ω**, sur du code du 12 août : tout le Monde 0 — métaparcours,
> guides, mentors, Immateria, Fresque, seuils, portages stricts — n'existe qu'en préprod.
> À six semaines du Festival, c'est l'écart le plus lourd du projet.
>
> Ce document est une **liste de contrôle exécutable**, pas une note d'intention. Chaque
> constat ci-dessous a été vérifié sur le serveur, pas déduit.

## 1. L'état réel des deux branches

| | Branche | Position | Date |
|---|---|---|---|
| Production | `main` | `0b266b6` | 12 août |
| Préprod | `preprod` | 143 commits d'avance | 17 août |

**Les branches ont divergé** : la prod porte 78 commits absents de préprod, ce qui interdit une
avance rapide. C'est le point qui rendait la promotion risquée — mais l'examen du CONTENU le
désamorce :

- **265 fichiers** existent en préprod et manquent à la prod (tout le Monde 0) ;
- **2 fichiers seulement** existent en prod et pas en préprod : `app/views/users/_stats.html.haml`
  et `app/views/users/stats.html.haml` — **supprimés volontairement** par le poste fixe
  (« Le Carnet de bord disparaît, sa matière propre rejoint Mes Traces »).

**Conclusion : la préprod est un sur-ensemble de la production.** Les 78 commits divergents sont
de l'histoire parallèle, pas du travail perdu — leur contenu a été refait ou dépassé côté préprod.
Rien à sauver, à la seule exception des deux fichiers ci-dessus, dont la suppression est un choix.

## 2. Deux prérequis, à traiter AVANT d'ouvrir la fenêtre

### 2.1 La clé LLM n'existe pas en production

`ANTHROPIC_API_KEY` est **présente en préprod, absente en prod**. Sans elle, les guides
(Professeur Sirbey, Docteur Z.E.R.O.) et les mentors ne fonctionnent pas.

Ce n'est **pas** un risque de plantage : `GuideReponse` porte un `rescue StandardError` délibéré
qui renvoie `statut: "panne"` et affiche un repli vers l'Aide. La page ne casse pas — mais la
fonctionnalité est morte, et un joueur du Festival qui écrit à un guide n'obtiendra rien.

**À faire** : poser la clé dans l'environnement de prod (`~/deploy/compose.yml`), et vérifier que
`PlafondLlm` a son plafond journalier réglé pour la production — la préprod tourne avec un
plafond de test.

### 2.2 ~~L'anomalie des Omégas~~ — levée le 17 août, la production est saine

**Ce prérequis n'en est plus un, et l'alerte initiale était fausse.** Je l'avais formulée à
partir d'un seul compte — `demo@preprod.local`, qui portait 97 Ω pour une expérience en valant 9 —
et j'en avais conclu que « le total est faux pour les joueurs migrés ». C'était une généralisation,
pas un constat.

Vérification faite sur les **deux** bases, en comptant les lignes `Point` en doublon sur un même
triplet (joueur, expérience, compétence) :

| | Triplets en doublon | Joueurs touchés | Ω en trop |
|---|---:|---:|---:|
| Production | **0** | **0** | **0** |
| Préprod | 1 | 1 (compte de démonstration) | 88 |

**La production est intacte : ses 927 Ω sont tous légitimes.** L'unique doublon vivait en préprod,
sur un compte de test, et a été retiré le 17 août — la ligne conforme au barème (3 Ω) conservée,
la ligne surnuméraire (88 Ω) supprimée.

Rien à faire côté production, ni avant ni après la promotion.

> **Ce que cet épisode apprend.** Un chiffre relevé sur un compte de démonstration ne dit rien de
> la production. La règle qui aurait évité l'erreur : quand un constat porte sur des données,
> le vérifier sur la base concernée avant de le nommer — surtout s'il conduit à toucher aux Ω de
> vraies personnes.

## 3. Stratégie de fusion

L'avance rapide est impossible et un `merge` ordinaire produirait des dizaines de conflits sans
valeur (la prod n'a rien à apporter). La voie sûre :

```bash
git checkout main
git merge origin/preprod -X theirs        # préprod tranche tous les conflits
```

**Puis vérifier que l'arbre obtenu est exactement celui de la préprod** — c'est le contrôle qui
transforme une stratégie en garantie :

```bash
git diff --stat origin/preprod HEAD        # doit être VIDE
```

S'il ne l'est pas, ne pas déployer : `-X theirs` n'agit que sur les conflits, un fichier modifié
d'un seul côté est conservé tel quel. Les deux fichiers `stats` reviendront ainsi — **il faut les
supprimer explicitement** pour retrouver l'état voulu.

## 4. Déroulé

1. **Sauvegarde base** — convention du serveur : `~/sauvegardes/avant-monde-0-<date>.sql.gz`.
2. **Sauvegarde code** — `tar` du répertoire `~/src/pointzero-app` (précédent : `ux-cible-avant-*.tgz`).
3. **Vérifier l'arbre propre** — `git status --porcelain` doit être vide côté prod.
4. **Fusionner** puis **contrôler l'égalité des arbres** (§3), et retirer les deux fichiers `stats`.
5. **Poser la clé LLM** (§2.1) si la décision est de l'activer.
6. **Construire** : `cd ~/deploy && docker compose build web`.
7. **Migrer** — cinq migrations en attente, toutes **additives** (aucune suppression de colonne) :
   `creer_traces`, `creer_guide_appels`, `creer_consentements_llm`, `creer_mentor_messages`,
   `add_visibilite_accomplissements_to_users`.
8. **Démarrer, puis REDÉMARRER une seconde fois.** Non négociable : les configurations sont
   mémoïsées en ivar de classe, **`nil` compris** — `mondes.yml`, `seuils.yml`, `coque.yml`,
   `monde_0.yml`, `monde_1.yml`, `journeys/*.yml`, `ressources/guides.yml`, plus `MoteurHelper`.
   Sans ce second redémarrage, la Marelle repart sans puissance ni métriques et les guides sans
   éditorial — **en silence**, ce qui est le pire des cas.
9. **Rejouer la donnée qui n'est pas dans le code** : la durée de
   `le-point-zero-entrer-dans-le-jeu` doit valoir **10 minutes** (et non 7) pour que le parcours
   fasse 6 h 30. C'est la seule écriture hors code de la livraison.

## 5. Vérifications, dans cet ordre

**Par les bancs**, sur la base de production, **en les espaçant de quelques secondes** — dix-sept
démarrages Rails d'affilée épuisent la mémoire du serveur et produisent de faux négatifs :

`verifier_intensites` (390 min, 12 obligatoires, 2 optionnelles) · `verifier_accueil_m0` ·
`verifier_illustrations_m0` · `verifier_marelle` · `verifier_graine` ·
`verifier_fresque_graines` · `verifier_attention` · `verifier_menu_compte` ·
`verifier_monde_1_etats`.

**Au navigateur, sur un compte jetable — jamais sur un compte réel** : l'accueil des 7 Puissances,
une carte activée avec son badge, la Marelle, un guide (repli propre si la clé n'est pas posée),
et `/users/me`.

**Sur les données réelles, sans rien écrire** : les 31 comptes répondent, les 927 Ω sont
inchangés, aucun joueur n'a perdu de validation.

## 6. Retour arrière

`git reset --hard 0b266b6`, reconstruire, restaurer la base depuis la sauvegarde de l'étape 1.

**Les cinq migrations étant additives, la base restaurée reste compatible avec l'ancien code** :
les tables ajoutées deviennent simplement inutilisées. C'est ce qui rend ce retour arrière sûr, et
c'est pourquoi il faut vérifier ce caractère additif avant de partir (étape 7).

## 7. Ce qui ne part PAS dans cette promotion

- Le **portage strict de l'accueil M1** et la vue de la Fresque rebranchée sur la création de
  Graines : chantiers ouverts du poste fixe.
- Le **contrat de remontée d'activité d'Immateria** (Boris + Codex) : la carte Désir reste sur son
  illustration, sans résumé vivant.
- Le **nettoyage des Ω** (§2.2), si Boris le veut séparé.

## 8. Recommandation

**Promouvoir tôt, et en une fois.** L'analyse ci-dessus montre que le risque n'est pas dans le
volume — 143 commits d'un sur-ensemble cohérent, cinq migrations additives — mais dans les
silences : le second redémarrage, la clé LLM, la durée à rejouer. Ce sont trois gestes explicites,
et ils sont dans la liste.

Découper la promotion en tranches serait plus risqué, pas moins : les branches divergeraient
davantage, et chaque tranche partielle laisserait l'application dans un état que personne n'a
vérifié.
