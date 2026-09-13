# Boîte du portable

⚠️ **Vidée le 14 septembre 2026, petit matin.** Traité depuis la vidange de la nuit : le contrat
E9 v2 de Codex (le Profil composé comme preuve, `4fb359e`), les noms du poste fixe (repris tels
quels), #259, puis #260 (la vue de l'éditeur, après mon lot) — préprod `aa08773`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le complément B des 18 verbes (après A, au mot de Boris).
- **Codex** : deux points tranchés sans lui sur E9 (le sceau « Présence choisie » suit le profil
  composé, Communication s'éveille toujours à la validation ; l'Annuaire `facultatif: true`) — à
  confirmer ou corriger.
- **Boris** : retest du M0 en préprod (`6bbe432`) — Recette A à E7, Émotion due ; la fusion de #202
  (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois
  PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb` ET `mise_en_service_profil_compose.rb`
  en production, `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19
  `*-v1`) : copier les dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de
  production et poser `photo`.

---

### 2026-09-14 · du poste fixe · Espace 1827 : branche `espace-composeur-stable` poussée — le composeur sort du fil, PR sur `preprod`

Cible Codex `7bd93cd`, validée par Boris. **Aucun contrôleur, modèle ni route.**

1. **`espaces/show`** : `.pz-fil-pied`, frère de `.workspace`, porte le composeur, ou l'état clos ou suspendu. Les formulaires d'objets restent dans le fil. `rencontre_possible` se calcule avant le fil.
2. **Hauteur** : la coque ne fait plus `100dvh - 68px`. La chaîne part de `body` (`height: 100dvh`) et passe par `main`, `.p-lg-5` et `#inner-main`, par `:has(.pz-m0-echanges--fil)` à toutes les largeurs et `--liste` au-dessus de 1121 px. Motif : avec une excursion ouverte, le bandeau (84 px) faisait déborder la page et poussait le composeur hors de l'écran. Sous 1121 px, la coque montait à 6 807 px.
3. **`composer.css`** : les marges négatives des Espaces sont retirées, et la réserve des messages passe de 110 à 16 px. Le `#composer` collant des fils d'expérience (`threads/show`) est **intact**.
4. **Bancs, avec un `ruby -c` d'abord** :
   - `verifier_espaces_s1` (fratrie du fil et du pied), `verifier_accueil_echanges` (chaîne de hauteur, §2 réécrit) et `verifier_apercu_espace` (le pied se cache avec le fil) ;
   - à rejouer aussi : `verifier_bascule_mobile`, `verifier_canal_m0`, `verifier_echanges`, `verifier_coque_m0`, et les bancs des réactions.
5. **À regarder sur la vraie page une fois déployée** (je ne l'ai vue qu'en simulation) : envoyer sans rechargement, répondre à un message, un espace clos, et `?objet=sondage`.

— poste fixe

---

### 2026-09-14 · du poste fixe · E10 : Boris supprime la constellation — « Explorer les cinq parcours » mène à la galerie du Sas, et la preuve devient « au moins un badge »

**Boris, en recette (Recette A à E10)** : « quand je clique sur "Explorer les 5 parcours", j'arrive sur la constellation. Il faut supprimer ce mini-jeu et renvoyer sur la page de sélection des parcours et un contrôleur doit vérifier si au moins un badge a été obtenu, avec possibilité d'en faire d'autres. »

**Destination tranchée par Boris** : la galerie du Sas, `/sas?screen=accueil` (« Cinq questions pour changer d'échelle »).

**Constat, mesuré sur la préprod `6bbe432`** (compte `nino`) :
- Le CTA du rang 1 ouvre `/excursion/ouvrir/point-zero-monde-0/le-site-du-point-zero/1`. Aucune `PORTES` n'est déclarée, donc la porte est l'adaptateur `site_point_zero_path` : « Explorer la constellation ».
- `RANGS_PROUVES["le-site-du-point-zero"] = [1, 2]`, prouvés par `TraceSas.pour(user).any?`, c'est-à-dire une trace IMPORTÉE, même inachevée.
- L'adaptateur `ExperienceState` d'E10 a pour `completed_check` le quiz de constellation achevé, et son `recommencer` relance ce quiz.
- ⚠️ **Une trace du Sas n'entre dans un compte QUE par `/sas/import`** (consentement, lecture du stockage local). Le Sas ne poste rien seul : un joueur connecté qui finit un parcours n'a encore RIEN en base.

**Ta part** (propositions ; la forme est à toi) :
1. **Porte du rang 1 : `/sas?screen=accueil`.** ⚠️ C'est une page publique, sans coque ni bandeau, alors que `verifier_excursion` exige qu'aucune porte d'excursion ne perde le bandeau. La session d'excursion survit pourtant : `/sas/import` est sous la coque et affiche « Revenir à l'Expérience » (vu sur la préprod). Deux voies :
   - porte directe, et retour par l'import ;
   - ou une exception motivée dans le banc.
2. **La preuve « au moins un badge obtenu »** est le fait que lit déjà `Badges::Lecture#parcours_du_sas_acheve` : une `TraceSas` avec `achevee_le`. **Nom proposé : `TraceSas.badges_obtenus(user)`**, les traces achevées. La même lecture sert à trois endroits : la preuve des rangs 1-2, `completed_check`, et le compteur de la fiche (ma PR). « Possibilité d'en faire d'autres » : rien ne se ferme, les quatre autres parcours restent jouables.
3. **Adaptateur d'E10** : plus d'`ExperienceQuizAttempt`, de `site_point_zero_path`, de `hint` « Carte de constellation » ni de `recommencer` de quiz.
4. **Retrait du mini-jeu** :
   - les trois routes `le-site-du-point-zero*`, `SitePointZeroController`, `ExperienceQuizzes::SitePointZero`, `config/experience_quizzes/le-site-du-point-zero.yml`, l'entrée l. 48 de `ExperienceQuizAttempt` et la note de `PlanDuSite` ;
   - **supprime aussi `app/views/site_point_zero/*` avec le contrôleur** : avant lui elles sont nécessaires, après lui elles sont mortes, une seule PR suffit ;
   - ⚠️ **les tentatives déjà en base** : `RegistreDesTraces` rend un quiz achevé comme Production avec `chemin: "/#{quiz_key}"`, donc une Carte de constellation conservée pointerait vers une route supprimée. À trancher : la garder sans lien, ou la retirer du registre. Aucune validation ni aucun Ω acquis ne se reprend.
5. **Bancs qui citent l'expérience ou le mini-jeu** :
   - à revoir : `verifier_marelle` (l. 2115), `verifier_portes_des_experiences` (l. 33), `verifier_omegas_du_sas`, `verifier_chaine_m0`, `verifier_accomplissements`, `verifier_illustrations_m0` ;
   - sans changement : les scripts de seed, durées et Ω (le slug reste).

**Ma part** (branche `e10-parcours-du-sas`, PR à suivre, **à fusionner après ou avec la tienne**) : sur la fiche d'E10, le compteur « X parcours réalisés sur 5 » devient **« X badges obtenus sur 5 »**, lu dans `TraceSas.badges_obtenus`. Sous le CTA, un lien vers `/sas/import` (« Faire passer mes traces dans le Jeu → ») : sans import, aucun badge n'arrive. Si tu choisis un autre nom, dis-le et j'aligne.

— poste fixe

---

### 2026-09-14 · du poste fixe · Éveils : les 54 figures d'incarnation — branche `eveil-figures-incarnation`, PR sur `preprod`

Demande de Boris portée par Codex (`zegame-prototypes@5ab49fe`) : dans l'écran Éprouver, chaque carte ouverte montre trois « Figures d'incarnation ». Aucun contrôleur, modèle ni route.

1. **Contenu** : `config/puissances/{6 Puissances}.yml`, clé `eveil.mouvements.<direction>.figures`, trois noms, 54 au total. ⚠️ `PuissanceAssessment.content` est **mémoïsé** : **deux redémarrages** après déploiement, sinon la page ne les rend pas.
2. **Vue, script, feuille** : `eveils/_eprouver` les rend cachées dans les trois cartes, `eveil.js` les révèle dans la carte ouverte, et la feuille `eveil.css` n'ajoute aucun palier (tout est dans le bloc de 650 px existant).
3. **Bancs, avec un `ruby -c` d'abord** : `verifier_eveil` (§2 bis : canon à 54, page à trois blocs cachés de trois noms, script servi ; §6 : règles servies). À rejouer par précaution : `verifier_eveil_reprise`, `verifier_roue_eveil`, `verifier_sas_d_eveil`.

Rien de la reprise, du compteur ni du POST `/carte/…` ne change. Vérifié en simulation à 1440 et 390 px : aucun nom au repos, seules les figures de la carte ouverte, aucune erreur, aucun débordement.

— poste fixe
