# Onboarding Monde 0 — accueil-métaparcours des sept Puissances

> **Ajout Codex — 2026-08-15. Décision de Boris incarnée dans les prototypes.**
> Ce document est la référence d'intégration de la nouvelle coque d'entrée. Il amende
> l'affichage principal décrit dans
> [coque-cinq-puissances.md](coque-cinq-puissances.md) : les cinq intentions restent une
> cartographie fonctionnelle utile, mais la navigation visible et l'accueil du Joueur
> s'organisent désormais autour des **sept Puissances**.

## 1. Décision structurante

L'accueil de l'application est un **métaparcours**. Chaque Puissance est simultanément :

- une carte d'appel sur l'accueil ;
- une entrée de navigation dans la roue des sept Puissances ;
- un territoire fonctionnel qui s'enrichit au fil des Mondes ;
- un seuil pédagogique parcouru selon la boucle `invitation → découverte → appropriation`.

Le Joueur choisit librement ce qui l'appelle. Il n'existe pas d'ordre imposé entre les
sept cartes. Leur état et leur prochain geste rendent néanmoins la progression lisible.

Le Désir et la Transcendance sont distingués comme **Racine** et **Couronne** dans la roue
et dans les cartes, jamais dans la barre compacte. La Transcendance n'est pas une septième
jauge : elle exprime la circulation commune des six autres Puissances.

## 2. Cartographie du Monde 0

| Puissance | Appel initial | Territoire ouvert | État de retour sur l'accueil |
|---|---|---|---|
| **Désir — Je suis** | Créer son jumeau numérique | Immateria, village de départ et premières quêtes solo | Quête en cours, avatar et mana disponible |
| **Volonté — Je décide** | Entrer dans le premier parcours | Marelle et parcours Monde 0 | Parcours, étape active et prochaine action réelle |
| **Imagination — Je crée** | Produire une première Graine | Fresque de Récit, puis Mes Traces | Graines, Résonances, Traces et transformations |
| **Émotion — Je ressens** | Choisir un héros inspirant | Catalogue limité des héros et dialogue avec le mentor | Mentor choisi, échanges et parcours associés |
| **Communication — Je m'exprime** | Rencontrer Sirbey ou Z.E.R.O. | Guides, puis Espace du Seuil | Guides disponibles et aperçu des échanges du Monde 0 |
| **Intuition — Je discerne** | Lire une première clé Point Zéro | Corpus PZ, événements ; ressources externes annoncées | Clés assimilées et Traces de lecture créées |
| **Transcendance — Je donne** | Observer son Moteur | Mon Moteur et Accomplissements | Puissances renseignées, Alchimisation et badges |

### 2.1 Règle d'incrémentation

> **Décision du 16 août 2026 — cette règle remplace le principe antérieur de visuel fixe.**

Une carte d'accueil conserve son **identité de Puissance** — couleur, icône, verbe et place dans
la roue — mais son illustration représente le **seuil fonctionnel actuellement proposé**. Son
contenu et son illustration évoluent ensemble :

1. `À explorer` : un appel, une promesse et un CTA concret ;
2. `Activée` : l'expérience a eu lieu et le territoire montre un usage courant ;
3. `À explorer` à nouveau : une nouvelle page vient de s'ouvrir dans ce territoire ;
4. `Appropriée` : les usages découverts sont résumés par quelques indicateurs intelligibles.

Exemple Imagination : première Graine → retour avec compteurs de Graines et Résonances →
première Trace créée → nouvelle invitation à découvrir `Mes Traces` → carte enrichie avec
Traces et Traces transformées.

Chaque page interne reçoit une illustration propre, dans la grammaire de sa Puissance. Lorsque
cette page devient la destination principale d'une carte au stade `À explorer`, la carte reprend
cette illustration. L'accueil devient ainsi le métaparcours visible du dévoilement : avant même de
lire, le Joueur voit qu'un nouveau territoire vient de s'ouvrir.

Après la première visite, l'illustration reste celle du dernier espace révélé tant qu'aucun seuil
plus récent ne devient prioritaire. Elle ne change pas au gré des notifications, d'un compteur ou
d'une activité ordinaire : seuls une révélation durable et le changement du CTA principal peuvent
la faire évoluer.

Si plusieurs invitations sont simultanément disponibles dans une même Puissance, le résolveur
retient une destination principale de façon déterministe — priorité éditoriale, puis invitation la
plus ancienne non visitée — et indique les autres par un compteur. Il ne compose pas plusieurs
illustrations sur une même carte.

La transition peut être accompagnée d'un fondu ou d'une métamorphose brève, jouée une seule fois
au retour sur l'accueil, avec une variante sans animation lorsque `prefers-reduced-motion` est
activé.

Une carte au stade `À explorer` ou `réouverture` reçoit en outre une **légère surbrillance** :
bordure plus lumineuse, halo très contenu et contraste localement renforcé. Cet appel visuel reste
stable et non pulsé afin de suggérer une possibilité plutôt qu'une urgence. Il disparaît après la
première visite de la destination. Le libellé d'état et le CTA restent indispensables : la couleur
ou la lumière ne portent jamais seules l'information, notamment pour l'accessibilité.

### 2.2 Application rétroactive au Monde 0

| Puissance | Premier visuel proposé | Nouveau visuel lors de la réouverture |
|---|---|---|
| Désir | création du jumeau et village d'Immateria | quête ou espace d'Immateria nouvellement révélé |
| Volonté | entrée dans la Marelle | étape ou parcours qui devient la prochaine invitation |
| Imagination | première Graine et Fresque | `Mes Traces` dès l'apparition de la première Trace |
| Émotion | catalogue des six héros | mentor choisi ou nouvelle page liée au mentor lorsqu'elle devient l'appel principal |
| Communication | rencontre des deux guides | `Espace du Seuil` après le premier dialogue |
| Intuition | dix clés Point Zéro | espace nouvellement ouvert, notamment les ressources externes au Monde 1 |
| Transcendance | Moteur de Conscience | `Accomplissements` lorsque les six Puissances sont renseignées |

Le prototype Monde 0 possède déjà des illustrations spécifiques pour la Fresque et les Traces ;
les autres variantes doivent être produites ou sélectionnées dans la même grammaire avant le
portage Rails. En attendant, l'absence d'un asset ne doit jamais conduire à inventer un état métier
supplémentaire : le CTA et sa destination restent la source du choix visuel.

## 3. Coque commune

La référence exécutable est le lot Monde 0 de
[zegame-prototypes](https://github.com/PointZero2050/zegame-prototypes) :

- `m0-shell.js` : montage des raccourcis communs, routes de la roue, Omégas et compte ;
- `m0-shell.css` et `m0-shell-v2.css` : coque, responsive et animation de la roue ;
- `m0-account.css` : menu technique de l'avatar ;
- `m0-typography.css` : Roboto Slab pour les titres, Poppins pour le corps ;
- `communication-guides-m0-cible/guide-widget.js` : bulle persistante des guides et
  chargement de la coque sur les pages autonomes.

### 3.1 En-tête persistant

De gauche à droite :

1. logo Point Zéro ;
2. bouton explicite `Accueil` ;
3. bouton `7 Puissances`, desktop **et** mobile ;
4. raccourci Échanges avec notifications, après ouverture de l'Espace du Seuil ;
5. pastille Oméga toujours visible ;
6. avatar ouvrant le menu de compte.

Les guides restent dans une bulle flottante en bas à droite après leur découverte. Cette
présence distingue l'aide sur le Jeu des échanges humains.

### 3.2 Roue des sept Puissances

La roue remplace la multiplication des items horizontaux sur tous les écrans. Chaque
Puissance mène directement à son territoire, et non à sa carte sur l'accueil. Le Désir
reste provisoirement relié à l'accueil tant que l'URL d'entrée d'Immateria n'est pas figée.

L'ouverture comporte un voile, une rotation/mise au point de la roue, puis une apparition
radiale séquencée des sept symboles. L'effet est centralisé dans la coque et respecte
`prefers-reduced-motion`.

### 3.3 Menu de compte

Le clic sur l'avatar ouvre une surface strictement technique :

- Paramètres du compte ;
- Connexion & mot de passe ;
- Notifications & rythme ;
- Conditions générales d'utilisation ;
- Se déconnecter.

Le profil communautaire, le chemin et les œuvres n'y figurent pas : ils appartiennent aux
territoires du Jeu. Les liens du prototype sont encore des ancres à raccorder aux routes
Rails.

### 3.4 Pastille Oméga au Monde 0

Le Monde 0 présente un solde unique, sans distinction historique/actif. La fenêtre explique
que l'Oméga est une monnaie non fongible : il ne se donne, ne se dépense et ne s'échange pas.
Il reconnaît la capacité à faire circuler la vie dans les polarités du Moteur et prépare une
gouvernance par domaines de souveraineté.

La ventilation distingue progression dans la Marelle, capacités reconnues, contributions au
Commun et impacts des œuvres/projets. Le million d'Omégas, la part relative du Joueur et le
pouvoir de financement ne sont dévoilés qu'au Monde 1.

## 4. Contrats pédagogiques par territoire

### Désir

Immateria s'ouvre directement sur le premier écran jouable. Le jumeau numérique n'est pas un
questionnaire déclaratif : son comportement et ses quêtes mettent le Joueur en abyme et lui
font rencontrer son Désir. Le Monde 0 se limite au village de départ et à quelques quêtes
solo. L'URL et le contrat d'intégration du pixel game restent à fixer.

### Volonté

Le parcours porte une puissance globale de transformation et d'impact sur **10**. Chaque
expérience porte séparément une intensité pour le Joueur sur **5**, une échelle d'effet sur
**5**, un Monde minimal, une durée, une modalité et des prérequis. Ces mesures décrivent
l'expérience, jamais la valeur du Joueur.

La première expérience articule vidéo, mini-jeu `Le coupable idéal` et cristallisation d'une
Trace. Les CTA décrivent toujours l'action réelle suivante.

### Imagination

La première visite explique la Fresque, les Graines et les Résonances. Un court rituel sur
les récits produit la première Graine. Les Traces ne sont pas un sas obligatoire avant la
Graine : elles sont produites par les expériences et conservées dans une page dédiée. Une
Trace peut être relue, rejouée ou transformée ultérieurement en Graine.

### Émotion

Le Monde 0 rend accessible une figure par Puissance centrale ; la bibliothèque complète est
annoncée pour le Monde 2. Il n'existe pas de héros de Transcendance. Une fiche comporte une
biographie inspirante, une Puissance principale et deux appuis, un lemniscate
Ombre–Source–Lumière, le diptyque relié par le Tao et des parcours associés. Le choix du
mentor est réversible.

### Communication

Le premier geste est un choix entre :

- Professeur Sirbey, regard de la Lumière ;
- Docteur Z.E.R.O., regard de l'Ombre.

Après le premier dialogue, le Joueur découvre l'Espace du Seuil du Monde 0. Il peut lire,
se présenter et faire résonner les Graines. La messagerie complète s'ouvre au Monde 1. Les
guides expliquent le Point Zéro et l'application ; ils ne remplacent ni le mentor personnel,
ni le facilitateur, ni l'aide humaine.

### Intuition

Le corpus Point Zéro et les ressources externes sont deux sous-ensembles de la même
Ressourcerie. Au Monde 0, dix fiches PZ sont visibles. Le Joueur lit d'abord la fiche, puis
répond à trois questions ouvertes ; cette appropriation crée une Trace. Les ressources
externes deviennent automatiquement disponibles au Monde 1, indépendamment du nombre de
clés assimilées. Les événements Point Zéro restent accessibles dès le Monde 0.

### Transcendance

Le Joueur renseigne les six Puissances à partir des questionnaires existants. Le grand Moteur
reprend le fond Ombre/Lumière, le Tao central, le trait plein de l'état observé et les
pointillés du prochain cap. Chaque Puissance mène à sa fiche détaillée.

L'Alchimisation n'apparaît pleinement qu'à `6/6`. Elle est représentée sur dix degrés et
combine circulation et amplitude ; ce n'est jamais une note de valeur. Les Accomplissements
distinguent badges de parcours et badges de seuil, avec visibilité communautaire réglable
par catégorie et activée par défaut.

## 5. Popups de première visite

Chaque nouvelle page affiche automatiquement, une seule fois, une explication suffisamment
substantielle : fonction de la page, place dans le Voyage et prochain geste. Elle reste ensuite
accessible par une aide discrète. Un seul CTA mène à la page ; l'aide ne doit pas offrir deux
sorties concurrentes.

En production, l'état `aide déjà vue` doit être stocké côté utilisateur, pas seulement dans le
navigateur.

## 6. État simulé dans les prototypes

Les clés `localStorage` permettent seulement de jouer les transitions :

| Clé | Rôle simulé |
|---|---|
| `pz_volonte_m0_v1` | étapes du premier parcours |
| `pz_fresque_demo_v1` | Graines, Résonances, Traces et transformation |
| `pz_hero_m0_v1` | héros choisi et nombre d'échanges |
| `pz_communication_demo_v1` | guide choisi, premier dialogue et Espace du Seuil |
| `pz_intuition_m0_v1` | fiches ouvertes, réponses et clés assimilées |
| `pz_moteur_m0_v1` | première lecture des six Puissances |
| `pz_accomplissements_visibility_v1` | visibilité communautaire des badges |

La traduction Rails ne doit pas reproduire ces objets tels quels. Elle doit raccorder les
états aux modèles canoniques, à la progression réelle, aux droits et au moteur de validation.

## 7. Routes des prototypes

| Territoire | Prototype |
|---|---|
| Accueil | `accueil-puissances-m0-cible/` |
| Volonté | `volonte-marelle-m0-cible/` |
| Fresque | `fresque-recit-m0-cible/` |
| Traces | `traces-m0-cible/` |
| Héros | `heros-mentors-m0-cible/` |
| Communication | `communication-guides-m0-cible/` |
| Intuition | `premieres-cles-m0-cible/` |
| Moteur | `moteur-conscience-m0-cible/` |
| Accomplissements | `accomplissements-m0-cible/` |

## 8. Écarts avant traduction Rails

1. Fixer l'URL et la technologie d'Immateria, puis remplacer la route provisoire du Désir.
2. Raccorder les états des cartes à la progression réelle, sans créer un second moteur de
   validation.
3. Réutiliser les questionnaires complets des Puissances et les fiches PZ existantes.
4. Raccorder Fresque, Graines, Résonances et Traces aux modèles qui seront retenus après
   analyse d'impact.
5. Brancher le catalogue réel des héros et conserver `principale + deux appuis`.
6. Implémenter les guides LLM selon l'analyse d'impact dédiée et leurs limites de contexte.
7. Brancher l'Espace du Seuil sur la messagerie réelle et ses règles d'accès.
8. Remplacer les ancres du menu de compte par les routes techniques et juridiques.
9. Alimenter événements et ressources depuis les données réelles au lieu du contenu figé.
10. Préserver la roue, les sous-menus par territoire, les popups initiales et la typographie
    commune lors du portage HAML/Hotwire.

## 9. Recette minimale attendue

- les neuf pages affichent Accueil, 7 Puissances, Omégas et menu de compte sans image cassée ;
- la roue route directement vers les territoires et son animation est rejouable ;
- aucun écran large ou mobile ne déborde horizontalement ;
- la première action significative réactive sa carte d'accueil ;
- une première Trace ouvre `Mes Traces`, sans retirer la Fresque du sous-menu ;
- les ressources externes annoncent une ouverture automatique au Monde 1 ;
- la Transcendance n'est jamais évaluée comme une Puissance indépendante ;
- les guides restent une aide sur le Jeu, distincte du mentor et des échanges humains ;
- les réglages de compte ne dupliquent ni le profil communautaire ni les œuvres.
