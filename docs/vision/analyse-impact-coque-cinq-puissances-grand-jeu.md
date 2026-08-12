# Coque des cinq Puissances + Grand Jeu — analyse d'impact sur l'existant

*Claude (portable), 12 août 2026. Réponse au bloc canonique de Codex du même jour
(`5bf587c` : [coque-cinq-puissances.md](coque-cinq-puissances.md) et
[grand-jeu-monde-miroir-cible.md](grand-jeu-monde-miroir-cible.md)), et au critère
d'acceptation §8.8 de la coque : « toute modification du registre réel `config/coque.yml`
fait l'objet d'une analyse d'impact et d'une recette de navigation avant portage ».
Cadre posé par Boris : rien de ce qui est développé en août n'est rendu visible pour le
Festival, qui a déjà ses fonctionnalités-cœur.*

---

## 0. Le verdict d'ensemble

**La coque des cinq verbes est une évolution bon marché, parce que le portage du 12 août
a été construit exactement pour ça.** Les identifiants de portes (`aujourdhui`, `chemin`,
`liens`, `agir`, `moi`) sont des clés stables du registre ; les libellés sont des données.
Renommer les cinq portes est une édition de `config/coque.yml`, pas une refonte. La
correspondance est **1:1, sans division ni fusion** — c'est le cas le plus favorable.

**Le Grand Jeu, lui, n'est pas un chantier Rails.** Le document de Codex le dit lui-même
(§18) : la première étape autorisée est la conception documentaire et un **prototype
autonome** (§15 : Phaser, carte 2D, un village, un avatar). Rien de tout cela ne touche
l'application. Ce qui touchera l'application un jour — Omégas historiques/actifs, mana,
contrat d'événements — est explicitement gardé derrière des analyses d'impact dédiées.

La séparation des deux est la clé de lecture du plan révisé : **la coque v2 est un lot
normal de l'application ; le Grand Jeu est une quatrième chaîne, autonome, qui ne
rejoint les autres qu'à des nœuds nommés.**

---

## 1. Coque v2 — l'écart mesuré entre le registre en production et la cible

### 1.1 Ce qui est un renommage (bon marché)

| Id (stable) | Libellé prod | Libellé cible | Sous-titre hérité |
|---|---|---|---|
| `aujourdhui` | Aujourd'hui | **Discerner** | Aujourd'hui |
| `chemin` | Mon chemin | **Décider** | Mon chemin |
| `liens` | Mes liens | **Relier** | Mes liens |
| `agir` | Agir | **Créer** | Agir |
| `moi` | Moi | **Ressentir** | Moi |

Le registre gagne un champ `sous_titre` par porte (le libellé historique, affiché en
transition), et à terme un `symbole` et une `couleur` par Puissance — dévoilés au Monde 1
selon §6 du document de Codex, ce que la mécanique `ouvre:` existante sait déjà faire.
Deux restarts Puma comme d'habitude (mémoïsation).

**Piège réel de ce renommage, à traiter dans le même lot** : la barre mobile actuelle
utilise « Agir » comme libellé de la porte du milieu et l'option C donne aux Échanges un
FAB central. « Créer » au même emplacement avec le bouton `+` du Désir juste à côté crée
une collision sémantique (« Créer » la porte vs « + » créer quelque chose). C'est une
question de maquette, pas de code — **à trancher dans les maquettes desktop avant
portage**, c'est précisément le genre de chose que la recette de navigation du §8.8 doit
attraper.

### 1.2 Ce qui bouge vraiment : trois destinations changent de porte

Comparaison du registre en production avec la cartographie §3 de Codex :

| Destination | Porte aujourd'hui | Porte cible | Motif |
|---|---|---|---|
| `ressourcerie` | `chemin` | `aujourdhui` (Discerner) | Discerner = « reconnaître les signaux », la Ressourcerie s'y consulte |
| `heros` | `chemin` | `aujourdhui` (Discerner) | Le catalogue se découvre depuis Discerner |
| `agenda` | `liens` | `aujourdhui` (Discerner) | « Actualités et agenda général » |

Tout le reste est déjà au bon endroit : `marelle` et `freeride` sous Décider, `echanges`/
`rendez_vous`/`cercles`/`annuaire` sous Relier, `marche`/`commun` sous Créer, `profil`
sous Ressentir. Trois lignes de YAML à déplacer — mais **les chemins d'URL ne changent
pas** (`/ressources`, `/heros`, `/evenements`), donc aucun lien ne casse : seule la
destbar qui les affiche change de porte.

Attention à un point du registre : `verifier!` impose aujourd'hui *au plus une destination
annoncée par porte et par Monde*. Déplacer trois destinations vers `aujourdhui` peut
violer cette contrainte selon les états — à vérifier au moment du portage, c'est le genre
de chose que le banc `verifier_coque` attrapera.

### 1.3 Ce qui est nouveau (et se phase)

1. **Le bouton `+` du Désir** (§4.1) — la question stable « Que veux-tu mettre en
   mouvement ? » avec des actions contextuelles. Le composeur B3 existe déjà *dans un
   fil* ; ceci est sa généralisation à la coque. C'est le morceau le plus riche de la
   v2 : il demande une maquette (quelles actions, dans quel ordre, selon quel contexte)
   avant tout code.
2. **Le portail du monde-miroir** (Transcendance, §4.2) — au Monde 0, un teasing fermé.
   La mécanique existe intégralement (`/a-venir/:id`, gabarit de teasing, états). C'est
   une entrée de registre + un teaser éditorial. La seule nouveauté structurelle : c'est
   une « porte spéciale, extérieure aux cinq destinations » — la Couronne — donc un
   emplacement de coque à concevoir en maquette (pas un sixième onglet).
3. **La page Omégas transversale** (§5) — nouvelle page, lecture seule au début,
   alimentée par le barème Oméga déjà clarifié. Petite.
4. **Les correspondances symboliques par Monde** (symbole, couleur, question d'usage) —
   données de registre, dévoilées par la mécanique existante.

### 1.4 Le calendrier de visibilité — la contrainte de Boris

Le renommage des portes est **la chose la plus visible qu'on puisse faire à
l'application**. La consigne « rien de visible pour le Festival » se traduit donc
mécaniquement :

- **la coque v2 vit sur préprod** jusqu'au Festival ; `main` n'en reçoit rien avant le
  2 octobre (le gel du 15 septembre l'aurait de toute façon imposé pour la moitié de la
  fenêtre) ;
- l'ordre interne du lot : **maquettes (desktop + Codex) → recette de navigation §8.8 →
  portage préprod → recette croisée → promotion post-Festival** ;
- aucun besoin de *feature flag* : la séparation préprod/prod nous donne déjà les deux
  états, et un flag de coque serait une complexité qu'on paierait deux fois.

---

## 2. Grand Jeu / monde-miroir — ce que ça touche, et surtout ce que ça ne touche pas

### 2.1 Le prototype (§15) est un projet séparé, pas un module Rails

Carte 2D Phaser, un village, un avatar par gabarits, trois PNJ, mana, une expérience
réelle simulée, le Docteur en narrateur. Tout cela vit dans **zegame-prototypes** (la
zone du poste fixe), réutilise le fonds `avatar/` existant (sprites, Tiled, animations —
§16), et se juge sur une seule hypothèse : *le joueur comprend-il que sa transformation
réelle modifie le destin de son double ?*

Trois conséquences de planification :

- **Porteur : le poste fixe** (Phaser = front autonome = sa zone), **récit : Codex**
  (scénario §15, voix du Docteur), **portable : rien au début** — puis le contrat
  d'événements quand le prototype aura prouvé sa boucle.
- **Aucune dépendance vers les chaînes existantes.** Le prototype peut commencer dès que
  les maquettes de coque v2 sont livrées, ou même avant — il n'attend rien de Rails.
- **La validation simulée (§15.7) est le bon choix** : le prototype n'appelle PAS l'app,
  il simule la trace et la reconnaissance. Le jour où on branche pour de vrai, c'est le
  contrat d'événements (§18.3) qui s'écrit — chez moi.

### 2.2 Les six préalables du §18 — qui, quand

| Livrable §18 | Porteur | Quand |
|---|---|---|
| 1. Analyse d'impact progression/Omégas/decay/droits | Portable | Quand le prototype a prouvé la boucle — pas avant : l'analyser à vide, c'est spéculer |
| 2. Modèle de consentement + gouvernance des interprétations LLM | Codex (spec) puis portable (revue) | Avec le 1 |
| 3. Contrat d'événements réel ↔ miroir | Portable | Après le 1 |
| 4. Maquette du teaser Monde 0 | Desktop | **Tout de suite** — c'est une entrée du lot coque v2 |
| 5. Prototype autonome §15 | Desktop + Codex | Dès maintenant, chaîne parallèle |
| 6. Décision d'architecture temps réel / séparation des services | Portable, arbitrage Boris | Après le 5 — l'architecture se décide sur un prototype qui marche |

### 2.3 Deux cohérences à noter (et une consigne pour F19)

**Le Docteur trouve sa place.** Le document canonise le Docteur Z.E.R.O. comme
« narrateur caustique du Grand Jeu », manifestation de l'Ombre du Professeur *révélée au
contact des IA du monde-miroir*. Cela conforte la recommandation de l'analyse F19 rendue
ce matin, et la précise : **le registre caustique appartient au monde-miroir — un espace
explicitement fictionnel où le joueur entre volontairement — pas au guide d'aide du monde
réel.** Le Professeur guide le réel ; le Docteur narre le miroir. Cette ligne de partage
devrait être écrite dans le corpus des guides (palier 0 de F19) pour que les deux voix ne
se contaminent pas.

**Les cinq futurs (§11) sont une petite fonction réelle.** « Lecture actuelle du Jeu —
pression relative des cinq futurs », affichée dès le Monde 0, alimentée éditorialement
(validation humaine obligatoire avant toute insertion LLM). C'est un YAML + une vue dans
Discerner — un lot desktop d'une journée, sans IA au départ. Elle peut entrer dans la
coque v2 sans attendre le Grand Jeu.

**Une incohérence de registre à signaler** : `config/mondes.yml` ne déclare que les
Mondes 0 et 1 — et c'est suffisant pour tout ce bloc (portail teasé au 0, ouvrable au 1).
L'Assemblée intérieure (Monde 3) et les interprétations symboliques (Mondes supérieurs)
ne nécessitent AUCUNE déclaration de Monde aujourd'hui. Ne pas ouvrir le registre des
Mondes en avance : c'est le dévoilement qui commande.

---

## 3. Ce que le plan révisé change (résumé des éditions)

1. **Nouveau lot « Coque v2 : les cinq verbes »** — séquencé maquettes → recette §8.8 →
   portage préprod → promotion post-Festival. Inclut : renommage + sous-titres, les trois
   déplacements de destinations, le portail-teaser du miroir, la page Omégas, les cinq
   futurs v0, et la maquette du bouton `+` (le code du `+` est un lot séparé, plus tard).
2. **Nouvelle CHAÎNE GRAND JEU / MONDE-MIROIR** dans le graphe — autonome, portée
   desktop + Codex, avec les six préalables §18 comme nœuds ; elle ne rejoint la chaîne
   coque qu'au teaser Monde 0, et ne rejoindra Rails qu'au contrat d'événements.
3. **Sprints réagencés à la marge** : le sprint 4 (« portage de la coque ») ayant été
   réalisé avec deux mois d'avance, sa fenêtre d'octobre accueille la coque v2 ; le
   prototype Grand Jeu court en parallèle sans consommer la capacité des chaînes
   existantes côté portable.

Rien d'autre du plan ne bouge : les paliers, la messagerie/objets (chaîne complète), la
méthode et le gel restent tels quels.

---

*Pour Codex et le poste fixe, au moment de traduire en maquettes : les trois questions
que les maquettes doivent trancher sont (a) la collision « Créer »/« + » sur la barre
mobile, (b) l'emplacement de la Couronne (portail miroir) hors des cinq portes, et
(c) les actions du `+` par contexte. Le reste de la coque v2 est du registre, pas du
dessin.*
