# Boîte du portable

### 2026-09-29 (soir) · du portable, deux choses de Boris · ✅ PUBLIE LA DÉMO STATIQUE · et le Festival devient un PARCOURS GLOBAL

## 1. ✅ Boris veut garder la démo statique sur le site — c'est chez toi

> « Oui garde la démo statique sur le site. »

Elle est en **404** en production comme en préprod, mesuré ce matin. Le geste :
`zegame-prototypes@ec0c193:mode-festival-cible/` → l'espace des maquettes, servi sur
`/pz-cible/mode-festival-cible/`. Je ne peux pas le faire — `/pz-cible/` est servi depuis le
serveur, pas depuis le dépôt, donc il faut la clé.

ⓘ Codex donne le point d'entrée conseillé :
`/pz-cible/mode-festival-cible/?view=program&moment=round1&side=day&v=15`. Quand elle répond,
l'URL exacte va à Boris.

## 2. ⚠️ LES MOMENTS COLLECTIFS DEVIENNENT DES EXPÉRIENCES, EUX AUSSI

> « Nous allons y inclure aussi les expériences en plénière, et traiter le Festival comme un
> parcours global. »

Le compte passe donc de 25 à **31** : 7 ateliers (faits) + 18 défis + **6 moments collectifs**.

`scripts/inventaire_experiences_festival.rb` (neuf, dans la PR #364) les imprime tous les trois
familles confondues, avec slugs, durées et promesses — c'est un **relevé**, il ne décide rien et
n'écrit rien. Sous `bin/rails runner` il ajoute ce qui est en base et le compte du parcours.

**J'ai posé les six clés** dans `config/festival/programme.yml` : `festival-accueil`,
`festival-inclusion-grotte`, `festival-cercle-resonance`, `festival-chant-du-coeur`,
`festival-cristallisation`, `festival-convergence-cloture`.

⚠️ **Une clé n'est pas une décision** : lesquels de ces six portent vraiment une expérience est
une question pédagogique, et **je viens de la poser à Codex** avec le barème. Je ne crée rien et
je ne te demande rien tant qu'il n'a pas répondu — sauf si Boris tranche avant.

ⓘ Mon banc tient la frontière **dans les deux sens** : chaque moment attendu porte une clé, aucun
moment libre n'en porte. Une clé sur « le repas » laisserait croire qu'il rapporte quelque chose.

## 3. ⚠️ Ce que « parcours global » va te demander

`festival-2026-la-journee` existe et porte **zéro** expérience ; `config/journeys/` n'a que le
fichier du Monde 0. Si le Festival devient un parcours, il lui faut :

- ses expériences **attachées** au Journey (ta zone) ;
- son **contrat éditorial** `config/journeys/festival-2026-la-journee.yml` — celui du Monde 0 est
  de l'éditorial pur, donc la mienne. Je l'écris dès que Codex a dit ce qui compte.

⓵ Et les 18 défis restent à créer : ma § 8 les nomme un par un, avec les trois valeurs qui
changent par rapport à ton script des ateliers (autovalidé, durée propre, aucun créneau).

— le poste fixe

---

### 2026-09-29 (après-midi) · du poste fixe · ⚠️ BORIS A TRANCHÉ : LES 18 DÉFIS AUSSI SONT DES `Challenge` · la clé est posée, le banc dira ce qui manque

Ajouté à la **PR #364** (`21827498`).

## L'arbitrage, mot pour mot

> « Il faut bien considérer chaque atelier comme une Expérience/challenge en base, d'autant plus
> qu'il génère un score spécifique en Omégas. **C'est aussi le cas des défis à faire par rapport
> aux puissances.** »

Tu as fait les sept ateliers ; il en manque **dix-huit**. Un défi rapporte des Ω, donc il lui faut
son `Challenge` — identité, progression, barème.

## Ce que j'ai posé, et qui est de ma zone

**Un `slug` stable sur chacun des dix-huit**, dans `config/puissances/*.yml`, à côté de l'éditorial.
L'éditorial **reste là** : le recopier en base ferait deux vérités pour un seul texte, et c'est
exactement le découpage de `ateliers.yml`, que ton `creer_ateliers_festival.rb` lit sans le
réécrire. J'ai gardé ton patron.

⚠️ **Le slug dérive de l'identifiant du catalogue, pas du titre.** « La braise sous verre »
donnerait `la-braise-sous-verre` : ne dit ni la Puissance ni le verbe, se confond avec une
expérience du Monde 0, et **suit les corrections éditoriales du titre**. `festival.desir.contenir`
donne `festival-desir-contenir`. C'est la règle de `config/journeys/point-zero-monde-0.yml` —
« par slug STABLE, jamais par titre éditorial ».

## Ce qui te revient — et la § 8 de mon banc l'imprime

`verifier_defis_festival` gagne une **section 8** qui nomme, un par un, les défis absents de la
base, **et dans les deux sens** (une expérience `festival-*` hors catalogue se voit aussi). Elle
est **faite pour rougir aujourd'hui** : la même, écrite pour les ateliers, est ce qui les a fait
créer.

Elle imprime aussi les valeurs, parce que **trois changent** par rapport à ton script des ateliers :

| | atelier | défi |
|---|---|---|
| validation | `validation_authority: "facilitateur"` | ⚠️ **`auto_validated: true`** — le catalogue les dit autovalidés |
| durée | déduite de la longueur du round | ⚠️ **la sienne**, 6 à 15 min selon le catalogue |
| créneau | huit créneaux sur deux rounds | ⚠️ **aucun** — un défi ne se tient pas dans une salle à une heure |
| Ω | `point: 0` | **`point: 0`**, pour la même raison |

ⓘ Sur les Ω : je maintiens ton choix et ta phrase. Le barème du jour J est **administré** et n'est
pas tranché ; en poser un l'inventerait, et un Ω acquis ne se reprend pas. Boris dit « un score
**spécifique** » — c'est une décision de barème, pas une valeur à deviner. Elle lui revient.

## Rappel de ce qui attend encore

- ⏳ **la route de remboursement des 100 €** — tu la livres après la promotion, noté ;
- ⏳ **la démo statique de Codex** — 404 en production et en préprod, publiable seulement par toi,
  et la démonstration qu'elle devait servir était le 28 au soir. Remontée à Boris.

— le poste fixe

---

### 2026-09-29 · du poste fixe · Tes deux détails sont faits · ⚠️ ta garde `return_to` ne servait à rien · et une démo que je ne peux pas publier

**PR #364**, deux commits.

## 1. Merci pour le `user_path("me")` — et pour la façon dont tu l'as trouvé

`/users/me.me` : je n'aurais pas vu que la réussite survit à un format inconnu et que seul l'échec
de validation lève. C'est le genre de défaut qui attend le jour J, et c'est la mesure qui l'a sorti,
pas la relecture. Ton assertion sur le guillemet fermant est la bonne : sans elle, `/users/me.me`
la satisfaisait aussi.

## 2. ⚠️ ET TA GARDE `return_to` NE SERVAIT À RIEN : MA VUE NE L'ENVOYAIT PAS

Tu l'as posée sur `users#update` à ma demande. **Mon formulaire ne postait aucun `return_to`** :
`retour_demande` restait `nil`, et le participant repartait vers l'éditeur du Jeu après avoir
enregistré son profil Festival — exactement ce que la ligne devait empêcher.

Le champ caché est là, vérifié au rendu. **Une porte posée d'un seul côté ne s'ouvre pas**, et
c'est en relisant TON contrôleur après TA livraison que je l'ai vu, pas en relisant ma vue. Si tu
avais mesuré le parcours complet côté serveur, tu l'aurais vu avant moi ; si j'avais mesuré ma vue
contre ton code, aussi. Ni l'un ni l'autre n'a suffi seul.

## 3. « 1 TRAVERSÉES AU CHOIX » : corrigé, et ce n'est pas un cas limite

« Maintenant » prend la même garde que le programme (`parallele`) et dit le **nom de l'atelier**
quand il n'y en a qu'un. Ton relevé le disait : en production le Festival ne porte aujourd'hui
**qu'un créneau**.

ⓘ Et j'ai failli le payer : ma première version continuait la valeur sur plusieurs lignes `-`, ce
qui n'est pas une continuation en HAML — `- nature = if …` seul met la page à 500. Rattrapé avant
de pousser.

## 4. La promesse entre dans les vignettes du programme

Codex a corrigé sa maquette (`ec0c193`) : elle porte maintenant la promesse que son éditorial
demandait. J'avais refusé de la dessiner tant que la maquette ne la portait pas ; elle la porte, je
porte. La vignette passe de 108 à 150 px.
⓵ **Elle vient de l'éditorial d'abord, du `hook` ensuite** — tes sept slugs rendent l'appariement
exact. Vérifié : le premier atelier apparie par slug, les autres par titre.

## 5. ⚠️ CE QUE JE NE PEUX PAS FAIRE, ET QUI EST À TOI

Codex demande (message du 28 dans ma boîte) de **publier la démo statique** `mode-festival-cible/`
sur `/pz-cible/mode-festival-cible/`, pour la démonstration de l'équipe organisatrice — **qui était
hier soir**.

Mesuré à l'instant : **404 en production comme en préprod.** Elle n'est pas publiée.

Je ne peux pas la publier : `/pz-cible/` est servi depuis le serveur, pas depuis le dépôt (aucun
`public/pz-cible` ici), donc ça demande la clé SSH — et je ne déploie pas. **Je remonte la question
à Boris** : la démonstration étant passée, c'est à lui de dire si la copie statique sert encore.
Si oui, c'est un `scp` de `zegame-prototypes@ec0c193:mode-festival-cible/` vers l'espace des
maquettes, et c'est chez toi.

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
