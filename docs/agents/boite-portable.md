# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, nuit.** Traité depuis la vidange de 15 h : la revue de Codex sur
`462092b` (partie serveur soldée), #252 (l'éveil entier à 650 px, le vrai bandeau d'excursion partout,
le troisième écran, l'emblème, la popup « Recommencer ») et #253 (le tiroir Dopamine sur le lot JSON,
la place anonyme des secrets) — préprod `998536c`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le complément B des 18 verbes (après A, au mot de Boris) ; rien d'autre en attente.
- **Codex** : rien en attente.
- **Boris** : retest du M0 en préprod (`998536c`) — Recette A remise à zéro à 13 h 15 après le
  correctif `3fcfc5a` (l'Hypothèse ne valide plus E2 : la fin du sas valide et verse) ; la fusion de #202
  (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR
  dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

## 13 septembre (nuit, suite) — Poste fixe : #255, le miroir de la drôle d'époque (demande de Boris)

Trois demandes de Boris sur la page finale d'« Une drôle d'époque », dans `drole_epoque/_miroir` et `conseil.css` :

- **Le Tao** : l'image de l'application (`/pz/m0/source.png`) remplace le symbole redessiné, dont les deux points étaient invisibles.
- **Le lemniscate de la posture est animé** : un point doré le parcourt (`animateMotion`), comme dans le Moteur, et disparaît sous `prefers-reduced-motion`.
- **« Prochains mouvements proposés » est retiré**, avec ses règles. `result["portes"]` reste calculé chez toi, mais la vue ne le lit plus : à toi de voir s'il doit survivre.

**Banc neuf `scripts/verifier_miroir_epoque.rb`** : il lit la vue et la feuille, sans Rails, puisque le miroir exige une traversée achevée. Il se lance avec `ruby` ou avec `bin/rails runner`. **À exécuter à la fusion**, et à ajouter à ta liste si tu en tiens une.

— poste fixe
