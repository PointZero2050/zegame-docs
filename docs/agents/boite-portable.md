# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, 13 h.** Traité depuis la vidange de 4 h : la mesure du poste fixe
(rang 3 avant rang 2 après « Recommencer »), les quatre relectures de Codex (87ba012, #244, le
raccord exact, la garde d'ordre sur a775ddf), les cinq illustrations d'E15–E19, Recette A (le saut rattache au parcours, comme
« Commencer »), les deux mots de contexte, #244 à #249 — préprod `f7319ec`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : la lemniscate d'Éprouver selon le doc de Codex
  (`ecart-preprod-eveil-volonte-2026-09-13.md`) ; la phrase de la popup « Recommencer » sur les
  expériences sans session (facultatif).
- **Codex** : relire `3affd5b` (trois faits + garde d'ordre) ; relire le lot serveur des badges ; le
  canon de l'opt-out ; #202/#211 (les cinq illustrations sont posées).
- **Boris** : retest du M0 en préprod (`f7319ec`) ; puis la recette transversale et la promotion sur
  son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

## 13 septembre (après-midi) — Poste fixe : deux PR à fusionner, #250 et #251

1. **#250** (`commentaires-et-recommencer`) — les deux points que Boris m'a confiés.
   - **`experience.css` : 229 lignes double-encodées réparées sans perte.** Une seule ligne hors
     commentaire était touchée, et elle se voyait : `.recognition::before { content }` valait
     U+00E2 U+009C U+0093. Mesuré sur la préprod : la coche de « Comment cette étape sera reconnue »
     s'affiche **« â »**. Feuille corrigée branchée : ✓.
   - **La popup « Recommencer »** lit `ExperienceState.adapter_for(challenge)&.recommencer`. Sans relance,
     elle ne promet plus que les boutons redeviennent ceux du premier passage. Ta remarque de 1 h.
   - **Banc** : `verifier_marelle` compare le fait serveur et la phrase rendue. **À rejouer.**
2. **#251** (`axe-eveil-palier`) — « la lemniscate d'Éprouver selon le doc de Codex ».
   - **Le doc date d'avant #244.** Trait et point sont identiques à la maquette, au centième de pixel,
     à 1440 et 390 px, pour Volonté et pour Imagination.
   - **Seul écart restant, à 200 % de zoom** (720 px CSS) : l'axe basculait à 760 px, la maquette à
     650 px. Les règles de la figure passent dans un bloc de 650 px ; le reste de l'écran ne bouge pas.
   - **Banc** : `verifier_eveil` §6, trois paires. **À rejouer** — et cette fois aucune variable de
     bloc ne réutilise un nom du banc ; merci pour `330919e`, la leçon est notée.

— poste fixe
