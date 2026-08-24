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

**12. Le portage est fait — la promotion est débloquée. [PR #86](https://github.com/PointZero2050/pointzero-app/pull/86).**

`content/articles/politique-de-confidentialite.md` est synchronisé sur `9a7eea8` : version
**1.0**, entrée en vigueur au **24 août 2026**, module de cookies au futur, chemin de fermeture
retiré. 384 lignes servies contre 453 au document de travail — les sections internes restent
hors ligne, vérifié.

**⚠️ ET TA MESURE ÉTAIT INCOMPLÈTE, COMME LA MIENNE : IL Y AVAIT QUATRE TROUS, PAS TROIS.**
Le §9 portait `[lien « Gérer mes cookies » à ajouter si nécessaire]` — même nature, autre
formule. Ton `grep -c "à compléter"` et mon assertion le manquaient tous les deux, pour la
même raison. Codex l'a fermé au passage.

La §7 compte donc désormais **tout crochet resté dans le HTML rendu**, pas une formule
particulière. C'est le troisième cas du même défaut aujourd'hui : la mienne guettait
`/users/sign_up` quand la porte s'appelait `/inscription`, la tienne interrogeait la table des
routes quand la page était servie par le catalogue. Aucune ne devient fausse — elles
deviennent hors sujet.

Tu avais raison sur la double assertion du §13 : je l'ai gardée, retournée. Elle garde
maintenant la porte réelle (courriel) et **le temps du verbe** — si quelqu'un repasse la
commande autonome au présent sans que la route existe, elle rougit.

**Vérifié dans les deux sens** : sur le texte porté, 0 crochet / courriel présent / futur
présent. Sur celui d'avant, 4 crochets et aucun futur.

**Fausse alerte écartée** : Codex a perdu les deux espaces de fin entre « Version » et
« Entrée en vigueur ». Sans conséquence — `kramdown-parser-gfm` a `hard_wrap` actif, la page
coupe déjà à chaque retour de ligne source. Rien à corriger.

Reste #87 (les trois défauts du téléphone), cinq contrôles au vert, et la suppression de
`claude/roue-en-liste-mobile` après sa fusion.

**13. [PR #88](https://github.com/PointZero2050/pointzero-app/pull/88) — quatre défauts des parcours de découverte (revue de Boris).**
Terminologie canonique (« Le Sas du Point Zéro » → « Les parcours de découverte du site »),
les vingt liens de cartes pointés sur les seuils (`?screen=…`) au lieu des accueils en
boucle, « Effacer mes traces » qui agit enfin sur les cinq clés et montre son résultat,
portraits pixel art des guides dans les médaillons. §6 ajoutée à `verifier_sas_vers_le_jeu`
— à rejouer au déploiement, comme d'habitude. Zone : vues sas, public/sas, aucun contrôleur.
La refonte du design et les illustrations sont relayées à Codex (demande de Boris).
