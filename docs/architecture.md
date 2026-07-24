# Ze.game — Architecture

## Présentation

Plateforme d'apprentissage par compétences gamifiée pour des communautés. Les utilisateurs progressent dans des **parcours** (journeys) composés de **défis** (challenges), valident ces défis pour gagner des **points** et développer des **compétences** (skills).

## La boucle de jeu

```
Communauté → Parcours → Défis → Soumission → Validation → Points/Compétences
```

La validation peut être automatique (`auto_validated: true`) ou manuelle via la messagerie contextuelle.

## Stack technique

| Composant | Détail |
|---|---|
| Framework | Rails 8.1.3, Ruby 4.0.0 |
| BDD | PostgreSQL — `zegame_prod` (app) + `zegame_prod_queue` (Solid Queue) |
| Serveur | Puma 7.2 derrière Caddy — port app 6065 |
| File de jobs | Solid Queue |
| Frontend | Hotwire (Turbo Rails 2 + Stimulus 3), Bootstrap 4.6 |
| Vues | HAML |
| CSS | Dart Sass |
| JS Build | esbuild (build.js custom) |
| Auth | Devise 5 + OmniAuth (Google, Microsoft 365, Apple) |
| Uploads | CarrierWave 3 |
| Temps réel | SSE (Server-Sent Events) pour messagerie |
| Déploiement | Capistrano — `~/zegame/current/` |

## Gems privées (framework interne)

- **`mathieu_core`** : DefaultActions, CanCan-like (Ability/authorize_resource), Slugable, multiple_filterable_by, searchable_by, on_change callbacks
- **`mathieu_core_messaging`** : engine Rails — Messaging::Thread, Messaging::Message, Messaging::Mention

## Modèles et relations

### Modèles principaux

| Modèle | Relations clés | Notes |
|---|---|---|
| Community | has_many journeys, skills, groups, challenges, users | Champ `default`, `is_joinable`, `token` |
| Journey | belongs_to community, has_many challenges (via challenges_journeys), pages, journeys_users | `auto_validated`, tags ARRAY PG |
| Challenge | belongs_to community, has_many skills (via challenges_skills), journeys, challenges_users | difficulty 1-5, `auto_validated` |
| Skill | belongs_to community, has_many challenges_skills, points | framework, keywords, url |
| User | rôles enum (dff, admin), has_many points, challenges_users, journeys_users | Devise + OmniAuth |
| JourneysUser | belongs_to journey+user, has_one Messaging::Thread | LTI grade passback, `validated_at` |
| ChallengesUser | belongs_to challenge+user, has_one Messaging::Thread | callback `gain_points` |
| Point | belongs_to user+skill+challenge | trace les points par compétence |
| Page | belongs_to journey | contenu statique, Positionable+Slugable |
| Resource | belongs_to challenge | ressources pédagogiques, Positionable |
| Validation | belongs_to challenge | critères de validation, Positionable |
| Onboarding | belongs_to journey+community | parcours de bienvenue |
| Dff | table liaison User↔Community | rôle DFF par communauté |
| Lti::Setting/Key/State | — | intégration LTI 1.3 |
| Messaging::Thread | polymorphique (container) | via gem mathieu_core_messaging |
| Messaging::Message | belongs_to thread, auteur polymorphique | — |

## Zones de l'application

### Zone publique (auth requise)
- **Home** : logbook utilisateur, parcours en cours
- **Journeys** : liste et détail des parcours
- **Challenges** : détail d'un défi dans le contexte d'un parcours
- **JourneysUsers** : s'inscrire à un parcours, restart
- **ChallengesUsers** : soumettre/valider un défi, restart
- **Communities** : liste, rejoindre par token
- **Users** : profil, édition, stats personnelles (points par compétence)
- **Threads** : messagerie contextuelle
- **Pages** : pages de contenu des parcours

### Zone admin (`/admin`)
- CRUD complet : challenges, journeys, skills, users, communities+groupes
- Suivi des soumissions (ChallengesUsers) et inscriptions (JourneysUsers)
- Import/export JSON et Markdown pour journeys et challenges
- Création d'utilisateurs en masse (CSV/JSON)
- Clone de ressources (journeys, challenges, skills)

### Zone LTI (`/lti`)
- Flux OIDC LTI 1.3 : `POST /lti/initiate-login` → LMS → `POST /lti/launch`
- Auto-création compte depuis JWT LTI
- Grade passback asynchrone (`Lti::LtiUpdateScore` job)
- Clés RSA publiques : `GET /lti/keys`

### Mobile (Hotwire Native)
- `/.well-known/assetlinks.json` — deep links Android (package `ze.game.store`)
- `/.well-known/apple-app-site-association` — deep links iOS (bundle `game.ze.ze-game`)
- Configurations de paths iOS/Android dans `hotwire/`

### Autres routes
- `/sse` — Server-Sent Events (messagerie temps réel)
- `/jobbbs` — MissionControl::Jobs (monitoring Solid Queue)
- `/up` — health check

## Particularités techniques

- Extension PostgreSQL `unaccent` activée (recherche sans accents)
- Tags en ARRAY PostgreSQL natif sur Journey et Challenge
- JSONB pour `skill_details` dans les scopes de Journey
- `goldiloader` : eager loading automatique (anti N+1)
- `has_scope` + `inherited_resources` : CRUD standard généré
- `pagy` : pagination
- `deep_cloneable` : clonage récursif des objets
- TinyMCE 8 : éditeur WYSIWYG pour les contenus
- Chart.js 4 : graphiques stats
- Playwright : tests E2E
- `exception_notification` → no-reply-bugs@rbean.io en production

## 8. Dépendances à `mathieu_core` / `mathieu_core_messaging`

<!-- Ajout Claude, 2026-07-12 -->

Cartographie complète pour arbitrer entre repartir sur une nouvelle base ou évoluer l'existant. Gems privées mono-mainteneur : `git@github.com:mathieumahe/mathieu_core.git` et `git@github.com:mathieumahe/mathieu_core_messaging.git`, épinglées sur une révision git précise (pas une release semver).

### Contrôleurs — dépendance structurelle forte

`DefaultActions` (`< InheritedResources::Base`) est la classe de base de ~15 contrôleurs sur ~18 (tout l'admin, Journeys/Challenges/Communities publics, LTI, Threads). Fournit CRUD standard, pagination (Pagy), layout embedded-frame (Hotwire Native), et injecte `Sortable`, `Searchable`, `RangeFilterable`, `BooleanFilterable`, `MultipleFilterable`, `InputFilterable`, `Cansable`.

### Autorisation — logique métier déjà applicative

La gem fournit seulement `AbilityBase` (DSL générique `model`/`roles`/`no_roles`/`scope`/`can?`). Toutes les règles métier réelles vivent dans `app/models/ability.rb` (~230 lignes), lisible et modifiable directement.

### Modèles — usage ciblé

| Concern gem | Modèles concernés | Poids du couplage |
|---|---|---|
| `BaseMathieuCoreRecord` + `Cans` | Tous (via `ApplicationRecord`) | Recherche globale, strip strings, DSL `on_change` (wrapper de `after_commit`) |
| `Slugable` | Challenge, Community, Group, Page, Skill, User | Override `find`/`to_param`, génération de slugs — couplage non trivial |
| `Positionable` | ChallengesJourney, Page, Resource, Validation | Triviale (7 lignes) |
| `CleanHtmlTiny` | Challenge, Community, Journey, Skill, Resource, Page, Validation | Sanitization contenu TinyMCE |
| `HasMultipleParts` | Journey seul | — |
| `BaseUser` | User seul | — |

La logique métier réelle (`gain_points`, `set_validated_at`, `send_data_to_lti` dans `ChallengesUser`/`JourneysUser`) vit dans les modèles applicatifs, pas dans la gem — `on_change` n'est qu'un wrapper de 3 lignes autour de `after_commit ... if: saved_change_to?`.

### Vues — couplage le plus profond

~25 composants Ruby (`dropitem`, `circle_image`, `title`, `back_to`, `pagination`, `sidemenu`, `table_*`, `badge`, `light_form_for`, `preview_stars`, `nested_fields`...) utilisés dans quasiment chaque vue HAML. Tout le langage visuel de [design.md](design.md) (badges, titres striked, rubans, blocs LEVEL/DURATION/POINT) passe par ces composants.

### Front-end JS — framework quasi complet externalisé

~35 modules JS (formulaires, drag & drop, Sortable, wrapper TinyMCE, SSE, Chart.js, notifications navigateur, upload preview, mass-create...) fournis par la gem et chargés via l'importmap (`app/javascript/application.js.erb`).

### Messagerie — moteur externe complet

`MathieuCoreMessaging::Engine` monté à la racine (`/`). Seules 3 vues sur ~10 sont surchargées localement (`threads/index`, `threads/show`, `messages/_fields`) ; le reste est rendu depuis la gem. Point d'extension : `container.try(:receive_message_extra, message, extra)`.

### Autres points sans surcharge locale

`SseController`, `UploadedFilesController`, contrôleurs de deep links Hotwire Native (iOS/Android), `MissionControlAdminController`, upload d'images (`SquareImageUploader`), email transactionnel (`CustomDeviseMailer`/`SendMyMailModule`), déploiement (tâches Capistrano `mathieu_core_deploy.rb`).

### Décision opérationnelle du 2026-07-24

Pour le Festival du 1er octobre 2026, Point Zéro doit devenir une application Rails autonome, sans dépendance d'exécution aux gems privées `mathieu_core` et `mathieu_core_messaging`, avec une base séparée. La stratégie ne consiste pas à réécrire le domaine : elle part de la branche `pointzero`, caractérise les comportements utiles par des tests, puis remplace uniquement l'infrastructure effectivement utilisée. Le cadrage canonique, le calendrier et les critères de bascule sont décrits dans [vision/application-festival-2026.md](vision/application-festival-2026.md).

Cette décision remplace la recommandation historique ci-dessous pour la trajectoire Festival.

### Recommandation historique (2026-07-12)

Ne pas repartir sur une nouvelle base applicative. Le domaine métier (Journey/Challenge/JourneysUser/ChallengesUser/Ability) est déjà propre et applicatif — le réécrire ne l'améliorerait pas. Ce que fournit la gem est de l'infrastructure qui fonctionne (CRUD, filtres, composants de vue, JS, upload, mail, déploiement) ; la reconstruire coûterait des mois pour zéro gain de domaine.

Le risque réel n'est pas technique mais de gouvernance : gems privées mono-mainteneur épinglées sur une révision git. Vu l'horizon pluriannuel de la [vision produit](vision/README.md), ce point mérite une conversation explicite avec le mainteneur sur son engagement de maintenance, plutôt qu'une réécriture préventive.

Pour la vision monde-miroir (avatar, salles de quête, mana, récit-fresque) : ces écrans n'ont probablement pas besoin du paradigme CRUD/admin de `DefaultActions`. Construire cette couche avec ses propres contrôleurs/vues en dehors de ce moule, en réutilisant les modèles et l'auth existants — sur le modèle de ce que fait déjà partiellement le namespace `Lti::`.
