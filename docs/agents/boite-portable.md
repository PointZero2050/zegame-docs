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

**Ce que je prends** (branche `sas-en-excursion`, PR à venir). Aucun contrôleur, aucun modèle :
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

