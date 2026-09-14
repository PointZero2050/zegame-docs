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

---

### 2026-09-14 · du poste fixe · « Dopamine sous le reçu » : la vue est prête — PR #278, à fusionner AVEC ton lot serveur

https://github.com/PointZero2050/pointzero-app/pull/278 · branche `dopamine-sous-le-recu` depuis `aa61a3e`. Elle suit mon contrat d'hier soir : la vue lit `recu[:dopamine]`, et rien d'autre.

- **Ce qu'elle rend** : quand `recu[:dopamine]` n'est pas vide, la note du Docteur et le tiroir du lot (`shared/_diagnostic_dopamine`, neuf), DANS `dialog.omega-receipt`.
  - Aucun `fetch`, rien de consommé.
  - `collection_ouverte` se lit du joueur par `territoire_devoile?`, ou d'un local quand un banc rend le partiel hors requête.
- **Ce qu'elle retire** :
  - l'appel sur l'accueil (`render "shared/remise_dopamine"` dans `home/monde_0` et `journeys/_show`) ;
  - `_remise_dopamine` et `dopamine.js` ;
  - les règles de la carte dans `dopamine.css` et `parcours.css`.
  - ⚠️ **Fusionnée seule**, elle laisse les Dopamine en attente, invisibles hors de Mes Accomplissements.
- **Chez toi** :
  - `recu[:dopamine]`, l'attache à la validation (et les Dopamine obtenus pendant l'expérience), la consommation avec le reçu ;
  - la fin de `@badges_dopamine_en_attente` et de `POST /badges/remise` ;
  - le sort des Dopamine déjà en attente chez les anciens joueurs.
- **Bancs** : `ruby -c` de `verifier_serie_de_badges` et `verifier_recu_omega`.
  - `verifier_serie_de_badges` :
    - **§3 retourné** : un Dopamine attend, et l'accueil et la carte du voyage ne rendent plus rien ; `dopamine.js` répond 404 ;
    - **§3 bis neuf** : le reçu rendu hors requête, avec la vue du §2 fusionnée de `dopamine:` ;
    - **§7** : la paire avant/après E14, lue sur le reçu.
  - `verifier_recu_omega` : les lots vide, un et deux.
  - ⚠️ **Laissés pour ton lot** : les assertions du POST `/badges/remise` dans le §3, et la ligne du §2 « sans reçu d'Omégas attaché (un Dopamine attend l'accueil) ». Le chemin réel est à écrire avec toi.
- **Simulé** sur `/jeu` servi, à 1440 et 390 px :
  - note à 18 px du bas, reçu et CTA au-dessus d'elle, note cliquable ;
  - le tiroir s'ouvre au vrai clic, et « Revenir au reçu » rend le focus à la note.
  - ⓘ Échap n'a pas pu être éprouvé : la touche injectée par le navigateur intégré n'émet pas de `cancel`, pas plus sur le reçu déjà servi.

— poste fixe

---

### 2026-09-14 · du poste fixe · PR #279 — les items des sous-menus calés à gauche (Boris), empilée sur #277

https://github.com/PointZero2050/pointzero-app/pull/279 · branche `sous-menu-a-gauche`, **partie de `suites-codex-14`**. #277 modifie la ligne de `coque.css` juste au-dessus : **à fusionner après #277**.

Boris : « Sous le menu principal, cale les items des sous-menus à gauche, je pense que ce sera plus lisible. »
- **`coque.css`** : `.territory-nav` passe de `justify-content: center` à `flex-start`, et la marge de rupture devient `max(16px, calc(50vw - 50%))`.
- **Mesuré à 1440 px** avec la feuille locale : le premier item tombe sous le logo du menu, à 113 px sur le profil et Mes Traces, à 16 px sur les Échanges ; aucun défilement horizontal.
- **Inchangé** : sous 800 px et sur les Clés, les items étaient déjà à gauche.
- **`ruby -c`**, puis `verifier_coque` : son §9 lit la règle du conteneur, commentaires retirés, et y exige `flex-start` sans `center`.

— poste fixe

---

### 2026-09-14 · du poste fixe · Boris : le mentor « préfère ne pas répondre » au moment de poser la Graine — ce n'est pas un refus, c'est l'outil seul. Chez toi

Boris, en recette, conversation anodine avec Aragorn (thématique Graine). Le mentor propose : « Veux-tu qu'on pose ça dans une Graine ? ». Boris répond « Oui ». La page affiche « Ton mentor préfère ne pas répondre à cela. Passer par l'Aide → », et aucune Graine n'apparaît.

**Le mécanisme** (lu dans `MentorReponse`, `38fee7b` ; rien joué, ni base ni journal lus) :
- `refuse = reponse.stop_reason == :refusal || bloc_texte.nil?` range sous « refuse » toute réponse **sans bloc de texte**.
- À « Oui », la réponse attendue EST le bloc de récit. La consigne dit de le transmettre « et lui seul, sans ta parole autour — par l'outil proposer_graine ». Le modèle a très probablement rendu un `tool_use` `proposer_graine` seul (`stop_reason: :tool_use`), malgré « ta réponse texte reste entière ».
- Deux effets : `statut: "refuse"`, donc la vue rend le repli de refus ; et `enregistrer_proposition` n'est pas appelé (`unless refuse`). **La Graine proposée est jetée.** La ligne `MentorMessage` du mentor est écrite avec `contenu: nil`.
- **Pour confirmer en base** : pour ce compte vers 15 h 46, une ligne `role: "mentor"` avec `contenu: nil` et `jetons_sortie > 0`, sans `PropositionDeGraine`. Un vrai refus du modèle aurait `stop_reason: :refusal` (et `stop_details`) : le service ne le journalise pas aujourd'hui.

**Proposition, la forme est à toi :**
1. **Seul `stop_reason == :refusal` est un refus.** Journaliser `stop_details` (catégorie, explication) pour distinguer un vrai refus.
2. **Un `proposer_graine` valide sans texte est une réponse** : `statut: "ok"`, `enregistrer_proposition` appelé. La vue rend la proposition, avec une phrase de repli du mentor (texte à Codex) ou la carte seule. Je porte le rendu si tu fixes la forme de `Resultat` (`texte: nil` avec `proposition:`).
3. **Ni texte, ni outil valide** (réponse vide) : un statut de panne (« ne répond pas pour l'instant »), pas « préfère ne pas répondre », qui accuse le joueur d'avoir demandé quelque chose d'inavouable.
4. **La consigne** peut exiger une phrase avant l'outil, mais le rempart doit être le serveur : le modèle vient de montrer qu'il suit « lui seul » avant « se suffit ».
5. **À vérifier** : la ligne `contenu: nil` est exclue de `messages_pour_api`. Le tour suivant envoie donc « Oui » puis la nouvelle question, deux `user` d'affilée, et le mentor ne se souvient pas avoir proposé la Graine.

**Banc** : `verifier_proposition_graine` fabrique déjà des réponses `OpenStruct` à `tool_use`. Le cas « `tool_use` seul, sans bloc texte » est le témoin à ajouter : `statut` ok, proposition créée, pas de repli de refus.

— poste fixe

---

### 2026-09-14 · du poste fixe · tes deux lots côté vues — PR #280 ; #277 amendée ; et `memoire_affichable` cache la Graine de l'outil seul

https://github.com/PointZero2050/pointzero-app/pull/280 · branche `fins-d-activite` depuis `e0cc40e`. **Aucun conflit** avec `preprod` pour #277, #278, #279 et celle-ci (vérifié par `git merge-tree`).

- **`d9de942`** :
  - ton `_miroir` est relu et juste ; j'ai seulement retiré la flèche ;
  - **les libellés mentaient encore** : le Coupable idéal (v1 et v2, `bouton_suite` « Poursuivre vers Une drôle d'époque ») et le Conseil Oméga (« Revenir au parcours ») mènent maintenant à leur fiche. Ils disent désormais `libelle_apres_experience`, sans flèche ; « Refermer le livre » reste ;
  - **#277 amendée** (`fc39739`) : la restitution compte `/excursion/retour` comme la fiche. Sans cela, « Continuer le parcours » revenait en excursion, puisque ton `suite_path` rend ce retour.
- **`e0cc40e`** : la bulle du mentor n'est rendue que si le texte de la réponse est présent, et une ligne du fil sans contenu n'est plus une bulle vide.
- ⚠️ **Chez toi : `MentorController#memoire_affichable`** exclut les lignes sans contenu. La proposition de l'outil seul **disparaît donc du fil au rechargement** : la vue ne rend une proposition que sous un message affiché, et la clause « fraîche » ne vaut que pendant le POST. Il faudrait garder aussi les lignes du mentor qui portent une proposition non écartée ; ma vue les rend déjà sans bulle.
- **La casse du libellé** : ton helper dit « Revenir à l'expérience », Codex écrit « Revenir à l'Expérience » (restitution). La question est posée à Codex ; si c'est sa forme, `verifier_action_experience` §4 suit.
- **Bancs** : aucun ne lisait ces libellés. Pour #280, rejouer `verifier_marelle`, `verifier_chaine_m0`, `verifier_mentor_page` et `verifier_miroir_epoque` ; `nids_haml.pl` est propre.

— poste fixe
