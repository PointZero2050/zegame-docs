# Spécifications fonctionnelles initiales de l’application

## 1. Modules principaux

### Profil du Moteur

Vue par Puissance : amplitude explorée, zone libre, zone en apprentissage, activation actuelle, archétype, niveau de confiance et preuves.

### Carte des déplacements

Graphe des états et transitions, avec chemin recommandé et alternatives.

### Catalogue de parcours

Recherche par Monde, Puissance, verticale, figure, contexte, intensité, modalité et durée.

### Lecteur de parcours

Expériences, ressources, interactions, mentor, Graine de Récit, feedbacks et validation.

### Éditeur d’expériences

Création manuelle ou assistée, métadonnées de transition, règles de sécurité, preuves et versioning.

### Moteur de recommandation

Sélectionne le prochain déplacement selon l’état du Moteur, le Monde, les préférences, les objectifs et les contraintes.

### Générateur adaptatif

Assemble ou crée les expériences manquantes, avec signalement expérimental et validation humaine.

### Atlas des Figures

Recherche, comparaison, constellation de destination, rôle modèle et Assemblée Intérieure.

### Commun Point Zéro

Catalogue de méthodes, statuts d’apprentissage, facilitation, contribution et gouvernance des ressources.

## 2. Vue d’une Puissance

Afficher séparément :

- amplitude Ombre explorée ;
- amplitude Lumière explorée ;
- amplitude maîtrisée librement ;
- état de circulation ;
- activation du moment ;
- archétype contextualisé ;
- pouvoirs acquis ;
- blocages possibles ;
- frontière proposée ;
- preuves et feedbacks ;
- historique des déplacements.

## 3. Moteur de recommandation

### Entrées

- profil du Moteur ;
- Monde ;
- objectifs explicites ;
- verticale ou contexte ;
- figures choisies ;
- disponibilités et modalités ;
- expériences précédentes ;
- niveau de sécurité requis ;
- composition du Cercle.

### Règles minimales

1. Prioriser la circulation si l’état est bloqué.
2. Consolider l’autonomie si l’état est intermédiaire.
3. Élargir l’amplitude ou le contexte si l’état est libre.
4. Ne pas travailler plusieurs sauts majeurs simultanément.
5. Proposer plusieurs itinéraires explicables.
6. Ne jamais mettre à jour le profil à partir d’une seule autoévaluation.

### Sortie explicable

> Ce parcours est proposé parce qu’il travaille la Communication O2, répond à un blocage de la Lumière L1, s’applique à la verticale Leadership et peut être réalisé avec ton Cercle actuel.

## 4. Mise à jour du profil

Le système agrège :

- autoévaluation ;
- comportements observés ;
- feedbacks des pairs ;
- observations du facilitateur ;
- dialogue mentor IA ;
- preuves réelles ;
- répétitions dans différents contextes.

Chaque conclusion possède :

- une date ;
- un contexte ;
- une source ;
- un poids ;
- un niveau de confiance ;
- une possibilité de contestation par le joueur.

## 5. Génération ad hoc

Une expérience générée doit afficher :

- pourquoi elle est proposée ;
- le déplacement visé ;
- les risques et conditions ;
- les ressources nécessaires ;
- son statut expérimental ;
- la manière de donner un retour ;
- la version du prompt ou du modèle générateur.

## 6. Gestion des intensités

Les expériences O3/L3, les confrontations profondes et les situations émotionnellement fortes doivent pouvoir exiger :

- un facilitateur ;
- un Cercle stable ;
- un consentement explicite ;
- un protocole d’arrêt ;
- une intégration différée ;
- une exclusion des personnes ou contextes pour lesquels l’expérience n’est pas appropriée.

## 7. Messagerie et Cercles

Le Monde 1 nécessite une plateforme de messagerie favorisant :

- conversations thématiques ;
- réactions aux ressources ;
- mise en relation ;
- constitution de Cercles de cinq à huit personnes ;
- carte de compagnonnage ;
- espaces temporaires de test avant engagement.

## 8. Versioning

Versionner :

- parcours ;
- expériences ;
- profils de figures ;
- algorithmes de recommandation ;
- règles d’évaluation ;
- ressources du Commun.

Conserver la trace de la version utilisée pour chaque expérience et décision.

## 9. Données sensibles et éthique

- contrôle fin de la visibilité ;
- consentement explicite pour les feedbacks ;
- possibilité de supprimer ou corriger des données ;
- séparation entre hypothèse pédagogique et diagnostic ;
- aucune décision médicale, psychologique, professionnelle ou juridique automatique ;
- transparence sur les sources et la confiance ;
- attention particulière aux profils de personnes réelles.
