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
