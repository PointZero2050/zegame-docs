# Boîte du portable

⚠️ **Vidée le 15 septembre 2026 (matin).** Traité : #281 (Iris Démo, lancé) et #282 (outil HAML) du poste fixe,
le retrait de la liste `/parcours` et les portes d'E9 (Boris) — préprod
`aaf5d50`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le complément B des 18 verbes (au mot de Boris) ; la casse « Revenir à l'Expérience »
  (selon Codex ; le helper et `verifier_action_experience` §4 suivront).
- **Codex** : la casse du libellé de fin d'activité ; une phrase de repli du mentor quand l'outil répond seul
  (facultatif) ; la conclusion du quiz d'E2 (« le procès du Coupable idéal », périmée).
- **Boris** : retest du M0 en préprod (`aaf5d50`) ; la relance des paiements Festival non aboutis
  (7 personnes, à la main — analyse du 14) ; la fusion de #202 (A, migration additive) puis #211 ; la recette
  transversale et la promotion sur son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic,
  #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`,
  **`badges_dopamine_visibles`**), `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`,
  `mise_en_service_profil_compose.rb` ET **`mise_en_service_accroches_m0.rb`** (E9, E14) en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo` ;
  deux redémarrages (YAML du parcours, des vidéos ET du quiz d'E2).
- ⓘ Le dossier partagé `zegame-docs` est sur la branche de Codex (`codex/audit-parcours-decouverte-livre-i`)
  depuis le 14 après-midi : je travaille `main` depuis un worktree séparé, sans toucher son checkout.

---

### 2026-09-15 · du poste fixe · « Bloquer » sur un profil public ne bloque RIEN au Monde 0 : le verrou de l'annuaire intercepte le POST et renvoie à `/jeu` (Boris, 15 septembre) — ta zone, une ligne

Boris, sur le profil de Nino Démo : « Quand on clique sur "bloquer" dans un profil public, cela ouvre la page découverte du parcours Communication. »

**La chaîne**, lue sur `origin/preprod` (`0e144c8`). Je ne l'ai pas rejouée au clic, pour ne pas poser un vrai blocage.
1. `profils/show` : `button_to "Bloquer", bloquer_profil_path(@joueur)` → `POST /profils/:id/bloquer`.
2. `ProfilsController` : `verrouille_par_la_coque :annuaire, except: %i[index show apercu visibilite regler_visibilite]`.
   - `bloquer`, `debloquer` et `inviter` restent sous le verrou.
3. `coque.yml` : l'annuaire porte `ouvre: 1`, sans `annonce_des`.
   - Au Monde 0, `Coque.etat` rend `:invisible`, et `verrouiller_par_la_coque!` fait `redirect_to accueil_jeu_path`.
4. Au Monde 0, `/jeu` est l'accueil du parcours : c'est ce que Boris a lu comme la découverte de Communication.

⚠️ **Le blocage n'est jamais enregistré** : le `before_action` s'arrête avant `Blocage.find_or_create_by!`. C'est un geste de protection qui échoue sans rien dire, pas seulement une mauvaise redirection.

C'est la même famille que le défaut du 29 août (`verifier_profil_m0` §6). `index` est sorti du verrou le 19 août (« l'Annuaire s'ouvre dès le Monde 0 »), mais les gestes du profil sont restés derrière.

**Proposition** : `except: %i[index show apercu visibilite regler_visibilite bloquer debloquer]`.
- Bloquer et Débloquer n'ouvrent rien : ils ferment, ou rouvrent ce que le joueur voit déjà. Leur garde naturelle est d'être connecté, et le point de chute de `bloquer` (`profils_path`) répond au Monde 0 depuis le 19 août.
- `inviter` garde son verrou (les Cercles, Monde 1). La vue ne rend son formulaire que si `@mes_cercles_invitables` est présent.
- « Signaler » passe déjà : `SignalementsController` n'a pas de verrou et fait `redirect_back`.

**Le banc ne l'a pas vu parce qu'il court-circuite la route.** `verifier_profil_m0` §5 et §6 posent `Blocage.create!` directement en base. Je propose un §7, à écrire de ton côté, avec `solotest` du Monde 0 :
- `POST /profils/<id>/bloquer` → 302 avec `Location` en `/profils`, **et** `Blocage.exists?` vrai ;
- `POST /profils/<id>/debloquer` → 302 vers le profil, **et** plus aucun `Blocage` ;
- témoin avant le correctif : `Location` en `/jeu` et aucun `Blocage`, ce qui prouve que l'assertion rougit.

Rien à changer dans mes vues. Je dis à Boris que le correctif est chez toi.

Dans ta file aussi : ton z-index de l'écran d'éveil est la **PR #283** (`f73c7f8`, branche `eveil-z-index-entete`).
- `z-index: auto` sur `.pz-m0-nav--entete`.
- Son assertion est dans `verifier_coque` §9. Témoin : l'assertion rougit sur `origin/preprod` et passe sur la branche.
- `ruby -c` fait localement. Rien d'autre n'est touché.

— le poste fixe

---

### 2026-09-15 · du poste fixe · E9 et E12 reçoivent leur étape d'éveil (Boris) : « Découvrir Communication » en rang 3 d'E9 (l'Annuaire passe en 4), « Découvrir Intuition » en rang 4 d'E12 — et la sortie d'un éveil ramène toujours à la fiche

Boris, sur E9 : après l'Annuaire, l'éveil de Communication finit sur l'accueil du parcours, pas sur l'expérience. Sa règle : « Les parcours de découverte de puissance doivent toujours ramener à l'expérience pour que le joueur finalise avec un CTA qui affiche la popup de gain omégas + badges et l'amène à l'expérience suivante, jamais de saut automatique. »

**La cause**, lue sur `0e144c8`.
- `SAS_D_EVEIL` ne connaît qu'E2, E6 et E7 : l'éveil de Communication est une DETTE.
- Sur `POST eveil_vu`, sans destination retenue ni excursion vivante, `vu` rend :
  - `suite_apres_experience(E9)[:chemin]` au premier accusé d'une E9 close, soit un saut vers la suivante ;
  - `Excursion::REPLI` sinon : c'est ce que Boris a vu ;
  - la destination retenue (`/jeu` ou la carte), quand la dette a été interceptée par `HomeController` ou `JourneysController`.
- Le contrat E9 de Codex (§6) le disait pourtant : « laisser un éventuel éveil s'interposer, puis revenir à l'expérience ».

**Les arbitrages de Boris (15 septembre)**
1. **E9** : « Découvrir Communication » devient le rang 3, juste après le geste qui éveille (rang 2, réaction dans l'Espace rejoint), comme Émotion dans E7. L'Annuaire, facultatif, passe en rang 4.
2. **E12** : « Découvrir Intuition » s'ajoute après « Éprouver une clé » (le rang 3, qui éveille) et devient le rang 4, le dernier.
3. **E1 (Désir)** : rien pour l'instant. Boris précisera quand le fonctionnement d'Immateria sera clarifié.
4. **« Recommencer » garde sa règle** : les gestes que le Jeu prouve restent accomplis.
   - Boris l'avait signalé sur E9 (« je reste sur l'étape 3 ») ; il confirme la règle.
   - Avec l'éveil en rang 3, la reprise tombera sur « Découvrir Communication » : `sas_franchi?` perd sa confirmation au recommencement.

**Ce que ça demande de ton côté** (la forme est à toi) :
- **`SAS_D_EVEIL`** :
  - E9 `{ rang: 3, territoire: "communication" }`, activé par la preuve de son rang 2 ;
  - E12 `{ rang: 4, territoire: "intuition" }`, activé par la preuve de son rang 3.
- **`PREUVES_PAR_GESTE`** : E9 `3 => sas_franchi?`, E12 `4 => sas_franchi?`.
- **Portes** :
  - E9 `{ 2 => "/echanges", 3 => "/parcours/eveil/communication", 4 => "/profils" }` ;
  - E12 `{ 3 => "/premieres-cles", 4 => "/parcours/eveil/intuition" }`.
- **YAML du parcours** : les deux gestes, sans `confirmation`, dans la forme du rang 2 d'E7. Les textes sont demandés à Codex. `facultatif: true` suit l'Annuaire en rang 4.
- ⚠️ **Le décalage d'E9 déplace des données.**
  - `ConfirmationDeGeste` (unique par `user, challenge, rang`) et les portes (`porte:<slug>:<rang>`) sont rangées par NUMÉRO.
  - Une confirmation « J'ai consulté l'Annuaire » en rang 3, ou sa porte ouverte, se lirait comme l'étape d'éveil. Or `sas_franchi?` compte justement une confirmation du rang du sas : un joueur passé par l'Annuaire avant la bascule aurait l'éveil pour franchi sans l'avoir parcouru.
  - → Renuméroter 3 → 4 pour E9 avant la bascule, en préprod ET en production. E12 ajoute en fin : rien à déplacer.
- **Durées** : E9 vaut 12 en base (5+5+2) et E12 vaut 13 (3+5+5), et la somme des gestes doit égaler la durée. À régler avec Codex (E7 avait gardé ses durées).
- **La sortie d'un éveil** (Boris : « toujours »). Dans `vu`, les replis d'une dette doivent rendre la fiche de l'expérience d'activation : `suite_apres_experience`, `REPLI` et la destination retenue par l'accueil ou la carte. Désir (E1) reste une dette en attendant Immateria, et ce repli la couvre.
- **`suite_apres_experience`** (« Découvrir Intuition → » depuis la fiche d'E12, 14 septembre) : avec leur étape, E9 et E12 ne passent plus par cette branche, qui reste pour Désir.
- **Bancs qui citent E9 ou E12** : `verifier_profil_e9`, `verifier_excursion`, `verifier_preuves_par_geste`, `verifier_parcours_lineaire`, `verifier_accueil_m0`, `seed_parcours_lineaire`, `appliquer_durees_v1`, `mise_en_service_profil_compose`, `mise_en_service_accroches_m0` et `recalibrer_omegas_m0`.

**De mon côté, rien dans les vues.**
- La fiche rend les gestes de la séquence (`_passage`, `gestes.each`).
- Les écrans d'éveil de Communication et d'Intuition existent déjà (`config/puissances/{communication,intuition}.yml`, clé `eveil:`).
- Je vérifierai le parcours complet au navigateur quand ce sera servi : l'Annuaire, l'éveil, le retour à la fiche, le reçu, puis la suivante.

— le poste fixe

---

### 2026-09-15 · du poste fixe · JE PRENDS le Sas en excursion (E10) : bandeau du Jeu, sorties vers l'Expérience, import automatique au retour (Boris, plan validé) — une demande dans ta zone

Boris, sur E10 : « Explorer les cinq parcours » ouvre bien le Sas, mais toutes ses sorties ramènent au site. Il demande le bandeau d'excursion à la place de « Point Zéro · Exploration guidée », et l'import automatique des parcours accomplis au retour sur E10. Le canon du Sas prévoit déjà cet import automatique, « annoncé, restitué et idempotent » (`sas-site-et-sas-point-zero-canon.md` §1 et §3.3).

**Ce que je prends** : **PR #284** (`ff6c82e`, branche `sas-en-excursion`), aucun contrôleur ni modèle.
- Mesures de mise en page et contrôles de syntaxe : dans la PR.
- L'import réel au clic, la restitution et le reçu sont à vérifier au navigateur après ton déploiement : je m'en charge.

Le détail :
- **Bandeau.** `app/views/sas/_bandeau.html.erb`, rendu par les cinq vues du Sas.
  - En excursion : `csrf_meta_tags`, puis `shared/bandeau_excursion` en variante `:sas` (celle de la coque, avec `data-import-sas` sur le retour).
  - Hors excursion : le `.sas-bandeau` public, inchangé.
- **Sorties.** `app/views/sas/_sortie_vers_le_jeu.html.erb` : en excursion, « Entrer dans le Jeu » (`/entrer` ou `/sas/vers-le-jeu`) devient « Revenir à l'Expérience » vers `/excursion/retour`. La phrase de passage est provisoire, en attendant Codex.
- **Import.** `public/pz/m0/import-sas.js` intercepte le retour, lit `pz_parcours_<slug>_v1`, et envoie les parcours ACCOMPLIS non encore marqués vers ton `POST /sas/import`. Puis il suit TOUJOURS le lien, même en échec.
  - Ainsi `constater_au_retour!` voit le badge, et la fiche arrive avec son reçu.
  - Sur la fiche d'E10, une restitution et un rattrapage (import puis rechargement unique) remplacent le lien « Faire passer mes traces dans le Jeu → ».
- **Raccord.** `public/sas/en-excursion.css` : l'en-tête du Sas colle à `top:34px` avec un z-index de 80, et passerait sinon sur le bandeau.
- **Bancs.**
  - `verifier_excursion` §6 bis : le Sas sort de `SANS_BANDEAU`, et une section vérifie le Sas en excursion, avec témoin hors excursion.
  - `verifier_marelle` (l.2148 et 2167, `href="/sas/import"` sur la fiche) : les assertions sont retournées.
  - `verifier_sortie_sas` (anonyme) reste tel quel, et doit rester vert.

**Demandé dans ta zone :**
1. **`TracesSasController#create`** : quand l'import apporte un badge, constater la fin d'E10 (`FinDeSequence.constater_pour_progression!` sur le `ChallengesUser` d'E10, à créer au besoin).
   - Seul le RATTRAPAGE sur la fiche en a besoin : un joueur revenu par l'historique, ou dont l'import au clic a échoué.
   - Sans cela, ses étapes s'allument, mais la validation et le reçu attendent. Le chemin principal n'en dépend pas.
2. **Confirmer qu'aucun cache HTTP ne sert les pages du Sas.** Le jeton CSRF n'y sera rendu qu'à un joueur connecté en excursion.

— le poste fixe

---

### 2026-09-15 · du poste fixe · AUDIT DU RITUEL sur tout le M0 (Boris : « vérifie que la règle […] est bien respectée sur tout M0 ») — #285 pour ma zone, sept points pour la tienne

**Méthode.** Vingt expériences, chaque étape : porte, lieu de l'action, toutes les sorties après accomplissement (`redirect_to`, écrans de fin, JS) et destination réelle. Code : `origin/preprod` `0e144c8`. Chaque ligne citée ci-dessous a été relue dans le code.

**Verdict.** Les sorties normales sont conformes presque partout : mini-jeux, quiz, Conseil, premier cap, Graine, confirmations, sas d'étape passent par `/excursion/retour` ou `chemin_apres_experience`.

**Un défaut de fond : arriver sur la fiche SANS `/excursion/retour` laisse l'excursion OUVERTE.** Rien ne la referme ailleurs que dans `ExcursionsController` et `eveils_controller.rb:50`. Conséquences : pas de popup d'étape, et le prochain accusé d'éveil (`vu` l.105) repart vers ce retour oublié.
- Exemple, E1 : `gotoMonde0` ouvrait la fiche en direct. Après « Découvrir Désir », le joueur retombait sur la fiche d'E1.

**Ma zone : #285** (branche `rituel-retour-fiche`, vues et JS). En excursion, ces sorties passent désormais par le retour :
- E1 : la sortie du jeu est posée sur `<body data-sortie-fiche>` et lue par `gotoMonde0`. Le repli du canvas vise la fiche d'E1, plus `/jeu`.
- Quiz : « Reprendre plus tard » devient l'abandon.
- Registre vide, écran d'import du Sas, « Reprendre mon passage » du refus de dévoilement, lien de retour de `eveils/show`.
- Bancs : `verifier_excursion` (une section, chaque sortie par paire, dont un compte neuf `registre-vide@exc.pz` couvert par la purge) et `verifier_fin_du_tutoriel` §10.

**Ta zone :**
1. **`EveilsController#vu` : ce que ton message décrit comme servi n'est pas dans `origin/preprod`.**
   - On y lit encore : l.100-104, la destination retenue en premier ; l.105, `retour_excursion_path` si une excursion est ouverte ; l.137-138, `suite_apres_experience` (la suivante) ; l.139-140, `REPLI`.
   - S'il est servi sans être poussé : le pousser. Sinon : à faire.
   - Dans les deux cas, traiter `Eveil.etape_de_sas?` AVANT l.100-105. Une destination ou une excursion restées en session détournent la fin d'un sas d'étape (E2, E6, E7) vers une autre fiche, et la popup y annonce le mauvais rang.
2. **Un filet sur la fiche.** `ChallengesController#show` pourrait refermer l'excursion de CETTE expérience, et idéalement faire ce que fait `revenir` (constater, reconnaître l'étape).
   - Toute arrivée sur la fiche deviendrait un retour : historique, adresse tapée, sortie que j'aurais manquée.
   - Mes correctifs ferment les sorties connues ; le filet ferme les autres.
3. **Le texte de la popup finale.** `reconnaitre_au_retour` (`excursions_controller.rb:135`) pose `finale: termine.present?`.
   - Or `termine` vaut nil quand l'activité a déjà validé l'expérience avant le retour (Conseil, quiz, premier cap). La popup dit alors « Étape reconnue », au lieu d'« Expérience accomplie ».
   - Sur `decouvrir-les-formats`, le flash porte le rang de l'excursion alors que les trois rangs sont prouvés.
4. **La popup après « Recommencer ».** `eveils_controller.rb:127` exige `premiere_annonce`, qui est faux au rejeu : le retour arrive sur la fiche sans popup d'étape.
5. **L'épilogue.** `parcours_gestes_controller.rb:96`, `redirect_to accueil_jeu_path, notice: "Ton espace est prêt."` : ni fiche, ni popup, ni CTA final. C'est à Boris d'arbitrer : exception de clôture, ou fiche avec `etape_reconnue` finale.
6. **Le refus d'éveil.** `eveils_controller.rb:50-51` renvoie à la carte. Le rituel voudrait la fiche de l'expérience d'activation.
7. **Des actions accomplies qui ne ramènent pas d'elles-mêmes.** Le bandeau reste là, mais le retour demande un clic de plus :
   - le questionnaire de Puissance (`puissances_controller.rb:41` → la page de la Puissance, E14 rang 1) ;
   - la réservation d'un créneau (`inscription_creneaux_controller.rb:44` → `retour`, pour l'Atelier) ;
   - `assimiler` des Premières clés (E12 rang 3).
   - Si Boris veut le retour automatique, c'est `retour_excursion_path` quand l'excursion en cours vise cette expérience.

**Mineurs :**
- `premier_cap_controller.rb:43` : hors excursion, la carte (la fiche d'E14 serait le rituel) ;
- `messages_controller.rb:76` : le repli sans Turbo reste sur le fil (Graine sans JS) ;
- l'Atelier : « S'inscrire » (`evenements_jeu/_ligne.html.haml:27`) sort, volontairement (Stripe), vers la page publique sans bandeau, alors que la preuve du rang est une réservation de créneau. Parcours à arbitrer avec Boris ; ma vue suivra.

— le poste fixe

---

### 2026-09-15 · du poste fixe · ARBITRAGE DE BORIS — l'épilogue suit le même rituel, et la fiche finale arrive DÈS L'ÉPILOGUE (l'Atelier ne conditionne que le Monde 1) — quatre points dans ta zone, #286 dans la mienne

**Boris, à la suite de l'audit du rituel :**
- sur l'épilogue, qui menait à `/jeu` : « Même rituel, mais il me semblait qu'il y avait une fiche finale […] créé par Codex, est-elle implémentée ? » ;
- puis, à la question « le joueur termine l'épilogue alors que l'Atelier attend encore son facilitateur : que montre le CTA final ? » : **« Fiche finale dès l'épilogue »**.

**Constat** (`origin/preprod` `0e144c8`, chaque ligne relue) :
- La fiche finale existe : `/parcours/<slug>/accompli` (`JourneysController#accompli`, `journeys/_cloture`, portage de `?view=closure`).
- **Elle exige `BadgeDeParcours`**, c'est-à-dire toutes les obligatoires validées, dont `vivre-l-atelier-point-zero` (`auto_validated: false`, facilitateur).
  - Un joueur qui finit l'épilogue avant le Festival n'a pas le badge.
  - `accompli` le renvoie donc à la carte (l.52), et « Refermer le livre » n'apparaît pas (`JourneyProgress.accompli` = `completed_by?`).
- **Quand le badge arrive par un POST du joueur**, `AnnonceDesSeuils` pose `flash[:parcours_accompli]`.
  - `conduire_a_la_cloture` redirige alors la requête GET SUIVANTE, quelle qu'elle soit. Même `/excursion/retour`, dont `revenir` ne s'exécute pas : saut automatique, sans fiche ni reçu.
  - Si c'est un facilitateur qui valide (`/gestion`), rien n'est annoncé au joueur.
- `cloture_m0` (`parcours_gestes_controller.rb:96`) mène à `/jeu`.

**Demandé (la forme est à toi) :**
1. **`cloture_m0` rend la FICHE de l'épilogue**, avec `flash[:etape_reconnue]` en finale et son reçu : c'est le rituel. Plus de `/jeu`.
2. **Le CTA final de la fiche de l'épilogue mène à la fiche finale.** `suite_apres_experience(EPILOGUE)` doit rendre `accompli_journey_path`, avec le libellé « Refermer le livre » (canon §3.8, à confirmer par Codex). Aujourd'hui, l'épilogue étant la dernière, il rend « Revenir au parcours ».
3. **Le badge et la clôture du Monde 0 n'attendent plus l'Atelier en attente de facilitateur.** C'est la même règle que `locked_challenge_ids_for` (`attend_un_facilitateur`, donc `cleared`).
   - ⚠️ La porte du Monde 1 continue de lire la VALIDATION de l'Atelier (raccord §4 de Codex : « clôturer le M0 n'ouvre pas le M1 »). Les 7 Ω de l'Atelier arrivent à sa validation.
   - `completed_by?` sert ailleurs : peut-être vaut-il mieux séparer « clôturable » de « accompli » que de le toucher.
4. **La redirection automatique tombe** (`conduire_a_la_cloture`). La fiche finale s'atteint par le CTA de l'épilogue, puis par « Refermer le livre » sur la carte.
   - Bancs à retourner : `verifier_traversee_m0` §2 (l.147-151, « l'accomplissement du parcours s'annonce », vers `/accompli`).
   - À relire avec le point 3 : `verifier_serie_de_badges` (clôture refusée avant accomplissement) et `verifier_marelle` l.990.

**Ma zone : #286** (branche `cloture-voir-mon-badge`) : « Voir mon badge » et les actions de la maquette sur la fiche finale.
- « Voir mon badge » ouvre la fenêtre partagée `shared/badge_detail` avec `badges.js`, lue sur ses `data-*`.
- `journeys/accompli` transmet `phrase` et `condition` de `@badge_obtenu`.
- Banc : `verifier_serie_de_badges`.

— le poste fixe
