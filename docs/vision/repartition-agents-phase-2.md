# Répartition des agents — phase 2 (post-portage)

> **v2 — Boris, 2026-08-16.** Révision de la version du 4 août, devenue fausse sur deux points :
> le périmètre du poste fixe s'élargit à l'intégration visuelle du Jeu, et l'état de
> l'application a beaucoup changé. Les règles inchangées sont reprises telles quelles.
> Version de référence, partagée entre agents et postes.

---

## 1. Qui fait quoi

**Poste fixe (Sonnet 5) — intégration visuelle, contenus, prototypes, tests UX.**

Écrit librement dans `zegame-prototypes` et `zegame-docs`.

Dans `pointzero-app` :
- `content/articles/` — les articles de fond en markdown ;
- `app/views/site/` et `public/sas/` — le site public et les parcours publics ;
- **NOUVEAU (16 août)** — `app/views/` et `public/pz/` **pour le Jeu** : le portage strict des
  maquettes, les feuilles de style, le responsive, l'accessibilité.

**Portable (Opus 5 / Fable 5) — fondations, serveur, déploiements.**

Modèles, migrations, services, contrôleurs, routes, droits, configuration serveur, billetterie.
Porte seul la clé SSH et **fait tous les déploiements**. Vérifie en production.

**Principe inchangé, et il vaut dans les deux sens : celui qui produit ne s'auto-valide pas.**

## 2. Ce que le poste fixe n'écrit jamais

Modèles, migrations, services, **contrôleurs et routes**, configuration serveur, billetterie,
gardes et droits.

Cette frontière a été franchie le 16 août (pages du menu de compte : routes et contrôleur créés
côté poste fixe). Ça a fonctionné, mais ce n'est pas la bonne façon. **Le schéma qui marche est
celui de la vague B** : le portable pose la route, la garde et le contrôleur ; le poste fixe
remplit la vue et le style. Si une page à porter réclame une route qui n'existe pas, **demande-la
plutôt que de la créer** — elle sera posée devant toi.

## 3. La règle du portage strict (leçon du 16 août)

**Une maquette validée se PORTE, elle ne se re-dessine pas** — même « en attendant », même « en
version sobre ». Le 16 août, l'accueil du Monde 0 a été livré dans une mise en page inventée
plutôt que dans celle de la maquette : illustrations au-dessus des textes au lieu d'être à
gauche, identités sous les images au lieu d'être par-dessus, boutons rectangulaires et roses au
lieu de ronds et sombres. Il a fallu tout refaire.

En pratique :
1. **Reprendre la structure DOM de la maquette, nom de classe pour nom de classe**, et ses
   valeurs CSS telles quelles. Un diff entre la maquette et l'intégration doit rester lisible.
2. **Tout écart est commenté en tête du fichier**, avec sa raison. Deux écarts sont légitimes par
   nature : le scopage sous une classe racine (l'application charge Bootstrap, la maquette non) et
   le remplacement des polices externes par celles déjà servies.
3. **Vérifier ce que la maquette AFFICHE, pas seulement ce qu'elle déclare.** Exemple vécu :
   `styles.css` importe Libre Caslon Text et DM Sans, mais `m0-typography.css` est chargée après
   et les remplace en `!important` par Roboto Slab et Poppins. Ces deux polices ne sont jamais
   rendues ; les importer aurait été une fidélité de façade.
4. **Le prototype reste la référence figée** : toute évolution se décide dans le prototype puis se
   reporte dans l'application, jamais l'inverse. Signale tout écart que tu constates — le
   prototype fait foi.

## 4. Travailler à deux sur le même serveur

L'arbre `~/src/pointzero-preprod` est **partagé**. Le 16 août, deux chantiers s'y sont
retrouvés mélangés au moment d'un commit et il a fallu trier à la main.

- **Avant tout `git add`, lire `git status --porcelain`.** Jamais de `git add -A` sans avoir
  regardé ce qu'il emporte.
- **Ne commite que tes propres fichiers**, nommément. Si tu vois des fichiers que tu n'as pas
  écrits, laisse-les : ils appartiennent à l'autre instance ou à Boris.
- **Tu produis, le portable déploie.** Ne lance ni `docker compose build`, ni restart.
- Commits préfixés `[Codex]` ou `[Claude]` selon l'agent, avec `Co-Authored-By`.

## 5. Les bancs

`scripts/verifier_*.rb` sont la mémoire des décisions : chacun rejoue un invariant arbitré.

- **Si tu changes un balisage qu'un banc assertait, ajuste le banc dans la même livraison.**
  Cas en cours : `verifier_menu_compte` assertait le bouton du menu de compte que les pages du
  16 août remplacent — il cassera tant qu'il n'est pas repris.
- **Un banc qui ne vérifie que des textes ne protège pas une mise en page.** Celui de l'accueil
  M0 est passé au vert sur une intégration infidèle. Quand tu portes une maquette, ajoute des
  assertions de **structure** : quel bloc contient l'image, quel élément est par-dessus, quelle
  classe porte le bouton.

## 6. Contrat d'intégration des mini-jeux (inchangé)

1. **Dossier autonome** en kebab-case, ouvrable par simple `index.html`.
2. **Aucune dépendance externe** : pas de CDN, pas de framework, pas d'étape de construction.
   CSS en variables personnalisées, polices embarquées localement.
3. Un **`NOTES.md`** documentant : les états simulés, les **données réellement attendues de
   l'application**, les **points de branchement** souhaités, et ce qui est hors périmètre.
4. **Persistance locale décrite explicitement** : clé, schéma, et ce qui ne part jamais au serveur.
5. **Aucune donnée inventée** : un contenu manquant reste visiblement manquant plutôt que comblé.

Le portable branche ensuite routes, comptes, attribution des Ω et validation d'expérience.

## 7. Où en est l'application (16 août)

**Monde 0 — le métaparcours des sept Puissances est en place.** L'accueil `/jeu` sert un deck de
sept cartes, une par Puissance, dont l'état se lit de sept sources réelles (`Monde0Etats`). Deux
états par carte : « à explorer » puis « territoire activé » à la première trace réelle, avec son
badge de seuil. Les sept territoires répondent : `/immateria` (Désir), `/parcours` (Volonté),
`/fresque` (Imagination), `/heros` (Émotion), `/guide` (Communication), `/premieres-cles`
(Intuition), `/users/me` (Transcendance). Navigation par la roue (`_coque_m0`).

**Autres briques livrées depuis le 4 août** : guides LLM (Professeur Sirbey, Docteur Z.E.R.O.),
mentors avec consentement et mémoire, Immateria, page « Mes Traces », seuils et badges,
Espaces de discussion, propositions/décisions/actions avec protocole de consentement, boîte
d'Échanges unifiée, source d'attention unique (F21), menu de compte à routes réelles.

**Doctrine de code à connaître** : un état **se lit, il ne se stocke pas**. Les services
`ExperienceState`, `JourneyProgress`, `Monde0Etats`, `Graine`, `SeuilFranchi` sont des résolveurs
en lecture seule, sans table. Une vue ne doit **jamais** écrire : un GET qui écrit casse le cache.

## 8. Ce qui t'attend

1. **Le portage strict des pages du Monde 0.** Seul l'accueil est aujourd'hui fidèle à sa
   maquette ; les autres territoires sont fonctionnels mais dessinés à la main. Même passe que
   celle faite sur l'accueil, page par page. **C'est la priorité.**

   | Maquette (`zegame-prototypes`) | Page Rails | Puissance |
   |---|---|---|
   | `accueil-puissances-m0-cible` | `/jeu` | — (**fait le 16 août**) |
   | `volonte-marelle-m0-cible` | `/parcours` | Volonté (**fait et validé le 16 août**) |
   | `fresque-recit-m0-cible` | `/fresque` | Imagination (**fait le 16 août** — pont Trace → Graine à arbitrer, voir `pont-trace-graine-fresque.md`) |
   | `heros-mentors-m0-cible` | `/heros` | Émotion — **fait le 17 août** : grille (lot 1) et fiche de détail (lot 2), avec les 48 portraits de Codex. Reste la 3ᵉ vue de la maquette, le **dialogue avec le mentor** (`/mentor`). |
   | `communication-guides-m0-cible` | `/guide` | Communication (**fait le 16 août**) |
   | `premieres-cles-m0-cible` | `/premieres-cles` | Intuition (**fait le 16 août**) |
   | `moteur-conscience-m0-cible` | `/users/me` | Transcendance (**fait le 16 août** — refonte visuelle, pas page nue) |
   | `traces-m0-cible` | `/mes-traces` | transversale — **débloqué** : Boris a tranché le vocabulaire (la Fresque crée les Graines, la page Traces ne convertit rien). Reste à porter. |
   | `accomplissements-m0-cible` | `/accomplissements` | transversale (**fait**, à réaligner sur le patron canonique) |
   | `profil-joueur-cible` | `/users/me` | — · **écartée de cette URL** : le Moteur la prend (arbitrage Boris, 16 août) |

   Le Désir n'a pas de maquette à porter : son territoire **est** le jeu Immateria, déjà intégré.
2. **Les Accomplissements du Monde 0** — page ouvrable immédiatement : `BadgeDeParcours.pour` et
   `SeuilFranchi.pour` sont livrés, avec leurs sceaux. Distinguer badges de parcours (acquisition)
   et badges de seuil (ouverture d'un territoire).
3. **Les pages du menu de compte** — en cours, à terminer avec l'ajustement du banc.

## 9. Arbitrages de Boris à ne pas rouvrir

- **Les Omégas, deux surfaces, deux règles** (précisé le 17 août — un premier report les avait
  confondues) : le **compteur du joueur** est visible à TOUS les Mondes, cliquable, et sa popup
  explique ce qu'il est (« une monnaie qui ne s'échange pas » — contenu en cours de révision
  Boris + Codex). Dans la **messagerie**, l'Ω d'un joueur n'apparaît qu'à partir du Monde 1,
  comme option d'affichage. La transparence du 16 août (annuaire M1 sans opt-in) demeure.
  Les Puissances, elles, restent opt-in — l'asymétrie est voulue.
- **La pastille transversale des guides est dégelée** (Palier 2, 17 août) : elle apparaît dès que
  le joueur est passé par la page de la rubrique Communication, et son déclencheur est le
  marqueur de visite — jamais un réglage. Le visuel du widget revient au poste fixe
  (`guide-widget` de la maquette) ; le branchement conditionnel est en place.
- **Le passage entre Mondes est structurel**, jamais un seuil d'Oméga.
- **Les Omégas acquis restent acquis** : aucune validation ne se révoque.
- **L'accueil est une projection de l'attention** (F21) : à tous les Mondes, une sélection courte
  et nommée, jamais un compteur à vider.
- **Deux états seulement au Monde 0** : à explorer / territoire activé.
