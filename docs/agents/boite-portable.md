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
