# Le mode événementiel du Festival — arbitrages, contrat et répartition

Relevé du poste fixe, **27 septembre 2026**. Référence de la maquette :
`zegame-prototypes`, branche `codex/mode-festival-cible`, tête `98dcde5`, dossier
`mode-festival-cible/` (illustrations au commit `d823324`).

Ce document existe parce que trois arbitrages de Boris **invalident des éléments de la maquette**
et parce qu'une question est explicitement reportée à octobre. Une boîte aux lettres se vide ; ceci
doit survivre.

---

## 1. Les trois arbitrages de Boris (27 septembre)

| question | réponse | ce qu'elle change |
|---|---|---|
| la fenêtre du choix des 100 € | **48 heures** | ⚠️ `PartDuCommun::DELAI` vaut **24.hours** en production (arbitrage du 5 septembre, « le choix est fait le jour même »). **À porter à 48 h** — zone du portable. |
| au silence, à l'échéance | **la part RESTE** (la personne est sociétaire) | ✅ le code est déjà juste. ⚠️ **La maquette dit l'inverse** — « absence d'investissement confirmé = remboursement automatique » : cet énoncé ne doit PAS être porté. |
| la porte du mode événementiel | **elle laisse passer le questionnaire de Puissance** | le mode n'est donc pas hermétique : `powers` et la fiche d'une Puissance restent atteignables depuis l'événement. |

⚠️ **Le deuxième est celui qui porte de l'argent.** Le code l'écrit en commentaire : « le défaut est
silencieux, et c'est tout le sujet — l'argent est déjà encaissé, il reste ; seul le refus produit un
événement ». Avec cent participants, ce défaut décide de dix mille euros. L'énoncé de la maquette est
donc une **erreur éditoriale à corriger à la source**, pas une variante.

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
| **Codex** | la maquette ; ⚠️ **corriger l'énoncé du remboursement automatique** (§ 1) et le libellé « M0 s'ouvre » (voir ci-dessous) |
| **le portable** | `PartDuCommun::DELAI` 24 h → 48 h ; la route joueur du choix ; les codes d'atelier (serveur, idempotents, expirants) ; les capacités et réservations ; le barème administré ; la porte du mode événementiel et son discriminant **levable** ; la mécanique de l'« an inclus » |
| **le poste fixe** | le portage du balisage et des feuilles, les bancs, l'intégration des 18 défis illustrés |

⚠️ **Un libellé à reprendre avec la décision de déploiement.** La maquette notifie « M0 s'ouvre »
juste après l'investissement (`?notify=1`). Or l'invitation à faire le Monde 0 part **quand
l'application sera disponible sur les stores, ou en PWA** (décision de Boris du 27 septembre).
Investir *donne droit* ; le libellé ne doit pas annoncer une porte qui n'est pas encore ouverte.

ⓘ **Ce que le consentement ne casse pas** : la photo du profil de rencontre est **déjà déclarée** au
formulaire de sécurité des données de Play (`PSL_PHOTOS` = collectée, non partagée, optionnelle,
finalité « fonctionnalité »). Seule réserve à regarder : l'**archétype** est une donnée de profil
psychologique, et il n'est pas établi que Play n'attende pas une ligne propre pour elle.
