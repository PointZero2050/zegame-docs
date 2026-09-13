# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, tard dans la nuit.** Traité depuis la vidange de la nuit : #254 (Codex, « Confiance » → lecture provisoire) et #255 (le miroir de la drôle d'époque) — préprod `f398eaa`. Avant : la revue de Codex sur
`462092b` (partie serveur soldée), #252 (l'éveil entier à 650 px, le vrai bandeau d'excursion partout,
le troisième écran, l'emblème, la popup « Recommencer ») et #253 (le tiroir Dopamine sur le lot JSON,
la place anonyme des secrets). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le complément B des 18 verbes (après A, au mot de Boris) ; rien d'autre en attente.
- **Codex** : rien en attente.
- **Boris** : retest du M0 en préprod (`f398eaa`) — Recette A remise à zéro à 13 h 15 après le
  correctif `3fcfc5a` (l'Hypothèse ne valide plus E2 : la fin du sas valide et verse) ; la fusion de #202
  (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR
  dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

## 13 septembre (soir) — Poste fixe : la sortie des découvertes d'E2 et d'E6 retombe sur la carte du parcours — chez toi

Boris, en recette : « à la fin de la troisième étape de découverte de la Volonté, on aboutit sur `/parcours/point-zero-monde-0` et non sur l'expérience suivante ». Même chose pour Imagination depuis E6.

**Diagnostic (lecture du code, sans compte de recette) :**

1. `SequenceDeGestes::PORTES` donne aux rangs 3 `/parcours/eveil/volonte` (E2) et `/parcours/eveil/imagination` (E6). Leurs commentaires disent « par l'excursion ».
2. Mais `porte_visible` rend telle quelle toute porte qui commence par `/parcours/` (`return reelle if journey.nil? || reelle.start_with?("/parcours/")`). **Aucune excursion ne s'ouvre** donc pour ces deux sas.
3. `EveilsController#vu` fait alors `return redirect_to retour_excursion_path if Excursion.en_cours(session)`, qui est faux ici, puis `FinDeSequence.constater_pour_progression!`, puis **`redirect_to Excursion::REPLI`**, c'est-à-dire la carte du parcours.

**Ce que Boris attend : l'expérience suivante.** Depuis `3fcfc5a`, c'est justement la fin du sas qui valide E2 et E6, donc la suivante est ouverte au moment du POST. Deux pistes, à toi de trancher :

- **(a)** Dans `vu`, quand l'expérience d'activation vient d'être close, rediriger vers sa suite, avec le même calcul que `suite_apres_experience` (la fiche courante si la suivante reste fermée) plutôt que vers `REPLI`.
- **(b)** Ou envelopper ces portes dans l'excursion. Mais le retour ramènerait alors à la **fiche** d'E2 ou d'E6, pas à la suivante : un clic de plus que ce que Boris demande.

⚠️ **Le libellé suit la destination.** Le bouton final de l'éveil dit « Revenir à l'Expérience → » (arbitrage de Boris via Codex, v22). S'il mène à l'expérience suivante, ce mot devient faux. Je le signale à Codex. Dis-moi quelle destination tu retiens, je porterai le libellé qui va avec.

Côté poste fixe, dans la même recette : #256 retire « Refaire l'étape » et affiche « Recommencer cette Expérience » sur chaque panneau dès qu'une étape est faite.

— poste fixe
