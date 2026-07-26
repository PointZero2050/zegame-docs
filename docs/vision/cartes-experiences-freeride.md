# Cartes-couvertures d'expérience et mode Freeride

> Ajout Codex - 2026-07-25. Architecture UX validée par Boris après inspection de la fiche d'expérience déployée sur `vibe.ze.game`.
>
> **Décision immédiate** : améliorer les fiches actuelles avec une carte-couverture mobile-first réutilisable.
>
> **Extensions validées le 2026-07-25** : une expérience fondée sur une vidéo adopte une variante vidéo-first ; la zone d'action indique la prochaine action réelle du joueur plutôt qu'un bouton générique de validation. Ces décisions préparent l'UX sans commander un moteur générique de workflows.

> **Extension validée le 2026-07-26** : la navigation `Précédent / Déroulé / Suivant` remonte sous
> la couverture ; les Puissances deviennent des cartes explicatives ; le média ou geste principal
> précède toute déclaration d'achèvement. Décision issue de l'audit des fiches déployées du Monde 0.
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

### Variante vidéo-first

Lorsqu'une vidéo porte l'entrée narrative ou le contenu principal, la couverture devient une **affiche vidéo**, pas une fiche contenant un lecteur secondaire :

- la scène d'image sert de poster 16:9 ;
- un bouton de lecture central et le CTA `Regarder… · n min` rendent le média immédiatement identifiable ;
- la durée distingue vidéo et expérience complète ;
- aucun son ni contenu essentiel ne démarre automatiquement ;
- la vidéo s'ouvre dans un mode immersion sur la même URL ;
- la fin du film propose directement la prochaine action de l'expérience, sans retour à la fiche ni second bouton `Commencer`.

Exemple :

```text
Le Point Zéro : entrer dans le Jeu

Et si la crise du monde était aussi une crise de nos récits ?

Vidéo 5 min · Expérience complète 12 min · 6 Ω

[ Regarder le prologue · 5 min ]
```

Pendant le visionnage :

- le lecteur occupe l'espace principal, en largeur complète sur mobile ;
- le reste de l'interface s'efface sans rompre la navigation ;
- sous-titres, transcription, clavier et lecteurs d'écran restent pris en charge ;
- la position de lecture peut être mémorisée pour afficher `Reprendre à 03:12` ;
- la fin du lecteur est éditorialisée : elle ouvre l'action suivante et ne montre aucune recommandation vidéo étrangère.

La vidéo peut être accompagnée d'une synthèse courte et d'une transcription. Cette trace écrite sert l'accessibilité, la mémorisation et le retour ultérieur ; elle n'est pas un doublon obligatoire à lire.

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

1. **Vivre l'expérience** — média, jeu, pratique ou interaction principale ;
2. **À quoi t'attendre** — promesse développée, sans répéter l'accroche de couverture ;
3. **Ce que cette expérience met en mouvement** — Puissances et polarités ;
4. **Comment ce passage sera reconnu** — trace, autorité de validation et état actuel ;
5. **Conditions** — prérequis, intensité, collectif, sécurité et accessibilité ;
6. **Ressources complémentaires** ;
7. **Oméga** — montant et logique d'attribution.

Une ressource indispensable à l'expérience n'est jamais classée dans les ressources complémentaires.
Pour une expérience vidéo-first, la vidéo ou son bouton de lecture apparaît avant toute action de
complétion.

### Deux contextes de détail

- **Lien direct ou parcours structuré** : couverture puis détails sous la même URL, accessibles par ancre.
- **Futur deck** : toucher la carte ouvre les mêmes détails dans un écran superposé plein format ou une feuille remontante. Fermer restitue exactement la position dans la main.

La fiche conserve une URL canonique unique. Le deck ne duplique pas son contenu.

### Barre d'orientation sous la couverture

La navigation de séquence remonte immédiatement sous la carte-couverture :

```text
[ ← Précédente ]   [ Voir le déroulé ↓ ]   [ Suivante → ]
```

- `Voir les détails →` devient `Voir le déroulé ↓`, car l'action descend sur la même page ;
- la barre reste secondaire face au CTA principal de l'expérience ;
- sur mobile, les trois commandes restent lisibles et disposent de zones tactiles suffisantes ;
- la première expérience d'un parcours ou d'un chapitre ne pointe pas vers une ancienne Page non
  cliquable : l'action est absente ou devient `Retour au parcours` selon le contexte ;
- précédent et suivant sont résolus depuis l'inclusion courante et les règles d'accessibilité du
  parcours, pas depuis une hypothèse globale sur le `Challenge`.

En bas de la fiche, ne pas dupliquer cette barre. Afficher une carte de continuité plus engageante :

```text
Étape suivante
Une drôle d'époque
20 min · 3 Ω
[ Continuer le parcours ]
```

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

### Le CTA décrit la prochaine action

Le CTA principal ne doit pas être figé autour de `Commencer` et `Valider`. Il décrit l'action concrète immédiatement disponible et évolue avec la traversée :

| État | Exemple de CTA | Indication |
|---|---|---|
| Non commencé | `Discuter avec le mentor` | Étape 1 sur 2 · Explorer |
| En cours | `Reprendre la conversation` | Conversation en cours |
| Trace prête | `Produire ma Graine de Récit` | Étape 2 sur 2 · Créer |
| Soumission requise | `Envoyer au facilitateur` | Dernière étape |
| En attente | `Voir ma Graine` | En attente de validation |
| Accomplie | `Voir ma Graine` | 6 Ω obtenus |

L'expression `Étape n sur n` décrit la progression dans l'expérience. Le mot `validation` est réservé au moment où une confirmation déclarative, système ou humaine est réellement attendue.

### L'action réelle précède la complétion

La fiche ne propose jamais `J'ai réalisé cette expérience` avant d'avoir rendu son média, son jeu ou
sa pratique principale directement accessible.

| État vidéo-first | Action principale |
|---|---|
| Non commencée | `Regarder la vidéo · 2 min` |
| Lecture interrompue | `Reprendre à 01:24` |
| Vidéo terminée, action requise | `Faire l'action suivante` |
| Confirmation déclarative légitime | `Confirmer mon passage` |
| Accomplie | `Revoir` ou `Rejouer`, en secondaire |

Un mécanisme observable utilise de préférence une validation système. Une déclaration autonome
reste possible lorsque le système ne peut raisonnablement observer le geste, mais son libellé
décrit ce que le joueur confirme.

### Rendre les Puissances intuitives

La section porte le titre **Ce que cette expérience met en mouvement** et commence par un résumé :

```text
3 Puissances mobilisées · 3 Ω disponibles
Ces indications décrivent ce que l'expérience exerce, pas ta personnalité.
```

Chaque association compétence–expérience devient une carte lisible :

```text
┌────────────────────────────────────────┐
│ ◉ IMAGINATION                    +1 Ω │
│ Projection                             │
│ Ombre ─── Point Zéro ─── LUMIÈRE       │
│ Cette expérience travaille le versant  │
│ Lumière de l'Imagination.              │
└────────────────────────────────────────┘
```

La carte expose :

- la Puissance, avec signe ou mini-lemniscate stable ;
- l'aspect mobilisé, par exemple `Projection`, `Conviction` ou `Service` ;
- l'axe `Ombre — Point Zéro — Lumière`, avec le versant travaillé mis en évidence ;
- les Oméga attribués à cette association ;
- un lien facultatif `Comprendre cette Puissance` vers sa fiche.

Les cartes s'empilent sur mobile et forment une grille de deux ou trois colonnes sur grand écran.
La couleur renforce la lecture sans porter seule l'information.

Ne pas afficher la chaîne technique brute `Point Zéro - Puissance - Lumière/Ombre`. Elle est
traduite en langage joueur. La polarité décrit le versant exercé par l'expérience, jamais un niveau
ou une identité attribués au joueur.

Avant rendu, vérifier la cohérence entre le nom de la compétence et son framework dérivé. L'audit du
26 juillet 2026 a relevé sur `L'écosystème Point Zéro` : `INTUITION : CONVICTION` associé à
`Point Zéro - Communication - Lumière`. Cette donnée contradictoire doit être corrigée à la source,
pas seulement masquée dans l'interface.

### Métadonnées en langage joueur

- `Validation Autonome` quitte la couverture ; afficher `À confirmer par toi` seulement lorsque
  cette autorité est réellement requise ;
- `0 / 3 Ω` devient `3 Ω à gagner` ;
- `3 / 3 Ω` devient `3 Ω gagnés` ;
- une rangée d'étoiles non expliquée devient par exemple `Intensité douce · 1/5` ;
- le titre de l'expérience est le `h1` de la page ; les sections utilisent des `h2` cohérents ;
- une illustration porteuse de sens reçoit une alternative accessible ;
- les tags, liens secondaires et états accomplis ou verrouillés respectent les contrastes attendus.

### Séparer action, preuve, validation et récompense

Une expérience possède quatre dimensions distinctes :

| Dimension | Question |
|---|---|
| Parcours d'action | Que doit faire le joueur ? |
| Preuve de traversée | Quelle trace montre que l'expérience a eu lieu ? |
| Autorité de validation | Qui ou quoi confirme l'achèvement ? |
| Récompense | Quand les Oméga sont-ils attribués ? |

Trois autorités de validation sont distinguées :

1. **déclarative** — le joueur confirme une action que le système ne peut raisonnablement observer ;
2. **système** — une trace vérifiable existe, par exemple une partie terminée, une Graine créée ou un questionnaire envoyé ;
3. **facilitateur** — une présence, une pratique collective ou une production à enjeu exige une confirmation humaine.

Une IA peut accompagner la production d'une Graine. Le système peut vérifier que cette Graine existe. Ni l'un ni l'autre ne doivent en déduire automatiquement sa qualité, sa profondeur ou un niveau de conscience.

Exemples :

```text
Regarder le prologue
    → jouer au Coupable idéal
    → obtenir la Carte narrative
    → validation système et attribution des Ω

Préparer l'Atelier
    → participer à l'Atelier
    → validation par le facilitateur
    → attribution des Ω
```

### Trajectoire technique proportionnée

La carte-couverture prépare dès maintenant une zone `prochaine action` capable d'afficher :

- libellé contextualisé ;
- `Étape n sur n` ;
- état disponible, en cours, en attente ou terminé ;
- action de reprise différente de l'action initiale ;
- éventuelle action secondaire.

La première version peut configurer ces éléments expérience par expérience et conserver le moteur de validation existant.

Dans un second temps, quelques expériences pilotes peuvent dériver leur état depuis des traces métier déjà présentes : conversation commencée, Graine créée, session terminée, Carte conservée ou demande de validation envoyée. Un résolveur de présentation peut traduire ces traces en :

`not_started → in_progress → evidence_ready → submitted → validated`

Ce résolveur ne doit pas attribuer lui-même les Oméga. La validation finale reste idempotente et passe par le mécanisme métier prévu.

Un modèle générique d'étapes, conditions et branchements ne sera envisagé qu'après observation de plusieurs expériences réellement répétitives. Il n'appartient pas au lot actuel.

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

Pour les expériences multiétapes, préparer également sans présumer du schéma Rails :

- libellé de l'action initiale ;
- libellé de reprise ;
- progression éditoriale `Étape n sur n` ;
- type de trace attendue ;
- autorité de validation ;
- action disponible après accomplissement.

Les noms de colonnes ou le besoin d'une migration doivent être vérifiés dans l'application avant implémentation. Cette liste décrit un contrat éditorial cible, pas encore un schéma Rails.

## 15. Trajectoire produit

### Lot A — amélioration actuelle

1. créer un composant réutilisable de carte-couverture ;
2. l'utiliser en tête des fiches d'expérience ;
3. ajouter ou dériver une accroche courte ;
4. créer la scène d'image adaptable ;
5. déplacer les informations techniques sous `Voir les détails` ;
6. créer la variante vidéo-first et sa sortie directe vers l'action suivante ;
7. remplacer le CTA générique par une zone `prochaine action` contextualisable ;
8. clarifier séparément progression, trace, validation et attribution des Oméga ;
9. rendre les actions dépendantes du contexte ;
10. remonter la barre `Précédente / Déroulé / Suivante` sous la couverture ;
11. remplacer les étiquettes techniques de Puissances par des cartes explicatives ;
12. corriger les incohérences compétence/framework avant affichage ;
13. décliner une version compacte sur la page du parcours.

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
- le moteur générique d'étapes, conditions et branchements ;
- la refonte du modèle de données.

Le chantier immédiatement autorisé par cette décision est la **carte-couverture réutilisable, sa variante vidéo-first, la zone de prochaine action et la réorganisation progressive de la fiche actuelle**. Les libellés et états peuvent d'abord être spécifiques aux expériences pilotes. Toute généralisation du workflow ou implémentation du Freeride doit faire l'objet d'un lot séparé et, pour les zones sensibles, d'une analyse d'impact.
