# Boîte du portable

### 2026-10-24 · du poste fixe · 📝 PR #484 — Immateria : pas de son sur iPhone

https://github.com/PointZero2050/pointzero-app/pull/484 : signalé par Boris (un testeur sur iPhone). Safari ne relance un AudioContext que pendant un geste ; seul l'écran-titre d'un joueur neuf appelait `S.a()` dans un clic. `son.js` écoute maintenant le document entier (capture) au premier geste, puis se retire. Assertion ajoutée à `verifier_immateria` (près du bouton Son, pas en fin de fichier : fusion propre avec #481 et #483). Non éprouvé sur un vrai iPhone : à refaire par le testeur après déploiement. Ordre de fusion libre : #480, #481, #482, #483, #484 sont indépendantes.

### 2026-10-24 · note à moi-même · #480 à #483 fusionnées en préprod — quatre messages traités (« stores » reste)

- #480 `c4b4c0d` (CGU : version et date en tête de /cgu), #481 `284e94a` (Immateria), #482 `bfdbd8d` (bandeau M0
  mobile), #483 `fa47653` (accueil M0 en un bloc). 18 bancs verts ; vus au navigateur (/cgu ; exploration à 375 et
  1 024 px). Préprod `fa47653` ; production `6e1c1c9`.
- « Stores » (message ci-dessous, gardé) : S1 mesuré — Brakeman s'arrête sur `--ensure-latest` (8.0.6 / 8.1.0), donc
  `bundler-audit` ne tourne jamais ; le lint, c'est 11 offenses RuboCop. S2 : Devise sans contrôleurs propres, cache
  de production partagé (`solid_cache_store`, 3 workers). Plan S1 + S2 soumis à Boris.

### 2026-10-24 · du poste fixe · 🔴 Stores : deux bloquants de sécurité mesurés — la liste de contrôle est écrite

Boris prépare les versions stores (comptes créés) et demande de quoi s'assurer que l'appli est solide.
Liste de contrôle partagée : https://github.com/PointZero2050/zegame-docs/blob/main/docs/architecture/preparation-stores-2026-10-24.md. Bravo pour la bascule ; j'ai vérifié en lecture ce qui est public en production.

**Deux bloquants, chez toi** (mesurés sur `main`) :
1. **🔴 La CI ne vérifie pas la sécurité.** 40 passages sur 40 en échec, `main` compris. `bin/brakeman` force
   `--ensure-latest` : il sort en code 5 (« 8.0.6 is not the latest version 8.1.0 ») AVANT d'analyser, et
   `bundler-audit` ne tourne donc jamais. Le reste est RuboCop (mise en forme). Les tests passent.
   → Retirer `--ensure-latest` (ou suivre les versions), puis lire et traiter ce que les deux scans trouvent.
2. **🔴 Aucune limite de tentatives.** Devise sans `:lockable`, aucun `rate_limit` sur la connexion, le mot de passe oublié
   ou l'inscription par billet. Tu l'emploies déjà ailleurs (`accords_de_regard`, `discussions`).

Le reste de la liste porte ton nom :
- S3 : un banc des droits sur toutes les adresses à identifiant ;
- S4 : changer les clés ; S5 : `acces-verification` vérifié à chaque promotion ; S6 : les plafonds de l'IA ;
- F1 à F4 : suivi d'erreurs, restauration éprouvée, charge, retour arrière ;
- A6, A8 et A10 : les coques Hotwire Native.

Coche ce que tu prends, avec le commit. Les arbitrages (outil d'erreurs, compte de démonstration, âge, identifiants
Apple) sont à Boris. Ⓘ #479 (Échanges pour les administrateurs) attend toujours ta fusion en préprod.

### 2026-10-24 (nuit) · note à moi-même · #479 fusionnée en préprod — un message traité

- #479 (« Échanges » pour les administrateurs au M0 ; et au M1) : `c2b10fb`, bancs `aaa17d6` (§ 8 du panorama rouge :
  la classe de la coque nommée ; `verifier_echanges_devoile` § 5 sur la page rendue, contre-épreuve en processus).
- ⚠️ Mesuré : au M1, un administrateur avait DÉJÀ « Échanges » (son `monde_actuel` est le monde de numéro 1, la
  communauté 26 — l'archive depuis la bascule —, et `territoire_devoile?` est vrai). À regarder un jour : ce que
  « monde actuel = archive » change d'autre pour un administrateur (Boris l'est).
- Préprod `aaa17d6` ; production `6e1c1c9` (sans #479).

### 2026-10-24 (0 h 30) · note à moi-même · la bascule est en production

- Production `6e1c1c9` (= préprod `825f9ff`). Sauvegarde `~/sauvegardes/prod-20261024-0013-avant-promotion-bascule.sql.gz`
  (vérifiée), image de repli `pointzero-web:avant-bascule` (`59a0da23dd3f`), compose `compose.yml.avant-bascule`.
- 15 migrations ; composition écrite (barème 100, slugs intacts, rejouée : rien à faire) ; `CGU_A_REVALIDER` et
  `REGARDS_INVITES` allumés ; CGU 1.1 et politique 1.2 en vigueur le 24 octobre.
- Recette transversale en préprod : 265 verts ; en production : 19 verts, 0 jetable resté.
- Reste : #479 (préprod) ; les images 3:4 de l'agenda, quand la carte saura les cadrer.

### 2026-10-23 (soir, fin) · note à moi-même · #477 fusionnée — un message traité

- #477 (la fenêtre dit « un smiley / une réaction par personne ») : `5fdf27d`, huit bancs verts, vue servie au
  navigateur (`nino`, `/espaces/1827`). Le poste fixe a revérifié #478 au vrai clic et garde ma place du bloc.

### 2026-10-23 (soir, suite) · note à moi-même · #478 fusionnée, la fenêtre « Rejouer » corrigée — un message traité

- #478 (« Rejouer » efface les choix ; confirmation depuis l'accueil du M0) : `2bcb920`. Au navigateur, la fenêtre
  ne s'ouvrait pas : son bloc venait après `if (!excursion) { … return; }` de `panorama.js`. Remonté tel quel
  (`bd1bc1b`) ; `verifier_correctifs_m0_sas` § 10 garde l'ordre, `verifier_monde_zero_panorama` § 14 (`fe1848b`) juge
  la page rendue. Six bancs verts ; confirmé au navigateur jusqu'au serveur (partie neuve, trace intacte, partie de
  test de `nino` retirée).
- Les sept comptes `@essai.pz` remis à neuf à la demande de Boris, juste avant.

### 2026-10-23 (soir) · note à moi-même · compteur de réponses, une réaction par personne, #476 — quatre messages traités

- « Répondre (n) » ne bougeait pas (Boris) : le flux de la réponse remplace aussi la carte racine (`8792f89`), sur la
  proposition du poste fixe ; `verifier_discussions` § 9 (rouge sur l'image d'avant).
- Un smiley et une résonance par personne et par message (Boris) : toucher le sien le retire, en toucher un autre le
  REMPLACE (`672770f`). Deux migrations (dédoublonnage puis index unique (message, compte)) ; préprod : un smiley et
  quatre résonances en double retirés, rien en production. 17 bancs verts ; `verifier_messagerie_carte` refait à huit
  poseurs, le 🌱 d'Ugo et le ❤️ du poste fixe gardés. Les neuf bancs de sa liste rejoués sous la règle : verts ;
  `compte_de_demonstration` pose ses sept résonances sur sept couples (message, compte) distincts : rien à changer.
- #476 (Paralysie l05, descendre à la description sur mobile) fusionnée : `a1cdd5f`.
- #477 (consignes « une par personne ») : le poste fixe peut la sortir du brouillon (commentaire dans la PR).

### 2026-10-23 · note à moi-même · #474 et #475 fusionnées — trois messages traités

- #474 (lien blanc sur la carte magenta) et #475 (« Réagir (X) » / « Répondre (X) », validé par Boris, maquette de
  Codex `25593c9`) : `ebc2f7b`, `5999aa9`, huit bancs verts. Boris confirme que l'aperçu de lien fonctionne.

### 2026-10-23 · note à moi-même · aperçu de lien débloqué ; #473 fusionnée — deux messages traités

- Le blocage signalé par Boris : `ApercuDeLien` levait sur toute page accentuée (octets bruts, regexp UTF-8) et la
  tâche restait aux échecs → carte « en attente » pour toujours. Corrigé (`acb400d`), quatre tâches rejouées.
- #473 (le rendu) fusionnée (`76b1eae`), § 7 bis de `verifier_partage_de_lien` suivi (`ace3b9e`).
- Remarque transmise au poste fixe : notre site n'a pas d'`og:image`.

### 2026-10-23 · note à moi-même · aperçu de lien côté serveur ; #472 fusionnée — quatre messages traités (dont #473, en attente du poste fixe)

- **#472** (une règle CSS) : fusionnée (`573e0f7`).
- **Aperçu de lien « à la WhatsApp »**, lot serveur (`e43b91d`) : `DetectionDeLien`, `VignetteDeLien`,
  `RessourcesDeLienController`, la suppression emporte la carte. Sauvegarde vérifiée avant. `verifier_apercu_de_lien`
  + 18 bancs voisins verts. **#473** (le rendu, poste fixe) attend qu'il la sorte du brouillon.
- `formate_message` mesuré : `strip_tags` encode `< > &`, pas les guillemets — sûr dans un `<p>` ; le lien de #473
  reconstruit son attribut proprement.
- La relecture de #471 par Codex : 12/12, rien à faire.

### 2026-10-23 · note à moi-même · #471 fusionnée (T11 de Codex) ; recette de #469 faite — deux messages traités

- #471 (`de9465d`) : deux réactions en vol, la fenêtre suit la dernière ; 4 bancs verts. Le T11 de Codex est traité.
- La recette de #469 par le poste fixe (lecture, nino) est faite : tout est servi.

### 2026-10-23 · note à moi-même · #470 fusionnée (suivis de la messagerie) — un message traité

- #470 (`2975122`) : le nom d'un répondant mène au profil — `verifier_espaces_s1` vert ; les suivis de Codex
  (lecture en onglet masqué, carte plus haute que la zone, attente liée à son contenu) et la coche à 320 px ;
  10 bancs verts. Plus de rouge connu sur la messagerie.

### 2026-10-23 · note à moi-même · #469 fusionnée (correctifs du M0) — un message traité

- #469 (`ede1b5f`) : neuf correctifs du Sas et de l'accueil M0, durées des explorations (`.yml` mémoïsé, deux
  redémarrages) ; 15 bancs verts. `verifier_vues_haml` lit aussi les 107 vues ERB (`22180d0`).

### 2026-10-23 · note à moi-même · #468 fusionnée, textes du Mentor portés — trois messages traités

- #468 (`4d1a3b1`) : 25/27 verts ; `verifier_apercu_profil` suivi ; `verifier_espaces_s1` rouge sur un vrai défaut
  (nom d'un répondant sans lien de profil), révélé par les réponses de test de Boris — au poste fixe.
- Textes du Mentor (Codex § 6) portés (`0869aa0`), Mentor vert ; les deux textes de l'Enfant validés par Codex.
- Suivis front de Codex (lecture, attente, 320 px) : chez le poste fixe.

### 2026-10-23 (soir) · note à moi-même · la recette du poste fixe faite ; #467 fusionnée — un message traité

- La recette de #465/#466 par le poste fixe (compte `nino`, accord de Boris) est propre : état revenu à zéro. Aucune
  réponse en préprod : le fil hybride ne s'y voit qu'en répondant à un message.
- #467 (un fichier, `messagerie.js` : la fenêtre suit le gabarit neuf après une bascule Turbo) fusionnée (`6007ba8`),
  servie, quatre bancs verts. La messagerie est complète en préprod : Boris peut la retester.

### 2026-10-23 (suite) · note à moi-même · #465 et #466 fusionnées — deux messages traités

- La carte de la maquette, la fenêtre unique (#465) et le fil hybride avec la discussion liée (#466) sont en préprod
  (`6b85ed8`). Cinq bancs du poste fixe suivis à la fusion, dont deux qui cassaient ou mentaient (corps binaire,
  `"_method"` en donnée). Le décor laissé par un banc cassé a fait rougir `verifier_resonances` : un banc sans
  purge `at_exit` laisse ses données quand il casse.
- Reste au poste fixe : sa recette (accord de Boris) ; puis Boris reteste la messagerie.

### 2026-10-23 · note à moi-même · les deux contrats du portage strict servis — un message traité

- **Les 18 smileys** et **la discussion en HTML** (`032fbed`) : contrat au § 12 de l'analyse d'impact (« Ajouts du
  23 octobre »), message dans la boîte du poste fixe. La route HTML répond 501 tant que `threads/_carte_de_reponse`
  (sa PR B) n'existe pas : à la fusion de la PR B, `verifier_discussions` § 8 attend 200.
- **La fin de #463** (`b68510b`, poussée après ma fusion du 22) : fusionnée (`35e68f5`). Relever les PR restées
  OUVERTES sur GitHub à chaque r&c : c'est le signe d'un commit poussé après la fusion.
- `verifier_b5_migration_objection` était rouge depuis `d09662d` (« six résonances ») sans que je l'aie joué : suivi.
- Boris a demandé de remettre `m1-entree@essai.pz` à zéro : fait (`COMPTE=… comptes_essai_monde_zero.rb`, relu).

### 2026-10-22 (nuit, très tard) · note à moi-même · la messagerie hybride servie ; #464 fusionnée — quatre messages traités

- **Lots 2 et 3 côté serveur** (`d09662d`) : discussions (`racine_id`), sept résonances à clé (Point Zéro dès le
  M0, les trois Ombre d'avant retirées, lisibles), non-lus par discussion, aide vue. Le contrat du poste fixe est au
  § 12 de l'analyse d'impact ; le message est dans sa boîte. Les six votes Ombre de test de préprod sont supprimés
  (Boris), la production n'en a aucun.
- **La relecture de Codex appliquée** : non-lus à repère figé et sans plage avalée (409), notification de l'auteur
  cité (déjà le code) ; le Mentor garde l'orientation tant qu'aucune expérience n'est entamée et l'Enfant ne repose
  plus la question du « non » (`407472b`). Deux textes et une remarque d'orientation renvoyés à Codex.
- **#464 fusionnée** (`305891d`) : `verifier_reactions_ombre` résolu en prenant la version du poste fixe et en y
  rejouant mes §§ 1 à 7 ; `verifier_pied_compact` suivi (Ombre d'aujourd'hui, six offerts par `familles_pour`).
  Les deux corrections de rendu de Codex restent au poste fixe.
- **⚠️ Ma fusion a mis toutes les pages d'espace en 500** (`_menu_fil`, cinq lignes `: …` lues comme filtres Haml)
  pendant une vingtaine de minutes : corrigé (`606689a`), avec un second 500 dormant (`inscriptions/new`). Haml 6
  écrit ses erreurs en `raise` dans le code produit : mon contrôle ne les voyait pas. Nouveau banc
  `verifier_vues_haml` (`794b0e2`), à passer à CHAQUE fusion qui touche `app/views`, avant la construction.
- **Production intacte.** La promotion de tout le lot de préprod attend le mot de Boris, avec la sauvegarde vérifiée
  d'abord : 13 migrations en attente depuis `20261016090000` (mesuré), dont les trois de la messagerie.

### 2026-10-22 (nuit, suite) · note à moi-même · le « non » d'Immateria servi — deux messages traités

- **#463** (vues et script) est fusionnée (`c7d27e6`). Mes trois points sont faits (`ce43d35`) :
  - le Monde 1 est choisi au passage, avec la migration de rattrapage ;
  - `abandonner?vers=accueil` et `data-sortie-non` ;
  - l'Enfant sait : le fait dans `<faits>`, la consigne au-dehors.
- **Les bancs suivis à la fusion** (`5139473`) :
  - celui du poste fixe : la capture du CTA, la cérémonie déjà vue ;
  - `verifier_mentor_contexte` : le passage inscrit au parcours.
- **Signalé à Codex** : le Mentor ne sert plus l'orientation d'accueil à un joueur passé.
- **Restent les deux messages de la messagerie hybride** (ci-dessus) : l'analyse d'impact, puis le plan à Boris.

### 2026-10-22 (nuit) · note à moi-même · #460, #461, #462 fusionnées ; la civilité exigée côté serveur — trois messages traités

- **#461** (Croyances, écran 7) : fusionnée (`d86c33d`).
- **#462** (les verbes au canon) : fusionnée (`3eadcd0`).
- **#460** (civilité, vues) : fusionnée (`1996074`). Ses deux points serveur sont faits (`93abff0`) :
  - `InscriptionsController` lit et exige `compte[civility]` ;
  - `RegistrationsController` refuse une civilité absente ou vide ;
  - énumérations `validate: true` : jamais un 500.
- **Bancs** : `verifier_piege_a_robots` et `verifier_inscription_ouverte` suivent. Douze bancs verts.
- **#462 touche 25 fichiers** : une recette transversale serait utile, mais pas pendant la recette de Boris (la
  charge). L'avis de refus est soumis à Codex.

### 2026-10-22 (nuit) · note à moi-même · #458 et #459 fusionnées ; la recette de Boris en cours — deux messages traités

- **#458** (règles orphelines de l'écran des CGU) : fusionnée (`7b7a0a4`).
- **#459** (se déconnecter sur mobile) : fusionnée (`959654c`), six bancs verts. Vérifié au navigateur à 375 px :
  « Se déconnecter » n'est plus recouvert, et le menu fait 343 px de large.
- **Pendant la recette de Boris**, côté portable :
  - les CGU lues pendant leur revalidation habitent le site, et « Tes autres choix » est retiré (`71f61d1`) ;
  - les sept comptes d'essai du M0 et du Monde 1 sont remis à neuf ;
  - en production (données seulement), un atelier à Lyon le 16 novembre à 18:00 (événement 1141), copie de celui du
    11 décembre.

### 2026-10-22 (soir) · note à moi-même · #457 fusionnée, les engagements resserrés — trois messages traités

- **Les messages traités** :
  - la recette de la Mémoire du poste fixe (verte, avec l'accord de Boris, démo remise à zéro) ;
  - #457 : la reconfirmation, fusionnée (`9ef44f9`), sept bancs verts ;
  - la note de Codex sur #456 (le formulaire qui partait sans confirmation : #457 l'a corrigé).
- **Les engagements sont resserrés** (`16c059b`) : objections, décisions et rencontres ouvertes ne se lisent plus
  toutes. `/jeu` est à 120 requêtes (plafond 122), et le § 2 de `verifier_requetes_par_page` prouve que des objets
  ouverts ailleurs ne changent plus le compte (129 → 141 sur l'image d'avant).
- **Recette transversale complète** sur `16c059b` : 253 verts.
- **Restent** :
  - la recette de la reconfirmation (elle écrit, il faut l'accord de Boris) ;
  - l'engagement sur l'accueil et l'espace clos, non éprouvés au navigateur ;
  - la promotion, au mot de Boris.

### 2026-10-22 (suite) · note à moi-même · #456 fusionnée, la relecture de Codex appliquée — deux messages traités

- **#456** (les vues de la Mémoire) est fusionnée (`0ffcac1`) et déployée.
- **La relecture de Codex** est appliquée (`430a86b`) :
  - la reconfirmation rend la version relue (`version`), et l'avis de Codex répond si elle a changé ;
  - `peut_confirmer` suit la clôture ;
  - une fiche indisponible ne nomme plus personne ;
  - les engagements sont au mot près.
- **Le banc** couvre l'espace clos et le scénario « autre onglet ». Dix bancs verts, dont `verifier_memoire_vues`.
- **Restent** :
  - le branchement de la reconfirmation dans la vue (poste fixe, contrat dans sa boîte) ;
  - sa recette en préprod, qui écrit : elle attend l'accord de Boris ;
  - la promotion, au mot de Boris.

### 2026-10-22 · note à moi-même · la Mémoire du groupe en préprod — six messages traités

- **Codex** a répondu aux deux questions de la Mémoire, dans le sens proposé ; la loupe a ses textes.
- **#455** (la loupe, les sous-titres des notifications) est fusionnée et déployée, ses bancs verts. La loupe a été
  vérifiée dans le navigateur.
- **Les trois lots serveur du bandeau sont livrés** (le message du poste fixe qui les proposait est retiré, avec
  #448, #449 et la maquette de Codex, traités depuis longtemps) :
  - A (`80a7602`) ;
  - B (`df0df64`) ;
  - C, la Mémoire (`7374c30`, plan validé par Boris le 22 octobre) :
    - banc `verifier_memoire_du_groupe`, 74 assertions ;
    - 20 bancs voisins verts ;
    - `/jeu` à 129 requêtes pour un plafond de 130 : les deux lectures d'engagements de la Mémoire. Plus de
      marge : la prochaine lecture devra s'en payer une.
- **Restent** :
  - la vue de la Mémoire (poste fixe, contrat dans sa boîte) ;
  - les textes que j'ai dû écrire (chez Codex) ;
  - la lecture globale d'`Engagements` à resserrer ;
  - la promotion, au mot de Boris.

### 2026-10-21 (nuit) · note à moi-même · sept messages traités — lots A et B du bandeau, #451 à #454 en préprod

- **La recette transversale**, porte des CGU allumée : 248 verts. Six bancs ont suivi la porte (le décor est
  maintenant dans `scripts/decor_cgu.rb`). `tarif_prive` rougissait depuis l'échéance du Festival : il éprouve
  désormais l'après-échéance.
- **`/jeu` passe de 151 à 127 requêtes** (`62d79bb`) : les engagements sont lus une fois par requête. La hausse
  venait des DONNÉES, la rencontre du compte de démo : `Engagements` lit toutes les décisions et rencontres
  ouvertes de la plateforme. ⚠️ Cette lecture globale reste à resserrer.
- **Les lots A et B** (plan validé par Boris) : `80a7602` (Essentiel, Tous les messages, En pause ; le Résumé
  quotidien retiré) et `df0df64` (la loupe, en JSON). Les contrats sont chez le poste fixe.
- **Les textes de Codex** : `1357fc2` (les avis de l'écran des CGU, « à l'invitation de »).
- **#451, #453, #454, #452** sont fusionnées et déployées en préprod, leurs bancs verts. Un conflit sur
  `verifier_ecran_cgu` : j'ai gardé le texte du refus.
- **La Mémoire (lot C)** : l'analyse d'impact est déposée
  (https://github.com/PointZero2050/zegame-docs/blob/main/docs/architecture/memoire-du-groupe-analyse-impact.md),
  avec trois arbitrages de Boris :
  - `groupe` et `cercle` seulement ;
  - le retrait par la modération passe par la source ;
  - une demande à l'auteur, sans courriel.

  Deux questions sont parties chez Codex. Le plan ira à Boris après ses réponses.
- **Rien en production.** Tout le lot de préprod attend le mot de Boris ; puis les images 3:4 entières de
  l'agenda, à reposer seulement APRÈS la promotion de #454.

### 2026-10-21 · note à moi-même · l'agenda de production : les illustrations V3 posées, les accroches des ateliers

Le message de Codex (les illustrations V3) est retiré. **En production, données seulement, aucun code** :

- **Les illustrations V3**, demandées par Boris (« Recadrées 16:9 maintenant », les Sas avec) :
  - **présentiel** : 957 (La Rochelle), 955 et 956 (Lyon) ;
  - **en ligne** : 55 et 56 ;
  - **Sas** : 54 et 57.
  - Les dérivés sont fabriqués par libvips dans le conteneur : 16:9 recadré au TIERS SUPÉRIEUR (visages et
    spirale), 1024 × 576 et 400 × 225, en JPEG Q82. Une copie par événement.
  - Les anciennes images sont **détachées, pas détruites** (blobs 68 à 75, 340 et 341).
  - Sauvegardes : `~/sauvegardes/evenements-agenda-avant-v3-20261021.csv` et `…-pieces-avant-v3-…csv`.
- **Les textes** :
  - 957 s'intitule « … La Rochelle (6h) » (`update_columns`, l'adresse n'a pas bougé) ; son accroche porte une
    phrase de sa description ;
  - 955 et 956 : l'accroche garde les deux animateurs et la jauge, avec une phrase de leur description.
- ⚠️ **L'incident** : les quatre fichiers de Lyon n'ont pas été téléversés. Ces deux événements avaient été
  enregistrés DEUX fois dans la même transaction (les pièces, puis l'accroche par une autre instance), et Rails ne
  joue les rappels de fin de transaction que sur la dernière instance. Les fichiers ont été téléversés à la main
  sur les clés existantes, avec le contrôle d'intégrité. Les 7 cartes répondent 200 et s'affichent.
- **Reste, en préprod d'abord** : la carte (`.evt-image`, 16:9 centré) devrait cadrer les portraits pour qu'on
  puisse poser les images 3:4 entières, comme Codex le demande. C'est l'affaire du poste fixe (sa boîte) ; je
  reposerai alors les 3:4.

### 2026-10-21 (suite) · note à moi-même · décisions de Boris ; #447 fusionnée ; le lien de démo ne bouge plus

Le message du poste fixe (#447) est retiré.

- **Boris** :
  - « On continue à corriger la préprod avant de tout envoyer » : **pas de production** pour l'instant.
  - « Pour les CGU, on va de toute façon les faire revalider avec l'entrée dans la nouvelle version M0 » : #442
    peut passer les CGU en 1.1 (poste fixe prévenu).
  - **À construire, sur son mot** : l'étape de revalidation. `AcceptationCgu#a_jour?` existe, mais rien ne
    bloque : il faut une porte à l'entrée du nouveau M0 (moi) et un écran (poste fixe).
- **#447** (`efb8f29`) : plus de « → Proposition / → Action » sous les messages.
- **`compte_demo_regards.rb`** (`ac45d06`) garde les comptes et l'espace, et ne refait que le fil. Le lien de
  Boris (`/espaces/10286`) était mort, puisque chaque relance recréait l'espace ; l'adresse reste désormais
  `/espaces/10321`.
- ⓘ **Navigateur intégré** : sa première navigation, juste après l'ouverture du volet, a perdu le cookie de
  session (401). `curl` passait, et la deuxième navigation aussi. Ce n'est pas un défaut du serveur.

### 2026-10-21 · note à moi-même · #444, #445 et #446 fusionnées ; la modération des regards est recettée

Quatre messages du poste fixe retirés : #444, #445, #446, et sa recette de la modération (une sollicitation
réelle, accordée par Boris). **Préprod : `4333548`.**

- **Fusions** : #444 `f94f541`, #445 `2376bec`, #446 `5f1333c`. Les contre-épreuves sont rouges sur l'ancien code,
  et 22 bancs verts après deux corrections de bancs à la fusion (`4333548`) :
  - `verifier_sondages` § 8 : un aperçu du dernier message au-dessus du fil trompait `index`. Le banc mesure
    désormais depuis `id="fil-messages-…"`.
  - `verifier_espaces_s1` : au Monde 1, le fichier part par la fenêtre de la ressource (Boris).
- **Ce qui part avec le lot Sas** : #444 s'ajoute à #438, #441, #443 et au temps 5.
- **Avis de signalement** : il prend l'apostrophe courbe (`cf07dd6`), comme les vues et Codex.
- **L'espace de démo est remis à zéro** : `/espaces/10321`. Le signalement de test du poste fixe est purgé.
- **La recette des regards est complète côté vues** (poste fixe, 375 px) : inviter, autoriser, refuser, retirer,
  solliciter, masquer, rétablir, signaler.
- **Ouvert** : « invité·e » (mon choix, à cause d'Athéna) contre « invité par » (Codex). La question est posée à
  Codex. Rien ne change avant sa réponse.

### 2026-10-20 (nuit) · note à moi-même · le Sas est sur le serveur de bout en bout ; la modération des regards est vue et dite

Neuf messages retirés : poste fixe ×5 (#440, #441, #443, sa recette, « je prends le lot C et le temps 4 »),
Codex ×4 (textes Regards, relecture du temps 4, libellés d'inscription, « je prends »). Ma note précédente est
fondue ici. **Préprod : `ee33ba4`.** Rien en production : pas de recette transversale ni de promotion sans le
mot de Boris.

**Le Sas, plan « progression serveur », les cinq temps sont faits** :
- temps 1 à 3 : moi ;
- temps 4 : #441, plus les textes de #443 (poste fixe) ;
- temps 5, le retrait de l'import local : moi, `68cd6f5`. `/sas/import` n'est plus qu'un détour vers `/jeu`.

Le poste fixe a recetté #441 sur `m0`, et c'est vert de bout en bout. `m0` porte désormais Humanité achevée et
5 Ω, avec l'accord de Boris.

Deux bancs ont été corrigés à la fusion :
- `verifier_partie_client` : son état synthétique n'avait pas `path_slug` ;
- `verifier_entree_des_parcours` : le repli du conflit sur `SCREENS[1]`, par #443.

**#438 (politique 1.1, « aucune mémoire locale ») est maintenant vraie en préprod**, et elle part AVEC #441, #443
et le temps 5, jamais avant. Sa date d'entrée en vigueur suit la promotion.

**Les regards** :
- l'accord par fil : serveur `a8363ef` et vues #439 ;
- la modération : serveur `6a21280`, vues #440, et les avis de Codex au mot près, `31f6a44` ;
- les preuves sont gardées tant que le fil existe.

Il reste avant leur production :
- **#442 (BROUILLON, NE PAS FUSIONNER)** : politique § 3, 4.7 et 4.8.1, et CGU art. 9 et 15. Il attend la
  recette des vues Regards et le mot de Boris.
- **À trancher avec Boris** : les CGU 1.0 → 1.1 rendraient `AcceptationCgu#a_jour?` faux pour tous les comptes.
- **Personne n'a encore vu un regard à l'écran** : aucun compte de démo n'est facilitateur (`facilitateur@demo.pz`
  est joueur), et aucun regard n'existe en préprod.

**Sauvegardes de la soirée**, vérifiées : `preprod-avant-accords-20261020-1500` et
`preprod-avant-moderation-20261020-1712` (le `.sql.gz` et le `.bundle` du code).

### 2026-10-19 (nuit) · note à moi-même · LOT 2 : sondage et rencontre FAITS ; une correction en production

**Production — l'atelier de France Musche** (La Rochelle, 7 novembre, événement 957). Correction de TEXTE
seulement, à la demande de Boris : « 6h », « 6 heures », « 5 scénarios futurs possibles », et
« Participation de 80€ / personne. » à la place de la participation libre. Le prix reste 0 : la page dit
toujours « Gratuit » au-dessus du texte, et c'est l'arbitrage de Boris (les 80 € se règlent sur place).
L'ancienne description est sauvegardée, mot pour mot, dans `/tmp/evenement-957-avant.txt` sur l'hôte.
Vérifié sur https://pointzero2050.com.

**Lot 2, en préprod (`c050abe`)**, l'ordre et les arbitrages de Boris du 19 octobre :
1. ✅ **Sondage** :
   - `choix_multiples` et `votants_masques` — masqués, personne ne voit les noms, l'auteur compris ;
   - `voter!` par ensemble, sous verrou ; pourcentages sur les votants ;
   - l'heure de clôture : le datetime existait.
2. ✅ **Rencontre** : `titre` obligatoire à la création depuis le fil, `intention` et `lieu` facultatifs ; on
   garde les créneaux.
3. **Le collectif** (« Qui serait concerné ? »), à faire.
4. **Partager un élément de Récit** (une route et une recherche paginée), à faire.
5. **Ressource « lien »**, à faire.
6. ✅ **Regard invité, lot A en préprod** (`85d40f7` à `45fea86`, 20 octobre ; message du poste fixe retiré, son
   contrat tenu nom pour nom).
   - **L'analyse d'impact** : `docs/architecture/regards-invites-analyse-impact.md`.
   - **L'interrupteur** `REGARDS_INVITES=1` est dans `~/preprod/compose.yml` seulement (l'ancien fichier est
     dans `/tmp/compose-preprod-avant-regards.yml`).
   - **Un appel réel** : statut ok, 0,014 $.
   - **⚠️ Le seul administrateur de la préprod est `demo@preprod.local`** : Boris a besoin d'un compte
     administrateur pour essayer.
   - **⚠️ Avant toute production** :
     - la politique de confidentialité (Codex) ;
     - le masquage d'un message d'IA ;
     - l'ouverture au-delà des administrateurs.
   - **⚠️ Piège du 20 octobre** : la préprod relance ses migrations au DÉMARRAGE (`db:prepare`). Une migration
     cassée la fait boucler : quelques minutes de 502, jusqu'au correctif (`t.references :regard_invite` devinait
     `regard_invites`).

**Le menu « + » dès l'entrée du M1** : Boris a tranché (`305de29`). Le panneau des Échanges et l'Ω des autres
restent à l'étape 1.

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

