# Boîte du portable

⚠️ **Vidée le 14 septembre 2026 (après-midi).** Traité : le contrat serveur de la remise Dopamine (Codex),
#277 (+ amendement), #278, #279, #280 du poste fixe, le mentor « préfère ne pas répondre » — préprod
`d471213`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le complément B des 18 verbes (au mot de Boris) ; la casse « Revenir à l'Expérience »
  (selon Codex ; le helper et `verifier_action_experience` §4 suivront).
- **Codex** : la casse du libellé de fin d'activité ; une phrase de repli du mentor quand l'outil répond seul
  (facultatif) ; la conclusion du quiz d'E2 (« le procès du Coupable idéal », périmée).
- **Boris** : retest du M0 en préprod (`d471213`) ; la relance des paiements Festival non aboutis
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

### 2026-09-15 · du poste fixe · un profil de démonstration bien rempli (Boris) — PR #281, un script à lancer sur la préprod

https://github.com/PointZero2050/pointzero-app/pull/281 · branche `profil-de-demonstration`. Un seul fichier neuf, `scripts/profil_de_demonstration.rb` : aucune vue, aucun modèle, aucun banc touché.

Boris : « peupler un peu plus les profils joueurs pour les tests », puis « un seul joueur suffit ». Il a choisi un joueur fictif **dédié**, profil complet et contenus, plutôt qu'enrichir nino, lou ou Ana, dont l'état de jeu servirait ailleurs.

- **Iris Démo** (`iris@demo.pz`), dans le Monde 0.
  - **Profil** : composé en entier, visibilité toute ouverte, mentor choisi.
  - **Validations** : six expériences auto-validées, validées comme le Jeu (`end_at` puis `mark_as_validated!`).
  - **Contenus** : un bilan d'expérience ; trois Graines de Fresque (`Graine.semer!`) ; deux Traces (Immateria, première bifurcation) ; la chaîne invisible achevée ; deux traversées d'Avant le Zéro (FIN_CLAIRIERE, FIN_CHOEUR) ; le Moteur et deux Puissances publiées.
- **Garde-fous** :
  - `DB_HOST` doit contenir « preprod » ;
  - le script est idempotent : `defaire!` de son seul compte, et `--purger` pour défaire seulement ;
  - le mot de passe est aléatoire : on entre par `/acces-verification/iris`.
- **À lancer** (Ruby est absent chez moi) :
  1. `ruby -c scripts/profil_de_demonstration.rb` ;
  2. `docker exec pointzero-preprod-preprod-web-1 bin/rails runner scripts/profil_de_demonstration.rb` ;
  3. **renvoie-moi le rapport**. Chaque étape y dit ok ou ÉCHEC avec sa cause, puis ce que le profil montrera (Traces par famille, Graines, badges, Omégas).
- ⚠️ `compte_de_demonstration.rb` purge tous les `@demo.pz` : relancer celui-ci après lui.

— poste fixe
