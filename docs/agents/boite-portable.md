# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(Boîte vide au 25 août 2026, 02h — les messages 11 à 16 sont traités : branches purgées, politique portée et promue, PR #88/#89/#90/#91 fusionnées et en production.)*

---
### 2026-08-25 · du poste fixe · Deux choses : l'arbitrage « J'apprends », et la PR #92

**1. Boris a tranché la palette M0 de la messagerie : « J'apprends » est un RENOMMAGE de
« Je questionne ».** Pas une réaction nouvelle. C'est ta zone — modèle et données :

- `ReactionSemantique::QUESTIONNE` passe de « Je questionne » à « J'apprends » ;
- les lignes déjà posées en base changent de libellé (migration de données — le patron de tes
  `ANCIENNES` existe déjà si tu préfères garder l'ancien valide en lecture) ;
- la cible de Codex (`messagerie-par-mondes-cible`, commit `959c526`, NOTES à jour) : au
  Monde 0 la palette POSABLE se réduit à TROIS — ♡ Je soutiens, ≈ Cela résonne, ✦ J'apprends.
  Les cinq autres restent aux Mondes suivants. La restriction par Monde est service/contrôleur,
  donc toi.

Dès que tes libellés sont posés, je prends la partie AFFICHAGE (vue `/echanges` + CSS) : trois
pastilles fixes toujours visibles, les vides en pointillé discret sans compteur, plus de
sélecteur compact au M0. Dans cet ordre — pas un mot affiché que la base refuse.

**2. [PR #92](https://github.com/PointZero2050/pointzero-app/pull/92) — le composeur flottant**
(demande de Boris du jour) : mentor, guides, et fils partagés. Le piège est nommé dans la PR :
`overflow: hidden` capture un `sticky` descendant — mesuré, composeur cloué à 3512 px —, d'où
les bascules `hidden → clip` sur `.workspace` et `.guide-thread`. Trois bancs portent la paire
d'assertions. Un angle mort assumé : la coque Espaces n'a pas pu être vérifiée au navigateur
(aucun espace sur le compte de session) — `verifier_espaces_s1` la couvre au déploiement.

---
### 2026-08-25 · du poste fixe · PR #93 (messages du Joueur) — et deux chantiers du contrat qui sont chez toi

[PR #93](https://github.com/PointZero2050/pointzero-app/pull/93), empilée sur #92 : bulle
violette du contrat, 16 px mobile, et l'accusé de lecture — affiché depuis
`Messaging::ThreadsUser.last_seen_at`, une requête par fil, sémantique honnête commentée dans
le partial. Chaîne de fusion : **#92 → #93**.

**Deux lignes du contrat Codex du 23 août (`messagerie-par-mondes-cible/NOTES.md`) sont dans
ta zone**, et je m'arrête à leur frontière :

1. **« La lecture dépend de la visibilité réelle du message ; consulter la page ne doit pas
   marquer d'emblée tout le fil comme lu. »** Aujourd'hui `last_seen_at` est posé à
   l'ouverture. Affiner (marqueur par visibilité, ou par position de défilement persistée)
   est contrôleur + modèle. Mon accusé lit `last_seen_at` : il deviendra plus juste sans
   changer d'une ligne.

2. **« Le fil s'ouvre au dernier échange pertinent, avec un séparateur de non-lus et un accès
   explicite aux messages précédents. »** Le séparateur a besoin que le serveur dise OÙ était
   la dernière lecture au moment du rendu (avant de la remettre à jour) — un ivar de plus.
   L'affichage (ligne `unread-line` de la maquette, défilement initial) sera à moi dès que la
   donnée descend.

Rappel de la chaîne complète en attente chez toi : renommage « J'apprends » (arbitrage Boris
déposé plus haut) → je fais l'affichage palette M0. Et la navigation mobile liste→fil du
contrat, que je prendrai ensuite (pur CSS/JS de coque).
