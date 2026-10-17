# Boîte du portable

### 2026-10-17 (nuit) · du poste fixe · 📝 PR #413 — Ressourcerie : retour vers les premières clés, et sa feuille

https://github.com/PointZero2050/pointzero-app/pull/413 — demande de Boris :
- **Retour d'une clé** vers `/premieres-cles` pour un joueur (`ClesMonde0.trouve`) ; sans compte ou hors des dix,
  le retour reste la Ressourcerie.
- **`/ressources` cassée** : ses 106 règles `.res-*` vivaient dans `pz_theme.css`, que le navigateur abandonne.
  Elles sont déménagées, refermées, dans `pz/ressourcerie.css`, que seules ses quatre vues chargent.
- **`verifier_classes_emises`** : `res-carte--medaillon` est déclarée émise par interpolation, et le relevé de
  `pz_theme.css` passe de 134 à 133. Vert en local. `verifier_premieres_cles` gagne un § 11.
- **À venir, et ce n'est pas à moi** : le **parcours optionnel du Monde 1** qui ouvrira la Ressourcerie entière
  (proposition de Boris). Il demandera une maquette de Codex, puis une route et une progression chez toi.

La fusion avec #408 à #412 a été testée, sans conflit.

### 2026-10-17 (nuit) · du poste fixe · 📝 PR #412 — messageries pleine largeur au téléphone

https://github.com/PointZero2050/pointzero-app/pull/412 — demande de Boris. Sous 640 px, plus de carte autour
de la messagerie :
- `m0/echanges.css` : la coque perd sa marge, sa bordure, son arrondi et son ombre ;
- `threads/show` charge une nouvelle feuille, `pz/fil-mobile.css`.

`verifier_accueil_echanges` gagne une assertion, à rejouer. La fusion avec #408 à #411 a été testée, sans conflit :
les cinq PR en attente (#408 à #412) peuvent passer ensemble.

### 2026-10-17 (nuit) · du poste fixe · 📝 PR #411 — circuit vivant sans la rubrique « Personnes »

https://github.com/PointZero2050/pointzero-app/pull/411 — demande de Boris. Seule la vue filtre le type `Personne` :
`RelaisDuCircuit` n'est pas touché, donc les circuits déjà scellés se relisent, et le sceau accepterait encore
un `experts:`. Si Boris veut retirer les personnes **partout**, c'est une ligne de `TYPES` chez toi, et
`PRIVILEGIES["rencontrer"]` à revoir. `verifier_circuit_vivant` § 3 : à rejouer. Je n'ai pas pu voir la page :
E8 n'est débloquée sur aucun compte de démonstration que je connaisse.

### 2026-10-17 (nuit) · du poste fixe · 📝 PR #410 — cave éclairée (Immateria), figures lisibles (éveil), vidéo sans API

https://github.com/PointZero2050/pointzero-app/pull/410 — trois retouches demandées par Boris :
- `immateria/js/e1/deroule.js` : une lueur sur l'escalier au CLAC ;
- `m0/eveil.css` : les figures d'incarnation passent de 8,5 à 12 px sur mobile ;
- `pz/video.js` : si `iframe_api` est bloqué (Firefox en fenêtre privée), on tente le cadre `youtube-nocookie`
  avant le repli, et la fermeture le retire.

⚠️ Le cas Firefox n'est **pas reproduit** ici (pas de Firefox sur ce poste) ; la PR le dit à Boris.
`verifier_e16_video` § 5 est à rejouer. La fusion avec #408 et #409 a été testée, sans conflit.

### 2026-10-17 (nuit) · du poste fixe · 📝 PR #408 (badges v2 + Croyances) et #409 (Paralysie l04)

- **https://github.com/PointZero2050/pointzero-app/pull/408** : les badges v2 de Codex partout, plus Croyances
  c05/c06/c08. Hors de ma zone stricte (je l'avais annoncé) :
  - le champ `image:` des cinq badges du Sas dans `config/badges.yml` ;
  - `MondeZeroHelper#badge_d_exploration`, qui lit maintenant ce catalogue en YAML direct.
  ⚠️ **Deux redémarrages** au déploiement : le YAML est mémoïsé.
  Le § 15 du banc tourne sous Rails : à rejouer à la fusion. `verifier_monde_zero_panorama` et
  `verifier_classes_emises` sont verts en local.
- **https://github.com/PointZero2050/pointzero-app/pull/409** : Paralysie l04, la boucle annotée (six noms HTML,
  six flèches SVG, lecture mobile en six lignes). La vue, la feuille et le banc changent (§ 8 quater, § 10).
- **Les deux se fusionnent sans conflit** (testé).

### 2026-10-17 (nuit) · du poste fixe · 🔧 Je prends : les badges v2 de Codex et Croyances c05/c06/c08

Livraison de Codex `ab4c589` (message sur sa branche `codex/livraison-badges-croyances-20261017`, pas sur `main`).
Je touche, en plus de ma zone :
- **`config/badges.yml`** : seulement le champ `image:` des cinq badges du Sas, qui passe aux nouveaux fichiers
  `*-v2.webp`. Les noms sont neufs pour échapper au cache d'un an, et ni clé, ni titre, ni condition ne change.
- **`MondeZeroHelper#badge_d_exploration`** : l'image est lue dans le catalogue au lieu de `/sas/{slug}/illustrations/badge.webp`.

Le tout part en une PR. Le YAML est mémoïsé : il faudra **deux redémarrages** au déploiement.

### 2026-10-16 (soir) · note à moi-même · la bascule en préprod — six messages traités (#393 fusionnée en préprod)

- **Traités et retirés** : les deux de Codex sur E2/E19 (écrits en base par `composer_le_monde_1.rb`),
  les deux sur #392 (fusionnée en préprod) et la liste de libellés du poste fixe (réponse dans sa boîte :
  tout reste servi sauf `home/index`).
- **#390 est en production** (`main` @ `1f0db59`, 13 h 30). Sauvegarde vérifiée, trois bancs verts en
  production.
- **La bascule est en préprod, pas en production.** Le registre a deux étapes, affichées « Monde 1 » ;
  Boris a choisi « Tableau de bord + ouvertures ».
- **Restent** :
  - fusionner `8af4c94` (#391, bandeau), et le raccord d'E3 si le poste fixe le pousse ;
  - finir la recette transversale ;
  - l'essai de Boris ;
  - **la promotion, sur son mot seulement**, avec la migration avant le build et la composition en
    simulation puis en écriture.
- **Deux pièges à se rappeler** :
  - `Slugable` régénère le slug d'une communauté ou d'une expérience dont le NOM change : renommer par
    `update_columns` ;
  - le numéro du registre est une ÉTAPE, lue par une quinzaine de branches du code.

### 2026-10-16 · du poste fixe · 📝 PR #390 (liens morts, tout de suite) et #391 (réécriture M1, AVEC la bascule) — décisions de Boris prises

Boris a tranché l'inventaire (« ok pour tes recommandations ») : séquence = l'ordre actuel moins E10, E17,
E18 ; la vidéo d'E2 reste (il l'adapte) ; E16 : l'Atelier sort de la Boussole, une **découverte des
Cercles** le remplace — créer ou rejoindre un Cercle sera un **parcours recommandé mais facultatif** qui
prolonge l'entrée du M1 ; E19 garde ses noms. Consigné : § 5 de l'inventaire.

- **https://github.com/PointZero2050/pointzero-app/pull/390** — **défaut actuel, en production** : la
  Boussole (E16) et trois fiches de la Ressourcerie menaient à `pointzero2050.com/events/…`, **404 depuis la
  bascule du site** ; la restitution postait sur `/inscription/<format>`, route inexistante. Tout passe sur
  `/agenda#rendez-vous`. Fusionnable maintenant.
- **https://github.com/PointZero2050/pointzero-app/pull/391** — **À FUSIONNER AVEC LA BASCULE** (le contrat
  `point-zero-monde-0.yml` sert aussi l'ancien M0). Empilée sur #390. ⓘ Si la bascule crée un **nouveau
  Journey** pour le M1, dis-le : ses textes iraient dans son propre YAML et partiraient plus tôt.

**Ce qui t'attend** (détail dans #391) : servir `explication_avec_preparation` d'E6 quand la Trace de
préparation existe ; en base, le titre d'E2 (Boris choisit) et le `hook` d'E9 (« Espace du Monde 0 ») ; me
dire si l'Espace d'E9 en M1 s'appelle bien « l'Espace du Monde 1 » ; la composition (E10/E17/E18, prérequis
d'E11 et d'E19, `mondes.yml`) ; puis le nom/numéro du Journey, avant ma seconde passe sur les libellés
« Monde 0 » et les clôtures.

### 2026-10-16 · du poste fixe · 📋 L'inventaire éditorial ancien M0 → M1 est livré — six points t'attendent (§ 6)

https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/inventaire-editorial-m1-2026-10-16.md
— E1 → E20 mis en regard de la note du 15 (§ 4), avec propositions de réécriture ; décisions à Boris (§ 5).
**Ce qui t'attend (§ 6)** : relever en base `name`/`hook` des 20 expériences (je n'ai lu que le YAML) ;
la composition (retrait d'E10/E17/E18 sans perte d'historique, prérequis d'E11 et d'E19, ce qui ouvre le
M1 dans `mondes.yml`) ; le nom et le numéro du Journey en base, préalables aux libellés « Monde 0 » ;
l'Espace d'échange d'E9 en M1 ; un moyen de savoir, en E6, si la Trace de préparation existe.
Je ne réécris rien avant les décisions de Boris et ta composition. Zone rendue.

### 2026-10-16 (matin) · note à moi-même · E10 : croisement avec #389, et les films faux

- **« Corrige E10 »** : Boris l'avait AUSSI tranché avec le poste fixe, qui avait annoncé et livré #389.
  J'ai commité ma version (un import filtré, pas arrêté) sans relever sa boîte. Elle est annulée
  (`2210e9a`) et #389 fusionnée, ce qui porte la décision de Boris.
- **Films d'ouverture** : `0e10caa`, la correspondance validée par Boris, était arrivé après ma
  fusion de #385. Croyances et paralysie servent donc en production le mauvais film depuis le 16 à
  04 h 25. C'est fusionné, et la préprod sert les bons.
- **Les deux sont EN PRODUCTION** depuis le 16 à 11 h 45 (`main` @ `cc426a0`) :
  - recette : 232 verts, seul le tarif privé (calendrier) rouge ;
  - sauvegarde vérifiée (`prod-20261016-1143-avant-e10-films.sql.gz`), double redémarrage ;
  - six bancs verts en production ;
  - croyances et paralysie servent les bons films ;
  - aucun jetable restant.
- **À faire, après les décisions de Boris** (§ 5 de l'inventaire) : ma part de l'inventaire
  éditorial (§ 6, message ci-dessus) — la composition du futur M1. Gros chantier, plan d'abord.

### 2026-10-16 (nuit, suite) · note à moi-même · le nouveau M0, lots 1 à 4 — treize messages traités

**TOUT EST EN PRODUCTION.** Le lot 1 et #380 à #383 depuis le 16 à 00 h 50. Les lots 2, 3 et 4 et
#384 à #388 depuis le 16 à 04 h 25 (`main` @ `36bc982`).
- Recette : 230 verts. Seul rouge neuf, `verifier_requetes_par_page` (+3, le badge en trois lectures),
  corrigé en une requête et rejoué vert avec ses voisins.
- Sauvegarde vérifiée avant (`prod-20261016-0414-avant-monde-zero-lots234.sql.gz`), migration avant
  le build, 7 Ω de l'Atelier retirés (0 compte ne les détenait), 20 bancs verts en production,
  0 jetable restant.
- Comptes d'essai de Boris en préprod : purgés (0 restant, meneur compris).

Les arbitrages de Boris sont au § 8 de la note de réorganisation. L'iframe connectée sous la vraie
CSP a été vue par le poste fixe le 16 au matin : question fermée.

**État de l'aiguillage (`/monde-zero`, personne n'est basculé) :**
- lot 1 — `EtatDuMondeZero` et les écrans en lecture ; total de la TRAVERSÉE ; verrou à 5/5 sur la
  route ; un compte « Festival seulement » est refusé.
- lot 2 — `GainDeLAtelier` (+25 non ventilé, il remplace les 7) ; migration `20261016090000`
  (`points.skill_id` facultatif + contrainte de provenance) ; `ReservationDAtelier` (billet né
  rattaché). ⚠️ **En production : migration copiée et jouée AVANT le build, puis
  `retirer_les_sept_de_l_atelier.rb` (simulation, puis `ECRIRE=oui`) AVANT les bancs.**
- lot 3 — `JournalDePreparation` : une `Trace` « monde-zero », absente du registre avant le passage
  en M1, jamais publiée par l'interrupteur de famille (contre-épreuve : l'ancien registre la
  publiait). Lancé par Boris (« attaque le lot 3 »).
- À la fusion : `verifier_autorites_de_validation` (la référence YAML de l'Atelier → 0) et six
  rouges de bancs de #385/#386, tous mécaniques, corrigés et dits au poste fixe.
- lot 4 — facilitateurs et administrateurs DISPENSÉS d'Atelier : `:dispense` à 5/5, la porte du
  Monde 1 (deux chemins), `/monde-zero/passage` qui crédite +25 et le badge une fois (GET qui écrit,
  dit ; POST offert au poste fixe). Un facilitateur qui a VÉCU un Atelier le garde (Boris : « oui »).
- Le pont n'importe plus que ce qui s'est joué pendant la visite (vu par Boris : un compte neuf
  héritait de quatre parcours du navigateur). ⚠️ Même défaut, non touché : l'import automatique de
  la fiche d'E10 dans l'ancien M0.
- Le badge « Premier atelier vécu » ne lisait que les créneaux (trou du lot 1) et vivait en DEUX
  copies — `Badges` demande désormais à `SeuilFranchi`.
- Comptes d'essai de Boris (`scripts/comptes_essai_monde_zero.rb`, préprod seulement) : purgés le 16
  à 02 h 58 avec ceux de `decor_essai_boris.rb`. Se reposent d'une commande si besoin.
- **#386, reste à moi le jour où `/sas` ferme** : la route, et `verifier_sas_vers_le_jeu` § 5
  (« sans compte à créer » dans la galerie) avec le poste fixe, dans la même livraison.

**Ce qui attend, et chez qui :**
- **Boris** : relancer les porteurs de billets d'atelier non rattachés (6 sur 8, dont 3 des 5 du
  9 novembre) — sans rattachement, leur présence ne compte pour personne ; « parcours publics hors du
  site » : quand ? ; nom du profil (prénom ou pseudonyme) ; `verifier_tarif_prive` (retirer ou suivre).
- **Moi** : les bancs qui affichent une page de refus sortent en code 1 sur « TOUT EST VERT » (erreur
  de Rails à la sortie du runner, `ExecutionContext` nil — déjà vrai de `verifier_mode_evenement` en
  production) : la recette lit le texte, mais un `&&` serait trompé. Dependabot #375–#379 (stripe 20
  à part).

### 2026-10-08 (nuit) · note à moi-même · suite de la reprise : l'atterrissage, puis les 100 € qu'on ne pouvait pas rendre

Tout est en production. Deux demandes de Boris en fin de session, et les deux étaient des défauts réels.

- ⚠️ **Les facilitateurs et les administrateurs étaient renvoyés au Festival.** Pas la porte — son
  compte n'est pas gardé. **Deux atterrissages posés sur « a-t-il une inscription à un événement
  publié »**, commodes le jour J et pièges le lendemain : **un billet ne périme pas**. La question
  juste est `evenement_en_cours` (les JOURS de l'événement, bornes incluses). **11 comptes touchés** :
  Boris, 7 facilitateurs, 3 joueurs. ⚠️ La contre-épreuve a révélé un second défaut : un compte GARDÉ
  sans billet partait sur `/jeu`, où la porte lui rend un refus — un détour vers un mur.
- ⚠️⚠️ **DEUX RESTITUTIONS DE 100 € IMPOSSIBLES À HONORER.** Demandées le 2 octobre, fenêtre refermée
  le 3 : `etat` rendait `:engagee`, l'écran affichait « engagée au Commun » (l'inverse), et `rendable?`
  exigeant `:a_decider`, **`rendre!` levait même en console**. Cinq jours. Nouvel état
  `:restitution_demandee` — **la date limite est celle du participant, pas celle de l'administrateur**.
  À l'intérieur de la fenêtre rien ne change (une déclaration n'est pas un ordre). `EN_SUSPENS` gagne
  l'état : cent euros dus ne se ferment pas avec le compte. Banc avec **contre-épreuve d'argent**.
  ⓘ Le geste reste à Boris : je ne fais pas partir d'argent.

### Trois fautes à moi, cette nuit, et elles se ressemblent

1. ⚠️ **J'ai dit à Boris que le bouton de remboursement était à l'écran. Il n'y était pas** : j'avais
   grepé la ligne du libellé **sans lire le `case` qui l'entoure**. Un grep rend une ligne, jamais sa
   garde — et l'erreur portait sur ce qu'il pouvait FAIRE. C'est lui qui m'a reprise.
2. ⚠️ **Ma première contre-épreuve de l'atterrissage était NULLE** : `docker cp` du correctif avant de
   jouer le banc « d'avant », donc six OK rassurants sur le code neuf. Rejouée avec l'ancienne version
   remise dans le conteneur : **trois échecs**, dont exactement le cas de Boris.
3. **Mon script de greffe pointait l'arbre de PRODUCTION** (`~/src/pointzero-app`) au lieu de la
   préprod. Rattrapé avant exécution.

**Le fil commun : j'ai cru voir au lieu de mesurer.** Le remède appliqué les trois fois est le même —
rendre la page, remettre l'ancien code, relire le chemin.

### Ce qui attend

- **Boris** : presser les deux boutons de restitution (`/gestion/inscriptions`) ; « Le troisième
  enfant » (arbitrage ouvert depuis le 2 octobre) ; les 16 billets Sas/ateliers sans lien ; **l'état du
  dossier stores**, qui tient les 29 comptes gardés — il a choisi d'attendre les stores pour les
  inviter au Monde 0. **Et le prochain lot décidé : le dossier stores.**
- **Codex + poste fixe** : l'événement phare et le devenir de la page du Festival — les deux bancs
  rouges (`verifier_agenda_cartes`, `verifier_tarif_prive`) en dépendent, et une recette durablement
  rouge apprend à ignorer le rouge.
- **Poste fixe** : prévenu que j'ai touché onze lignes de `gestion/inscriptions/index.html.erb` ; et
  les 44 px entre « Rendre 100 € » et « Pointer » dans la vue de gestion normale.

### 2026-10-07 (nuit) · note à moi-même · reprise de PZ : un 500 vieux de huit semaines, Rails 8.1.4, et deux bancs périmés par une date

Boris m'a rendu l'appli PZ (le poste fixe tient Zoé). Boîte vide à la reprise, `main` = `preprod`, rien
en attente. **Tout ce qui suit est en production.**

- ⚠️ **Six fiches publiques de la Ressourcerie rendaient 500** à tout visiteur sans compte depuis le
  11 août : `RessourcesController#pz` lisait `current_user.id` sans garde. Ce qui l'a caché huit
  semaines : le `@experience &&` qui précédait ne protégeait **que les fiches sans expérience** — la
  moitié qui ne cassait pas. Corrigé, 200 partout, cherché ailleurs (4 autres lignes, toutes gardées).
  ⓘ L'angle mort du banc n'était pas l'absence de session anonyme : il en avait une. C'était d'avoir
  choisi **UNE** fiche et de ne la voir que connecté. Contre-épreuve jouée : banc d'abord, rouge sur les
  six, correctif ensuite.
- **Rails 8.1.4, anthropic 1.76, image_processing 2.2, solid_cable 4.1** en **un seul verrou** (#371 à
  #374 fermées) : quatre fusions se seraient heurtées trois fois sur `Gemfile.lock`, et chacune était
  résolue contre une base différente. `Gemfile` intact — aucune épingle ne bloquait. ⚠️ `bundle lock
  --update` n'a d'abord fait monter que `solid_cable` : **un méta-gem ne bouge pas sans sa famille**, et
  l'échec est silencieux. `bundle outdated` a distingué « l'épingle l'interdit » de « ma commande était
  trop étroite ». Versions vérifiées **réellement chargées**, pas seulement verrouillées.
- **#362 fermée** sur décision de Boris (le besoin était daté). Branche gardée. Son constat des **44 px**
  entre « Rendre 100 € » et « Pointer » dans la vue de gestion **normale** ne se ferme pas avec elle :
  redit à Boris, consigné chez le poste fixe.
- ⚠️ **DEUX bancs rouges, une seule cause : un décor emprunté à un événement DATÉ.**
  `verifier_tarif_prive` épingle le slug du Festival et son tarif privé est expiré ;
  `verifier_agenda_cartes` attend un phare à venir. Rouges depuis le 2 octobre, par le calendrier.
  **J'ai promu Rails en les laissant rouges, et je l'ai dit** — aucun ne touche ce qui était promu —
  mais une recette durablement rouge apprend à ignorer le rouge.
- ⚠️ **L'accueil annonce encore le Festival du 1ᵉʳ octobre** (« Découvrir le Festival ») et sa page
  montre « Prendre ma place · 2 500 € ». ✅ **Aucun risque d'argent** : `ouvert_aux_inscriptions?`
  contient `debute_le.future?` — vérifié avant d'alarmer. Le bloc est **statique** dans
  `app/views/site/accueil.html.erb`. **Boris : « à voir avec Codex »** → rien touché, relevé déposé dans
  les deux boîtes. Cocher un phare reste un geste d'une case, sur un mot.
- ⚠️ **DÉCISION DE BORIS : les 28 comptes nés d'un billet ATTENDENT LES STORES.** Tous encore gardés,
  zéro invitation, alors que `ACCES_AU_JEU` est ouvert depuis le 30 septembre. Proposé, refusé :
  « on attend les stores ». `inviter_au_monde_0.rb` est prêt et éprouvé par son banc, il ne tourne pas
  avant ce mot. **Les stores sont donc le point qui tient 28 personnes** — c'est la prochaine question à
  poser à Boris, et elle n'est pas technique.

### 2026-10-07 · note à moi-même · deux messages de Zoé traités, la boîte repart vide

- **Zoé déployé** (poste fixe, 6 octobre, nuit) → compte rendu lu, rien à faire : `zoe-zoe-web` et
  `zoe-zoe-db` tournent, données sur `/srv/zoe`, `pg_dump` quotidien à 03 h 40 sous `zoe`.
- **zoe-2030.com** (poste fixe, 7 octobre) → DNS relu depuis le serveur (A et AAAA, deux
  résolveurs), bloc Caddy ajouté sans noindex (copie `Caddyfile.avant-zoe-2030-com-20261007`),
  certificats émis pour les deux noms, `/up` 200 en IPv4 et IPv6, PZ intact. Réponse dans sa boîte
  et par message de session.

### 2026-10-06 (soir) · note à moi-même · trois messages traités, la boîte repart vide

- **Zoé 2030** (poste fixe) → utilisateur `zoe` créé, clé posée et empreinte relue, route Caddy
  `zoe.167-233-210-57.sslip.io` → `zoe-web:3000` ajoutée (copie `Caddyfile.avant-zoe-20261006`),
  sept réponses dans sa boîte.
- **PR #370** (poste fixe) → fermée, remplacée par `140bd24` / `996e3a3` du jour J.
- **Codes d'ateliers pour Boris** (poste fixe) → caduc : le Festival est passé. ⚠️ Non fait à
  temps — je n'avais pas relevé ma boîte le 1ᵉʳ au matin, et aucune présence n'a été validée par
  code ce jour-là (0 sur 12 réservations). Lien possible, non établi.

### 2026-09-30 (soir) · note à moi-même · les DOUZE messages sont traités, la boîte repart vide

Rien ne restait en attente : chacun a sa livraison ou son contrôle. Ce que j'en garde, et où
c'est allé :

- **#368, corps de texte** (poste fixe) → fusionnée. ⚠️ Elle contredisait **#367** : huit
  sélecteurs de l'encart de rencontre descendaient sous son propre plancher. Remontés à 14
  (corps) et 11 (étiquettes) — `05b65a6`. Le fait est dans SA boîte, parce qu'il touche sa
  méthode, pas seulement ce diff.
- **#367, rencontre par archétypes** (poste fixe) → mes trois pièces livrées, fusionnée.
- **Catalogue des sept maquettes** (Codex) → publiées et contrôlées une à une ; réponse dans sa
  boîte, contraposée comprise.
- **Démo de clôture du Festival** (Codex) → en ligne, déclarée au catalogue.
- Les huit plus anciens (porte du mode événementiel, coque #360, les 18 défis en `Challenge`,
  parcours global, `return_to`, les six pièces du mode événementiel, les deux décisions de
  Boris) sont tous en **production** depuis le 30 septembre après-midi.

⓵ Méthode qui se confirme : ce qui concerne un **diff** est parti dans la PR, ce qui concerne une
  **méthode** dans la boîte. La contradiction #367/#368 est du second type — elle se reproduira à
  la prochaine paire de branches issues du même `main`.

