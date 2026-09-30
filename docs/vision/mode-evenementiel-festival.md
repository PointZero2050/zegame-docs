# Le mode événementiel du Festival — arbitrages, contrat et répartition

Relevé du poste fixe, **27 septembre 2026**. Référence de la maquette :
`zegame-prototypes`, branche `codex/mode-festival-cible`, tête `e49e67a`, dossier
`mode-festival-cible/` (illustrations au commit `d823324`).

Ce document existe parce que trois arbitrages de Boris ont **invalidé des éléments de la maquette**
et parce qu’une question est explicitement reportée à octobre. Une boîte aux lettres se vide ; ceci
doit survivre. Les deux incohérences de la maquette ont été corrigées à sa source au commit
`e49e67a`.

---

## 1. Les trois arbitrages de Boris (27 septembre)

| question | réponse | ce qu'elle change |
|---|---|---|
| la fenêtre du choix des 100 € | **48 heures** | ✅ `PartDuCommun::DELAI` vaut désormais **48.hours** en production (`17b1c53`) et son banc protège la nouvelle borne. |
| au silence, à l’échéance | **la part RESTE** (la personne est sociétaire) | ✅ le code est juste. ✅ La maquette l’indique désormais explicitement (`e49e67a`) ; seul un refus demandé produit un remboursement. |
| la porte du mode événementiel | **elle laisse passer le questionnaire de Puissance** | le mode n'est donc pas hermétique : `powers` et la fiche d'une Puissance restent atteignables depuis l'événement. |

⚠️ **Le deuxième est celui qui porte de l'argent.** Le code l'écrit en commentaire : « le défaut est
silencieux, et c'est tout le sujet — l'argent est déjà encaissé, il reste ; seul le refus produit un
événement ». Avec cent participants, ce défaut décide de dix mille euros. Cet énoncé a donc été
corrigé à la source de la maquette, et son banc protège maintenant ce comportement.

ⓘ Et un manque que la maquette comble à juste titre : **aujourd'hui le joueur ne peut pas refuser
lui-même.** Le seul appelant de `PartDuCommun.rendre!` est `gestion/inscriptions_controller` — un
administrateur. Aucune route joueur n'existe.

---

## 2. Une promesse en production que rien n'implémente

« Devenir sociétaire et **accéder à l'application pendant un an** » : la page d'inscription le promet,
la maquette le répète. Or l'état `:engagee` n'est lu que par `fermeture_de_compte` (pour empêcher la
fermeture d'un compte pendant la décision) et par la liste d'administration. **Il n'ouvre rien.** Le
Monde d'un joueur vient de `user.monde_actuel`, et rien ne relie la part du Commun à cette valeur.

À trancher avec la question d'octobre ci-dessous : l'investissement *donne droit*, mais par quelle
mécanique ?

---

## 3. Le contrat d'actions — dix attributs, dix besoins serveur

La maquette construit tout en JavaScript (`index.html` fait 3,5 ko pour 67 ko d'`app.js`, le `<main>`
est vide). **Il n'y a donc pas de DOM à porter classe pour classe** : il se lit dans les gabarits
littéraux d'`app.js`. En revanche le comportement est explicite — dix attributs `data-*`, et chacun
est une route à demander :

| attribut | ce qu'il demande au serveur |
|---|---|
| `nav` | les quatre onglets : Maintenant · Programme · Ma journée · Mes puissances |
| `side` | les deux volets du programme : Lumière (journée, horaires) / Ombre (soirée, émergente) |
| `power` · `cap` | la Puissance et le cap choisi → le défi nocturne correspondant |
| `workshop` · `toggle-reservation` | capacités, places, état de réservation — **vérité serveur** |
| `validate-workshop` | code de **5 lettres** propre au créneau, communiqué sur place, validé côté serveur et idempotent |
| `omega-id` · `omega-kind` | le barème **administré** (celui de la maquette est un barème de démonstration) |
| `make-choice` | le choix des 100 € — **route joueur inexistante à ce jour** |

Périmètre de la maquette : **8 vues** (`now`, `program`, `myday`, `powers`, `power`, `workshop`,
`profile`, `choice`), 10 fonctions de rendu, **189 classes CSS**, 67 actifs dont **18 défis
illustrés** (un par verbe de chaque Puissance).

---

## 4. Ce qui existe déjà — le mode est à CLÔTURER, pas à fonder

- `programme#show`, `programme#ma_journee` ;
- `evenements_jeu#index`, `#show` ;
- six écrans gardés par `verifier_etats_festival` : `festival-inscription`, `-reserve`, `-attente`,
  `-confirme`, `-lier`, `-experience` ;
- la route `evenements/:evenement_id/ateliers/:id` ;
- `PartDuCommun` avec sa fenêtre **dérivée des dates** (aucune date en dur) et ses cinq états ;
- les six Puissances, le Moteur, le registre des Omégas.

---

## 4 bis. LES DIX-HUIT DÉFIS — livrés le 28 septembre (PR #361)

Le catalogue éditorial (`CATALOGUE-DEFIS-FESTIVAL.md`, zegame-prototypes branche
`codex/mode-festival-cible`) vit désormais dans **`verbes.<pôle>.defi_festival`** des six
`config/puissances/<slug>.yml`. Neuf champs par défi : `cap`, `id`, `titre`, `format`, `duree`,
`illustration`, `alt`, `consigne`, `accompli`.

**Aucun modèle, aucun service, aucune migration, aucune route** : `PuissanceAssessment.content`
charge déjà ces fichiers, et aucun consommateur n'itère sur les clés d'un verbe.

### ⚠️ La jointure traverse TROIS nomenclatures — et c'est `cap` qui la porte

| le catalogue nomme | le Moteur range | la config range |
|---|---|---|
| un **verbe** — `festival.desir.contenir` | un **cap** — `moteur_caps["desir"] = "accueillir"` | un **pôle** — `verbes.ombre` |

Rien ne garantissait leur correspondance ; un décalage d'un cran aurait donné au joueur le défi du
verbe voisin, sur une page belle et complète. Chaque bloc porte donc son `cap`, **dans la donnée**,
ce qui évite une quatrième table cap↔pôle dans le code (`premier_cap/_orienter.html.haml` en porte
déjà une en littéral). `verifier_defis_festival` § 2 asserte la correspondance dans les deux sens,
contre `PremierCap::CAPS`.

Les deux sources ont été **croisées, pas recopiées** : zéro écart sur titre, format, durée,
consigne et condition ; et les 18 verbes concordent avec `verbes.<pôle>.mot`.

### Les images : 1180 px, pas 540

⚠️ **Une erreur de lecture à retenir.** `.challenge-reveal{grid-template-columns:270px 1fr}`
appartient à la branche **sans** illustration. Dès qu'un défi en porte une, la maquette ajoute
`challenge-reveal-immersive` (`display:block`) et l'image occupe **toute la largeur**. Les dix-huit
en portent une : cette colonne de 270 px ne rend **jamais**, et les deux familles qui en dépendent
(`.challenge-visual`, `.meeting-sign`) sont hors du portage, ni émises ni dessinées.

Dérivés à **1180 px** (`.screen{max-width:1180px}`) : 5 889 → 2 800 ko, **156 ko par défi**, et un
seul s'affiche à la fois. Sur téléphone, 358 CSS × 3 = 1074 — le même dérivé couvre les deux.

### Ce qui reste au portable

1. les cinq routes `/festival/*` et `layout "evenement"` — **sans elles rien n'est atteignable** ;
2. les deux gestes du défi (« j'accepte », « j'ai accompli »), **autovalidés** selon le catalogue,
   avec attribution idempotente des Ω ;
3. rejouer `verifier_defis_festival` sous `bin/rails runner` (ses § 4 à 7 demandent Rails).

⓵ **Le choix du cap, lui, est déjà un vrai geste** : `PATCH /moteur-caps` existe et accepte
`caps[<puissance>]` + `return_to`.

### ⚠️ Et une gouttière que nos deux bancs ne pouvaient pas voir

`public/pz/evenement.css` n'avait **aucune** règle `#main` là où la maquette en a deux : tout le
mode événementiel rendait **bord à bord**, à toutes les largeurs, depuis #360 — programme et
atelier compris. `verifier_classes_emises` ne compare que des **classes** ; `#main` est un **ID**.
Les sélecteurs d'ID et d'attribut sont un angle mort commun à nos bancs de mise en page.


## 4 ter. Le barème Oméga du Festival — validé par Boris le 29 septembre

Le Festival forme un parcours global de **31 expériences définies** : six moments collectifs,
sept ateliers alternatifs et dix-huit défis de Puissance alternatifs. Ce nombre décrit le
catalogue ; il ne doit jamais devenir le total qu'un participant peut gagner, puisqu'une personne
ne suit que deux ateliers et au plus cinq défis rétribués.

### Le chemin individuel : 50 Ω le jour, puis des défis à 3, 4 ou 5 Ω

| expérience accomplie | gain total |
|---|---:|
| `festival-accueil` | **3 Ω** |
| `festival-inclusion-grotte` | **7 Ω** |
| atelier choisi au round 1 — quel que soit l'atelier | **8 Ω** |
| `festival-cercle-resonance` | **6 Ω** |
| `festival-chant-du-coeur` | **5 Ω** |
| atelier choisi au round 2 — quel que soit l'atelier | **8 Ω** |
| `festival-cristallisation` | **6 Ω** |
| `festival-convergence-cloture` | **7 Ω** |
| **maximum du côté Lumière** | **50 Ω** |

Les sept ateliers ont donc tous le même montant de **8 Ω**. Leur répartition entre Puissances peut
différer, mais une salle, une capacité ou une réservation imposée ne doit jamais faire gagner moins
qu'un autre choix.

Un défi nocturne rapporte **3, 4 ou 5 Ω** selon son intensité. La durée seule ne décide pas : le
nombre de rencontres, l'exposition personnelle, la coordination et la production d'une trace
comptent aussi.

| Puissance · cap | défi | intensité | gain |
|---|---|---|---:|
| Désir · accueillir | La braise sous verre | soutenue · attente, relevé et témoin | **4 Ω** |
| Désir · circuler | Le portrait sans étiquette | soutenue · trois rencontres | **4 Ω** |
| Désir · assumer | Le désir en chœur | forte · quatre personnes et action collective | **5 Ω** |
| Volonté · accueillir | Le geste utile invisible | soutenue · service réel de dix minutes | **4 Ω** |
| Volonté · circuler | Pile, face, vérité | légère · un choix et un premier geste | **3 Ω** |
| Volonté · assumer | Le conseil debout | forte · cinq personnes, décision et rôles | **5 Ω** |
| Imagination · accueillir | Objet trouvé en 2050 | soutenue · prototype et démonstration | **4 Ω** |
| Imagination · circuler | La collision impossible | forte · quatre rencontres et création | **5 Ω** |
| Imagination · assumer | Le bulletin de 2050 | soutenue · production audio et deux retours | **4 Ω** |
| Émotion · accueillir | Caméra sans commentaire | légère · une interaction en deux récits | **3 Ω** |
| Émotion · circuler | Cartographie minute | légère · exercice bref en binôme | **3 Ω** |
| Émotion · assumer | Même battement | soutenue · binôme, accordage et témoin | **4 Ω** |
| Communication · accueillir | L'histoire avec témoin | soutenue · écoute, transmission et correction | **4 Ω** |
| Communication · circuler | Trois phrases nettes | légère · échange bref en binôme | **3 Ω** |
| Communication · assumer | L'émissaire de 2050 | forte · personnage et deux rencontres | **5 Ω** |
| Intuition · accueillir | Le procès de l'évidence | soutenue · trio et critère de réfutation | **4 Ω** |
| Intuition · circuler | La chasse aux trois signaux | forte · quatre rencontres et contre-signe | **5 Ω** |
| Intuition · assumer | Le pari du quart d'heure | soutenue · engagement, geste et témoin | **4 Ω** |

Seuls les **cinq premiers défis distincts** sont rétribués, puis les défis restent jouables sans
nouveau gain. Un même défi ne crédite jamais deux fois. Cinq défis d'intensité moyenne portent le
parcours très engagé à **70 Ω** ; le plafond théorique est de **75 Ω** si les cinq défis accomplis
valent chacun 5 Ω.

La répartition du gain d'un défi entre Puissances reste une décision éditoriale propre à chacun des
dix-huit défis. Il ne faut pas recopier comme canon la règle générique `Puissance choisie +
Puissance secondaire` de la maquette : elle était explicitement démonstrative.

Une proposition exhaustive pour les **31 expériences**, avec une à trois Puissances et leur état
Ombre / Source / Lumière, est disponible dans
[`festival-repartition-omegas-puissances.md`](festival-repartition-omegas-puissances.md). Elle
respecte tous les montants ci-dessus, mais reste à relire avant écriture en base.

### Ce qui ne rapporte rien

Le repas, la pause, le dîner libre, la navigation, la réservation, le questionnaire seul et le
choix d'investir ou de demander le remboursement valent **0 Ω**. Le choix financier ne doit produire
ni avantage ni pénalité en Omégas. Les règles de preuve des six moments collectifs et des ateliers
sont fixées ci-dessous ; une réservation ou l'ouverture d'une page ne valent jamais participation.

### Validation des expériences du Festival — décision du 30 septembre

Trois familles d'expériences suivent trois gestes lisibles pour le joueur :

| famille | preuve | moment de validation | garde-fou |
|---|---|---|---|
| moment collectif / plénière | billet Festival **pointé à l'entrée** | automatiquement à la clôture du moment | aucun gain pour un billet seulement acheté ou réservé |
| atelier | code de **5 lettres** propre au créneau | lorsque le participant saisit le code communiqué à la fin | inscription active au créneau ; pointage facilitateur conservé en secours |
| défi nocturne | déclaration du joueur | lorsqu'il confirme avoir accompli le défi | seuls les cinq premiers défis distincts sont rétribués |

#### Plénières : automatique signifie « après émargement », pas « après ouverture de la page »

`registrations.presente_le`, posé à l'entrée par l'équipe, est la preuve commune aux moments
collectifs. `festival-accueil` est validé par ce pointage lui-même. Les cinq moments suivants sont
validés à leur heure de fin pour les participants dont l'arrivée a été pointée avant cette fin.
Une arrivée tardive n'ouvre donc pas rétroactivement les moments déjà terminés. En revanche,
l'application ne prétend pas mesurer un départ anticipé : l'émargement d'entrée vaut présence aux
moments collectifs postérieurs. C'est une preuve volontairement proportionnée à des séquences
plénières communes, sans QR code, géolocalisation ni geste supplémentaire.

La clôture doit appeler un service serveur idempotent. Il doit aussi pouvoir être rejoué depuis
l'administration afin de rattraper un traitement différé ou une coupure réseau. Les gains ne sont
jamais attribués au simple chargement de la page Festival et une relance ne recrédite rien.

#### Ateliers : un code court par créneau, avec le pointage existant en secours

Le code contient exactement **5 lettres majuscules**. Il exclut les lettres ambiguës `I`, `O` et
`L`, accepte indifféremment minuscules et majuscules à la saisie, et reste valable jusqu'à 23 h le
jour du Festival. Il est propre au **créneau**, pas seulement au titre de l'atelier : le même atelier
programmé dans deux rotations ne partage pas son code. Le facilitateur le montre ou le dicte à la
fin de la séance.

La saisie n'est proposée qu'à un participant rattaché au Festival et inscrit activement à ce
créneau. Une personne accueillie sans réservation est d'abord ajoutée par la fonction
`accueillir` de la feuille de présence. Le facilitateur peut aussi pointer directement une présence
si un téléphone ou le réseau fait défaut. Code et pointage appellent **la même validation** de
l'expérience ; leur répétition ne produit ni nouvelle progression ni nouveaux Omégas. Pour freiner
les essais au hasard sans gêner la salle : cinq tentatives par participant et par créneau sur quinze
minutes, avec un message d'échec qui ne révèle rien du code attendu.

Le reçu de gain Oméga existant s'affiche après succès. L'application peut conserver le mode de
preuve (`code`, `facilitateur`, `automatique`) et l'heure pour l'audit, mais ne doit pas afficher ce
détail technique au joueur.

#### Analyse d'impact avant implémentation

- `EmargementBillet` sait déjà poser de façon idempotente `registrations.presente_le`, mais son
  contrat actuel dit explicitement qu'il ne valide aucune expérience : l'automatisation des
  plénières doit vivre dans un service Festival distinct, appelé après le pointage et aux clôtures ;
- `EmargementAtelier` valide déjà le `Challenge`, pose `end_at` et `validated_at`, puis laisse
  `gain_points` attribuer les Omégas. La confirmation par code doit réutiliser ce chemin et ne pas
  créer un second moteur de points ;
- la vérification doit viser le `Creneau`, car `atelier-du-geste` est un seul `Challenge` relié à
  deux créneaux. Un second passage au même atelier reste sans second gain ;
- les 31 expériences sont actuellement déclarées avec une autorité facilitateur et sans
  autovalidation. Il faut distinguer l'autorité `systeme` des moments collectifs, la preuve par
  code/facilitateur des ateliers et la déclaration des défis, sans rendre les plénières
  autovalidables par simple visite ;
- la limite des cinq défis rétribués appartient au service de crédit, pas seulement à l'interface.
  Les défis suivants peuvent être marqués accomplis avec **0 Ω**, en l'annonçant avant confirmation ;
- dépointer une présence posée par erreur ne révoque pas une validation ni des Omégas déjà acquis,
  conformément à la règle générale déjà appliquée aux ateliers.

#### Recette minimale

1. billet confirmé mais non pointé : aucune plénière n'est créditée ;
2. billet pointé avant la fin d'une plénière : un seul gain à la clôture, même après relance ;
3. arrivée après la fin : aucun rattrapage de la plénière passée ;
4. bon code et inscription active : atelier validé, reçu affiché, un seul gain ;
5. mauvais code, code d'un autre créneau ou participant non inscrit : aucun effet ;
6. validation par code puis pointage facilitateur, ou l'inverse : aucun doublon ;
7. sixième défi accompli : expérience reconnue, aucun Oméga supplémentaire.

### Comparaison avec M0 et conséquences visibles

M0 totalise **100 Ω** sur dix-neuf expériences récompensées, pour environ sept heures. Le Festival
représente donc 50 à 75 % de ce volume pour une journée et une soirée entières. Le rapport reste
cohérent : le Festival est un prologue majeur, avec un rendement horaire inférieur à M0 et une part
variable qui dépend d'actions nocturnes réellement accomplies.

Les Omégas du Festival rejoignent le total général du joueur, mais la progression de M0 doit rester
locale au parcours et commencer à **0 / 100**. Le badge Dopamine des 100 Ω pourra être atteint après
25 à 50 Ω gagnés dans M0 par un participant au Festival : c'est une conséquence assumée d'un seuil
global, pas un signal de complétion de M0.



---

## 5. Le triage par date, et il tient à une mesure

| ce qui doit exister | quand | pourquoi |
|---|---|---|
| Ma journée, le billet, le programme des deux côtés, les réservations, les codes d'atelier, l'automatisation des plénières et le crédit, les 18 défis | **1ᵉʳ octobre** | c'est ce qu'on ouvre dans la salle |
| l'écran du choix des 100 € | **2 octobre** | ⓘ sa fenêtre s'ouvre APRÈS la fin de la journée : un jour de marge, ce n'est pas une opinion |
| le profil de rencontre et le rapprochement | après | facultatif par conception, sans effet sur le défi ni sur les Omégas, et la pièce la plus chargée en données personnelles |

---

## 6. ⚠️ LA QUESTION REPORTÉE À OCTOBRE (Boris, 27 septembre)

> « Comment intégrer les informations remontées lors du Festival — **questionnaire et caps définis**,
> mais aussi **Omégas gagnés via les ateliers et défis** — dans le M0 ? »

Boris la reporte explicitement : il y a le temps d'ici l'ouverture du Monde 0, **courant octobre**.
Ce qu'il faut avoir en tête le jour où on l'ouvre, et qui est déjà mesuré :

- **les Omégas ne se reprennent pas.** Un Ω acquis est définitif, et la validation d'une expérience
  ne se rejoue pas (`FinDeSequence.constater!` rend nil sur une expérience déjà validée). Des Omégas
  gagnés au Festival entrent donc dans le même registre, et la question n'est pas « les convertir »
  mais « les faire cohabiter avec ceux du Monde 0 » ;
- **les résultats de questionnaire de Puissance vivent déjà** côté joueur (`/users/me`, les fiches de
  Puissance). Un questionnaire passé au Festival n'est donc pas une donnée neuve à inventer : c'est
  la MÊME donnée, produite plus tôt. La vraie question est celle de l'**antériorité** — que devient
  un résultat du 1ᵉʳ octobre quand le joueur refait le questionnaire dans le Monde 0 ;
- **les caps** (accueillir l'Ombre / faire circuler / assumer la Lumière) n'ont pas d'équivalent dans
  le Monde 0 aujourd'hui. Ce sont eux qui risquent de rester orphelins ;
- ⚠️ **et deux fils de Graines existent déjà, distincts** : celui de `User` (la Fresque) et celui de
  `ChallengesUser` (l'expérience). Un défi de Festival autovalidé doit choisir son fil, et le mauvais
  choix se verrait ailleurs.

---

## 7. Répartition

| qui | quoi |
|---|---|
| **Boris** | les arbitrages produit et éditoriaux ; la question du § 6 |
| **Codex** | la maquette ; ✅ l’énoncé du remboursement automatique et le libellé « M0 s’ouvre » ont été corrigés au commit `e49e67a` |
| **le portable** | ✅ `PartDuCommun::DELAI` porté à 48 h et porte événementielle livrée ; restent la route joueur du choix, les codes d'atelier (serveur, idempotents, expirants), les capacités et réservations, le barème administré et la mécanique de l'« an inclus » |
| **le poste fixe** | le portage du balisage et des feuilles, les bancs, l'intégration des 18 défis illustrés |

✅ **Libellé repris avec la décision de déploiement.** La maquette distingue maintenant le droit
acquis de l’ouverture effective. Elle ne déclenche plus de notification après l’investissement ;
`?notify=1` prévisualise l’invitation ultérieure, envoyée **quand l’application sera disponible sur
les stores, ou en PWA** (décision de Boris du 27 septembre).

ⓘ **Ce que le consentement ne casse pas** : la photo du profil de rencontre est **déjà déclarée** au
formulaire de sécurité des données de Play (`PSL_PHOTOS` = collectée, non partagée, optionnelle,
finalité « fonctionnalité »). Seule réserve à regarder : l'**archétype** est une donnée de profil
psychologique, et il n'est pas établi que Play n'attende pas une ligne propre pour elle.

---

## 8. Ce qui EXISTE déjà et ne doit PAS être redessiné — mesuré le 27 septembre

Trois composants de la maquette ont déjà leur équivalent dans l'application, et deux d'entre eux
sont **des portages antérieurs de maquettes de Codex**. Les porter une seconde fois créerait
exactement la « seconde vérité » que son propre contrat interdit.

| dans la maquette | ce qui existe | ce que ça change |
|---|---|---|
| ses 12 classes `omega-*` (`omega-glyph`, `omega-orbit-track`, `omega-moving-dot`…) | **`app/views/shared/_omega.html.haml`** — le lemniscate, avec ses locales documentées (`nombre`, `taille` en six valeurs dont `:pastille`, `anime`, `libelle`) | ses notes demandent « le lemniscate Oméga animé **de l'application** » : ses classes sont une doublure de simulation. ⚠️ Le composant dit lui-même pourquoi : « UN COMPOSANT, PAS UN SVG RECOPIÉ — recopiées vingt fois, elles divergeraient à la première retouche » |
| « la fenêtre se rouvre après validation pour confirmer le crédit » | **`app/views/shared/_recu_omegas.html.haml`** — déjà un portage de SON `dialog.omega-receipt` | rien à dessiner : il faut **alimenter `@recu_omegas`** à la validation d'un atelier ou d'un défi. Sa forme est documentée dans le partiel (expérience, gain, solde avant/après, puissances, suivante) |
| « Mon Moteur de Conscience » et les six cartes de Puissance | **`app/views/users/_moteur.html.haml`** et **`_moteur_cartes.html.haml`** — ce dernier est déjà un « PORTAGE STRICT de la `.power-grid` de `moteur-conscience-m0-cible` » | et il est **déjà nourri par le réel** : `o_level`/`l_level` (`PuissanceAssessment`), `etat` (circulation), `verbes` et `couleur` du YAML, `power_breakdown` (les Omégas) |

ⓘ `eveils/_deux_mondes.html.haml` n'est PAS réutilisable : c'est « l'écran d'ouverture du sas de
  **Désir**, et de lui seul ».

### ⚠️ Et la règle de rapprochement ne demande AUCUNE donnée neuve

| ce que la règle exige | où ça vit déjà |
|---|---|
| l'**amplitude** dans une direction | `moteur_assessments` → `result["powers"][slug]["declared_amplitude"]`, borné 1..3 |
| la **direction** (Ombre / Lumière) | le même `result` → `spontaneous_polarity` (`ombre` / `lumiere`) |
| l'état **`intégré`** pour un cap Source | `PuissanceAssessment#etat == "libre"` — et `etat_label` le rend déjà **« Intégré »** |

**Le vocabulaire de Codex et le nôtre disent la même chose** : notre modèle fait déjà la traduction.
Le moteur de suggestion est donc **une requête, pas un modèle** — plus le drapeau de consentement
Festival, qui est la seule donnée réellement nouvelle.

### Le gabarit : zéro collision, et ce n'est pas une chance

La maquette émet **186 classes** (trois de mes 189 premières étaient du bruit d'extraction : `&&`,
`===`, `?`, pris dans les conditions de ses gabarits littéraux). Contre TOUTES les feuilles du dépôt,
14 collisions. Mais **contre les feuilles qu'une coque dédiée charge réellement, ZÉRO** — le
précédent est `layouts/conseil.html.haml`, qui charge sa feuille, fontello, `accomplissements.css` et
`typographie.css`, et **ni `styles.css`, ni `coque.css`, ni `pz_theme.css`**.

Les onze collisions évitées par ce seul choix : `button`, `button-light`, `dialog-close`, `info-card`,
`is-disabled`, `left`, `light`, `prototype-bar`, `right`, `skip-link`, `text-link`.

ⓘ `dialog-close` est **exactement** la collision que le portage de la page Festival avait déjà
  documentée — « la coque du site emploie ce même nom pour son dialogue de lecture, en clair ; celui
  de Codex est sombre ». Le remède est écrit, il se rejoue.

⚠️ **Et la mesure demande sa contre-épreuve, parce que la première était fausse** : j'ai d'abord
vérifié « le gabarit ne charge pas `pz_theme.css` » par un `include?` sur le fichier — qui a matché
le **commentaire disant qu'il ne le charge pas**. Troisième fois dans la même journée qu'un
commentaire est lu comme du code. La bonne mesure ne regarde que les lignes `feuille_publique` et
`rel: "stylesheet"`, commentaires retirés.
