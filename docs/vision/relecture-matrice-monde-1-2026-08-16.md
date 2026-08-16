# Relecture de la matrice d'impact Monde 1 — contre `pointzero-app`

> **Claude (portable), 16 août 2026.** Relecture demandée par la
> [matrice d'impact](matrice-impact-onboarding-monde-1.md) elle-même (§13 : « Le Lot A peut être
> prototypé dans Rails **après relecture du portable** »). Audit en lecture seule de
> `pointzero-app`, branche `preprod`, commit `920ecd2`. Aucun modèle, aucune migration, aucun
> déploiement modifié pendant cette relecture.

## 1. Pourquoi ce document existe

La matrice annonce son propre périmètre dès sa troisième ligne : elle a été auditée sur
**`zegame-app`**, commit `c4383bb`. Or `zegame-app` est la sandbox `vibe.ze.game` ; l'application
qui ira au Festival est **`pointzero-app`**. Les deux ont divergé.

Cet écart n'enlève rien à la qualité de la matrice — sa règle d'architecture (§1), sa légende de
maturité (§2) et sa recette (§12) restent la référence, et l'application les respecte déjà. Mais
**quatre lignes classées « nouvel objet nécessaire » désignent des objets déjà livrés**. Bâtir le
Lot A sur la matrice telle quelle reviendrait à les reconstruire.

Les 72 lignes des §3 à §9 ont été reprises une à une. Chaque verdict ci-dessous s'appuie sur un
fichier et une ligne de `pointzero-app`.

## 2. Ce qui change vraiment : les lignes sous-estimées

Ces lignes passent de « à construire » à « déjà construit ». C'est le cœur de la relecture.

| Ligne | Verdict de la matrice | Réalité dans pointzero-app |
|---|---|---|
| **E07** Boîte d'échanges unifiée | `N` — « ne sait agréger que Journey/Challenge » | **`E`** — `BoiteDEchanges` + `ContexteDeFil.conteneurs_de` agrègent quatre familles (Experience, Parcours, Candidature, EspaceDeDiscussion). C'est l'« interface polymorphe de conteneur » dite « à concevoir ». |
| **E08** Espace communautaire M1 | `N` — « aucun modèle d'espace/channel » | **`E`** — `Espace` couvre les trois critères nommés : intention (`finalite`, + `Messaging::Thread#intention` à 7 valeurs), participants (`EspaceMembership`), cycle de vie (`ETATS` à 5 états). Limite réelle : un espace ne sert **qu'un seul fil** aujourd'hui. |
| **E09** Proposition → objection → consentement → action | `N` — « aucun objet structuré » | **`E`** — sept tables livrées (`propositions`, `versions_de_proposition`, `decisions`, `consentements_de_decision`, `objections_de_decision`, `actions_de_fil`). Le protocole de consentement est câblé : une objection non levée impose « à retravailler », jamais un passage en force. **Seul le mot « mémoire » reste sans objet** (il n'existe que comme réaction sémantique). |
| **G06** Trace personnelle | `N` — « aucun modèle `Trace` » | **`E` pour le Monde 0** — `Trace` existe (`user_id`, `territoire`, `cle`, `reponses` jsonb, unicité sur le triplet), alimentée par Désir, Intuition et Imagination. **Voir l'arbitrage 1 du §5** : ce n'est pas l'agrégateur universel des mini-jeux. |
| **P03** Boussole disponible non commencée | `R` | **`E`** — le résolveur existe : `Monde0Etats#parcours_rejoint?` et `JourneysController` (`.where.missing(:journeys_users)`). |
| **P10** Preuve prête | `E/R` | **`E`** — `ExperienceState.evidence_ready?` est en service avec **dix** adaptateurs, pas quatre. |
| **O02** Ventilation Ω par expérience | `E/R` | **`E`** — calculée et agrégée par chapitre dans `JourneyProgress` (`omega_total`, `omega_gagnes`), rendue par `omega_chapitre`. |
| **F03** Position et cap par Puissance | `E/R` | **`E`** — `PuissanceAssessment` est complet (`from_answers`, `position`, `archetype`, `cap` à un pas contraint) et **surdétermine** délibérément les blocs 1 et 3. |
| **§10** projection `living` | « décisions structurées » à garder fictives | **Réelles** — voir E09. |

## 3. Les preuves à corriger (la maturité est juste, la source citée ne l'est pas)

Ces lignes ne changent pas de maturité, mais leur colonne « source de vérité » enverrait un
lecteur vers du code inexistant.

| Ligne | Ce que la matrice cite | Ce qu'il faut citer |
|---|---|---|
| **§3.1** le piège du callback | « Dans `mathieu_core`, ce hook est un `after_commit` limité aux mises à jour » | **`mathieu_core` n'est pas une dépendance de pointzero-app.** Le hook est réimplémenté dans `ApplicationRecord.on_change` (`app/models/application_record.rb`). **Le fond de l'avertissement est confirmé** — et vérifiable localement, contrairement à ce que la formulation laisse craindre. |
| **P03, P08** colonne « Droit » | `can?(:show, journey)`, `can?(:create, ChallengesUser)` | **CanCan a été retiré du portage.** Gardes réelles : `parcours_visibles` + `verifie_ouverture_du_monde` (P03), `current_user.journeys_users.exists?` (P08). |
| **P11** soumission au facilitateur | message `ask_for_validation` | **Zéro occurrence dans le dépôt.** Les chemins réels sont `EmargementAtelier` (présence en salle) et `RetoursController#create` (les trois questions). Le fil de validation facilitateur est un TODO déclaré. |
| **C01** garde du Monde 1 | `CerclesController#verifier_monde_1` | **N'existe plus.** Remplacé par `VerrouDeCoque` + `config/coque.yml`. Surtout : **la forme du refus a changé** — un joueur du Monde 0 reçoit une page de teasing en 200, non une redirection. Seul l'état `invisible` redirige. |
| **C08** demande refusée | « nouvelle demande possible » | **Le code l'interdit** pour le même cycle (règle V1 §6). Seul un membre `parti` peut redemander ; l'invitation reste l'échappatoire de l'ouvreur. |
| **E01** fil d'expérience | « `has_one` sur `ChallengesUser`/`JourneysUser` » | **Ce `has_one` n'existe pas** (TODO déclaré). Le fil se résout par conteneur polymorphe dans `ThreadsController`. C'est précisément cette absence qui a causé le bug `cu.thread` du 16 août. |
| **E06** notification | `GlobalSettings.notify_of_new_message` | Remplacé par `NotificationFilJob` (envoi débouncé), mentions immédiates, digest quotidien, et réglage par espace (`EspaceMembership::NOTIFICATIONS`). |
| **O08** Fonds du Commun | « aucune table financière » | **Faux au sens littéral** : il existe un circuit euros réel (billetterie Stripe, `montant_centimes`, `prix_centimes`), strictement disjoint des Ω. Écrire plutôt : « aucune table de Fonds du Commun ni règle d'allocation ». **L'interdit qui compte est respecté : aucune écriture ne débite d'Oméga nulle part.** |

## 4. Ce que la matrice voit juste, et qu'il faut garder

- **`Resonance` n'existe pas.** Le proche-voisin est `ReactionSemantique` avec le libellé « Cela
  résonne » — insuffisant : il se pose sur un message, pas sur une Graine, sans destinataire ni
  visibilité propre. L'interdit « une réaction générique n'est pas une Résonance » tient.
- **La filiation Trace → Graine n'existe pas**, et l'absence est **délibérée et documentée** dans
  `MesTracesController` : « ce pont n'existe pas encore. En fabriquer un ici mentirait au joueur. »
- **La synthèse commune (G09) n'existe pas.** `ExportDeFil` rejoue une conversation, ce n'est pas
  une synthèse consentie.
- **Le profil de Cercle et le flow (F05, F06) n'existent pas** — aucune colonne de cadre ni de
  puissance systémique sur les tables Cercle. *(Ne pas confondre avec `RessourceEvaluation`, qui
  évalue des ressources sur cinq cadres.)*
- **Tout le §4 (intensités, M01–M07) est exact**, y compris le point délicat : `difficulty` vaut
  bien 1–10 avec une sémantique ambiguë — confirmée par du code mort qui supposait une échelle
  sur 5.
- **L'interdit de performance d'E07 est fondé et déjà violé** : `BoiteDEchanges` charge puis
  filtre en mémoire. La ligne passe de `N` à `E`, la vigilance reste entière.

## 5. Trois arbitrages qui ne sont pas techniques

Ils reviennent à Boris ; je les expose sans trancher.

**Arbitrage 1 — que vise exactement G06 ?** `Trace` est un registre des productions du Monde 0
par territoire. Si G06 signifie « le joueur dispose d'un registre de ses productions », la ligne
est `E`. Si elle signifie « l'agrégateur canonique de tous les mini-jeux », le constat d'origine
tient et la ligne reste `N` — les résultats de mini-jeux vivent bien dans des tables hétérogènes.

**Arbitrage 2 — le corpus versionné compte-t-il comme source de vérité ?** Deux lignes en
dépendent. Le palier du million d'Ω (`O06`) et la convention d'alchimisation sur 10 (`F04`) sont
**écrits et versionnés** dans `config/guides/`, servis par `GuideCorpus`, avec un `status:
hypothese` et leur propre garde-fou éditorial. Les données, elles, n'existent pas. Pour `F04`,
les **deux entrées de la formule existent déjà en base** (circulation et amplitude par Puissance) :
la spec n'est plus « à concevoir », elle est « à câbler après arbitrage ».

**Arbitrage 3 — TRANCHÉ PAR BORIS LE 16 AOÛT : la publication est voulue.**
La matrice écrivait, pour `O01`, que la publication communautaire du total Oméga se fait « selon
politique dédiée ». Cette politique n'existe pas dans le code : le total Ω est affiché à tout
membre du Monde 1, sur chaque carte de l'annuaire et sur chaque profil, sans consentement et sans
retrait — là où les Puissances sont explicitement opt-in (`PuissanceAssessment#publie`).

**Arbitrage de Boris : c'est un parti-pris de transparence, assumé.** Le total Oméga se publie.
L'asymétrie avec les Puissances n'est donc pas un défaut à corriger : les Puissances disent une
position intérieure, que chacun choisit d'exposer ou non ; le total Oméga dit une contribution au
commun, et le Point Zéro fait le choix de la rendre visible.

Conséquences à tenir : `O01` reste `E`, sa colonne « Droit » doit dire **« publication assumée,
sans opt-in »** au lieu de « selon politique dédiée » ; une carte du Monde 1 peut afficher le
total Ω sans garde supplémentaire ; et **la réserve 3 du §6 tombe**.

## 6. Verdict sur le Lot A

Le Lot A demande : un résolveur `Monde1HomeState` en lecture seule, les états **P01–P16**,
**C01–C14** et **O01–O05**, des liens vers des pages réelles, des tests négatifs de droits, et les
états vide/chargement/erreur.

**Le Lot A est intégralement projetable.** Les trois familles qu'il couvre sont `E` de bout en
bout après relecture — P03 et P10 y entrent même en meilleur état qu'annoncé, et O02 également.
Aucune des lignes du Lot A n'est bloquée par un objet manquant.

Trois réserves à porter dans l'implémentation, aucune bloquante :

1. Reprendre les gardes réelles, pas celles de la matrice (§3 de ce document) — sans quoi les
   tests négatifs viseraient des méthodes inexistantes.
2. `C01` n'est plus une redirection mais une page de teasing en 200 : la recette doit vérifier le
   **contenu**, pas le code de statut.
3. ~~`O01` attend l'arbitrage 3~~ — **levée le 16 août** : Boris tranche que la publication du
   total Oméga est un parti-pris de transparence assumé. Une carte du Monde 1 peut l'afficher
   sans garde supplémentaire.

**Au-delà du Lot A**, la relecture ouvre trois lignes que la matrice réservait au Lot C : `E07`,
`E08` et `E09` sont livrées. Le Lot C n'est donc plus intégralement conditionné — restent
`Resonance`, la synthèse commune, le profil de Cercle et le flow, tous quatre réellement absents.

## 7. Dettes de code relevées au passage

Trois commentaires du dépôt sont faux et **induisent activement en erreur** — deux d'entre eux ont
déjà produit une ligne de matrice erronée. Ils seront corrigés côté `pointzero-app`.

1. `ApplicationRecord.on_change` affirme se déclencher « y compris à la création », alors que son
   propre `on: [:update]` l'en empêche, et que six autres commentaires du dépôt disent
   correctement l'inverse. **C'est le garde-fou de l'attribution des Omégas** : qui croit ce
   commentaire écrit une ligne créée déjà validée, et valide une expérience sans attribuer un
   seul Ω.
2. `CircleMembership` annonce en en-tête qu'« une nouvelle demande reste possible » après un
   refus, quand son propre contrôleur l'interdit. C'est la source de l'erreur sur `C08`.
3. `ChallengesUser` porte encore le TODO d'un `has_one :thread` jamais implémenté — l'origine du
   bug `cu.thread`, désormais contourné par le service `Graine`.
