# Le Conseil du Seuil — structure UX et direction artistique

> Ajout Codex - 2026-07-16. Proposition de conception à partir de [11_evaluation_initiale_moteur.md](corpus-point-zero/11_evaluation_initiale_moteur.md), challengée au regard de la [note de convergence](convergence-2026-07-16.md) et de la grammaire du [Moteur ontologique](../vision/moteur-ontologique-visuel.md). Prototype autonome : `zegame-prototypes/conseil-du-seuil/`.

## 1. Intention

Le Conseil du Seuil n'est pas un test de personnalité. C'est une **scène d'orientation** : le joueur découvre que les deux pôles d'une Puissance peuvent être féconds ou captifs selon le contexte, puis reçoit une première hypothèse de navigation.

Il est aussi un **dispositif de transmission** : chaque dilemme dévoile, après la réponse, une technique de relation au monde inspirée de savoirs de peuples premiers et reformulée pour un usage Point Zéro.

La promesse visible est :

> Six situations, aucune réponse parfaite. Un premier miroir de tes mouvements et trois portes pour commencer.

### Voix du Conseil

> Mise à jour Codex - 2026-07-16. Application de la [charte de voix Point Zéro](../vision/voix-point-zero.md).

Le Conseil n'est ni un thérapeute satisfait, ni un oracle qui aurait lu les conditions générales de l'univers. Sa voix est adulte, lucide, légèrement provocatrice et capable de mettre sa propre autorité à distance. Elle confronte les contradictions sans récompenser la conformité et introduit une touche d'humour sec lorsque la scène risque de devenir trop solennelle.

La promesse pourra être poussée vers :

> Six situations. Aucune réponse parfaite. Le Conseil avait oublié de commander le corrigé.

Règles spécifiques :

- aucune félicitation automatique après un choix ;
- les deux mouvements restent légitimes, mais leurs conséquences peuvent être formulées avec davantage de mordant ;
- la restitution se présente comme un miroir contestable, « pas un verdict cosmique gravé dans le marbre » ;
- l'humour vise le Conseil, l'algorithme, les procédures et nos contradictions communes, jamais une réponse intime ;
- une seule touche décalée forte par scène suffit.

Le dispositif doit donner envie d'entrer dans la Marelle tout en diminuant, et non en augmentant, l'autorité apparente de l'évaluation.

## 2. Principaux défis adressés à la proposition initiale

### Une durée sous-estimée

Six questions d'Appel, six scènes en trois interactions, le Don au Commun, deux récits libres et une restitution ne tiennent pas honnêtement en 15 à 18 minutes. Le noyau proposé vise **12 à 15 minutes**, avec :

- un Appel resserré à cinq interactions ;
- six scènes progressives sur un seul écran chacune ;
- un Don au Commun ;
- une restitution courte ;
- les micro-récits déplacés après la restitution comme approfondissement facultatif.

Le joueur peut enregistrer et reprendre entre l'Appel, la troisième scène et la restitution.

### Une précision impossible au premier passage

Un dilemme auto-déclaré ne permet pas de conclure sérieusement à une amplitude `O1–O3` / `L1–L3`, encore moins à une circulation libre. Le premier miroir stocke :

- un mouvement spontané ;
- l'intensité que le joueur dit pouvoir choisir dans ce scénario ;
- sa disposition déclarée envers le mouvement inverse ;
- le contexte ;
- une confiance initiale faible ou moyenne ;
- des zones encore inconnues.

Les amplitudes et maîtrises détaillées restent des hypothèses à éprouver longitudinalement.

### Des formulations trop héroïques ou chargées

`Domination intégrée`, `sacrifice`, `glaciation`, `envoûtement` et `foi totale` sont précieux dans le référentiel approfondi, mais trop inducteurs pour une première évaluation. Avant la restitution, les choix utilisent des verbes situés et concrets. Les termes Ombre, Lumière et degrés ne sont révélés qu'avec une explication.

### Une expérience trop centrée sur le déficit

La restitution doit toujours présenter :

1. un mouvement à mieux comprendre ;
2. une circulation à expérimenter ;
3. un élan déjà disponible à mobiliser.

Le joueur ne reçoit donc jamais une liste de six problèmes à corriger.

## 3. Architecture cible

| Temps | Contenu | Durée cible | Sortie |
|---|---|---:|---|
| Franchir | Accueil, consentement, contexte et droit de retrait | 1 min | Contexte de lecture |
| Répondre à l'Appel | Motivations, profondeur souhaitée, inconfort, engagement réel, relation recherchée | 3 min | Appel d'activation + première signature d'engagement |
| Siéger au Conseil | Six situations ; mouvement spontané, intensité et mouvement inverse | 7 min | Tendances par Puissance et inconnues |
| Donner au Commun | Choisir deux gestes familiers et un geste difficile | 1 min | Profil de contribution non agrégé |
| Recevoir le miroir | Appel, tendances, deux mouvements et trois portes | 2 à 3 min | Carte provisoire et recommandations |
| Approfondir | Un ou deux micro-récits adaptatifs facultatifs | hors noyau | Confiance affinée, jamais validation automatique |

### Appel resserré

Les questions initiales A1 et A6 sont conservées en sélection multiple. A2 porte l'intensité souhaitée. A3 sépare le consentement à l'inconfort du soutien demandé. A4 et A5 sont regroupées dans une **signature d'engagement** concrète : temps, cadence, place de l'action et tonalité relationnelle.

Aucune moyenne générale n'est affichée. `Observer`, `Expérimenter`, `Traverser`, `Transformer` et `Œuvrer` sont des modes d'entrée, pas des rangs.

### Une scène, trois gestes

Chaque scène se déroule sur un seul écran à révélation progressive :

1. lire une situation et choisir entre deux mouvements également légitimes ;
2. découvrir un **geste-source** relié à la situation, avec son origine et le statut de l'adaptation ;
3. préciser la place réellement accordée au mouvement choisi ;
4. indiquer sa relation au mouvement inverse : menaçant, accessible avec un cadre, ou choisissable avec retour.

La deuxième polarité reste `inconnue` si la relance ne permet pas de l'observer. Le système ne transforme jamais l'absence de réponse en amplitude nulle.

### Restitution en trois profondeurs

1. **Premier regard** : Appel, contexte et phrase synthétique accessible.
2. **Six tendances** : mouvement spontané, mouvement à explorer et confiance pour chaque Puissance.
3. **Prochaines portes** : une proposition de circulation, une proposition partant d'un élan disponible et une proposition de conscientisation.

Le détail `O1–O3`, `L1–L3`, les archétypes et les cinq degrés n'est pas affiché comme résultat ferme. Il devient accessible après des expériences dédiées ou une réévaluation.

## 4. Parcours des écrans

1. **Le Seuil** — image plein écran, promesse, durée et entrée.
2. **Consentement et contexte** — personnel, professionnel, collectif ou général ; confidentialité et droit de correction.
3. **L'Appel** — cinq interactions, avec une seule décision dominante par écran.
4. **Ouverture du Conseil** — les six glyphes apparaissent sans révéler leur interprétation.
5. **Six scènes** — image, dilemme, intensité, mouvement inverse.
6. **Le Don au Commun** — documenter, transmettre, ouvrir, redistribuer ; deux gestes familiers et un geste difficile.
7. **Calcul transparent** — animation brève ; rappel des limites et possibilité de continuer sans résultat détaillé.
8. **Premier miroir** — synthèse, tendances et confiance.
9. **Portes du Monde 1** — trois recommandations explicables.
10. **Approfondir ou entrer dans la Marelle** — récit adaptatif facultatif ou sortie.

## 5. Direction artistique : archéologie civique du futur

Le Conseil du Seuil doit sembler découvert dans un futur qui se souvient de très anciennes manières de faire assemblée. Ce n'est ni un temple ésotérique, ni un tableau de bord psychométrique.

### 5.1. Savoirs de peuples premiers : apprendre sans extraire

Le système ancestral de connaissances des peuples Arhuaco, Kankuamo, Kogui et Wiwa de la Sierra Nevada de Santa Marta est inscrit depuis 2022 au patrimoine culturel immatériel de l'UNESCO. Il relie harmonie du monde physique et spirituel, soin des sites, transmission intergénérationnelle et relation aux messages du territoire. L'UNESCO souligne notamment le rôle des Mamos et des Sagas dans cette transmission et cette lecture du vivant ([source UNESCO](https://ich.unesco.org/fr/RL/le-systeme-ancestral-de-connaissances-des-quatre-peuples-autochtones-arhuaco-kankuamo-kogi-et-wiwa-de-la-sierra-nevada-de-santa-marta-01886?RL=01886)).

Les dialogues conduits par Tchendukua entre représentants Kogis et scientifiques donnent un précédent concret de **diagnostic croisé** : faire dialoguer connaissances ancestrales sensibles et sciences modernes pour lire la santé d'un territoire, sans réduire l'une à l'autre ([présentation Tchendukua](https://www.tchendukua.org/seances-film-kogis/), [cadre UNESCO BRIDGES](https://www.unesco.org/en/articles/toward-establishment-bridges-action-promote-sustainability-science)).

Le Conseil du Seuil ne doit ni reproduire des rites, ni enseigner une pratique Kogi sans mandat. Il peut transmettre des **principes relationnels documentés**, puis créer des techniques propres au Point Zéro. Chaque contenu comporte trois mentions :

1. **Inspiration documentée** — peuple, contexte, source et sens donné par ses détenteurs ;
2. **Adaptation Point Zéro** — ce que nous avons transformé en exercice et ce qui n'est pas une pratique d'origine ;
3. **Réciprocité** — partenaire, validation, rémunération ou redistribution lorsque l'emprunt devient substantiel.

La direction artistique n'imite ni costumes, ni motifs, ni objets sacrés. La continuité visuelle repose sur la grammaire néoarchaïque propre au Point Zéro.

### Premiers gestes-sources candidats

| Moment | Inspiration documentée | Technique Point Zéro candidate |
|---|---|---|
| Franchir le Seuil | Le territoire n'est pas un décor mais un système de relations physiques et spirituelles | **Se situer avant de répondre** : nommer le contexte, le lieu et ce qui est affecté |
| Désir | Les décisions s'inscrivent dans une relation à la vitalité et aux cycles du territoire | **Écouter avant de projeter** : distinguer l'appel personnel, celui du groupe et celui du lieu |
| Volonté | Les responsabilités de gardiens relient décision, connaissance du milieu et continuité collective | **Le cercle des conséquences** : regarder qui porte, qui bénéficie, qui répondra plus tard |
| Imagination | Diagnostics croisés Kogis-scientifiques menés dans le Haut-Diois et le long du Rhône | **Le diagnostic croisé** : données, expérience vécue et signaux du territoire |
| Émotion | Les connaissances sensibles sont admises dans le dialogue sans être réduites à des données instrumentales | **Le relevé sensible** : corps, relations et milieu comme trois sources distinctes |
| Communication | Créer un espace où des traditions de connaissance peuvent parler dans leurs propres termes | **Les voix irréductibles** : reformuler sans traduire trop vite dans son propre cadre |
| Intuition | Les savoirs décrits par l'UNESCO incluent l'attention aux rivières, sommets et messages de la nature | **Le carnet des signaux** : observer avant de conclure, puis croiser avec les faits disponibles |
| Don au Commun | Soin des sites et gestes de rétribution envers les puissances spirituelles | **Restituer avant de diffuser** : documenter ce qui est reçu, redistribuer et laisser transformer |

Cette table est une base de recherche, pas l'affirmation que les exercices Point Zéro sont des techniques Kogis.

### Grammaire

- **Néoarchaïque** : matières minérales, papiers, empreintes, cercles, seuils et glyphes gravés.
- **Civique** : table commune, cartographie, décisions situées et langage concret.
- **Futur précis** : grilles, lignes fines, indicateurs de confiance et interactions nettes.
- **Vivant** : les glyphes s'éveillent progressivement ; la carte garde des blancs et respire.

### Palette

| Couleur | Usage |
|---|---|
| Obsidienne `#151014` | structure, mouvement de retrait, texte principal |
| Craie `#F4F1EB` | espace commun et silence visuel |
| Violet Point Zéro `#82246F` | continuité de marque, état provisoire et actions principales |
| Turquoise oxydé `#1D6B6A` | cadre, choix accompagné, information fiable |
| Jaune solaire `#EFB51D` | seuil, attention et sélection active |
| Corail `#CF5279` | appel vivant et accent ponctuel |

Les couleurs propres aux six Puissances apparaissent avec retenue pendant les scènes, puis pleinement dans la restitution. Aucune signification ne repose uniquement sur la couleur.

### Typographie et composition

- `Roboto Slab` pour les titres, noms de scènes et formulations oraculaires courtes ;
- `Poppins` pour les choix, explications et données ;
- grandes images-seuils en plein cadre ;
- écrans de décision en deux zones : situation visible, choix stables ;
- rayons de 4 à 8 px, sauf cercles et glyphes fonctionnels ;
- aucune carte décorative imbriquée ; les sections sont des bandes ou des surfaces franches.

### Mouvement

- apparition séquentielle des six glyphes ;
- tracé progressif, non pulsation permanente, du lemniscate ;
- transition courte lors du choix du mouvement inverse ;
- mode `prefers-reduced-motion` sans perte d'information ;
- aucun son obligatoire ni lecture automatique.

## 6. Famille d'illustrations à produire

### Direction validée

> Mise à jour Codex - 2026-07-16. Direction retenue avec Boris après génération de plusieurs images pilotes.

La série adopte un **collage néoarchaïque contemporain** fait de papiers déchirés, matières minérales, fragments cartographiques, graines, racines et architectures civiques du futur. Deux plans coexistent dans une seule matière :

- le **plan explicite** occupe environ 70 à 75 % de l'image : humains, territoire, problème concret et action possible ;
- le **plan archétypal implicite** occupe environ 25 à 30 % : signes Point Zéro partiellement enfouis dans les strates, tracés, reflets, racines et fragments du décor.

Les symboles ne forment ni bordure décorative ni collection de pictogrammes. Ils se découvrent dans un second temps et répondent discrètement aux éléments explicites : chemin et ligne, assemblée et présences abstraites, infrastructure et cercle, territoire et réseau de racines. Le vocabulaire reste volontairement limité et original : cercle imparfait, graine, bifurcation, onde, main ouverte et figures en relation. Il ne reproduit aucun motif sacré ou culturellement identifiable.

La série reprend aussi la voix visuelle Point Zéro : les humains restent réalistes, mais ne posent pas pour une brochure de transformation. Chaque scène peut contenir un **grain de sabotage** discret — thermos au milieu du Conseil, carte recousue, chaise pliante sous l'architecture monumentale, symbole qui refuse de s'aligner ou regard sceptique devant une procédure trop parfaite. Le plan archétypal peut commenter et contredire le plan explicite. Le détail reste secondaire : il crée une seconde lecture sans transformer l'image en caricature.

Les images actuelles du prototype servent de composition. La série finale doit comprendre :

1. **Un seuil** : silhouette entrant dans une chambre civique circulaire, architecture minérale et lumière contemporaine.
2. **Six scènes** : même territoire et mêmes personnages secondaires, avec un enjeu lisible sans texte incrusté.
3. **Un Don au Commun** : méthode ou objet circulant entre plusieurs communautés, transformé sans perdre sa source.
4. **Une texture commune** : papier minéral, marques topographiques et traces de gestes, utilisable avec parcimonie.

Chaque scène doit disposer de variantes 16:9 et 4:3 avec une zone sûre centrale. Les personnages restent divers, non héroïsés et sans costume associé à un peuple réel. Les symboles sont abstraits et propres au Point Zéro.

### Prompt matrice

```text
Illustration éditoriale néoarchaïque pour Le Conseil du Seuil, archéologie civique du futur, assemblée humaine diverse dans un territoire en transition, matières minérales et papier découpé, formes primitives abstraites mêlées à une cartographie contemporaine précise, obsidienne, craie, turquoise oxydé, jaune solaire et accent corail, lumière claire, composition lisible sur mobile, profondeur modérée, aucun texte, aucun logo, aucun costume tribal identifiable, aucune esthétique fantasy médiévale, aucune interface.
```

Chaque prompt de scène ajoute uniquement la situation, le geste principal et la Puissance concernée afin de conserver une famille cohérente.

## 7. Données et règles proposées pour Claude

Le prototype n'impose pas un modèle Rails, mais la future intégration devra distinguer :

- la version du dispositif et du scoring ;
- le contexte de passation ;
- l'Appel d'activation ;
- la signature d'engagement ;
- les réponses brutes aux scènes ;
- les hypothèses dérivées et leur confiance ;
- les inconnues explicites ;
- les contestations ou corrections du joueur ;
- les recommandations et leurs raisons ;
- les micro-récits, séparés du résultat calculé.

Une nouvelle passation crée un instantané ; elle ne réécrit pas silencieusement l'ancien. Le premier miroir ne doit jamais alimenter directement une évaluation dite 360° ni déplacer seul l'état violet consolidé du Profil.

## 8. Critères de validation du design

- médiane de complétion du noyau entre 12 et 15 minutes ;
- compréhension spontanée que les deux mouvements ont une valeur ;
- absence d'incitation à choisir la réponse la plus intense ;
- capacité à expliquer la différence entre tendance, inconnu et confiance ;
- possibilité de corriger le contexte et les réponses ;
- aucune confusion avec un diagnostic clinique ou un test de personnalité ;
- trois recommandations perçues comme distinctes et explicables ;
- lecture et action possibles à 390 × 844, 768 × 1024 et 1440 × 900 ;
- navigation clavier, alternatives aux images et mode mouvement réduit.

## 9. Points à arbitrer après revue

1. Le Conseil du Seuil est-il obligatoire dans le Monde 0 ou fortement recommandé avec possibilité de différer ?
2. Le terme visible doit-il rester « évaluation », devenir « premier miroir », ou varier selon l'écran ?
3. La restitution révèle-t-elle immédiatement les mots Ombre et Lumière ou seulement après La Boussole ?
4. Les cinq degrés du Moteur doivent-ils rester absents de cette première restitution ? Recommandation Codex : oui.
5. Quelle part de la signature d'engagement est visible lors de la future composition des Cercles ?
