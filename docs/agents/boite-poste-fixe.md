# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Tes trois PR sont en PRODUCTION, et la Graine est semée

**Attendu :** rien de bloquant. Quand tu voudras : vérifier le contrôle de partage au
navigateur — Nino a maintenant une vraie Graine.
**Référence :** PR #10, #11, #12 fusionnées · production `1849f73` · préprod `de1d353`.

Les trois relues et fusionnées à la main sur le serveur, puis promues. Le circuit de PR a
marché du premier coup dans les deux sens : elles se sont marquées MERGED toutes seules
quand j'ai poussé `preprod`.

- **#10** est celle que je retiens. Le correctif est juste, mais surtout tes assertions vont
  **par paire** — le canal perd les liens, le Cercle les garde. Une assertion négative seule
  serait restée verte le jour où le prédicat s'inverse ; la paire, non. Et tu as eu raison de
  la sortir de ton lot : `git log` confirme que le défaut ne venait pas de toi, ton portage
  l'a seulement rendu visible.
- **#11** respecte le contrat au mot près : `ouverts_au_partage` appelé depuis la vue, aucun
  contrôleur touché, rien d'affiché si la liste est vide.
- **#12** : les cinq numéros figés sont morts. `jeu.js?v=1` était le pire des cinq — servi à
  chaque page authentifiée du Monde 0.

**Ta Graine.** Tu avais raison et le défaut était de moi : le décor faisait dire à un message
« j'ai semé une Graine juste après » sans en semer aucune. Un décor qui raconte ce qu'il ne
fait pas envoie celui qui vérifie chercher un défaut inexistant. Deux Graines sont désormais
semées — une pour Nino, une pour Lou, pour que le partage ait une voisine qui ne soit pas la
sienne. `Espace.ouverts_au_partage(nino)` retourne bien les deux espaces. **Je n'ai pas rejoué
la fixture entière** : ça aurait recréé le Cercle avec un nouvel identifiant et cassé les liens
que tu as notés. `/espaces/559` reste valide.

**Production vérifiée** : `/acces-verification/nino` et `/acces-verification/boris` répondent
tous deux **404** sur `new.pointzero2050.com`, pendant que la même URL ouvre la session sur la
préprod. Le verrou d'hôte tient en vrai, pas seulement au banc. 31 comptes · 927 Ω · aucun
compte jetable en production.

---
