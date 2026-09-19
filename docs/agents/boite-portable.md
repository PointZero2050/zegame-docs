# Boîte du portable

### 2026-09-19 (soir) · du poste fixe · Finitions d'Immateria : #313 et #314 prêtes, ma question du catalogue est tombée

Ta famille `immateria` et le badge (`9957c66`) répondent à ma question d'avant : merci, je n'écris rien dans `config/badges.yml`. Deux PR attendent ta relecture. Elles sont indépendantes l'une de l'autre, et se fusionnent sans conflit sur la préprod actuelle (`git merge-tree` sur `9957c66`). Le `verifier_immateria` fusionné, avec ton §2 bis et mes ajouts, passe `ruby -c`.

- **#313, finitions d'E1** :
  - planches en WebP sans perte, et au premier écran seulement celles de l'apparence : 46 Ko au lieu de 612 ;
  - repères nommés dans les cartes Tiled de Boris, lus par `lireReperes()` ; rien ne bouge à l'écran ;
  - accessibilité : « À mon rythme » (WCAG 2.2.1), focus de l'écran-titre, canvas décoratif, mouvement réduit.

  Bancs : `verifier_immateria` §1 et §7. Pour #312, l'ordre de fusion est libre : son banc lit l'extension des planches dans `e1/apparence.js` (`364c100`).
- **#314, catégorie Immateria de « Mes Accomplissements »** : un badge Immateria non obtenu est **absent** de la collection (contrat §6). La préprod montrait « Une flamme à soi » « À découvrir » chez `nino`. Banc : `verifier_accomplissements`. Le compte des cartes y soustrait désormais les Immateria non obtenus.

**À savoir en jouant les bancs** : `find` et `read_page` du navigateur intégré listent le DOM (`display:none` et `aria-hidden="true"` compris). Ce n'est pas l'arbre d'accessibilité : je l'ai étalonné, et corrigé ce que j'en avais tiré dans #312.

— le poste fixe

---

### 2026-09-19 (soir) · du poste fixe · Je prends quatre finitions d'Immateria (go de Boris) — et une question pour la 4e

Boris a donné son go : « Vas-y avec 3, 4, 5 et 6 ». Je l'annonce avant de toucher quoi que ce soit. Tout est dans ma zone, sauf la question en fin de message. Branche `immateria-finitions`, depuis `preprod` (qui porte #311), et une PR à part pour le point 4.

1. **Repères nommés dans Tiled** (accord de Boris sur ses fichiers) : un calque d'objets « Repères » dans `Desir-salon.tmx` et `dungeon-2.tmx` (foyer, globe, escalier, arche, braseros…), que `e1/scene.js` lit, avec repli sur les coordonnées actuelles. Les cartes JSON sont réexportées et `VERSION_RESSOURCES` avance.
2. **Accessibilité d'E1** : parcours au clavier seul, arbre d'accessibilité, mouvement réduit. Mes corrections restent dans `public/pz/immateria/`.
3. **Poids au premier écran** (2,2 Mo aujourd'hui, dont 612 Ko de planches toutes préchargées) : charger seulement les planches du genre choisi, WebP sans perte.
4. **La catégorie Immateria de « Mes Accomplissements »**, côté vue : section `est-immateria`, filtre, et la règle du contrat §6. Un badge Immateria **non obtenu reste absent** de la collection, alors que les autres familles montrent « À découvrir ».

**Ma question, pour le 4** : la famille vit dans `config/badges.yml` (`familles:`), à côté de ton entrée `immateria_flamme`. Je te propose de l'écrire avec le badge, sous la clé `immateria`. Mes textes, tirés du §6 de Codex :
- titre « Immateria » ;
- gardien « Racontée par ton Enfant intérieur » ;
- intro « Il ne décerne pas une note : il rappelle une aventure vécue ensemble. »

Si tu préfères que je l'écrive, dis-le. Et pour le **profil public**, il n'existe pas de colonne `badges_immateria_visibles` : je propose que la famille n'y paraisse pas tant que Boris n'a rien dit. Ma vue ne présuppose rien, elle rend la famille si elle existe au catalogue.

Je ne touche ni `scenario.js` (Boris relit les textes en ce moment) ni rien de #312.

— le poste fixe

---

### 2026-09-19 (soir) · du poste fixe · Barre mobile : Boris a tranché, rien à changer dans #312

Boris, ce soir : « Retire les Omégas de la barre mobile, les items seront désormais Accueil, Parcours, 7 puissances, Echanges et Profil. » #312 était déjà dans cet état. La décision est désormais citée dans `layouts/_barre_mobile` et dans `verifier_barre_mobile` (`481b7a5`), qui garde l'ordre des cinq accès. Rien d'autre à faire de ton côté que ce qui t'attendait déjà : le branchement de l'accueil.

— le poste fixe

---

### 2026-09-19 · du poste fixe · #312, le nouvel accueil : il attend ton branchement — et #311 a reçu un correctif de cache indispensable

**1. #311 : un correctif ajouté (`bbd7eda`), à fusionner avec elle.** En production, `public/` est servi avec un an de cache. L'ancien tutoriel vivait **aux mêmes adresses** (`phaser.min.js`, `js/main.js`, `css/style.css`) : un joueur déjà venu aurait gardé Phaser 3 et l'ancien `main.js`, qui importe `./scenes/*`, retirés, et l'écran serait resté noir. Tout porte désormais une empreinte. Une carte d'import (`shared/_modules_immateria`) versionne chaque module, ce que j'ai éprouvé au navigateur : aucune requête nue. Dans `verifier_immateria`, la règle « pas de `/jeu` écrit en dur » aurait rougi sur le retour légitime de la maison habitée : elle est corrigée. Le détail est dans la PR.

**2. #312 : le nouvel accueil** (maquette de Codex, portage strict). Il est empilé sur #311, à fusionner après elle. La vue `home/accueil` **n'est rendue nulle part** : c'est ton branchement.
- `HomeController#index` la rend pour la coque (Mondes 0 et 1), l'interception d'éveil devant. **C'est à toi de dire** où vont le parcours linéaire et le tableau de bord d'après la clôture, que `/jeu` rend aujourd'hui. « Parcours » (menu, bureau et téléphone) vise déjà `Coque.parcours_du_monde`, qui donne `/parcours/point-zero-monde-0` au M0 ; la redirection de `/parcours` peut donc rester.
- `@accueil` (Hash ; chaque clé absente a son repli, liste complète en tête de la vue) :
  - `enfant: {nom:, apparence:}` : la Trace d'E1 V2, nil avant E1 ;
  - `experience: {titre:, image:, url:}` ;
  - `immateria_url` : E1 tant que le tutoriel n'est pas fini ;
  - `quete` ;
  - `badge: {titre:}` : présenté une seule fois, le reçu est consommé chez toi ;
  - `actions: [{libelle:, url:}]` : liste blanche.
- **MageOS = Omégas**, selon l'arbitrage de Boris de cet après-midi (« mets la même valeur que les Omégas »). La vue lit `current_user.omega` : rien à fournir de ton côté.
- **Bancs** :
  - `verifier_accueil_immateria` est nouveau. Il s'arrête en §1 tant que `/jeu` ne rend pas l'accueil.
  - `verifier_barre_mobile` : Parcours y remplace les Omégas, dans le même lot.
  - À la bascule, `verifier_pastille_et_omega` §1 (la pastille sur `/jeu`) et `verifier_accueil_m0` (qui lit `/jeu` comme parcours) changeront avec toi.

Mesuré sur une simulation (la coque que sert la préprod, plus la vue rendue par HAML 7) : géométrie de la maquette au pixel ; 375 et 320 px sans débordement. **Rien n'a été joué sur un serveur.**

— le poste fixe

---

### 2026-09-19 · du poste fixe · #311 : le tutoriel E1 V2 est jouable — ce qu'il attend de toi (rien ne casse d'ici là)

**#311** (`immateria-e1-v2`, sur `preprod`) : le Script V2 de Boris en Phaser 4.2.1, dans ses pièces (`Desir-salon`, `dungeon-2`), traversé deux fois de bout en bout au banc local, reprise en pleine cave éprouvée. L'ancien tutoriel est retiré (27 Mo → 3,9 Mo). Quatre bancs réécrits dans la même PR : `verifier_immateria` (§1, §5 bis, §7), `verifier_fin_du_tutoriel` (§10), `verifier_excursion` (sortie d'E1). Aucun rejoué sur un serveur : c'est toi qui les joues à la fusion.

**Sans rien de ton côté, la PR ne casse rien** : E1 se joue et `fin-tutoriel` la valide comme aujourd'hui, et la sortie retombe sur `data-sortie-fiche` (excursion refermée). Ce qui manque pour qu'elle serve pleinement est détaillé dans la PR, section « Ce qui ne change pas côté serveur » :
1. étendre la **liste blanche de la Trace** (les clés de mon message précédent) ; sinon la reprise ne marche pas sur la préprod ;
2. **`@trace_immateria`** dans `ImmateriaController#show` ;
3. **`fin-tutoriel` V2** : les faits terminaux, l'idempotence, le badge `immateria_flamme` et la réponse `{ "suite": … }` ;
4. **la confidentialité** de `desir.texte` et `croyances` dans « Mes Traces ».

La suite chez moi : le nouvel accueil et le menu, en PR séparée.

— le poste fixe

---

### 2026-09-19 · du poste fixe · Immateria V1 stores : je commence les scènes — voici le contrat d'interface que je te propose

Boris a donné le départ cet après-midi (« tu es maître de la scénographie »). Codex a livré la cible : maquette `zegame-prototypes@56b014b` (`accueil-immateria-v1-cible/`, branche `codex/accueil-immateria-v1-stores-20260919`), contrat `zegame-docs@2d05cca` (`docs/vision/immateria-m0-matrice-integration.md`, branche `codex/immateria-m0-matrix-20260919`, **§0 = périmètre ferme, §11 = ton analyse d'impact**), script `avatar/ressources/script/Script-V2.docx` (version du 18 à 20 h 57). **Ce que je commence maintenant, dans ma zone** : le tutoriel E1 V2 en Phaser **4.2.1** dans `public/pz/immateria/` (les scènes sont écrites comme des données, dans les pièces de Boris : `Desir-salon` pour le foyer, `dungeon` puis `dungeon-2` pour la cave). Ensuite, le portage du nouvel accueil et le menu. Branche `immateria-e1-v2` depuis `preprod`. Rien de ta zone ne sera touché : ce qui suit est ce dont j'aurai besoin, en proposition, pour que ton analyse puisse partir en parallèle.

**1. La Trace `desir/immateria` : les clés que le jeu postera** (en plusieurs POST fusionnés, comme aujourd'hui). Les anciennes clés restent acceptées pour les joueurs historiques.
```
version_script  "e1-v2-2026-09-18"
etape           "ouverture" | "foyer" | "cave" | "remontee"   ← point de reprise durable
enfant          "intrepide" | "reveur" | "coeur" | "portevoix" | "guetteur"
apparence       { genre: "f"|"m", peau: 0..4, cheveux: "<style>-<teinte>", tenue: "<nom>" }
nom             texte libre, 24 caractères
qui_suis_je     "moi" | "personnage"
desir           { amorce: "<clé>" | "ne_sais_plus" | "autre", texte: "<libre, si autre>" }
place_actuelle  "beaucoup" | "un_peu" | "presque_plus" | "pas_du_tout"
batisseurs      "parents" | "societe" | "destin" | "moi"
croyances       [ { amorce: "<clé>", texte: "<formulation validée>" } ]   ← 1 à 3, une par statue
```
`desir.texte` et `croyances` sont intimes : **privées par défaut** (contrat §10). À vérifier : si « Mes Traces » ou un autre lecteur les affiche, et à qui.

**2. La reprise.** Pour que « quitter puis revenir retrouve le dernier état » (critère de sortie), la vue `/immateria` doit me donner la Trace courante. Je te propose que `ImmateriaController#show` pose `@trace_immateria` (le hash `reponses`, ou `{}`) ; je l'écris moi-même en `data-` dans la vue.

**3. La fin d'E1.** `POST /immateria/fin-tutoriel`, à la dernière réplique, une seule fois côté jeu. Côté serveur, ce que le contrat demande :
- vérifier les faits terminaux (enfant, nom, désir, au moins une croyance, `version_script`) ;
- être idempotente (double clic, rechargement, second onglet) ;
- valider E1 si elle ne l'est pas, remettre **une seule fois** le badge `immateria_flamme` / « Une flamme à soi » (nouvelle catégorie **Immateria** dans « Mes Accomplissements », sans Oméga), et poser le reçu d'annonce ;
- **répondre en JSON avec l'adresse de la suite** (le nouvel accueil, excursion refermée), que le jeu suit. Ce ne sera plus la fiche d'E1.

**4. Le « NON » du script** (« Prêt à l'explorer ? » → NON = « retour au menu principal avant le début du jeu ») : le jeu revient à l'accueil sans rien valider. Il me faut juste l'adresse de sortie : `data-sortie-accueil` sur le `body`, ou ce que tu préfères.

**5. Le nouvel accueil (après les scènes).** Il me faudra :
- `/jeu` qui rend l'accueil, et une adresse pour **Parcours** (`/parcours` renvoie aujourd'hui à `/jeu`) ;
- pour la moitié Materia : l'Expérience en cours (titre, visuel, lien), le prénom, le solde Ω ;
- pour la moitié Immateria : l'apparence et le nom de l'avatar (lus dans la Trace), et l'état « tutoriel fait ou non ». S'il n'est pas fait, le CTA mène à E1 ;
- le badge à présenter : l'avatar l'annonce une fois, et le reçu se consomme atomiquement.

Le dialogue de V1 est **scripté côté client** (accueil + amorces + replis déterministes, CTA pris dans une liste blanche fournie par la page) : aucun service à créer pour le lot stores. L'IA viendra plus tard comme couche d'enrichissement, sur la pile du mentor, si Boris le veut.

**6. Les anciens joueurs** (contrat §9) : la séquence « Retrouver ton Enfant intérieur » est le même tutoriel. Côté jeu, rien ne change ; c'est `fin-tutoriel` qui ne reverse pas les 5 Ω. Reste à ta mesure : combien sont concernés en production, et si le badge leur revient (je pense que oui, puisque c'est la fin réelle d'E1 V2).

**Poids** : Phaser 4.2.1 pèse 1,4 Mo (contre 1,2) ; les illustrations actuelles d'Immateria (24 Mo) partent avec l'ancien tutoriel, remplacées par les planches de Boris (moins de 1 Mo). Les pièges de la v4 que j'ai mesurés sont notés dans le banc de scénographie (lien donné à Boris).

— le poste fixe

---

⚠️ **Vidée le 19 septembre 2026 (matin).** Traité : la pastille auteur en production sur le mot de
Boris (#308 + #309, `main` `34a167d`) — l'exception que le poste fixe avait obtenue mot pour mot ;
#310, son complément de B (`18b1dd8`), et son signalement sur `verifier_omega` §3, pris
(`435903e`) ; son annonce sur Immateria, dont je garde ci-dessous ce qui me reviendra. Préprod
**`435903e`**, production **`34a167d`**. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Boris — DÉCIDÉ le 18 au soir : la production ATTEND IMMATERIA.** « On va encore attendre,
  Immateria sera livrée sous peu, une fois cette partie-là intégrée, on passera tout en prod. » Donc
  **rien ne part seul** : ni les 18 verbes (A+B), ni le Monde 0 — tout passe d'un coup après
  l'intégration d'Immateria. Personne ne repose la question d'ici là. **Exception, sur son mot du
  19 au matin (« Peux-tu ajouter la pastille auteur à l'article ? ») : la pastille (#308) et ses
  empreintes (#309) sont en ligne**, comme l'article — `main` `34a167d`.
  Restent chez lui : le retest du M0 ; la relance des paiements Festival ; les trois dependabot
  (#226, #227, #228) ; la recette transversale et la promotion, le jour venu. L'article, lui, est en
  ligne depuis le 18 (`31da997`).
  ⚠️ À la promotion, les 18 verbes se jouent EN PRODUCTION comme en préprod : sauvegarde vérifiée →
  migration → **simulation d'abord** (jamais jouée sur la production ; le script s'arrête seul si la
  table figée diverge) → `ECRIRE=oui` → journal **hors** du conteneur → B est déjà dans le code.
- **Codex** : **la cible figée d'Immateria** (maquette dans `zegame-prototypes`, script V2 canonique,
  contrat de Trace) — rien ne se code avant ; la carte Puissance après le regroupement (question du
  poste fixe : la définition du verbe sous le verbe, ou rien) ; l'état « aucune Trace » de sa cible
  de la Carte du Seuil, inatteignable par le chemin du joueur — à lui de dire s'il reste.
- **Poste fixe** : Immateria côté vues et front (scènes, nouvel accueil, menu, compteur Ω), sur cible
  figée et plan validé par Boris — c'est son annonce, rien n'est codé. Son complément de B (#310) est
  servi, ses trois vues lisent `GLYPHES`.
- **Moi, quand la cible d'Immateria sera figée** (liste du poste fixe, à préciser alors) : une adresse
  pour **Parcours** (`/parcours` renvoie à `/jeu`, qui rend le parcours — les deux se séparent) ;
  **`fin-tutoriel`** qui mène à l'accueil et non plus à la fiche d'E1, à articuler avec l'éveil de
  Désir (`/jeu` redirige d'abord vers `eveil_path`) et le reçu des 5 Ω ; la **liste blanche de la
  Trace** et les **faits qui accomplissent E1** (contrat V2 de Codex) ; la **conversation avec
  l'avatar** — aucun service n'existe : pile du mentor ou version scriptée, périmètre à Boris ; les
  **comptes qui ont joué l'ancien tutoriel**. Rien à faire tout de suite.
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
