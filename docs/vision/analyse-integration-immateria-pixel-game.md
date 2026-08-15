# Immateria — analyse du prototype pixel game et contrat d'intégration Rails

*Claude (portable), 15 août 2026. Demandée par Boris après livraison du guide LLM (F19
Palier 1) : le prototype `avatar/` (dossier Dropbox, hors dépôt) mène au monde d'Immateria,
l'entrée du territoire **Désir** de la roue des 7 Puissances — le seul des sept encore
raccordé à l'accueil générique faute d'URL stable (constat de la passation Codex du
15 août). Boris produit lui-même les graphismes définitifs ; ce document dit ce qu'est le
prototype, dans quel langage et quel environnement le faire tourner, et comment
l'interfacer à pointzero-app. Il ne construit rien.*

---

## 1. Ce qu'est le prototype

Un jeu **Phaser 3 (3.60.0, chargé par CDN)** en **JavaScript pur, modules ES natifs, sans
framework ni étape de build** — environ 2 100 lignes réparties en cinq scènes
(`BootScene`, `IntroScene`, `CustomizeScene`, `GameScene`, `DungeonScene`) et des
utilitaires de données (`archetypes.js`, `fears.js`, `characterData.js`, `avatarAnim.js`).
Viewport portrait mobile 390×844, `Phaser.Scale.FIT`.

Le parcours joué : saisie du prénom → personnalisation de l'avatar (2 genres, 5 teintes de
peau, coiffures par genre) → dialogue guidé dans une chambre (carte Tiled 32×32) →
questionnaire d'aspirations et de chakras → calcul d'un **archétype** parmi douze
(l'Éteint, le Suradapté, le Protecteur, le Serviteur, le Bâtisseur, le Créateur, le
Passionné, le Leader, l'Influenceur, le Visionnaire, le Chercheur, l'Intégré) → descente
au donjon → identification d'une **peur** → épilogue où l'avatar reçoit la tenue de son
archétype. C'est un tutoriel narratif complet du Désir, pas un mini-jeu décoratif.

Trois faits structurants :

1. **Le pipeline sprites est mûr et documenté** (`avatar/CLAUDE.md`, excellent) :
   spritesheets maîtres 192×1600 px (grille 32×32, 6 colonnes, 48 poses documentées dans
   `Poses.xlsx`), couches corps/coiffure/vêtement dessinées frame par frame
   (pixel-parfait, jamais généré par offsets), scripts Node de déclinaison
   (`generate-lutin.js`, `generate-wizard.js`, codec PNG maison sans dépendance). Les
   graphismes de Boris remplaceront des **fichiers**, pas du code.
2. **La sortie du jeu est déjà de la donnée structurée** :
   `{gender, skin, hair, archetype, fear, aspirations, chakraAnswers}` — envoyée par
   trois `fetch('/api/player')` vers un petit Express (`server.js`, 43 lignes) qui écrit
   dans un `players.json`. Ce backend est un bouchon de prototype, pas une architecture.
3. **Le dossier `deploy/` est déjà pensé pour vivre sous un chemin** :
   `<base href="/jeu/">`, chemins relatifs, 30 Mo d'assets triés (charactersets,
   tilesets, illustrations, badges). Le reste du dossier (`tiled/` = l'éditeur Tiled
   lui-même, 98 Mo ; `psd/` ; `ressources/` = bibliothèques d'images sources) est de
   l'outillage et des sources, pas du livrable.

## 2. Préconisation : rester en Phaser 3 + JavaScript pur, servi statiquement par Rails

**Ne pas changer de langage ni d'environnement.** Le prototype est déjà dans la seule
stack compatible avec la discipline de pointzero-app : l'application est délibérément
sans framework JS (pas de Turbo, pas de Stimulus actif, pas de bundler — formulaires HTML
et `<details>`), et le jeu est autonome dans son canvas. Phaser est une exception bornée :
il vit sur SA page, ne touche ni la coque ni les formulaires, et disparaît quand on
quitte la page. Réécrire en autre chose (Godot/WASM, React, Turbo) serait du travail pur
sans gain, et casserait la référence visuelle.

L'intégration tient en trois mouvements :

### 2.1 Les fichiers — `public/pz/immateria/` de pointzero-app

Le contenu de `deploy/` (index, css, js, assets, maps) se copie sous
`public/pz/immateria/`, servi statiquement comme les assets m0 et le Sas. Zéro process
Node en production — l'Express de dev ne servait que les fichiers et le bouchon JSON.
Deux ajustements au passage :

- **vendorer `phaser.min.js` en local** (actuellement CDN jsdelivr) — même règle de
  résilience réseau que tout le reste de l'application le jour du Festival ;
- **auto-héberger la police** (actuellement Google Fonts) — même raison, plus la
  confidentialité ;
- la carte Tiled peut redevenir un chargement `tilemapTiledJSON` normal : l'astuce
  `chambre.js`/`window.CHAMBRE_MAP` ne servait qu'à contourner le blocage `file://` de
  Firefox, sans objet une fois servie par Rails en même origine.

### 2.2 La persistance — le modèle `Trace`, déjà en place

C'est le point élégant : Intuition écrit `Trace(territoire: "intuition")`, Imagination
`Trace(territoire: "imagination")` — le pixel game est le territoire **Désir** et écrit
sa Trace par le même canal :

```ruby
Trace(user:, territoire: "desir", cle: "immateria",
      reponses: {archetype:, fear:, aspirations:, chakras:,
                 avatar: {gender:, skin:, hair:}})
```

Les trois `fetch('/api/player')` deviennent un unique `POST /immateria/trace` vers un
petit contrôleur Rails (`authenticate_user!` ; jeton CSRF lu dans la balise
`<meta name="csrf-token">` et envoyé en en-tête `X-CSRF-Token` — patron déjà éprouvé).
Plus de `players.json`, plus d'identifiant joueur côté client : `current_user` fait foi.
Conséquences gratuites : l'avatar et l'archétype apparaissent sur `/users/me` et dans
`/mes-traces` sans code supplémentaire, et `Trace#chemin_de_relecture` sait renvoyer vers
`/immateria` pour rejouer.

### 2.3 La navigation — l'URL stable qui manquait

Une route `get "immateria" => "immateria#show"` avec une vue quasi-nue qui charge le jeu
(compte requis), et la roue des 7 Puissances de `_coque_m0.html.haml` raccorde enfin
**Désir → `/immateria`** au lieu de l'accueil générique. C'est précisément le point 3 de
la liste de reprise de la passation Codex du 15 août (« raccorder l'entrée Désir à l'URL
stable d'Immateria »).

## 3. Points d'attention

- **Assets sous licence** : les tenues d'archétype référencent un pack acheté
  (`Base_character_Male_King_Cloak`, etc.). Sans objet à terme (Boris redessine tout),
  mais à garder en tête si une version intermédiaire devait être visible publiquement.
- **Mobile d'abord** : le viewport 390×844 est portrait. La page Rails devra assumer ce
  format sur desktop (jeu centré, fond sobre) plutôt que de l'étirer.
- **Les graphismes se remplacent sans toucher au code** : le format des sheets
  (192×1600, 48 lignes, `Poses.xlsx` comme référence) est le contrat entre les dessins
  de Boris et le moteur. Tant que ce format tient, l'intégration Rails peut se faire
  AVANT les graphismes finaux, et les fichiers se remplacent ensuite un à un.
- **Répartition phase 2 inchangée** : le prototype (et les graphismes de Boris) restent
  la référence visuelle figée ; le portable branche côté Rails (contrôleur, route,
  portage de `deploy/`) ; rien de tout cela ne touche les zones du poste fixe.

## 4. Arbitrages de Boris (15 août 2026)

Les trois questions ouvertes ont été tranchées le jour même :

1. **Nom d'avatar distinct, choisi EN FIN de tutoriel.** L'écran d'intro du prototype
   (saisie du prénom avant de jouer) disparaît dans l'app : `current_user` porte déjà un
   prénom, le jeu démarre directement. Au terme du tutoriel, un écran propose de garder
   son prénom réel ou de nommer son avatar différemment — le nom d'avatar est un fruit du
   parcours, pas un préalable. Il se range dans la Trace
   (`reponses.avatar.nom`).
2. **Le rejeu écrase.** Patron `find_or_initialize_by` des autres territoires : une Trace
   est un état, pas un journal. Rejouer Immateria réactualise l'archétype, la peur et
   l'avatar.
3. **« Puissances » est le vocabulaire canon.** Le portage Rails remplace « chakras »
   partout dans les textes du jeu (les six de `CHAKRA_LABELS` recouvrent les Puissances) ;
   le prototype `avatar/` suivra au rythme de Boris, l'app n'attend pas.

## 5. Socle livré (Claude portable, 15 août au soir) — corrections et contrat

Le socle Rails est en préprod (`zegame-app`, branche `preprod`, commit `6d4eaac`).
L'exploration approfondie du code pendant le chantier corrige trois points du §1-2 :

1. **`deploy/` est un artefact cassé** : son `js/` est vide (le build réel de `deploy.ps1`
   va dans `%TEMP%`, pas dans `deploy/`). La source intégrée est **`public/`** (index,
   css, js, maps) ; seuls les **assets** viennent de `deploy/assets/` (sous-ensemble trié,
   30 Mo, vérifié complet contre les chargements de `BootScene.js`).
2. **Aucun texte « chakra » n'est visible par le joueur** — uniquement des identifiants
   internes (variables, ids DOM, sélecteurs CSS). Les libellés affichés sont déjà les
   Puissances (`CHAKRA_LABELS`). L'arbitrage vocabulaire n'exige donc AUCUNE réécriture
   de texte ; renommer les identifiants reste une affaire de propreté, pour la passe
   prototype.
3. **La sortie du jeu pointait vers l'ancien serveur** (`app.ze.game/journeys/...`) —
   réécrite vers `/jeu`. Le hook `CustomEvent pointzero:goto-monde0` du prototype reste
   émis avant la redirection.

**Le contrat de persistance, pour la passe de refonte du flux** (Boris + Codex) :

- `GET /immateria` — la page du jeu, compte requis (jamais un fichier statique : c'est la
  vue Rails qui porte l'authentification et le `<meta csrf-token>`).
- `POST /immateria/trace` — JSON, en-tête `X-CSRF-Token` lu dans le `<meta>`. Liste
  blanche : `name, gender, charKey, hairKey, archetype, fear, avatarName` (scalaires),
  `aspirations, answers` (tableaux), `scores, fearScores` (objets). Toute autre clé est
  ignorée sans erreur. Chaque POST **fusionne** dans l'unique
  `Trace(territoire: "desir", cle: "immateria")` du joueur — le jeu peut poster autant de
  fois qu'il veut, quand il veut ; le rejeu écrase clé par clé. `avatarName` est déjà
  admis pour le futur écran de nommage.
- L'endpoint **tolère les POST concurrents** : le prototype actuel attache deux écouteurs
  au bouton du prénom (submit + click), un seul geste part en deux requêtes simultanées —
  invisible sur le `players.json` du prototype, fatal contre l'index unique de `traces`
  sans le `retry` ajouté côté serveur. La passe de refonte peut corriger le double
  écouteur, mais le serveur n'en dépend plus.

Assets servis sous `/pz/immateria/assets/…`, Phaser 3.60 vendoré
(`/pz/immateria/phaser.min.js`), Nunito auto-hébergée — plus aucune dépendance CDN. La
roue des 7 Puissances pointe désormais Désir → `/immateria` (le point 3 de la reprise du
15 août est fermé). Banc : `scripts/verifier_immateria.rb`.
