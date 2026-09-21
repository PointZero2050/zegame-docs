# Boîte du portable

⚠️ **Vidée le 22 septembre 2026 (matin).** Traité depuis le 20 : **E8 « Mon premier circuit vivant »** côté serveur (`3d53e40`) et sa vue (#329) ; **le Conseil Oméga 2.0** — la version du poste fixe (#330) remplace mon moteur 2.0, avec la branche `circulation`, le `goto` des sections typées, la garde de l'Atlas, l'écran ROLE (Codex) et les mots de Codex ; **E1 en trois étapes** (`04ab894` : six points serveur, la visite guidée de l'accueil `GET /jeu/visite` + `POST /jeu/visite/terminer`, `accomplie:`/`transition:`/`cta_reprise:`, cinq bancs réécrits) et sa vue (#340 — trois commits, le seuil compris —, #341 : `23c1e02`, la conclusion de Codex exposée) ; **les lots mobile 1 à 4** (#328, #331 → #335), l'échelle typographique et le `h2` sans `!important` ; #336, #338, #339 et la dette Brakeman (0 avertissement) ; les empreintes des illustrations d'articles ; huit états de démonstration `@demo.pz` (`scripts/etats_de_demonstration.rb`) ; recette transversale **192/192** sur `c47d3dd`, puis bancs ciblés verts à chaque fusion. Préprod **`23c1e02`** ; production **`34a167d`**. Rien n'attend ici.


Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#318 à #330) et les boîtes des autres.

**Une leçon de plus, et elle a coûté une demi-journée** : le poste fixe et moi avons écrit le même Conseil en parallèle. Sa boîte disait « je porte, il me faut six lignes » pendant que je servais un moteur entier depuis un plan validé la veille — deux arbitrages de Boris m'étaient parvenus par lui, pas par ma boîte. **Avant un chantier de ma zone qui touche la sienne, relever sa boîte À LUI (`boite-poste-fixe.md`) aussi, pas seulement la mienne** : c'est là que vivent les décisions prises avec Boris pendant que je construis.

## Ce qui reste ouvert — et chez qui

- **Boris — la production ATTEND IMMATERIA, E8 ET LE CONSEIL 2.0, tous trois en préprod.** À lui de
  **tester** (`/jeu` → l'Enfant répond ; « Rejoindre Immateria » → la traversée → le retour, le badge une
  fois ; la fiche d'E8 → la vidéo → « Composer mon circuit » → le sceau → le retour ; la fiche d'E15 →
  le Conseil : le siège, une archive, trois gestes, l'Atlas, conclure) et de dire **la promotion
  d'ensemble** (M0 + 18 verbes + Immateria + l'avatar + E8 + le Conseil 2.0). **Le chiffrage d'E8** :
  la colonne dit 5 min, la cible de Codex 6 à 8 — à lui. **Les textes fixes de l'avatar** et les mots
  portés au YAML d'E8 et du Conseil (registre de Codex) : Codex écrit, Boris valide. Restent
  chez lui : le retest du M0 ; la relance des paiements Festival ; les dependabot (#226, #228, #315,
  #316) ; **relever le plafond global (20 $/jour) avant le Festival**.
  ⚠️ À la promotion, les 18 verbes se jouent EN PRODUCTION comme en préprod : sauvegarde vérifiée →
  migration → **simulation d'abord** → `ECRIRE=oui` → journal **hors** du conteneur → B est déjà dans
  le code. Et la clé Anthropic de la production doit exister (l'avatar répond `repli` sans elle — le
  script joue, personne ne le voit, mais Boris le verra).
- **Codex** : ses mots sont portés (E8, le Conseil et son écran ROLE, la fiche d'E15, E1 en trois
  étapes) ; **E1** — l'introduction courte, la restitution et « Désir activé » n'ont pas de logement (dit
  dans sa boîte), les mots du chemin de fer à l'écran attendent son mot ou celui de Boris ; les 14 autres
  cas du §9 de l'avatar en opt-in ; la carte Puissance après le regroupement ; l'état `empty` de la
  Carte du Seuil.
- **Poste fixe** : E1 est complète (#340 avec le seuil) ; **le sprite du visage en seconde copie** (`experience.css` ↔ `accueil.css`) — extraction à faire ensemble, avec sa mesure avant/après, à sa fenêtre ; l'écran `role` du Conseil
  (`_section` en attendant son portage) ; le Conseil est fusionné sur SON graphe (#330), son en-tête
  immersif reste à lui ; la vue d'E8 (#329) — réordonner les relais avec `types_privilegies` ; les huit
  états jetables (`six`, `mentor`, `huit`, `conseil`, `guide`, `espace`, `accompli`, `jumeau` `@demo.pz`)
  sont là pour ses mesures ; le sas du mentor lit `@accueil[:mentor]` (posé).
- **Moi, à la relecture de ses prochaines PR** : `ruby -c` des bancs avant la fusion, rejouer
  `verifier_circuit_vivant`, `verifier_conseil_circulation`, `verifier_accueil_immateria`, `verifier_accueil_deux_plans`,
  `verifier_avatar_reponse`.
- **Moi, ensuite** : le commentaire dans `Challenge` disant que les exports gardent `name` (poste fixe, pas urgent).
- **Moi, à la promotion** — la liste, tenue à jour :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : **`referentiel_18_verbes_schema`** (puis le REGROUPEMENT, qui est un SCRIPT : simulation
    d'abord, `ECRIRE=oui` ensuite, journal hors conteneur ; pas une migration), **`cartes_du_seuil`**,
    **`l_avatar_parle_par_claude`** (le journal de coût de l'avatar, le cache sur les deux autres tickets,
    la cascade des propositions), **`le_premier_circuit_vivant`** (E8), `mentor_messages.challenges_user_id`,
    `recus_omega.rappel_le`, `propositions_de_graine.challenges_user_id`, plus les anciennes
    (`recus_omega`, `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb`, **`mise_en_service_e1_trois_etapes.rb`** (l'accroche d'E1) ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
    **les huit JPEG** de #325/#326 (`public/`, dans git) ; **les quatre portraits du Conseil**
    (`/home/deploy/pz/epoque/co-p-{sonia,imane,nadia,etienne}.jpg`, bind mount — hors git, à recopier à la main) ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`, `sas.yml`, `conseil_omega/*.yml`) ;
  - ⚠️ **`public/` est servi un an en cache** : l'ancien tutoriel vivait aux mêmes adresses, les
    empreintes du poste fixe (#311) le couvrent — vérifier au navigateur, en production, qu'aucune
    requête nue ne part vers `/pz/immateria/` ;
  - ⚠️ **`ANTHROPIC_API_KEY` en production**, sinon l'avatar est muet (repli) — et le plafond global.
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
