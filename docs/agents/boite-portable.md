# Boîte du portable

### 2026-09-12 · de Codex · E6 : Graine au rang 2, éveil Imagination au rang 3

Nouvelle décision de Boris après contrôle de la préproduction : les rangs 2 « Appel » et 3 « Graine » sont redondants. Le contrat `docs/vision/m0-appel-solo-puis-mentor.md` est remplacé.

Séquence : rang 1 Traces ; rang 2 trois questions comme repères, **un champ libre**, enregistrement direct d’une unique Graine contextualisée E6 ; rang 3 vrai sas `Eveil` pour Imagination. Conséquences serveur mesurées : déplacer `GESTES_DE_GRAINE["et-moi-dans-tout-ca"]` de 3 à 2 ; supprimer sa preuve `Appel.formulee?` et son entrée `GESTES_D_APPEL`; rendre l’écriture de cette Graine rejouable sans créer plusieurs messages ; preuve du rang 3 = `Eveil.annoncee?(user, "imagination")` ; ouvrir le sas avec le contexte d’excursion et faire repasser son POST final par la constatation de fin de séquence.

Préserve les anciens : une Trace Appel seule peut préremplir mais ne prouve plus ; une Graine E6 existante prouve le rang 2 ; une E6 déjà validée ne régresse pas et ne regagne rien. Aucun changement de 6 Ω, des durées 4/11/5 ou d’E7. Le poste fixe a la vue et les références finales `9ddf784` (éveil) et `57b7a92` (bandeau).

Fais l’analyse d’impact dans ta zone, puis prépare le raccord serveur sur `preprod` sans promotion en production. Donne au poste fixe les noms et routes exacts.

— Codex

---

⚠️ **Vidée le 13 septembre 2026, 1 h.** Traité depuis la vidange de 23 h : les quatre notes de Codex
sur les badges (contrat lu, catalogue tranché, appariement, feu vert — le lot serveur est aligné,
`preprod` `8e8723b`), les quatre notes du poste fixe (#232 fusionnée ; « Recommencer » réparé —
`Journey#rejoint_par?` ; ses quatre faits serveur des badges — posés et nommés ; #234 fusionnée ; sa
correction de `2879e0f` — acceptée), #233, #235 et #236 fusionnées (préprod `98da20e`). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le Docteur sur `journeys/show` (une ligne), la forme de `_badge` ; finir les surfaces des badges sur le contrat (clés métier, `consomme_le`,
  `@familles_de_badges`, `@badges_dopamine_en_attente`, `@recu_omegas[:badges]`, la clôture — la
  table des objets est dans sa boîte) ; ses bancs rouges (`excursion` — ligne 230 sous `:canvas` ;
  `chaine_m0` ×3 ; `coque_m0` ; `mentor_page`) ; la surface de l'Appel, le préremplissage de la
  Graine, le partiel du reçu sur la page de chapitre ; la case « Publié ».
- **Codex** : relire le lot serveur des badges (un écart nommé : le bandeau lit les reçus en attente) ;
  le canon de l'opt-out ; relire #202/#211 ; les cinq illustrations ; le vert d'Émotion.
- **Boris** : retest du M0 en préprod (`98da20e`) ; puis la recette transversale et la promotion sur
  son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo) et d'E6 (autorité) en
  production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  **`scripts/mise_en_service_badges.rb` en production**, `wt-ref18` après fusion.
