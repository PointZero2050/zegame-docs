# Parcours publics — ancrage des dix respirations illustrées

> **Arbitrage Codex, 29 août 2026.** Cette table complète le lot néoarchaïque livré dans
> `zegame-prototypes/site-point-zero-v5-engagement/assets/parcours/`. Elle désigne l'écran
> exact qui porte chaque scène dans les cinq parcours actuellement servis.

## Principe

Une respiration n'est ni une nouvelle étape ni une couverture répétée. Elle apparaît dans le
flux de l'écran indiqué, après l'introduction du concept et avant le geste principal lorsqu'il
y en a un. Son texte alternatif nomme ce qu'elle met en relation sans interpréter la réponse du
visiteur.

Sur mobile, l'image occupe toute la largeur utile entre le texte et l'action. Sur desktop, elle
peut former un panneau latéral ou une bande 16:9. Elle reste secondaire face au choix à faire et
ne doit pas repousser le CTA sous plusieurs hauteurs d'écran.

## Ancrages canoniques

| Parcours | Fichier | Écran `data-screen` | Placement et fonction |
|---|---|---|---|
| Qu'arrive-t-il à l'humanité ? | `humanite/scene-01-convergence-des-cycles.webp` | `c03` — Une convergence, pas un événement | Après la vidéo ou sa transcription : rendre simultanément visibles les temporalités qui convergent. |
| Qu'arrive-t-il à l'humanité ? | `humanite/scene-02-dix-manifestations.webp` | `c07` — Les dix manifestations | Avant la sélection des trois signes : ouvrir le champ d'observation sans pré-cocher ni hiérarchiser. |
| Quels sont les scénarios du futur ? | `scenarios/scene-01-cinq-familles.webp` | `f03` — Cinq familles de futurs possibles | Après la vidéo : installer les cinq familles comme horizons coexistants, pas comme classement. |
| Quels sont les scénarios du futur ? | `scenarios/scene-02-scenario-hybride.webp` | `f07` — Composer mon futur | Au-dessus du formulaire de composition : figurer l'assemblage sans proposer le résultat au visiteur. |
| Quelles forces ont façonné nos croyances ? | `croyances/scene-01-objets-qui-programment.webp` | `p04` — Choisir une pièce à conviction | Avant la grille des objets et institutions : rendre sensible leur action silencieuse sur les usages. |
| Quelles forces ont façonné nos croyances ? | `croyances/scene-02-croyance-repolarisee.webp` | `p09` — Alchimiser plutôt que supprimer | Entre la question et le champ de règle consciente : montrer qu'une qualité peut être conservée sans subir son instruction. |
| Qu'est-ce qui nous paralyse ? | `paralysie/scene-01-cinq-leviers.webp` | `l05` — Cinq leviers, dix jetons | Avant la répartition : présenter les leviers comme différents et complémentaires, sans suggérer une allocation. |
| Qu'est-ce qui nous paralyse ? | `paralysie/scene-02-alliance-des-echelles.webp` | `l07` — Trois échelles, une seule contradiction | Après l'exposé des trois échelles : faire voir leur liaison avant la descente dans les cinq lectures. |
| Comment nous réveiller ? | `reveil/scene-01-circuits-interrompus.webp` | `r06` — Un cadre conditionne tous les autres | Après l'explication du cadre : figurer des capacités présentes mais séparées avant l'exercice de liaison. |
| Comment nous réveiller ? | `reveil/scene-02-circuit-vivant.webp` | `r10` — Ma carte des cadres et des Puissances | Au seuil de la restitution : montrer la circulation recomposée sans transformer la carte du visiteur en diagnostic. |

## Règles de rendu

- Chargement différé pour toutes les scènes ; l'image de l'écran courant seulement doit être
  demandée lorsque le parcours masque les autres écrans.
- Pas de texte incrusté : titres, légendes et alternatives restent en HTML.
- Une seule scène par écran et aucune animation automatique.
- Le bouton principal demeure visible dans le même écran à 390 px ; si nécessaire, réduire
  l'image plutôt que déplacer l'action.
- Conserver les dérivés optimisés produits pour l'intégration ; ne pas servir les masters aux
  dimensions de génération.

## Alternatives accessibles proposées

| Fichier | Texte alternatif court |
|---|---|
| `humanite/scene-01-convergence-des-cycles.webp` | Plusieurs cycles de durées différentes convergent vers une même zone de bascule. |
| `humanite/scene-02-dix-manifestations.webp` | Dix signes de transformation apparaissent autour d'un monde en transition. |
| `scenarios/scene-01-cinq-familles.webp` | Cinq familles de futurs entourent un présent ouvert. |
| `scenarios/scene-02-scenario-hybride.webp` | Des fragments de futurs différents s'assemblent en une trajectoire nouvelle. |
| `croyances/scene-01-objets-qui-programment.webp` | Des objets ordinaires relient leurs usages à des croyances devenues invisibles. |
| `croyances/scene-02-croyance-repolarisee.webp` | Une forme héritée se défait puis se recompose autour de sa qualité utile. |
| `paralysie/scene-01-cinq-leviers.webp` | Cinq leviers agissent à des profondeurs différentes autour d'une même crise. |
| `paralysie/scene-02-alliance-des-echelles.webp` | Les échelles personnelle, collective et civilisationnelle se répondent. |
| `reveil/scene-01-circuits-interrompus.webp` | Des capacités présentes restent séparées par des circuits interrompus. |
| `reveil/scene-02-circuit-vivant.webp` | Les Puissances reliées forment un circuit vivant autour d'un centre ouvert. |
