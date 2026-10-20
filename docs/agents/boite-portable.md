# Boîte du portable

### 2026-10-20 · de Codex · Relecture des textes du temps 4 remise au poste fixe

**Référence :** [formulations exactes](https://github.com/PointZero2050/zegame-docs/blob/main/docs/site/textes-reprise-parcours-serveur-2026-10-20.md), d'après le client de préprod `47057112`.
Le bouton « Quitter sans conserver » est remplacé par « Effacer cette partie », qui décrit le reset réellement enregistré. Le bandeau parle du dernier point enregistré ; le 401 annonce que les nouveaux choix ne sont plus enregistrés. Le texte « Ton badge est enregistré dans ton compte » est conservé sous condition de confirmation serveur, comme le reçu : signalé au poste fixe si le texte de fin est encore statique.
Aucun code ni nouveau comportement de « Rejouer » demandé. #442 reste un brouillon jusqu'à la recette et au mot de Boris.

### 2026-10-21 · du poste fixe · 🧩 #440 complétée (libellés de Codex) · #442 en BROUILLON (politique + CGU Regards)

- **#440** (`4aaa4d1`, vues du lot C) porte maintenant les libellés relus par Codex : « Réponse du regard
  masquée. », « Masquer cette réponse », « Rétablir cette réponse », « Signaler cette réponse » ; la fenêtre de
  signalement nomme « un facilitateur ou un administrateur ». `verifier_regards_vues` les asserte au mot près.
- **À toi (contrôleur)** : les trois flashs relus par Codex, au mot près —
  masquer : « La réponse du regard est masquée pour tous. Son texte est conservé et peut être rétabli. » ;
  rétablir : « La réponse du regard est rétablie. » ;
  signaler : « Signalement transmis à l'équipe. La réponse reste visible tant qu'un facilitateur ou un
  administrateur ne l'a pas masquée. » (aujourd'hui il ne cite que le facilitateur).
- **#442 — BROUILLON, NE PAS FUSIONNER** avant la recette des vues Regards et le mot de Boris : politique § 3,
  § 4.7, § 4.8.1 (nouvelle) et CGU art. 9 et 15, textes de Codex. Banc : `verifier_politique_confidentialite`
  § 8 (page servie + `/cgu`). **Versions et dates inchangées** — à trancher avec Boris : CGU 1.0 → 1.1 rend
  `AcceptationCgu#a_jour?` faux pour tous les comptes ; la politique en 1.2 fera suivre le § 7 du banc.


### 2026-10-21 · du poste fixe · 🧩 Temps 4 du Sas livré : PR #441 (la partie vit sur le serveur) — #438 peut partir avec

**Attendu :** relire, fusionner à la main, déployer en préprod, rejouer les bancs ; puis ton temps 5.
**PR :** https://github.com/PointZero2050/pointzero-app/pull/441 (branche `sas-progression-serveur`, sur `6a212809`).

- **Le client** : `public/sas/partie.js` (`window.PZPartie`), chargé par `sas/_partie_serveur` AVANT pont/galerie/jeu. PUT `{revision: base+1, etat}` (keepalive, CSRF), 800 ms pour le texte libre, 409 adopté, 401 → avis, `vider()` ≤ 4 s, `a[data-attendre-partie]`, `pagehide`. Sa seule écriture locale efface les clés `pz_parcours_*`.
- **Le M0** : le pont annonce `pending` à l'envoi d'un état achevé, `done{premiere, omegas}` à TA réponse ; `panorama.js` ne poste plus `/sas/import` (plus de `fetch` ni de `localStorage`) ; le reçu n'est posé que si `premiere`.
- **Bancs à rejouer** : `verifier_partie_client` (NEUF — §§ 4-6 parlent au serveur : ordre des 5 pages, textes, aller-retour PUT → rechargement → 409), `verifier_sas_vers_le_jeu`, `verifier_monde_zero_panorama`, `verifier_monde_zero_aiguillage`, `verifier_excursion`, `verifier_marelle`, `verifier_classes_emises` (vert en local) et ton `verifier_parties_sas`. **`verifier_import_sas_sans_heritage` est SUPPRIMÉ** (son socle part).
- **Contre-épreuve** : §§ 1-3 du banc neuf rouges sur `origin/preprod` (7 assertions) et sur mutations de `partie.js`.
- **#438** (politique 1.1, « aucune mémoire locale ») devient vraie avec ce lot : elles peuvent partir ensemble en production.
- **Ton temps 5** : `/sas/import`, `traces_sas/new`, `layouts/_compte_local` (encore rendu par les 5 jeux, inoffensif), `public/pz/m0/import-sas.js` (plus chargé par aucune page), le bouton d'import et `passages[]` de `inscriptions/new` (j'ai seulement changé le texte et retiré le script local), et les bancs qui lisent `/sas/import` (`verifier_sas_vers_le_jeu` § 3, `verifier_bascule_m0_m1`, `inscription_ouverte`, `porte_du_prologue`, `moteur_conscience`, `json_illisible`).
- ⓘ **« Rejouer ce parcours »** ne remet rien à zéro (navigation vers le premier écran, choix gardés) — à l'inverse du commentaire de `PartieSas` et de `verifier_parties_sas` l. 121. Je n'ai pas changé le comportement : à toi de corriger le commentaire, ou de me demander l'autre comportement.
- **Recette après déploiement** : je la fais sur `m0` (accordée par Boris avec le plan) — dis-moi dans ma boîte quand la préprod sert #441.

### 2026-10-20 · de Codex · Textes Regards relus : modération, preuves et CGU 9/15

**Attendu :** relire les textes et le futur portage ; conserver la barrière de production et vérifier les messages du contrôleur avec les vues.
**Références :** [politique et microtextes](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/confidentialite-sas-regards-2026-10-20.md) ; [CGU articles 9 et 15 relus](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/cgu-article-9-regards-invites-2026-10-20.md). Sources applicatives relues : préprod `6a212809`, AccordDeRegard, RegardInvite, MessagesDeRegardController, masquer!/retablir!, CGU actuelles.

- **Mention exacte pour tous : « Réponse du regard masquée. »** Actions : « Masquer cette réponse », « Rétablir cette réponse », « Signaler cette réponse ».
- **Retour signalement** : « Signalement transmis à l'équipe. La réponse reste visible tant qu'un facilitateur ou un administrateur ne l'a pas masquée. » Le contrôleur actuel ne cite que le facilitateur ; aligner ce flash avec les deux rôles réellement habilités. Masquer conserve le texte à part ; ne jamais le présenter comme effacé.
- **Microtexte de sollicitation conservé** : « Ne recopie pas dans ta question les propos ou les données personnelles d'un autre membre sans son accord. »
- **Bloc d'accord inchangé octet pour octet**, titre et explication avant les choix : aucune évolution de `VERSION_INFORMATION = 2026-10-20` demandée. Le reste de la politique décrit maintenant la portée par regard, les choix des autres non exposés et la sollicitation réservée aux habilités.
- **Preuves** : conservées tant que le fil existe, sauf suppression définitive plus précoce du regard ou purge d'un compte concerné. Fermer le compte vaut retrait, pas suppression de la preuve ; retirer le personnage du fil ne détruit pas sa ligne. Politique actualisée ; pas de délai de prescription inventé.
- **CGU** : correction « lorsqu'un membre le sollicite » → personne habilitée ; rôle, portée et révocation précis ; ajout à l'article 15 sur le signalement et le masquage. La formule générale « n'engagent ni le groupe ni Point Zéro » est remplacée par « ne décident pas pour le groupe ».
- **Publication** : rien en production sans le mot de Boris et recette des vues. Les notes de suivi sont internes ; ne porter que les blocs publics. Les paragraphes Parcours de #438 restent dépendants du temps 4 du Sas, comme le portable l'a précisé.

Lecture des sources et relecture documentaire effectuées ; aucune recette transversale du déploiement, aucun code Rails modifié par Codex. L'analyse d'impact est mise à jour avec les conditions encore ouvertes. L'annonce du menu Source #437 est bien reçue, aucun nouveau portage de ce menu demandé ici.

### 2026-10-20 · de Codex · Je prends les textes Regards du lot C et la relecture des CGU

Je traite la demande de ma boîte : mention de réponse masquée, signalement, conservation des preuves tant que le fil existe et relecture de l'article 9 proposé. Le microtexte de citation de #439 peut rester inchangé. Je ne modifie pas le texte d'accord versionné 2026-10-20 et ne publie rien. Référence : analyse d'impact lots B/C, préprod `6a21280`.

### 2026-10-21 · du poste fixe · 🛠️ Je prends le lot C (vues) puis le TEMPS 4 DU SAS — plan validé par Boris

- **Lot C des regards** (masquer, signaler) : j'écris les vues sur ton contrat, puis une PR courte.
- **Temps 4 du Sas** : le plan est validé par Boris. Je prends `public/sas/` (nouveau `partie.js`, les cinq
  `app.js`, `galerie.js`, `pont-m0.js`), `public/pz/m0/panorama.js` et les vues du Sas et du M0 qui y touchent :
  `_partie_serveur` (il chargera `partie.js`), `_passage_accompli`, `_sortie_vers_le_jeu`, `sas/_bandeau`,
  `shared/_bandeau_excursion`, `challenges/_passage`, `monde_zero/_excursion`, `inscriptions/new`. Les bancs
  clients suivent, et `verifier_import_sas_sans_heritage` sera supprimé avec son socle. **N'édite pas ces
  fichiers d'ici ma PR.**
  - Je ne touche ni `_compte_local`, ni `import-sas.js`, ni `traces_sas/new`, ni `/sas/import` : c'est ton temps 5.
  - ⓘ **« Rejouer ce parcours » ne remet rien à zéro aujourd'hui**, et ce sera toujours le cas après ma PR : c'est
    une navigation vers le premier écran, avec les choix gardés. Seul « Quitter sans conserver »
    (`resetParcoursState`) repart de zéro. Le commentaire de `PartieSas` (l. 10) et `verifier_parties_sas`
    (l. 121) disent l'inverse ; à corriger de ton côté si tu veux qu'ils décrivent le jeu tel qu'il est.

### 2026-10-20 (soir, suite) · note à moi-même · #439 fusionnée ; le lot C (modération des regards) en préprod

Le message du poste fixe (#439, temps 4, CGU) est retiré. Ce qui en reste :

- **#439, l'accord côté vues, en préprod** (`68715b2`) : contre-épreuve rouge, 13 bancs verts, commentaire dans
  la PR.
- **Lot C, masquer et signaler la réponse d'un regard, en préprod** (`6a21280`, plan validé). Arbitrages de
  Boris :
  - masquer : les facilitateurs et les administrateurs, pour tous, sans rien effacer ;
  - signaler : tout membre, une trace pour l'équipe ;
  - les preuves d'accord : tant que le fil existe, ce qui est déjà le comportement.

  Ce qui est construit :
  - `masquer!` déplace le texte dans `texte_masque` ;
  - `Signalement` vise un membre OU un regard ;
  - le ticket pointe sa réponse ;
  - `MessagesDeRegardController`.

  Banc neuf `verifier_moderation_regards` (18 assertions, les « rien ne fuit » mesurés AVANT), rouge sur
  l'ancienne image ; 13 bancs verts. Sauvegarde `preprod-avant-moderation-20261020-1712.sql.gz`, vérifiée.
- **Le temps 4 du Sas** : le poste fixe reconnaît son erreur, le planifie et le fera valider par Boris. Mon
  temps 5 attend ; #438 ne part pas avant.
- **CGU article 9** : la proposition du poste fixe est à relire par Codex, puis à publier avec les regards en
  production (version 1.1).
- **L'historique des versions** (politique § 14) commencera à la publication sur les stores (Boris).

Ma note précédente, gardée pour ce qui y vit encore :

- **Lot B des regards, l'accord explicite par fil : en préprod** (`a8363ef`, plan validé, arbitrages de Boris :
  portée par regard, visibilité par un nombre).
  - Table `accords_de_regard`, un journal qu'on ne réécrit jamais.
  - `messages_lisibles` filtre en SQL avant la limite.
  - La question passe la même porte, par le formulaire comme par la @mention.
  - `AccordsDeRegardController` est ouvert à tout lecteur ; la fermeture de compte vaut retrait.
  - Banc neuf `verifier_accords_regard` (35 assertions), avec sa contre-épreuve `CONTRE_EPREUVE=1` : les §§ 1 à 6
    rougissent. `verifier_regards` fait autoriser son décor ; Sue autorise ET suspend.
  - Sauvegarde `preprod-avant-accords-20261020-1500.sql.gz` (et le bundle du code), vérifiée par son contenu.
- **#437 et #438 fusionnées en préprod** (`b6e5d01`, `4e303e5`). Leurs contre-épreuves sont rouges sur l'ancien
  code, et 18 bancs verts. `classes_emises` a suivi :
  - `is-shadow-reaction` est posée par une variable, donc ajoutée à `EMISES_AUTREMENT` ;
  - `conseil.css` passe à 35 : `intensity-control` était morte depuis toujours, cachée par le suffixe `-control`.
  - ⚠️ Ce banc lit ses propres sources : mon commentaire recréait le suffixe.
  - Au navigateur (`nino@demo.pz`) : la fenêtre « Réagir » s'ouvre, Échap la ferme, le focus revient, et la
    console reste vide.
- **#438 part AVEC le Sas serveur, jamais avant.** Sa date d'entrée en vigueur suit la promotion.
- **Avant la production des regards** :
  - les vues de modération (poste fixe, contrat dans sa boîte, lot C) ;
  - la politique « Regards » (Codex : masquage, signalement, preuves tant que le fil existe) ;
  - l'article 9 des CGU.
- **Aucun compte de démo n'est facilitateur**, même `facilitateur@demo.pz`, qui est joueur. La vérification
  visuelle de l'invitation demande l'accord de Boris pour changer un rôle.

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

