# Audit éditorial — parcours 5, écosystème et navigation du site

> **Ajout Codex — 2026-08-03.**
>
> **Objet** : identifier les écarts entre le corpus public existant, le Livre II et la vision
> récente de l'écosystème ; décider quelles pages conserver, actualiser, fusionner ou créer ;
> proposer une architecture de navigation qui maintient le corpus profond librement accessible
> tout en donnant une boussole au visiteur.
>
> **Périmètre audité** : export assaini des 138 contenus WordPress, pages du bloc
> `Comprendre / Écosystème / Formats`, articles reliés à « Comment nous réveiller ? »,
> `PRT-Le Point Zéro - Livre II.docx`, documents de vision sur les Puissances, les Cercles,
> l'Oméga et le fonctionnement global de l'écosystème.
>
> **Hors périmètre** : réécriture complète des pages, code Rails, choix de la formule juridique
> de l'Oméga et publication de la cosmogonie du Livre II.

---

## 1. Recommandation exécutive

Le site ne manque pas de matière. Il manque de **liaisons** entre trois ensembles aujourd'hui
juxtaposés :

1. le diagnostic du Livre I, déjà abondant et utile ;
2. la grammaire opératoire du Livre II, presque absente du site ;
3. l'écosystème réellement conçu depuis : Jeu, Marelle, Puissances, Cercles, projets, Oméga et
   Commun.

La réponse n'est donc ni de supprimer le corpus existant, ni d'ajouter une huitième page
« Écosystème » à côté des sept autres. Il faut **changer le principe d'architecture** :

```text
COMPRENDRE CE QUI ARRIVE
Livre I, cinq questions, parcours publics, articles
                     ↓
COMPRENDRE COMMENT LE POINT ZÉRO AGIT
Moteur, Puissances, Cadres, Marelle, Cercle
                     ↓
VOIR COMMENT CELA DEVIENT UN ÉCOSYSTÈME
projets, organisations, Oméga, Commun, besoins
                     ↓
ENTRER DANS LE JEU
application, Monde 0, événements et autodiagnostic
```

### Décision recommandée

- conserver les cinq pages `Comprendre` et les articles comme corpus du Livre I ;
- **réécrire profondément** `/comprendre-question-5/`, qui doit devenir la charnière entre le
  diagnostic et le Jeu ;
- remplacer le menu `Écosystème` fondé sur des catégories de publics par une architecture
  fonctionnelle : **Le Jeu · Agir ensemble · Le Commun** ;
- créer cinq contenus canoniques réellement manquants : le Moteur et les Puissances, le Cercle,
  l'économie Oméga, l'architecture de l'écosystème et le parcours des projets/organisations ;
- transformer les anciennes pages longues en destinations, répertoires ou redirections, sans
  retirer du Web les contenus de fond qui restent utiles ;
- afficher sur les pages d'écosystème le statut de chaque mécanisme : **Actif aujourd'hui · En
  expérimentation · Horizon**.

---

## 2. Ce que montre l'audit du corpus actuel

### 2.1 Le parcours 5 arrive sur une page qui décrit encore surtout le problème

La page `/comprendre-question-5/` comporte environ 1 100 mots. Elle présente :

- les étapes de l'intercycle ;
- l'alchimisation de l'Ombre ;
- la crisologie ;
- une liste d'articles rattachés.

Cette matière n'est pas fausse. Elle explique pourquoi une bifurcation devient possible. Elle
n'explique pas encore **comment** le Point Zéro entend la rendre praticable.

Il manque notamment :

- la symétrie entre Point Zéro individuel et collectif ;
- le Moteur et les sept Puissances ;
- la correspondance entre cinq Puissances centrales et cinq Cadres ;
- le flow comme activation et synchronisation, non comme absence de tension ;
- la fonction du Cercle et du Pacte-Source ;
- la Marelle comme progression par paliers ;
- l'Oméga comme reconnaissance non fongible et domaine de souveraineté ;
- la différence entre Oméga, Fonds du Commun, cagnotte de Cercle et fonds de projet ;
- le passage concret vers le Monde 0.

Le parcours public 5 fait déjà vivre une partie de ces principes. La page de fond qui doit
l'accompagner est donc moins avancée que le jeu qui y conduit.

### 2.2 Deux pages promises comme fondamentales sont presque vides

- `/le-point-zero/` ne contient pas de corps éditorial exploitable dans l'export ;
- `/les-strategies-daction/` ne contient qu'un titre et une très courte amorce.

Ces deux URL ont pourtant une forte valeur sémantique. Elles ne doivent pas être supprimées sans
réflexion : ce sont de bons emplacements pour les deux pages canoniques suivantes :

- `/le-point-zero/` → **Qu'est-ce que le Point Zéro ? Une architecture de circulation** ;
- `/les-strategies-daction/` → **Cinq profondeurs d'action — pourquoi les solutions justes
  restent parfois insuffisantes**.

La seconde page devient le prolongement naturel du parcours 4, pas du parcours 5.

### 2.3 Le bloc Écosystème est long, répétitif et organisé selon une taxonomie antérieure

Les huit pages `ecosysteme-*` représentent plus de 13 000 mots bruts, mais leur longueur masque
trois problèmes :

1. **répétition de blocs** : six pages reproduisent les mêmes cartes Sas, Atelier, formats et
   partenaires ; huit ou neuf pages répètent les mêmes témoignages ;
2. **segmentation marketing devenue trop étroite** : Explorateurs, Chrysalides et Vaisseaux ne
   suffisent plus à décrire Joueurs, Cercles, facilitateurs, projets, métiers, organisations et
   Commun ;
3. **absence de la mécanique réelle** : presque rien sur la Marelle, les Puissances, le flow,
   le cycle des Cercles, l'Oméga non fongible ou les trois circuits financiers.

La page `ecosysteme-incubateur` est l'exception par sa richesse propre : plus de 4 000 mots et
de nombreux projets. Mais elle fonctionne comme une longue liste éditoriale, sans statut,
porteur, besoin, domaine, étape ou possibilité de contribution. Elle doit devenir un **répertoire
structuré de projets**, alimenté par l'application, plutôt qu'une page-manifeste.

### 2.4 Le corpus contient déjà de bonnes briques qu'il faut mieux distribuer

Plusieurs contenus sont solides et doivent être conservés :

- `Le pouvoir des récits` pour la chaîne récit → croyance ;
- `La métamorphose interdite` pour le risque de polarisation vertueuse des Chrysalides ;
- `Le Point Zéro : un écosystème « méta »` pour la matrice de récits ouverts ;
- `Les cadres systémiques` comme base d'une page canonique à mettre à jour ;
- `L'écologie interne` pour le versant individuel ;
- `2040 : de la société de la peur à la société du courage` pour la projection ;
- `Les phases du Point Zéro`, `2025-2050 : ... métacivilisation` et les articles sur les
  crises/récits comme profondeurs du parcours 5.

Leur faiblesse n'est pas leur contenu, mais leur rôle actuel : ils sont listés sans former un
chemin de lecture ni distinguer modèle actif, hypothèse et vision.

### 2.5 Incohérences à corriger en priorité

| Sujet | État constaté | Correction recommandée |
|---|---|---|
| Les trois Livres | `/cycle-point-zero/` attribue au Livre II le plan d'action et au Livre III la conscience | rétablir : Livre I diagnostic ; Livre II grammaire de Conscience et dispositifs ; Livre III plan d'action, encore en chantier |
| Verticales | une page parle de 12 verticales, une autre de 20 | réserver les 20 verticales à la cartographie civilisationnelle des Chrysalides ; ne plus structurer le parcours joueur autour de 12 verticales |
| 10 % d'ici 2050 | parfois présenté comme un seuil démontré par les systèmes complexes | le formuler comme ambition et hypothèse stratégique du PZ, pas comme loi scientifique établie |
| Oméga | ancien vocabulaire de « monnaie » ou de points à investir | partout préciser : unité nominative, non fongible, non transférable ; elle oriente de l'argent commun mais ne se dépense pas |
| Cadres | présentés sans leurs correspondances canoniques | ajouter Volonté–Relationnel, Imagination–Sens, Émotion–Gouvernance, Communication–Opérationnel, Intuition–Apprenance |
| Cercle | traité comme un format parmi d'autres | le présenter comme cellule-souche de croissance, 5 à 8 personnes, évolutive, avant spécialisation |
| Offre | Sas, formats et témoignages répétés sur presque toutes les pages | un seul composant dynamique de sortie, contextualisé par la page |

---

## 3. Écart conceptuel entre le site et la vision actuelle

| Concept | Présence actuelle | Décision éditoriale |
|---|---|---|
| Crise des récits et intercycle | forte | conserver comme rampe du Livre I |
| Intégration des polarités | présente mais dispersée | en faire le geste central du Point Zéro |
| Empire / Cité cosmique | présent dans les nouveaux brouillons, absent du site historique | publier comme deux morphologies, sans naïveté envers les rapports de pouvoir |
| Chaîne récit → croyance → Puissance → Cadre | absente | créer le schéma-pivot de l'ensemble du site |
| Moteur de Conscience | absent | nouvelle page canonique |
| Sept Puissances | absentes | nouvelle page canonique + sept cartes courtes, pas sept longues pages en V1 |
| Cinq Cadres | présents partiellement | réécrire la page existante et ajouter les correspondances canoniques |
| Flow individuel / collectif | absent | intégrer aux pages Moteur, Cadres et organisations |
| Marelle et Mondes | absents du site historique | créer une présentation opérationnelle, sans cosmogonie ni correspondance avec les cinq lectures du site |
| Cercle de croissance | absent | nouvelle page canonique |
| Pacte-Source | absent | contenu de profondeur dans la page Cercle ; version légère seulement côté public |
| Oméga non fongible | absent ou vocabulaire obsolète | nouvelle page canonique avec simulation simple |
| Fonds du Commun / cagnotte du Cercle / projets | absents | expliquer les trois circuits sans publier les paramètres encore expérimentaux |
| Rôles d'appel et métiers PZ | absents | teaser dans la page Jeu ; détails dans l'application |
| Projets et besoins du système | projets listés sans fonctionnement | répertoire dynamique et CTA de contribution dans l'application |
| Statut réel des mécanismes | absent | ajouter Actif / Expérimentation / Horizon |

---

## 4. Sort recommandé des pages existantes

### 4.1 Pages pivots et conceptuelles

| URL actuelle | Décision | Nouveau rôle |
|---|---|---|
| `/comprendre-question-5/` | **réécriture profonde, URL conservée** | page-charnière « Comment nous réveiller ? » entre les cinq questions et le Jeu |
| `/le-point-zero/` | **création sur URL existante** | définition canonique, architecture fractale et passages site → Jeu → Cercle → œuvre → Commun |
| `/les-strategies-daction/` | **création sur URL existante** | cinq profondeurs d'action ; prolongement du parcours 4 |
| `/les-cadres-systemiques/` | **réécriture majeure** | page canonique des cinq Cadres, correspondances avec les Puissances, activation/synchronisation/flow |
| `/le-point-zero-un-ecosysteme-meta/` | **conserver comme article daté, mise à jour légère** | profondeur éditoriale ; renvoi vers les pages canoniques, sans porter seul la définition actuelle |
| `/cycle-point-zero/` | **corriger immédiatement** | histoire du projet et articulation exacte des trois Livres |

### 4.2 Ancien menu Écosystème

| URL actuelle | Décision | Destination ou transformation |
|---|---|---|
| `/ecosysteme-introduction/` | **fusionner** | redirection vers `/le-point-zero/` après reprise des meilleurs passages |
| `/ecosysteme-vision/` | **fusionner** | ambition, mission et principes intégrés à `/le-point-zero/` ; association en porte la gouvernance institutionnelle |
| `/ecosysteme-explorateurs/` | **retirer du menu** | conserver comme landing temporaire ou rediriger vers `/le-jeu/`; « Explorateur » devient une posture d'entrée, pas une classe de membre |
| `/ecosysteme-chrysalides/` | **réécrire** | page « Faire grandir un projet sans reproduire ce qu'il combat » + appel à candidatures |
| `/ecosysteme-vaisseaux/` | **réécrire** | page organisations : autodiagnostic Puissances/Cadres, accompagnement, parcours dédié |
| `/ecosysteme-incubateur/` | **transformer** | répertoire de projets avec filtres, statuts, besoins et porteurs ; données issues de l'application |
| `/ecosysteme-commun/` | **réécrire profondément** | page du Commun : besoins individuels/système, Fonds du Commun, circulation de la valeur et transparence |
| `/ecosysteme-association/` | **conserver et actualiser** | personne morale, équipe, gouvernance, partenaires, rapports et contact ; aucun contenu pédagogique dupliqué |

### 4.3 Formats, parcours et conversion

| URL actuelle | Décision | Nouveau rôle |
|---|---|---|
| `/formats-introduction/` | **remplacer par un index dynamique** | événements et chemins disponibles aujourd'hui, filtrés par public et intensité |
| `/parcours/` | **réécrire ou rediriger vers l'application** | ne plus présenter 12 verticales comme structure centrale ; montrer les parcours réellement ouverts |
| `/rejoindre/` | **fusionner** | page simple de passage : entrer dans le Jeu, participer à un événement, porter un projet, contacter l'association |
| pages Conférences / Ateliers / Formations | **conserver si offre active** | pages transactionnelles claires ; retirer le manifeste générique et les blocs répétés |
| anciennes pages Sas | **rediriger** | accueil des cinq parcours publics ou agenda réel |

### 4.4 Articles et Ressourcerie

- conserver les 33 articles à leur URL ;
- afficher leur date et leur statut de **texte de recherche / point de vue**, distinct d'une
  page de doctrine actuelle ;
- ajouter une courte mention « Pour poursuivre dans le Jeu » avec un concept PZ et un parcours ;
- corriger le vocabulaire Oméga ou les faits devenus faux, sans réécrire rétroactivement les
  prises de position historiques ;
- garder la bibliographie et les cartographies comme profondeur librement accessible ;
- séparer visuellement les ressources PZ des Pensées, Pratiques et Chrysalides externes.

---

## 5. Les contenus canoniques à créer

La V1 n'a pas besoin d'une page par notion. Six pages bien construites suffisent pour combler
l'écart, en plus des réécritures sur URL existante.

### 5.1 `/le-point-zero/` — Une architecture de circulation

**Question répondue** : qu'est-ce que le Point Zéro, au-delà d'une vision ou d'une méthode ?

Structure :

1. la crise des solutions produites depuis le récit qui a créé les problèmes ;
2. le Point Zéro comme accueil des polarités, pas comme compromis ;
3. la transformation fractale : individu, Cercle, organisation, projet, économie ;
4. la chaîne `récits → croyances → Puissances → Cadres → flow` ;
5. l'architecture `site → Monde 0 → Monde 1 → Monde 2+ → œuvre → Commun` ;
6. ce qui existe, ce qui est expérimenté, ce qui relève de l'horizon ;
7. CTA : **Entrer dans le Jeu**.

Cette page absorbe `ecosysteme-introduction` et `ecosysteme-vision`.

### 5.2 `/le-jeu/` — Pourquoi un Jeu ?

**Question répondue** : pourquoi ne pas proposer simplement des contenus et des formations ?

Structure :

1. le visiteur ne manque pas seulement d'information ;
2. la Marelle comme progression par paliers et rites de passage ;
3. le Monde 0 comme entrée, le Monde 1 comme articulation individuel/collectif ;
4. le Moteur, les traces, les Graines et les Résonances ;
5. les Cercles comme lieux d'expérience ;
6. les Rôles d'appel comme promesse de contribution future ;
7. CTA direct vers l'application.

La page doit rester opérationnelle. Source, multivers et plan archétypal demeurent dans les
Livres et dans les profondeurs du Jeu.

### 5.3 `/le-moteur-et-les-sept-puissances/`

**Question répondue** : qu'est-ce qui se réveille exactement ?

Structure :

1. la puissance comme circulation, non possession ;
2. le Moteur : Désir → cinq Puissances centrales → Transcendance ;
3. sept cartes : `JE SUIS · JE VEUX · JE CRÉE · JE RESSENS · JE M'EXPRIME · JE DISCERNE · JE DONNE` ;
4. Ombre et Lumière comme directions nécessaires, jamais score positif/négatif ;
5. capacité = sens de circulation adapté à une situation ;
6. du Moteur individuel aux cinq Cadres collectifs ;
7. garde-fou : aucun diagnostic automatique de la conscience du visiteur.

Les sept cartes peuvent réutiliser les fiches pédagogiques et vidéos existantes. Il n'est pas
nécessaire de créer sept pages SEO séparées avant de disposer d'un contenu suffisant.

### 5.4 `/pourquoi-le-cercle/` — Se remettre en cercle pour recommencer à grandir

**Question répondue** : pourquoi le collectif ne peut-il pas être un simple forum ou groupe de
discussion ?

Structure :

1. le Cercle de croissance comme cellule-souche de 5 à 8 personnes ;
2. la progression individuelle reste la finalité ;
3. cinq Cadres appris par cinq fonctions tournantes ;
4. Pacte-Source léger en Monde 1, complet en Monde 2 ;
5. autofacilitation puis facilitation certifiée ;
6. spécialisation organique : médiation, stratégie, redistribution, projet ;
7. ce que le Cercle ne promet pas : unanimité, thérapie collective ou absence de conflit.

### 5.5 `/economie-omega/` — Rendre à l'argent une direction consciente

**Question répondue** : comment une unité non fongible peut-elle agir sur l'argent réel ?

Structure :

1. ce que l'Oméga reconnaît ;
2. ce qu'il n'est pas : euro, crypto, récompense achetable ou jeton à dépenser ;
3. Oméga actif et domaine de souveraineté ;
4. simulation : fonds en euros / Omégas actifs / capacité d'orientation ;
5. trois circuits : Fonds du Commun, cagnotte de Cercle, financement des projets ;
6. retour d'une part de la valeur au Commun ;
7. transparence, decay et confrontation ;
8. statut public : principe stabilisé, mécanismes financiers réels encore en expérimentation et
   soumis à validation juridique.

La page ne publie pas en V1 les taux, coefficients ou formules encore à tester.

### 5.6 `/agir-ensemble/` — Projets, organisations et Commun

**Question répondue** : que devient la transformation lorsqu'elle rencontre le monde réel ?

Trois entrées :

- **Porter un projet / une Chrysalide** : intégrer les qualités de l'Empire sans reproduire sa
  charge destructive ; candidater à un parcours ;
- **Transformer une organisation / un Vaisseau** : autodiagnostic par les Puissances et les
  Cadres, puis proposition de rendez-vous et parcours Monde 1 ;
- **Contribuer au Commun** : voir les besoins du système, rejoindre un projet, proposer une
  capacité, participer à un événement.

Les termes Chrysalide et Vaisseau peuvent rester comme noms symboliques secondaires. Ils ne
doivent plus constituer seuls le premier niveau de navigation.

---

## 6. Réécriture recommandée de `/comprendre-question-5/`

Titre public conservé : **Comment nous réveiller ?**

### Nouvelle promesse

> Nous ne nous réveillerons pas en trouvant enfin le bon récit à imposer aux autres. Nous nous
> réveillerons en apprenant à reconnaître les forces qui nous traversent, à intégrer leurs
> polarités et à construire les cadres où elles peuvent circuler sans se capturer mutuellement.

### Architecture en cinq mouvements

#### 1. Cesser de chercher un nouveau vainqueur

- chaque civilisation compense le déséquilibre de la précédente ;
- la Chrysalide peut reproduire l'Empire qu'elle combat ;
- intégrer n'est ni nier le pouvoir ni glorifier l'Empire ;
- schéma : `capacité → capture → dommages → réintégration → garde-fous`.

#### 2. Réveiller le Moteur individuel

- introduire les sept Puissances en langage concret ;
- montrer Ombre et Lumière comme deux directions ;
- expliquer que le cœur devient un centre de décision, non un substitut sentimental au
  discernement ;
- lien vers la page Moteur.

#### 3. Donner aux Puissances une forme collective

- présenter les cinq couples Puissance–Cadre ;
- expliquer activation, synchronisation et flow ;
- montrer pourquoi un collectif de personnes conscientes peut produire un système toxique ;
- lien vers `Les cadres systémiques` et `Pourquoi le Cercle`.

#### 4. Transformer la croissance en œuvre et en circulation

- du Cercle au projet ;
- l'Oméga reconnaît ce qui a été rendu possible ;
- l'argent réel reste distinct de l'Oméga ;
- une part de la valeur revient au Commun ;
- lien vers l'économie Oméga.

#### 5. Passer de la compréhension à l'expérience

- le site permet de construire une carte ;
- le Monde 0 commence l'expérience personnelle ;
- le Monde 1 relie individu et collectif ;
- CTA principal : **Entrer dans le Monde 0** ;
- CTA secondaire : **Faire le parcours public « Comment nous réveiller ? »** si le visiteur est
  arrivé directement sur cette page.

### Profondeurs proposées à la fin de la page

- `La métamorphose interdite` — contrepoint sur les Chrysalides et la polarisation vertueuse ;
- `Le Point Zéro : un écosystème « méta »` — matrice de récits ouverts ;
- `2040 : de la société de la peur à la société du courage` — projection ;
- `L'écologie interne` — versant individuel ;
- `Les cadres systémiques` — versant collectif.

---

## 7. Nouvelle structure de navigation recommandée

Le menu actuel juxtapose `Comprendre · Écosystème · Ressourcerie · Formats`. Il oblige le
visiteur à comprendre la taxonomie interne du PZ avant de comprendre le PZ.

La nouvelle navigation doit suivre une progression d'usage.

```text
ACCUEIL
│
├── COMPRENDRE
│   ├── Les 5 parcours publics
│   ├── Les 5 questions
│   ├── Le Récit : bascule / Empire et Cité / Marelle
│   └── Articles et bibliographie
│
├── LE JEU
│   ├── Pourquoi un Jeu ?
│   ├── Le Moteur et les 7 Puissances
│   ├── La Marelle et les Mondes
│   ├── Pourquoi le Cercle ?
│   └── L'Oméga
│
├── AGIR ENSEMBLE
│   ├── Porter un projet / une Chrysalide
│   ├── Transformer une organisation / un Vaisseau
│   ├── Projets et besoins du Commun
│   └── Autodiagnostic organisationnel
│
├── RESSOURCES
│   ├── Ressources Point Zéro
│   ├── Pensées
│   ├── Pratiques
│   ├── Chrysalides
│   └── Scénarios, vidéos et cartographies
│
├── ACTUALITÉS & ÉVÉNEMENTS
│   ├── Agenda
│   ├── Festival
│   └── Actualités / newsletters
│
└── [ENTRER DANS LE JEU]
```

### Navigation secondaire et pied de page

- L'association ;
- l'équipe et les partenaires ;
- les Livres ;
- contact ;
- presse ;
- politique de confidentialité et mentions légales.

### Pourquoi cette structure est préférable

- les cinq parcours restent visibles immédiatement depuis l'accueil ;
- le corpus actuel n'est pas dissimulé : il est rangé sous `Comprendre` et `Ressources` ;
- `Le Jeu` explique les concepts avant le CTA d'entrée ;
- `Agir ensemble` remplace la segmentation abstraite par des intentions concrètes ;
- l'association n'est plus confondue avec l'écosystème ;
- les événements ne sont plus dupliqués dans chaque page ;
- l'application devient l'action principale sans priver le site de sa profondeur.

Sur mobile, les cinq entrées peuvent être réduites à quatre : `Comprendre · Le Jeu · Agir ·
Ressources`, avec `Agenda` et `Entrer` comme actions persistantes.

---

## 8. Nouvelles recommandations de sortie du parcours 5

Le bloc final ne doit plus renvoyer vers les pages actuelles par défaut. Il devient dynamique
selon la trace laissée par le visiteur.

| Situation observée dans le parcours | Page essentielle | Approfondissement | Contrepoint |
|---|---|---|---|
| découverte générale des cinq circuits | `/le-moteur-et-les-sept-puissances/` | `/comprendre-question-5/` | `La métamorphose interdite` |
| intérêt pour les règles collectives | `/les-cadres-systemiques/` | `/pourquoi-le-cercle/` | `Le Point Zéro : un écosystème « méta »` |
| intérêt pour le Cercle | `/pourquoi-le-cercle/` | `/le-jeu/` | `L'écologie interne` |
| tension forte autour du financement | `/economie-omega/` | `/ecosysteme-commun/` réécrite | `2040 : société de la peur / du courage` |
| désir de porter un projet | `/agir-ensemble/` | page Chrysalides | `La métamorphose interdite` |

L'ordre des recommandations varie selon le guide :

- le Professeur commence par la page qui stabilise la carte ;
- le Docteur commence par le texte qui met au travail l'angle mort ou le risque de capture.

Le CTA d'entrée dans l'application reste séparé des lectures : approfondir n'est jamais une
condition pour commencer à jouer.

---

## 9. Règle de vérité éditoriale : ne pas vendre l'horizon comme un produit actuel

Chaque page du bloc `Le Jeu / Agir ensemble` doit employer trois marqueurs sobres :

| Marqueur | Sens | Exemples |
|---|---|---|
| **Actif aujourd'hui** | disponible dans l'application ou dans un format réel | Monde 0, profils, Ressourcerie, Cercles V1, événements |
| **En expérimentation** | principe acté, protocole ou économie encore simulé | Cercle Monde 1, decay, Fonds du Commun, autodiagnostic organisationnel |
| **À l'horizon** | direction structurante non disponible | crowdfunding réel, consultations pondérées, métiers PZ reconnus, marketplace complète |

Ce dispositif évite deux écueils : réduire la vision à ce qui existe déjà, ou présenter une
architecture encore expérimentale comme un service contractualisable aujourd'hui.

Les formulations financières doivent rester prudentes. Le site peut expliquer le principe de
l'économie Oméga, mais pas promettre un rendement, une valeur monétaire stable, un droit acquis
sur un fonds ou une conformité juridique non validée.

---

## 10. Séquence éditoriale recommandée

### Lot P5-A — indispensable avant l'intégration du parcours 5

1. réécrire `/comprendre-question-5/` ;
2. créer `/le-moteur-et-les-sept-puissances/` ;
3. réécrire `/les-cadres-systemiques/` ;
4. créer `/economie-omega/` ;
5. créer `/pourquoi-le-cercle/` ;
6. mettre à jour la matrice de recommandations du parcours 5.

### Lot P5-B — rendre l'écosystème compréhensible

1. créer le nouveau `/le-point-zero/` ;
2. créer `/le-jeu/` ;
3. créer `/agir-ensemble/` ;
4. fusionner Introduction et Vision ;
5. transformer Chrysalides, Vaisseaux et Commun ;
6. retirer Explorateurs du premier niveau de navigation.

### Lot P5-C — rendre l'écosystème vivant

1. transformer l'Incubateur en répertoire de projets ;
2. connecter projets, besoins et événements aux données de l'application ;
3. créer les statuts `Actif / Expérimentation / Horizon` ;
4. actualiser Association et partenaires ;
5. relier les articles à un parcours et à une fiche pédagogique.

### Lot P5-D — nettoyage et redirections

1. corriger `/cycle-point-zero/` ;
2. résoudre 12 / 20 verticales ;
3. retirer les blocs Sas/Atelier/témoignages dupliqués ;
4. établir les redirections des pages fusionnées ;
5. vérifier les liens internes et le maillage des cinq parcours.

---

## 11. Critères d'acceptation

L'architecture éditoriale est prête lorsque :

- un visiteur peut expliquer en une phrase la différence entre le diagnostic, le Jeu et
  l'écosystème ;
- le parcours 5 dispose d'au moins une page de fond pour chacune de ses trois acquisitions :
  Puissances/Cadres, Cercle, économie Oméga ;
- aucune page ne présente l'Oméga comme une monnaie échangeable ou dépensable ;
- les cinq correspondances Puissance–Cadre sont identiques partout ;
- la navigation ne demande pas de connaître les termes Explorateur, Chrysalide ou Vaisseau pour
  choisir une action ;
- le corpus Livre I reste accessible sans inscription ;
- les pages publiques ne publient ni cosmogonie imposée ni correspondance entre cinq lectures
  et Mondes ;
- tout mécanisme non disponible porte un statut explicite ;
- les anciens blocs promotionnels ne sont plus répétés sur chaque page ;
- chaque page propose un seul prochain pas principal et, au maximum, trois approfondissements ;
- l'entrée dans l'application est toujours possible sans avoir lu tout le site.

---

## 12. Sources de travail

- `Ressources Point Zero/Livres/PRT-Le Point Zéro - Livre II.docx` ;
- [Révision éditoriale Livre I → Livre II](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/refonte-site-revision-editoriale.md) ;
- [Fonctionnement global de l'écosystème — Q/R](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/ecosysteme-point-zero-questions-reponses-cercle-coeur.md) ;
- [Sept Puissances](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/sept-puissances.md) ;
- [Cercles, profils, flow et Oméga](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/cercles-croissance-profils-flow-omega.md) ;
- [Cosmo Coin Oméga](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/cosmo-coin-omega.md) ;
- [Parcours publics du Sas](https://github.com/PointZero2050/zegame-docs/blob/main/docs/site/parcours-publics-sas.md) ;
- export assaini `migration/import-rails/manifest.json` et contenus HTML associés.
