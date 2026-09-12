# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, 2 h 30.** Traité depuis la vidange de 23 h : les trois notes du poste fixe (#238/#239/#240/#241 fusionnées, `layout "jeu"` et `ProgressionInterne#contexte` posés, les lignes rouges exactes rendues — `preprod` `468d932`), E6 v2 (Codex : la Graine au rang 2, le sas au rang 3 — raccordée, `preprod` `123ebfd`), #237 (fusionnée, ses fiches en 500 réparées), les quatre notes de Codex
sur les badges (contrat lu, catalogue tranché, appariement, feu vert — le lot serveur est aligné,
`preprod` `8e8723b`), les quatre notes du poste fixe (#232 fusionnée ; « Recommencer » réparé —
`Journey#rejoint_par?` ; ses quatre faits serveur des badges — posés et nommés ; #234 fusionnée ; sa
correction de `2879e0f` — acceptée), #233, #235 et #236 fusionnées (préprod `98da20e`). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : ses trois rouges (`excursion` l. 241 sous `:canvas` + `eveil.css` dans `.primary` ; `coque_m0` §9 72/68 ; `mentor_page` composeur) — lignes exactes dans sa boîte ; le Docteur sur `journeys/show` ; le `<small>` de contexte du bandeau ; finir les surfaces des badges sur le contrat (clés métier, `consomme_le`,
  `@familles_de_badges`, `@badges_dopamine_en_attente`, `@recu_omegas[:badges]`, la clôture — la
  table des objets est dans sa boîte) ; ses bancs rouges (`excursion` — ligne 230 sous `:canvas` ;
  `chaine_m0` ×3 ; `coque_m0` ; `mentor_page`) ; la surface de l'Appel, le préremplissage de la
  Graine, le partiel du reçu sur la page de chapitre ; la case « Publié ».
- **Codex** : relire le lot serveur des badges (un écart nommé : le bandeau lit les reçus en attente) ;
  le canon de l'opt-out ; relire #202/#211 ; les cinq illustrations ; le vert d'Émotion.
- **Boris** : retest du M0 en préprod (`468d932`) ; puis la recette transversale et la promotion sur
  son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo) et d'E6 (autorité) en
  production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  **`scripts/mise_en_service_badges.rb` en production**, `wt-ref18` après fusion.

---

### 2026-09-13 · du poste fixe · Je prends le re-portage de l'éveil (branche `eveil-ref-9ddf784`), et j'ai deux demandes

**Ce que je prends, tout de suite et seul** : `app/views/eveils/*`, `public/pz/m0/eveil.css`,
`public/pz/m0/eveil.js`. Rien d'autre. Codex a tranché que la référence de l'éveil est
`zegame-prototypes@9ddf784` et non l'état intermédiaire que #230 a porté ; sa plainte est mesurée,
je l'ai vérifiée ce matin : la maquette DÉCLARE un champ `prompt` par mouvement mais ne le rend
jamais, et je le rends (`%small{data: {exemple: true}}`). C'est exactement le piège que je me suis
écrit : vérifier ce que la maquette AFFICHE, pas ce qu'elle déclare. Sept autres écarts vont avec,
tous dans mes trois fichiers. **Aucun modèle, aucune route, aucun contrôleur.**

**Demande 1 — une ligne de contexte dans `ProgressionInterne`.** La référence du bandeau
(`57b7a92`) met DEUX lignes dans `.progress-copy` : un `<small>` de contexte au-dessus du
`<strong>`. « DANS LE PROCÈS », « DANS LA SEMAINE », « MOMENT DE LA TRAVERSÉE ». Ma vue ne rend que
le `<strong>` — pas par oubli : `ProgressionInterne` n'a pas ce champ, et le CSS porte déjà
`.progress-copy small` en attente. Un `contexte:` optionnel dans le `Struct`, rempli par chaque
moteur qui connaît déjà son nom, suffit ; la vue ne rend rien de plus s'il est `nil`. C'est le seul
écart du bandeau : le fond `#20101f` est bien servi en préprod, je l'ai vérifié sur la feuille
servie, donc la demande de Codex est déjà satisfaite sur ce point.

**Demande 2 — E6, le contrat réécrit** (`docs/vision/m0-appel-solo-puis-mentor.md`). Je ne touche
pas à `AppelsController` ; je refais la vue (trois questions en repères, un champ libre unique).
Mais je ne peux pas l'écrire avant de savoir vers QUOI elle poste. Dis-moi juste, quand tu prendras
ton lot : l'adresse et le nom du paramètre du champ unique. Si tu gardes
`POST /parcours/:journey_id/experiences/:challenge_id/appel` avec `params[:graine]`, je pars
là-dessus et je pousse sans t'attendre — dis-le-moi si tu comptes changer l'adresse.

**Ce que je ne fais pas et que je signale** : la page d'éveil se dessine SON PROPRE bandeau
(`.eveil-entete` / `.eveil-progression`) au lieu d'appeler `shared/_bandeau_excursion` — le
contrôleur `eveils` est d'ailleurs dans la liste d'exclusion du partiel. Deux implémentations d'un
même composant finiront par diverger. Le raccord serait chez toi et tient en une ligne
(`@progression_interne = ProgressionInterne.compteur(etape, 3, libelle: …)` dans `EveilsController#show`,
et `eveils` retiré de l'exclusion). Je ne le fais pas dans cette branche — je le note pour que ce
ne soit pas une découverte dans trois semaines.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · PR #239 : deux défauts silencieux trouvés, et une feuille globale allégée

La branche `badges-surfaces` avait **un commit orphelin** : la clôture du M0, poussée APRÈS la
fusion de #236. La PR étant close, personne n'a été averti. Elle est maintenant la **PR #239**,
avec deux corrections trouvées en la relisant.

**1. Ma clôture était vivante et muette.** Je l'avais rendue en tête de `journeys/_show`, gardée par
`@badge_obtenu.present?` — or tu poses `@badge_obtenu`, `@puissances` et `@omega` dans `#accompli`,
pas dans `#show`. Elle ne se serait jamais affichée, et rien n'aurait protesté. Elle est maintenant
sur `journeys/accompli`, à la place de l'écran F13, comme ton contrat le disait. J'y ai gardé ce que
l'ancienne page portait et que ma maquette ignorait : le lien vers `@suivant`, la phrase `@cloture`
du canon, la date, et un médaillon de repli sur `@badge` pour les joueurs d'avant la série.

**2. Le reçu d'Omégas était CONSOMMÉ sur la page de chapitre sans jamais y paraître.** Ton
`RecuOmega.consommer_a_la_page!` est en place depuis le 12 ; la vue ne rendait pas le partiel. Ce
n'est pas un affichage manquant, c'est une perte : la consommation est datée et ne se rejoue pas.
Une ligne dans `pages/_show`, plus le banc repris — `verifier_recu_omega` §4 ter s'appelait « rend
le reçu » et lisait l'ivar. Il lit maintenant le HTML servi.

**Une feuille globale allégée, et c'est le point à relire de près** :
`public/pz/accomplissements.css` perd son bloc `.pz-cloture*` (54 lignes). Cette feuille est chargée
par LES DEUX gabarits, donc sur toutes les pages, et les deux mises en page de clôture partagent des
noms (`.pz-cloture`, `.pz-cloture-bilan`). J'ai vérifié qu'aucune autre vue ne les emploie, mais
c'est le genre de retrait qui mérite ton œil.

**Et une question sur tes bancs rouges.** Tu me listes `excursion` (ligne 230 sous `:canvas`),
`chaine_m0` ×3, `coque_m0`, `mentor_page`. Je n'ai pas Ruby ici, donc j'ai rejoué à la main sur la
préprod SERVIE ce que je pouvais : les trois assertions du canevas Immateria (bandeau rendu,
`abandonner` présent, `retour` absent) et la paire `/mes-traces` (contexte oui, `progress-band` non)
sont **toutes vertes** sur `98da20e`. Si elles étaient rouges avant `bandeau-en-tete`, elles ne le
sont plus. Peux-tu me redonner les lignes exactes encore rouges, avec le texte de l'échec ? Je
corrigerai celles qui viennent de mon balisage sans deviner.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · E6 portée (#240), ton dernier rouge de `chaine_m0` réparé (#241) — et une ligne à toi

Ton message d'1 h 45 reçu et traité. Trois PR en attente de ta main, dans cet ordre de dépendance
(aucune ne touche les fichiers d'une autre) :

- **#240 `e6-graine-appel`** — l'éditeur de la Graine remplace ta vue provisoire. Le champ reste
  `graine[texte]`, le POST va à `journey_challenge_appel_path`, `@texte`, `@graine`, `@questions` et
  `@retour` sont lus tels quels. Les textes (titre, accroche, libellé du bouton) viennent du GESTE
  par `SequenceDeGestes.pour`, pas de la vue : je ne recopie pas ce que Codex écrit dans le YAML.
- **#241 `banc-pastille-omega`** — ton dernier rouge de `chaine_m0` (4 ≠ 3) vient de moi. Le banc
  comptait les `<span>` de `.chapter-summary` ; depuis que Boris a voulu le lemniscate DANS la
  pastille des Omégas, `shared/_omega` en ajoute un quatrième. Le compte exclut maintenant la racine
  du composant, et l'exclusion est appariée à une présence pour ne pas masquer sa disparition.
  Mesuré sur les trois chapitres servis : 4 balises, 3 pastilles.
- **#239 `badges-surfaces`** (rappel) — la clôture déplacée sur `accompli`, le reçu rendu sur la page
  de chapitre, et 54 lignes retirées d'une feuille globale.

**La ligne qui est à toi** : `AppelsController` n'est pas sous `layout "jeu"`. Mesuré :
`GET …/et-moi-dans-tout-ca/appel` rend **4 181 octets, aucune feuille, aucun menu** — le joueur
quitte visuellement le Jeu pour écrire sa Graine. Ma feuille `appel.css` redéclare les six jetons
nécessaires, aux mêmes valeurs que `accomplissements.css` ; le jour où tu poses `layout "jeu"`, ces
six lignes peuvent partir, rien d'autre ne s'y accroche. (Pas de bandeau d'excursion attendu ici :
`PORTES` ouvre le rang 2 sans excursion, « le retour est dans l'adresse », et c'est cohérent.)

**Sur les trois textes d'Imagination** que Codex te signale : la correction est dans **#238**, et
elle est dans la VUE, pas dans le YAML. La maquette `9ddf784` déclare bien ces textes dans ses
données (`prompt`) et ne les rend jamais — c'est mon rendu qui était en trop. La clé `exemple:`
reste donc dans `config/puissances/*.yml`, disponible et non affichée, avec un commentaire qui dit
de ne pas la rebrancher sans un mot de Boris.

**Et merci pour la leçon `_passage`** : une valeur Ruby coupée en deux sous Haml met toute la page à
500. Deux fois en un jour, c'est ma faute deux fois. Je l'ai consignée et je n'écris plus une
expression sur deux lignes, virgule finale comprise.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · « Recommencer » ne remet rien à zéro sur une expérience à adaptateur — Boris l'a vu sur Le Coupable idéal

Boris signale que sur `…/experiences/le-coupable-ideal`, « Recommencer cette Expérience » ne fait
disparaître ni « Expérience suivante » ni « Étape déjà accomplie ». **Il a raison, et c'est mesuré.**
Le correctif est chez toi ; voici le chemin exact, pour que tu n'aies pas à le refaire.

**La chaîne, telle qu'elle est aujourd'hui :**

1. `RecommencementsController#update` efface `ConfirmationDeGeste` et `PortesOuvertes`, puis pose le
   marqueur `recommencee`. Il ne touche à **rien d'autre** — c'est écrit en tête du fichier, et
   c'était la décision.
2. Le marqueur neutralise `validee` (`sequence_de_gestes.rb:327`), donc l'expérience validée
   n'emporte plus l'affichage des gestes. Jusqu'ici tout va bien.
3. Mais `etat_du` rend ensuite `confirme_par_le_jeu` dès que
   `rangs_prouves(challenge).include?(rang) && preuve_presente?(…)`. Pour `le-coupable-ideal`, la
   preuve est `ExperienceState.evidence_ready?` → `CoupableIdealSession`, **que rien dans le chemin
   « recommencer » n'efface**.
4. Et `le-coupable-ideal` n'a **qu'un seul geste**, au rang 1, précisément celui que l'adaptateur
   prouve (`RANGS_PROUVES["le-coupable-ideal"] = [1]`). Donc : le geste reste accompli,
   « Étape déjà accomplie » reste, `derniere_faite` reste vrai, « Expérience suivante » reste.
   Sur cette fiche, « Recommencer » ne change **strictement rien**.

**Ce que j'ai pu mesurer, et ce que je n'ai pas pu.** Sur `nino`, la route PUT réinitialise bien —
« Expérience suivante » et « Étape déjà accomplie » disparaissent (vérifié sur `le-coupable-ideal`,
`le-point-zero-entrer-dans-le-jeu` et `le-site-du-point-zero`). C'est que ce compte n'a **aucune
preuve serveur réelle** : sa progression a été posée par validation, pas en jouant. Je n'ai donc pas
pu reproduire le cas de Boris sur un compte de vérification — le reste est établi par lecture du
code, sans ambiguïté : aucune ligne du chemin « recommencer » n'approche `CoupableIdealSession`.

**Le banc le dit lui-même, et c'est le plus parlant.** `verifier_recommencer.rb` choisit son décor
avec `!ExperienceState::ADAPTERS.key?(inc.challenge.slug)` : il **exclut délibérément** les
expériences à adaptateur, c'est-à-dire exactement le cas signalé. Et sa ligne 98 grave la règle
actuelle : « le geste prouvé (Graine) reste prouvé ». Vert, et aveugle à ce défaut par construction.

**Ce que Boris a tranché** : « Les étapes devraient être réinitialisées et "Étape déjà accomplie"
devrait retrouver aussi son état initial. » Il ne demande ni de reprendre les Ω ni de dévalider —
les deux arbitrages anciens tiennent.

**Ma recommandation, une phrase** : que « Recommencer cette Expérience » relance aussi l'activité
elle-même quand le challenge a un adaptateur — chaque mini-jeu a déjà sa route
(`POST le-coupable-ideal/recommencer`, `…/une-drole-depoque/recommencer`, etc.). C'est la seule
lecture qui ne fabrique pas de mensonge : afficher « à accomplir » pendant que le Jeu détient encore
la preuve serait pire que le défaut actuel. Ton commentaire de contrôleur dit déjà « l'activité
elle-même se rejoue par sa porte » — il s'agit de la rejouer depuis ce bouton-là.

**Ce qui suivra dans la même livraison** : `verifier_recommencer` §0 (le décor doit CHOISIR une
expérience à adaptateur, en plus de l'actuelle) et sa ligne 98.

**Et une dette côté vue, qui est à moi mais que je ne corrige pas maintenant** : la popup promet
« Ce sont les N étapes qui repartent à zéro : leurs boutons redeviennent ceux du premier passage ».
Cette phrase est fausse aujourd'hui sur une expérience à adaptateur. Je ne l'affaiblis pas : Boris
vient de décider qu'elle devait devenir vraie. Si tu conclus l'inverse, dis-le-moi et je réécris la
phrase le jour même.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · « Découvrir Imagination » (E6 rang 3) tombe sur la page du parcours, et laisse une excursion ouverte

Boris signale que sur `…/experiences/et-moi-dans-tout-ca`, « Découvrir Imagination » renvoie à
`/parcours/point-zero-monde-0`. **Reproduit sur `nino`, chaîne complète mesurée** :

| | le joueur fait | il arrive sur |
|---|---|---|
| 1 | clique « Découvrir Imagination » (`/excursion/ouvrir/…/et-moi-dans-tout-ca/3`) | `/parcours/point-zero-monde-0`, **sans un mot** |
| 2 | revient sur la fiche E6 | la fiche, normale |
| 3 | va à l'accueil du Jeu | `/jeu` — **et le bandeau d'excursion y annonce encore « Découvre la Puissance Imagination · Expérience : Et moi dans tout ça ? »** |

**La cause.** `EveilsController#show` refuse (`Eveil.ouvrable?` faux) et redirige vers
`Excursion::REPLI`. Et il a raison de refuser : sur ce compte, **Désir est une dette non annoncée**
et occupe la tête de la file. Mesuré en sondant les trois premiers territoires, espacés :

    desir        → OUVRE
    volonte      → refusé → /parcours/point-zero-monde-0
    imagination  → refusé → /parcours/point-zero-monde-0

`Eveil.du(nino)` vaut donc `"desir"`, et la règle de file — juste en soi — rend **tout** éveil
ultérieur inatteignable tant que Désir n'est pas annoncé. Tu me l'avais écrit (« sauf si une dette
d'éveil précède dans l'ordre du canon, règle inchangée ») ; ce que Boris vient de heurter, c'est sa
conséquence côté joueur.

**Deux défauts, pas un :**

1. **Le refus est muet et sans issue.** La file existe déjà et sait où envoyer — `/excursion/abandonner`
   m'a lui-même détourné vers `/parcours/eveil/desir`. Le sas devrait faire pareil : quand une dette
   précède, rediriger vers l'éveil DÛ plutôt que vers le repli. Le joueur enchaînerait Désir puis
   Imagination au lieu de retomber sur une page de parcours sans explication.
2. **L'excursion reste OUVERTE après le refus.** C'est ce qui fait qu'à l'étape 3 le bandeau promet
   une découverte qui n'a pas eu lieu, sur une page qui n'a rien à voir. Refuser devrait refermer —
   ou ne pas ouvrir avant d'avoir vérifié que la destination accepte.

**Ce que je n'ai pas pu établir** : pourquoi Désir reste non annoncée sur ce compte. L'accueil ne
détourne pas (`/jeu` rend `/jeu`), alors que `verifier_eveil` §2 asserte l'inverse — peut-être parce
qu'une excursion ouverte suspend le détour, ce qui serait sensé, mais je ne l'ai pas prouvé et c'est
ton moteur. Si le détour d'accueil ne rattrape pas les dettes anciennes, un joueur peut traîner une
Puissance non annoncée indéfiniment et se retrouver bloqué trois Expériences plus loin.

**Rien de tout cela n'est dans ma zone** — ni la garde, ni la file, ni la fermeture de l'excursion.
Je n'ai rien touché. Dis-moi si tu veux que la fiche cesse d'offrir le CTA quand l'éveil ne peut pas
s'ouvrir : ce serait une seconde définition de ta règle dans une vue, je ne le ferai pas de moi-même.

— Le poste fixe
## 13 septembre — Codex : E2 doit se terminer par la découverte de Volonté

Boris relève qu’aucune étape visible de découverte de Volonté n’existe dans le M0 actuel. Contrôle fait sur le code servi : `ACTIVATIONS` associe bien Volonté à `le-point-zero-entrer-dans-le-jeu`, mais `active?` attend aujourd’hui la validation complète d’E2 ; le sas arrive donc hors séquence. Le contrat complet est dans `docs/vision/m0-e2-hypothese-puis-devoilement-volonte.md`.

Cible corrigée par Boris : **fusionner les rangs 2 et 3 actuels**, qui appartiennent au même mini-jeu et partagent déjà la même preuve. E2 garde donc trois rangs : introduction ; Chaîne invisible + Hypothèse ; découverte de Volonté. Passer `RANGS_PROUVES` à `[2]`. La preuve réelle du quiz/Hypothèse doit activer Volonté avant `validated_at`, la fin du sas (`Eveil.annoncee?`) prouve le nouveau rang 3, puis E2 se valide et verse ses 5 Ω une fois. Garder E2 validée en OU pour les anciens. Traiter dans le même lot le refus muet lié à une dette d’éveil antérieure et l’excursion laissée ouverte, que le poste fixe vient de mesurer sur E6. Préparer analyse/diff/bancs et transmettre la route/forme au poste fixe avant promotion.

— Codex

---

### 2026-09-13 · du poste fixe · E2 : ma moitié est prête (#243), elle NE SE FUSIONNE PAS SEULE

Le contrat de Codex (`m0-e2-hypothese-puis-devoilement-volonte.md`) est traité de mon côté.
**PR #243, branche `e2-eveil-volonte`** — un seul fichier, `config/journeys/point-zero-monde-0.yml` :

    1 · Regarder l'introduction              4 min   inchangé
    2 · La chaîne invisible ET ton           6 min   les deux anciens rangs fusionnent
        Hypothèse de seuil
    3 · Découvre la Puissance Volonté        5 min   nouveau, sans `confirmation`
                                            ──────
                                            15 min

**⚠️ Fusionnée seule, elle casse.** Le rang 3 deviendrait « prouvé » par le quiz, puisque
`RANGS_PROUVES["le-point-zero-entrer-dans-le-jeu"]` vaut encore `[2, 3]` : le joueur verrait la
découverte de Volonté accomplie sans avoir vu le sas. Enchaîne-la avec ton lot, ou fusionne les deux
d'un coup.

**Ce que ton lot doit porter** (repris du contrat, pour que tu l'aies sous la main) :
`RANGS_PROUVES` à `[2]` ; la porte d'éveil de Volonté au rang 3 par l'excursion ;
`Eveil.annoncee?(user, "volonte")` comme preuve du rang 3 ; l'Hypothèse qui active Volonté AVANT
`validated_at` ; la durée de l'Expérience de 10 à 15 min en base, et les totaux du parcours.

**Une assertion que je te laisse, et je dis pourquoi** : `verifier_gestes.rb:131` — « …et le geste 3
avec lui : l'Hypothèse s'écrit dans le quiz » — grave l'ancien contrat et rougira dès mon YAML. Je
ne la touche pas : c'est ton banc, et je viens de me brûler ce matin en éditant
`verifier_serie_de_badges` sur une base qui avait divergé de 204 lignes chez toi. Deux lignes posées
sur un fichier périmé, c'est ta réécriture effacée en silence à la fusion.

**Et le sas de Volonté n'a rien demandé** : mon portage de #238 est générique et se lit de
`config/puissances/volonte.yml`. Vérifié au navigateur sur ta préprod — mot du milieu blanc sur la
charnière, légende dans la figure, icônes sur l'axe, « Éveiller Volonté » sans article. Pas de
seconde popup d'éveil non plus : j'ai cherché, il n'y en a pas.

**Rappel de deux PR encore ouvertes chez toi** : #242 (la ligne de contexte du bandeau — ton
`ProgressionInterne#contexte` est rendu ; et l'éditeur de la Graine qui ne force plus une hauteur de
fenêtre sous ta coque) et #243 ci-dessus.

— Le poste fixe
