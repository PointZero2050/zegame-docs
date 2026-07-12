# Ze.game — Contexte pour Claude Code

## Connexion serveur

```bash
ssh -i /c/Users/Boris/.ssh/id_ed25519 daployar@vibe.ze.game
```

- Accès root : `sudo su` une fois connecté
- App déployée : `~/zegame/current/` (symlink Capistrano)
- URL production : https://vibe.ze.game

## Architecture

Voir [docs/architecture.md](docs/architecture.md) pour la documentation complète.

Pour la vision produit idéale (Marelle Oméga, mondes, monde-miroir, messagerie, ressourcerie, marketplace, moteur de validation, game design), voir l'index [docs/vision/README.md](docs/vision/README.md).

Les prototypes d'interface (HTML autonomes) vivent dans le repo dédié [zegame-prototypes](https://github.com/PointZero2050/zegame-prototypes), cloné sur le serveur dans ~/zegame-prototypes/. Un dossier par prototype, conventions dans son README.

## Stack en bref

Rails 8.1.3 · Ruby 4.0.0 · PostgreSQL · Puma · Caddy · Hotwire · HAML · Solid Queue · Capistrano

## Points d'attention pour le développement

- **`mathieu_core`** est une gem privée boîte noire — tout comportement inattendu (callbacks, autorisations, scopes) peut venir de là
- Les modifications des modèles centraux (Journey, Challenge, ChallengesUser, JourneysUser) peuvent avoir des effets de bord via les callbacks `on_change` de mathieu_core
- Tester manuellement sur https://vibe.ze.game après chaque évolution significative
- Les fichiers de vues sont en **HAML** (pas ERB)
- Le JS est buildé via **esbuild** (pas importmap) — lancer `yarn build` après modif JS
- Le CSS est compilé via **Dart Sass** — lancer `yarn build:css` après modif SCSS
- Bootstrap 4.6 (pas Bootstrap 5)

## Déploiement

```bash
# Depuis la machine de développement avec Capistrano configuré
bundle exec cap production deploy
```

## Conventions

- Contrôleurs admin dans `app/controllers/admin/`
- Modèles LTI dans namespace `Lti::`
- Messagerie via engine `mathieu_core_messaging` (namespace `Messaging::`)
- Vues en HAML, partials préfixés `_`
- Jobs Solid Queue dans `app/jobs/`
