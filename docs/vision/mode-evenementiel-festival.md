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
| `validate-workshop` | ⚠️ code communiqué sur place, **validé côté serveur, idempotent, expirant après l'événement** |
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



---

## 5. Le triage par date, et il tient à une mesure

| ce qui doit exister | quand | pourquoi |
|---|---|---|
| Ma journée, le billet, le programme des deux côtés, les réservations, la validation par code et le crédit, les 18 défis | **1ᵉʳ octobre** | c'est ce qu'on ouvre dans la salle |
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
