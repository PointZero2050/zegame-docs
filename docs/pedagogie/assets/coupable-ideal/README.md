# Le Coupable idéal — illustrations du procès

> Ajout Codex - 2026-07-27. Série générée avec l'outil ImageGen intégré, après inspection de la
> V2 livrée par Claude (`zegame-app` commit `851a132`). Ces fichiers sont des assets de production
> proposés ; ils ne sont pas encore intégrés dans l'application ni déployés sur le serveur.

## Direction retenue

Les figures sortent volontairement de la famille de personnages utilisée dans **Une drôle
d'époque**. Le Procureur et l'Avocat ne sont pas deux humains costumés, mais deux **fonctions
archétypales** propres au procès :

- le **Procureur** incarne la ligne, la coupe, la limite et la pièce à conviction ;
- l'**Avocat** incarne l'arche, la couture, le lien et la réversibilité ;
- le **Réel** n'est pas un personnage : il apparaît comme une déchirure de lumière simple qui
  traverse les cartes causales et met leurs limites en évidence.

La matière reste néoarchaïque : bas-relief de papiers minéraux déchirés, cartographies civiques du
futur, obsidienne, craie, violet Point Zéro, turquoise oxydé et corail discret. Aucun jaune ou doré
n'est utilisé, conformément à la convention de la roue collective.

## Fichiers

| Fichier | Format | Usage principal proposé |
|---|---:|---|
| `proces-cour-causes-uniques-v1.png` | 1672 × 941 · 16:9 | Contrat, banc des accusés, sous l'accusation ; image-seuil de la Cour |
| `proces-procureur-archetype-v1.png` | 1448 × 1086 · 4:3 | Réquisitoire ; texte ou formulaire dans l'espace clair à droite |
| `proces-avocat-archetype-v1.png` | 1448 × 1086 · 4:3 | Plaidoirie ; texte ou formulaire dans l'espace clair à gauche |
| `proces-le-reel-v1.png` | 1672 × 941 · 16:9 | Contre-interrogatoire, transition vers le verdict |

La roue finale ne reçoit pas d'illustration supplémentaire : elle doit rester l'objet visuel
principal de la restitution.

## Intégration UX recommandée

### Écrans 0 à 2 — la Cour

Utiliser la vue large comme image-seuil, idéalement avant le titre ou entre le titre et le premier
texte. La chaise vide représente l'accusé variable ; ne pas incruster son nom dans l'image.

Alternative accessible :

> Dans une cour circulaire de papier minéral, le Procureur anguleux et l'Avocat fait d'arches se
> font face autour d'une chaise pliante vide. Une déchirure de lumière traverse le mur derrière elle.

### Écran 3 — le Procureur

Sur grand écran, grille image / formulaire. Sur mobile, image puis titre et formulaire. L'image
peut être recadrée entre `object-position: left center` et `center` ; préserver l'œil, la main qui
tient le fil et l'éventail des pièces.

Alternative accessible :

> Figure verticale d'obsidienne et de papier, le Procureur tient un éventail de pièces causales et
> tend un fil qui marque une limite.

### Écran 4 — l'Avocat

Reprendre la grille en miroir. Préserver la main ouverte, les fragments reliés et les grandes
arches réparées. Ne pas traiter la figure comme une présence apaisante : elle porte une complexité,
pas une absolution.

Alternative accessible :

> Figure de papier faite d'arches et de coutures, l'Avocat maintient séparés deux fragments de
> carte tout en les reliant par un fil turquoise.

### Écran 5 — le Réel

Utiliser la vue large comme respiration entre les trois objections et les questions, ou comme
bandeau d'entrée. L'image montre qu'une carte peut être intelligente et néanmoins insuffisante.

Alternative accessible :

> Une déchirure de lumière traverse un mur de cartes causales ; une racine, un câble noué et des
> fragments contradictoires débordent des tracés ordonnés.

### Écrans 6 à 8

- Graine : retour discret à un détail de la Cour, si nécessaire ; ne pas introduire un troisième
  personnage psychologique.
- Verdict : la déchirure du Réel peut revenir en bandeau fin.
- Roue : aucune image narrative concurrente.

## Responsive et performance

- conserver les originaux comme masters ;
- produire lors de l'intégration des dérivés WebP ou AVIF adaptés, sans écraser les PNG ;
- prévoir au minimum des largeurs de 480, 960 et 1600 px pour les vues 16:9, et 480 / 960 / 1448 px
  pour les figures 4:3 ;
- réserver les dimensions dans le HTML pour éviter le déplacement de mise en page ;
- ne pas charger les quatre masters sur chaque écran ;
- ne porter aucune information uniquement par l'image.

## Prompts de production

### Procureur

> Figure archétypale originale incarnant la fonction qui nomme le dommage, trace les limites et
> établit la responsabilité : présence adulte verticale faite de strates de papier minéral,
> visage asymétrique d'obsidienne à un œil clair, éventail de pièces causales et fil tendu ; collage
> néoarchaïque civique, violet, craie, corail discret, sans costume judiciaire ni symbole sacré.

### Avocat

> Figure archétypale originale incarnant la fonction qui retrouve le besoin légitime et préserve
> ce qui ne doit pas être perdu : présence adulte large faite d'arches, de coutures et de ponts en
> papier minéral, deux fragments maintenus séparés mais reliés par un fil turquoise ; même monde
> néoarchaïque que le Procureur, sans costume judiciaire ni figure de sage.

### Cour des causes uniques

> Mettre les deux archétypes face à face dans une chambre civique circulaire de papier minéral,
> autour d'une chaise pliante vide et d'un dossier anonyme. Une déchirure verticale de lumière
> traverse l'architecture et interrompt leurs géométries. Autorité visuelle égale, aucun vainqueur,
> aucun texte, aucun jaune ou doré.

### Le Réel

> Représenter le Réel comme une déchirure de lumière traversant un mur de cartes causales fermées,
> jamais comme une personne ou une divinité. Une racine traverse la grille, un câble est réparé par
> un nœud ordinaire et des fragments contradictoires restent reliés sans fusionner ; collage
> néoarchaïque sobre, aucune imagerie mystique.

## Garde-fous

- ne pas transformer le Procureur en Ombre et l'Avocat en Lumière ;
- ne pas féminiser ou masculiniser implicitement les deux fonctions ;
- ne pas ajouter de toge, perruque, marteau, balance ou palais de justice réaliste ;
- ne pas faire du Réel une autorité omnisciente ;
- ne pas réintroduire les personnages récurrents d'`Une drôle d'époque` ;
- ne pas placer ces figures dans la roue des polarités.
