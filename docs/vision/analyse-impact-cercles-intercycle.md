# Analyse d'impact — Cercles de croissance et Intercycle

> Ajout Claude - 2026-07-31. Répond à l'analyse d'impact obligatoire exigée par
> [cercles-croissance-profils-flow-omega.md](cercles-croissance-profils-flow-omega.md) § 17 et
> [atelier-seuil-et-jeu-intercycle-monde-1.md](../pedagogie/atelier-seuil-et-jeu-intercycle-monde-1.md)
> § 12, avant toute implémentation. Méthode : audit en lecture seule du code et de la base de
> production de `vibe.ze.game` au 31 juillet 2026 (aucune écriture). Les faits cités — colonnes,
> volumétries, extraits de code — ont été vérifiés sur le serveur, pas déduits de la documentation.

## 0. Synthèse exécutive

Trois découvertes qui modifient ou précisent le plan :

1. **Le marqueur « 100 premiers Oméga » pour le passage au Monde 1 est inatteignable.** Le barème
   réel du Monde 0 plafonne à **84 Ω** sur les expériences requises, **99 Ω** avec les optionnelles.
   Le joueur le plus avancé (hors admins) est à 99 Ω — il a tout fait, optionnelles comprises, et
   n'atteindra jamais 100. Le marqueur doit être soit recalibré, soit remplacé par un critère
   structurel (voir § 8.1).
2. **`JourneysUser` a conservé la révocation de validation** (`set_validated_at` remet
   `validated_at` à `nil` quand `end_at` disparaît), alors que `ChallengesUser` l'a perdue par
   décision de Boris du 2026-07-28 (« une validation acquise ne se révoque jamais »). Tant que le
   passage M0 → M1 s'appuiera sur `journey.completed_by?` (calculé depuis les expériences), c'est
   sans conséquence ; le jour où quoi que ce soit s'appuiera sur `JourneysUser#validated_at`, un
   simple `restart!` révoquerait un passage de Monde. À aligner avant C1 (voir § 8.2).
3. **Le terrain Cercles est vierge.** Aucune table, aucun modèle, aucune donnée à migrer. Les 5
   tables du Lot 1 sont des créations pures : pas de rétrofit, retour arrière trivial
   (`DROP TABLE`), aucune modification des tables existantes nécessaire.

Feu par chantier du plan : **C1 vert** (sous réserve du § 8.2) · **C2 vert** · **C3 vert**
(après prototype papier) · **C4 vert** · **Lots 2/3/5 confirmés reportés** (§ 7).

## 1. Progression et parcours (Journey, Challenge, ChallengesJourney)

- **1 Journey** en production : `point-zero-monde-0` (id 14), `mandatory: true`. Colonnes utiles :
  `mandatory` (ouverture du catalogue — exactement le rôle que lui assigne la spec),
  `auto_validated`, `progression_mode`, `community_id`.
- **16 Challenges**, dont 14 inclus dans le parcours via `ChallengesJourney` (`position`,
  `required`, `optional_note`). Les Pages (chapitres) s'intercalent dans `journey.parts` par
  position — mécanique éprouvée, réutilisable telle quelle pour La Boussole.
- La configuration éditoriale d'un parcours vit dans `config/journeys/{slug}.yml` (mémoïsée en
  ivar de classe → **deux restarts Puma** après modification). `JourneyProgress` calcule chapitres,
  état, prochaine étape ; le seuil de fin est repéré par `validation_authority == "facilitateur"`,
  pas par un id en dur — un second parcours en héritera sans configuration.
- `challenges_journeys_users` (skip d'expériences, 0 ligne aujourd'hui) existe et fonctionne.

**Conclusion C1** : créer le Journey « La Boussole du nouveau monde » est une opération de données
(un Journey, ses Challenges, un YAML), pas de code. La machinerie existante suffit pour les
expériences 1-3 et 6. Aucun impact sur le Monde 0.

## 2. Inscriptions et callbacks (`JourneysUser`, `ChallengesUser`, `on_change`)

Sémantique exacte de `on_change` (gem `mathieu_core`, révision `c193dd17`,
`base_mathieu_core_record.rb:76`) :

```ruby
def on_change field, method, ons: [:update]
  self.send(:"after_commit", method, on: ons,
    if: -> { transaction_include_any_action?([:create]) or [*field].any? { |f| send(:"saved_change_to_#{f}?") } })
end
```

Le `if` accepte les transactions de création, mais `on: [:update]` restreint le déclenchement aux
commits de mise à jour : **une ligne créée directement avec `validated_at` posé ne déclenche
jamais `gain_points`**. C'est le piège documenté ; le motif de parade (écrire la ligne nue, puis
poser la validation dans un second `update`) est déjà appliqué dans les 5 modèles de session
(`CoupableIdealSession`, `Traversee`, `MoteurAssessment`, `ConseilSession`,
`ExperienceQuizAttempt`). **Toute nouvelle écriture de `ChallengesUser` pour l'Intercycle devra
suivre ce motif à l'identique.**

Callbacks en place :

| Modèle | on_change | Effet |
|---|---|---|
| `ChallengesUser` | `validated_at → gain_points` | Ω recalculés (destroy + create) |
| `ChallengesUser` | `end_at → set_validated_at` | auto-validation si `auto_validated` ; **ne révoque plus jamais** (décision 2026-07-28) |
| `JourneysUser` | `validated_at → send_data_to_lti` | export LTI (sans objet hors LTI) |
| `JourneysUser` | `end_at → set_validated_at` | **révoque encore** (`validated_at: nil`) — voir § 8.2 |

Les deux modèles portent aussi `receive_message_extra` : la validation facilitateur passe par un
message de thread avec extra, gardée par `Current.ability.can?(:edit, ...)`.

## 3. Validation des expériences et idempotence

- `ExperienceState` : résolveur en lecture seule (5 états, registre `ADAPTERS` par slug), aucune
  colonne nouvelle. La traversée solo de l'Intercycle s'y branchera comme 6ᵉ adaptateur — motif
  identique aux 5 existants (session dédiée + `validate_marelle_experience!` + deux écritures).
- `validation_authority` en production : `systeme` 9 · `declarative` 6 · `facilitateur` 1
  (l'Atelier/seuil). La traversée solo sera `systeme` ; la traversée collaborative posera la
  question de la **validation multi-acteurs** (plusieurs membres confirment la tenue de la
  séance) : rien ne l'implémente aujourd'hui, c'est un objet neuf de C4, pas une extension de
  `validation_authority`.
- Idempotence Ω : `gain_points` détruit puis recrée les `Point` du couple (user, challenge) —
  rejouable sans double comptage. **Ne jamais appeler `gain_points` directement** : poser
  `validated_at` par un `update` et laisser le callback faire.

## 4. Oméga et référentiel Skill

- Table `points` : (user, challenge, skill, point) — 186 lignes. Le « total Ω » affiché est la
  somme des points ; il n'existe **ni solde dépensable, ni distinction actifs/historiques** :
  la structure actuelle correspond au futur « Ω générés historiquement » et à rien d'autre.
  Le decay et la ventilation en trois piliers (Lot 5) exigeraient des objets nouveaux
  (`OmegaEvidence`, `OmegaDecayEvent`…) — **aucun n'est à créer maintenant**, et surtout aucune
  réinterprétation des 186 lignes existantes n'est nécessaire ni souhaitable.
- 42 `skills` (référentiel des puissances, scoping par `community_id` déjà audité), 43
  `challenges_skills` porteurs du barème.
- **Barème réel du Monde 0** : 84 Ω requis / 99 Ω avec optionnelles. Distribution actuelle des
  joueurs (hors comptes techniques) : 99, 90, 57, 54, 51, 27, 18, 15, 12.

## 5. Graines de Récit et messagerie

- **Il n'existe pas de modèle Graine.** Une Graine est aujourd'hui un message authoré par le
  joueur dans le thread du `ChallengesUser` de fin de chapitre (`_action_button.html.haml:31`,
  positions 5/10/16). Pas de champ de visibilité, pas de consentement, pas de Résonances.
- Messagerie : engine `mathieu_core_messaging`. `messaging_threads` est polymorphe
  (`container_type/container_id`) — `ChallengesUser` et `JourneysUser` ont chacun `has_one
  :thread`. 67 threads, 86 messages en production.
- **Impact Cercles** : la spec exige la séparation trace individuelle privée / synthèse commune,
  et des consentements de partage révocables. Le thread polymorphe peut porter la synthèse
  commune d'une `CircleSession` (un thread par séance, container = la séance) ; il ne peut **pas**
  porter les traces privées ni les consentements — ces objets sont à créer, pas à greffer sur la
  messagerie. La Fresque de Récit et l'Intention souveraine (Lot 2) exigeront un vrai modèle
  Graine avec visibilité ; le contournement actuel (message dans un thread) ne doit pas être
  étendu au-delà du Monde 0.

## 6. Communautés, droits, abonnements

- **`Community` ne doit pas servir de Cercle**, et l'audit le confirme au-delà de l'argument de
  principe : (a) le scoping des droits DFF (`is_dff?` → visibilité des users par
  `communities_users`) est câblé sur cette table dans `Ability` — y mettre les Cercles ferait des
  co-membres de Cercle des périmètres de droits ; (b) `community_id` scope aussi les `skills`,
  `journeys`, `challenges` — sémantique d'espace pédagogique, pas de groupe de pairs ;
  (c) aucune notion de dates d'appartenance, de statut, de cycle. Deux communautés existent
  (Cercle pédagogique #11, Monde 0 #15 par défaut) et ne bougent pas.
- **Droits** : `User.role` est un enum `{dff: 1, admin: 2}`. Il n'existe **aucun rôle
  facilitateur** — sans impact pour le Lot 1 (autofacilitation : les membres suffisent), requis au
  Lot 2. Recommandation : ne pas étendre l'enum `role` (il pilote l'admin mathieu_core) mais
  porter la facilitation par `CircleFacilitationContract` le moment venu.
- **Abonnements / paiements** : aucune table, aucun code. Confirme le report du Lot 2, déjà
  suspendu au cadrage juridique.

## 7. Ce que cette analyse interdit ou reporte explicitement

- **Aucune modification** de `gain_points`, du barème, ou des 186 `Point` existants.
- **Pas de decay, pas de ventilation trois piliers, pas d'enveloppe de mission** (Lot 5) : les
  formules sont déclarées expérimentales par la spec elle-même.
- **Pas de cagnotte financière** (Lot 2, cadrage juridique préalable).
- **Pas de 360° ni d'évaluations nominatives** (Lot 3) — noter le précédent utile :
  `ressource_evaluations` (signée, révisable, une par joueur et par objet, accès conditionné)
  fournit le motif de départ, mais la politique de conservation/export des feedbacks nominaux
  (§ 18 de la spec) reste ouverte.
- **Pas de moteur de spécialisation des Cercles** (V2).

## 8. Points remontés pour arbitrage ou correctif

### 8.1 Marqueur de passage vers le Monde 1 — le « 100 Ω » est impossible

Options, par ordre de préférence de Claude :

1. **Critère structurel** : le passage M1 = `journey.completed_by?` du Monde 0 **+ Atelier validé**
   (le Challenge `facilitateur`). C'est déjà le critère qu'utilise la Ressourcerie
   (`peut_evaluer_ressources?`) — un seul mécanisme, aucun nombre magique, insensible aux
   évolutions du barème (la scission du Challenge 236 a déjà fait bouger le total une fois).
2. Abaisser le marqueur à 80 Ω (atteignable par le seul requis, de justesse).
3. Recalibrer le barème du Monde 0 pour que le requis atteigne 100 — déconseillé : toucher aux
   `challenges_skills` recalculerait les Ω des joueurs existants au prochain `gain_points`.

### 8.2 Révocation résiduelle sur `JourneysUser`

Aligner `JourneysUser#set_validated_at` sur la décision d'irrévocabilité du 2026-07-28 (même
correctif que `ChallengesUser`), **avant** que C1 ne fasse du Monde 0 validé un prérequis du
Monde 1. Correctif d'une ligne, à faire en tête de C1 avec backup DB préalable.

### 8.3 Validation multi-acteurs des séances collectives

Aucun mécanisme existant ne permet « plusieurs membres confirment la tenue d'une séance ». C'est
un objet propre à `CircleSession` (attestations par membre), pas une extension de
`validation_authority`. À concevoir en C4 ; la traversée collaborative en version hybride
(plateau + compagnon) peut vivre en V1 avec une confirmation simple par les présents.

## 9. Décisions de schéma proposées pour C2 (Lot 1)

Cinq tables, toutes nouvelles, aucune colonne ajoutée aux tables existantes :

| Table | Rôle | Choix notables |
|---|---|---|
| `circles` | identité durable, lignée | `name`, `theme`, `description`, `opener_id`, `parent_circle_id` (filiation, nullable) |
| `circle_cycles` | incarnation | `circle_id`, `starts_on`, `ends_on`, `status` — créée dès le Lot 1 avec un cycle unique ouvert, pour ne jamais rétrofitter l'identité/incarnation |
| `circle_memberships` | appartenance | `circle_cycle_id`, `user_id`, `joined_at`, `left_at`, `status` — l'appartenance vit au niveau du **cycle**, la spec l'exige (instantané de fin de cycle) |
| `pact_source_versions` | Pacte-Source léger | `circle_cycle_id`, `version`, contenu des 5 questions (jsonb), `adopted_at` |
| `circle_sessions` | séances | `circle_cycle_id`, date, protocole, rôles tenus (jsonb en V1 : la rotation n'a pas besoin d'une table dédiée avant le 360°) |

Règles de facture : ActiveRecord standard, **aucun `on_change`**, aucun `receive_message_extra`,
pas de dépendance aux concerns mathieu_core au-delà de l'héritage `ApplicationRecord` (inévitable
dans cette app, passif tant qu'on n'utilise pas ses macros). Objectif : des modèles transplantables
tels quels dans la future appli dédiée sans la gem. Taille 5-8 en validation de modèle,
appartenances multiples permises, aucune écriture d'Ω depuis les objets Cercle en Lot 1.

## 10. Stratégie de retour arrière

- Lot 1 : tables neuves uniquement → rollback = migrations down, aucune donnée existante exposée.
- Le correctif § 8.2 et la création du Journey Boussole : backup `pg_dump` préalable
  (`~/backups/`), comme pour chaque opération de données de ce chantier.
- Aucune modification de YAML mémoïsé sans double restart Puma documenté dans le commit.
- Les scripts one-off restent en scratchpad avec assertions de garde (`count == 1`), motif
  éprouvé sur les 20 derniers déploiements.
