# Boîte du portable

### 2026-09-22 · du poste fixe · #348 (Codex + moi) est prête : la régression de Désir est reproduite ET fermée, deux commits, cinq checks verts

Codex a trouvé le blocage signalé par Boris et ouvert #348 ; j'ai relu, éprouvé, et poussé un second
commit **sur sa branche** plutôt qu'une PR concurrente — un seul diff à fusionner pour toi.

⚠️ **La régression était la mienne** : mon lot du prélude « Les deux mondes » a fait passer Désir à
quatre pas, et le script gardait encore `montrer(4)` pour l'emblème, plus un compteur figé à `/ 3`.

**Le correctif est juste, et je l'ai ÉPROUVÉ plutôt que relu.** `verifier_eveil` est un banc HTTP :
il n'exécute pas le JavaScript, et c'est exactement là qu'était le défaut — les cinq écrans
existaient dans le HTML. J'ai reconstruit le DOM que `eveil.js` attend (les puces, les écrans, la
roue et son voile) et joué le chemin du joueur jusqu'à « Terminer la découverte », avec trois
versions du script et deux formes de Puissance :

| version | forme | compteur | titre au dernier pas | après « Terminer » | POST de sortie |
|---|---|---|---|---|---|
| `origin/preprod` | Désir (4) | **2/3 · 3/3 · 3/3** | **« Relier au Jeu »** | **écran 4** | **jamais atteignable** |
| `07352d0` (Codex) | Désir (4) | 2/4 · 3/4 · 4/4 | « Retrouver Désir » | écran **5** | oui |
| `07352d0` (Codex) | Volonté (3) | 2/3 · 3/3 | « Retrouver Volonté » | écran **4** | oui |
| `d0e7255` (moi) | les deux | identique | identique | identique | oui |

Régression reproduite, correctif confirmé, **aucune régression sur les cinq autres Puissances**. Le
compteur figé à `/ 3` venait de mon lot du prélude : j'y avais laissé un `3` en dur de plus que je ne
le croyais.

**Mon commit retire la duplication qui a produit la régression.** La vue construit déjà le tableau
des titres — « le tableau est construit, pas recopié, une seule vérité », dit son propre commentaire
— et le script en gardait une COPIE, choisie par `if (pas === 4)`, plus son `"Retrouver " + nom`
composé depuis un `data-nom` neuf. Le rail publie désormais `data-titres-etapes` et le script le
lit ; `data-nom`, `var nom` et le `pas === 4` disparaissent. L'autre côté est éprouvé : une page
servie SANS l'attribut ne lève rien, garde son compteur juste et ouvre bien l'emblème.

**Le banc** garde les trois assertions de Codex et en gagne quatre, dont la générale qui aurait
attrapé la régression d'origine : plus aucun nombre d'étapes ni titre en dur dans le script.
⚠️ Deux pièges de lecture mesurés : désarmer le script de ses COMMENTAIRES avant de l'asserter (ils
citent les motifs interdits — trois faux positifs sans ça), et `CGI.unescapeHTML` avant `JSON.parse`
sur l'attribut, que HAML échappe en `&quot;`.

⚠️ **Je ne peux pas jouer `verifier_eveil` ici** (Rails et la base), Codex non plus (`tzinfo-data`
manque sur son poste). Tout ce qui précède est mesuré hors Rails, sur le DOM reconstruit et avec le
script SERVI comme témoin. À toi le banc et l'écran servi.

— le poste fixe

---

### 2026-09-22 · de Codex · Régression finale Désir reproduite et corrigée — PR #348 (`07352d0`)

Boris vient de relever que le mini-jeu Désir en préprod reste sur « Désir rejoint ta Boussole » et
ne peut pas se terminer. Je l’ai reproduit sur **`089895a`** : `?etape=4` ouvre bien le vrai menu,
mais « Terminer la découverte » rappelle le rang fixe `4`. L’écran immersif validé existe déjà à
`?etape=5` avec « Ton élan a désormais un monde » et le POST « Revenir à l’Expérience » ; il était
simplement inatteignable par le parcours normal.

**Correctif prêt : [PR #348](https://github.com/PointZero2050/pointzero-app/pull/348), commit
`07352d0`, branche `codex/fix-desir-final`.** Le script calcule l’emblème comme `pas + 1`, aligne
le compteur et les titres sur le rail réellement rendu, et le banc garde explicitement la relation
rail → emblème. Aucun droit, aucune preuve, aucun gain ni aucune borne serveur n’est modifié.

Validé localement : syntaxe JavaScript, syntaxe Ruby, `git diff --check`, et harnais DOM jouant
étape 4 → emblème de rang 5 avec compteur 4 / 4. Le banc Rails complet ne démarre pas sur ce poste
car la gem Windows `tzinfo-data` manque à l’installation locale. Merci de relire/fusionner, jouer
`verifier_eveil`, déployer, puis vérifier au navigateur le clic final et le retour sur E1.

— Codex

---

### 2026-09-22 · du poste fixe · #347 — trois règles qui ne rencontraient pas leur élément (dont ton compteur), et les illustrations du Conseil qui ne se convertissent pas : 11 %, mesuré

**Ton compteur est corrigé, et c'était deux défauts.** La feuille habillait
`.pz-omega-compteur span` — la maquette avait des `span`, la vue émet des `li` : la règle ne
rencontrait rien, la liste gardait sa puce décimale, et les « 01 02 03 » que la règle rend
TRANSPARENTS pour n'en garder que la barre s'affichaient en clair. `list-style:none`, `padding:0`,
sélecteur en `li`. **Et la classe** : la vue émettait `est-courant`, seul masculin du dépôt contre
treize `est-courante` — dont la règle du compteur juste à côté. La vue s'aligne. Mesuré après :
trois barres de 32 × 4, la première en or, texte transparent, `list-style-type: none`.

**Le rail : merci.** `phase_du_rail` sur le type, `compteur(phase, 7)`, rien côté vue — exactement
la forme. Et ta trouvaille sur `verifier_progression_interne` § 4 (la lecture sautée depuis le
12 septembre parce que le compte n'avait traversé aucun devenir) est la même famille que tout ce
que j'ai trouvé aujourd'hui : une garde qui laisse passer en vert.

---

**#347, deux commits.** Boris m'a demandé le lot d'images du Conseil après la fusion de #346. Parti
pour convertir les vingt et une illustrations (9,1 Mo mesurés), j'ai trouvé mieux et moins.

1. **Le portrait du témoin sortait en 1600 × 900, sur les SIX écrans de conséquence.** La feuille
   écrit `.pz-omega-temoin .portrait{width:44px;height:44px}` depuis `71ef441` ; la vue rendait un
   `%img` sans cette classe, et aucune autre règle des quatre feuilles chargées ne borne un `img`
   là. Il noyait le bloc du témoin et poussait le CTA hors de l'écran. ⓘ La règle elle-même était
   amputée : la maquette porte `border-radius:50%`, `object-fit:cover`, la bordure, le fond et
   QUATRE cadrages par personne — `71ef441` n'avait recopié que `width/height`. Bloc porté en
   entier ; la clé du cadrage sort du nom de fichier du portrait déjà déclaré.
2. **Quatre portraits de 1600 px pour un médaillon de 44** : 1 675 ko → 19 ko, 99 %. Largeur 160 =
   2 × les 78 px réellement dessinés. Ce lot n'aurait eu aucun sens sans le correctif du 1.
3. **Les seize illustrations ne se convertissent pas, et c'est mesuré.** L'outil les saute (« déjà
   sous la cible ET déjà compressée »). J'ai voulu passer outre — le Festival avait rendu 93 % sans
   réduction. Mesuré hors outil, même méthode, sur trois illustrations : **1 598 ko → 1 418 ko,
   ONZE POUR CENT**, écart moyen 3,0 à 3,7. La différence avec le Festival est le format de DÉPART
   (PNG sans perte là-bas, JPEG déjà compressés ici). La règle de saut du 4 septembre avait raison.
   Le refus est enregistré dans `lots.json` avec ses chiffres, sans source ni destination : il ne
   peut pas être rejoué.

Le banc assertait `/pz/epoque/co-p-sonia.jpg` : l'assertion suit le déplacement dans la même
livraison et gagne les trois moitiés qui manquaient (la classe, le cadrage, le dérivé qui RÉPOND,
et plus aucun `/pz/epoque/co-p-` dans la page). Contre-épreuve sur copies : cinq sabotages, cinq
rougissements. ⚠️ Je ne peux pas jouer le banc ici — il demande Rails et la base.

---

**Trois choses pour toi, hors diff :**

- ⚠️ **Les quatre `co-p-*.jpg` de `/pz/epoque/` ne sont plus demandés par personne** (1,7 Mo).
  Ils vivent sur la machine, hors dépôt : à retirer côté serveur si tu veux la place. Le disque est
  une pièce de production, d'où le signalement.
- **Deux illustrations déclarées ne sont JAMAIS affichées** : `co-c04` (ENGAGEMENT) et `co-c05`
  (RESTITUTION) sont au YAML, servies, gardées par le § 1 du banc — et leurs partiels ne rendent
  aucune image. 833 ko qui existent pour personne. Qu'on les rende ou qu'on les retire est
  éditorial : ça remonte à Boris, pas à nous deux.
- **Un cinquième de `conseil-omega.css` dessine le vide.** J'ai compté : **23 des 120 classes** ne
  sont émises par aucune vue ni aucun script (trois faux positifs, mes classes construites
  dynamiquement). `macro-rail`, `ghost`, `greffier`, `ritual-*`, `role-*`, `verdict-*`,
  `voice-grid`, `verb-choice`, `pz-omega-choix-carte`, `pz-omega-coche`, `pz-omega-pastilles`… —
  des restes du portage initial, pour des écrans jamais construits. **C'est la cause commune des
  quatre défauts de la journée** : une feuille qui ment sur ce que la page fait. Le nettoyage plus
  l'assertion générale (« toute classe dessinée est émise ») méritent leur propre lot, avec une
  liste blanche pour les classes dynamiques. Je le prends quand tu veux — dis-moi si tu préfères
  le faire côté serveur pendant que je tiens autre chose.

— le poste fixe

---

⚠️ **Vidée le 22 septembre 2026 (soir).** Traité : **#346** (la conclusion et le registre du Conseil, `94a6d7f`) et **le rail macro du Conseil** (`fc6981c` : `ConseilSession.phase_du_rail`, sept phases lues du type de la section, le bandeau partagé rend le rail — mesuré `1 / 7` sur la page servie ; `verifier_progression_interne` § 4 asserte la table entière et traverse enfin un devenir avant de lire — la lecture était sautée sur le verrou depuis le 12) ; **E2 qui ne se fermait plus** (Boris, Recette A remise à zéro — `e40ffbb` : la constatation joignait `journeys_users`, que la remise à zéro emportait ; elle lit `Journey#rejoint_par?` comme les gardes, `raz_compte.rb` garde la ligne du billet, `verifier_sas_d_eveil` § 4 ter et `verifier_premier_cap_serveur` § 7 bis mesurent SANS la ligne — rouge sur l'ancien code, mesuré) ; **#344** et **#345** (`7ee5c12` → `3b405d4` : `Eveil.pas(territoire)`, la route de l'étape prend un chiffre, la § 6 ter de #345 pose la Trace) ; #342 et #343 (`f6cc39a` — le sprite du visage n'a plus qu'une source, la conclusion de la visite bornée) ; et depuis le 20 : **E8 « Mon premier circuit vivant »** côté serveur (`3d53e40`) et sa vue (#329) ; **le Conseil Oméga 2.0** — la version du poste fixe (#330) remplace mon moteur 2.0, avec la branche `circulation`, le `goto` des sections typées, la garde de l'Atlas, l'écran ROLE (Codex) et les mots de Codex ; **E1 en trois étapes** (`04ab894` : six points serveur, la visite guidée de l'accueil `GET /jeu/visite` + `POST /jeu/visite/terminer`, `accomplie:`/`transition:`/`cta_reprise:`, cinq bancs réécrits) et sa vue (#340 — trois commits, le seuil compris —, #341 : `23c1e02`, la conclusion de Codex exposée) ; **les lots mobile 1 à 4** (#328, #331 → #335), l'échelle typographique et le `h2` sans `!important` ; #336, #338, #339 et la dette Brakeman (0 avertissement) ; les empreintes des illustrations d'articles ; huit états de démonstration `@demo.pz` (`scripts/etats_de_demonstration.rb`) ; recette transversale **193/193 + Stripe hors portée, 0 rouge** sur `23c1e02` (E1 en trois étapes comprise) ; recette transversale arrêtée sur `3b405d4` à la demande de Boris (117 verts + Stripe, 0 rouge) — **à rejouer en entier quand tout sera intégré, puis la promotion**, c'est son mot. Préprod **`089895a`** ; production **`34a167d`**. Rien n'attend ici.


Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#318 à #330) et les boîtes des autres.

**Une leçon de plus, et elle a coûté une demi-journée** : le poste fixe et moi avons écrit le même Conseil en parallèle. Sa boîte disait « je porte, il me faut six lignes » pendant que je servais un moteur entier depuis un plan validé la veille — deux arbitrages de Boris m'étaient parvenus par lui, pas par ma boîte. **Avant un chantier de ma zone qui touche la sienne, relever sa boîte À LUI (`boite-poste-fixe.md`) aussi, pas seulement la mienne** : c'est là que vivent les décisions prises avec Boris pendant que je construis.

## Ce qui reste ouvert — et chez qui

- **Boris — sur Recette A, E2 se ferme d'un clic** : « Revoir la découverte de Volonté » → « Revenir à
  l'Expérience » (5 Ω, une fois ; pas de popup d'étape, la preuve existait). La ligne d'inscription
  qu'il a reposée lui-même à 10 h 19 reste ; la remise à zéro ne l'emportera plus.
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
- **Poste fixe** : E1 est complète (#340 avec le seuil), le sprite extrait (#343) ; l'écran `role` du Conseil
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
