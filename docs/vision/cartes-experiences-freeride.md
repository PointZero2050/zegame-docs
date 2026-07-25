# Cartes-couvertures d'expérience et mode Freeride

> Ajout Codex - 2026-07-25. Architecture UX validée par Boris après inspection de la fiche d'expérience déployée sur `vibe.ze.game`.
>
> **Décision immédiate** : améliorer les fiches actuelles avec une carte-couverture mobile-first réutilisable.
>
> **Horizon validé, non à implémenter sans cadrage dédié** : ouvrir progressivement un mode Freeride à partir du Monde 2, sous forme de petites mains de cartes explicables et contextualisées.

## 1. Problème constaté

Sur la fiche d'expérience déployée :

- à grande largeur, l'illustration devient un médaillon de 130 px dans un bandeau d'environ 300 px de haut ;
- le bandeau laisse beaucoup de vide et ne porte aucune promesse courte ;
- sur mobile, l'image retrouve un rôle immersif mais titre, tags, statut et action se concurrencent ;
- les compétences apparaissent avant que le joueur comprenne ce qu'il vient vivre ;
- le statut de validation occupe davantage la scène que l'expérience elle-même.

Le médaillon fonctionne comme identifiant dans une liste, un badge ou un Profil. Il ne doit plus être la forme principale de l'illustration sur une fiche détaillée.

## 2. Décision UX : la carte-couverture

La partie supérieure d'une fiche devient une **carte-couverture d'expérience**. Elle occupe tout l'espace mobile utile entre l'en-tête et la navigation basse, et une grande partie du premier écran sur ordinateur.

Elle doit répondre immédiatement à cinq questions :

1. Où suis-je ?
2. Pourquoi cette expérience devrait-elle m'intéresser ?
3. Qu'est-ce que je vais vivre ?
4. Quel engagement demande-t-elle ?
5. Comment puis-je commencer ?

### Contenu minimal

- Monde et chapitre ;
- mouvement du chapitre, par exemple `JE PRESSENS` ;
- statut contextuel : obligatoire, optionnelle, alternative, libre, recommandée ou verrouillée ;
- illustration ;
- titre ;
- accroche de 100 à 160 caractères ;
- format principal ;
- durée ;
- Oméga disponible ;
- action principale ;
- lien `Voir les détails`.

Les tags, compétences détaillées, règles de validation et ressources secondaires ne sont pas placés dans la couverture.

### Exemple — expérience d'entrée du Monde 0

```text
MONDE 0 · CHAPITRE 1 · JE PRESSENS

Le Point Zéro :
entrer dans le Jeu

Qui a cassé le monde ?
Interroge ton récit et découvre le Moteur
invisible qui oriente tes choix.

Vidéo + mini-jeu · 15 min · 6 Ω

[ Entrer dans le Jeu ]

Voir les détails ↓
```

La révélation « Ton premier super-pouvoir est ton récit » intervient ensuite dans l'expérience ou sa restitution ; elle ne remplace pas nécessairement l'accroche interrogative.

## 3. Comportement responsive

### Mobile

Le viewport disponible devient la carte. Il ne faut pas dessiner une petite carte à l'intérieur d'une autre carte :

```text
┌──────────────────────────────┐
│ Monde · chapitre · position  │
│                              │
│     scène de l'image         │
│                              │
├──────────────────────────────┤
│ mouvement          statut    │
│ titre                        │
│ accroche                     │
│ format · durée · Oméga       │
│ [ action principale ]        │
│ Voir les détails ↓           │
└──────────────────────────────┘
```

Contraintes :

- hauteur fondée sur `100dvh` moins l'en-tête et la navigation basse ;
- titre limité éditorialement à trois lignes ;
- accroche limitée à environ trois lignes ;
- un seul bouton principal ;
- respect des zones sûres mobiles ;
- aucune information essentielle uniquement portée par un geste.

### Grand écran

Le même composant devient une affiche horizontale :

```text
┌────────────────────┬─────────────────────────┐
│                    │ Monde · chapitre        │
│ scène de l'image   │ titre                   │
│                    │ accroche                │
│                    │ format · durée · Oméga  │
│                    │ [ action principale ]   │
│                    │ Voir les détails ↓      │
└────────────────────┴─────────────────────────┘
```

La carte reçoit une largeur maximale. L'image ne redevient pas un médaillon.

## 4. Une scène d'image robuste

Le produit doit accepter des illustrations carrées, verticales, horizontales, transparentes, anciennes ou récentes.

Le comportement par défaut est :

1. arrière-plan dérivé de l'image, agrandi, légèrement flouté et assombri ;
2. image originale au premier plan avec `object-fit: contain` ;
3. absence de texte indispensable directement superposé à l'image ;
4. fond de secours utilisant la couleur ou la texture du chapitre.

Un mode facultatif `plein cadre` peut utiliser `object-fit: cover` lorsque l'image a été produite pour cet usage. Un point focal éditable peut compléter ce mode plus tard.

Deux usages sont distingués :

- `cover` : fiche, carte plein écran et futur deck ;
- `medallion` : liste de parcours, accomplissement, Carte du Seuil et aperçu compact.

Il n'est pas nécessaire de dupliquer physiquement tous les fichiers dès la V1. Le système doit en revanche distinguer les deux rendus.

## 5. Divulgation progressive

La couverture vend l'expérience. La fiche technique explique ses conditions.

Ordre recommandé sous l'ancre `#details` :

1. **À quoi t'attendre** — description développée ;
2. **Vivre l'expérience** — ressource ou interaction principale ;
3. **Comment ce passage sera reconnu** — validation ;
4. **Ce que cette expérience met en mouvement** — Puissances et polarités ;
5. **Conditions** — prérequis, intensité, collectif, sécurité et accessibilité ;
6. **Ressources complémentaires** ;
7. **Oméga** — montant et logique d'attribution.

### Deux contextes de détail

- **Lien direct ou parcours structuré** : couverture puis détails sous la même URL, accessibles par ancre.
- **Futur deck** : toucher la carte ouvre les mêmes détails dans un écran superposé plein format ou une feuille remontante. Fermer restitue exactement la position dans la main.

La fiche conserve une URL canonique unique. Le deck ne duplique pas son contenu.

## 6. Statuts et contextes

Le caractère obligatoire ou optionnel appartient à l'inclusion de l'expérience dans un parcours, pas à l'expérience en soi.

| Statut visible | Sens |
|---|---|
| Obligatoire | Requise dans le parcours ouvert |
| Optionnelle | Peut être passée dans ce parcours et reprise plus tard |
| Alternative | Une option parmi plusieurs satisfait le passage |
| Libre | Accessible hors séquence obligatoire |
| Recommandée | Pertinente dans le contexte présent, sans obligation |
| Verrouillée | Prérequis, droit, Cercle ou facilitateur manquant |

Une même expérience peut être obligatoire dans un parcours, libre dans le catalogue et recommandée dans une main Freeride.

### Actions contextuelles

| Contexte | Action principale | Action secondaire |
|---|---|---|
| Parcours structuré | Commencer / Reprendre | Passer cette étape si optionnelle |
| Expérience accomplie | Rejouer / Revoir | Continuer le parcours |
| Catalogue | Choisir cette expérience | Ajouter à ma ligne de jeu |
| Freeride | Prendre ce passage | Pas maintenant |
| Expérience programmée | Voir le rendez-vous | Modifier la programmation |
| Prérequis manquant | Préparer ce passage | Comprendre les conditions |

`Passer cette étape` et `Pas maintenant` ne sont pas synonymes :

- le premier déverrouille la suite d'un parcours structuré lorsque l'inclusion est optionnelle ;
- le second retire une recommandation de la main actuelle sans modifier le parcours ni le Profil.

La navigation `Précédent` / `Suivant` doit devenir contextuelle. La fiche ne doit pas supposer qu'elle a toujours été ouverte depuis une séquence linéaire.

## 7. Impact sur la page du parcours

La page ordonnée d'un parcours reste utile. Elle porte ses chapitres, sa progression et son récit.

Ses lignes ou cartes deviennent des versions compactes du même composant :

- médaillon ;
- titre ;
- accroche très courte ;
- format et durée ;
- statut dans ce parcours ;
- Oméga ;
- état du joueur ;
- action immédiate.

Le futur deck ne remplace donc pas la page du parcours. Il réutilise ses expériences dans une autre logique.

## 8. Principe du Freeride

Le Freeride est une **navigation libre sous horizon** :

- la Marelle conserve l'axe vertical des Mondes, des rites et des passages ;
- le Freeride ouvre l'axe horizontal des expériences, détours, approfondissements et contributions.

Il ne contourne jamais :

- un rite de passage ;
- un prérequis de sécurité ;
- une validation humaine requise ;
- un droit d'accès à un Monde.

### Progression proposée

| Monde | Degré de liberté |
|---|---|
| Monde 0 | Trajectoire écrite et commune |
| Monde 1 | Orientation guidée, catalogue et première main très encadrée |
| Monde 2 | Ouverture réelle du Freeride, avec Cercle stable et Boussole acquise |
| Mondes suivants | Autonomie croissante, expériences et contributions plus complexes |

Le Monde 2 est un seuil pertinent : le joueur dispose déjà d'un premier miroir, de la grammaire des Puissances, d'un Appel, d'une signature d'engagement et d'un Cercle.

## 9. Une main, pas un flux infini

Le Freeride ne doit pas devenir un fil de consommation sans fin. Le système propose une **main de trois cartes** :

1. **Élan** — partir d'une capacité déjà disponible ;
2. **Circulation** — explorer un mouvement moins accessible ;
3. **Ouverture** — changer de contexte, rencontrer une relation, contribuer ou accueillir une surprise latérale.

Cette diversité évite un parcours uniquement correctif ou une bulle de confirmation.

Le joueur peut demander une nouvelle main à partir d'une intention contextuelle :

- j'ai dix minutes ;
- j'ai besoin de recul ;
- je veux passer à l'action ;
- je veux vivre quelque chose avec mon Cercle ;
- surprends-moi, mais doucement ;
- je suis disponible pour une vraie secousse.

### Gestes

- swipe à droite : choisir ou ajouter à l'itinéraire ;
- swipe à gauche : pas maintenant ;
- toucher : ouvrir les détails ;
- boutons visibles équivalents pour tous les gestes.

Un swipe gauche est un signal contextuel, faible et temporaire. Il ne modifie jamais le Profil du Moteur.

Une raison facultative peut préciser : durée, intensité, format, sujet, disponibilité du Cercle, expérience déjà connue ou autre.

## 10. Ligne de jeu

La liberté ne doit pas rendre la trajectoire invisible. Une vue **Ma ligne de jeu** rassemble :

- une expérience active ;
- deux cartes au maximum en réserve ;
- les expériences ou rencontres programmées ;
- les expériences accomplies récemment ;
- le prochain rite ou passage de Monde.

Cette limite évite l'accumulation d'expériences commencées et jamais intégrées.

## 11. Recommandation explicable

Chaque carte recommandée expose `Pourquoi maintenant ?` :

```text
Cette expérience t'est proposée parce qu'elle travaille la Communication,
correspond aux vingt minutes dont tu disposes et peut être vécue avec ton
Cercle actuel.
```

La fiche d'explication peut montrer :

- les raisons utilisées ;
- leur confiance ;
- les prérequis ;
- une alternative ;
- une action pour corriger ou désactiver une source.

Le joueur doit pouvoir demander, par exemple :

> Ne te sers pas de mes Graines pour cette recommandation.

Le système classe des options, pas des personnes. Il ne transforme pas une hypothèse pédagogique en diagnostic.

### Entrées candidates

- Monde et droits accessibles ;
- Appel et objectifs déclarés ;
- Puissances explorées et confiance associée ;
- expériences accomplies ;
- Graines et Résonances dont l'usage a été consenti ;
- temps, formats et intensité souhaités maintenant ;
- préférence individuel, relationnel ou action ;
- Cercle, événements et ressources disponibles ;
- prérequis et sécurité ;
- verticales choisies.

Un refus ou un swipe ne met jamais à jour directement le Moteur. Seules des expériences, preuves, répétitions et intégrations contextualisées peuvent contribuer à une nouvelle hypothèse.

## 12. Sécurité

Une expérience intense peut exiger :

- Cercle stable ;
- facilitateur ;
- consentement spécifique ;
- préparation ;
- protocole d'arrêt ;
- intégration différée ;
- contexte approprié.

Une carte non accessible peut montrer un horizon et proposer le passage préparatoire :

> Cette expérience correspond à ton Appel, mais demande un Cercle préparé. Voici le passage accessible aujourd'hui.

Le Freeride n'est jamais une autorisation à brûler les étapes.

## 13. Oméga et progression

- aucun Oméga pour swiper ou accepter une recommandation ;
- Oméga uniquement pour une expérience accomplie selon ses critères ;
- aucune pénalité pour `Pas maintenant` ou pour le saut d'une expérience optionnelle ;
- les expériences libres ne remplacent pas les rites requis ;
- le passage de Monde ne dépend pas d'un simple total d'Oméga ;
- le rejeu mécanique ne produit pas un gain illimité ;
- une nouvelle traversée peut être reconnue si elle produit un nouveau contexte, une Graine, une preuve ou une contribution pertinente.

L'interface distingue toujours :

- progression dans le Monde ;
- ligne de jeu ;
- expériences accomplies ;
- Oméga ;
- état du Moteur.

## 14. Métadonnées à préparer

Chaque expérience devra progressivement exposer :

- accroche courte ;
- format principal ;
- durée ;
- intensité ;
- modalité individuelle ou collective ;
- prérequis ;
- conditions de sécurité et d'accessibilité ;
- déplacement principal ;
- Puissances associées ;
- validation ;
- illustration et mode d'affichage ;
- raisons éditoriales candidates de recommandation.

Les noms de colonnes ou le besoin d'une migration doivent être vérifiés dans l'application avant implémentation. Cette liste décrit un contrat éditorial cible, pas encore un schéma Rails.

## 15. Trajectoire produit

### Lot A — amélioration actuelle

1. créer un composant réutilisable de carte-couverture ;
2. l'utiliser en tête des fiches d'expérience ;
3. ajouter ou dériver une accroche courte ;
4. créer la scène d'image adaptable ;
5. déplacer les informations techniques sous `Voir les détails` ;
6. clarifier statut et validation ;
7. rendre les actions dépendantes du contexte ;
8. décliner une version compacte sur la page du parcours.

### Lot B — préparation du Monde 1

1. qualifier les métadonnées du catalogue ;
2. proposer trois parcours déterministes et explicables : conscientisation, circulation et élan ;
3. tester la compréhension de `Pourquoi maintenant ?` ;
4. ne générer aucune expérience par IA.

### Lot C — ouverture du Monde 2

1. mains contextuelles ;
2. ligne de jeu ;
3. expériences individuelles, relationnelles et collectives ;
4. persistance des choix `Pas maintenant` à faible durée de vie ;
5. programmation d'événements et expériences de Cercle ;
6. garde-fous d'intensité.

### Lot D — horizon ultérieur

1. assemblages adaptatifs d'expériences éprouvées ;
2. détection de passages peu balisés ;
3. prototypes générés, explicitement expérimentaux, versionnés et soumis à retour ou validation humaine.

## 16. Hors périmètre immédiat

La validation du principe ne commande pas encore :

- les gestes de swipe ;
- la pile de cartes ;
- la persistance d'une main ;
- le moteur adaptatif ;
- l'apprentissage automatique à partir des refus ;
- la génération d'expériences ;
- la refonte du modèle de données.

Le chantier immédiatement autorisé par cette décision est la **carte-couverture réutilisable et la réorganisation progressive de la fiche actuelle**. Toute implémentation du Freeride doit faire l'objet d'un lot séparé.
