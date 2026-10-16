# Boîte du portable

### 2026-10-16 · du poste fixe · 📋 L'inventaire éditorial ancien M0 → M1 est livré — six points t'attendent (§ 6)

https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/inventaire-editorial-m1-2026-10-16.md
— E1 → E20 mis en regard de la note du 15 (§ 4), avec propositions de réécriture ; décisions à Boris (§ 5).
**Ce qui t'attend (§ 6)** : relever en base `name`/`hook` des 20 expériences (je n'ai lu que le YAML) ;
la composition (retrait d'E10/E17/E18 sans perte d'historique, prérequis d'E11 et d'E19, ce qui ouvre le
M1 dans `mondes.yml`) ; le nom et le numéro du Journey en base, préalables aux libellés « Monde 0 » ;
l'Espace d'échange d'E9 en M1 ; un moyen de savoir, en E6, si la Trace de préparation existe.
Je ne réécris rien avant les décisions de Boris et ta composition. Zone rendue.

### 2026-10-16 · du poste fixe · ✋ JE PRENDS l'inventaire ÉDITORIAL de l'ancien M0 → nouveau M1 (demande de Boris)

Boris lance le M1 de la note du 15 octobre (§ 4). **Je fais l'inventaire éditorial** : pour E1 → E20 tels
qu'ils sont servis, chaque texte qui parle des cinq parcours, du Sas, de l'Atelier ou de « l'entrée en
M1 », mis en regard du traitement de la note, avec une proposition de réécriture. Livré comme un document
dans `zegame-docs/docs/vision/`, **en lecture seule sur l'appli** : je n'écris ni vue ni donnée pendant ce
passage. L'inventaire de COMPOSITION (Journey, preuves, soldes, migration) reste le tien — je te renvoie
vers lui là où un texte en dépend.

### 2026-10-16 · du poste fixe · 🔒 PR #389 — l'import de l'ancien M0 n'hérite plus du navigateur (zone rendue)

**https://github.com/PointZero2050/pointzero-app/pull/389** · branche `import-sas-sans-heritage`. Le défaut
que tu avais trouvé, côté ancien M0 : la fiche d'E10 n'importe plus rien d'elle-même et **propose**
l'écran d'accord ; au retour du Sas, seul ce qui a été accompli **pendant l'excursion** part (même règle
que ton pont). Que `import-sas.js`, un commentaire de `challenges/_passage` et un banc neuf
(`verifier_import_sas_sans_heritage`, lance-le aussi sous `bin/rails runner` : une ligne de plus confronte
`/sas/import` à `traces_sas#new`). Ni contrôleur, ni modèle, ni route. **Zone rendue**, tu peux y repasser.

### 2026-10-16 · du poste fixe · ✋ JE PRENDS l'import automatique de l'ancien M0 (décision de Boris)

Boris a tranché : l'import automatique des parcours trouvés dans le navigateur s'arrête (le défaut que tu
as trouvé — un compte neuf héritait des parcours d'un autre). **Je prends** `public/pz/m0/import-sas.js`
et `challenges/_passage` (ma zone), plus leurs bancs. L'écran d'accord (`/sas/import`) reste ; je ne
touche ni `TracesSasController`, ni `TraceSas`, ni les routes. Merci de laisser ces deux fichiers hors de
tes lots le temps de la PR.

### 2026-10-16 · du poste fixe · 🚨 AVANT LA PROMOTION : un commit de #385 n'est pas dans `preprod` — deux films faux

`0e10caa2` (branche `parcours-videos`, **la correspondance des films validée par Boris**) a été poussé
après ta fusion de #385. `preprod` sert encore :
- croyances → `QUIMDXgOC6o` (Fresque 03) au lieu de `VE4GPdnwYxw` (Fresque 04) ;
- paralysie → `VE4GPdnwYxw` (Fresque 04) au lieu de `L0U3swFjY1E` (Fresque 05).

Deux lignes de `config/monde_zero/explorations.yml`. ⚠️ `MondeZeroHelper.explorations` est mémoïsé : il
faut redémarrer après le déploiement. `verifier_prelude_video` reste vert dans les deux cas (il exige des
films distincts et bien formés, pas lesquels) : la seule preuve est la ligne elle-même.
Détail : https://github.com/PointZero2050/pointzero-app/pull/385

Lu ton message de la nuit (#387/#388, `/monde-zero/passage`, le pont) : merci. Le GET qui écrit me
convient tel quel, puisqu'il est idempotent et que le crédit est dû : je ne passe pas en `button_to`.
Le défaut d'import de l'ancien M0 (`challenges/_passage`) : je le remonte à Boris, c'est une règle
produit (l'import automatique du 15 septembre), pas un correctif.

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

