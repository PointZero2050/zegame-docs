# Boîte du portable

⚠️ **Vidée le 14 septembre 2026.** Traité : #261, #263, #264 (poste fixe) ; E10 v2 — la constellation
retirée, le Sas et un badge comme preuve — avec #262 ; l'audit des badges de Codex (trois bancs rejoués) et #265 (son point 1) — préprod `a23b82d`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le libellé du bouton de suite quand il mène à un éveil (`suite_experience[:libelle]`) ; le mot du tiroir avant E14 (selon
  Codex) ; le complément B des 18 verbes (après A, au mot de Boris).
- **Codex** : le mot du tiroir Dopamine avant E14 ; la `description` d'E9 en base (« confirme sa
  visibilité ») ; les deux points d'E9 (sceau, Annuaire facultatif).
- **Boris** : retest du M0 en préprod (`5f2c582`) — Recette A à E12 ; la fusion de #202 (A, migration
  additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR dependabot
  (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb` ET `mise_en_service_profil_compose.rb`
  en production, `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19
  `*-v1`) : copier les dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de
  production et poser `photo`.

---

### 2026-09-14 · du poste fixe · Guides : le socle du dialogue (Codex `928ef0b`) — PR #266 ; et les suggestions n'envoyaient rien (Guides ET mentor)

https://github.com/PointZero2050/pointzero-app/pull/266 · branche `guides-composeur-stable`. Vues, feuille et scripts : **aucun contrôleur, modèle ni route.**

1. **Portage** :
   - `guides/new` : fil en colonne (seul `.pz-thread` défile), socle empilé, bulle d'attente avec `shared/_omega` ;
   - retirés de la vue : « Badge obtenu » et « Signaler cette réponse » (la route de signalement reste) ;
   - « Effacer toutes mes conversations » passe dans un menu d'en-tête : l'ancien « Effacer ce fil » effaçait tout ;
   - script neuf `guides-dialogue.js`.
2. **⚠️ Défaut réel, mesuré sur la préprod** : les suggestions et le champ portent `name="question"`, et le champ vient après. `new FormData(formulaire, suggestion)` donne `question=<suggestion>` **puis** `question=` ; Rack garde la dernière valeur, le joueur lit donc « Écris ta question. » (Guides) ou « Écris quelque chose à ton mentor. » (mentor, même balisage).
   - **Mon correctif** : `guides-dialogue.js` et `mentor-panneau.js` recopient la suggestion dans le champ avant l'envoi.
   - **Sans script, le défaut reste.** Pour le fermer côté serveur, je te propose : je renomme les boutons `name="suggestion"`, et tu lis `params[:question].presence || params[:suggestion]` dans `GuidesController#creer` et `MentorController#message`. Dis-moi si tu le prends.
3. **Bancs, avec un `ruby -c` d'abord** : `verifier_guides_page` (§3 ter neuf, §4 retourné, feuille) et `verifier_mentor_page`. À rejouer aussi : `verifier_widget_guides`, `verifier_fil_guides`, `verifier_conversations_guides`, `verifier_guide_llm`, `verifier_images_servies`.
4. **Sur la vraie page une fois déployée** : une vraie question, où la bulle d'attente doit rester visible pendant l'appel ; puis un clic sur une suggestion, qui doit recevoir une réponse.
5. **Tiroir Dopamine** (reste de l'audit de Codex) : j'attends l'arbitrage de Boris avant d'y toucher.

— poste fixe
