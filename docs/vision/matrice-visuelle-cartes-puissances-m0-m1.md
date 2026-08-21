# Matrice visuelle des cartes-Puissances — Mondes 0 et 1

**Statut :** outil de production éditoriale et visuelle, état audité le 16 août 2026  
**Références canoniques :**
[onboarding-monde-0-sept-puissances.md](onboarding-monde-0-sept-puissances.md),
[onboarding-monde-1-sept-puissances.md](onboarding-monde-1-sept-puissances.md) et
[matrice-impact-onboarding-monde-1.md](matrice-impact-onboarding-monde-1.md).

## 1. Fonction de la matrice

Cette matrice indique quand une carte de l'accueil doit changer d'illustration, quelle page elle
révèle et quels visuels restent à produire. Elle ne crée aucun état métier supplémentaire.

Une carte change d'image uniquement lorsque son CTA principal révèle un **territoire durable** :
une page, un sous-espace ou un usage qui restera accessible dans le sous-menu de la Puissance.
Elle ne change pas pour :

- une notification ou un message non lu ;
- la variation d'un compteur ;
- une étape ordinaire d'un parcours déjà ouvert ;
- une nouvelle quête dans Immateria ;
- une action courante dans un Cercle ;
- le simple passage de `invitation` à `appropriation`.

Après la première visite, l'illustration du dernier territoire révélé reste visible. Lorsqu'une
nouvelle page devient accessible, la carte repasse en `À explorer`, adopte l'image de cette page et
reçoit une surbrillance légère. L'image matérialise ainsi l'approfondissement du territoire ;
l'icône, la couleur, le verbe et la position dans la roue maintiennent l'identité de la Puissance.

### 1.1 Légende

| Code | Signification | Décision de production |
|---|---|---|
| **E** | Asset spécifique existant et exploitable | Brancher ou conserver |
| **R** | Asset existant réutilisable, à recadrer ou mutualiser | Adapter sans régénérer |
| **P** | Territoire et direction validés, asset spécifique absent | Produire |
| **C** | Concept/page encore à stabiliser | Ne pas produire avant cadrage |
| **A** | Animation native de la page | Décliner en animation légère ou poster statique |

Les chemins ci-dessous décrivent l'état des prototypes. Ils ne constituent pas des chemins à
exposer dans l'interface ni dans le corpus des guides.

## 2. Monde 0 — matrice rétroactive

| Puissance | Seuil visible | Déclencheur métier ou éditorial | CTA et territoire durable | Illustration cible | État | Action |
|---|---|---|---|---|---|---|
| **Désir** | Premier appel | entrée dans le Monde 0 | `Créer mon jumeau` → Immateria | création du jumeau et village ; `accueil-puissances-m0-cible/assets/powers/desir.webp` | **E** | conserver ; Immateria porte ensuite ses propres décors |
| **Désir** | Retour | jumeau créé ou quête active | `Basculer vers Immateria` | dernier seuil majeur du jeu, pas la quête courante | **C** | définir seulement avec l'équipe du pixel game ; ne pas créer une image par quête |
| **Volonté** | Premier appel | premier parcours Monde 0 disponible | `Entrer dans la Marelle` | entrée dans la Marelle ; `assets/powers/volonte.webp` | **E** | conserver |
| **Volonté** | Appropriation | parcours commencé | prochaine action réelle du parcours | même image ; titre, étape et CTA évoluent | **E** | aucun nouvel asset |
| **Imagination** | Premier appel | première Graine proposée | `Créer ma première Graine` → Fresque | `fresque-recit-m0-cible/assets/fresque-hero-v1.webp` | **E** | brancher aussi sur la carte d'accueil à ce seuil |
| **Imagination** | Réouverture | première Trace créée dans un parcours ou mini-jeu | `Découvrir mes Traces` → Mes Traces | `accueil-puissances-m0-cible/assets/powers/traces.webp` | **E** | branché ; conserver ensuite comme mémoire du dernier espace révélé |
| **Émotion** | Premier appel | catalogue pilote accessible | `Choisir mon mentor` → Héros et mentors | couverture de catalogue, distincte d'un portrait individuel | **P** | produire une scène de rencontre avec plusieurs figures possibles |
| **Émotion** | Appropriation | mentor choisi | `Parler avec mon mentor` | portrait du mentor choisi dans un cadre néoarchaïque commun | **R** | composer depuis les portraits carrés existants, sans générer une nouvelle œuvre |
| **Communication** | Premier appel | Profil communautaire disponible | `Composer mon profil` → Profil communautaire | image-source de la Puissance `communication.webp` | **E** | conserver : la production Rails ne déclare plus d'image spécifique à ce stade |
| **Communication** | Réouverture 1 | Profil communautaire confirmé | `Entrer dans l'Espace d'échange` | `accueil-puissances-m0-cible/assets/powers/communication-echanges.webp` | **E** | branché ; conserver jusqu'à l'entrée effective dans l'Espace |
| **Communication** | Réouverture 2 | Espace d'échange rejoint | `Explorer l'Annuaire` | `accueil-puissances-m0-cible/assets/powers/communication-annuaire.webp` | **E** | branché ; conserver ensuite comme mémoire du dernier territoire révélé |
| **Intuition** | Premier appel | Guides accessibles | `Choisir un regard` → Guides | `accueil-puissances-m0-cible/assets/powers/intuition-guides.webp` | **E** | branché ; les deux voix sont réunies dans une même composition Ombre/Lumière |
| **Intuition** | Réouverture | premier échange Guide complet | `Découvrir les clés du Point Zéro` → Point Zéro | `premieres-cles-m0-cible/assets/intuition-hero.webp` | **E** | brancher sur la carte ; les QCM produisent des Traces, pas de nouvelles couvertures |
| **Intuition** | Appropriation | fiche lue ou QCM rempli | lire la prochaine clé / voir les événements | même illustration, compteurs de clés et Traces | **E** | aucun nouvel asset en M0 |
| **Transcendance** | Premier appel | questionnaire du Moteur accessible | `Observer mon Moteur` → Moteur | `assets/powers/transcendance.webp` | **E** | conserver |
| **Transcendance** | Réouverture | six Puissances renseignées et premier badge disponible | `Voir mes Accomplissements` | constellation animée de la page Accomplissements | **A** | conserver le principe ; créer une miniature animée simplifiée et un poster statique |

Éditorial de la réouverture 2 de Communication : **`Découvre qui joue déjà`** — `Des milliers de
chemins possibles. Des personnes bien réelles. Découvre celles qui ont choisi de prendre place
dans le Jeu.` Le CTA canonique reste **`Explorer l’Annuaire`**.

### 2.1 Arbitrage Transcendance

La constellation peut vivre dans une carte responsive si elle est traitée comme un composant et
non comme une capture miniature de la page :

- cinq à sept nœuds maximum dans la carte ;
- aucun libellé à l'intérieur de l'animation ;
- mouvement lent, non pulsé, limité au fond de l'image ;
- `aria-hidden="true"` car le statut et le CTA portent le sens ;
- `prefers-reduced-motion` affiche un poster statique ;
- gel de l'animation lorsque la carte est hors écran.

L'accueil conserve donc l'animation comme singularité de la Couronne. Il ne faut pas la convertir
par principe en illustration raster.

## 3. Monde 1 — territoires révélés

La matrice suivante ne demande pas une image à chaque ligne. La colonne **Bascule visuelle** indique
si le moment révèle réellement un nouveau sous-espace. Les usages ordinaires conservent le dernier
visuel acquis.

### 3.1 Entrée dans le Monde 1

| Puissance | Invitation principale | Territoire révélé | Bascule visuelle | Illustration cible | État | Action |
|---|---|---|---|---|---|---|
| **Désir** | relire ce qui appelle puis préparer la traversée solo | Carte du Seuil | oui | `assets/invitations/desir-carte-seuil-v2.webp` | **E** | triangle des trois scénarios ; branché dans le prototype |
| **Volonté** | commencer la Boussole obligatoire | Boussole Monde 1 | oui | `assets/invitations/volonte-boussole-v4.webp` | **E** | conserver la version v4 |
| **Imagination** | choisir une Graine à partager | partage et visibilité des Graines | oui | `assets/invitations/imagination-graine-partageable-v1.webp` | **E** | branché dans le prototype |
| **Émotion** | découvrir des constellations de Cercle | constellations possibles | oui | `assets/invitations/emotion-constellation-cercle-v5.webp` | **E** | conserver la version v5 |
| **Communication** | se présenter, accueillir, produire une Résonance | Espace du Seuil | oui | `assets/invitations/communication-espace-seuil-v2.webp` | **E** | conserver la version v2 |
| **Intuition** | explorer ce qui existe déjà hors du PZ | Ressources externes | oui | `assets/invitations/intuition-ressources-externes-v1.webp` | **E** | branché dans le prototype ; destination Rails à confirmer |
| **Transcendance** | comprendre l'origine de ses Omégas | Omégas et domaine de souveraineté | oui | `assets/invitations/transcendance-souverainete-omega-v1.webp` | **E** | branché dans le prototype |

**Lot d'entrée M1 achevé dans le prototype : sept images sur sept.** Les quatre nouvelles créations
complètent la Boussole, les constellations de Cercle et l'Espace du Seuil déjà validés. La page Rails
d'entrée des ressources externes reste à confirmer, mais son asset ne dépend pas de cet arbitrage.

### 3.2 Après la traversée solo

| Puissance | Usage proposé | Nouveau territoire ? | Décision visuelle |
|---|---|---|---|
| **Désir** | poursuivre les Sept Années dans Immateria | non | conserver Carte du Seuil jusqu'à un vrai seuil du jeu |
| **Volonté** | achever la Boussole et sa restitution | non | conserver Boussole |
| **Imagination** | cristalliser la restitution en Graine | non | conserver partage des Graines |
| **Émotion** | comparer les constellations et choisir librement | non | conserver constellation |
| **Communication** | lire les réponses et produire une Résonance | non | conserver Espace du Seuil ; les non-lus sont un compteur |
| **Intuition** | découvrir une première carte systémique | oui, si une page `Cartes systémiques` entre dans le sous-menu | **C** : cadrer la page avant l'image |
| **Transcendance** | lire la ventilation de ses Omégas | non | conserver Domaine de souveraineté |

### 3.3 Formation et activation du Cercle

| Puissance | Invitation principale | Territoire durable | Bascule visuelle | État | Direction proposée |
|---|---|---|---|---|---|
| **Désir** | produire puis tenir le Pacte-Source | Pacte-Source | oui | **P** | racines individuelles convergeant vers une flamme commune sans fusionner |
| **Volonté** | traverser une quête collective | parcours collectifs | oui si un catalogue/écran collectif distinct est créé | **C** | stabiliser d'abord la navigation des parcours collectifs |
| **Imagination** | relier les récits sans les absorber | Fresque du Cercle | oui | **P** | fragments narratifs autonomes dessinant une œuvre commune inachevée |
| **Émotion** | habiter les cinq Cadres par rotation | rôles tournants | oui | **P** | cinq figures ou cinq objets en circulation autour d'un centre vide |
| **Communication** | préparer, tenir et mémoriser une séance | espace d'échanges du Cercle | oui | **P** | cercle parlant où intention, objection, décision et action restent discernables |
| **Intuition** | récolter les apprentissages et angles morts | apprenance du Cercle | oui | **P** | miroir collectif révélant une forme absente ou un point aveugle |
| **Transcendance** | observer Cadres et flow | profil du Cercle | oui | **P** | Moteur collectif et cinq Cadres, distincts du profil individuel |

Ce lot ne doit être produit qu'après vérification des pages déjà présentes dans les prototypes
`cercle-croissance-cible`, `messagerie-point-zero-cible` et `profil-joueur-cible`. Une illustration
existante de page doit être adaptée avant d'en générer une nouvelle.

### 3.4 Cercle vivant et autonomie

| Puissance | Usage courant | Nouveau territoire ? | Décision visuelle |
|---|---|---|---|
| **Désir** | confronter l'écart entre actes et Pacte-Source | non | conserver Pacte-Source |
| **Volonté** | choisir librement durée, intensité et rayon d'effet | oui seulement lors de la première ouverture du catalogue libre | réutiliser l'illustration du catalogue Freeride si elle existe |
| **Imagination** | faire circuler Graines, Résonances et synthèse | non | conserver Fresque du Cercle |
| **Émotion** | prendre le prochain rôle tournant | non | conserver rôles tournants |
| **Communication** | suivre le fil, préparer et lancer une action | non | conserver espace du Cercle |
| **Intuition** | conduire un débrief collectif | non | conserver apprenance du Cercle |
| **Transcendance** | accéder au Commun et lire le flow | oui pour le premier accès au Commun | réutiliser la couverture du Commun après audit des maquettes existantes |

## 4. Ordre de production recommandé

### Lot V0 — terminé dans le prototype M1

1. Volonté — Boussole ;
2. Émotion — constellations de Cercle ;
3. Communication — Espace du Seuil.

### Lot V1 — raccordement rétroactif M0

1. brancher Fresque, Traces et Point Zéro sur les cartes correspondantes ;
2. brancher les trois états Communication : Profil → Espace d'échange → Annuaire ;
3. produire la couverture du catalogue des héros ;
4. composer l'état `mentor choisi` depuis le portrait sélectionné ;
5. adapter la constellation Accomplissements en composant de carte et poster statique.

### Lot V2 — entrée M1 — terminé dans le prototype

1. Carte du Seuil — `desir-carte-seuil-v2.webp` ;
2. Graine partageable — `imagination-graine-partageable-v1.webp` ;
3. Ressources externes — `intuition-ressources-externes-v1.webp` ;
4. Domaine de souveraineté Oméga — `transcendance-souverainete-omega-v1.webp`.

### Lot V3 — Cercle

Auditer d'abord les maquettes existantes, puis compléter seulement les manques : Pacte-Source,
Fresque du Cercle, rôles tournants, échanges du Cercle, apprenance et profil du Cercle.

## 5. Convention d'assets et résolution

Le portage Rails doit résoudre une clé éditoriale à partir de la destination principale, par
exemple :

```text
m0.imagination.fresque
m0.imagination.traces
m0.communication.profil
m0.communication.echanges
m0.communication.annuaire
m0.intuition.guides
m0.intuition.point_zero
m0.transcendance.moteur
m0.transcendance.accomplissements
m1.volonte.boussole
m1.emotion.constellations
m1.transcendance.souverainete_omega
```

`illustration_key` est **dérivée**, jamais enregistrée comme progression. Le résolveur suit cet
ordre :

1. déterminer les destinations accessibles depuis les sources métier réelles ;
2. exclure celles déjà visitées pour identifier les invitations ;
3. appliquer la priorité éditoriale stable, puis l'ancienneté ;
4. produire le CTA ;
5. en déduire `illustration_key` et la surbrillance ;
6. utiliser l'image de la Puissance comme fallback si l'asset manque.

Le fallback garantit qu'un asset absent ne bloque jamais un parcours et ne provoque jamais une
validation, un gain d'Oméga ou une transition métier fictive.

## 6. Contraintes graphiques et responsive

- néoarchaïsme symbolique : collages, matière, polarités, lignes géométriques et triangulation
  discrète ;
- couleur dominante de la Puissance, sans dépendre d'elle pour transmettre le statut ;
- composition lisible avant les détails : un symbole central et deux à quatre masses secondaires ;
- zone sûre centrale compatible avec la carte verticale mobile et le recadrage horizontal desktop ;
- aucun texte ni chiffre incorporé dans l'image ;
- personnages archétypaux ou objets symboliques, sans répéter systématiquement la même silhouette ;
- état `À explorer` : halo CSS sobre autour de la carte, non peint dans l'image ;
- transition de révélation jouée une seule fois et désactivable ;
- optimisation WebP/AVIF et poster statique pour toute animation.

## 7. Critères de recette

1. Une nouvelle notification ne change jamais l'illustration.
2. Une nouvelle page durable réactive la carte avec son image et un CTA explicite.
3. Une seule invitation est principale par Puissance ; les autres sont comptées.
4. Après visite, la surbrillance disparaît mais l'image reste.
5. L'absence d'un asset utilise le fallback de Puissance sans modifier l'état métier.
6. La carte reste compréhensible sans couleur, animation ni image.
7. Les visuels restent lisibles à 320 px de large et dans un recadrage desktop horizontal.
8. La constellation Transcendance possède un poster et respecte `prefers-reduced-motion`.
9. Aucun clic de la coque ne valide une expérience, ne forme un Cercle ou ne gagne un Oméga.
10. Les libellés restent `JE M'EXPRIME` et `JE DISCERNE` dans toutes les variantes.
