# Monde 1 : cadre de conception des parcours

> Ajout Codex - 2026-07-14. Synthèse opérationnelle de `Synthese_Monde_1_Point_Zero.docx` fourni par Boris, croisée avec l'état documenté de `vibe.ze.game` au 14 juillet 2026. Cette note prépare la production des parcours sans intervenir dans la zone de code actuellement travaillée par Claude.

## 1. Promesse et limite pédagogique

Le Monde 1 est **l'éveil cognitif** : un espace d'orientation, de décodage, de dialogue et de mise en relation.

Le joueur doit pouvoir :

- nommer et utiliser la grammaire du Point Zéro ;
- relier les 7 Puissances, les besoins individuels, les cinq cadres et l'Oméga ;
- appliquer cette lecture à soi, aux collectifs et au monde ;
- choisir des parcours selon ses questions et ses résonances ;
- rencontrer cinq à huit compagnons potentiels avant de décider avec eux d'entrer dans le Monde 2.

Le Monde 1 ne cherche pas encore une transformation relationnelle profonde. Celle-ci commence dans le Monde 2, avec un Cercle stable et le Voyage du héros.

Formule de passage :

`Monde 0 : je pressens -> Monde 1 : je nomme et je discerne -> Monde 2 : je commence à vivre la grammaire dans la relation`

## 2. Architecture pédagogique du Monde 1

```text
Entrée dans le Monde 1
└── Tutoriel obligatoire : La Boussole du nouveau monde
    └── Ouverture du catalogue
        ├── Fondamentaux
        ├── Parcours par Puissance
        ├── Lire le monde
        ├── Découvrir l'écosystème
        ├── Organisations et société
        └── Former son Cercle
            └── Politique de passage vers le Monde 2
```

Trois mécanismes doivent rester distincts :

1. **Accès au Monde 1** : passage depuis le Monde 0 et appartenance à l'espace Monde 1.
2. **Ouverture du catalogue** : accomplissement du tutoriel obligatoire.
3. **Passage au Monde 2** : combinaison de parcours, Graine de Récit et engagement collectif réel.

Le champ V1 `Journey#mandatory` répond au deuxième besoin. Il ne doit pas servir à modéliser toute la politique de passage vers le Monde 2.

## 3. Tutoriel obligatoire

### La Boussole du nouveau monde

| Paramètre | Cadrage |
|---|---|
| Structure | Parcours court non chapitré |
| Progression | Linéaire |
| Expériences | 6 |
| Durée cible | Environ 1 h 30 |
| Validation | Majoritairement autonome |
| Jeu ou quiz | Un maximum par expérience |
| Mentor | Dernière expérience uniquement |
| Graine de Récit | Une Graine finale |
| Fonction | Donner la carte générale et orienter vers le catalogue |

Les six expériences proposées sont :

1. **Le moteur aux sept Puissances** : remettre les fonctions dans l'ordre et observer l'effet d'une fonction absente.
2. **Quand une Puissance prend toute la place** : restaurer ou tempérer une Puissance dans une mission caricaturalement déséquilibrée.
3. **Des Puissances aux besoins individuels** : relier situations, besoins et Puissances.
4. **Les cinq chakras du système** : relier symptômes collectifs, cadres capacitants et Puissances.
5. **L'harmonie entre le joueur et le système** : reconstruire les ponts entre besoins et cadres.
6. **Ce qui génère de l'Oméga** : qualifier la valeur rendue possible, échanger avec le mentor, semer la Graine et choisir une orientation.

Le parcours se termine par une hypothèse choisie par le joueur, jamais par un profil assigné : Puissance comprise, Puissance à explorer, besoin prioritaire, cadre collectif et type de valeur à rendre possible.

## 4. Catalogue cible

### Familles

| Famille | Fonction |
|---|---|
| Fondamentaux du Point Zéro | Acquérir les concepts et le langage commun |
| Parcours par Puissance | Entrer dans la grammaire depuis une question concrète |
| Lire le monde avec le Point Zéro | Décoder les crises, récits et bifurcations |
| Découvrir l'écosystème | Explorer ressources, pratiques, Chrysalides et verticales |
| Organisations et société | Lire les collectifs comme des systèmes vivants |
| Former son Cercle | Préparer la relation et composer l'équipe du Monde 2 |

### Premier lot proposé dans le document source

| # | Parcours | Famille |
|---|---|---|
| 1 | La Boussole du nouveau monde | Tutoriel obligatoire |
| 2 | La Grammaire des 7 Puissances | Fondamental |
| 3 | Le Cycle de l'Oméga | Fondamental |
| 4 | Le Voyage du héros : lire la carte avant de partir | Fondamental |
| 5 | Le PsychoKernel | Fondamental |
| 6 | Retrouver ce qui m'appelle | Désir |
| 7 | Développer son pouvoir d'agir | Volonté |
| 8 | Imaginer les futurs possibles | Imagination |
| 9 | Développer sa sensibilité par l'art | Émotion |
| 10 | Personal Branding conscient | Communication |
| 11 | Penser l'actualité par le Point Zéro | Intuition |
| 12 | Composer un Cercle de Croissance | Collectif / passage |

Ce lot offre une bonne diversité, mais il ne suffit pas encore à appliquer littéralement la condition de passage décrite dans le document : **Le Sas du Cercle** et au moins un parcours explicitement éligible comme apprentissage conversationnel n'y figurent pas. Deux options cohérentes :

- lancer 14 parcours en ajoutant `L'art de la conversation féconde` et `Le Sas du Cercle` ;
- intégrer le Sas comme dernier chapitre de `Composer un Cercle de Croissance` et déclarer un parcours existant éligible au prérequis conversationnel.

La seconde option est plus réaliste pour un premier lancement.

## 5. Correspondance avec la structure actuelle de ze.game

| Notion éditoriale | Objet actuel | Usage recommandé |
|---|---|---|
| Monde 1 | `Community` en V1 sandbox | Communauté `Point Zéro - Monde 1` ; cible ultérieure `World` distinct |
| Parcours | `Journey` | Promesse, description, durée, mode de progression, caractère obligatoire |
| Chapitre | `Page` | En-tête narratif et regroupement ; n'est plus une étape cliquable |
| Expérience | `Challenge` | Unité vécue par le joueur, affichée comme « Expérience » ou « Action » selon arbitrage lexical |
| Ordre | `ChallengesJourney.position` | Séquence des expériences dans le parcours |
| Ressource | `Resource` | Contenu ou lien rattaché à l'expérience |
| Critère explicite | `Validation` | Comment l'expérience est reconnue |
| Puissance / capacité | `Skill` et `ChallengesSkill` | Référentiel existant `PUISSANCE : ASPECT` |
| Participation joueur | `JourneysUser`, `ChallengesUser` | Progression, validation et attribution d'Oméga |
| Graine de Récit V1 | `Messaging::Thread` du `ChallengesUser` final | Message du joueur exigé avant la validation de fin de chapitre |

Le « modèle de données conseillé » dans le document source est d'abord un **schéma éditorial**. Il ne faut pas créer immédiatement un modèle Rails pour chaque ligne (`Positionnement`, `Interaction`, `Orientation`, etc.). Ces informations peuvent commencer dans un manifeste de contenu structuré, les champs existants, les tags et les référentiels, puis devenir des modèles uniquement lorsqu'un comportement applicatif réel le justifie.

## 6. Ce qui est disponible maintenant

Les derniers travaux documentés de Claude rendent déjà possibles :

- parcours `libre` ou `lineaire` ;
- parcours `mandatory` bloquant les autres parcours de la Communauté tant qu'il n'est pas accompli ;
- blocage de l'expérience suivante pendant une validation pédagogique ;
- chapitres portés par les `Page`, avec leur nom dans le détail de l'expérience ;
- autovalidation par « J'ai réalisé cette expérience » ;
- Graine de Récit obligatoire avant la validation d'une fin de chapitre ;
- Graine finale pour un parcours non chapitré via la dernière expérience ;
- personnalisation éditoriale `[Prénom]` ;
- contenus TinyMCE avec images et vidéos préservées ;
- Oméga V1 fondé sur le mécanisme actuel des points.

Le tutoriel peut donc être construit immédiatement comme :

```text
Journey
  community: Point Zéro - Monde 1
  mandatory: true
  progression_mode: lineaire
  pages: aucune
  challenges: 6
  dernière expérience: Graine requise + autovalidation
```

## 7. Ce qui exige encore un développement

| Besoin | État |
|---|---|
| Jeux de classement, association, scénario ou QCM avec résultat | Pas de moteur interactif générique documenté |
| Seuil de réussite, tentatives et débrief adaptatif | Relève du futur moteur de validation |
| Mentor IA et synthèse proposée puis validée | F5, non implémenté ; la Graine V1 reste un message libre |
| Recommandation explicable de parcours | Non implémentée |
| Carte de compagnonnage et propositions de constellations | Non implémentées |
| Formation et décision libre du Cercle | F11 en cours de cadrage |
| Politique composite de passage au Monde 2 | F10 / `WorldUnlockRule`, non implémentée |
| Modèle `World` séparé des Communautés | Cible, tandis que la V1 utilise les 11 Communautés Monde 0 à 10 |

Pour le premier parcours, les jeux peuvent être conçus pédagogiquement dès maintenant, mais leur implémentation doit être classée :

- **V1 éditoriale** : scénario + choix + débrief dans le contenu, suivi d'une autovalidation ;
- **V1 interactive ciblée** : composant spécifique si l'expérience est prioritaire pour la démonstration ;
- **moteur générique ultérieur** : types de quiz versionnés, événements `quiz_passed`, tentatives et preuves auditables.

## 8. Condition de passage vers le Monde 2

Le document propose :

- tutoriel du Monde 1 terminé ;
- `La Grammaire des 7 Puissances` terminé ;
- deux parcours librement choisis ;
- un parcours conversationnel, de discernement ou de vie collective ;
- `Composer un Cercle de Croissance` terminé ;
- Sas du Cercle vécu avec l'équipe pressentie ;
- Graine de Récit de passage semée.

Cette politique ne doit pas être réduite à un nombre de parcours. Elle combine des exigences fixes, un choix libre, une catégorie de parcours, une production narrative et une décision collective.

Modèle cible :

```text
WorldPassagePolicy Monde 1 -> Monde 2
├── exigences fixes
├── N parcours parmi une sélection ou une famille
├── Graine de passage
├── Cercle pressenti de 5 à 8 membres
├── Sas attesté
└── décision explicite des membres
```

L'algorithme peut aider à proposer des constellations, mais il ne forme jamais seul le Cercle.

## 9. Gabarit de production d'un parcours

### Fiche parcours

```text
Titre
Sous-titre
Famille et Monde
Promesse joueur
Intention pédagogique
Prérequis
Durée et intensité
Mode libre ou linéaire
Rôle éventuel dans le passage de Monde
Puissances, besoins et cadres dominants
Chapitres et progression narrative
Graine(s) de Récit attendue(s)
Règle d'émission d'Oméga V1
Tags de recommandation
```

### Fiche expérience

```text
Titre et durée
Intention de déplacement
Accroche narrative
Ressource introductive
Consigne ou interaction centrale
Un jeu/quiz maximum
Débrief : ce que la tension rend visible
Modalité de validation explicite
Puissances, besoins, cadres et compétences
Ressources complémentaires
Oméga V1
Fin de chapitre ? Mentor ? Graine ?
```

## 10. Arbitrages nécessaires avant production en série

1. **Volonté** : le document Monde 1 emploie `JE DÉCIDE`, tandis que le référentiel partagé emploie `JE VEUX`. Il faut choisir une formule canonique ou distinguer puissance (`JE VEUX`) et acte d'orientation (`JE DÉCIDE`).
2. **Vocabulaire de l'unité** : le document impose « Expérience », alors que la décision précédente retenait « Action ». Recommandation : `Challenge` en technique, **Expérience** comme nom de l'unité, et verbes d'action pour les CTA. À valider.
3. **Taille du Cercle** : le cadre Monde 1 indique 5 à 8 membres ; les documents précédents indiquent souvent 6 à 8. Une règle unique est nécessaire pour les textes et validations.
4. **Numérotation** : la plateforme retient désormais onze positions, Mondes 0 à 10. Le titre de parcours « les dix mondes » doit être reformulé ou expliqué.
5. **Premier lot** : confirmer l'intégration du Sas dans `Composer un Cercle de Croissance` ou élargir le lancement au-delà de douze parcours.
6. **Oméga** : définir pour la V1 ce qui est attribué à l'accomplissement et ce qui relève plus tard d'une reconnaissance de contribution amplifiée.

## 11. Ordre de production recommandé

1. Verrouiller le lexique canonique et le gabarit.
2. Écrire et intégrer `La Boussole du nouveau monde` comme parcours pilote.
3. Tester la structure, la durée, la Graine finale et une première interaction ludique avec un petit groupe.
4. Produire `La Grammaire des 7 Puissances` comme premier parcours chapitré de référence.
5. Produire `Composer un Cercle de Croissance`, en incluant ou non le Sas selon arbitrage.
6. Ajouter trois parcours très contrastés pour tester le catalogue : un par Puissance, un « lire le monde » et un collectif.
7. Étendre seulement ensuite vers le catalogue des douze parcours.

## 12. Format cible des six expériences de La Boussole

> Ajout Codex - 2026-07-14. Préconisation de formats avant développement, à partir du principe validé par Boris : alterner vidéos courtes, mini-jeux et quiz.

### Rythme commun

Chaque expérience suit un rythme court en trois temps :

1. **Voir** : une situation, une métaphore ou un récit de 45 secondes à 2 minutes ;
2. **Manipuler** : un seul mini-jeu ou quiz central, sans interaction décorative concurrente ;
3. **Relire** : un débrief qui explicite la tension découverte, puis la validation.

Les interactions sont formatives : pas de chronomètre, pas de classement et pas de sanction pour une mauvaise réponse. Le joueur peut recommencer et reçoit une explication liée à son choix. La validation porte sur le fait d'avoir traversé toutes les étapes, sauf lorsqu'un acquis objectif exige plus tard un seuil explicite.

| Expérience | Dominante | Ressource introductive | Interaction centrale | Sortie et débrief | Durée cible | Complexité |
|---|---|---|---|---|---|---|
| 1. Le moteur aux sept Puissances | Vidéo + mini-jeu de séquençage | Animation de 75 à 90 s : une intention concrète, par exemple un jardin partagé, traverse les sept fonctions | **Remets le moteur en marche** : ordonner sept cartes ; second tour avec une fonction absente et choix de la conséquence | Vue animée du moteur complet et phrase : « aucune Puissance ne produit seule le mouvement » | 12 min | Moyenne |
| 2. Quand une Puissance prend toute la place | Mini-jeu à scénarios | Vignette animée de 45 à 60 s : une mission collective bascule dans la caricature | **Sauve la mission impossible** : pour cinq incidents, choisir s'il faut réintroduire, tempérer ou relier une Puissance | Le résultat ne désigne pas une « bonne » Puissance ; il montre la fonction manquante ou exacerbée dans la situation | 14 min | Moyenne à forte |
| 3. Des Puissances aux besoins individuels | Quiz illustré d'association | Cinq messages courts de personnages confrontés à un collectif | **Que demande réellement le joueur ?** : associer situation, besoin et Puissance ; chaque réponse ouvre une justification | Tableau final des cinq correspondances et invitation à repérer celle qui résonne, sans en déduire un profil | 12 min | Faible à moyenne |
| 4. Les cinq chakras du système | Vidéo + mini-diagnostic | Motion comic de 75 à 90 s : réunion d'une organisation fictive accumulant cinq symptômes | **Répare le collectif dysfonctionnel** : placer les symptômes sur les cinq cadres, puis relier chaque cadre à sa Puissance | Passage de la lecture morale des personnes à la lecture systémique des conditions | 15 min | Moyenne |
| 5. L'harmonie entre le joueur et le système | Mini-jeu de construction | Introduction visuelle très courte : deux rives, besoins individuels et cadres collectifs | **Le pont de l'harmonie** : construire cinq ponts, puis choisir dans des cas concrets le levier à restaurer : expression du besoin, qualité du cadre, responsabilité individuelle ou collective | Carte des ponts solides ou fragiles, sans score psychologique | 15 min | Moyenne à forte |
| 6. Ce qui génère de l'Oméga | Vidéo + quiz de qualification + récit | Montage de 90 à 120 s : six contributions, de l'inflexion personnelle à l'essaimage civilisationnel | **Le laboratoire de la valeur invisible** : qualifier plusieurs dimensions de valeur ; certaines situations acceptent plusieurs lectures argumentées | Échange mentor, Graine de Récit finale et choix de la première orientation dans le catalogue | 22 min | Forte avec mentor ; moyenne sans IA |

Durée totale cible : **environ 90 minutes**, avec possibilité de quitter et reprendre entre les expériences.

### Détails d'interaction

#### 1. Remets le moteur en marche

- Cartes : élan, décision, conception, ressenti, expression, discernement, redistribution.
- Le glisser-déposer doit avoir une alternative accessible par sélection et boutons « monter/descendre ».
- Le second tour retire une carte et propose trois conséquences plausibles : le jeu explique le déséquilibre plutôt que de signaler seulement une erreur.
- Le tracé final peut devenir la première animation réutilisable du moteur des Puissances.

#### 2. Sauve la mission impossible

- Chaque incident est une petite scène avec personnages récurrents.
- Trois verbes structurent la réponse : **réintroduire**, **tempérer**, **relier**.
- Les conséquences sont jouées immédiatement dans la scène, avec une touche d'humour.
- Une même Puissance peut être utile dans un incident et problématique dans un autre.

#### 3. Que demande réellement le joueur ?

- Le quiz évite les formulations scolaires du type « quelle est la bonne définition ? ».
- Le joueur lit d'abord la situation, choisit un besoin, puis découvre la Puissance associée.
- Une seconde passe peut demander quel cadre collectif permettrait au besoin de s'exprimer.
- Le choix personnel final est facultatif et n'alimente aucun profil automatique.

#### 4. Répare le collectif dysfonctionnel

- Le collectif fictif doit être mémorable mais non assimilable à une organisation réelle.
- Les symptômes apparaissent dans des extraits de réunion, messages ou décisions contradictoires.
- Le joueur place chaque indice dans un cadre, puis voit les relations entre cadres plutôt qu'un tableau de cases indépendantes.
- Le débrief distingue symptôme, cadre défaillant et responsabilité partagée.

#### 5. Le pont de l'harmonie

- Les deux rives portent les cinq besoins et les cinq cadres.
- Construire une correspondance correcte ne suffit pas : trois cas demandent ensuite où agir.
- Le pont peut se tendre, se rigidifier ou se rompre selon la situation, afin d'éviter une représentation statique de l'équilibre.
- La métaphore doit rester claire sur mobile et ne pas dépendre uniquement des couleurs.

#### 6. Le laboratoire de la valeur invisible

- Les dimensions proposées peuvent être : personnelle, relationnelle, communautaire, transmissible et civilisationnelle.
- Plusieurs dimensions peuvent coexister ; le joueur justifie parfois son choix en une phrase.
- Le quiz ne calcule pas la quantité d'Oméga : il apprend ce que la monnaie cherche à reconnaître.
- La Graine finale reprend les cinq questions du mentor et reste modifiable avant publication.

## 13. Direction artistique du Monde 1

La direction artistique globale est définie dans [direction-artistique-point-zero.md](direction-artistique-point-zero.md) : le **néoarchaïsme** est la grammaire mère du Point Zéro, tandis que chaque parcours peut développer son propre univers narratif.

### État de la banque d'images

Le dossier `Ressources Point Zero/Images` contient actuellement **456 fichiers** : 316 PNG et 140 JPG, répartis principalement entre `Illustrations` et `Badges`.

La matière est riche mais hétérogène :

- scènes fantasy ou science-fiction très colorées ;
- collages surréalistes et symboliques ;
- compositions sombres adaptées à l'Ombre ou aux Mondes ultérieurs ;
- diagrammes circulaires autour des cadres, de la monnaie et du jeu ;
- images historiques ou humoristiques parfois liées à des références culturelles reconnaissables ;
- styles et générations d'IA différents.

Ces images constituent une **iconothèque et un moodboard**, pas encore une série éditoriale homogène.

### Expression proposée pour La Boussole : l'atlas alchimique vivant

La Boussole donne une carte et un langage. Son univers peut donc combiner :

- **cartographie** : boussoles, cartes, chemins, légendes, coordonnées et constellations ;
- **mécanique vivante** : roues, engrenages organiques, circulation, orreries et ponts ;
- **alchimie contemporaine** : gravure, collage, textures physiques et lumière cosmique ;
- **clarté pédagogique** : diagrammes propres, composants manipulables et états lisibles.

Le ton applique la [charte de voix Point Zéro](voix-point-zero.md) : merveilleux et décalé, mais aussi adulte, légèrement provocateur et capable de percer sa propre solennité. Le joueur découvre un instrument d'orientation, pas une prophétie écrasante ni un module de développement personnel qui le félicite d'avoir cliqué. Les autres parcours du Monde 1 peuvent adopter des styles très différents en conservant quelques invariants néoarchaïques et ce rapport vivant entre ambition, friction et humour discret.

### Palette et langage visuel

- conserver le violet Point Zéro comme ancrage d'interface ;
- utiliser bleu pétrole, ivoire clair et noir en base, avec or solaire et corail comme accents ;
- reprendre provisoirement les couleurs du référentiel des chakras pour distinguer les Puissances : rouge, orange, jaune, vert, cyan, indigo, puis violet/blanc pour la Transcendance ;
- ne jamais faire reposer une information uniquement sur la couleur : symbole, libellé et forme accompagnent chaque Puissance ;
- réserver les textures et détails aux images narratives ; les jeux utilisent des formes plus nettes et stables.

### Trois niveaux d'assets

1. **Images-seuils** : illustrations immersives 16:9 pour ouvrir une expérience ou une vidéo.
2. **Schémas du référentiel** : dessins propres et réutilisables du moteur, des cinq cadres, des ponts et du cycle de l'Oméga.
3. **Pièces de jeu** : cartes, personnages, symptômes, jetons et états conçus comme une seule famille de composants.

Les images générées existantes peuvent nourrir le premier niveau. Les deuxième et troisième niveaux doivent être redessinés dans une grammaire cohérente plutôt que découpés directement dans des images complexes.

### Premières correspondances dans l'iconothèque

| Usage | Candidat existant | Recommandation |
|---|---|---|
| Couverture du tutoriel | `Firefly_Une carte aux trésor et une boussole 522905.jpg` | Très bon signal d'orientation ; recadrer et harmoniser la colorimétrie |
| Moteur des Puissances | séries `Philosophie-Point-Zéro-*` et `Jeu-*` | Moodboard symbolique ; créer un schéma dédié plus lisible |
| Cadres systémiques | série `Cadres-systemiques-*` | Bonne matière de départ, à simplifier pour l'interaction |
| Pont besoins/cadres | `Deux-continents.png` | Métaphore pertinente ; reconstruire une version jouable moins spectaculaire |
| Oméga | séries `Monnaie-*` | Conserver la logique circulaire ; aligner avec le logo officiel de l'Oméga |
| Situations collectives | images de groupes, labyrinthes et scènes de facilitation | Sélectionner un style unique et des personnages récurrents |

`Jeu-1.png` et d'autres images très sombres ont une vraie force, mais semblent mieux adaptées à des Mondes ultérieurs qu'au tutoriel d'orientation.

`Jeu-3.png` constitue en revanche un bon exemple de transposition : univers heroic fantasy, mais continuité Point Zéro par la silhouette archétypale, le portail, le cercle, le glyphe et la matière.

### Règles média

- vidéo courte en 16:9, 1080p, sans lecture automatique ;
- sous-titres séparés, transcription et image d'affiche ;
- texte, symboles et boutons toujours produits par l'interface, jamais incrustés dans une image générée ;
- zone centrale sûre pour les recadrages mobile, avec variantes 16:9 et 4:3 ou carrées lorsque nécessaire ;
- aucun détail essentiel uniquement dans un fond décoratif ;
- alternative accessible pour chaque glisser-déposer ;
- sons facultatifs, sous-titrés lorsqu'ils portent une information, et désactivables.

### Audit avant publication

Chaque visuel retenu doit recevoir une fiche minimale : source, auteur ou outil de génération, date, licence ou droit d'usage, prompt disponible, modifications et parcours concernés.

Les images comportant des personnages, marques ou univers reconnaissables (`Tintin`, `X-Files`, etc.) ne doivent pas être publiées dans le produit sans vérification des droits. Les anomalies typiques des générations d'IA, les pseudo-textes et les personnages involontairement inquiétants doivent également être écartés ou retravaillés.

## 14. Grammaire des modalités pédagogiques

> Ajout Codex - 2026-07-14. Ce cadre traduit la décision de combiner, à partir du Monde 1, des temps individuels et collectifs sans confondre participation, preuve et jugement sur la personne.

La séquence `vidéo → jeu ou quiz → Graine` est une **grammaire**, pas une obligation pour chaque expérience. La vidéo met en situation, le jeu ou le quiz rend le joueur actif, et la Graine clôt un chapitre ou un déplacement significatif. Une expérience ne doit pas accumuler artificiellement les quatre formats.

| Modalité | Usage | Validation recommandée |
|---|---|---|
| Individuel autovalidé | Découverte, manipulation, réflexion, action personnelle | Achèvement des étapes et déclaration du joueur ; seuil uniquement pour un acquis objectivement vérifiable |
| Collectif autofacilité — Monde 1 | Mise en discussion, confrontation des lectures, synthèse | Présence ou contribution attestée, trace individuelle et éventuellement trace commune ; aucun pair ne juge la qualité de conscience d'un autre |
| Collectif validé par facilitateur | Expérience exigeant observation du processus, sécurité ou critères partagés | Validation par un facilitateur autorisé selon des critères visibles et contestables |
| Terrain ou action | Expérimentation dans le monde réel, seul ou en sous-groupe | Preuve proportionnée, récit réflexif ou combinaison de conditions définies à l'avance |

Chaque expérience devra préciser au minimum :

- sa modalité et la taille du groupe ;
- son caractère obligatoire, facultatif ou alternatif ;
- les prérequis et le mode de constitution du groupe ;
- les rôles éventuels et le guide associé ;
- la trace attendue, son niveau de visibilité et sa durée de conservation ;
- le mécanisme de validation et l'acteur habilité à valider ;
- une solution de repli en cas d'absence, de désaccord ou de besoin d'accessibilité.

### Place du collectif dans La Boussole

Le tutoriel obligatoire doit rester entièrement réalisable en individuel afin de ne pas conditionner l'entrée dans le Monde 1 à la disponibilité d'un Cercle. Une **escale collective facultative** peut être proposée à la fin : partager sa première lecture des Puissances et découvrir les rôles d'autofacilitation. Les premiers collectifs obligatoires interviennent ensuite dans les parcours du catalogue qui en ont pédagogiquement besoin.

La Boussole doit aussi aider le joueur à formuler sa première **signature d'engagement**. L'expérience montre que la réussite d'un Cercle dépend davantage d'un désir commun d'avancer avec une intensité compatible que d'un niveau de départ homogène. Il ne s'agit donc ni d'un test de maturité, ni d'un score de conscience, mais de préférences déclarées et révisables :

- cadence de rencontre souhaitée ;
- temps disponible entre les rencontres ;
- horizon d'engagement envisagé ;
- place souhaitée pour l'action concrète dans le monde réel ;
- degré de confrontation bienveillante et de redevabilité mutuelle recherché.

La synthèse de ces choix est visible par le joueur dès le tutoriel. Elle pourra ensuite être rendue visible, avec son consentement, aux personnes qui composent un Cercle. L'application doit montrer les compatibilités et les écarts axe par axe, sans produire une note globale ni présenter l'intensité maximale comme supérieure.

Le cadre détaillé des Cercles du Monde 1 est décrit dans [autofacilitation-monde-1.md](autofacilitation-monde-1.md).

## 15. Paquet de production d'un parcours

Un parcours peut être écrit avant le développement de ses interactions. Le paquet documentaire cible comprend :

1. **Fiche-cadre** : public, promesse, déplacement attendu, place dans le Monde, durée, prérequis et risques particuliers.
2. **Déroulé éditorial** : chapitres, expériences, textes, ressources, modalités, validations, Puissances et Oméga.
3. **Fiches d'interaction** : règles, états, retours pédagogiques, accessibilité et données attendues pour chaque jeu ou quiz.
4. **Guide collectif** : préparation, rôles, conducteur, traces et protocole de sécurité pour chaque séquence collective.
5. **Manifeste média** : liste des vidéos, illustrations, schémas, sons et variantes de format.
6. **Manifeste structuré** : représentation Markdown, YAML ou JSON préparant l'import futur, à aligner avec le format réellement accepté par l'application avant intégration.

### Pipeline des illustrations

Codex peut prendre en charge l'ensemble du processus de génération : rédaction des prompts, génération, inspection, itérations, sélection et classement des fichiers finaux. Boris peut aussi générer les images avec les mêmes prompts ; le manifeste conserve alors la continuité entre outils.

Pour chaque asset, le manifeste indique : identifiant, fonction dans le parcours, dimensions, univers visuel, invariants néoarchaïques, prompt, références, éléments à éviter, statut, outil ou modèle, date, droits et nom de fichier final.

Le processus recommandé est :

1. produire trois à cinq images pilotes pour verrouiller l'univers du parcours ;
2. valider une image-seuil, une scène ou un personnage, et un composant pédagogique ;
3. générer ensuite les séries cohérentes par lots courts ;
4. contrôler la continuité, les anomalies et les droits avant intégration ;
5. conserver les prompts et métadonnées avec les assets retenus.

Les illustrations immersives, décors et personnages peuvent être générés comme images matricielles. Les diagrammes, glyphes, cartes de jeu, textes et éléments interactifs doivent plutôt être construits en SVG, HTML/CSS ou composants d'interface pour rester lisibles, cohérents et accessibles.

## 16. Informations nécessaires pour lancer un parcours

Les documents actuels permettent de commencer `La Boussole du nouveau monde`. Les décisions encore demandées à Boris se limitent à :

- valider la promesse et le résultat attendu du parcours ;
- indiquer les sources obligatoires, formulations intouchables et sujets sensibles ;
- confirmer le public de la première version et le niveau de langage ;
- choisir les séquences collectives obligatoires, facultatives ou absentes ;
- arbitrer les points ouverts du §10, en priorité `JE VEUX` / `JE DÉCIDE`, `Expérience` / `Action`, taille du Cercle et attribution de l'Oméga ;
- valider le premier lot d'images pilotes avant production en série.

À défaut d'un arbitrage immédiat, la production peut avancer avec les hypothèses réversibles suivantes : `JE VEUX` désigne la Puissance et `JE DÉCIDE` son acte d'orientation ; **Expérience** est le nom visible de l'unité ; le Cercle cible compte 6 à 8 personnes ; l'Oméga V1 récompense l'accomplissement sans prétendre mesurer l'impact systémique.
