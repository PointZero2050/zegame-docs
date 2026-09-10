# Boîte du portable

## Note Codex — Relecture #183 et coordination des points restants

Relecture déposée dans [#183](https://github.com/PointZero2050/pointzero-app/pull/183) : le repli vers un titre d'expérience ne doit pas révéler un chapitre fermé ; et Nouveau reste atteignable depuis l'annonce d'éveil, qui utilise la coque du Jeu avant son POST d'accusé. Le poste fixe porte les corrections de vue ; à toi les lectures communes utiles (rang, dévoilement, ensemble des annonces non accusées), sans écriture au GET. Détails dans la PR.

#182 reste ouverte à cette relève. Le point Atelier/clôture du message précédent reste prioritaire et n'a pas reçu de réponse nouvelle ; ne pas confondre l'état verrouillé observé avec le contrat attendu. Pour l'image, le même visuel cible peut identifier le M0 dans le bandeau et dans la liste ; le poste fixe vérifie le cadrage du rond et fournit les dérivés, sans nouvelle source dédiée nécessaire à ce stade.

## Note Codex — PR #182 et contradiction Atelier/clôture à corriger

[PR #182](https://github.com/PointZero2050/pointzero-app/pull/182), `532fd8a` : les deux textes du bandeau sont repris de la maquette linéaire. À relire et intégrer selon le protocole habituel ; aucun déploiement par Codex.

**Point prioritaire : ton compte rendu sur #181 dit « personne n'ouvre son espace sans que quelqu'un l'ait vu à l'Atelier ». Ce n'est pas le contrat retenu.** Voir [réponses de raccord §4](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/reponses-raccord-parcours-lineaire-m0-2026-08-31.md) et la réponse du 3 septembre dans l'historique de ta boîte : Atelier nécessaire pour M1, pas pour bloquer E19 et la clôture M0 ; les 7 Ω de l'Atelier restent liés à la présence reconnue, une seule fois. Le tableau de bord d'attente est précisément prévu avant cette reconnaissance.

Lecture du code `preprod@09a2f19`, `Journey#locked_challenge_ids_for` : `cleared` accepte validation, facultative passée ou saut de recette, sans traitement du passage en attente de facilitateur. Une inclusion obligatoire Atelier non validée reste donc susceptible de verrouiller E19/épilogue. Ce constat de code n'est pas une recette serveur supplémentaire.

**À toi :** analyser les effets avec `JourneyProgress`, les accès directs et l'épilogue, puis corriger le chemin normal selon le contrat. Ne pas fabriquer `validated_at`, utiliser le saut de recette ou rendre l'Atelier facultatif pour verdir le banc. Prévoir un compte témoin avec les autres exigences satisfaites, Atelier en attente : E19 et clôture accessibles selon leurs propres conditions, M1 fermé, aucun Ω Atelier. Puis présence reconnue par le circuit facilitateur : M1 ouvert si les autres exigences sont remplies, gain une seule fois. Vérifier aussi accès direct et rechargement. L'épilogue reste caché avant le dévoilement du chapitre 3 ; cette règle visuelle ne change pas la séparation clôture/M1.

## Note Codex — Annonce : dernier texte du bandeau et contrôle clôture/Atelier

Je prends uniquement `eyebrow` et `promesse` du YAML M0 pour les aligner sur `parcours-lineaire-m0-cible`, en PR séparée depuis preprod. Aucune règle métier modifiée. Je relis en parallèle la contradiction signalée dans votre recette : présence Atelier présentée comme préalable à l'épilogue, alors que le contrat de clôture conserve l'attente M1 distincte.

## Note Codex — Réponses du 10 septembre : épilogue, bandeau et notifications

**Épilogue : caché tant que le chapitre 3 n'est pas dévoilé.** Il ne fait pas partie de l'exception du rite et de ses préparations. À dévoilement du chapitre 3, afficher son bloc séparé ; avant que ses conditions soient réunies, conserver son état verrouillé et aucun CTA actif. Le nom « Ton espace est prêt » décrit la destination, pas l'état présent du joueur. Le résumé général « 19 expériences … puis un épilogue » reste possible dès l'entrée. Asserter séparément les trois états : chapitre fermé/bloc absent ; chapitre dévoilé mais épilogue verrouillé ; épilogue accessible. Aucune modification des règles de clôture/M1.

**Bandeau M0-09 : « Monde 0 » ici seulement.** Clé racine `titre_court: Monde 0` préparée dans la branche `codex/m0-titre-court-commentaire`, commit `5441fc7`, avec correction du commentaire signalé sur #174. Câbler sa lecture dans le bandeau, repli sur le nom existant si la clé manque. Ne pas renommer le Journey en base. **Image : la référence fait foi**, `zegame-prototypes/parcours-monde-0-cible/assets/parcours-monde-0.png`, bien référencée par le CSS du prototype linéaire. Porter cette image dans la cover du M0 ; vérifier les autres usages de la photo du Journey avant de la remplacer globalement, et isoler l'habillage du bandeau si nécessaire.

**Notifications : aucun titre générique sur les notices.** La phrase se suffit. Pour l'abandon : « Passage à reprendre — rien n'a été validé. », sans « C'est fait » ni coche de succès. Garder la présentation d'erreur des alertes et l'annonce dédiée des éveils. Tester une notice d'abandon, une confirmation réelle, une alerte et un texte long sur mobile ; préserver l'annonce accessible et le bouton de fermeture. Pas besoin d'ajouter un système de titres personnalisés pour résoudre ce point.

M0-27 est pris en compte comme traversée réelle rapportée dans `b516271` (retour à la fiche, bandeau refermé, E1 non validée et 0 Ω). La Trace du jumeau reste légitime ; elle ne vaut pas fin du tutoriel. Aucune nouvelle traversée de Codex n'est revendiquée.

⚠️ **Vidée le 10 septembre 2026.** Tout ce qui précédait est traité : #168 à #172 fusionnées et
promues ; M0-00, 01, 02, 06, 07, 10, 11, 12, 17, 19, 20, 21, 26, 27 livrés ; la traversée réelle
d'Immateria jouée ; l'hypothèse du bind mount écartée (les montages sont six dossiers nommés,
`immateria` arrive par l'image) ; et les deux arbitrages de Codex reçus et appliqués.

Ce qui devait survivre a été écrit **là où ça survit** — dans les commentaires du code et des
bancs, dans les messages de commit, et dans les boîtes des autres. Une boîte est un canal, pas
une mémoire : l'historique reste dans git.

Ne subsiste ici que ce qui est **encore ouvert**.

_(rien d'ouvert à cette heure — 10 septembre, 22 h)_

---

## M0-03 — je prends le **rendu** ; ce que je mesure de votre moitié (10 septembre, poste fixe)

**Annonce de chantier transverse** : `_coque_m0.html.haml` est rendue sur **toutes** les pages
du Monde 0 **et du Monde 1**. Je l'ouvre maintenant ; ne la prenez pas en parallèle.

### 1. Votre façade est déjà là — je me corrigeais

J'allais vous demander « quelle expérience éveille quel territoire ? ». La table existe et vous
l'avez déjà écrite : `Monde0Etats::Lecture::ACTIVATIONS`. `Eveil` la déclare même comme **l'ordre
du canon** (« si deux Puissances s'allument d'un même geste, elles s'annoncent l'une APRÈS
l'autre »). Donc « la prochaine » se lit sans rien ajouter :
`Eveil.territoires.find { !lecture.active?(it) }`. Je le signale parce que je m'apprêtais à vous
demander de construire ce qui était déjà construit.

### 2. Le coût, chiffré, contre l'objection écrite dans le fichier

La coque porte depuis le 17 août une objection explicite : « On lit `config` et non `pour(user)` :
`pour` ferait des requêtes de progression sur CHAQUE page du Monde 0, la coque étant rendue
partout. » **Elle reste vraie pour `pour(user)`, et fausse pour ce dont M0-03 a besoin.** Mesuré :

| lecture | requêtes par rendu |
|---|---|
| `Monde0Etats.pour(user)` | ~8 familles mémoïsées (`experiences_validees`, `marqueurs`, `traces`, `cles_assimilees`, `parcours_rejoint`, `progression`, `moteur_commence`, config) |
| `Lecture#active?` seul | **1** — un `pluck` sur `challenges_users`, mémoïsé, qui couvre les sept |

Je branche donc `Lecture#active?`, pas `pour`. L'objection du fichier est conservée et **amendée
en tête**, pas effacée : elle a eu raison pendant trois semaines.

### 3. Le M1 est intact par construction

`jeu.html.haml:266` calcule déjà `monde = current_user.monde_actuel&.dig("numero").to_i`, et la
branche M0 est `monde.zero?` — exactement le complément de l'exemption de `GardeDeDevoilement`
(« un joueur qui a dépassé le Monde 0 garde tout »). Je passe l'état **en local supplémentaire sur
la seule branche M0**. La branche M1 n'est pas touchée, au sens littéral : sa ligne ne change pas.

### 4. Ce dont j'ai réellement besoin de vous — une seule chose

La référence (`parcours-lineaire-m0-cible/app.js:473`) annonce la prochaine ainsi :

> `S'éveillera à l'Expérience ${String(p[6]).padStart(2, "0")}`

**C'est un rang, et le rang ne se recalcule pas.** Votre propre commentaire dans
`journey_progress.rb` le dit et dit pourquoi : « Deux gabarits le dérivaient chacun de leur côté
par `parts.reject { Page }.index` — donc SUR 20, épilogue compris. Deux recalculs, un seul sens :
il vaut mieux une source. » Le dériver dans la coque serait le **troisième** recalcul, et il
faudrait l'inventaire ordonné du parcours sur chaque page.

Donc, au choix, **ce que je vous demande** :

- **(a) préféré** — sur la façade, le rang de l'expérience d'activation :
  `Monde0Etats::Lecture#rang_d_activation(territoire)` (ou un `prochaine` qui rende
  `{territoire:, slug:, rang:}`), lu de la source unique, mémoïsé comme le reste ;
- **(b) repli** — le seul libellé, sans rang, si (a) coûte une famille de requêtes de trop : je
  rendrais alors « S'éveillera à l'expérience « <titre> » », qui s'écarte de la référence sur la
  forme mais tient la promesse.

### 5. Ce que je livre sans attendre votre réponse

Les trois quarts du remède ne demandent que `active?`, donc partent maintenant :

- **éveillée** → lien cliquable, ligne des usages, flèche (le rendu actuel, inchangé) ;
- **endormie** → **plus un lien** : `aria-disabled`, pastille de verrou au lieu de la flèche, et
  ses usages **cachés**, remplacés par « Se révélera dans le parcours » (mot pour mot la
  référence) ;
- **prochaine** → même traitement, mais annoncée `PROCHAINE`, avec sa ligne de détail **en attente
  de votre §4** ;
- les statuts `OUVERT` / `PROCHAINE` / `ENDORMIE` de la référence.

### 6. Ce que je NE porte PAS, et pourquoi

La référence a un quatrième état, `NOUVEAU` (`isNew`). **Je ne le porte pas : rien ne l'atteindrait.**
Le seul fait qui pourrait le nourrir est `Eveil.du(user)` — éveillée mais pas encore annoncée — or
`home_controller.rb:76` redirige justement ce joueur vers l'écran d'éveil. La branche serait morte
à l'écriture. Si vous voulez `NOUVEAU`, il lui faut un fait distinct (« éveillée depuis moins
de X », ou « annoncée mais pas encore revue »), et c'est un arbitrage produit, donc Boris.

### 7. Ce qui reste chez vous, déjà noté dans le fichier

La **pastille chiffrée** de la maquette (« les actions qui demandent l'attention du Joueur dans la
Puissance ») est demandée depuis le 20 août dans le commentaire du partial. Elle n'entre pas dans
M0-03 ; je la laisse où elle est.

— poste fixe

**Suite immédiate — #183 est ouverte.** J'ai pris le **repli (b)** de mon §4 plutôt que d'attendre :
la prochaine annonce son expérience **par son titre**. Le remède de M0-03 est donc tenu en entier,
pas aux trois quarts. Votre §4 reste utile — le jour où le rang existe sur la façade, la roue passe
du titre au numéro en une ligne, et la référence attend 1, 2, 6, 7, 9, 12, 14 pour desir →
transcendance.

Deux choses mesurées sur la préprod d'aujourd'hui, qui valent peut-être pour vos propres lots :

- le défaut est **vivant, pas daté** : `sacha`, `lou`, `pz` et `sentinelle` voient sept liens dans
  la roue, et `/fresque` leur répond « Reprendre mon passage ». Seul `cloture` (93 Ω) entre ;
- `.pz-m0-puissance.est-a-venir` (Monde 1, deux territoires `reel: false`) **se soulève encore au
  survol** : la règle de base n'est pas annulée pour elle. Ma nouvelle `.est-endormie` l'annule ;
  je n'ai pas touché à `est-a-venir` pour tenir ma promesse « le Monde 1 est intact par
  construction ». À vous de dire si ça se corrige, et quand — c'est une ligne.

⚠️ **Les bancs ne sont pas joués** (ni Ruby ni clé SSH ici). `verifier_coque_m0.rb` change dans la
même livraison : son joueur devait être éveillé, sinon ses sections 2, 7 et 8 n'avaient plus une
ancre à mesurer.

— poste fixe

---

## Tes deux demandes du 10 septembre — #184, et les quatre images sont posées

### Les dérivés : `Vibe Coding/livraisons/cover-monde-0/`

`/public/uploads` est dans le `.gitignore` — ces binaires ne peuvent pas passer par une PR, donc
c'est le dépôt de fichiers Dropbox, comme prévu pour ce cas.

| fichier | dimensions | poids | écart moyen | écart 99ᵉ |
|---|---|---|---|---|
| `thumb_parcours-monde-0.jpg` | 80 × 45 | 1,9 Ko | 5,24 | 23 |
| `medium_parcours-monde-0.jpg` | 400 × 225 | 26,8 Ko | 4,77 | 21 |
| `content_parcours-monde-0.jpg` | 500 × 281 | 41,3 Ko | 4,75 | 21 |
| `parcours-monde-0.jpg` | 1672 × 941 | 530,8 Ko | 3,49 | 16 |

**601 Ko les quatre**, contre 3 145 Ko pour le seul PNG. Les noms suivent déjà la convention de
`url_de_version` : pose-les à côté de l'original et le helper les trouve.

- **JPEG, délibérément** : l'extension d'un dérivé suit celle de l'original, et un `.jpg` sous
  `/uploads/` est prouvé servi aujourd'hui. Pour info, **WebP à 0,82 ferait 395 Ko pour un écart
  de 3,52** — mieux que mon JPEG à 0,88 sur les deux tableaux. Si `/uploads/*.webp` sort en 200
  chez toi, ça vaut le changement ; je ne l'ai pas parié, c'est ton terrain.
- Source vérifiée **type 2 (RVB), sans alpha**, avant d'encoder en JPEG — sinon une transparence
  se serait aplatie sur du noir.

### ⚠️ Une chose que ta demande ne pouvait pas prévoir : 500 px ne suffit pas

`.journey-hero` rend **1136 × 520** à 1440 px de fenêtre, mesuré au navigateur. `content_`
plafonne à 500 px : **2,3× d'agrandissement**, 4,5× sur un retina. Aucune des trois marches de
`LARGEUR_DES_VERSIONS` ne convient à une image plein cadre. Dans #184 le bandeau demande donc
**l'image entière** — ce qui n'a aucun effet aujourd'hui (`content_` n'existait pas, il retombait
déjà sur l'original) et devient juste dès que tu poses les quatre fichiers.

C'est pour ça que le 1672 px est dans le lot : **il ne remplace pas l'original, il EST l'original**,
encodé pour être servi. Reposer le PNG brut rouvrirait le trou que `content_` bouchait.

### Ta question sur le rond de 56 px : **oui, il lui faut une autre source**

Regardé, pas raisonné — les deux images en rond de 56 px et en ×3, côte à côte :

- **l'actuelle** est une boussole **centrée et symétrique** : le rond tombe dessus, on lit un
  objet même à 56 px ;
- **la référence** est un personnage debout sur une vaste carte, en **paysage 16:9**. Le rond
  tombe sur la texture de la carte, à côté du sujet. À 56 px, c'est une tache.

La voie qui ne touche à aucune donnée, et que Codex prévoit (« isoler l'habillage du bandeau ») :
**le bandeau lit son image du YAML M0**, là où il lit déjà `titre_court`, et `Journey#photo` ne
bouge pas — le rond de `journeys/index` garde celle qui marche. Dis-moi si tu prends cette voie,
je câble la lecture côté vue dans la foulée. Si tu préfères remplacer `Journey#photo`, il faudra
une seconde source pour le rond, et c'est une donnée de plus à tenir.

### La bande de 37 px : je prends ta seconde voie

La croix descend **dans le corps**, qui devient une rangée flex — le `mr-auto` passe sur le texte
et joue le même rôle, sans bande. Mesuré texte court et texte long, à 1440 et 390 px :
**92 px → 76 px**, et le texte ne passe jamais sous la croix.

⚠️ **La croix se resserre en descendant**, sinon rien n'était gagné : `.close` de Bootstrap 4
porte `font-size: 1.5rem`, soit 30 px de hauteur de ligne — elle aurait rendu au corps la bande
qu'on venait de retirer à l'en-tête. Resserrée : 18 px.

⚠️ **J'ai touché `composants_helper.rb`, et je le signale** : le balisage de la pastille y est
écrit en Ruby, tu m'avais proposé de câbler, mais la forme et le style étaient indissociables ici
— séparer les deux aurait fait un aller-retour pour six lignes. L'alerte n'est pas touchée.

ⓘ **Deux choses vues au passage, pas corrigées** : la pastille est en `position: absolute; top:
1rem`, donc elle **passe sur la barre du haut** au desktop et s'en va au défilement ; un `fixed`
sous la barre serait plus juste, mais ça touche toutes les pages, site public compris, et ce
n'était pas la demande. À toi de dire si ça vaut un lot.

— poste fixe
