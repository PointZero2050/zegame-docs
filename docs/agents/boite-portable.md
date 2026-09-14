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

---

### 2026-09-14 · du poste fixe · Audit des badges, point 2 : le tiroir Dopamine — PR #267 sur `preprod`

https://github.com/PointZero2050/pointzero-app/pull/267 · branche `dopamine-collection-gardee`. Vue, script et banc : **aucun contrôleur, modèle ni route, et la garde ne change pas** (arbitrage de Boris : même règle que #265).

1. **`shared/_remise_dopamine`** : `data-collection-url` n'est rendu que si `territoire_devoile?(current_user, :transcendance)`. **`dopamine.js`** : sans adresse, « Mes Accomplissements » est écrit dans un `span`, sans lien.
2. **Banc, avec un `ruby -c` d'abord** : `verifier_serie_de_badges`.
   - §3 : compte à E1, carte rendue **sans** adresse.
   - §7 : sept Puissances, un Dopamine en attente, carte rendue **avec** l'adresse.
   - ⚠️ Si la première valeur du §7 (un Dopamine en attente) rougit, c'est le décor et non la vue : dis-le-moi.

Avec #266 (Guides), tu as deux PR de moi en attente.

— poste fixe

---

### 2026-09-14 · du poste fixe · Mon Moteur : l'archétype sous les trois verbes, avec son médaillon — PR #268 sur `preprod`

https://github.com/PointZero2050/pointzero-app/pull/268 · branche `moteur-archetype-sous-verbes`. Vue, feuille et banc : **aucun contrôleur, modèle ni route.**

1. **`users/_moteur_cartes`** (demande de Boris) : l'archétype quitte l'en-tête de la carte et passe sous `.poles`, dans une rangée rendue sur les six cartes :
   - archétype connu : le médaillon `/pz/puissances/atlas/{puissance}-o{O}-l{L}-{etat}.png` (le même chemin que `puissances/show`) et le nom ;
   - sinon : encart « ? » et « Précise pour dévoiler ton archétype ».
   Hauteur de carte constante, mesurée : 408 px à 1440, 377 px à 390.
2. **Banc, avec un `ruby -c` d'abord** : `verifier_moteur_conscience` §5 bis.
   - Carte du Désir : le nom est sous les verbes et absent de l'en-tête, le médaillon est **demandé** (200), la règle n'a plus d'italique.
   - **Assertion retournée** : le compte neuf a six encarts et aucune illustration de l'atlas.
   - ⚠️ Les PNG de l'atlas sont hors dépôt, servis par le montage : si le 200 rougit, regarde d'abord le montage, pas la vue.

Avec #266 et #267, trois PR de moi attendent.

— poste fixe

---

### 2026-09-14 · du poste fixe · Bandeau d'excursion collant à toutes les largeurs — PR #269 sur `preprod`

https://github.com/PointZero2050/pointzero-app/pull/269 · branche `bandeau-excursion-collant`. Feuilles et banc : **aucune vue, aucun contrôleur, modèle ni route.**

1. **`excursion.css`** (Boris : « sticky pour toutes les pages où il y a du scroll ») : l'enveloppe `.excursion-bandeau` passe en `position: sticky; top: 0` dans la règle de base. Elle ne collait que sous 600 px.
   - `html:has(.excursion-bandeau)` pose `scroll-padding-top` (96 px, 164 avec la ligne de progression ; 94 et 146 sous 600 px), pour que les ancres et les focus tombent sous le bandeau.
2. **`echanges.css`** : le `scroll-margin-top` de `#seuil-espace` (#264) est retiré, sinon il s'ajouterait au décalage global.
3. **Banc, avec un `ruby -c` d'abord** : `verifier_excursion`.
   - L'assertion « collant SOUS 600 px, et seulement là » est retournée en « à toutes les largeurs », et aucun palier ne la défait.
   - Nouveau : les deux `scroll-padding-top`.
   - À rejouer aussi : `verifier_canal_m0` (il n'assertait pas le `scroll-margin`), `verifier_eveil`.
4. **Mesuré sur la préprod** (nino, excursion ouverte par sa porte) : `/mes-traces` et `/users/me` à 1440 et 390 px, `/une-drole-depoque` (coque `conseil`, avec la progression) à 1440 et 390 px. Pas vu : l'éveil.

Quatre PR de moi attendent : #266, #267, #268 et #269.

— poste fixe
