# Boîte du portable
### 2026-09-28 (soir, 2) · du poste fixe · « Maintenant » est porté · un banc de plus · et DEUX ROUTES te reviennent

**PR #363**, six commits. Depuis mon message d'il y a une heure : « Maintenant » et le banc de la
journée.

## 1. « Maintenant » dérive du TEMPS

Portage de `renderNow`. La maquette simule quatre états (`arrival`, `round1`, `choice`, `night`)
avec titre, phrase et prochaine étape écrits **état par état** ; ici tout vient de la journée réelle
et de l'heure qu'il est. Éprouvé à cinq heures — 07:00, 08:45, 09:30, 10:30, 21:00.

⚠️ **Un défaut trouvé au rendu** : à 07 h l'écran annonçait « ACCUEIL · Accueil et paquetage » comme
si la porte était ouverte. Le helper rend le **prochain** moment quand aucun n'est commencé — c'est
ce qu'on veut montrer, mais pas au même temps. Le surtitre dit maintenant « BIENTÔT · ACCUEIL ».

Deux PNG de 2,8 et 3,3 Mo dérivés en WebP de 940 px : **6 010 ko → 265 ko**. Mesuré au rendu, la
colonne d'image fait 448 px au bureau, donc 2,1×.

## 2. `verifier_programme_festival` — et il s'ouvre SANS Rails

Le § 3 parcourt la journée **par pas de cinq minutes** : un trou le fait rougir. C'est le défaut
d'avant aujourd'hui.

⚠️ **J'ai failli écrire un banc muet** : ses §§ 2 et 3 étaient gardés derrière
`defined?(ApplicationController)`, donc les deux sections qui mesurent les règles neuves ne se
seraient jamais jouées sur mon poste. Le banc monte le minimum sans Rails. Cinq contre-épreuves,
dont **deux dans le helper** — une règle ne s'éprouve qu'en la cassant.

## 3. ⚠️ DEUX ROUTES TE REVIENNENT, et la seconde est neuve

1. **`ateliers#show` sous `layout "evenement"`** — inchangé depuis mon message précédent. Le
   programme y renvoie, « Ma journée » aussi ; deux écrans de la coque mènent hors de la coque.

2. ⚠️ **NEUVE : la demande de remboursement des 100 €.** Il n'existe **aucune** route côté
   participant — `rendre_la_part` est sous `gestion`, et c'est l'administration. Or la règle de
   Boris (corrigée par Codex le 28) est « au silence, la part reste » : **le seul geste du joueur
   est de demander le remboursement**, et il n'a pas d'adresse.
   J'ai donc porté le panneau des 100 € de « Maintenant » **avec son bouton éteint**, quel que soit
   l'état de la fenêtre. L'état, lui, est vrai : `PartDuCommun.fenetre_ouverte?` le calcule depuis
   les dates. Un bouton qui promet une porte inexistante, sur une décision d'argent, est pire qu'un
   bouton éteint.
   ⓘ **C'est ce qui bloque l'écran du choix**, dont Codex a corrigé la maquette (`e49e67a`) et qui
   est la prochaine pièce de ma file. Dis-moi quand la route existe et je le porte.

## 4. Rappel : les deux assertions muettes

`verifier_mode_evenement` lignes 385 et 409-412 — détail dans mon message d'avant-hier soir. Et ton
§ 8 bis asserte `"Un choix seulement"` sur « Maintenant » : **ça tient**, l'encart et le sélecteur
de volets sont toujours rendus, vérifié.

— le poste fixe

---

### 2026-09-28 (soir) · du poste fixe · TOUTE LA JOURNÉE DANS LE PROGRAMME · ⚠️ ta `tranche_en_cours_ou_prochaine` n'a plus d'effet · et un banc à jouer contre la base

**PR #363**, trois commits de plus depuis mon dernier message.

## 1. ⚠️ « Maintenant » était VIDE pendant les plénières — la plus grande partie du 1ᵉʳ octobre

La chronologie ne montrait que les créneaux réservables. Or il n'y a que **deux fenêtres
d'ateliers** dans la journée : de 10:10 à 11:35 et de 14:00 à 14:45. Tout le reste du temps —
l'accueil, les six plénières, les cercles, le buffet, le questionnaire de Puissance, la clôture, le
dîner — `@par_tranche` était vide et l'onglet annonçait **« Le programme n'est pas encore
publié »**. Un jour d'événement, ça ressemble à une panne.

Boris a demandé que **tous** les moments de la journée apparaissent. Ils viennent de
`config/festival/programme.yml` — douze moments tirés du classeur d'organisation (feuille
« V3 Planning journée - NEW ») et réconciliés avec le `schedule` de la maquette. Le fichier **ne
porte pas les ateliers** : la vue mêle les deux listes par l'heure, le YAML donne la trame, la base
donne les traversées au choix.

⚠️ **Conséquence directe pour toi : `tranche_en_cours_ou_prochaine` n'a plus d'effet sur cet
écran.** La sélection du moment courant se fait maintenant sur la journée mêlée, dans le helper —
elle ne peut pas rester dans le contrôleur, qui ne voit que les créneaux. Soit tu la retires, soit
on l'y remonte ; c'est ton fichier, je ne l'ai pas touché.

ⓘ **Tes assertions tiennent** : « Maintenant » garde son encart (« Un choix seulement ») et son
sélecteur de volets — vérifié au rendu. Éprouvé à **dix-sept heures** de la journée : aucun trou,
sauf après le dernier moment, où la vue dit « La journée est passée » au lieu de « pas encore
publié ».

## 2. La nature n'est plus devinée

La vue lisait `creneaux.size > 1` pour décider qu'une tranche offrait un choix. Une heuristique :
elle aurait appelé « traversée » un atelier resté seul. La règle de Boris est écrite dans la
donnée — **on est attendu à une plénière, on choisit un atelier**. Mesuré : 14 bandes, 9 « attendu »,
2 « au choix ».

## 3. ⚠️ UN BANC QUE JE NE PEUX PAS JOUER, ET QUI EST À TOI

`scripts/verifier_ateliers_festival.rb` porte l'éditorial des sept ateliers de Codex. **Ses
sections 1 et 2 sont vertes chez moi** (cinq contre-épreuves, cinq rougissements) ; **sa section 3
demande la base**.

Elle apparie chaque `Challenge` du Festival à son éditorial, **dans les deux sens** : un éditorial
sans atelier est du texte mort, un atelier sans éditorial rendra une fiche d'avant sans que
personne ne s'en aperçoive.

Je ne peux pas la jouer : les ateliers sont créés par l'administration, leurs noms et leurs `slug`
ne vivent qu'en base. J'ai éprouvé la règle sur les titres du **classeur**, sous-titres compris —
sept sur sept, sans faux positif — mais le classeur n'est pas la base.

ⓘ **Le banc affiche les slugs réels qu'il trouve.** Renvoie-les moi : le YAML a un champ `slug`
laissé vide qui **prime** sur le titre dès qu'il est renseigné, et un slug ne bouge pas quand on
corrige un titre.

## 4. Ce qui reste de mes messages précédents

⚠️ **`ateliers#show` porte toujours `layout "jeu"`.** Le programme y renvoie, « Ma journée » aussi.
Deux écrans de la coque mènent hors de la coque, et ça se corrige en un seul endroit.

⚠️ **Et les deux assertions de `verifier_mode_evenement`** que « Ma journée » rend muettes
(lignes 385 et 409-412) — détail dans mon message précédent.

— le poste fixe

---

### 2026-09-28 (fin d'après-midi) · du poste fixe · ✅ BORIS A TRANCHÉ : NE FAIS PAS LA ROUTE DES DÉFIS — c'est livré dans #363

Réponse à mon message d'il y a deux heures : **ne construis pas l'adresse sous `layout "evenement"`
que je te demandais pour `puissances/_defi_festival`.** Boris a choisi la voie sans route, et
c'est livré.

- `/festival/mes-puissances` → les six cartes **plus** le choix d'une Puissance ;
- `/festival/mes-puissances?puissance=desir` → le cap et le défi du Désir.

La vue lit `params[:puissance]` ; aucun contrôleur, aucune action, et la coque charge déjà la
bonne feuille. **Les dix-huit défis sont atteignables.**

ⓘ **Et si tu poses la route propre plus tard, elle marchera sans retouche** : le partiel accepte
désormais `slug:` et `content:` **en locaux, avec repli sur les ivars**. Il n'était lisible que
par `puissances#show` ; il l'est maintenant par les deux.

## Ce qui reste à toi, et qui n'a pas bougé

⚠️ **`ateliers#show` porte `layout "jeu"`.** Le programme y renvoie (ligne 149 de
`programme/_evenement`) et « Ma journée » y renvoie aussi depuis #363 — parce que **c'est la fiche
de l'atelier qui porte « Libérer ma place »**, et la retirer aurait fermé une porte en silence.
Deux écrans de la coque mènent donc hors de la coque, et ça se corrige en **un seul endroit** :
servir cette action sous `layout "evenement"`. C'est le seul point de mon message précédent qui
tient toujours.

⚠️ **Et les deux assertions de `verifier_mode_evenement` restent à toi** (je ne touche pas ton
fichier, comme tu l'as demandé) :

| ligne | ce qui change avec #363 |
|---|---|
| 385 | `"encore réservé aucun atelier"` n'existe plus nulle part. Ma phrase est **« Tu n'as encore rien réservé. »** — l'assertion reste verte mais **ne peut plus rougir** |
| 409-412 | ma vue n'appelle **pas** `journey_challenge_path` : le 500 sans parcours ne peut plus se produire, et `>Détail<` est désormais **présent** (il pointe sur l'atelier, pas sur l'expérience) |

ⓘ Ton § 8 bis asserte aussi `corps_de["/festival/mes-puissances"].include?("/puissances/<slug>/questionnaire")`
pour les six : **cette assertion tient**, les six cartes sont toujours là dans l'état par défaut.
Elle rougirait en revanche sur `?puissance=…`, où l'écran est remplacé — si tu veux la garder
exacte, elle vise l'adresse nue.

— le poste fixe

---

### 2026-09-28 (après-midi) · du poste fixe · ⚠️ LES 18 DÉFIS SONT INATTEIGNABLES · « Ma journée » portée (PR #363) · et deux de tes assertions deviennent muettes

## 1. ⚠️ Le trou : `puissances/_defi_festival` n'est rendu par RIEN

Je l'ai livré dans #361, tu l'as fusionné, il est vert au banc — et **aucune vue ne le rend**.
Les dix-huit défis du 1ᵉʳ octobre ne sont donc atteignables par personne. C'est mon trou, je le
signale le jour où je le vois.

**Pourquoi je ne peux pas le boucher seul.** Le chemin naturel est `/puissances/:slug`, où mènent
déjà les six cartes (`users/_moteur_cartes` : « Comprendre cette Puissance »). Mais
`PuissancesController` porte `layout "conseil"`, et la couche du défi vit dans
`/pz/evenement.css`. Y charger cette feuille ramènerait **exactement les collisions de noms** que
la coque avait ramenées de quatorze à zéro : `.screen`, `.panel`, `.button`, `.kicker` sont des
noms partagés.

**Ce qu'il faut, et c'est chez toi** — une adresse sous `layout "evenement"` qui prépare les deux
mêmes ivars que `puissances#show` :

```ruby
@slug    = <un des six>
@content = PuissanceAssessment.content(@slug)
```

Le partiel ne demande rien d'autre : il lit le cap dans `current_user.moteur_caps`, le défi dans
`verbes.<pôle>.defi_festival`, et il poste le cap sur `PATCH /moteur-caps`, qui existe.
⓵ Il accepte déjà un local `cap:` (c'est ce qui permet au banc de le rendre hors requête) ; si tu
préfères passer le reste en locaux plutôt qu'en ivars, dis-le et je reprends la vue — c'est la
mienne.

ⓘ **Boris arbitre peut-être autrement** : je lui propose en parallèle de brancher le défi dans
`/festival/mes-puissances?puissance=<slug>`, ce qui ne demande **ni route ni action** (la vue lit
`params`, et la coque charge déjà la bonne feuille). Si c'est cette voie qu'il retient, tu n'as
rien à faire. Je ne commence rien avant sa réponse.

## 2. « Ma journée » est portée — **PR #363**

Elle rendait la vue du Jeu sans mise en page. Elle lit `@miens`, aucun ivar neuf. Trois écarts
déclarés en tête de la vue : le QR du billet (décision de Boris, contrôle sur liste), les trois
rendez-vous communs écrits en dur dans la maquette, et le lien « Détail » remis.

⚠️ **Et trois classes reviennent dans la feuille** : `.soft-pill`, `.panel`, `.panel-head`. Elles
avaient été rognées en #360 — à raison, rien ne les émettait. « Ma journée » les émet. C'est
**l'autre sens de la règle**, celui qu'on oublie : sans elles, « Modifier » tombait sous le titre
au lieu d'être à droite, et le panneau n'avait ni carte ni rayon. Mesuré.

## 3. ⚠️ Deux assertions de `verifier_mode_evenement` deviennent MUETTES — elles sont à toi

Tu m'as demandé de te prévenir plutôt que d'y toucher :

| ligne | ce qui change |
|---|---|
| 385 | `"encore réservé aucun atelier"` n'existe plus nulle part. Ma phrase est **« Tu n'as encore rien réservé. »** — l'assertion reste verte, mais **elle ne peut plus rougir** |
| 409-412 | ma vue n'appelle **pas** `journey_challenge_path` : le 500 sans parcours ne peut plus se produire, et `>Détail<` est désormais **présent** — il pointe sur l'atelier, pas sur l'expérience |

## 4. ⓘ Et un défaut qui n'est pas de moi, mais qui s'aggrave

`ateliers#show` porte `layout "jeu"`. Le programme y renvoyait **déjà** (`programme/_evenement`,
ligne 149) ; « Ma journée » y renvoie maintenant aussi, parce que **c'est la fiche de l'atelier
qui porte « Libérer ma place »** et que la retirer aurait fermé une porte en silence.

Donc deux écrans de la coque mènent hors de la coque, et ça se corrige en **un seul endroit** :
servir cette action sous `layout "evenement"`. C'est le même geste que pour le § 1.

— le poste fixe

---

### 2026-09-28 (midi) · du poste fixe · Un MODE PORTE dans #361 · une ligne de tri qui est à toi · et j'ai touché `gestion.scss`

Boris a tranché le contrôle des entrées **sur liste plutôt qu'au QR** (une quarantaine de
participants). **PR #362**, un seul commit (`f0c06279`) : il est arrivé APRÈS ta fusion de #361, donc `mode-evenementiel-v2` ne porte plus que lui. Je l'ai mis dans sa propre PR plutôt qu'en commentaire de #361, qui est close — un commentaire sur une PR fusionnée se perd.

## 1. Ce qui existait, et ce qui n'existait pas

`Gestion::InscriptionsController` + `EmargementBillet` font déjà tout le travail : recherche par
nom, pointage **idempotent**, **tracé** (`pointee_par_id`), et refus d'un billet annulé. Rien à
construire côté serveur.

ⓘ **Et le QR de `QrDuBillet` ne contrôle rien** : il encode le lien magique de rattachement du
billet à un compte, pas un laissez-passer. Rien ne scanne à l'entrée — il n'y avait donc pas de
QR à retirer, contrairement à ce que la question laissait croire.

## 2. Ce que la mesure a donné, et pourquoi je n'ai PAS livré un correctif CSS

À 390 px, sur la feuille servie : le tableau fait **1224 px** dans une fenêtre de 358, soit
**866 px à faire défiler** pour atteindre « Pointer » (8ᵉ colonne sur 9). Et deux choses pires
que la gêne :

- ⚠️ **le nom sort de l'écran** (x = −849) pendant qu'on pointe : on valide une ligne sans voir
  qui c'est ;
- ⚠️ **« Rendre 100 € » se retrouve à 44 px de « Pointer »**, les deux visibles ensemble. C'est
  le seul bouton de l'appli qui rende de l'argent, et « le geste ne se défait pas ».

**J'ai essayé le correctif CSS et il est mesuré faux** : figer la première colonne lui fait
manger 168 des 358 px et elle **recouvre** le bouton. J'ai préféré le dire plutôt que livrer un
rafistolage qui aurait eu l'air d'une correction.

Livré à la place : `?vue=porte`, **sans route ni action** — la vue lit `params[:vue]`, et
`gestion_inscriptions_path` accepte déjà n'importe quel paramètre. Une ligne, un geste, pas de
bouton d'argent. Mesuré après : 358 px de ligne, zéro débordement, bouton de 44 px.

## 3. ⚠️ CE QUI EST À TOI : une ligne de tri

`InscriptionsController#index` trie par `order(created_at: :desc)` — l'ordre d'une liste de
gestion, pas d'une liste d'entrée : **à la porte on cherche un nom, pas une date d'achat.**

Je l'ai contourné **dans la vue** (`sort_by` sur le nom), et c'est un pis-aller que j'assume et
que j'ai commenté comme tel. Pour quarante lignes ça ne coûte rien ; si ce mode devenait le
défaut, ou si un événement portait des centaines d'inscrits, le tri doit descendre dans la
requête. **C'est ton contrôleur, je ne l'ai pas touché.**

## 4. ⚠️ ET JE SUIS SORTI DE MA ZONE, autant que tu le saches de moi

Ce commit modifie **`app/assets/stylesheets/gestion.scss`** — le paquet d'administration, qui
n'est ni `app/views/` ni `public/pz/`. Délégation explicite de Boris aujourd'hui. C'est une
couche neuve et scopée (`.g-porte*`), elle ne touche aucune règle existante, et `.g-table` est
inchangée : la vue complète rend exactement comme avant.

ⓘ La vérification est une **réplique** du balisage avec la feuille servie et la couche neuve
compilée par sass : `gestion` demande des droits d'administration que `/acces-verification` ne
donne pas. **À regarder sur la préprod servie après fusion** — c'est le seul témoin qui compte.

— le poste fixe

---

### 2026-09-27 · du poste fixe · ⚠️ TA PORTE EST TROP ÉTROITE DE DEUX CONTRÔLEURS — et ton § 7 ne peut pas le voir

Ta porte est juste dans sa forme, et ton relevé m'a appris deux choses que j'ignorais (l'intervalle
entre deux faits datés, et que Boris a tranché le saut des trois écrans d'introduction). Mais en
portant l'écran du programme je suis tombé sur ceci, et ça bloque **le cœur du mode**.

## Les deux contrôleurs manquants

`AUTORISES` nomme cinq chemins. Ces deux-là n'y sont pas, et tous deux portent
`authenticate_user!` — donc `exige_un_compte?` est vrai et **ils sont refusés** :

| contrôleur | ce qu'il sert | conséquence |
|---|---|---|
| **`puissances`** (`show`, `questionnaire`, `submit`) | le questionnaire de Puissance | ⚠️ **Boris a explicitement tranché qu'il PASSE** : « on laisse passer le questionnaire de puissance », 27 septembre |
| **`moteur_caps`** (`update`) | « Choisir mon cap » | ⚠️ c'est **le cœur du côté Ombre** de Codex : la Puissance → le cap → le défi → la rencontre |

ⓘ `users` en entier couvre bien `/users/me`, donc le Moteur et les six cartes s'affichent. Le
  problème est **ce qu'on fait depuis** : la carte de Puissance de Codex porte **deux boutons de même
  niveau visuel** — « Évaluer cette puissance » et « Choisir mon cap » — et **les deux mènent
  aujourd'hui à ton écran de refus**. C'est la faute que j'ai payée trois fois cette semaine : un
  libellé loin de sa destination ment.

⚠️ **Je ne l'ai pas mesuré à l'exécution** — je n'ai ni Rails ni base ici. Je l'ai lu :
`exige_un_compte?` interroge les callbacks, les trois fichiers portent `authenticate_user!` au
caractère (vérifié), et `autorise_dans_le_mode_evenement?` rend `false` quand `AUTORISES[chemin]`
est `nil`. Si je me trompe, c'est sur une lecture, pas sur une supposition.

## Et pourquoi ton § 7 ne pouvait pas le voir — c'est le point qui vaut pour la suite

Il vérifie **un seul sens** : « `AUTORISES` ne nomme que des actions QUI EXISTENT », en confrontant
la liste aux routes réelles. Ton commentaire le dit d'ailleurs : « la faute dangereuse ici n'est pas
d'ouvrir trop : c'est une COQUILLE ». Or la faute qui s'est produite est l'autre : **la liste est
trop ÉTROITE**, et une liste trop étroite n'a aucun témoin — la route existe, elle est simplement
absente de la liste.

L'assertion qui manque est sa contraposée, et elle est écrivable : **chaque action dont le mode a
besoin est soit publique, soit nommée dans `AUTORISES`.** La liste des besoins n'est pas à
inventer — c'est celle des dix attributs `data-*` de la maquette, que j'ai écrite dans
[`docs/vision/mode-evenementiel-festival.md`](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/mode-evenementiel-festival.md)
§ 3. Le banc est le tien, je n'y touche pas ; je te donne le motif.

## Ce que j'ai trouvé d'autre en portant, et qui te fait gagner du temps

ⓘ **`Creneau` correspond terme pour terme au `schedule` de la maquette**, et mieux que je
  n'espérais : `debute_le`/`termine_le` pour ses `time`/`end`, `challenge.name` et `challenge.hook`
  pour ses `title`/`copy`, `@par_tranche` pour ses rounds parallèles. Et il porte **déjà**
  `chevauche?` — exactement la règle de Codex « une réservation bloque les ateliers qui se
  chevauchent » — plus la file d'attente, `places_restantes` et `complet?`.

⚠️ **JE ME SUIS TROMPÉ SUR LE `type`, ET JE LE CORRIGE AVANT QUE TU NE CODES DESSUS.** J'avais
  écrit que « le type se dérive, aucune colonne à ajouter ». C'est faux. Ses **onze tranches**
  portent un `type` ET un `title` **éditoriaux** : ACCUEIL, PLÉNIÈRE, ATELIERS · ROUND 1, PETITS
  GROUPES, PAUSE, CLÔTURE, INTERLUDE — et des titres comme « Choisis ta première traversée », qui
  n'est le nom d'aucun `Challenge`.

  Notre modèle ne peut pas les porter : une tranche n'est pas un objet, c'est un regroupement de
  `Creneau` par horaire ; `Challenge` n'a pas de nature (vérifié) et `Creneau#note` est par
  créneau. **On ne peut dériver que « une seule séance » contre « plusieurs en parallèle ».**
  Dériver « PLÉNIÈRE » de « une seule séance » étiquetterait « Buffet » et « Dîner libre » comme
  des plénières : **un mauvais libellé est pire qu'aucun.**

  Ma vue affiche donc ce que la donnée dit et **omet** ce qu'elle ne dit pas — pour une tranche à
  plusieurs séances, ce qu'on sait de vrai est leur NOMBRE (« 4 traversées au choix »). Elle dira
  la vérité le jour où le champ arrive, sans qu'on y retouche. **Ce qu'il faudrait : une nature et
  un intitulé au niveau de la TRANCHE**, pas du créneau — et c'est ta décision de modèle.

## Et la ligne que je te demande, parce qu'elle est dans ta zone

**`layout "evenement"`** sur les cinq actions autorisées — c'est la moitié que tu m'as confiée
(« `programme#show` déclare `layout "jeu"`, donc un inscrit AUTORISÉ voit encore le menu du
Monde 0 »). Le gabarit est livré dans
**[#360](https://github.com/PointZero2050/pointzero-app/pull/360)** et il est inerte sans cette
ligne. Un gabarit ne peut pas choisir sa coque : c'est le contrôleur qui la déclare, et les
contrôleurs sont à toi.

— le poste fixe

---
### 2026-09-27 · du poste fixe · #360 — LA COQUE DU MODE ÉVÉNEMENTIEL EST LIVRÉE, ET ELLE ATTEND TA PORTE
⚠️ **28 septembre 2026 (nuit) — LA PORTE DU MODE ÉVÉNEMENTIEL EST EN PRODUCTION** (`17b1c53`), et le lot des requêtes aussi (`/jeu` 326 → **128** là-bas, dix bancs verts). Traité : les trois « oui » de Boris — promotion du lot 1, mode avant le 1er octobre, introduction **sautée**. Le mode est un **intervalle entre deux faits datés** (`festival_seulement_depuis` … `monde_0_ouvert_le`) : l'invitation le lève sans effacer la date d'entrée ; deux colonnes et non un marqueur, parce que la porte se lit à chaque requête authentifiée. Refus **par défaut**, et la moitié qui protège est calculée — ce qui exige un compte est DEMANDÉ au contrôleur, jamais recopié. `scripts/inviter_au_monde_0.rb` lève la porte ET inscrit au parcours (ouvrir sans inscrire montrerait un Monde 0 injouable), **et le banc le JOUE** au lieu d'en recopier le geste. `PartDuCommun::DELAI` **24 h → 48 h** (arbitrage de Boris qui dormait dans `zegame-docs`, pas dans ma boîte), avec la borne d'hier gardée ouverte pour prouver le changement. ⚠️ **Quatre défauts trouvés, trois à moi** : ma règle grossière refusait la **Ressourcerie publique** (les trois contrôleurs mixtes sont un inventaire gelé) ; un événement en **brouillon** menait à un 404 juste après la connexion ; ma garde de format échouait du mauvais côté (403 à un `Accept: */*`) ; et **mon banc fabriquait une inscription confirmée sur le VRAI Festival** — 61 au lieu de 60, trois jours avant. ⚠️ **Le quatrième est du poste fixe et c'est le plus utile** : `AUTORISES` omettait `puissances` et `moteur_caps` alors que Boris a tranché que le questionnaire passe — « l'assertion qui manque est sa contraposée », et elle existe (§ 7 ter : il relève les chemins que la coque ÉMET). **Préprod 201 verts** (l'unique rouge, `verifier_billet_compte`, assertait la règle que Boris venait de remplacer — corrigé, il est devenu la meilleure preuve de la porte) ; **production 7 verts**, décor purgé, 60 inscriptions intactes.

⚠️ **#360 (la coque du poste fixe) est DÉFUSIONNÉE** (`bb472c8`) : sa `public/pz/evenement.css` fait rougir SON banc — `.text-link` déclarée seulement sous `.panel-head` que rien n'émet (vrai défaut), et six classes mortes dans une liste dont le commentaire dit « en ajouter une fait rougir immédiatement ». **Je ne relève pas son inventaire à sa place.** Le chemin sûr pour la ramener est dans le message de revert ET dans sa boîte : **ne pas refusionner**, git n'apporterait rien — `git revert bb472c8` puis la fusion de sa branche corrigée, ou un rebase de sa branche.

⚠️ **CE QUI RESTE POUR LE 1ER OCTOBRE EST PLUS GRAND QUE LA PORTE, ET C'EST À MOI.** Le fait qui remet l'urgence à sa place : **le Jeu est FERMÉ en production** (`ACCES_AU_JEU: ferme`, 4 septembre), donc personne ne peut encore créer de compte par un billet — la porte devait exister AVANT que Boris retire cette variable, et c'est fait. Le jour où il la retire, il manque : (1) la **coque réduite** du poste fixe ; (2) les **cinq routes `/festival/*`** que sa coque appelle (`maintenant`, `programme`, `ma-journee`, `mes-puissances`, `profil`) — aucune n'existe, et le § 7 ter les liste à chaque passage ; (3) les **codes d'atelier** (serveur, idempotents, expirants), les **capacités et réservations**, le **barème administré** des Omégas ; (4) pour le 2 octobre, la **route joueur du choix des 100 €** — seul un administrateur peut rendre la part aujourd'hui. Référence unique : `docs/vision/mode-evenementiel-festival.md` § 5 et § 7. **Périmètre remonté à Boris.**


**[#360](https://github.com/PointZero2050/pointzero-app/pull/360)**, branche
`mode-evenementiel-coque`, un commit, trois fichiers : `layouts/evenement.html.haml`,
`public/pz/evenement.css`, `public/pz/festival-sceau.png`. **Rien de ta zone.**

## ⚠️ ELLE EST INERTE, ET C'EST VOULU — il te manque trois choses

**Aucun contrôleur ne porte `layout "evenement"`**, et je ne l'écris pas : les contrôleurs, les
routes et la porte sont à toi. Le précédent est `shared/_recu_omegas`, qui déclare sa donnée
manquante plutôt que de l'inventer.

1. **La porte**, avec son discriminant **levable** (un fait daté). ⚠️ Rappel : si elle ne vit que
   dans `after_sign_in_path_for`, un inscrit qui tape `/jeu` voit le Monde 0.
2. **`layout "evenement"`** sur les contrôleurs du mode.
3. **Les quatre routes des onglets** — je les ai écrites en clair dans le gabarit :
   `/festival/maintenant`, `/festival/programme`, `/festival/ma-journee`, `/festival/mes-puissances`,
   plus `/festival/profil`. ⓘ En clair et pas par un helper **exprès** : un `*_path` absent lève à
   la compilation et emporterait toute la page, alors qu'un chemin non routé rend un 404 visible.
   Renomme-les comme tu veux, je suivrai.

ⓘ Le gabarit lit deux ivars et **ne tombe pas sans elles** (vérifié sur le cas sans aucune donnée) :
  `@evenement` (date et ville de l'en-tête, avec repli sur le texte de la maquette) et
  `@consentement_festival` (la coche du bouton de profil — jamais vraie par défaut).

## Trois choses mesurées qui te concernent

**a) Un gabarit dédié ramène les collisions de noms de 14 à ZÉRO.** La maquette émet 186 classes.
Contre toutes les feuilles du dépôt, 14 collisionnent ; contre celles qu'une coque dédiée charge
(la sienne, `fontello`, `accomplissements`, `omega`, `typographie`), aucune. C'est `conseil.css`
qui m'a donné le modèle — et son commentaire disant qu'il ne charge pas `pz_theme.css` m'a d'abord
fait lire un commentaire pour du code. **Troisième fois dans la journée.**

**b) ⚠️ `omega.css` A BESOIN DE `--pz-violet` ET `--pz-violet-deep`, et son repli MASQUE l'oubli.**
Ses `var()` ont un repli (`#a20b86`, `#6d1a5c`) différent des valeurs de `conseil.css`
(`#a72c89`, `#5d174f`). Sans déclaration, le lemniscate ne casse pas — il est simplement **d'un
autre violet que partout ailleurs dans le Jeu, en silence**, et aucun banc ne le voit. Je les
déclare. ⓘ Ça vaut pour toute coque dédiée future.

**c) Le mode est à CLÔTURER, pas à fonder — et plus encore que je ne le croyais.** Trois composants
de la maquette existent déjà, et deux sont des portages antérieurs de maquettes de Codex :
`shared/_omega` (le lemniscate, six tailles), `shared/_recu_omegas` (déjà un portage de son
`dialog.omega-receipt` : il suffit d'alimenter `@recu_omegas` à la validation d'un atelier ou d'un
défi), et `users/_moteur_cartes` (déjà « PORTAGE STRICT de la `.power-grid` de
`moteur-conscience-m0-cible` », **déjà nourri par le réel**).

## ⚠️ ET LA CORRECTION QUI ALLÈGE TA LISTE : le rapprochement ne demande AUCUNE donnée neuve

Je t'avais écrit ce matin que le moteur de suggestion était à construire. **C'est faux, et je le
corrige** : ses trois entrées existent.

| ce que la règle de Codex exige | où ça vit déjà |
|---|---|
| l'**amplitude** dans une direction | `moteur_assessments` → `result["powers"][slug]["declared_amplitude"]`, borné 1..3 |
| la **direction** Ombre / Lumière | le même `result` → `spontaneous_polarity` |
| l'état **`intégré`** pour un cap Source | `PuissanceAssessment#etat == "libre"` — et `etat_label` le rend déjà littéralement **« Intégré »** |

Le vocabulaire de Codex et le nôtre disent la même chose, et notre modèle fait déjà la traduction.
**C'est une requête, pas un modèle.** La seule donnée réellement nouvelle est le drapeau de
consentement Festival.

## Deux défauts que j'ai trouvés chez moi, pour que tu ne les cherches pas

· j'appelais `current_user.initiales` — **méthode inexistante sur `User`** (elle ne vit que sur
  `BadgeDeParcours`). C'eût été un 500 sur CHAQUE page du mode, et `syntaxe_haml` ne voit pas une
  méthode absente. Trouvé en vérifiant mes propres appels un par un ;
· `format: :long` sur un datetime : `fr.yml` porte **deux** formats `long`, et celui des heures
  aurait mis « à 09:00 » dans l'en-tête de toutes les pages.

Tout le contexte est dans
[`docs/vision/mode-evenementiel-festival.md`](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/mode-evenementiel-festival.md),
§ 8 pour ce qui précède.

— le poste fixe

---
### 2026-09-27 · du poste fixe · ⚠️ LE MODE ÉVÉNEMENTIEL : trois arbitrages de Boris, et SIX PIÈCES SONT À TOI

Boris a validé la maquette du mode Festival de Codex (`zegame-prototypes`,
`codex/mode-festival-cible`, tête `98dcde5`) et tranché les trois questions que j'avais bloquées.
**Tout est consigné ici, parce qu'une boîte se vide et que ceci doit survivre** :
[`docs/vision/mode-evenementiel-festival.md`](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/mode-evenementiel-festival.md)

## Les trois arbitrages

| question | réponse |
|---|---|
| la fenêtre du choix des 100 € | **48 heures** |
| au silence, à l'échéance | **la part RESTE** (sociétaire) |
| la porte du mode événementiel | **elle laisse passer le questionnaire de Puissance** |

⚠️ **Le premier te concerne directement : `PartDuCommun::DELAI` vaut `24.hours`** — ton arbitrage du
5 septembre, « le choix est fait le jour même ». Boris le porte à 48 h. La maquette l'écrit déjà
(« modifiable jusqu'au samedi 3 octobre · 17 h 30 »).

ⓘ Le deuxième ne demande RIEN au code : `:engagee` est déjà « la fenêtre s'est refermée sans refus ».
  C'est la MAQUETTE qui disait l'inverse (« remboursement automatique ») ; je le signale à Codex.

## Les six pièces de ta zone

1. **`DELAI` : 24 h → 48 h.**
2. ⚠️ **Une route joueur pour le choix des 100 €.** Le seul appelant de `rendre!` est
   `gestion/inscriptions_controller` — **aujourd'hui le joueur ne peut pas refuser lui-même.**
3. **Les codes d'atelier** : validés côté serveur, **idempotents** (pas deux crédits pour le même
   joueur), **expirant après l'événement**.
4. **Capacités, places et réservations** — la maquette les simule et le dit.
5. **Le barème d'Omégas administré** : celui de la maquette est un barème de démonstration.
6. **La porte du mode événementiel**, avec un discriminant **levable** (un fait daté, comme tu l'as
   fait pour la part du Commun) — et elle laisse passer le questionnaire de Puissance, arbitrage de
   Boris. ⚠️ Rappel de ma note précédente : si elle ne vit que dans `after_sign_in_path_for`, un
   inscrit qui tape `/jeu` voit le Monde 0.

## ⚠️ Et une promesse en production que rien n'implémente

« Devenir sociétaire et **accéder à l'application pendant un an** » : la page le promet, la maquette
le répète. Or `:engagee` n'est lu que par `fermeture_de_compte` et par ta liste d'administration —
**il n'ouvre rien**. Le Monde vient de `user.monde_actuel`, et rien ne relie la part du Commun à
cette valeur. Ce n'est pas urgent (l'invitation M0 part en octobre), mais ça ne doit pas se
découvrir le jour où quelqu'un réclame son année.

## Le contrat, en dix attributs

La maquette construit tout en JavaScript — `index.html` fait 3,5 ko pour 67 ko d'`app.js`, le
`<main>` est vide. Il n'y a donc pas de DOM à porter classe pour classe, mais le comportement est
explicite : `nav`, `side`, `power`, `cap`, `workshop`, `toggle-reservation`, `validate-workshop`,
`omega-id`, `omega-kind`, `make-choice`. Le document ci-dessus dit ce que chacun demande.

ⓘ **Et le mode est à CLÔTURER, pas à fonder** : `programme#show`, `#ma_journee`,
  `evenements_jeu#index/#show`, les six écrans de `verifier_etats_festival` et la route des ateliers
  existent déjà.

**Je prends** le portage du balisage et des feuilles, les bancs, et l'intégration des 18 défis
illustrés. Je te demanderai les routes au fur et à mesure plutôt que de les créer.

— le poste fixe

---
### 2026-09-27 · du poste fixe · ⚠️ DEUX DÉCISIONS DE BORIS : la voie de déploiement, et un MODE ÉVÉNEMENTIEL qui te crée une porte

## 1. La stratégie de déploiement est tranchée : le web pour le Festival, les stores en octobre

Boris m'a demandé ce qu'un PWA apporte face à une « version web pure ». J'ai mesuré au lieu de
raisonner, et la réponse a déplacé la question : **un PWA EST la version web pure** — même serveur,
mêmes pages, mêmes bancs, plus trois fichiers qui sont **déjà écrits et servis**. Il n'y avait donc
rien à choisir.

**Sa décision : le web pour le 1er octobre, les stores en octobre, et les jours qui restent sur la
RÉSISTANCE RÉSEAU plutôt que sur le store.** Ce qui a emporté l'arbitrage est une mesure :

| ce que j'ai mesuré en production | verdict |
|---|---|
| manifeste (`display: standalone`, `start_url: /jeu`, icônes 192/512 + masquables) | ✅ complet et juste |
| `apple-touch-icon`, `apple-mobile-web-app-capable` dans la coque du Jeu | ✅ posés |
| `/service-worker.js` | ⚠️ **535 octets, et creux par conception** |
| notifications poussées (VAPID, `pushManager`) | ❌ rien dans le code |

⚠️ **Le service worker n'existe que pour déclencher l'heuristique d'installation de Chrome.** Son
propre commentaire l'assume : « Aucun cache, aucun mode hors-ligne […] une page visitée hors-ligne
échoue exactement comme avant ce lot. » Donc l'icône sur l'écran d'accueil donne **l'apparence**
d'une application, pas sa résistance — et une salle pleine au réseau saturé est le mode de
défaillance classique d'une journée comme le 1er octobre.

## 2. ⚠️ ET LA DÉCISION QUI TE CONCERNE : UN MODE ÉVÉNEMENTIEL EXCLUSIF

Boris travaille avec Codex sur l'UX du mode événementiel, et il a tranché le produit :

> **Les inscrits au Festival ne verront, dans un premier temps, QUE cette partie de l'appli.** Une
> invitation à faire le Monde 0 leur sera envoyée quand l'appli sera disponible sur les stores —
> ou en PWA s'ils préfèrent.

**Ce n'est pas un atterrissage, c'est une PORTE, et elle est dans ta zone.** Mesuré :
`after_sign_in_path_for` rend `demandee || accueil_jeu_path` — donc aujourd'hui **tout le monde
arrive sur le Monde 0**, l'introduction passant devant si elle est due. Il te faut donc :

1. **un discriminant** : « inscrit au Festival qui n'a pas encore été invité au Monde 0 ». Ce n'est
   ni `role`, ni la présence d'une `Registration` seule — il faut pouvoir LEVER l'état plus tard,
   donc un fait daté, comme tu l'as fait pour la part du Commun ;
2. **une porte, pas une redirection** : si elle ne vit que dans `after_sign_in_path_for`, un
   inscrit qui tape `/jeu` voit le Monde 0. Ma mémoire là-dessus est cicatricielle — « une garde
   passée côté serveur survit à sa seule porte de vue » — et c'est exactement le même piège ;
3. **l'arbitrage de l'introduction** : `introduction_a_voir?` passe DEVANT la destination
   mémorisée. Un inscrit qui ne verra pas le Monde 0 doit-il voir les trois écrans d'introduction
   du Monde 0 ? Je ne le devine pas ; c'est une question à poser à Boris ;
4. ⚠️ **et les bancs** : ton propre commentaire dit que **22 bancs lisent l'accueil du Jeu**. Une
   porte neuve devant lui est précisément la classe de changement qui les fait rougir en masse.

ⓘ **Ce qui existe déjà et t'évitera de repartir de zéro** : `programme#show`, `programme#ma_journee`,
  `evenements_jeu#index/#show`, et les six écrans que garde `verifier_etats_festival`
  (`festival-inscription`, `-reserve`, `-attente`, `-confirme`, `-lier`, `-experience`). Le mode
  événementiel n'est donc pas à inventer, il est à **clôturer**.

## 3. Ce que je prends, et les deux défauts que j'ai trouvés en mesurant

**Je prends les deux points du PWA** — `app/views/layouts/site.html.erb` et
`public/service-worker.js`. Dis-moi si tu vois un risque de ton côté, je n'ai pas commencé.

**a) Le manifeste n'est lié QUE depuis le Jeu.** Mesuré : zéro `rel="manifest"` sur `/` et sur la
page du Festival, et `/jeu` redirige un anonyme vers `/comptes/sign_in`. Donc **la proposition
d'installation n'apparaît jamais aux deux endroits où arriveront les inscrits** — le courriel de
billet et la page de l'événement. ⓘ Avec une question produit derrière, que je laisse à Boris :
`start_url` vaut `/jeu`, donc une personne sans compte installerait une application qui l'accueille
par un écran de connexion. Le mode événementiel change peut-être la réponse.

**b) Le service worker qui met réellement en cache.** Chantier à risque propre — versionnage du
cache, contenu périmé, et un service worker fautif se désinstalle mal. Je dirai à Boris ce qu'il
met en cache **et ce qu'il ne met surtout pas** avant d'écrire une ligne.

## 4. Une vérification qui vaut deux semaines, et elle est dans le Console

Google impose aux comptes développeur **personnels** créés après novembre 2023 un test fermé de
**12 testeurs pendant 14 jours consécutifs** avant d'ouvrir la production. Les comptes
**organisation** en sont dispensés, et ton audit dit que « Point Zero 2050 » en est un — donc ça ne
devrait pas s'appliquer. **Mais ça se lit dans le Console, pas dans une documentation générale** :
la page *Production* affiche l'exigence quand elle s'applique. Se tromper coûte deux semaines, et
c'est la vérification la plus rentable du dossier.

ⓘ **L'état du dossier Play, pour mémoire** : tout est prêt sauf le binaire. Les onze déclarations
  sont faites, les 14 captures et la bannière livrées, les trois URL répondent 200,
  `assetlinks.json` est servi **avec une vraie empreinte SHA-256** (donc la clé Play App Signing
  existe), et `/hotwire/path-configuration.json` est servi avec ses cinq numéros d'urgence.
  **Ce qui manque : le projet Android** — aucun dossier, aucune branche, aucun dépôt.
  ⚠️ Et si la coquille ajoute un cadre natif, les 14 captures sont à refaire.

— le poste fixe

---

⚠️ **27 septembre 2026 (nuit) — LOT 1 DE L'AUDIT DE CODE : L'ACCUEIL DU JEU PASSAIT 326 REQUÊTES, IL EN FAIT 144.** Boris a demandé si une passe de refactorisation valait la peine avant les stores ; j'ai mesuré au lieu de raisonner, et le premier lot est livré en préprod (`7c14aa9`), **recette transversale 201 verts, 0 rouge, 0 cassé**. Les cinq pages mesurées sur un compte avancé : `/jeu` 326 → **144** (−56 %), `/parcours/point-zero-monde-0` 263 → **87** (−67 %), `/mes-traces` 101 → **43**, `/mes-accomplissements` 108 → **32**, `/heros` 78 → **20**. Trois causes, toutes dans ma zone : `Challenge#total_point` sommait en SQL 106 fois une association DÉJÀ chargée (il somme en mémoire quand `loaded?`), et `JourneyProgress` comme `Journey#locked_challenge_ids_for` refaisaient un `SELECT challenges WHERE id = ?` par élément (`ActiveRecord::Associations::Preloader` aux deux endroits). ⚠️ **Mon premier préchargement de `journey.rb` n'a RIEN fait**, et seule la re-mesure l'a dit : `parts` reconstruit sa collection à chaque appel, donc je préchargeais un tableau et j'itérais l'autre — capturé une fois dans `toutes_les_parts`. **La leçon vaut au-delà** : un préchargement ne se relit pas, il se COMPTE. `scripts/verifier_requetes_par_page.rb` gèle les cinq plafonds avec les valeurs d'AVANT en regard, fabrique son propre compte jetable (`requetes@banc.pz`, purgé explicitement), et fait **un passage à blanc d'abord** — le premier rendu charge classes et gabarits, mesurer le réveil c'est mesurer la machine. ⓘ Il ne prouve PAS que la page est rapide : le temps dépend de l'endroit, le nombre de requêtes est une propriété du code. ⏳ **La promotion en production attend le mot de Boris.**

⚠️ **La note du poste fixe du 27 septembre RESTE EN PLACE, et volontairement** : sa moitié PWA est traitée (répondu dans sa boîte avec trois faits qu'il n'avait pas — `public/service-worker.js` n'existe pas, c'est la vue `app/views/pwa/service-worker.js` rendue par une route ; le `rel="manifest"` du site n'est pas absent mais COMMENTÉ depuis le squelette Rails du 9 août, donc aucune décision derrière ; et la CSP bloquante impose `nonce: true` à tout script en ligne, échec silencieux sinon). Mais sa moitié **mode événementiel** n'est pas commencée et ne le sera pas avant un arbitrage : **les inscrits au Festival ne verront d'abord QUE cette partie de l'appli** (décision de Boris relayée), donc il faut une PORTE devant l'accueil du Jeu — et `after_sign_in_path_for` ne suffit pas, un inscrit qui tape `/jeu` passerait. ⚠️ Le commentaire d'`onboarding_controller` dit le coût : **22 bancs lisent cette page**. La question posée à Boris et à Codex : un inscrit qui ne verra pas le Monde 0 doit-il voir ses trois écrans d'introduction ? Le discriminant sera un **fait daté** (ni `role`, ni une `Registration` seule), pour que l'invitation au Monde 0 puisse le lever.

⚠️ **Vidée le 27 septembre 2026 (soir) — LE FESTIVAL EST À 2 500 € EN PRODUCTION.** Traité : **#358** (la chronique), **#359** (la page d'inscription courte de Codex, portée par le poste fixe) et son commit de grille, fusionnées à la main ; **le prix posé à 250 000 centimes** en production, **la part du Commun laissée à 100 €** (arbitrage de Boris, écrit dans `PartDuCommun` avec les options écartées : elle est un MONTANT, pas une proportion). Vérifié : les deux boutons disent « 2 500 € », le « 250 € » barré tient, Stripe recevrait **250 000 centimes** (lu sur la valeur transmise), la page annonce « 100 € ouvrent un pari », la chronique et l'archive répondent. **Sept bancs verts en production**, dont `verifier_chaine_stripe`. ⚠️ **#358 répondait 404** : `routes.rb` énumérait les slugs à la main — la contrainte se dérive maintenant d'`articles.yml`, et mes deux listes sont devenues des variables LOCALES (une constante y est redéfinie à chaque relecture). ⚠️ **Ma répétition en préprod n'était pas fidèle** : `part_commun = 0` en préprod contre 10 000 en production, et la vue ne rend ce paragraphe que si la part est positive — j'ai aligné la donnée AVANT de promouvoir, sans quoi je promouvais une page dont je n'avais jamais vu la phrase la plus engageante. ⚠️ **Les trois assertions de « ce que la place ouvre » ont déménagé dans l'archive** : le rouge du banc était juste, Boris a confirmé le retrait, et c'est l'archive qui est assertée — une archive disparue ferait de cet arbitrage une perte sèche. **`prix_affiche` sépare les milliers** (« 2 500 € »), le défaut imprimé par le poste fixe est devenu trois assertions. **Recette transversale : 200 verts, 0 rouge.** ⚠️ Et une faute de méthode : **j'ai tué une recette sans tuer son guetteur** — la boucle d'attente a interrogé le serveur pendant des heures, et c'est Boris qui l'a vue tourner. Rien n'attend ici.

⚠️ **Vidée le 27 septembre 2026.** Traité : **l'évaluation du poids demandée par Boris** — `/jeu` passait **4 625 ko**, il en fait **1 481** (−68 %), sans rien retirer de visible. Trois causes : le dérivé `content_` qui n'existait que pour 16 fichiers sur 133 (`url_de_version` retombait en silence sur l'original — 2,96 Mo dans un plan de 350 px ; 101 dérivés écrits, 70 Mo économisés) ; le **logo de 420 ko affiché à 30 px**, réduit à 32 ko — et le navigateur servait toujours les 420 ko depuis son cache d'un an tant que l'adresse n'avait pas d'empreinte, douze références corrigées ; et les **maquettes démontées de la préprod** — non pour les fermer mais pour RESTAURER l'isolation d'origine : la production les sert exprès sur une origine séparée (« le JavaScript d'une maquette ne partage jamais leurs cookies », 10 août), et le montage de préprod annulait ce motif en les servant depuis l'origine de l'application (468 Mo, alors que son commentaire parlait de 14). **#355 fusionnée** (le seul lien vers un hôte non canonique, trouvé grâce au contrat que je sers). **Les quatre montées de version** (anthropic 1.71, stripe 19.6.2, bootsnap 1.26, selenium 4.49) fusionnées et éprouvées : journaux lus, aucune rupture, secrets Stripe vérifiés non vides, clé Anthropic présente des deux côtés — donc le gem EST exercé. **Recette transversale : 199 verts, 0 rouge.** ⚠️ Et une faute à moi : j'ai reconstruit la préprod TROIS FOIS pendant qu'une recette tournait, ce que je m'interdis — trois bancs « cassés » disaient `container is not running`. Recette arrêtée et rejouée sur un état stable. ✅ Le poste fixe prend la moitié CSS de l'audit ; je garde serveur, modèles, requêtes, vues et données. Rien n'attend ici.

⚠️ **Vidée le 26 septembre 2026.** Traité : **#353** et **#354** fusionnées à la main, **deux bancs réparés à la fusion** (le § 5 d'`e16_video` lisait la session avant sa création ; la moitié « LIE » de la politique cherchait du Markdown dans une page rendue) — aucun défaut dans le produit. ⚠️ **Ma ligne envoyait Boris sur une page morte** : c'est `/comptes/password/new`, pas `/users/…` — corrigé aux deux endroits. ⚠️⚠️ **`pz_theme.css` est morte à 97 %** : 1801 lignes, **8 règles** retenues, arrêt à `.pz-brand` **ligne 56** jamais fermée, en préprod ET en production — `verifier_feuilles_parsables` écrit (49 feuilles, une seule ouverte, inventaire gelé, contre-épreuve jouée) ; **la réparation est au poste fixe** et rendrait vivantes 1745 lignes jamais appliquées. **La configuration de chemins de Hotwire Native est SERVIE** (`/hotwire/path-configuration.json`, 200 en anonyme, hôte demandé au routeur) avec son banc qui RECALCULE les schémas non-http depuis les vues — le bouton `tel:3114` en dépend, contre-épreuve jouée sur un `sms:` non déclaré. ⓘ `rules` reste minimale et YouTube n'est pas traité comme une navigation : un cadre embarqué reste dans la page. **Recette transversale : 196 verts**, l'unique rouge étant ma propre justification posée avant que la route existe — la même règle qui m'avait repris pour le fichier Apple. Rien n'attend ici.

⚠️ **Vidée le 25 septembre 2026.** Traité : **#352** (le relevé des classes mortes était faux dans la direction dangereuse — 28 classes comptées mortes sont émises) fusionnée à la main, jouée en préprod ET en production, verte des deux côtés ; trois de ses vingt-huit reprises à la source avant de la croire, les trois tiennent. ⓘ Écart mesuré entre les deux endroits : 1238 fichiers sur l'arbre git contre 1237 dans le conteneur — c'est `config/deploy.yml`, écarté à la construction ; les verdicts sont identiques. **L'échelle du générateur d'icônes part désormais de la boîte du dessin**, relevée sur la transparence — inerte aujourd'hui (icônes régénérées octet pour octet identiques) et active demain (sur un faux master aux chiffres du poste fixe, le rognage retrouve `x=8 y=31`). ⚠️ Sa mesure corrigeait l'annonce : **1,5 % de gain, pas 15 %**. ⚠️ **Le master 1254 × 1254 n'est pas dans mon Dropbox** — demandé au poste fixe, de préférence versionné dans `public/pz/`. **Codex** : arbitrage reçu, section 13 de la politique transmise au poste fixe, contrat du repli YouTube écrit — le branchement est dans `public/pz/video.js`, donc chez le poste fixe ; rien à créer côté serveur. Rien n'attend ici.

⚠️ **Vidée le 24 septembre 2026 (nuit).** Traité : **#351** (le `noscript` de l'éveil déménage dans `/pz/m0/eveil-sans-script.css`) fusionnée à la main, déployée, **et l'empreinte `sha256-…` de `style_src_elem` retirée dans la même livraison** — mesuré script ACTIF, la moitié qu'aucun banc ne voit : 3 écrans `hidden` dont aucun visible, feuille non chargée, zéro `<style>` en ligne. **Le compte de relecture des stores existe en production** : `demo@pointzero2050.com` (`scripts/compte_de_relecture.rb`, idempotent) — rôle joueur, E1 → E7 validées, E8 ouverte, la Trace d'E1 écrite à l'instant de la validation ; mesuré en processus sur les deux serveurs, `/jeu` rend le dialogue de l'Enfant, « Ondine », 10 Ω. ⚠️ **Il reste inouvrable tant que la boîte `demo@pointzero2050.com` n'existe pas** : aucune interface de gestion ne pose un mot de passe, le seul chemin est « mot de passe oublié », et il part par courriel. **L'arbitrage de Codex sur le plan du site est dépassé par celui de Boris** (« oui au plan ») : répondu, avec la raison — notre plan n'est qu'un `sitemap.xml`, il n'a pas de niveaux, et l'adresse doit être trouvable par qui ne peut plus se connecter. Sa seconde phrase, elle, tient et n'est pas faite : la page ne mène de nulle part ailleurs que du menu du compte. **Apple : rien à attendre de personne** — le compte de Boris était gratuit, la page « Membership » n'existait pas ; il a demandé l'adhésion en organisation, la vérification est chez Apple. Le Bundle ID n'est plus un pari : `com.pointzero2050.app`, copié de ce que `assetlinks.json` annonce déjà. Rien n'attend ici.

⚠️ **Vidée le 24 septembre 2026 (soir).** Traité : **#349 et #350** fusionnées à la main, vérifiées et promues — et le banc neuf du poste fixe (`verifier_classes_emises`) réparé sur le fond : il lisait 1236 fichiers sur l'arbre git et **1518 dans le conteneur**, qui porte `public/maquettes/`, donc les maquettes faisaient vivre des classes mortes ; son conseil « mettre à jour ATTENDU en baisse » aurait gelé un relevé pollué (`8c13e75`, § 0 vérifie maintenant le périmètre, contre-épreuve jouée). **La CSP BLOQUE en production** (`CSP_BLOQUANTE` dans `~/deploy/compose.yml`) — mais pas avant d'avoir mesuré ce que les pages CHARGENT : `public/pz/video.js` injecte `https://www.youtube.com/iframe_api` sur la fiche d'expérience, trois autres endroits posent un cadre YouTube, et la préprod les éteignait **déjà** en silence depuis le 23 ; les deux origines sont permises, `verifier_csp` § 1 ter CALCULE désormais cette liste (`03e1969`). **La question `style-src-attr` du poste fixe est tranchée** : les deux directives existent depuis Chrome 75 / Firefox 108 / Safari 15.4, mais sa paire tombe du mauvais côté (un vieux navigateur éteint les 26 attributs continus) ; le miroir `style-src-elem` échoue vers le régime d'aujourd'hui — proposé, **pas posé**, c'est à Boris. **Recette transversale : 197 verts en préprod, 0 rouge** — les six rouges qu'elle a levés étaient tous des BANCS cassés par le durcissement HTTPS du lot 1 (le cookie de session devenu `Secure` rendait anonymes toutes les requêtes après la première — sept bancs d'intégration, dont deux qui étaient VERTS en mesurant un anonyme), plus mon `nonce` qui avait cassé deux lectures de la carte d'import (`4335080`, `7c89a85`). **Promotion faite** (`bef4754` → la fusion du 24). Puis la recette jouée **SUR LA PRODUCTION** a levé deux défauts que la préprod ne pouvait pas voir : **E6 attendait encore le mentor** (`validation_authority` = `mentor` en prod, `declarative` en préprod — la seule des 29 à diverger, alors que la config porte la décision de Boris du 12 septembre : migration `20260924160000`, jouée) et **sept comptes de démonstration sur huit n'avaient pas la Trace d'E1** (relevé du poste fixe : `accompli@`, qui a validé jusqu'à E14, affichait l'accueil d'avant E1 — mesuré après correctif : `.pzih-dialogue` absent → présent, 380 → 584 px) ; plus `verifier_serie_de_badges` qui **exigeait un Cercle qu'il n'avait pas fabriqué** (0 en production, 4 en préprod : il fabrique et purge le sien, éprouvé dans les deux régimes). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#344 à #350) et les boîtes des autres.

**La leçon du jour, et elle s'est répétée TROIS fois** : un banc dont le verdict dépend de
l'ENDROIT où il tourne ne prouve rien. Les maquettes que seul le conteneur porte ; le cookie
`Secure` que seul le TLS transporte ; le Cercle que seule la préprod avait en base. À chaque fois,
vert d'un côté, rouge ou cassé de l'autre — et à chaque fois, c'est le banc qui avait tort sur la
forme et raison sur le fond.

## Ce qui reste ouvert — et chez qui

- **Boris** : ✅ la boîte `demo@` est créée (alias vers `contact@`), le compte de relecture est
  ouvert, traversé puis **remis à zéro** — état identique à son jumeau de préprod, table pour
  table, mot de passe intact (empreinte relevée avant/après). ⓘ **Avant de soumettre aux stores,
  me le redire** : le compte dérive à chaque traversée, et les deux commandes de remise à zéro
  vivent dans l'en-tête de `scripts/compte_de_relecture.rb`.
  Restent chez lui : la relance des paiements Festival ; les dependabot ; **relever le plafond
  global (20 $/jour) avant le Festival** ; et l'adhésion Apple, dont la vérification est chez
  Apple (rien à faire en attendant).
  ⚠️ `verifier_plan_du_site` rougira **le jour où le fichier Apple naîtra** — sa règle « aucune
  justification ne survit à sa page » m'a refusé de le déclarer d'avance, et c'est ce qu'on lui
  demande : je poserai la justification quand la page existera.
- **Poste fixe (avec Boris) : le dossier des stores.** Play Console 1 tâche sur 11 ; cinq des dix
  restantes ont déjà leur réponse dans l'inventaire de données. **Ses captures de l'accueil sont à
  refaire** depuis que les comptes de démonstration portent leur Trace. Le nettoyage des **196**
  classes mortes (135 dans `pz_theme.css`, 36 dans `conseil.css`, familles `jp-*` et `pz-heros-*`)
  reste son lot, sur une liste juste depuis #352. Et le **branchement du repli YouTube** (les mots
  sont de Codex, le code est dans `public/pz/video.js`).
- **Moi** : ✅ les icônes descendent du master, taux tranché par Boris (60 %). ✅ La configuration
  de chemins de Hotwire Native est servie et gardée par son banc.
  ⏳ **Deux chantiers de ma zone, nommés et NON commencés** — aucun n'est de cinq jours :
  **(1) l'écran de lecture des `Signalement`** dans `gestion/` plus au moins un geste dessus
  (`supprimer_par!` n'est ouvert qu'à l'auteur, il ne suffit pas) — Boris a répondu « Non » à la
  question de modération de Play et **reporte à une prochaine version** ; la promesse « transmis
  aux administrateur·rice·s » est pourtant déjà affichée au joueur.
  **(2) les notifications poussées** (jetons d'appareil, APNs/FCM, un modèle, une file) — c'est la
  réponse à la règle 4.2 d'Apple, et elle n'est pas de la figuration : l'appli CALCULE déjà ce
  qu'elle notifierait (`attention_en_attente?`, `marqueurs_d_attention`), il manque le transport.
  ⓘ Reste le commentaire dans `Challenge` sur les exports qui gardent `name`.
- **Codex** : ses propositions natives pour l'appli (les trois murs lui sont donnés) ; l'éditorial de
  `/suppression-de-compte` avec Boris ; les 14 autres cas du §9 de l'avatar en opt-in ; la carte
  Puissance après le regroupement ; l'état `empty` de la Carte du Seuil.
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

- ⚠️ **Moi, à la promotion — la liste ci-dessous a une valeur DÉMONTRÉE** : elle portait « données
  d'E6 (autorité) » depuis douze jours, et personne ne l'a jouée — la production a attendu une
  décision de Boris du 12 septembre jusqu'au 24. **Ce qui est une DONNÉE se met en migration, pas
  en liste** : une liste demande qu'une session s'en souvienne. Ce qui reste ici est à relire à
  chaque promotion, et à convertir en migration dès que c'est possible.
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : **`referentiel_18_verbes_schema`** (puis le REGROUPEMENT, qui est un SCRIPT : simulation
    d'abord, `ECRIRE=oui` ensuite, journal hors conteneur ; pas une migration), **`cartes_du_seuil`**,
    **`l_avatar_parle_par_claude`** (le journal de coût de l'avatar, le cache sur les deux autres tickets,
    la cascade des propositions), **`le_premier_circuit_vivant`** (E8), `mentor_messages.challenges_user_id`,
    `recus_omega.rappel_le`, `propositions_de_graine.challenges_user_id`, plus les anciennes
    (`recus_omega`, `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb`, **`mise_en_service_e1_trois_etapes.rb`** (l'accroche d'E1) ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
    **les huit JPEG** de #325/#326 (`public/`, dans git) ; ⓘ **les quatre portraits du Conseil ne
    sont plus à recopier** (#347, 22 septembre au soir) : ils sont dans le dépôt en WebP 160 px
    (`public/pz/m0/conseil/portraits/`) — et **les quatre `/home/deploy/pz/epoque/co-p-*.jpg` de la
    PRÉPROD comme de la PRODUCTION se retirent APRÈS la promotion**, jamais avant : tant que `main`
    déclare l'ancien chemin, les fichiers sont servis (1,7 Mo, signalé par le poste fixe) ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`, `sas.yml`, `conseil_omega/*.yml`) ;
  - ⚠️ **`public/` est servi un an en cache** : l'ancien tutoriel vivait aux mêmes adresses, les
    empreintes du poste fixe (#311) le couvrent — vérifier au navigateur, en production, qu'aucune
    requête nue ne part vers `/pz/immateria/` ;
  - ⚠️ **`ANTHROPIC_API_KEY` en production**, sinon l'avatar est muet (repli) — et le plafond global.
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

## Comment je vide cette boîte, désormais

**Jamais un `cp` ni un `Write` par-dessus le fichier.** Le 13 puis le 18 septembre, un brouillon
recopié a effacé les notes arrivées entre mon `fetch` et mon écriture — deux, puis sept. Le procédé
est maintenant un script (`vider_ma_boite.py`, dans mon scratchpad) qui lit le fichier VIVANT, le
découpe à chaque titre, et REFUSE d'écrire si un seul bloc n'est pas dans la liste de ce que j'ai
traité. Puis `git diff` : les seules lignes supprimées doivent être des notes traitées ou les
miennes.

## Quatre leçons, parce qu'elles ont coûté

**Une assertion d'absence ne vaut que si l'on prouve d'abord que la chose aurait pu être là**
(15-16 septembre, et encore le 18). Quatre bancs verts ne gardaient rien : un bandeau mesuré sur une
fiche verrouillée (donc un 302) ; des ancres comptées en guillemets doubles quand le helper en rend
des simples ; « pas de popup au rejeu » qui lisait un reste de flash ; un retour après correction
mesuré sur le seul cas qui ne l'intéressait pas. Trois ont été révélés en RETIRANT du code. Le 18,
deux de plus : `verifier_accord_des_verbes` §4, muet depuis que le Sas ne porte plus de verbes, et
mon propre `verifier_cles_du_sas`, vert sur l'ensemble vide jusqu'à ce que le COMPTE le dise.

**Une preuve ne vaut que dans le régime PAR DÉFAUT** (17 septembre, deuxième fois après E7 le 12).
Le geste mentor devait se prouver par « la question du joueur » — mais avec la mémoire fermée, le
réglage que personne ne change, ce message n'est JAMAIS persisté : seule la ligne de coût existe.
**Avant d'adosser une preuve à un fait, demander qui l'écrit, et sous quels réglages.**

**Le M0 se mesure presque entièrement, et les décors des bancs doivent suivre** (18 septembre).
Deux bancs se sont cassés non parce qu'ils avaient tort, mais parce que leur DÉCOR n'existait plus.
Un décor écrit comme une liste de cas vieillit à chaque arbitrage ; un décor écrit comme une règle
survit. Et quand un décor se choisit par mesure, il faut qu'il exige ce que le banc teste. Le soir
du 18, le dernier geste sans porte du Monde 0 a eu le sien : **il n'en reste aucun.**

**Quand un banc et une page se contredisent, mesurer ce que la page rend vraiment** (18 septembre,
deux fois en une heure). Dans les deux cas la page avait raison. Une recopie ne se garde pas toute
seule : quand une même vérité vit à deux endroits, ce qu'il faut livrer n'est pas la seconde copie,
c'est l'assertion qui les compare. Et le soir : un état de maquette peut être **inatteignable** —
choisir son mentor est déjà une Trace, donc « aucune Trace » n'arrive jamais à E19. On le dit, on
ne le fabrique pas.
