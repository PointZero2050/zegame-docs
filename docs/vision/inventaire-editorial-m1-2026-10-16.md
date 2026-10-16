# Inventaire éditorial : de l'ancien M0 au nouveau M1

*Poste fixe, 16 octobre 2026, à la demande de Boris. Application de la
[réorganisation M0 / M1 du 15 octobre](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/reorganisation-m0-m1-2026-10-15.md),
§ 4. Lecture seule : rien n'a été modifié dans l'application pour produire ce document.*

## 1. Objet, sources, limites

La note décide de reprendre l'ancien M0 dans le nouveau M1. Ce que les joueurs ont déjà vécu
en M0 en est retiré : les cinq parcours, le Sas, l'Atelier. Les textes qui parlent de ces
étapes, ou qui annoncent « l'entrée en Monde 1 », deviennent donc faux. Ce document les relève
un par un, avec le traitement que la note demande et une proposition de réécriture.

**Sources lues** (`pointzero-app`, `preprod` du 16 octobre) :
- `config/journeys/point-zero-monde-0.yml`, le contrat éditorial des 20 expériences : gestes,
  accroches, explications, CTA, prérequis ;
- les surfaces de l'ancienne coque :
  - `home/index`, `home/_bilan_m0`, `home/monde_1` ;
  - `journeys/_cloture`, `journeys/_cloture_en_attente` ;
  - `config/coque.yml`, `config/badges.yml`, `config/monde_1.yml` ;
- les quiz `config/experience_quizzes/` ;
- les fiches des Guides `config/guides/monde-0|monde-1/fiches.md`.

**Limites, dites franchement :**
- **Les titres et descriptions des expériences vivent en base** (`Challenge#name`, `hook`).
  Seuls les six titres créés par `scripts/seed_parcours_lineaire.rb` sont dans le dépôt.
  - Je n'ai pas lu les pages servies connecté : la recette transversale du portable est en
    cours, et une lecture de fiche n'est pas neutre (marqueurs, excursions).
  - Les titres cités ci-dessous viennent des gestes et de la note. **Un relevé en base par le
    portable doit les confirmer.**
- *Avant le Zéro* contient « l'Atelier » (un forum de fiction) et une scène `M1` : ce sont des
  homonymes, hors sujet, exclus.
- La **composition** n'est pas traitée ici : Journey, ordre réel, preuves, soldes, migration.
  C'est l'inventaire du portable (note § 6). Chaque fois qu'un texte en dépend, c'est indiqué.

## 2. Synthèse, expérience par expérience

Repères : la numérotation historique de la note (E1 → E20) et le slug, qui fait foi.

| # | Slug | Traitement de la note | Textes touchés | Dépend du portable |
|---|---|---|---|---|
| E1 | `faconner-mon-jumeau` | Entrée du nouveau M1 ; rappeler le M0 vécu | 1 ajout (geste 1) | non |
| E2 | `le-point-zero-entrer-dans-le-jeu` | Réorienter vers l'exploration personnelle ; garder Volonté | titre, gestes 1-2 | titre en base |
| E3 | `le-coupable-ideal` | Relier aux grilles vues en M0 | geste 1 (explication) | non |
| E4 | `une-drole-d-epoque` | Introduction : collectif → personnel | geste 1 (accroche, explication) | non |
| E5 | `avant-le-zero` | Idem | geste 1 (explication) | non |
| E6 | `et-moi-dans-tout-ca` | Raccorder au journaling de M0 ; garder Imagination | geste 1 | journaling visible en M1 (fait, lot 3) |
| E7 | `choisir-qui-marchera-a-mes-cotes` | Garder mentor et Émotion | — | non |
| E8 | `l-ecosysteme-point-zero` | Découverte de l'écosystème en M1 | — (relecture faite, rien de faux) | non |
| E9 | `choisir-ma-place-parmi-les-autres` | Profil communautaire ; le profil simple existe depuis M0 | gestes 1-2 | **quel Espace d'échange en M1** |
| E10 | `le-site-du-point-zero` | Retirer la reprise des cinq parcours | **toute l'expérience** | composition, historique |
| E11 | `le-signe-de-reconnaissance` | Reprendre | prérequis (cite E10) | ordre |
| E12 | `choisir-un-double-regard` | Reprendre ; garder Intuition | — | non |
| E13 | `les-choses-se-precisent` | Reprendre | — | non |
| E14 | `lire-mon-moteur` | Reprendre ; garder le choix du cap et Transcendance | — | non |
| E15 | `le-conseil-omega` | Reprendre | — | non |
| E16 | `decouvrir-les-formats` | Ne plus obliger à traverser Sas ou Atelier | geste 2, quiz « Boussole » | non |
| E17 | `le-sas-d-entree` | Retirer du parcours M1 | aucun texte à réécrire | composition |
| E18 | `vivre-l-atelier-point-zero` | Retirer du parcours M1 | aucun texte à réécrire | composition, `mondes.yml` |
| E19 | `mon-recit-de-passage` | Ne plus annoncer d'entrée en M1 ; pas de rite M1 → M2 | prérequis, gestes 1 et 4 | prérequis |
| E20 | `ton-espace-est-pret` | Idem | note d'effet, geste 1 | non |

**Hors expériences** (§ 4) : libellés « Monde 0 » de l'ancienne coque, clôtures du parcours,
conditions des badges des cinq parcours, condition du Cercle dans `coque.yml`, fiches des Guides.

## 3. Le détail, et les propositions

Format : **actuel** (texte servi, `point-zero-monde-0.yml`) → **proposé**. Une proposition est
une base de relecture, pas une décision. Le tutoiement et le vocabulaire du Jeu sont gardés
(Trace, Graine, Puissance, Moteur).

### E1 · Façonner mon jumeau — l'entrée du nouveau M1

La note : « rappeler le passage déjà vécu en M0 ». Rien ne le fait aujourd'hui, puisque E1
était la première expérience du jeu.

- **Geste 1, explication, actuel** : « Donne un visage et un nom à ton Enfant Libre, puis
  accompagne-le dans sa première traversée. […] »
- **Proposé**, une phrase en tête : « Tu as regardé l'histoire du monde par cinq questions,
  puis tu l'as mise à l'épreuve avec d'autres à l'Atelier. Le Monde 1 part de toi. » Puis le
  texte actuel, inchangé.
- ⓘ Pour un facilitateur dispensé d'Atelier, « avec d'autres à l'Atelier » est faux. Variante
  neutre : « Tu as regardé l'histoire du monde par cinq questions. Le Monde 1 part de toi. »
  **Je recommande la variante neutre** : une seule phrase, vraie pour tous.

### E2 · Le Point Zéro : entrer dans le Jeu — garder Volonté

Le titre en base annonce une **entrée dans le Jeu** : en M1, le joueur y est depuis le M0.

- **Titre, proposé** (à trancher par Boris) :
  - « Le Point Zéro : à partir de toi » ;
  - ou « Le Point Zéro, ton hypothèse ».
- **Geste 1 (vidéo d'introduction)**. L'explication actuelle « relie la crise du monde, la
  puissance des récits et la possibilité d'un Point Zéro intérieur ».
  - ⚠️ Les films d'ouverture des cinq parcours (« Fresque du Point Zéro ») couvrent désormais
    la crise et les récits.
  - **Question pour Boris** : cette vidéo reste-t-elle, ou fait-elle doublon ? Si elle reste,
    proposé : « Regarde cette courte introduction. Elle part de ce que tu as exploré en M0 et
    ouvre la question qui suit : et si le Point Zéro passait aussi par toi ? »
- **Geste 2 (la chaîne invisible et l'Hypothèse de seuil)**.
  - Accroche actuelle : « Relie crise, récit et croyance, puis donne une direction à ce qui
    vient de bouger. »
  - Accroche proposée : « Les croyances que tu as explorées en M0 vivent aussi dans tes choix
    les plus ordinaires. Retrouve-les, puis donne une direction à ce qui vient de bouger. »
  - L'explication peut rester.
- **Geste 3 (Volonté)** : inchangé.

### E3 · Le Coupable idéal — relier aux grilles de M0

En M0, le parcours « Qu'est-ce qui nous paralyse ? » fait manipuler cinq cartes (Récit,
Croyances, Cadres systémiques, Écologie interne, Écologie externe) et révèle une **boucle** :
aucune cause n'agit seule. Le procès d'E3 fait accuser des forces. Le raccord est naturel.

- **Explication, proposé**, une phrase en tête : « Au Monde 0, tu as vu qu'aucune cause n'agit
  seule. Ici, la question devient personnelle : vers qui ton doigt se tourne-t-il d'abord ? »
  Puis le texte actuel.

### E4 · Une drôle d'époque · E5 · Avant le Zéro — introductions

Les contenus restent distincts (note). Seule l'entrée change : de l'histoire collective vue en
M0 à la situation personnelle.

- **E4, accroche, actuel** : « Tes choix mettent déjà ton Moteur en mouvement. »
- **E4, accroche, proposé** : « L'époque que tu as regardée de loin, tu la traverses aussi en
  semaine. Tes choix mettent déjà ton Moteur en mouvement. »
- **E5, explication, proposé**, en tête : « Les futurs que tu as confrontés au Monde 0
  deviennent ici une expérience vécue de l'intérieur. » Puis le texte actuel.

### E6 · Et moi dans tout ça ? — le journaling de M0

Le journaling de préparation à l'Atelier (« Mon histoire dans celle de l'humanité », trois
réponses) est désormais une Trace **révélée en M1** (lot 3 du portable). E6 est l'endroit que
la note désigne pour le reprendre.

- **Geste 1, explication, actuel** : « Relis les choix, miroirs et hypothèses produits depuis
  le début du parcours. […] »
- **Proposé** : « Relis les choix, miroirs et hypothèses produits depuis le début du parcours,
  et les trois réponses que tu as écrites avant l'Atelier. Repère ce qui continue de vibrer ou
  de résister. »
- ⓘ Même réserve qu'en E1 pour un dispensé : il n'a rien écrit avant un Atelier.
  - Soit la phrase reste vraie parce qu'elle ne dit « et » que si la Trace existe (portable :
    un local ou une condition).
  - Soit on écrit « et, si tu en as écrit, tes réponses de préparation à l'Atelier ».
  - **Recommandé : la condition côté serveur**, pour une phrase propre.

### E9 · Choisir ma place parmi les autres — le profil existe déjà

- **Geste 1.**
  - Titre actuel : « Compose ton Profil » ; titre proposé : « Enrichis ton Profil ».
  - Explication proposée, en tête : « Ton profil existe depuis le Monde 0 : un prénom, une photo
    si tu l'as choisie, une présentation. Ici, il devient communautaire. » Puis le texte actuel
    à partir de « complète au moins un repère… ».
- **Geste 2**. L'actuel : « Entre dans l'Espace du Monde 0 et réagis », et « Retrouver
  l'Espace du Monde 0 ».
  - ⚠️ **Dépend du portable** : en M1, quel Espace ? Celui du Monde 1 ou un espace de
    bienvenue ? Le texte suit sa réponse.
  - Proposé par défaut : « Entre dans l'Espace du Monde 1 et réagis ».

### E10 · Le site du Point Zéro — à retirer

Les deux gestes ne parlent que des cinq parcours, désormais vécus en M0 :
- « Entre par l'une des cinq questions… accomplis au moins un parcours public » ;
- « Choisis jusqu'où poursuivre ».

Aucun geste distinct ne survit, et le compteur « X badges obtenus sur 5 » fait doublon avec la
Progression du M0.

- **Recommandé : retirer l'expérience entière du parcours M1.**
  - Côté portable, il faut garder l'objet et son historique : validations, badges, Ω. On ne
    le supprime pas.
- **Conséquences textuelles** :
  - le prérequis d'E11 (« Après « Le site du Point Zéro » ») ;
  - les cinq badges des parcours (§ 4.3) ;
  - `import-sas.js` sur la fiche (#389), qui n'aura plus de fiche.

### E11 · Le signe de reconnaissance

- **Prérequis, actuel** : « Après « Le site du Point Zéro » ». **Proposé** : le prérequis
  réel suivra l'ordre fixé par le portable. À réécrire une fois l'ordre connu.

### E16 · Découvrir les formats — sans obligation de Sas ni d'Atelier

- **Geste 2, accroche, actuel** : « Sas, atelier, formation ou Festival ne font pas vivre la
  même chose. »
  - Proposé : « Un Sas, un Cercle, une formation ou le Festival ne font pas vivre la même
    chose. »
- **Quiz « La Boussole de passage »** (`la-boussole-de-passage.yml`, options) :
  - `atelier` : « L'Atelier Point Zéro — 3 h […] Le rite qui ouvre le Monde 1. » **Faux en
    M1** : le joueur l'a vécu. **Recommandé : retirer l'option.**
  - `sas` : « Le Sas d'exploration — 1 h 30, en ligne, gratuit. Pour voir de quoi il s'agit
    sans s'engager. » Le Sas reste un format indépendant (note § 3). En M1, il s'adresse
    plutôt à un proche. Proposé : « Le Sas d'exploration — 1 h 30, en ligne, gratuit. Pour
    revenir aux bases, ou y inviter quelqu'un. »
  - **À ajouter, si Boris le veut** : une option `cercle`, « Rejoindre un Cercle — facultatif ;
    pour les parcours collectifs du Monde 1. », qui renvoie vers `/cercles`.
  - ⚠️ Le Cercle est facultatif (note § 4). La Boussole peut le proposer, jamais l'exiger.
  - `organisation`, `festival`, `pas_maintenant` : inchangés.

### E17 · Le Sas · E18 · L'Atelier — retirés du parcours

Rien à réécrire dans leurs textes : ils ne seront plus servis comme étapes.

- **À ne pas oublier** :
  - `config/mondes.yml` porte `presence_requise: vivre-l-atelier-point-zero` pour ouvrir le
    Monde 1. C'est le portable qui décide de ce qui ouvre désormais le M1 (le nouvel Atelier
    du M0).
  - `config/heros/catalogue.yml` cite « Vivre l'Atelier Point Zéro ».

### E19 · Mon récit de passage — ne plus annoncer le M1

- **Prérequis, actuel** : « Atelier confirmé ». **À remplacer** par l'expérience qui la précède
  dans le nouvel ordre (portable).
- **Geste 1, explication, actuel** : « Rassemble les Traces […] qui ont marqué ton Monde 0. »
  - Proposé : « Rassemble les Traces, Graines, miroirs, résonances et choix qui ont marqué ta
    traversée. »
  - Le mot « traversée » vaut pour M0 et M1 à la fois.
- **Gestes 2 et 3** (mentor, Graine de passage) : inchangés. « Passage » y désigne une
  transformation personnelle, pas un changement de Monde.
- **Geste 4, Carte du Seuil** : l'explication est juste (« Cette Carte reste privée »).
  - ⚠️ **Le nom « Carte du Seuil » évoque un seuil franchi**, et la note interdit d'inventer
    un rite M1 → M2.
  - **Recommandé : garder le nom**, car c'est un objet en base (Trace, page `carte_du_seuil`).
    Le seuil est celui de la traversée personnelle. On ne réécrit aucune promesse de Monde.
  - À trancher par Boris.
- **Titre de l'expérience** (en base) : « Mon récit de passage ». À garder ou à remplacer par
  « Mon récit de traversée ». **Boris.**

### E20 · Ton espace est prêt

- **Note d'effet, actuel** : « Transforme l'accueil, n'ouvre pas le Monde 1. »
  - Proposé : « Transforme l'accueil en tableau de bord. »
- **Geste 1, explication, actuel** : « […] Ce geste transforme l'accueil en tableau de bord —
  il n'ouvre pas, à lui seul, le Monde 1. »
  - Proposé : « […] Ce geste transforme ton accueil en tableau de bord : tu y retrouves tes
    Puissances, tes Traces et ce que le Monde 1 t'ouvre ensuite. »
  - ⚠️ Aucune mention du Monde 2.
- ⓘ « Relis tes **sept** Puissances éveillées ».
  - Vérifié dans `SequenceDeGestes` (`SAS_D_EVEIL`, `EVEILS_PAR_FAIT`) : Désir (E1), Volonté
    (E2), Imagination (E6), Émotion (E7), Communication (E9), Intuition (E12), et
    Transcendance au premier cap du Moteur (E14).
  - Le compte reste juste si E10, E17 et E18 partent : aucune découverte de Puissance n'y vit.

## 4. Hors des expériences

### 4.1 Les libellés « Monde 0 » de l'ancienne coque

L'ancien M0 devient le M1. Ses libellés visibles « Monde 0 » deviendront faux. Ils sont
nombreux dans `journeys/_show`, `layouts/jeu`, `layouts/_coque_m0`, `home/monde_0`,
`home/_bilan_m0`, `challenges/_fiche_joueur`, `coque.yml`, `badges.yml`… Beaucoup sont des
commentaires : le relevé exact se fera au moment de la réécriture.

- **Dépend du portable** :
  - le nom du Journey en base (« Point Zéro - Monde 0 ») ;
  - le numéro de Monde de sa communauté ;
  - le kicker « Monde 0 · … », qui est dérivé.

  Je propose que **le portable fixe d'abord le nom et le numéro en base**, puis que je reprenne
  les libellés écrits en dur, d'un seul passage.

### 4.2 Les clôtures du parcours

| Surface | Actuel | Proposé |
|---|---|---|
| `home/index` | « Toutes les Actions du Monde 0 sont accomplies. Le passage vers le Monde 1 approche. » | « Toutes les Actions de ton entrée dans le Monde 1 sont accomplies. » |
| `home/_bilan_m0` | « Tu as traversé le Seuil du Monde 0. […] Tu seras averti dès que ton passage au Monde 1 est validé après ta participation à l'atelier. » | à retirer de l'ancienne coque. Le bilan du M0 vit désormais dans le nouveau M0 (`monde_zero/_bilan`) |
| `journeys/_cloture` | « L'Atelier Point Zéro reste à vivre pour ouvrir le Monde 1. Ses Omégas te seront attribués après validation par le facilitateur. » | à retirer : il n'y a plus d'Atelier dans ce parcours |
| `journeys/_cloture_en_attente` | « […] L'Atelier Point Zéro suit son propre rythme […] » | à retirer pour la même raison |

### 4.3 Les badges des cinq parcours (`config/badges.yml`)

- **Actuel** : « Achever le parcours public « Qu'arrive-t-il à l'humanité ? » », puis les
  quatre autres, sur le même modèle.
- **Proposé** : « Accomplir l'exploration « Qu'arrive-t-il à l'humanité ? » ».
- Les parcours ne sont plus publics : ils se vivent dans le M0 de l'application (décision de
  Boris du 16 octobre).
- **Indépendant du M1** : à faire dès la fermeture de `/sas`, avec la galerie des jeux.

### 4.4 Le Cercle (`config/coque.yml`)

- **Actuel** : « S'ouvre au Monde 1, quand ton Cercle naît. »
- La note : le Cercle est **facultatif**, et prérequis des seuls parcours collectifs.
- **Proposé** : « S'ouvre au Monde 1. Facultatif : un Cercle n'est nécessaire qu'aux parcours
  collectifs. »

### 4.5 Les fiches des Guides (`config/guides/`)

Les Guides ont un contexte canonique par Monde.

- **Monde 0** (`monde-0/fiches.md`) :
  - « Le site est un Sas public : il donne accès aux […] parcours légers » ;
  - « À partir du Monde 1, le Cercle devient le collectif de soutien dans lequel les
    expériences » ;
  - « Le Monde 1 commence en autofacilitation… ».
- **Monde 1** (`monde-1/fiches.md`, M1-05 à M1-08 sur le Cercle) : le Cercle y est présenté
  comme le cadre du Monde 1, sans le dire facultatif.
- ⚠️ **Ce sont des sources de réponse pour un LLM**. Une fiche fausse fait dire une chose
  fausse au Guide, avec aplomb.
- **Proposé** :
  - une phrase de cadrage dans M1-05 : « Rejoindre un Cercle est une suite possible du
    tutoriel, jamais une obligation : il n'est requis que pour les parcours collectifs. » ;
  - la mention « parcours légers » du site retirée de la fiche Monde 0.
- ⓘ Ces fiches relèvent du canon de Codex : **à lui transmettre**, plutôt qu'à réécrire ici.

## 5. Ce qui revient à Boris

| # | Décision | Recommandation du poste fixe |
|---|---|---|
| 1 | **Séquence finale et titres** du M1 (note § 7) | L'ordre actuel moins E10, E17 et E18 ; titres à revoir pour E2 et E19, les autres gardés |
| 2 | **E10** : retirer l'expérience entière ? | Oui, aucun geste distinct ne survit |
| 3 | **E2** : garder la vidéo d'introduction ? | À juger après avoir revu les films d'ouverture des cinq parcours : risque de doublon |
| 4 | **E16** : retirer l'option Atelier de la Boussole, proposer le Cercle ? | Retirer l'Atelier ; ajouter le Cercle comme option facultative |
| 5 | **E19** : garder « Mon récit de passage » et « Carte du Seuil » ? | Garder les noms (objets en base), changer les explications seulement |
| 6 | **Phrases du rappel M0** (E1, E6) : neutres pour tous, ou conditionnées ? | E1 neutre ; E6 conditionnée côté serveur |
| 7 | **Répartition des 100 Ω** du M1 (note § 7) | — (le portable chiffre, après retrait des blocs) |

### Décisions de Boris (16 octobre 2026, réponse à ce tableau)

Boris : « Ok pour tes recommandations », avec trois précisions.

1. **Séquence** : l'ordre actuel moins E10, E17 et E18.
2. **E10** : retirée entière (l'objet et son historique restent en base).
3. **E2** : **la vidéo d'introduction est conservée.** Boris l'adaptera lui-même pour ne pas
   répéter ce que montre le M0. Le texte du geste 1 l'annonce dans ce sens.
4. **E16** : l'option Atelier est retirée. Elle est **remplacée par une découverte des
   Cercles, sans création ni adhésion**. Rejoindre ou créer un Cercle sera l'objet d'un
   **parcours recommandé mais optionnel, qui prolonge le parcours d'entrée du M1**. La Boussole
   fait connaître ; elle n'inscrit pas.
5. **E19** : les noms « Mon récit de passage » et « Carte du Seuil » sont gardés. Seules les
   explications changent.
6. **Rappel du M0** : E1 avec une phrase neutre ; E6 avec la mention de la préparation
   seulement si la Trace existe (condition côté serveur).
7. **100 Ω** : chiffrés par le portable après les retraits.

⚠️ **Le titre d'E2** reste à choisir. Deux propositions : « Le Point Zéro : à partir de toi »
ou « Le Point Zéro, ton hypothèse ». Le titre vit en base.

## 6. Ce qui revient au portable

- **Relever en base les titres et descriptions** (`name`, `hook`) des expériences E1 → E20.
  Ce document n'a pu lire que le contrat YAML.
- **Composition** :
  - ordre ;
  - retrait d'E10, E17 et E18 sans perte d'historique ;
  - nouveaux prérequis (E11, E19) ;
  - ce qui ouvre désormais le Monde 1 (`mondes.yml`).
- **Nom et numéro du Journey et de sa communauté** : préalable au relevé des libellés
  « Monde 0 » (§ 4.1).
- **E9** : quel Espace d'échange en M1.
- **E6** : un moyen de savoir si la Trace de préparation existe, pour une phrase conditionnée.

## 7. Suite proposée

1. Boris tranche le § 5 (une séance suffit : la plupart sont des oui ou non).
2. Le portable fixe la composition et les noms (§ 6).
3. Le poste fixe réécrit, en une PR :
   - les textes du contrat YAML ;
   - les surfaces du § 4 qui sont à lui ;
   - les bancs qui lisent ces textes, dans la même livraison.

   Les fiches des Guides partent à Codex.
