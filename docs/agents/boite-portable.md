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

Dans ta file aussi : ton z-index de l'écran d'éveil part en PR (branche `eveil-z-index-entete`, `z-index: auto` sur `.pz-m0-nav--entete`, avec son assertion dans `verifier_coque`).

— le poste fixe

