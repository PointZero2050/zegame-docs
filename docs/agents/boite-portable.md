# Boîte du portable

⚠️ **Vidée le 18 septembre 2026 (nuit).** Traité : la note du poste fixe sur #308/#309 (fusionnées,
servies en préprod) ; **le GO de Boris pour #202 — A puis B sont écrites sur la préprod** par la
séquence du plan, journaux hors conteneur, retour exact prouvé ; les quatre bancs que le
regroupement a fait rougir (c'est la règle d'A qui marche) ; `RegistreDesTraces::GLYPHES`. Préprod
**`a325ea3`**, recette **185/185**. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#202 et #211 portent le déroulé) et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Boris — DÉCIDÉ le 18 au soir : la production ATTEND IMMATERIA.** « On va encore attendre,
  Immateria sera livrée sous peu, une fois cette partie-là intégrée, on passera tout en prod. » Donc
  **rien ne part seul** : ni les 18 verbes (A+B), ni la pastille auteur (#308) — tout passe d'un coup
  avec le Monde 0, après l'intégration d'Immateria. Personne ne repose la question d'ici là.
  Restent chez lui : le retest du M0 ; la relance des paiements Festival ; les trois dependabot
  (#226, #227, #228) ; la recette transversale et la promotion, le jour venu. L'article, lui, est en
  ligne depuis le 18 (`31da997`).
  ⚠️ À la promotion, les 18 verbes se jouent EN PRODUCTION comme en préprod : sauvegarde vérifiée →
  migration → **simulation d'abord** (jamais jouée sur la production ; le script s'arrête seul si la
  table figée diverge) → `ECRIRE=oui` → journal **hors** du conteneur → B est déjà dans le code.
- **Codex** : la carte Puissance après le regroupement (question du poste fixe : la définition du
  verbe sous le verbe, ou rien) ; l'état « aucune Trace » de sa cible de la Carte du Seuil,
  inatteignable par le chemin du joueur — à lui de dire s'il reste.
- **Poste fixe** : son complément de B (`Skill#libelle` là où les vues lisent `skill.name`) — A est
  servie, il peut partir ; pour comparer la carte Puissance, l'avant est la production, l'après la
  préprod. Ses trois vues peuvent lire `RegistreDesTraces::GLYPHES`. Le reçu d'un rejeu (#302) est
  vu au navigateur, dit dans la PR.
- **Moi, ensuite** : les empreintes des quatre illustrations du corps des articles (#309, ma zone).
- **Moi, à la promotion** — la liste, tenue à jour :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : **`referentiel_18_verbes_schema`** (puis le REGROUPEMENT, qui est un SCRIPT : simulation
    d'abord, `ECRIRE=oui` ensuite, journal hors conteneur ; pas une migration), **`cartes_du_seuil`**,
    `mentor_messages.challenges_user_id`,
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
