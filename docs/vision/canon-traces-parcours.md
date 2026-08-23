# Traces produites par les parcours — canon fonctionnel

> **Ajout Codex — 23 août 2026. Décision de Boris.** Cette note précise la portée de
> `RegistreDesTraces` et prévaut sur les formulations antérieures qui limitaient les Traces à
> quelques territoires du Monde 0. Elle complète
> [Le pont Trace → Graine](pont-trace-graine-fresque.md) sans modifier la nature des Graines.

## 1. Définition

Une **Trace** est une empreinte laissée par le passage du Joueur dans le Jeu : quelque chose
qu'il a produit, reçu, observé ou choisi au cours d'un parcours.

Le principe est désormais général : **tout résultat pédagogique significatif généré dans un
parcours est récupéré sous forme de Trace**. Une expérience ne doit plus produire un résultat
visible à l'écran puis le perdre à la fermeture de la page.

La Trace conserve de la matière ; elle ne décide pas à la place du Joueur de ce que cette
matière signifie.

## 2. Ce qui devient une Trace

Le registre agrège quatre familles, conformément à la maquette de référence :

| Famille | Contenu attendu | Exemples |
|---|---|---|
| **Productions du Jeu** | résultat composé par le Joueur dans une expérience ou un mini-jeu | scénario du futur, hypothèse, carte, roue, réponse ouverte, restitution d'un QCM |
| **Retours reçus** | retour pédagogique structuré et rattaché à un passage identifiable | synthèse de mentor, regard de facilitateur, restitution produite par une expérience |
| **Diagnostics** | photographie datée et provisoire d'un état observé | Moteur, Puissance, alchimisation, profil systémique lorsqu'il existera |
| **Positionnements** | choix structurant posé par le Joueur | héros inspirant, posture du Conseil, rôle ou autre figure choisie |

La liste est extensible : une nouvelle expérience peut produire une nouvelle forme de Trace sans
créer une cinquième famille si l'une des quatre décrit déjà sa nature.

### Ne sont pas des Traces

- les messages ordinaires, réactions et conversations brutes ;
- les dialogues avec les Guides ;
- les brouillons et saisies abandonnées ;
- les événements techniques, journaux d'activité et données de télémétrie ;
- les validations d'expérience, badges, Omégas et états de progression ;
- les Graines de Récit, qui sont des cristallisations éditoriales distinctes.

Un message de mentor n'entre dans le registre que s'il devient un **retour pédagogique structuré**,
explicitement relié à une expérience ou à un passage. Le fil de conversation complet n'y entre pas.

## 3. Règle de capture dans les parcours

La capture est **automatique** lorsqu'un résultat significatif est effectivement enregistré par la
surface qui le produit. Elle ne dépend pas d'un second bouton « Conserver ».

Chaque Trace doit permettre de retrouver au minimum :

- son auteur et sa date ;
- sa famille et son type précis ;
- le parcours, le chapitre, l'expérience ou la surface source ;
- un titre et un résumé lisibles ;
- le résultat structuré nécessaire à sa restitution complète ;
- un lien pour relire la Trace ;
- lorsque cela reste pertinent, un lien pour rouvrir ou rejouer la source ;
- son état de visibilité communautaire.

La mécanique doit être idempotente : le même événement métier ne crée pas plusieurs Traces. Le
rejeu, en revanche, ne doit pas écraser silencieusement l'histoire du Joueur. Le choix entre version
nouvelle et évolution d'une Trace existante doit être explicité par l'adaptateur de l'expérience.

L'implémentation part des **événements et résultats déjà persistés** par les expériences. Elle ne
déduit pas une Trace d'un libellé de bouton et n'ajoute pas de callback générique sur les modèles
centraux sans analyse d'impact.

## 4. Trace et Graine

Une Trace n'est pas une Graine inachevée.

- La **Trace** garde une matière produite ou rencontrée dans le Jeu.
- La **Graine** formule ce que le Joueur choisit d'en faire dans son Récit.

La page **Mes Traces** est un registre de relecture. Elle ne propose pas une conversion mécanique
« En faire une Graine ». Une Trace peut nourrir une Graine au cours d'un parcours ou d'un dialogue
avec le mentor ; la cristallisation reste un geste pédagogique et éditorial distinct.

Une future filiation explicite entre une Trace et une Graine pourra être ajoutée, mais elle ne doit
pas être simulée tant qu'aucune source de vérité ne la porte.

## 5. Visibilité et profil communautaire

- Les Traces sont **privées par défaut**.
- Le Joueur peut activer globalement leur publication, puis déroger Trace par Trace.
- Le profil communautaire ne reproduit pas tout le registre : il affiche uniquement les Traces que
  le Joueur a choisi de rendre visibles.
- Un changement de visibilité ne modifie ni la Trace source ni la progression.

Cette règle demeure distincte de celle de la Fresque, partagée par défaut avec possibilité de
retrait. **Fresque : opt-out ; Traces : opt-in.**

## 6. Cas de référence — la roue du Coupable idéal

À la fin du procès :

1. la **roue complète** devient automatiquement une Trace de famille `Productions du Jeu` ;
2. la Puissance nommée dans la chambre du jury est conservée comme donnée structurée de cette
   Trace, avec les autres éléments de restitution ;
3. aucune section spéciale « roue » n'est ajoutée au Profil ;
4. le bouton « Conserver cette roue » disparaît au profit de **« Voir cette Trace »** une fois la
   restitution enregistrée ;
5. « Garder une phrase pour ma Graine » reste un geste distinct et peut créer ou préremplir la
   Graine selon le mécanisme déjà retenu.

Cette règle sert de modèle aux autres mini-jeux : le résultat complet devient une Trace ; une
formulation choisie pour la Fresque devient éventuellement une Graine.

## 7. Référence UX et contrat de portage

Claude part de la maquette
[`traces-m0-cible`](https://github.com/PointZero2050/zegame-prototypes/tree/main/traces-m0-cible)
pour le registre, ses quatre familles, ses filtres, ses états vide/première Trace/registre étoffé et
ses liens de relecture.

Le portage doit ensuite **récupérer l'ensemble des résultats générés dans les parcours**, expérience
par expérience. Avant de coder les écritures, établir la matrice suivante :

| Expérience / surface | résultat réellement persisté | événement fiable | famille | contenu de la Trace | règle de rejeu |
|---|---|---|---|---|---|

Une ligne sans résultat persistant ou sans événement fiable reste un écart à traiter ; elle ne doit
pas être masquée par une Trace fictive dans la vue.

## 8. Recette minimale

- terminer une production de parcours crée exactement une Trace ;
- recharger la page ou rejouer le callback ne la duplique pas ;
- `Mes Traces` retrouve la source, le contexte et la restitution complète ;
- une production éphémère annoncée comme conservée est effectivement persistée ;
- une Trace privée n'apparaît jamais sur le profil communautaire ;
- publier ou retirer une Trace ne valide aucune expérience et ne génère aucun Oméga ;
- aucune conversation brute, Graine, réaction ou donnée technique ne rejoint le registre ;
- le registre reste exploitable lorsque le nombre de Traces devient important.

