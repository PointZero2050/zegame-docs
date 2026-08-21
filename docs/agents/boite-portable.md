# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — tout le courrier du 21 août est traité, et la liste des chantiers du portable est
VIDE pour la première fois.)*

## Le 21 août en trois lignes

- **La CI est verte, cinq travaux sur cinq — la première fois de l'histoire du dépôt.**
- **PR #47, #49, #50 en production** ; la #48 a été remplacée par #50 après le sauvetage des
  25 assertions ; les quatre illustrations de destination sont SERVIES (200 en production) —
  le mécanisme du 20 août a enfin quelque chose à montrer.
- **`image_processing` 2.x en production** (`a2c0e2a`, puis `5bb34c7`) — DEUX pièges, pas
  un. En 2.x le processeur devient optionnel : `ruby-vips` doit se déclarer soi-même, sans
  lui le BOOT casse au précompile. Puis **la CI a attrapé ce qu'aucun banc ne pouvait voir**
  (ils tournent dans le conteneur, où libvips existe) : déclarée sans `require: false`, la
  gem chargeait vips AU BOOT via Bundler.require, et `scan_js` — un runner sans libvips
  système — cassait sur `vips.so.42`. `require: false` rétablit la paresse ; le Gemfile
  raconte l'histoire. Variant réel prouvé des deux côtés, **CI verte cinq sur cinq après
  correctif**. La PR Dependabot #9 se fermera seule.

## Ce qui n'attend personne mais reste bon à savoir

- `verifier_illustrations_declarees` a l'attente VIDE : il rougira à la première illustration
  déclarée sans fichier. Ne jamais y remettre un nom pour faire passer un banc.
- `bin/brakeman` redeviendra rouge à la prochaine sortie de Brakeman (`--ensure-latest` du
  binstub Rails) : la réponse est `bundle update brakeman --conservative`, pas un contournement.
- Le jour où de vrais tests arrivent dans `test/`, les travaux `test` et `system-test` de
  `ci.yml` redeviennent `db:test:prepare test` — les commentaires du fichier le disent.

**État du serveur au 21 août** : production et préprod à égalité (`a2c0e2a`), témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable), tous bancs joués verts, CI verte.
