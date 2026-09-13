# Boîte du portable

⚠️ **Vidée le 14 septembre 2026, matin.** Traité depuis la vidange de la nuit : #254 (Codex, « Confiance » → lecture provisoire) et #255 (le miroir de la drôle d'époque) — préprod `f398eaa`. Avant : la revue de Codex sur
`462092b` (partie serveur soldée), #252 (l'éveil entier à 650 px, le vrai bandeau d'excursion partout,
le troisième écran, l'emblème, la popup « Recommencer ») et #253 (le tiroir Dopamine sur le lot JSON,
la place anonyme des secrets). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le libellé de l'emblème selon Codex ; le complément B des 18 verbes (après A, au mot de Boris).
- **Codex** : le libellé de l'emblème de l'éveil (la sortie mène à la suite) ; l'`explication` du rang 2 d'E7 (la mienne est provisoire) ; les portes du miroir.
- **Boris** : retest du M0 en préprod (`f752d5b`) — Recette A remise à zéro à 13 h 15 après le
  correctif `3fcfc5a` (l'Hypothèse ne valide plus E2 : la fin du sas valide et verse) ; la fusion de #202
  (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR
  dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

---

### 2026-09-13 (soir) · du poste fixe · je prends la finition visuelle de `/mentor` et les fonds des trois espaces relationnels

Boris a validé la cible de Codex (`zegame-prototypes@af48876`, `mentor-dialogue-cible`). Branche `mentor-journal-finition` depuis `preprod`.

**Ce que je touche** (vue et feuilles uniquement) : `mentor/show` (commentaire d'écarts), `heros.css` (bloc mentor), `mentor-panneau.js` (focus du tiroir), et le fond de page dans `echanges.css` et `guides.css` : bleu pour Échanges, vert pour Mentor, indigo pour Guides.

**Ce que je ne touche pas** : ni messages, ni appels au modèle, ni consentements, ni Graines. PR à suivre.

— poste fixe

---

### 2026-09-13 (soir) · du poste fixe · #258 poussée — la finition de `/mentor` et les fonds des trois espaces, à fusionner

PR sur `preprod`, branche `mentor-journal-finition`. Aucun contrôleur, modèle ni route touché.

- **Vue** : `mentor/show` ne change que dans son commentaire de tête (écarts). **Feuilles** : `heros.css` (bloc mentor), `echanges.css` et `guides.css` (fond de page ; la racine des Guides et son `.bg-box` deviennent transparentes). **Script** : `mentor-panneau.js` (focus du tiroir).
- **Bancs à rejouer** (pas de Ruby ici) : `verifier_mentor_page` (nouvelle section « La finition du 13 septembre »), puis `verifier_journal_mentor`, `verifier_mentor`, `verifier_mentor_contexte` (même vue), et les bancs d'Échanges et des Guides si l'un d'eux lit le fond de page.
- **Vérifié au navigateur** par simulation, aucun compte `@demo.pz` n'ayant de mentor : DOM de `/heros` transformé avec les feuilles locales, à 1440, 720, 701, 650 et 390 px ; clavier et tiroir ; voile de l'aide `?` au-dessus de la coque.
- **Une fois déployée**, un regard sur une vraie page `/mentor` serait bienvenu : je ne peux pas l'ouvrir avec un compte de vérification.

— poste fixe
