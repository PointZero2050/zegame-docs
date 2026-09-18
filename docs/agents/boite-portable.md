# Boîte du portable

⚠️ **Vidée le 18 septembre 2026 (soir).** Traité : les sept notes que mon `cp` de la veille avait
effacées (restaurées le matin, `1d21773`) et les deux arrivées ensuite. C'est-à-dire : #302, #303,
#304 et #305 fusionnées à la main et servies ; **la Carte du Seuil côté serveur** (`33e8c59`), sous
les noms du poste fixe et la règle de Codex ; ses mots du rang 4 (`432ca4a`) ; la déclaration morte
d'E13 (`b8ceaab`) ; puis #306 et #307 (`d9c0f00`). Préprod **`d9c0f00`**, recette **184/184** (sur
`6c695a3`, avant ces deux petites fusions — bancs ciblés verts ensuite). Rien n'attend ici.

⚠️ **Le GO de Boris pour #202 est enregistré, et c'est le premier travail de la prochaine session** —
pas la fin de celle-ci : schéma additif, script, simulation, puis B (#211) qui réécrit `sas.yml`
après mes clés du 18 — « pas de conflit textuel ne veut pas dire des références encore justes ». La
séquence est dans la PR : https://github.com/PointZero2050/pointzero-app/pull/202#issuecomment-5729080435

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#304 porte le contrat servi) et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Boris** : ~~la mise en ligne de l'article~~ **faite le 18 au soir, seule, sur son mot** — `main`
  `31da997`, quinze fichiers identiques à la préprod, rien d'autre ; le retest du M0 ; la relance des
  paiements Festival ; les trois dependabot (#226, #227, #228) ; la recette transversale et la
  promotion du Monde 0 (424 fichiers attendent).
- **Codex** : l'état « aucune Trace » de sa cible de la Carte du Seuil est inatteignable par le
  chemin du joueur (choisir son mentor est déjà une Trace) — à lui de dire s'il reste.
- **Moi, en tête de la prochaine session** : **#202** (GO de Boris), puis #211 relue contre `sas.yml` ;
  `RegistreDesTraces::GLYPHES` (les quatre signes vivent trois fois dans les vues — demande du poste
  fixe, ma zone).
- **Poste fixe** : le complément de B (`Skill#libelle`), qu'il empile sur A. Le reçu réel d'un rejeu
  (#302) est vu au navigateur sur un compte jetable, dit dans la PR.
- **Moi, à la promotion** — la liste, tenue à jour :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : **`cartes_du_seuil`**, `mentor_messages.challenges_user_id`,
    `recus_omega.rappel_le`, `propositions_de_graine.challenges_user_id`, plus les anciennes
    (`recus_omega`, `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb` ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`, `sas.yml`).
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

## Comment je vide cette boîte, désormais

**Jamais un `cp` ni un `Write` par-dessus le fichier.** Le 13 puis le 18 septembre, un brouillon
recopié a effacé les notes arrivées entre mon `fetch` et mon écriture — deux, puis sept. Le procédé
est maintenant un script (`vider_ma_boite.py`, dans mon scratchpad) qui lit le fichier VIVANT, le
découpe à chaque titre, et REFUSE d'écrire si un seul bloc n'est pas dans la liste de ce que j'ai
traité. Puis `git diff` : les seules lignes supprimées doivent être des notes traitées ou les
miennes.

## Quatre leçons, parce qu'elles ont coûté

**Une assertion d'absence ne vaut que si l'on prouve d'abord que la chose aurait pu être là**
(15-16 septembre, et encore le 18). Quatre bancs verts ne gardaient rien : un bandeau mesuré sur une
fiche verrouillée (donc un 302) ; des ancres comptées en guillemets doubles quand le helper en rend
des simples ; « pas de popup au rejeu » qui lisait un reste de flash ; un retour après correction
mesuré sur le seul cas qui ne l'intéressait pas. Trois ont été révélés en RETIRANT du code. Le 18,
deux de plus : `verifier_accord_des_verbes` §4, muet depuis que le Sas ne porte plus de verbes, et
mon propre `verifier_cles_du_sas`, vert sur l'ensemble vide jusqu'à ce que le COMPTE le dise.

**Une preuve ne vaut que dans le régime PAR DÉFAUT** (17 septembre, deuxième fois après E7 le 12).
Le geste mentor devait se prouver par « la question du joueur » — mais avec la mémoire fermée, le
réglage que personne ne change, ce message n'est JAMAIS persisté : seule la ligne de coût existe.
**Avant d'adosser une preuve à un fait, demander qui l'écrit, et sous quels réglages.**

**Le M0 se mesure presque entièrement, et les décors des bancs doivent suivre** (18 septembre).
Deux bancs se sont cassés non parce qu'ils avaient tort, mais parce que leur DÉCOR n'existait plus.
Un décor écrit comme une liste de cas vieillit à chaque arbitrage ; un décor écrit comme une règle
survit. Et quand un décor se choisit par mesure, il faut qu'il exige ce que le banc teste. Le soir
du 18, le dernier geste sans porte du Monde 0 a eu le sien : **il n'en reste aucun.**

**Quand un banc et une page se contredisent, mesurer ce que la page rend vraiment** (18 septembre,
deux fois en une heure). Dans les deux cas la page avait raison. Une recopie ne se garde pas toute
seule : quand une même vérité vit à deux endroits, ce qu'il faut livrer n'est pas la seconde copie,
c'est l'assertion qui les compare. Et le soir : un état de maquette peut être **inatteignable** —
choisir son mentor est déjà une Trace, donc « aucune Trace » n'arrive jamais à E19. On le dit, on
ne le fabrique pas.
