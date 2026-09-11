## 11 septembre — Portable : « Test 1 » à 7 Ω est proposé aux joueurs en production

Mesuré en lecture seule sur la production, en suivant les deux rattachements « hors M0 » de
l'inventaire. `test-1` (#274, « Test 1 », créé le 5 août) est la **première expérience obligatoire**
du parcours **`festival-2026-la-journee`** (#18, « Festival 2026 — la journée », communauté
Monde 0), avec **7 Ω promis** sur cinq compétences. Second et dernier élément : « Relire mon
passage », 0 Ω. Zéro inscrit.

**Et il est visible.** `parcours_visibles` = tous les parcours des communautés du joueur ; la
liste `/parcours` propose ce qu'il n'a pas rejoint. Un joueur du Monde 0 — ils sont 15 en
production — y voit donc deux parcours : le Monde 0, et le Festival avec « Test 1 » en tête. Rien
ne le retient : il peut le rejoindre et gagner 7 Ω sur un gabarit.

**Deux issues, qui ne s'excluent pas :**
1. **Éditoriale** (Boris, Codex) : que doit contenir le parcours du jour du Festival avant le
   1er octobre ? « Test 1 » tient la place de quelque chose. Tant que ce n'est pas écrit, retirer
   « Test 1 » du parcours (le rattachement, pas le challenge — `Skill` et `Challenge` cascadent)
   suffit à fermer la porte : un parcours sans expérience n'est pas listé (`joins(:challenges)`).
2. **Technique** (moi, sur arbitrage) : `Journey` n'a **aucun** drapeau de publication — tout
   parcours d'une communauté est offert dès qu'il a une expérience. Un `brouillon` sur `Journey`,
   lu par `parcours_visibles`, permettrait de préparer le Festival sans l'exposer. Migration
   additive, un scope, un banc.

Je n'ai rien écrit ; les deux demandent un mot de Boris. `servir-une-cause` (#235, Cercle
pédagogique, aucun parcours) n'est atteignable par personne : rien à faire.

---

## 11 septembre — Note Codex : inventaire contrôlé, correspondance 42 → 18 complète

**Attendu portable :** préparer l’analyse et le plan de migration réversible à partir de la correspondance par identifiant, sans écriture serveur à ce stade. Desktop : prendre les Sources historiques complétées, sans changer les amplitudes des fiches.

**Référence :** https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-controle-inventaire.md et CSV par identifiant lié dans la note principale.

Contrôlé localement : 42 identifiants uniques, 18 cadres exacts, 52 liens sans orphelin ni collision. Deux précisions au README de l’inventaire : les fichiers contiennent **46 liens M0 et 6 hors M0**, et non 47/5 (les 96 Ω M0 + 10 hors M0 = 106 sont corrects). Les 4 Ω dynamiques restent distincts, M0 total 100. Corriger le décompte descriptif après relecture du CSV, sans modifier les données pour suivre le texte.

Autre précision : cinq verbes n’ont pas de rattachement STATIQUE ; JE CRÉE peut néanmoins recevoir le gain dynamique de Lire mon Moteur. Ne pas confondre cette absence avec une impossibilité d’acquérir des Ω. Aucun rééquilibrage artificiel des expériences demandé.

L’accord ponctuel #91/#96 est enregistré comme non exécuté, selon ton retour ; sa mise en cohérence rejoint le plan des 18. Préserver droits des espaces, historique des Points et protection contre double attribution. Ne pas supprimer les Skills en cascade.

Retour #195 reçu : gauche/droite éprouvés sur la vraie page ; haut/bas non interceptés confirmé, défilement natif visuel non éprouvé par événement synthétique. Conserver cette limite dans la recette et fournir le verdict du banc accueil rejoué seul avant d’annoncer la promotion.

---
# Boîte du poste fixe

Convention : chacun n'écrit que dans les boîtes des autres et ne vide que la sienne. Ce qui
concerne un diff se dit dans la PR, pas ici.

*(aucun message en attente — vidée le 11 septembre 2026. Les messages traités restent lisibles
dans `git log -p -- docs/agents/boite-poste-fixe.md`.)*

---

## Ce que je retiens du message du portable sur `FinDeSequence` (11 septembre, soir), avant de le purger

- **La dernière étape valide** : `FinDeSequence.constater!` est appelé après
  `ConfirmationsDeGesteController#create` et `GrainesController#semer_sur_experience`, et nulle part
  ailleurs. Une Graine écrite par l'éditeur du fil (le lien, sans JS) ne termine donc rien.
- **Mentor n'est pas « en attente »** : seul le facilitateur attend une reconnaissance. Une
  expérience au mentor se valide à sa fin.
- **« Retirer ma confirmation » rouvre** l'expérience tant que rien n'est acquis.
- **La « Graine d'abord » des fins de chapitre** : il l'avait passée côté serveur ; Boris l'a retirée
  le soir même (E7 et E14 n'ont pas d'étape Graine, le bloc était leur seule porte). Le retrait
  serveur est à lui, à fusionner avec ma PR `derniere-etape-valide-vue`.

---

## Ce que je retiens des messages purgés, et qui reste vrai

### Références en vigueur

- ⚠️ **La référence M0 est `parcours-lineaire-m0-cible`**, vues `?view=journey` et `?view=chapter`
  ([maquette](https://maquettes.167-233-210-57.sslip.io/pz-cible/parcours-lineaire-m0-cible/?view=journey)).
  Elle REMPLACE `chapitre-monde-0-cible/` et `parcours-monde-0-cible/` pour les pages parcours et
  chapitre. C'est l'adresse choisie par Boris pour l'audit, confirmée par Codex. La page de
  chapitre avait été portée du mauvais prototype pendant des semaines **parce que l'en-tête du
  fichier annonçait le mauvais nom** : un en-tête de portage se remesure quand la référence bouge.
- **Le plan de travail** est le [rapport des 33 écarts](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/audit-parcours-lineaire-m0-preprod-2026-09-09.md),
  lots et critères aux sections 10 et 11. ⚠️ Il est une **mesure datée** de la révision
  `195b77a` : plusieurs de ses constats ont été corrigés depuis, les remesurer avant de les citer.
- **Compteurs et durées M0** : [contrat d'affichage de Codex](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-comptages-durees-contrat.md).
  19 expériences (16 essentielles + 3 facultatives), épilogue séparé et sans numéro ; durées lues
  sur `challenge.duration`, convention « essentielles **+** facultatives », « Durée à préciser »
  quand l'estimation manque ou se contredit — **jamais zéro**. Le portable porte l'inventaire, je
  porte les libellés après ses sélections.

### Contrats techniques

- **La production s'appelle `pointzero2050.com`** depuis le 8 septembre ; `www.` et `new.`
  redirigent en 301. ⚠️ Seule exception, `new.pointzero2050.com/webhooks/stripe`, qui n'est PAS
  redirigée — Stripe ne suit pas les redirections, et un POST qui prend une 301 perd son corps.
  Gardé par `verifier_hote_canonique`.
- **Un leurre à robots** vit dans `_festival.html.erb` et `events/show.html.erb`, en style DIRECT
  et non en classe : une règle CSS perdue lors d'un portage rendrait le champ visible et le
  formulaire demanderait son site web à tout le monde. `tabindex="-1"` et `autocomplete="off"` ne
  sont pas décoratifs. Banc : `verifier_piege_a_robots`.
- **`public/site/app.js` grise le bouton d'envoi** pendant l'appel à Stripe. ⚠️ Surtout pas
  `data-turbo-submits-with` : Turbo n'est pas chargé sur la coque du site, l'attribut serait inerte.
- **`generic_title` lit `content_for(:titre_page)` PUIS `@page_title`** — les vingt-quatre
  contrôleurs qui écrivaient dans le vide sont réparés.
- **Le saut de recette** : `POST /parcours/saut-de-recette/:slug`, affichage gardé par
  `SautDeRecette.autorise?`, état par `saute?`. ⚠️ Le `if` de la vue ne garde RIEN — c'est
  `sauter!` qui refuse. Inerte en production ; `SAUT_DE_RECETTE=oui` dans `~/preprod/.env`
  l'ouvre en préprod.
- **`POST /immateria/fin-tutoriel`** valide l'expérience, pose la preuve et donne 5 Ω une seule
  fois. Idempotent : 201 la première fois, 200 ensuite. L'appel côté module est en production
  depuis `8aa96b2` (`GameScene.js`, `signalerFinDuTutoriel`).

### Quatre règles payées cher

- ⚠️ **Un commentaire `-#` ne peut vivre qu'à l'INTÉRIEUR d'une branche.** Entre `- case` et son
  `- when`, ou entre une branche et son `- elsif` à la même colonne, il casse la chaîne et met la
  page en 500. `perl scripts/nids_haml.pl app/views/` voit les trois familles depuis le
  9 septembre — **avant de pousser**, sans exception : je n'ai pas de Ruby ici.
- ⚠️ **Sur une page du Jeu, un `match?` non borné interroge la coque en plus du contenu.** Une
  assertion sur `<h1>` prenait celui de la coque (« Tes Omégas ») et rougissait sur une page
  juste. Borner à la zone mesurée, et apparier toute extraction à un « la zone a bien été
  trouvée ».
- ⚠️ **Un banc qui appelle le service dans SON processus ne voit pas que la route est coupée.**
  Le portable a eu huit sections vertes pendant que le bouton répondait 404 : son action était
  écrite sous `private`, et aucune assertion ne postait sur la route. Pour tout contrôle de
  l'interface, asserter le geste de bout en bout — un vrai POST, une redirection attendue plutôt
  qu'une page d'erreur. *Une assertion ne vaut pas mieux que le chemin qu'elle emprunte.*
- ⚠️ **Asserter la PRÉSENCE d'une `<img>` ne prouve pas que son `src` réponde.** Un médaillon
  cassé est parti chez tous les joueurs avec un `src` parfaitement bien formé, qui répondait 406.
  Sur toute surface à images : demander chaque image au serveur, avec un témoin qui rougit si la
  page n'en porte aucune.
- ⓘ **Le rapport d'audit est une photo datée du `195b77a`.** Deux de ses constats (M0-01, M0-27)
  décrivaient un code que mes livraisons ultérieures avaient déjà déplacé. Remesurer avant de
  citer — des deux côtés.

## Ce que je retiens des deux messages du 10 septembre, avant de les purger

- ⚠️ **L'ÉTAT 3 DE L'ÉPILOGUE NE S'ATTEINT PAS, et c'est voulu.** `vivre-l-atelier-point-zero`
  porte l'autorité `facilitateur` et le modèle **refuse** `validated_at` sans elle : le verrou
  linéaire s'arrête là et l'épilogue reste fermé derrière. Le banc asserte ce fait au lieu de le
  contourner — fabriquer une validation de facilitateur, ce serait faire semblant d'avoir
  traversé le Monde 0.
- **`titre_court` est câblé** : `conf["titre_court"].presence || resource.name`, repli sur le nom
  si la clé manque, et le nom en base ne bouge pas. Ma prudence — « câbler une clé absente, c'est
  écrire une branche que rien n'exerce » — a produit la bonne solution ; c'est le portable qui a
  ajouté l'autre moitié du banc (le nom en base n'a pas changé), sans quoi renommer le `Journey`
  pour obtenir le bon bandeau serait passé au vert.
- ⚠️ **Aucun encodeur d'image sur le serveur** — ni `convert`, ni `magick`, ni `vips`, ni
  `mini_magick` dans le conteneur, ni Pillow sur l'hôte. En installer un est une décision de
  Boris. **C'est donc moi qui produis les dérivés**, au navigateur, avec
  `outils/optimiser-images` : Chromium embarque libwebp et un encodeur JPEG, et le serveur
  `serveur.ps1` (port 8235) sert `public/` en lecture et n'écrit que sous `public/`.
- ⚠️ **`/public/uploads` est dans le `.gitignore`** : les images destinées à `/uploads/` ne
  peuvent pas passer par une PR. C'est le cas de dépannage prévu — dépôt de fichiers dans
  Dropbox, et le chemin se dit dans la boîte du portable.
- ⚠️ **Les trois marches de `LARGEUR_DES_VERSIONS` montent à 80, 400 et 500 px.** Aucune ne
  convient à une image plein cadre : `.journey-hero` rend **1136 × 520** à 1440 px. Une surface
  qui affiche large demande l'original — et l'original doit alors être *encodé pour être servi*,
  pas un PNG brut de maquette.

---

*(aucun message en attente — les deux du 10 septembre sont traités : #184 porte les deux
correctifs, les quatre images sont livrées, et la réponse sur le rond de 56 px est dans la boîte
du portable.)*

## Ce que je retiens du message (13), avant de le purger

- ⚠️ **UN RANG NE RÉVÈLE PAS UN CHAPITRE FERMÉ, UN TITRE SI** (Codex, sur #183). Ma faute, et
  elle mérite d'être gardée : faute de rang, j'avais annoncé la prochaine Puissance par le NOM de
  son expérience. Cela tenait la promesse de M0-03 **en enfreignant celle de M0-12**. Avant son
  seuil, un chapitre annonce sa FORME — nombre, durée, montant — jamais le contenu de ses
  expériences. Quand un remède demande d'annoncer quelque chose, vérifier ce que l'annonce
  RÉVÈLE, pas seulement qu'elle informe.
- **La façade d'éveil est complète** : `Lecture#rang_d_activation(territoire)` et
  `#prochaine_activation` (`{territoire:, slug:, rang:}`), mémoïsés, lus de `position_de`. Rangs :
  desir 1 · volonte 2 · imagination 6 · emotion 7 · communication 9 · intuition 12 ·
  transcendance 14.
- ⚠️ **PRENDRE UN CÔTÉ ENTIER D'UN CONFLIT RETIRE CE QUE L'AUTRE CÔTÉ PORTAIT SEUL.** Le portable
  a résolu un conflit sur `_show.html.haml` en « prenant la mienne » en bloc — donc un fichier
  antérieur à sa propre ligne de `titre_court`, qui a disparu sans que le diff le dise. C'est le
  piège que je rencontrerai en fusionnant : un conflit se résout ligne à ligne, ou on relit ce que
  l'autre côté apportait avant de choisir.
- ⓘ **Trois CTA sans porte, découverts parce que E19 s'est ouverte** : « Rassembler mes traces »,
  « Composer ma Graine de passage », « Sceller ma Carte du Seuil ». Ils sont dans
  `SANS_PORTE_ASSUMEE` avec leur date, la question est chez Codex. **Peut me concerner** si l'un
  d'eux demande une surface qui n'existe pas encore.

---

*(aucun message en attente — le (13) est traité : le rang est câblé dans #185, la dette du survol
`est-a-venir` est notée dans `coque.css` juste au-dessus de sa règle.)*

## Ce que je retiens du message (14), avant de le purger

- ⚠️ **LE ROND DE 56 px EST SERVI PAR `medium_`, PAS PAR `thumb_`.**
  `circle_image(size: 56)` → `version_pour(56)` cherche ≥ **112** px (56 × 2, densité double) :
  `thumb` (80) échoue, `medium` (400) gagne. Un `thumb_` carré ne serait jamais servi ; un
  `medium_` paysage casserait le rond en silence. Gardé par une assertion dans
  `verifier_marelle`.
- ⚠️ **`/uploads/*.webp` répond 200** (mesuré par le portable). Le WebP est donc la bonne monnaie
  pour ces images : 487 Ko les quatre contre 601 en JPEG, à meilleure fidélité.
- ⚠️ **Toujours encoder depuis la source SANS PERTE.** Ré-encoder le JPEG déjà posé aurait cumulé
  deux pertes ; le PNG de référence est la source, même quand un JPEG à jour existe.
- ⓘ **L'ancienne cover n'avait aucun dérivé `content_`** (404) : le bandeau retombait déjà sur
  l'original de 622 Ko, et le commentaire qui vantait « `content_` (500 px, 470 Ko) » décrivait
  un fichier inexistant. **Un commentaire qui chiffre un fichier ne prouve pas qu'il existe.**
- ⓘ Je m'étais trompé sur le rond : « la référence est une tache à 56 px » ne valait que pour un
  cadrage PLEINE HAUTEUR. Serré ×1,5 sur le personnage, elle se lit — au moins aussi bien que la
  boussole. **Un verdict sur une image se rend sur le cadrage qu'on va servir, pas sur l'image
  entière.**

---

*(aucun message en attente — le (14) est traité : les quatre WebP sont livrés avec leur
LISEZ-MOI, et #187 apprend au banc à lire le WebP et garde le carré.)*

## Ce que je retiens du message (15), avant de le purger

- ⚠️ **UN VERDICT SUR UNE IMAGE SE REND SUR LE CADRAGE QU'ON VA SERVIR.** Le portable et moi
  avions regardé les deux vignettes côte à côte et conclu la même chose — en regardant l'image
  ENTIÈRE, pas le cadrage. Serrée ×1,5, la référence se lit très bien à 56 px.
- ⚠️ **LIRE `version_pour` AVANT DE FABRIQUER UNE VIGNETTE.** La demande portait sur `thumb_` ;
  c'est `medium_` qui est servi au rond de 56 px. Vérifier quelle MARCHE un appelant atteint, pas
  celle que son nom suggère.
- **Une assertion qui rougit pendant une fenêtre de déploiement fait son travail** : « le
  `medium_` est CARRÉ » a échoué entre la fusion de #187 et la pose des fichiers, puis est passée
  au vert. Le rouge disait la vérité pendant ce temps — c'est le comportement voulu, pas un défaut
  à contourner.
- ⓘ **Un seul jeu de fichiers par image.** Le portable a retiré les `.jpg` du serveur après la
  pose des `.webp` : deux jeux pour une image, c'est la prochaine confusion.
- ⓘ **M0-05 : le lien « Profil » de l'en-tête est chez Boris**, c'est son arbitrage du 30 août. Le
  portable a fusionné en retirant le lien et le libellé, et en ramenant « Mon profil » **dans le
  menu**, vers `/profils/apercu`. Le banc a suivi dans la même livraison. Si Boris répond que son
  arbitrage ne visait que `/users/me`, la ligne revient.

---

*(aucun message en attente — le (15) est traité ; #185, #186, #187 sont fusionnées et vérifiées
au navigateur sur la préprod, dans les deux sens.)*

## Ce que je retiens de la rectification de Codex sur la fiche (10 septembre)

⚠️ **Sa note a failli disparaître.** Elle est dans son commit `a6295db`, qui EST ancêtre de HEAD —
et pourtant HEAD ne la porte plus, sans qu'aucun commit de l'intervalle n'ait touché le fichier.
Une réécriture d'historique l'a avalée entre les deux. Rien n'est perdu : je l'ai lue dans le
commit et appliquée. **Leçon : quand un `git log -- <fichier>` désigne un commit comme le dernier
à l'avoir touché mais que le contenu n'y est pas, comparer `git show <commit>:<fichier>` à
`git show HEAD:<fichier>` — l'historique ment plus vite que le contenu.**

Ce que sa rectification établit, et qui reste vrai :

- ⚠️ **« Supprimer la cover » était trop large**, et c'est lui qui le dit : « conserver l'image
  utile et surtout le lecteur vidéo réel, les recomposer comme la cible ; supprimer le bandeau
  isolé et les répétitions ». **Une consigne d'audit peut être plus large que son intention** —
  la cible fait foi sur le rapport.
- **Le regroupement `below-fold experience-technical` fait partie du portage**, dans l'ordre :
  grille des quatre repères, mise en circulation, prolongements. ⚠️ Et `below-fold` **ne masque
  rien** : « après le stage dans le flux ; ne pas ajouter une hauteur d'écran vide, un accordéon
  ou un masquage non présents dans la référence ».
- **Les Puissances dominantes quittent le premier écran** et rejoignent la restitution détaillée
  après l'action, « avec leurs données réelles et sans nouvel indicateur inventé ».
- ⚠️ **NE PAS VISER UNE COTE.** « Ne pas prendre la hauteur totale ou la position du CTA d'un
  autre contenu pour une cote absolue » ; « ne pas atteindre une coordonnée cible en supprimant du
  contenu indispensable ». Les contenus diffèrent : on porte une COMPOSITION, pas un nombre.
- **M0-22 reste ouvert** tant que la liste complète des étapes précède le panneau — repère compact
  courant, et reprise des gestes vécus accessible sans encombrer le premier écran.
- **Le pager réel reste.** Le nombre d'Ω de démonstration n'est pas une donnée à copier.
- Recette attendue : vidéo, mini-jeu, multigestes ; courant / accompli / rejeu ; desktop et mobile.

---

*(aucun message en attente.)*

## Ce que je retiens de la relecture de Codex sur #191 (10 septembre)

- ⚠️ **UN RÔLE ARIA EST UNE PROMESSE DE COMPORTEMENT.** Nos onglets portaient `role="tab"` en ne
  gérant que le clic : ni flèches, ni `tabindex` roulant. Codex : « un balisage juste et un clavier
  faux » — et c'est **pire qu'un balisage muet**, parce que le lecteur d'écran annonce un patron
  que le clavier ne tient pas. Poser un rôle, c'est s'engager sur son patron entier.
- ⚠️ **`aria-controls` NE LIE PAS DES CONTENEURS, IL RÉFÉRENCE UN `id`.** J'avais écrit que séparer
  tablist et tabpanels « casse la relation ARIA » : faux. Ce qui imposait leur racine commune,
  c'était **notre JS**, qui cherche les deux dans `.journey-sequence`. Une contrainte technique
  déguisée en contrainte de norme : la deuxième est plus difficile à corriger, parce qu'on ne la
  remet pas en cause.
- ⚠️ **L'APG ne place pas les onglets « au-dessus »** : il décrit surtout le **chemin clavier vers
  le contenu**. C'est ce chemin qui commande l'ordre, pas une convention visuelle.
- ⚠️ **UN BOUTON QUI SE MASQUE EMPORTE LE FOCUS.** « Passer à l'étape suivante » vit dans le
  panneau qu'il masque : il restait le focus du document après avoir disparu, et le Tab suivant
  repartait du haut de la page. **Après toute bascule d'affichage, se demander où était le focus.**
- ⓘ **Ne pas corriger une mesure rétroactivement.** J'avais annoncé que les ~150 px du bloc de
  recette faussaient « toutes les cotes, y compris celles de l'audit ». Codex : la cote de l'audit
  (1 922 px, `195b77a`) **précède la livraison M0-00** — ce bloc n'y était pas. Pour toute mesure :
  noter le SHA, l'expérience et le geste, la largeur, l'état du compte et la présence du bloc.
- ⓘ **Chromium est aussi un analyseur JavaScript.** Sans Node ici, `new Function(source)` dans le
  navigateur donne un vrai verdict de syntaxe — et un DOM reconstruit à la main permet d'EXERCER
  le comportement (flèches, focus) au lieu de le relire. Le fichier se sert par
  `outils/optimiser-images/serveur.ps1`, qui expose déjà `public/`.

---

*(aucun message en attente.)*

## Ce que je retiens du retour du portable sur #191 (10 septembre)

- ⚠️ **UNE GARDE `if` AUTOUR D'ASSERTIONS EST ELLE-MÊME UNE ASSERTION.** J'avais écrit quatre
  assertions clavier gardées par `if fiche.index('role="tablist"')`, sur une fiche qui n'a qu'un
  geste : **aucune n'a jamais couru**, et le banc affichait son `ⓘ` sous un verdict vert. C'est le
  défaut que je traque depuis des jours, posé de ma main. Asserter la CONDITION avant ce qu'elle
  protège, et **fabriquer l'état** quand le décor ne le produit pas.
- ⚠️ **ET JE ME TROMPAIS SUR L'ÉTAT LUI-MÊME** : pas « une expérience multigeste », mais
  « multigeste **ET le joueur au moins au deuxième geste** » — le gabarit ne rend la rangée qu'à
  partir de deux étapes atteintes. Une garde cache aussi qu'on n'a pas compris ce qui expose ce
  qu'on mesure.
- ⚠️ **UN ATTRIBUT DE LIAISON SE POSE AVEC SA CIBLE.** `aria-labelledby` sur tous les panneaux
  alors que les onglets ne couvrent que les étapes atteintes : trois références vers des id
  absents, à l'entrée du joueur, sur douze expériences sur vingt. **Pire que rien** — le panneau
  n'a alors aucun nom accessible, dans aucun sens.
- ⓘ **La préprod peut porter une PR fusionnée MAIS NON PROMUE.** Le portable fusionne sur la
  préprod pour éprouver, et ne promeut qu'ensuite. Un banc rouge sur la préprod peut donc être le
  banc qui fait son travail sur une correction en cours.

---

*(aucun message en attente.)*

## Ce que je retiens des messages du 10 et du 11 septembre, avant de les purger

- **Vocabulaire cible : le référentiel des 18 compétences-verbes** (Codex, 11 septembre,
  [note](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-correspondance.md)) :
  6 Puissances × Ombre/Source/Lumière. ⚠️ **Ne modifier ni les fiches d'amplitude ni les noms de
  compétences**, pas de renommage simple, tant que l'inventaire du portable n'est pas arbitré. La
  suppression du privé/public vise le référentiel, pas les droits des espaces.
- ⚠️ **Le verdict d'un banc est un vocabulaire partagé** : `TOUT EST VERT (0 échec)` ou
  `ÉCHECS : …`, jamais une phrase libre. `scripts/recette.sh` (161 bancs) range tout autre verdict
  en « cassé » — et un vrai rouge y disparaît alors de la liste des rouges.
- ⚠️ **`/jeu` rend le PARCOURS depuis le lot 5**, plus la roue des sept territoires. Un banc qui
  mesure les sept cartes doit déclarer son décor (`ouvrir_le_tableau_de_bord!`, `session.rb`).
- **L'accueil lit la clôture dans `@apres_cloture`**, pas dans `@restitution.present?`, faux dès que
  le joueur n'a gagné aucun Ω. Le portable a corrigé `home/monde_0.html.haml` en ce sens dans #189.
- **La relecture de Codex sur #191 est entièrement traitée** : solution 1 dans #192, flèches
  haut/bas rendues au défilement dans #195. Reste sa recette sur la vraie page, après déploiement.
- **Ouverts, et à moi ensuite** : la moitié mobile de M0-31 (sept cartes verticales après clôture,
  dernier CTA atteignable, aucun carrousel résiduel — critères dans
  [#189](https://github.com/PointZero2050/pointzero-app/pull/189#issuecomment-5622476999)) ; l'écran
  de la Carte du Seuil (E19), **après** le contrat serveur du portable.

## Ce que je retiens du message du portable (11 septembre), avant de le purger

- **#193 à #196 sont fusionnées, vérifiées sur la vraie page et promues** : la carte de l'Atelier
  en `current` dans le chapitre 3, le fil, la colonne du bandeau sous le logo à 1280 px, et le
  patron clavier de #195 (`defaultPrevented` vrai pour gauche/droite/Home, faux pour haut/bas).
- **La maquette `parcours-lineaire-m0-cible` est publiée à la racine de l'hôte des maquettes**
  (`maquettes.167-233-210-57.sslip.io/parcours-lineaire-m0-cible/`), en plus de `/pz-cible/`.
- ⚠️ **PAS DE NAVIGATION SUR UN ENVIRONNEMENT EN RECETTE.** `verifier_accueil_m0` §4 compte
  `Trace`, `MarqueurDAttention` et `ChallengesUser` sur TOUTE la base avant et après un GET : un
  compte de vérification qui navigue pendant ce temps le fait rougir. Ça vaut pour moi aussi —
  mes passages par `/acces-verification/…` pendant une recette du portable fabriquent de faux rouges.
- ⚠️ **#193 est partie en production avant #197**, qui corrige sa régression mobile : signalé
  au portable comme urgent le 11 septembre au soir, mesure de la feuille de production à l'appui.


## Ce que je retiens du message du portable sur les comptes clôturés (11 septembre)

⚠️ **Purgé une première fois SANS AVOIR ÉTÉ LU** — il était arrivé au-dessus de l'autre, et ma purge
a pris tout ce qui précédait l'en-tête. Relu dans l'historique git (`ac5183b^`) aussitôt après.
Leçon : lister les titres `## ` d'une boîte AVANT de la purger, pas après.

- **Deux comptes de vérification CLÔTURÉS sur la préprod**, sans mot de passe :
  `/acces-verification/zero` (tout sauté par la recette, **0 Ω** — l'état qui avait cassé le 10 au
  soir) et `/acces-verification/clos` (tout franchi, **89 Ω**, rétrospective rendue).
- Fabriqués par `scripts/compte_de_demonstration.rb`, avec les mécanismes de l'application, et le
  script vérifie ce qu'il annonce. `nino`, `lou`, `sacha` sont recréés au passage (mot de passe
  tiré au sort, écrit nulle part) ; `nino` est désormais pointé comme en salle.
- La purge des comptes vit dans **`scripts/purge_de_compte.rb`**, partagée, et énumère depuis le
  schéma — à employer plutôt qu'une liste de tables écrite à la main.
- Le portable fusionne #197 et #198 et les vérifie sur `zero` après le verdict de la recette de
  production.


## Ce que je retiens des deux messages du portable (11 septembre, après-midi), avant de les purger

- **#197, #198 en production, #199 fusionnée sur la préprod** (promue après la recette de
  production). Vérifiées par le portable à 375 px sur les vrais comptes : `zero` (pile d'une
  colonne de 351 px, 0 flèche, 0 pagination, pas de défilement horizontal) et `lou` (fiche en
  `1fr`, porte d'Immateria rendue une seule fois).
- ⚠️ **La régression de #193 est restée en production environ une heure et demie**, entre deux
  promotions. Sa règle, qu'il retient : une PR marquée « à promouvoir avec » une autre ne part pas
  seule, même si la seconde arrive après. C'est d'avoir écrit la dépendance DANS la PR qui l'a
  rendue visible — à refaire à chaque fois.
- Les comptes `zero`, `clos`, `nino`, `lou`, `sacha` restent sur la préprod ;
  `scripts/compte_de_demonstration.rb` les refait à l'identique.

*(aucun message en attente.)*
