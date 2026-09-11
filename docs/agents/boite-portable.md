# Boîte du portable

⚠️ **Vidée le 11 septembre 2026, au matin.** Traité depuis la dernière purge (10 septembre,
18 h) : les notes de Codex sur l'épilogue (3 min écrites, totaux inchangés), sur EXPRESSION /
DISCERNEMENT (diagnostic déposé, publication **non exécutée** — le cap a changé vers les
18 verbes), sur l'ARIA de #191 (corrigé par #192, promu), et sa correspondance vers les 18
compétences-verbes (inventaire déposé dans `docs/vision/inventaire-referentiel-2026-09-11/`).
Les PR #186 à #192 sont en production. Les sept rouges et deux muets de la recette transversale
sont retournés et promus.

Ce qui devait survivre est dans les commentaires du code et des bancs, dans les messages de
commit, et dans les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : la mécanique du « référentiel commun sans privé/public » (`Challenge#skill_visibility`
  est le point à traverser) et la forme du regroupement vers les 18 verbes — l'inventaire id par
  id est déposé, la migration attend son plan de conservation ; les deux arbitrages de la Carte du
  Seuil (le sceau prouve-t-il le rang 3 ? les Graines entrent-elles sur la Carte ?) ; cinq verbes
  sans aucune expérience pour les exercer.
- **Poste fixe** : #193 (mise en forme de la fiche), en cours de relecture ; la restitution mobile
  de M0-31 ; la vignette carrée 80 × 80 pour le rond de 56 px.
- **Moi** : `raz_compte.rb` sans banc ; le repli `update_column` de `appliquer_durees_v1.rb`
  reste tant que les deux Sources privées le justifient.
- **Boris** : rien en attente.

---

## 11 septembre — Je prends l'alignement de `#top-bar` sur le conteneur (chantier transverse)

Boris, capture à l'appui : « sur desktop, le menu principal est ferré à gauche, ce qui le décale
sur écran large. Il faut le caler sur le container principal. » Mesuré à 2000 px : logo à 16 px,
`#inner-main` de 391 à 1591.

**Transverse** parce que la barre sert toutes les pages du Jeu. Ce que je touche, et rien d'autre :
`public/pz/m0/coque.css` (la règle `#top-bar.pz-shell-v2`, au-dessus de 992 px seulement),
une règle scopée dans `public/pz/m0/echanges.css` (seule page qui élargit son conteneur, 48 → 1948)
et une section de `verifier_coque_m0.rb`. **Aucun gabarit, rien sous 760 px.** PR à suivre.

Ensuite, séparément : la note de Codex du 10 septembre demandait que les flèches **haut/bas**
ne soient plus interceptées par la rangée d'onglets (défilement conservé). `gestes.js` les
prend encore (l. 142-144 sur preprod@66e84db) — je le corrige dans une seconde PR.

— poste fixe

---

## 11 septembre — Deux PR poussées, indépendantes : #194 (barre calée) et #195 (flèches)

- **[#194](https://github.com/PointZero2050/pointzero-app/pull/194)** — la barre du bureau se
  cale sur `#inner-main` au-dessus de 992 px, comme annoncé plus haut ; `/echanges` et tout ce qui
  est sous 992 px restent au pixel près comme avant. Nouveau `verifier_coque_m0` §11. Relevé
  avant/après dans la PR.
- **[#195](https://github.com/PointZero2050/pointzero-app/pull/195)** — `gestes.js` ne prend plus
  haut/bas (relecture Codex sur #191) ; deux assertions dans `verifier_marelle`, hors du
  `if multi`. ⚠️ Codex demande la recette « gauche/droite et défilement haut/bas **sur la vraie
  page** » : une multigeste au deuxième geste, après déploiement — le DOM reconstruit ne prouve
  que le script.

Aucun fichier commun entre #193, #194 et #195 ; aucune ne touche un gabarit.

— poste fixe

---

## 11 septembre — Je prends la page parcours en pleine largeur (demande de Boris, chantier transverse)

Boris demande le portage strict de `parcours-lineaire-m0-cible?view=journey` sur
`/parcours/point-zero-monde-0` : cover pleine largeur collée au menu, fond fixe derrière le fil,
fil plein sur les expériences faites qui devient un pointillé animé pour celles à venir, et retrait
de « Passage vers la suite », « À propos de ce parcours » et « Ce que ce parcours peut mettre en
mouvement ».

**Transverse** parce que `/jeu` rend la même vue avant la clôture, et parce que quatre de tes bancs
lisent les blocs qui partent. Ce que je touche : `journeys/_show.html.haml`, `journeys/_rite`
(qui n'aura plus d'appelant), `public/pz/m0/parcours.css`, une image de fond dans `public/pz/m0/`,
et dans la même PR `verifier_marelle` (§6, §11, bornes `map-section`/`journey-about`),
`verifier_cartes_chapitres` (§1, rite, §5) et `verifier_accueil_m0` (l. 897). **Aucun service,
aucune route** : `JourneyProgress` range déjà l'Atelier et ses préparations dans le chapitre 3,
la vue cessera seulement de les en sortir.

— poste fixe
