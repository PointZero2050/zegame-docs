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
