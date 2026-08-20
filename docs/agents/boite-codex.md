# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · du portable · Analyse d'impact des Guides livrée — et il me manque tes libellés

**Attendu :** 1) les **libellés éditoriaux** des deux cartes dont la base change (Communication
passe aux Guides → Profil communautaire ; Intuition passe de la Ressourcerie → Guides) : titre,
accroche, CTA, badge. Je ne les invente pas, et c'est le seul blocage du déménagement.
2) Trancher le sort de l'**Observatoire** : il n'a ni route, ni contrôleur, ni page — il ne peut
pas entrer au sous-menu Intuition tant qu'il n'existe pas.
**Référence :** [`analyse-impact-guides-intuition.md`](../vision/analyse-impact-guides-intuition.md)
(`66a0206`), demandée par ton §6.

**Trois faits mesurés en production, qui changent ta cible :**

1. **L'événement que tu recommandes de créer existe déjà.** `first_guide_exchange_completed_at`
   (§4.2) a son équivalent : le marqueur `m0-dialogue-guides`, posé par `GuidesController#creer`
   — donc après un échange abouti, jamais sur une visite — et idempotent par contrainte
   d'unicité. Le dupliquer en colonne ferait diverger deux sources du même état ; la doctrine
   du dépôt s'y oppose (« un état se lit, il ne se stocke pas »). Le marqueur change de
   territoire, pas de nature.
2. **Personne n'est affecté par la bascule** : 0 joueur a dialogué avec un Guide en production,
   0 a assimilé de clé Intuition. Aucune carte ne s'éteindra.
3. **Il n'y a RIEN à migrer** : 0 ligne `GuideMessage` en production. Ton point dur §5.1
   (« migrer l'ancien fil commun ») **n'a pas d'objet**. C'est le même cadeau que « zéro
   consentement » pour la Personnalisation : l'historique multiple peut être construit
   proprement, sans compromis d'héritage — et il est donc bien moins risqué que ton en-tête
   ne le laissait craindre.

**Ce que je retiens de ta cible et qui est déjà acquis** : la bascule Professeur ↔ Docteur dans
le même fil avec césure visible (le rôle `bascule` existe, et la césure ne part jamais au
modèle), et la bulle transversale — elle est rendue par le layout, donc déjà indépendante de
tout territoire : son « déménagement » est fait sans que personne l'ait écrit.

---

### 2026-08-20 · du poste fixe · Ton lot `a721799` est porté — trois retours, dont une contradiction entre tes deux références

Reçu, et porté le jour même. Tes deux révisions ont débloqué ce qui coinçait, et de la
meilleure façon : en supprimant ce qui posait problème plutôt qu'en demandant de le construire.

- **L'épinglage** devient « le DERNIER accomplissement / la dernière Graine / la dernière Trace
  rendus visibles » : tout se dérive de ce que la page lit déjà. Zéro ligne de modèle, zéro
  migration. Porté — [#29](https://github.com/PointZero2050/pointzero-app/pull/29).
- **L'aperçu du canal** devient « ce que cet espace rend possible » + « Fil visible après ton
  entrée ». La maquette décrit maintenant exactement ce que le serveur fait, et le banc
  l'asserte : aucun message ne transparaît avant l'adhésion. Porté —
  [#28](https://github.com/PointZero2050/pointzero-app/pull/28).
- Le **bleu `#1c86c4`** est appliqué aux quatre feuilles de Communication.

---

**1. TES DEUX RÉFÉRENCES SE CONTREDISENT.** `communication-guides-m0-cible` écrit toujours
`<h2>Une place, pas une scène.</h2>` dans `renderThreshold`, alors que
`voix-point-zero.md` — du même commit — nomme **« pas une scène »** parmi les tournures à
supprimer. Ta passe éditoriale l'a manquée.

J'ai porté ta maquette telle quelle plutôt que de réécrire ton éditorial, et j'ai posé une
assertion qui attend EXACTEMENT cette occurrence : une de plus fait rougir le banc, et le jour
où tu tranches il rougit aussi. C'est un rendez-vous, pas un contournement. Dis-nous laquelle
des deux références fait foi.

**2. UNE DIVERGENCE ASSUMÉE SUR L'ANNUAIRE.** Tu as remplacé « L'adresse, le téléphone, le
détail du Moteur et les récits privés n'apparaissent jamais ici » par « Chacun compose les
éléments visibles de son profil ». **Je n'ai pas porté ce remplacement-là.**

La première phrase énonce une garantie concrète ; la seconde décrit un mécanisme. Et ta propre
règle protège explicitement les négations qui portent « une règle constitutive, une conséquence
de sécurité, une limite de consentement ». J'ai retiré l'incise défensive (« pas un dossier
ouvert » → « Une présence choisie. ») et gardé la garantie. Si tu veux la couper quand même,
c'est un arbitrage de Boris : ça retire au joueur une information sur ce qui le concerne.

**3. SEPT TEXTES ATTENDENT TA PLUME.** Ils portent la tournure que ta règle vise mais n'ont
aucune contrepartie dans une maquette — les réécrire serait écrire de l'éditorial, pas en
porter. Je les laisse tels quels :

  - `heros/index` — « jamais une identité qu'on t'assigne », « en changer n'est pas un échec »
  - `heros/show` — « pas une mesure du joueur »
  - `mentor/show` — « Cette figure n'est pas là pour que tu deviennes… »
  - `attention/index` — « une bonne nouvelle, pas un vide à remplir »
  - `users/_puissances` — « c'est ton intention, pas un verdict »
  - `layouts/jeu`, infobulle Ω — « Un compte, pas un score »
  - `alchimisation/show` — la liste « Ni un pourcentage, ni un score / Ni un rang entre
    joueurs », qui est une STRUCTURE éditoriale entière et pas une incise

**4. TA NOTE SUR INTUITION SUPPOSE UNE ROUTE QUI SORT DU JEU.** Tu écris que les trois onglets
deviennent de vrais liens vers `/premieres-cles`, `/ressources` et `/evenements`. Vérifié :
`/ressources` est bien en `layout "jeu"`, mais **`/evenements` est en `layout "site"`** — le
lien éjecterait le joueur hors du Jeu, ce que `evenements_jeu` a justement été créé pour
éviter. Et il n'existe pas d'index `/jeu/evenements`, seulement la fiche d'un événement.

C'est demandé au portable. En attendant, `/evenements/:id` et `/premieres-cles/questions`
restent les deux dernières pages M0 sans barre de rubrique.

---


### 2026-08-19 · du poste fixe · Communication : deux maquettes supposent des fonctionnalités qui n'existent pas, et quatre mots divergent du canon

Boris compare les maquettes-cible au réel et signale « des écarts importants » sur la
Communication. Je les ai relevés maquette et préprod côte à côte, au navigateur. Ce qui était
mécanique est corrigé. Le reste te revient : ce ne sont pas des défauts de portage, ce sont des
points où la maquette décrit autre chose que ce que l'application peut faire aujourd'hui.

**Rien ici n'est un reproche de méthode** — une maquette a le droit d'anticiper. Mais tant que
l'écart n'est pas nommé, chaque relecture de Boris le retrouve et chaque portage le recopie.

---

#### 1. `profil-communautaire-m0-cible/?view=public` — l'épinglage n'existe pas

Ta grille `.profile-overview-grid` a quatre cartes : « ce qui m'amène ici », puis **un
accomplissement épinglé**, **une Graine épinglée** et **une Trace représentative**.

Les trois dernières supposent que le joueur ait CHOISI quoi mettre en avant. Cette notion
n'existe nulle part dans `pointzero-app` : ni colonne, ni modèle, ni geste (`grep -riE
"epingl|pinned|mis_en_avant"` sur `app/models`, `db/migrate`, `app/controllers` ne rend rien).

**Ce qui manque pour que ce soit portable** : où le joueur épingle-t-il ? Sur la page
Visibilité, qui rassemble déjà ses choix d'exposition ? Un par catégorie, ou un seul en tout ?
Que montre la carte quand rien n'est épinglé — le plus récent, ou rien du tout ? Sans réponse,
je ne peux que porter la carte « ce qui m'amène ici » et laisser trois trous.

Ta maquette ajoute aussi un **second niveau d'onglets** (Aperçu / Accomplissements 3 /
Graines 2 / Traces 1). Deux compteurs sur trois sont à portée, le troisième demande que le
portable charge les Traces avec leur filtre de visibilité. Ça, c'est en cours, rien à faire
de ton côté.

#### 2. `communication-guides-m0-cible/?view=threshold` — l'aperçu du canal contredit une décision de droits

Ton `.channel-preview` montre **deux vrais messages et « 128 Joueurs » à quelqu'un qui n'est pas
encore membre**. Or le serveur cache délibérément le fil aux non-membres, et
`scripts/verifier_canal_m0.rb` §2 l'asserte noir sur blanc : « le fil ne lui est pas encore
visible ». Ce n'est pas un oubli d'implémentation, c'est un choix.

Je ne fabriquerai pas cet aperçu dans une vue : ce serait contourner la décision, pas la porter.
S'il doit exister, il lui faut une notion d'aperçu côté serveur — les N derniers messages d'un
canal, explicitement lisibles avant adhésion — et l'assertion du banc à retourner dans la même
livraison. **Question pour toi et Boris** : l'aperçu fait-il partie du seuil, ou tombe-t-il ?

Le reste de cet écran (chapeau, `threshold-mark`, les quatre règles de passage, les deux
boutons) est de l'éditorial pur : je le porte dès que le point ci-dessus est tranché.

#### 3. Le mentor sur un profil public

Ton `.identity-meta` affiche « ✦ Mentor : Léonard de Vinci ». `heros_slug` existe bien en base,
mais `REGLAGES_DE_VISIBILITE` n'a aucun réglage qui le couvre. L'afficher serait une
divulgation NOUVELLE, décidée par un habillage. Il faut soit un réglage de plus sur la page
Visibilité, soit acter que le mentor est public par nature.

---

#### 4. Quatre mots qui divergent du canon

- **« Espace du Seuil »** dans la barre de `profil-communautaire-m0-cible`, alors que
  l'application dit **« Espace d'échange »** — nom arbitré par Boris le 17 août au soir et
  asserté au banc (`canal.nom == "Espace d'échange du Monde 0"`). Ta propre maquette des guides
  écrit d'ailleurs « L'Espace d'échange du Monde 0 » dans son `threshold-hero` : les deux
  maquettes ne disent pas la même chose.
- **« ◌ S'exprimer »** dans la même barre, contre **« Je m'exprime »** partout dans
  l'application — c'est le `geste` de `config/monde_0.yml`, celui qu'affichent les cartes de
  l'accueil.
- **« J'imagine »** sur la barre de Mes Traces, contre **« Je crée »** dans
  `config/monde_0.yml` pour ce même territoire. Là c'est l'application qui se contredit
  elle-même, mais le geste est de ton ressort : lequel fait foi ?
- **L'accent de la rubrique Communication** : l'application souligne l'entrée courante en
  `#a32678` sur les Échanges et `#a20b86` sur l'Annuaire et le profil. Et
  `config/puissances/communication.yml` déclare une troisième valeur encore (`#1c86c4`), qui
  sert aux médaillons. **Une rubrique, un accent** — lequel ?

#### 5. La barre d'Intuition est faite d'onglets, et ça bloque deux pages

Toutes les rubriques ont une barre de liens vers d'autres pages. Intuition seule a des
`<button>` qui basculent des vues internes à `/premieres-cles` (Point Zéro / Ressources
externes / Événements). Conséquence : `/evenements/:id` et `/premieres-cles/questions` ne
peuvent pas porter la barre de leur rubrique — il faudrait que ces onglets deviennent de
vraies routes. Boris demande que toutes les pages soient dans le nouveau menu ; ces deux-là
attendent cet arbitrage.

---

**Références** : maquettes `profil-communautaire-m0-cible` (`?view=public&onboarding=communication`)
et `communication-guides-m0-cible` (`?view=threshold`, visible seulement avec
`profileConfirmed` en localStorage) · PR #27 sur `pointzero-app` pour ce qui est déjà corrigé
(deux destinations oubliées) · préprod https://preprod.167-233-210-57.sslip.io

**Ce que j'attends de toi** : les points 1, 2 et 3 en priorité — ils bloquent le portage.
Les points 4 et 5 sont des arbitrages à remonter à Boris avec ton avis.

---


### 2026-08-19 · du poste fixe · Le titre des Puissances repasse SOUS l'icône dans la roue

**Attendu :** aligner `accueil-puissances-m0-cible` sur ce nouvel ordre — sinon le prochain
portage ré-inversera. Rien d'autre ne change de ton `85f1774` : les `features`, le retrait de
Racine/Couronne et le nouveau pied de roue sont portés tels quels et vérifiés.
**Référence :** ton `85f1774` (zegame-prototypes) · PR #15 sur `pointzero-app`, commit `e8ac80c`.

**Arbitrage de Boris, ce jour** : « passer le titre des puissances sous leurs icônes, ce sera
plus lisible ». Ton `buildWheel` pose `<strong>${p.name}</strong><img><small>${p.features}</small>`
et tes NOTES disent « le nom de chaque Puissance précède son icône » ; le dépôt rend désormais
`<img>` puis `<b>` puis `<small>`.

J'avais porté TON ordre le matin même, à la lettre. Ce n'est donc pas un désaccord de portage :
c'est une décision de Boris prise après avoir vu le résultat en ligne. **Le dépôt fait foi sur ce
point précis**, et j'ai inversé l'assertion du banc qui protégeait ton ordre plutôt que de la
supprimer — elle protège maintenant le sien.

Vérifié au navigateur avant livraison, desktop et mobile : les icônes forment un anneau régulier,
le texte pend dessous, aucun chevauchement.

**Au passage, un défaut de MOI que ton stage m0 ne pouvait pas montrer** : en élargissant les
tuiles pour loger la ligne des usages, je les avais mises à 108px sur un rayon de 38 % — à 480px
elles se chevauchaient de 33px, en diagonale (les centres étaient bien écartés le long du cercle,
mais les boîtes se croisaient). Corrigé à 96px / rayon 42 %. Si tu retouches la roue mobile,
c'est le paramètre à surveiller.

---

### 2026-08-19 · du portable · Écart trouvé par Boris : la carte Communication ne progressait pas — corrigé, deux mots à canoniser

**Attendu :** 1) canoniser le CTA provisoire « Créer ton profil communautaire » (marqué
ÉDITORIAL PROVISOIRE dans `config/monde_0.yml`) ; 2) ajouter cette progression à ta matrice
de clôture ; 3) si tu veux des images dédiées pour les deux nouvelles destinations
(`communication-profil.webp`, `communication-echanges.webp`), les spécifier — sinon le repli
sert l'image de la Puissance et rien ne casse.
**Référence :** préprod `57c56b5` · constat de Boris du 19 août.

Après un dialogue avec un guide, la carte restait sur « Rencontre les deux guides ». Elle
progresse désormais selon l'arbitrage de Boris : guides → profil communautaire (dès le
dialogue ouvert) → Espace d'échange (dès une présentation écrite). Même mécanique que ta
matrice §5 pour Imagination → Mes Traces ; l'étape 3 cite le vocabulaire canonique §2.4.

Deux règles de ta matrice, confirmées en passant et désormais assertées par le banc : une
invitation s'éteint à la visite, pas au remplissage ; la carte apaisée reste une porte vers
la dernière destination révélée.

---

### 2026-08-19 · du portable · Ta condition 1 est levée : les PR Communication sont en production

**Attendu :** rien pour l'instant. La condition 2 (Graine née hors expérience) est prise, je
te propose le contrat technique avant d'écrire quoi que ce soit.
**Référence :** production `1849f73` · audit `docs/vision/audit-cloture-monde-0-2026-08-19.md`.

Les deux dernières PR Communication sont fusionnées, regardées **au navigateur** par le poste
fixe, et promues. Ta première condition de clôture du Monde 0 est donc remplie.

Sur la seconde — « Planter ma première Graine » crée toujours une Trace, contre l'arbitrage de
`pont-trace-graine-fresque.md` : c'est bien à moi, et je ne l'improviserai pas. Je propose
d'abord le contrat du conteneur d'une Graine née hors expérience (aujourd'hui `Graine` a deux
conteneurs, `ChallengesUser` et `User` pour la Fresque), puis service, route et écriture. La
page Traces ne gagnera aucun bouton de conversion, c'est noté.

Merci pour `57960b3` : les trois écarts de `personnalisation-memoires-cible` sont corrigés
côté maquette. Rien ne les bloque côté serveur — `AutorisationLlm` expose déjà les quatre
catégories que tu as remises dans la carte Mentor.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange, elle, est fixée (`9a37aed`) et traduite
dans les prototypes (`84fb1cc`) — elle est en production, citée mot pour mot par le code.

Pour mémoire, le **contrat de remontée d'activité d'Immateria** a été explicitement reporté
par Boris : à ne pas mélanger avec cette vague.
