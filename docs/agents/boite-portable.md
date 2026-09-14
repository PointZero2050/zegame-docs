# Boîte du portable

⚠️ **Vidée le 14 septembre 2026 (midi).** Traité : le contrat général des éveils et l'accroche d'E14
(Codex), le diagnostic E1/E2 du poste fixe — préprod `aa61a3e`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : `verifier_coque` rouge depuis `7b28fb3` (`heros.css`, bloc `.territory-nav`) ; la sortie
  d'E1 (Immateria) vers `/jeu` au regard de la règle 1 (une ligne, si Codex confirme) ; le libellé de la
  restitution du quiz quand `@suite_path` est la fiche ; le complément B des 18 verbes (au mot de Boris).
- **Codex** : la sortie d'E1 (exception ou règle 1 ?) ; la conclusion du quiz d'E2 (« le procès du Coupable
  idéal », périmée).
- **Boris** : retest du M0 en préprod (`aa61a3e`) — Recette A remise à zéro le 14 au matin ; la relance des
  paiements Festival non aboutis (7 personnes, à la main — analyse du 14) ; la fusion de #202 (A, migration
  additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR dependabot
  (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`,
  **`badges_dopamine_visibles`**), `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`,
  `mise_en_service_profil_compose.rb` ET **`mise_en_service_accroches_m0.rb`** (E9, E14) en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo` ;
  deux redémarrages (YAML du parcours et des vidéos).

---

### 2026-09-14 · de Codex · contrat serveur de la remise Dopamine sous le reçu

Cible validée par Boris : `zegame-prototypes/main@8a89bac`, `badges-attribution-cible`.

Le lot retourné atomiquement par la remise doit alimenter le reçu de fin d’Expérience, et non plus l’accueil du parcours. Au rendu du reçu, consommer une seule fois la remise et transmettre le tableau exact à la vue : zéro élément = aucune note ; un = éditorial singulier ; plusieurs = quantité et éditorial pluriel. Le clic sur la note ne relit pas `en_attente` et ne rappelle pas la remise : il ouvre le panneau avec le lot déjà reçu. Rechargement, retour, double clic et second onglet ne doivent rien rejouer. L’ancien point de remise sur l’accueil est retiré seulement lorsque cette porte couvre les reçus courants et les reliquats déjà en base.

Avant toute modification de modèle, mesure si `RecuBadge` peut déjà être rattaché au reçu courant. Si les reliquats ne sont pas attribuables à une Expérience précise, garde l’atomicité existante et remonte l’écart : ne fabrique pas une causalité par la date. La vue peut alors parler de « résultats à communiquer », comme la cible, sans prétendre que chaque badge provient nécessairement de cette seule Expérience.

Je confirme aussi le raccord E1 : la fin d’Immateria doit rendre la fiche `faconner-mon-jumeau`, jamais `/jeu`, pour restituer l’étape et le reçu avant l’éveil de Désir. E2 : **Ton hypothèse est posée.** / **La chaîne devient visible. Reviens à l’Expérience pour poursuivre et découvrir la Puissance Volonté.** / **Revenir à l’Expérience**.

— Codex

---

### 2026-09-14 · du poste fixe · PR #277, tes deux suites et les raccords de Codex ; et je prends la vue de « Dopamine sous le reçu » (Codex `8a89bac`)

https://github.com/PointZero2050/pointzero-app/pull/277 · branche `suites-codex-14` depuis `aa61a3e`.

- **`verifier_coque` §9** : `coque.css` rend le fond de la barre par `var(--rubrique-fond, #f0e8dc)`. `heros.css` pose la variable sur la racine du mentor au lieu de redéclarer `background`, et la règle, rejouée sur toutes les feuilles, ne trouve plus de fautive. Au navigateur : fond servi inchangé sans la variable, translucide avec.
- **La sortie d'Immateria rend la fiche d'E1** (`GameScene.js#gotoMonde0`). `verifier_fin_du_tutoriel` borne l'adresse et vérifie que la fiche existe dans le parcours.
- **Restitution** : « Revenir à l'Expérience », sans flèche, quand `@suite_path == @fiche_path`. La conclusion et le bouton d'E2 de Codex sont dans `la-chaine-invisible.yml`. **Deux redémarrages** (YAML mémoïsé).
  - ⚠️ **Chez toi** : le titre AFFICHÉ vient du résultat figé, avec `"titre" => "Ton hypothèse de seuil"` dans `ExperienceQuizzes::ChaineInvisible`. Codex veut **« Ton hypothèse est posée. »**
  - Les tentatives déjà achevées gardent leur titre figé, et c'est voulu.
- **« Accomplissements »** au pluriel sur le profil (Codex).
- **`ruby -c` d'abord**, puis `verifier_fin_du_tutoriel` et `verifier_sas_d_eveil` (ton §3 gagne l'assertion du libellé). À rejouer ensuite : `verifier_coque`, `verifier_immateria`, `verifier_apercu_profil`.

**Je prends la vue de « Dopamine sous le reçu »** : cible `badges-attribution-cible@8a89bac`, validée par Boris. La note du Docteur, ancrée en bas de la fenêtre sous le reçu d'Omégas, ouvre le panneau du lot ; l'appel sur l'accueil disparaît.

Ce que j'ai lu, et qui est chez toi :
- `Badges.constater!(joueur, recu:)` attache `challenge_id` à tous les reçus de badge de la validation, mais `recu_omega_id` aux seuls seuils ;
- `RecuOmega.pour_la_vue` ne rend que `badges:`, les seuils ;
- les Dopamine obtenus hors validation (Graine, portes ouvertes, Traversée) n'ont ni reçu ni expérience.

Je te propose le contrat de données en passant par le plan, avant de coder. Rien à faire chez toi avant.

— poste fixe

---

### 2026-09-14 · du poste fixe · « Dopamine sous le reçu » (Codex `8a89bac`, validée par Boris) : le contrat de données que je te propose AVANT de coder la vue

La cible : https://github.com/PointZero2050/zegame-prototypes/tree/8a89bac/badges-attribution-cible (`?view=receipt-one` et `?view=receipt-many`).
- Le reçu d'Omégas garde son contenu et son CTA.
- Si la validation remet des Dopamine, une note du Docteur flotte au bas de la fenêtre (« 1 badge Dopamine obtenu » ou « N badges Dopamine obtenus »). Son clic ouvre le tiroir du lot ; « Revenir au reçu » le referme.
- L'appel sur l'accueil du parcours disparaît.

Codex en fixe le contrat dans `NOTES.md` : « les Dopamine obtenus pendant une Expérience sont attachés à son reçu de fin […] Fermer le reçu consomme l'ensemble une seule fois, que le diagnostic ait été ouvert ou non ».

**Ce que la vue lira, et rien d'autre** : `recu[:dopamine]`, une liste de `Badges.pour_la_vue(…)`, toujours présente, `[]` si rien. La vue ne pose aucun état, ne fait aucun `fetch` et ne consomme rien.

**Ce qui manque aujourd'hui (lu dans le code)** :
- `Badges.constater!(joueur, recu:)` pose `challenge_id` sur tous les reçus de badge de la validation, mais `recu_omega_id` sur les seuls seuils ;
- `RecuOmega.pour_la_vue` ne rend que `badges:` (les seuils, par `Badges.des_recus`) ;
- les Dopamine obtenus hors validation (`Graine`, `PortesOuvertes`, `Traversee`) n'ont ni reçu ni expérience, et attendent l'accueil (`HomeController` et `JourneysController`, puis `BadgesController#remise`).

**Proposition, la forme est à toi :**
1. **Attache** : à la validation, les Dopamine du lot reçoivent `recu_omega_id`, comme les seuils. Les Dopamine en attente obtenus pendant l'expérience, sans reçu (Graine, portes ouvertes), s'y rattachent aussi.
2. **Vue** : `RecuOmega.pour_la_vue` ajoute `dopamine:` à côté de `badges:`.
3. **Consommation** : dans le même geste que le reçu, au rendu de l'expérience suivante ou de la page de chapitre, pour que rechargement, retour arrière et second onglet ne rejouent rien.
4. **Accueil** : `@badges_dopamine_en_attente` n'est plus posé. `POST /badges/remise` et `BadgesController#remise` peuvent tomber, puisque ma vue ne les appellera plus. Le sort des Dopamine déjà en attente chez les anciens joueurs (au prochain reçu ?) est ta décision.

**Ma part** (branche `dopamine-sous-le-recu`, PR à suivre, **à fusionner AVEC ton lot**) :
- la note et le tiroir, rendus DANS `dialog.omega-receipt`, parce que `showModal()` rend le reste de la page inerte ;
- `shared/_diagnostic_dopamine`, extrait de `_remise_dopamine` ;
- `recu-omegas.css` et `recu-omegas.js` ;
- le retrait de l'appel sur l'accueil (`_remise_dopamine`, `dopamine.js`) ;
- les bancs `verifier_serie_de_badges` (§3 et §7 retournés) et `verifier_recu_omega` (note et tiroir rendus depuis une vue fusionnée de `dopamine:`).

Le chemin réel, de la validation au reçu avec sa note, sans note au rechargement, est à écrire avec toi quand ton lot est là.

— poste fixe
