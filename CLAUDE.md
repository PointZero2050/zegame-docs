# zegame-docs — Contexte pour Claude Code

Dépôt de DOCUMENTATION partagée du projet Point Zéro (Festival du 1er octobre 2026).
Il ne contient aucun code exécutable : de la vision, des canons éditoriaux, des analyses
d'impact et les boîtes aux lettres des agents.

## ⚠️ Le serveur de travail n'est PAS celui d'anciens documents

- **L'application d'aujourd'hui** est `pointzero-app` (dépôt privé
  `PointZero2050/pointzero-app`), déployée sur **167.233.210.57** :
  préprod https://preprod.167-233-210-57.sslip.io · production https://new.pointzero2050.com.
  Le portable porte seul la clé SSH et tous les déploiements.
- **`vibe.ze.game` est l'ANCIENNE sandbox Rails, GELÉE** (app `zegame-app`, gem
  `mathieu_core`, Capistrano). N'y toucher que si Boris le demande explicitement. Toute
  instruction de ce dépôt qui parle de `vibe.ze.game`, de `mathieu_core` ou de Capistrano
  décrit l'ancienne sandbox, pas le code d'aujourd'hui.

## S'orienter dans ce dépôt

- `docs/agents/` — **les boîtes aux lettres inter-agents** et leur protocole (README.md).
  Début de session : `git pull --ff-only`, puis relever SA boîte. Chacun n'écrit que dans
  les boîtes des autres et ne vide que la sienne.
- `docs/vision/` — canons produit et éditoriaux (Codex y fait foi). La répartition des
  rôles entre agents : `docs/vision/repartition-agents-phase-2.md`.
- `docs/pedagogie/assets/atlas/` — les versions canoniques des médaillons Atlas.
- Les `.md` de ce dépôt se citent par URL GitHub complète, jamais par chemin local.

## Conventions

- Commits préfixés `[Claude]` (Codex : `[Codex]`), avec
  `Co-Authored-By: Claude <modèle> <noreply@anthropic.com>`.
- GitHub est la source de vérité — jamais la copie Dropbox. Après un soupçon de conflit :
  `git fsck`, comparaison avec `origin`, purge des débris `*conflit*`.
- Les prototypes HTML vivent dans `zegame-prototypes` (un dossier par prototype).
