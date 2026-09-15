# Boîte du portable

⚠️ **Vidée le 15 septembre 2026 (fin de matinée).** Traité : #281, #282, #283, #284, #285, #286 du poste fixe ;
le retrait de la liste `/parcours` ; les portes d'E9 ; le retour de l'écran d'éveil ; l'arbitrage de Boris sur
le rituel ; « Bloquer » au Monde 0 ; la fermeture de compte (500) ; la mémoïsation de `monde_actuel` et le
préchauffage de l'Annuaire — préprod `2d94b71`.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Moi, de l'audit du rituel du poste fixe (15 septembre)** — le point 1 (`EveilsController#vu`) est servi :
  1. **Un filet sur la fiche** : `ChallengesController#show` refermerait l'excursion de CETTE expérience et
     ferait ce que fait `revenir` (constater, reconnaître l'étape). Toute arrivée sur la fiche deviendrait un
     retour — historique, adresse tapée, sortie oubliée.
  2. **Le texte de la popup finale** : `reconnaitre_au_retour` pose `finale: termine.present?`, or `termine`
     vaut nil quand l'activité a validé l'expérience AVANT le retour (Conseil, quiz, premier cap) — la popup
     dit « Étape reconnue » au lieu d'« Expérience accomplie ».
  3. **La popup après « Recommencer »** : `eveils_controller` exige `premiere_annonce`, faux au rejeu.
  4. **Le refus d'éveil** (`eveils_controller`, la garde) renvoie à la carte ; le rituel voudrait la fiche.
  5. **Les actions qui ne ramènent pas d'elles-mêmes** (questionnaire de Puissance, réservation de créneau,
     `assimiler` des Premières clés) : demande le mot de Boris avant de forcer le retour automatique.
  6. **Mineurs** : `premier_cap_controller` hors excursion (la carte), `messages_controller` sans Turbo,
     l'Atelier « S'inscrire » qui sort vers la page publique (à arbitrer avec Boris).
- **Moi, de l'arbitrage de Boris sur la clôture (15 septembre)** :
  1. `cloture_m0` rend la FICHE de l'épilogue, avec `flash[:etape_reconnue]` finale et son reçu — plus `/jeu`.
  2. Le CTA final de cette fiche mène à la fiche finale (`accompli_journey_path`, libellé à confirmer par Codex).
  3. Le badge et la clôture du M0 n'attendent plus l'Atelier en attente de facilitateur (même règle que
     `locked_challenge_ids_for`) — ⚠️ la porte du Monde 1 continue de lire la VALIDATION de l'Atelier.
  4. `conduire_a_la_cloture` (la redirection automatique) tombe. Bancs : `verifier_traversee_m0` §2,
     `verifier_serie_de_badges`, `verifier_marelle`.
  ⚠️ **#286 est fusionnée : la vue de la fiche finale existe AVANT son chemin.**
- **Moi, E9/E12 (étapes d'éveil)** : **bloqué sur Codex** — textes des deux gestes et durées. La mécanique
  (`SAS_D_EVEIL`, `PREUVES_PAR_GESTE`, portes, renumérotation d'E9 rang 3 → 4 en préprod ET production) ne se
  pose pas à moitié : la fiche et le contrat se contrediraient.
- **Codex** : les textes d'E9/E12 et les durées ; la casse du libellé de fin d'activité ; une phrase de repli
  du mentor quand l'outil répond seul ; la conclusion du quiz d'E2 ; le libellé « Refermer le livre ».
- **Poste fixe** : le complément B des 18 verbes (au mot de Boris).
- **Boris** : retest du M0 en préprod (`2d94b71`) ; la relance des paiements Festival (7 personnes, à la main) ;
  #202 (A) puis #211 ; les trois PR dependabot (#226, #227, #228) ; la promotion sur son mot ; le point 5
  ci-dessus (retour automatique) et l'Atelier.
- **Moi, à la promotion** : données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; migrations (`recus_omega`,
  `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ; `mise_en_service_badges.rb`,
  `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`, `mise_en_service_accroches_m0.rb` ;
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) ; **deux
  redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`).
- ⓘ `zegame-docs` est sur la branche de Codex depuis le 14 : je travaille `main` depuis un worktree séparé.
