# Boîte du portable

⚠️ **Vidée le 20 septembre 2026 (suite).** Traité : les neuf notes du poste fixe (19 au soir, 20) — #318, #319, #320, #321, #322
fusionnées (`91c3be9`, `f0d7d7e`, `751b515`), **l'Enfant parle par Claude** (`e1d3290` : `AvatarReponse`,
`POST /jeu/avatar`, l'usage `avatar`, la limite du jour, la mémoire de session, la vigilance, le journal de
coût), ses trois défauts du robinet LLM réparés (filtre des logs, clé étrangère des propositions, le cache
dans le plafond), son point serveur sur l'éveil **tranché par Boris** (« la popup de gains puis le retour à l'accueil ») et porté. Préprod **`ba826ec`** (puis #321, `@accueil[:mentor]`, la sortie d'E1 vers l'accueil sur le mot de Boris — bancs ciblés verts, recette en cours), recette
**189 bancs : 186 verts + Stripe hors portée, 2 rouges de bancs réparés et rejoués verts** ; production **`34a167d`**. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#318 à #322) et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Boris — la production ATTEND IMMATERIA, et Immateria est en préprod, Claude compris.** À lui de
  **tester** (`/jeu` → l'Enfant répond ; « Rejoindre Immateria » → la traversée → le retour, le badge une
  fois) et de dire **la promotion d'ensemble** (M0 + 18 verbes + Immateria + l'avatar). La sortie d'E1 est
  tranchée et portée : l'éveil de Désir, le reçu des 5 Ω par le CTA de la fiche, puis l'accueil (`ba826ec`).
  **Les textes fixes de l'avatar** (vigilance, plafond, phrases lues) sont provisoires : Codex écrit,
  Boris valide. Restent
  chez lui : le retest du M0 ; la relance des paiements Festival ; les dependabot (#226, #228, #315,
  #316) ; **relever le plafond global (20 $/jour) avant le Festival**.
  ⚠️ À la promotion, les 18 verbes se jouent EN PRODUCTION comme en préprod : sauvegarde vérifiée →
  migration → **simulation d'abord** → `ECRIRE=oui` → journal **hors** du conteneur → B est déjà dans
  le code. Et la clé Anthropic de la production doit exister (l'avatar répond `repli` sans elle — le
  script joue, personne ne le voit, mais Boris le verra).
- **Codex** : les quatre textes de l'avatar (vigilance, plafond, les seize phrases lues, « je vis dans
  le présent ») ; les 18 cas du §12 avec leur réponse attendue (le banc a sa §9 réelle derrière
  `AVATAR_LLM_TEST_REEL=1`) ; la carte Puissance après le
  regroupement ; l'état `empty` de la Carte du Seuil.
- **Poste fixe** : le sas du mentor lit `@accueil[:mentor]` (posé) ; la fluidité d'E1 sur un vrai
  téléphone (plafond de `DEF` à 2 si la cave saccade). Entrée envoie (#321) ; la pose `reflechir` sans
  transition est voulue.
- **Moi, à la relecture de ses prochaines PR** : `ruby -c` des bancs avant la fusion, rejouer
  `verifier_accueil_immateria`, `verifier_accueil_deux_plans`, `verifier_avatar_reponse`.
- **Moi, ensuite** : les empreintes des quatre illustrations du corps des articles (#309, ma zone) ;
  le commentaire dans `Challenge` disant que les exports gardent `name` (poste fixe, pas urgent).
- **Moi, à la promotion** — la liste, tenue à jour :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : **`referentiel_18_verbes_schema`** (puis le REGROUPEMENT, qui est un SCRIPT : simulation
    d'abord, `ECRIRE=oui` ensuite, journal hors conteneur ; pas une migration), **`cartes_du_seuil`**,
    **`l_avatar_parle_par_claude`** (le journal de coût de l'avatar, le cache sur les deux autres tickets,
    la cascade des propositions), `mentor_messages.challenges_user_id`,
    `recus_omega.rappel_le`, `propositions_de_graine.challenges_user_id`, plus les anciennes
    (`recus_omega`, `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb` ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`, `sas.yml`) ;
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
