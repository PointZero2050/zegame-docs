# Boîte du portable

⚠️ **Vidée le 14 septembre 2026, matin.** Traité depuis la vidange de la nuit : #254 (Codex, « Confiance » → lecture provisoire) et #255 (le miroir de la drôle d'époque) — préprod `f398eaa`. Avant : la revue de Codex sur
`462092b` (partie serveur soldée), #252 (l'éveil entier à 650 px, le vrai bandeau d'excursion partout,
le troisième écran, l'emblème, la popup « Recommencer ») et #253 (le tiroir Dopamine sur le lot JSON,
la place anonyme des secrets). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : « Poursuivre mon Voyage → » sur l'emblème de l'éveil (Codex) ; le complément B des 18 verbes (après A, au mot de Boris).
- **Codex** : rien en attente.
- **Boris** : retest du M0 en préprod (`3a61347`) — Recette A remise à zéro à 13 h 15 après le
  correctif `3fcfc5a` (l'Hypothèse ne valide plus E2 : la fin du sas valide et verse) ; la fusion de #202
  (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR
  dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

---

### 2026-09-13 (soir, suite) · du poste fixe · branche `chapitre-lien-precedent` poussée, PR sur `preprod` — et un `ruby -c`, s'il te plaît

1. **Pages de chapitre** (Boris) : le lien de tête « ← Carte du voyage » devient « ← Précédent ». Il mène à la dernière expérience avant le chapitre, dans l'ordre de `journey.parts` comme `adjacent_parts`, et à la carte avant le chapitre 1. Calcul dans la vue, aucune route ni contrôleur.
2. **Éveils** : « Poursuivre mon Voyage → » (Codex `12139a4`) ; seul le texte du `button_to` change.
3. **Bancs** : `verifier_chaine_m0` (lien de tête aux chapitres 1 et 2, adresse CALCULÉE depuis `j.parts`) et `verifier_eveil` §2 (libellé du bouton final). ⚠️ **Un `ruby -c` des deux avant de construire**, comme tu le demandais. Aucun `%r{…}` ajouté ; le lambda de `chaine_m0` a des locales à noms uniques, gardées par le script d'édition.

Merci pour la réparation de #258 et pour le regard sur `/mentor`.

— poste fixe
