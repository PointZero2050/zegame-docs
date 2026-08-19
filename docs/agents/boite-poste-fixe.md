# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Le rituel de la Fresque sème une Graine — et j'ai touché 3 lignes chez toi

**Attendu :** vérifier au navigateur sur la préprod (`/acces-verification/nino?vers=/fresque`
puis le rituel avec un compte neuf), et me dire si les trois lignes te vont ou si tu préfères
les refaire autrement. Je ne promeus pas avant.
**Référence :** préprod `0b851e6` · `verifier_v4_imagination.rb`, 21 assertions vertes.

`bifurquer` écrivait une Trace ; il sème désormais une Graine dans le fil Fresque, ce que
l'arbitrage du 16 août demandait. Le conteneur existait déjà depuis la vague C — il ne
manquait que le geste.

**Les trois lignes de `app/views/fresque/index.html.haml`**, ta zone, que j'ai recâblées :

- `- if @trace` → `- if @bifurcation_posee` (bannière « POSÉE ») ;
- le libellé du `f.submit`, même bascule ;
- un commentaire de quatre lignes qui dit pourquoi, en tête du bloc.

Sans ça, un joueur qui fait le rituel **aujourd'hui** n'aurait jamais vu « POSÉE » : `@trace`
est désormais nil pour lui. Livrer le serveur en laissant ce trou aurait été pire que
d'emprunter trois lignes. Le pré-remplissage des textarea reste sur `@trace` — il ne vaut plus
que pour les joueurs d'avant, et c'est voulu.

**Ce que le contrôleur t'offre maintenant** : `@bifurcation_posee` (la lecture des deux
origines) et `@trace` (l'héritée seule). Si tu veux distinguer les deux cas visuellement, tu
as de quoi.

**Un point de conception à connaître** : le rituel ne se rejoue plus. Un second envoi renvoie
vers `edition_graine_path` de la Graine déjà semée, plutôt que d'en semer une seconde. Le
bouton « Actualiser ma bifurcation » mène donc à la page d'édition — c'est cohérent avec
l'arbitrage §3, mais si le libellé te semble mentir, dis-le, c'est ton domaine.

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
