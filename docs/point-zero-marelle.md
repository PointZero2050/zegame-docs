# Point Zéro, Marelle Oméga et mondes

> Ajout Codex - 2026-07-11. Première lecture fonctionnelle de `PRT-Le Point Zéro - Livre II.docx`. Cette note distingue les éléments explicitement décrits dans le livre des hypothèses de traduction dans ze.game.

## 1. Vision produit issue du livre

La Marelle Oméga est une école de la Conscience et une méta-architecture initiatique. Elle organise une progression par paliers depuis l'inconscience jusqu'à l'hyperconscience, sans imposer à tous le même degré d'engagement.

Ses principes structurants sont :

- le lancer, qui matérialise une intention souveraine ;
- la case interdite, qui représente un point aveugle révélé par la relation ;
- l'alternance de cases simples et doubles, donc de passages individuels et relationnels ;
- une progression permanente où l'échec produit de l'apprentissage ;
- le recommencement, dans une logique de spirale fractale plutôt que de fin de jeu.

Chaque monde ouvre un catalogue de parcours, pratiques, expériences, formations, rites, communautés et initiatives partenaires. La Marelle donne une grammaire commune à ces éléments sans chercher à remplacer les dispositifs existants.

Le critère de passage central est la sécurité ontologique : capacité à traverser l'incertitude, la remise en question et la désidentification sans désorganisation psychique ni projection violente sur le collectif.

## 2. Progression des mondes explicitement décrite

| Monde | Fonction principale | Formes d'engagement | Passage ou accomplissement |
|---|---|---|---|
| 0 - Terre | Sas d'entrée, mise en résonance, découverte du Point Zéro et premières expériences réflexives | Contenus courts, échanges légers, exploration personnelle | Atelier Point Zéro d'une journée et choix d'un scénario de futur |
| 1 | Découverte du moi face au collectif ; articulation entre besoins individuels et besoins du système | Communauté, événements et constellation de parcours choisis | Mise en récit de soi reliant futur souhaité, récit présent et transformations nécessaires |
| 2 | Entrée dans un cercle de croissance stable de 6 à 8 personnes autour du Voyage du héros | Réunion mensuelle, facilitateur certifié, héros modèles, challenges et projets | Nuit blanche initiatique et épreuves incarnées |
| 3 | Engagement approfondi sur un an et transformation identitaire, relationnelle et professionnelle | Cercle stable, Chrysalides, pratiques profondes et projet à impact | Oeuvre personnelle réelle, soutenue et ritualisée par l'écosystème |
| 4 | Exploration directe de la Conscience et de son langage | Méditation, retraites, immersions ; cercle devenu autonome | Oeuvre collective mobilisant les talents singuliers de l'équipe |
| 5 | Service collectif conscient et incarnation dans la vie quotidienne | Travail de l'Ombre, persona symbolique, communautés de vie ou de service | Parcours initiatique personnalisé sur un an au service d'autres communautés |
| 6 | Construction et mise en réseau de Cités Cosmiques | Service cosmolocal, gouvernance et création communautaire territoriale | Oeuvre collective multi-cercles et multi-territoires, au moins nationale |
| 7 | Fin du parcours humain et entrée consciente dans la dimension cosmique | Présence souveraine dans l'existence ordinaire | Cérémonie-Source, archétype profond et nom véritable |
| 8 et 9 | Non décrits opérationnellement dans la version lue | À définir | À définir |
| 10 | Communion avec la Source et conscience souveraine de son origine divine | Évoqué comme horizon, sans dispositif détaillé | Recommencement fractal du Jeu |

Le livre emploie « 10 mondes » tout en décrivant une échelle allant du Monde 0 au Monde 10, soit onze positions si les deux bornes sont comptées. Cette convention doit être clarifiée avant de figer le modèle de données ou la représentation graphique.

## 3. Traduction fonctionnelle possible dans ze.game

Les éléments ci-dessous sont des hypothèses de conception, pas encore des décisions.

### Articulation entre Mondes et Journeys

Le Monde 0 existe déjà sous la forme d'un Journey prototypé dans ze.game. Cette représentation constitue une base valide pour expérimenter l'expérience et éviter une refonte abstraite prématurée.

À court terme, chaque Monde peut donc être représenté par un Journey, la Marelle servant de navigation entre ces parcours et les rites de passage pouvant prendre la forme de Challenges particuliers.

Un modèle `World` séparé ne devra être introduit que si les besoins réels dépassent clairement les capacités de `Journey`, par exemple lorsqu'un Monde doit contenir plusieurs catalogues, parcours, rites, événements et expériences externes. La hiérarchie cible éventuelle serait alors :

`Marelle -> Monde -> catalogue d'expériences -> Journey -> Challenge`

Le catalogue pourrait référencer des objets internes et externes : parcours ze.game, ateliers, événements, rites, communautés, contenus, retraites ou dispositifs partenaires.

La vision narrative du jumeau numérique et du monde-miroir est documentée séparément dans [vision-monde-miroir.md](vision-monde-miroir.md).

### Plusieurs progressions liées

La progression actuelle est principalement calculée dans un Journey. La Marelle introduit au moins quatre dimensions distinctes :

- avancement dans les parcours et challenges ;
- maturation sur les 7 puissances ;
- posture ou trajectoire identitaire ;
- qualité de contribution à un cercle, une communauté ou l'écosystème.

Ces dimensions ne doivent pas être réduites à un score unique. Certaines sont observables, d'autres déclaratives ou validées par des pairs et facilitateurs.

### Passages entre mondes

Un passage n'est pas un déblocage automatique par points. Il peut combiner prérequis, expérience vécue, production d'une oeuvre, validation collective, cérémonie et décision libre du Joueur. Le système devra donc distinguer :

- l'éligibilité technique ;
- la préparation ressentie par le Joueur ;
- une éventuelle validation par un facilitateur ou un cercle ;
- le passage rituel réellement accompli ;
- la possibilité de recommencer ou d'approfondir sans perdre le chemin parcouru.

### Collectifs durables

À partir du Monde 2, l'équipe stable devient un objet fonctionnel central. La notion actuelle de Communauté paraît trop large pour représenter à elle seule un cercle de 6 à 8 personnes avec cycle, facilitateur, maturité collective, rencontres, oeuvre commune et historique.

Il faudra étudier un objet dédié de type `Circle` ou une spécialisation explicite de `Community`, ainsi que les relations entre Joueurs, facilitateurs, Chrysalides, Cités Cosmiques et territoires.

### Sécurité et éthique

La « sécurité ontologique » ne devrait pas devenir une note psychologique automatisée. Les états sensibles, pratiques thérapeutiques et expériences initiatiques impliquent consentement, confidentialité, limites d'accès, droit au retrait et responsabilité humaine clairement identifiée.

## 4. Impacts design à explorer

- Faire de la Marelle une carte vivante et un repère de navigation, sans transformer l'expérience en tableau de niveaux compétitif.
- Donner à chaque monde une identité visuelle propre tout en maintenant une continuité Point Zéro.
- Montrer simultanément le monde actuel, les espaces accessibles et l'horizon, sans exposer comme des récompenses les passages qui exigent de la maturité.
- Représenter les progressions individuelle, relationnelle et collective sans classement public simpliste.
- Donner une place visible aux rites, oeuvres, cercles et contributions, aujourd'hui absents du vocabulaire principal de l'interface.
- Concevoir mobile d'abord : la Marelle doit rester lisible et navigable sur un écran étroit sans devenir une longue suite de cartes.
- Prévoir une expression plus immersive pour les moments de passage, tout en gardant les outils quotidiens sobres, rapides et accessibles.
- Éviter que les codes de gamification (points, badges, verrouillage, rang) contredisent la progression permanente et le principe de choix libre décrits dans le livre.

## 5. Questions de cadrage pour Boris, Claude et Codex

1. Parle-t-on de dix mondes au total, ou de onze positions numérotées de 0 à 10 ?
2. Les Mondes 8 et 9 restent-ils à écrire, ou existent-ils dans une autre source ?
3. Un Joueur appartient-il à un seul monde à un instant donné, ou peut-il explorer plusieurs mondes selon les dimensions de sa vie ?
4. Qui atteste un passage : le Joueur, un facilitateur, son cercle, une cérémonie, ou une combinaison de ces acteurs ?
5. Quels éléments de progression peuvent être visibles par le cercle, la communauté, les administrateurs et le public ?
6. Les 7 puissances remplacent-elles les compétences actuelles, les structurent-elles, ou forment-elles une couche indépendante ?
7. Les Chrysalides et Cités Cosmiques doivent-elles être administrées dans ze.game ou seulement référencées ?
8. Quelle première version apporte une valeur réelle sans tenter d'implémenter immédiatement toute la cosmologie ?

## 6. Première stratégie de découpage

Une évolution progressive paraît préférable :

1. Clarifier le vocabulaire, la numérotation et les règles de passage.
2. Prototyper la Marelle comme nouvelle navigation et couche de découverte, sans modifier les calculs de progression existants.
3. Relier les Journeys actuels à un ou plusieurs mondes et tester le Monde 0 avec de vrais utilisateurs.
4. Introduire les rites de passage et un historique de progression explicite.
5. Ajouter les cercles et la progression collective lorsque le fonctionnement du Monde 2 est stabilisé.
6. Étendre ensuite aux Chrysalides, oeuvres et Cités Cosmiques.

Cette séquence conserve les modèles sensibles actuels (`Journey`, `Challenge`, `JourneysUser`, `ChallengesUser`) aussi longtemps que possible et permet de valider l'expérience avant d'élargir l'architecture.
