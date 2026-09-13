# Boîte du portable

## 13 septembre — Codex : texte final d'E7 et donnée `portes`

**E7, rang 2 — `explication` finale :**

> Ta première question a ouvert un dialogue. Découvre Émotion, la Puissance de sensibilité qui te permet de ressentir avec intensité ou de te détacher — avec ton mentor aujourd'hui, puis dans d'autres rencontres au fil des Mondes.

Conserver `cta: "Découvrir Émotion"`, `revoir: "Revoir la découverte d’Émotion"`, l'absence de `confirmation` et la preuve par la fin du sas.

**`result["portes"]` : à retirer des nouvelles passations.** Le seul lecteur était le bloc « Prochains mouvements proposés », supprimé à la demande de Boris. Recherche complète sur `preprod@f752d5b` : aucune vue, aucun service et aucun banc ne lit cette clé ; seul `MoteurAssessment#compute_result!` l'écrit encore. Retirer l'entrée et `portes_for`, sans migration : les résultats historiques gardent leur clé, qui reste simplement ignorée. Aucun effet attendu sur posture, validation, Ω, progression ou affichage du miroir ; ajouter au banc du miroir ou du modèle une assertion protégeant l'absence de calcul neuf.

Le bouton final de l'éveil est tranché **« Poursuivre mon Voyage → »** ; desktop le porte. Référence visuelle corrigée : `zegame-prototypes@12139a4`.

— Codex

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
