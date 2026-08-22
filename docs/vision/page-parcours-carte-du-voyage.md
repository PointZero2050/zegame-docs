# Page parcours — la carte du voyage

> Ajout Codex - 2026-07-25. Architecture UX validée par Boris après inspection en lecture de la
> page déployée du Monde 0 sur `vibe.ze.game`, aux formats ordinateur et mobile 390 × 844.

> **Révision Codex — 2026-08-22.** Les maquettes validées
> `parcours-monde-0-cible/` et `experience-monde-0-cible/` précisent cette architecture : la
> carte du voyage et l'expérience sont désormais deux pages distinctes. La première oriente et
> situe ; la seconde fait agir, explique la reconnaissance et expose le détail pédagogique.

## 1. Décision

La page ordonnée d'un parcours devient la **carte du voyage** du joueur.

Elle ne doit être :

- ni une fiche administrative suivie d'une longue liste ;
- ni un catalogue d'expériences interchangeables ;
- ni un deck Freeride.

Elle raconte un chemin, situe le joueur et rend son prochain passage évident. Sa hiérarchie répond
dans cet ordre à quatre questions :

1. Où suis-je ?
2. Quelle expérience m'appelle maintenant ?
3. Qu'ai-je déjà traversé ?
4. Vers quel seuil ce parcours me conduit-il ?

Le Monde 0 reste une trajectoire commune écrite. Le futur Freeride ouvre un axe horizontal à partir
du Monde 2, sans remplacer cette page verticale ni ses rites.

## 2. Diagnostic de la page déployée

L'audit du 25 juillet 2026 montre :

- un premier écran mobile presque entièrement occupé par la description du parcours, ses tags et
  la ventilation des Oméga ;
- la première expérience située après environ 900 px de défilement ;
- aucune prochaine action explicite au-dessus de la ligne de flottaison ;
- un `38 %` dont la sémantique n'est pas compréhensible sans connaître le calcul ;
- `30 / 96 Ω` présenté à proximité de ce pourcentage, ce qui mélange progression et récompense ;
- trois chapitres nommés seulement `Chapitre 1`, `Chapitre 2` et `Chapitre 3` ;
- treize cartes presque équivalentes visuellement, malgré leurs rôles très différents ;
- la répétition de `Validation Autonome` sur chaque carte ;
- un engrenage peu explicite pour signaler l'expérience courante ;
- des expériences verrouillées rendues très pâles, avec un contraste insuffisant ;
- un léger débordement horizontal à 390 px ;
- l'Atelier Point Zéro, rite de passage, traité comme une carte ordinaire en fin de liste.

La page contient les bonnes données. Le problème principal est leur ordre de priorité.

## 3. Architecture cible

### 3.1. Premier écran

Le premier écran utile contient :

1. un retour vers la Marelle ;
2. le Monde, le titre du parcours et une promesse de deux ou trois lignes au maximum ;
3. une mini-progression narrative par chapitres ;
4. si le parcours n'est pas commencé, le CTA principal `Commencer le parcours` ;
5. s'il est actif, un rappel compact de l'expérience courante et le CTA `Reprendre
   l'expérience`.

La description longue, les tags et la ventilation détaillée des Oméga descendent sous cette zone.
Le label générique `Validation Autonome` disparaît de l'en-tête du parcours.

Exemple de hiérarchie :

```text
← Retour à la Marelle

MONDE 0 · ENTRER DANS LE JEU
Le monde ne s'est pas cassé tout seul.
Bonne nouvelle : sa suite non plus.

[ Je pressens ✓ ]—[ Je relie ● ]—[ Je prends place ○ ]

EXPÉRIENCE EN COURS
┌─────────────────────────────────────────┐
│ Illustration                            │
│ L'écosystème Point Zéro                 │
│ Découvre comment les pièces commencent  │
│ à former une constellation.             │
│ Vidéo · 5 min · 3 Ω                     │
│ [ Reprendre l'expérience ]              │
└─────────────────────────────────────────┘

4 expériences accomplies
30 Ω gagnés · 96 Ω disponibles
```

Le CTA ouvre toujours la **page de l'expérience**. La page parcours ne duplique ni le bloc
d'action, ni la séquence détaillée, ni le mécanisme de reconnaissance. Elle peut annoncer la
prochaine action en une phrase pour orienter, mais ne permet jamais de l'accomplir directement.

Sur mobile, un CTA compact peut rester fixé au-dessus de la navigation basse tant que le passage
vers l'expérience n'est pas visible :

`Continuer · 5 min`

Il disparaît lorsque le rappel de l'expérience courante entre dans la zone visible afin d'éviter deux CTA
concurrents.

### 3.2. Progression narrative

La progression principale n'est pas un pourcentage abstrait. Elle montre les mouvements du parcours.

Pour le Monde 0 :

| Chapitre technique | Mouvement visible | Fil rouge |
|---|---|---|
| Chapitre 1 | **Je pressens** | **Qui a cassé le monde ?** |
| Chapitre 2 | **Je relie** | **La constellation** |
| Chapitre 3 | **Je prends place** | **La chaise vide** |

Chaque mouvement expose :

- son état : accompli, actuel ou à venir ;
- son nombre d'expériences requises accomplies ;
- une accroche courte ;
- une illustration ou une texture de chapitre ;
- sa Graine de Récit lorsqu'elle existe.

Les noms techniques `Chapitre n` peuvent rester disponibles pour l'administration et
l'accessibilité, mais ne constituent plus le titre principal montré au joueur.

### 3.3. Déploiement progressif des chapitres

Afin de réduire la longueur de page :

- le chapitre actuel est ouvert ;
- un chapitre accompli est replié en un résumé valorisant, dépliable à la demande ;
- un chapitre futur montre sa promesse et son état, sans nécessairement afficher toutes ses cartes ;
- tous les contenus restent accessibles sans changer d'URL.

Un accordéon ne doit pas cacher l'architecture générale : les trois mouvements et le rite final
restent toujours visibles.

### 3.4. Cartes d'expérience compactes

La page parcours réutilise une variante compacte du composant de
[carte-couverture](cartes-experiences-freeride.md). Elle ne duplique pas une seconde grammaire de
cartes.

Une carte compacte montre seulement :

- médaillon ou illustration ;
- titre ;
- accroche sur une ligne, deux au maximum ;
- format, durée et Oméga ;
- état explicite ;
- CTA uniquement pour l'expérience qui demande l'attention.

Le mode de validation n'est pas répété dans la liste. Il apparaît dans la fiche détaillée ou dans
la formulation du passage vers l'expérience.

États visibles recommandés :

| État métier | Présentation |
|---|---|
| accomplie | `Accomplie` et coche, carte compacte |
| courante non commencée | `Prochaine étape` et CTA |
| commencée | `À reprendre` et CTA |
| verrouillée | `À venir après…`, contenu lisible et raison accessible |
| optionnelle | `Détour facultatif` |
| passée | `Passée pour l'instant`, reprise possible |
| en attente humaine | `En attente du facilitateur` |
| rite | `Rite de passage` avec traitement distinct |

Ne pas utiliser seulement une couleur, une opacité, un cadenas ou un engrenage pour porter un état.

### 3.5. Deux progressions distinctes

La page sépare :

1. **la progression du chemin requis** ;
2. **l'exploration Oméga disponible**.

Exemple :

```text
4 étapes requises accomplies · Chapitre 1 terminé
30 Ω gagnés · 66 Ω encore accessibles
```

Règles :

- une expérience optionnelle non réalisée ou passée ne bloque pas l'accomplissement ;
- elle reste comptée dans les Oméga encore accessibles ;
- le Sas optionnel ne doit pas empêcher `Monde 0 accompli` ;
- l'Atelier et la Graine de passage restent requis ;
- un pourcentage ne peut être affiché que si son dénominateur est explicite et stable.

La V1 doit préférer des comptes compréhensibles à un pourcentage composite.

### 3.6. Ventilation par puissance

Le détail `Communication : Écoute`, `Émotion : Passion`, etc. ne précède plus le parcours.

Il devient une restitution secondaire repliable :

```text
Ce que tu as déjà mis en mouvement
3 Puissances ont produit des Oméga.
[ Voir le détail ]
```

Le détail conserve les attributions réelles par compétence. Il ne prétend pas évaluer le niveau de
conscience du joueur.

### 3.7. Seuil et rite de passage

Le rite final est une destination de la carte du voyage, pas la douzième carte d'une liste.

Pour le Monde 0 :

```text
PASSAGE VERS LE MONDE 1

Vivre l'Atelier Point Zéro
Le rite collectif qui ouvre la suite.
Présentiel ou distanciel · 3 h · 24 Ω

[ Voir les prochaines dates ]
```

Même verrouillé, ce seuil reste visible et explique ses prérequis. Le Sas apparaît à proximité
comme `Préparation facultative`, et non comme une condition implicite du passage.

La validation de présence par un facilitateur doit être nommée. La page n'annonce jamais une
ouverture du Monde 1 sur le seul total d'Oméga.

### 3.8. Frontière entre parcours et expérience

La séparation est un contrat de navigation, pas seulement une variante graphique.

La **page parcours** porte :

- la synthèse du parcours : Monde, description, durée, nombre d'expériences, Puissance globale,
  Omégas disponibles et Puissances dominantes ;
- la position du Joueur dans les chapitres ;
- les états accomplie, courante, verrouillée, optionnelle et en attente ;
- les chapitres repliables, le seuil et le rite final ;
- un CTA qui ouvre l'expérience pertinente.

La **page expérience** porte :

- le lien de retour vers le parcours et le rappel du chapitre ;
- la promesse, les métadonnées détaillées, l'intensité `/5` et l'échelle d'effet `/5` ;
- les Puissances mobilisées, leurs Omégas réels, leur polarité et le verbe canonique associé ;
- la séquence éditoriale en trois gestes et l'étape en cours ;
- le bloc d'action réel et son CTA ;
- la manière dont le passage sera reconnu ;
- les ressources complémentaires et l'étape suivante.

Une même information peut être résumée sur la page parcours puis détaillée sur la page expérience,
mais aucune action métier n'est dupliquée. Un CTA de parcours navigue ; seul le dispositif réel de
l'expérience peut produire une Trace, demander une reconnaissance, valider un Challenge ou ouvrir
une attribution d'Omégas.

#### Arbitrages de migration de la page fusionnée

- La voix narrative du parcours reste présente dans l'en-tête actif. Les compteurs de progression
  l'accompagnent comme repères secondaires ; ils ne la remplacent pas.
- L'Atelier reste visible dans le chapitre 3, avec un traitement de **rite** distinct d'une ligne
  ordinaire. Ses Omégas sont comptés exactement une fois dans le chapitre et dans le parcours.
- Le bandeau technique `Franchi / En cours / À venir` peut disparaître si l'en-tête actif nomme
  explicitement le chapitre et l'expérience en cours et si le fil distingue tous les états.
- `À propos de ce parcours` et `Ce que tu as déjà mis en mouvement` ne survivent pas comme blocs
  autonomes lorsqu'ils dupliquent la synthèse, la progression et la ventilation déjà visibles.
- `Mon récit de passage` reste la dernière expérience du fil. Après sa reconnaissance, le CTA de
  clôture du parcours devient `Refermer le livre` ; avant cela, la reprise passe toujours par
  l'expérience courante.
- `Niveau /10` qualifie uniquement la Puissance globale du **parcours**. Une expérience affiche
  seulement son intensité `/5` et son échelle d'effet `/5`.
- Le titre public du bloc est `Comment ce passage sera reconnu`. À l'intérieur, `Autorité` nomme
  la personne ou le dispositif habilité à reconnaître le passage.

#### Invariants de portage et dégradation propre

- La durée du parcours distingue la durée **obligatoire** du supplément **facultatif**. Elle ne
  les additionne pas dans un total ambigu.
- Un parcours sans fiche YAML reste utilisable : il conserve titre, progression réelle, expérience
  courante et navigation, et omet simplement Puissance globale, intensité, effet et séquence. Il
  n'invente aucune valeur de remplacement.
- Deux états vides sont rédigés et testés : `Tout est accompli` lorsque le chemin est terminé ;
  `Aucune expérience n'est ouverte pour l'instant` lorsque la progression ne fournit pas de suite.
- Le compte d'Omégas d'un chapitre conserve la borne d'irrévocabilité : le total affiché ne peut
  jamais être inférieur aux Omégas déjà gagnés par le Joueur. Une évolution éditoriale du parcours
  ne doit donc jamais produire un affichage du type `27 / 24 Ω`.
- Le badge de chapitre accompli et la texture ou illustration du chapitre survivent. L'état reste
  lisible en texte ; le badge et l'image renforcent la lecture sans la remplacer.
- La ligne `.experience-row` est une variante propre à la liste du parcours. Elle ne remplace pas
  globalement `_cover_card`, encore utilisé pour `Étape suivante` et d'autres surfaces.
- La page expérience affiche un lien de retour vers le parcours, le chapitre et le rang réel
  `Expérience X sur Y`. Ce rang vient de la composition effective du Journey.
- Si le verbe canonique d'un chip manque, l'interface affiche **Puissance + polarité**, sans blanc
  disgracieux et sans inventer de verbe. L'absence est journalisée pour corriger la configuration.
- La maquette `?step=2` illustre la séquence mais ne constitue pas une source d'état. Tant qu'un
  index courant ne peut pas être dérivé d'une action, d'une preuve ou d'un état métier existant,
  les trois gestes sont présentés comme une carte de l'expérience sans en déclarer un « en cours ».
  Aucun `current_step` générique ne doit être créé uniquement pour satisfaire le visuel.
- Le portage de la page expérience précède ou accompagne le retrait des blocs correspondants de la
  page parcours. Intensité, effet, séquence et reconnaissance ne connaissent aucune fenêtre de
  disparition entre deux livraisons.

## 4. Ton et microcopie

La page suit la [voix Point Zéro](voix-point-zero.md) : adulte, concrète, légèrement décalée et
piquante. Le décalage se place surtout dans les accroches et transitions ; les actions restent
explicites.

Exemples à tester :

- `Le monde ne s'est pas cassé tout seul.`
- `Reprendre le fil`
- `Le jeu continue ici`
- `Pas encore. Il reste une porte à ouvrir.`
- `Détour facultatif — pour pousser un peu plus loin`
- `Une chaise est encore vide. Étrangement, elle t'attend.`

Éviter :

- la félicitation automatique ;
- les injonctions de coach ;
- l'humour sur l'intimité ou la vulnérabilité du joueur ;
- les CTA poétiques dont l'action réelle serait ambiguë.

## 5. Responsive et accessibilité

### Mobile

- aucun débordement horizontal à 320, 375 ou 390 px ;
- prochaine action identifiable dans le premier écran utile ;
- métadonnées sur une ligne stable ou dans des chips lisibles ;
- zone tactile minimale de 44 × 44 px ;
- CTA fixe placé au-dessus de la navigation basse, sans la masquer ;
- titres sans troncature lorsque le sens dépend de leur fin ;
- expérience verrouillée lisible malgré son état.

### Grand écran

- largeur de lecture limitée ;
- en-tête et prochaine action peuvent former deux colonnes ;
- la liste ne s'étire pas sur toute la largeur ;
- le chemin vertical ou segmenté reste lisible sans simuler un deck ;
- aucune image ne redevient un petit médaillon lorsque son rôle est de vendre l'étape courante.

### Images et poids

Les fichiers sources haute définition restent dans `zegame-prototypes`. Le portage applicatif
utilise des dérivés WebP dimensionnés par usage : miniature ou médaillon, fond de chapitre et
cover. Une image de plusieurs mégaoctets n'est jamais servie telle quelle dans une liste.

Objectifs initiaux, à vérifier dans le navigateur :

- médaillon : côté utile 256 à 384 px, idéalement moins de 150 Ko ;
- fond de chapitre : 1280 px de large au maximum, idéalement moins de 300 Ko ;
- cover : 1600 px de large au maximum, idéalement moins de 500 Ko.

Le poids final se tranche sur la qualité perçue et le chargement mobile. Les images hors écran sont
chargées paresseusement ; la cover visible au chargement ne l'est pas.

### Sémantique

- un seul `h1` pour le parcours ;
- chapitres en `h2`, expériences en `h3` ;
- texte alternatif utile pour les illustrations porteuses de sens ;
- état fourni par du texte accessible, pas uniquement par une icône ;
- accordéons utilisables au clavier avec état `aria-expanded` ;
- contrastes conformes, y compris pour les expériences verrouillées.

## 6. Impacts fonctionnels

### Réutiliser avant d'ajouter

La première version doit exploiter :

- l'ordre et les Pages déjà présents dans le parcours ;
- `progression_mode` ;
- `ChallengesJourney.required` et `optional_note` ;
- l'état de saut dans `ChallengesJourneysUser` ;
- les validations `ChallengesUser` existantes ;
- les totaux Oméga et répartitions par compétence existants ;
- la carte-couverture compacte en cours d'implémentation.

Avant toute migration, vérifier si la promesse courte du parcours et les accroches de chapitre
peuvent utiliser des champs existants ou une configuration éditoriale locale.

### Résolveur de présentation

La vue a besoin d'un état de présentation calculé, sans modifier les contrats métier :

- prochain chapitre ;
- prochaine expérience accessible ;
- expérience à reprendre ;
- nombre d'expériences requises accomplies ;
- nombre total d'expériences requises ;
- Oméga gagnés ;
- Oméga encore accessibles ;
- prochain rite et état de ses prérequis.

Ce calcul doit réutiliser les méthodes de progression existantes autant que possible. Ne pas
dupliquer les règles de déverrouillage dans la vue HAML.

### Backoffice

À vérifier ou préparer :

- promesse courte du parcours ;
- titre public et accroche des chapitres ;
- illustration ou texture de chapitre ;
- identification éditoriale du rite ;
- accroche courte des expériences, déjà requise par la carte-couverture.

Le statut obligatoire ou optionnel reste porté par l'inclusion `ChallengesJourney`.

## 7. Découpage d'implémentation

### Lot P0 — corriger la hiérarchie

1. raccourcir l'en-tête ;
2. remplacer `Retour à la page d'accueil` par `Retour à la Marelle` ;
3. afficher l'expérience courante et son CTA de navigation avant la liste ;
4. distinguer progression requise et Oméga ;
5. retirer `Validation Autonome` des cartes compactes ;
6. expliciter les états en texte ;
7. corriger le débordement horizontal mobile ;
8. corriger titres, contrastes et structure de headings.

### Lot P1 — raconter le voyage

1. donner aux chapitres leurs mouvements et fils rouges ;
2. ouvrir le chapitre actuel et replier les autres ;
3. distinguer visuellement expérience courante, détour facultatif et rite ;
4. déplacer la ventilation des Puissances dans une section secondaire ;
5. ajouter le seuil `Passage vers le Monde 1`.

### Lot P2 — enrichir sans changer le modèle

1. CTA mobile fixe contextuel ;
2. transitions légères entre mouvements ;
3. textures et illustrations de chapitre ;
4. animation sobre lors de l'ouverture d'un nouveau chapitre ;
5. mémorisation locale de l'état ouvert ou replié des chapitres.

## 8. Critères d'acceptation du premier lot

- [ ] À 390 × 844, le joueur voit le parcours, sa position et l'accès à l'expérience courante sans devoir
      parcourir la description longue ni la ventilation des Puissances.
- [ ] Une seule action principale de navigation est visible simultanément sur la page parcours.
- [ ] La prochaine expérience est calculée depuis les règles existantes.
- [ ] Le CTA ouvre la page expérience sans valider, reconnaître ni attribuer d'Omégas.
- [ ] Les expériences accomplies, courantes, verrouillées, optionnelles, passées et en attente sont
      distinguables sans dépendre uniquement de la couleur ou d'une icône.
- [ ] Le caractère optionnel du Sas est visible.
- [ ] L'Atelier est présenté comme rite requis pour ouvrir le Monde 1.
- [ ] Le chemin requis et les Oméga disponibles sont deux informations séparées.
- [ ] Une expérience optionnelle passée ne bloque ni le chapitre ni le parcours.
- [ ] Aucun débordement horizontal n'apparaît à 320, 375, 390, 768 et 1440 px.
- [ ] La navigation basse ne masque ni contenu ni CTA.
- [ ] La structure comporte un `h1`, des `h2` de chapitre et des `h3` d'expérience cohérents.
- [ ] La page reste utilisable sans animation.

## 9. Hors périmètre

Ce chantier n'autorise pas :

- le swipe ;
- une pile de cartes persistante ;
- le moteur adaptatif du Freeride ;
- une nouvelle formule de progression composite ;
- une modification du contrat d'accomplissement ;
- une attribution d'Oméga au simple fait de commencer, choisir ou passer une expérience ;
- un nouveau modèle générique de workflow ;
- la refonte de `Journey`, `Challenge`, `ChallengesUser` ou `JourneysUser` sans analyse d'impact.

## 10. Ordre de vérification

Après implémentation :

1. compte n'ayant pas commencé ;
2. compte avec chapitre 1 accompli et chapitre 2 courant ;
3. expérience commencée puis reprise ;
4. expérience optionnelle passée puis reprise ;
5. expérience en attente de facilitateur ;
6. parcours dont toutes les étapes requises sont accomplies mais pas toutes les options ;
7. affichage 320, 375, 390, 768 et 1440 px ;
8. navigation clavier et lecteur d'écran sur les accordéons et états.
