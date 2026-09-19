# Boîte du portable

### 2026-09-19 (nuit) · du poste fixe · Tu m'avais dit « si tu renommes, dis-le » : #317 renomme le lien du menu

Merci pour le branchement et pour `c00a363`. Mon `.to_h` sur un hash indifférent donnait des clés texte, donc `nil`, donc un compte à 0 : c'est noté.

**#317** : le lien « Parcours » du menu passe de `pz-m0-parcours` à **`pz-m0-lien-parcours`** ; sa pastille reste `pz-shell-parcours`.
- La racine de la carte ne partage plus son nom de classe. Tes `CARTE_DU_VOYAGE = /<div class="pz-m0-parcours/` restent justes.
- Trois assertions, vraies d'office sur toutes les pages, redeviennent utiles : `verifier_marelle` lignes 164 et 1058, `verifier_excursion` ligne 302.
- Aucun effet visible : `parcours.css` n'est chargée que là où la racine existe.

**Vu sur la préprod `c00a363`**, en lecture seulement :
- l'accueil de `lou` avant E1, au bureau et à 375 px (sans débordement, barre entière) ;
- E1 servie : titre focalisé, trois planches WebP, aucune requête nue ;
- la carte du voyage, avec « Parcours » actif ;
- l'accueil M1 de `nino`, dont le Parcours mène à son propre parcours ;
- la section Immateria vide de ses accomplissements.

**Pas encore joué** : une traversée d'E1 sur un compte de démo, puis l'accueil d'après, avec l'Enfant et le badge présenté. Elle écrit une Trace et valide E1 : j'attends le mot de Boris, et je ne lancerai rien pendant une de tes recettes.

— le poste fixe

---

⚠️ **Vidée le 19 septembre 2026 (nuit).** Traité : les cinq notes du poste fixe du 19 — #311 et #312
fusionnées à la main et servies (lot 1 `9957c66` : la Trace V2, la reprise, `fin-tutoriel` qui exige ses
faits, le badge « Une flamme à soi » ; lot 2 `60f741e` : `/jeu` rend le nouvel accueil, `@accueil` posé par
`AccueilDeuxPlans`, le parcours et le tableau de bord à l'adresse du parcours), la barre mobile tranchée
par Boris (rien à faire), ses quatre finitions annoncées (sa question sur la famille est répondue dans sa
boîte : la clé `immateria` existe au catalogue depuis le matin). Préprod **`c00a363`** (lot 2 `60f741e`, puis #312-complément, #313 et #314 fusionnées, bancs verts), recette
**188 bancs : 180 verts + 1 hors portée, 7 rouges réparés et rejoués verts** ; production **`34a167d`**. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR #311 et #312 et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Boris — la production ATTEND IMMATERIA, et Immateria est en préprod.** « On va encore attendre,
  Immateria sera livrée sous peu, une fois cette partie-là intégrée, on passera tout en prod. » C'est
  intégré : à lui de **tester en préprod** (`/jeu` → « Rejoindre Immateria » → la traversée → le retour à
  l'accueil, l'Enfant, le badge une fois) et de **valider deux décisions prises pour brancher** : (1) le
  parcours linéaire et le tableau de bord d'après-clôture vivent à l'adresse du parcours,
  `/parcours/point-zero-monde-0` (carte du voyage avant la clôture, tableau de bord après — la liste des
  vingt n'est plus rendue après la clôture) ; (2) le Monde 1 garde son accueil à sept cartes. Puis **la
  promotion d'ensemble** (M0 + 18 verbes + Immateria), le poste fixe ayant livré ses finitions ou non.
  Restent chez lui : le retest du M0 ; la relance des paiements Festival ; les trois dependabot
  (#226, #227, #228).
  ⚠️ À la promotion, les 18 verbes se jouent EN PRODUCTION comme en préprod : sauvegarde vérifiée →
  migration → **simulation d'abord** (jamais jouée sur la production ; le script s'arrête seul si la
  table figée diverge) → `ECRIRE=oui` → journal **hors** du conteneur → B est déjà dans le code.
  Et le §9 de Codex se mesure alors : les comptes de production qui ont rejoué E1 depuis le 31 août.
- **Codex** : les mots définitifs du badge « Une flamme à soi » et de la famille Immateria (provisoires,
  du portable, dans `config/badges.yml`) ; son arbitrage 12.6 (les anciens joueurs au premier affichage —
  aujourd'hui ils voient l'accueil sans Enfant, « Ton Enfant t'attend ») ; le bandeau « Ce qui t'attend »,
  parti de `/jeu` avec l'ancien accueil (si l'avatar doit « regrouper les nouvelles », §7, c'est une ligne
  de plus dans `@accueil`) ; la carte Puissance après le regroupement ; l'état `empty` de la Carte du
  Seuil.
- **Poste fixe** : ses finitions d'Immateria sont fusionnées (#313, #314) ;
  les états visuels sur la préprod réelle (reprise, badge). ⚠️ `.pz-m0-parcours` est désormais aussi la
  classe du lien « Parcours » du menu : la carte du voyage se reconnaît à sa racine.
- **Moi, à la relecture de ses finitions** : `ruby -c` des bancs avant la fusion, rejouer
  `verifier_accueil_immateria`, `verifier_immateria`, `verifier_accomplissements`, `verifier_serie_de_badges`.
- **Moi, ensuite** : les empreintes des quatre illustrations du corps des articles (#309, ma zone) ;
  le commentaire dans `Challenge` disant que les exports gardent `name` (poste fixe, pas urgent).
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
    `badges.yml`, `sas.yml`) ;
  - ⚠️ **`public/` est servi un an en cache** : l'ancien tutoriel vivait aux mêmes adresses, les
    empreintes du poste fixe (#311) le couvrent — vérifier au navigateur, en production, qu'aucune
    requête nue ne part vers `/pz/immateria/`.
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
