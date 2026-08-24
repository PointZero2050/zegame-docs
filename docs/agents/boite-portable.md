# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

**11. Les quatre branches dormantes : trois mortes, une VIVANTE — et il y en avait 69.**

Tu as eu raison de ne pas fusionner à ma place. Verdict, avec la preuve à chaque ligne :

| branche | SHA | verdict |
|---|---|---|
| `claude/fiche-experience-coque` | `c492e68` | morte — `git cherry` : appliqué · `.meta-nav` présent 9× dans `experience.css` |
| `claude/historique-complet` | `bf357d8` | morte — ses 3 fichiers sont dans preprod |
| `claude/illustrations-declarees` | `b8bc46c` | morte, **et c'était la plus dangereuse malgré son conflit** : ses 4 `.webp` sont dans l'arbre et servis (200, 188 Ko), et son banc a évolué en un fichier SÉPARÉ. La fusionner aurait écrasé `verifier_illustrations_m0.rb` — 164 lignes — par une version antérieure de ce qui est devenu `verifier_illustrations_declarees.rb`. Les deux coexistent aujourd'hui. |
| `claude/roue-en-liste-mobile` | `2224a84` | **VIVANTE** — voir ci-dessous |

**⚠️ LES TROIS DÉFAUTS DU TÉLÉPHONE DE BORIS SONT TOUJOURS EN LIGNE.** Mesuré sur
`origin/preprod` avant de toucher au fichier : le filigrane est encore à `min(118vw, 600px)`,
le voile encore en `inset: 0 / place-items: center / overflow: auto`, et le bloc sous 480 px
ne porte que `.pz-m0-liste { gap: 9px }`. Aucun des trois correctifs du 20 août n'a jamais
atteint la préprod : ils y sont restés absents **cinq jours**, sans que rien ne le signale.

Réappliqués sur la préprod d'aujourd'hui, pas fusionnés — [PR #87](https://github.com/PointZero2050/pointzero-app/pull/87),
**les cinq contrôles au vert**. Et cette fois **le banc les garde** : quatre assertions dans
`verifier_coque_m0`, dont la première ne dépend d'aucune mesure — aucune largeur de la coque
ne peut dépasser le viewport. Vérifiées dans les deux sens : elles rougissent sur le
`coque.css` d'avant, elles passent sur celui-ci.

**⚠️ ET IL Y AVAIT 69 BRANCHES `claude/*`, PAS QUATRE.** J'ai mesuré chacune :
`git rev-list --count origin/preprod..<branche>`. **Une seule** était en avance —
`roue-en-liste-mobile`. Les 68 autres étaient entièrement contenues dans la préprod, donc
incapables de réintroduire quoi que ce soit, mais c'étaient 68 fois le piège que tu décris.

Supprimées, plus `portage-inscription-publique` (fusionnée). L'origine porte désormais **six**
branches : `main`, `preprod`, mes deux PR ouvertes (#86, #87), `roue-en-liste-mobile` que je
garde jusqu'à la fusion de #87, et celle de dependabot.

**Ce qui reste à faire quand tu prends #87** : confirmer sur un vrai téléphone. Le défaut du
vide au-dessus du menu ne se reproduit pas dans un panneau de vérification, qui n'a pas de
barre d'URL rétractable — il est diagnostiqué par la géométrie de la capture de Boris et
corrigé par le remède standard. Et supprimer `claude/roue-en-liste-mobile` après fusion.
