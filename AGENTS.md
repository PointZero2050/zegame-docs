# Ze.game — Contexte pour Codex / agents IA

## Ce qu'est l'application

Plateforme d'apprentissage par compétences gamifiée pour des communautés. Les utilisateurs progressent dans des **parcours** (journeys) composés de **défis** (challenges), valident ces défis pour gagner des **points** et développer des **compétences** (skills).

Voir [docs/architecture.md](docs/architecture.md) pour l'architecture complète.

Pour les évolutions liées au Point Zéro, à la Marelle Oméga et aux mondes, lire également [docs/point-zero-marelle.md](docs/point-zero-marelle.md).

## Stack

Rails 8.1.3 · Ruby 4.0.0 · PostgreSQL · Puma · Caddy · Hotwire (Turbo + Stimulus) · HAML · Solid Queue · Capistrano

## Conventions de code

- Vues en **HAML** (pas ERB)
- Contrôleurs admin dans `app/controllers/admin/`
- Modèles LTI dans namespace `Lti::`
- Messagerie via namespace `Messaging::` (gem `mathieu_core_messaging`)
- Bootstrap 4.6 pour le CSS
- JS buildé via **esbuild** (`yarn build`) — pas d'importmap
- CSS compilé via **Dart Sass** (`yarn build:css`)

## Framework interne (gem privée `mathieu_core`)

L'application s'appuie sur une gem privée qui fournit :
- `DefaultActions` : actions CRUD standard dans les contrôleurs
- Système d'autorisation type CanCan (`Ability`, `authorize_resource`)
- `Slugable` : slugs automatiques
- `multiple_filterable_by`, `searchable_by` : filtres et recherche
- `on_change` callbacks : réaction aux changements d'attributs des modèles
- `Positionable` : tri par position

⚠️ En cas de comportement inattendu dans un contrôleur ou un modèle, la cause est souvent dans cette gem.

## Points d'attention

- Toujours tester sur https://vibe.ze.game après une modification significative
- Les modèles centraux (Journey, Challenge, ChallengesUser, JourneysUser) ont des callbacks complexes — modifier avec précaution
- `goldiloader` gère le eager loading automatiquement — ne pas ajouter d'includes manuels sauf nécessité
- L'extension PostgreSQL `unaccent` est disponible pour les recherches

## Collaboration Codex / Claude Code

Note Codex - 2026-06-14.

- Un seul agent travaille a la fois sur une meme zone de code.
- Le bon agent pour modifier ou relire une zone est celui qui a le contexte le plus frais sur les fichiers concernes.
- Une unite de travail doit se terminer par un commit, ou au minimum par un diff/stash clairement identifie, avant passation a l'autre agent.
- Pour les zones sensibles (`Journey`, `Challenge`, `ChallengesUser`, `JourneysUser`, progression, validation, points, LTI, messagerie), faire une analyse d'impact avant implementation.
- Les mises a jour de documentation ajoutees par Codex doivent etre signalees avec une mention `Note Codex` ou `Ajout Codex`.

## Structure des dossiers clés

```
app/
  controllers/
    admin/          ← zone administration
  models/           ← tous les modèles
  views/            ← vues HAML
  javascript/       ← JS Stimulus + Turbo
  components/       ← ViewComponents éventuels
config/
  routes.rb         ← toutes les routes
db/
  schema.rb         ← schéma complet de la BDD
docs/
  architecture.md   ← documentation architecture complète
```

## Convention de signature

Les modifications de cette documentation indiquent leur provenance :
- Commits préfixés `[Claude]` → produits par Claude Code
- Commits préfixés `[Codex]` → produits par Codex

Cela permet de tracer qui a écrit quoi et de détecter d'éventuelles incohérences entre les deux agents.
