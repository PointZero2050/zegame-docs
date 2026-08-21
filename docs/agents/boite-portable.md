# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — les quatre messages du 21 août sont traités.)*

- *Poste fixe, PR #47* → en production (`f726eb8`).
- *Poste fixe, PR #49 (la promesse des Héros) et #48 (illustrations déclarées)* → fusionnées,
  **en production** (`83bf69c`). La #48 portait un défaut invisible sans exécution — voir sa
  boîte : le banc neuf ÉCRASAIT `verifier_illustrations_m0.rb` et ses 25 assertions. L'ancien
  est restauré, le neuf vit dans `verifier_illustrations_declarees.rb`, les deux sont verts.
- *Codex, illustrations livrées + libellés canoniques* → le `detail` de Communication est
  canon en production ; les quatre `.webp` sont dans `zegame-prototypes` (`c293f57`, révision
  `073d96f`), **leur pose dans `public/pz/m0/powers/` revient au poste fixe** — le rendez-vous
  de `verifier_illustrations_declarees` rougira à ce moment-là, comme prévu.
- *Codex, couleur d'Intuition* → rien pour moi, déjà porté par le poste fixe (`coque.css:287`).

## La CI, après déblocage de la facturation (merci)

Premier verdict réel depuis le 19 août : **lint, Brakeman et scan_js VERTS** — la journée
d'hier a tenu. Les deux travaux de test mouraient sur « db/schema.rb doesn't exist yet » :
ils vérifient désormais ce que le dépôt tient VRAIMENT — les 52 migrations construisent une
base depuis RIEN (répété sur le serveur avant de pousser : « Boot OK — 72 tables ») et
l'application démarre dessus, eager loading compris. Le jour où de vrais tests arrivent dans
`test/`, ils redeviennent `db:test:prepare test` — les commentaires du fichier le disent.

## Ce qui reste chez moi

**`image_processing` 1.x → 2.x** (PR #9) — saut majeur touchant les variantes Active Storage.
Sa propre livraison, avec vérification visuelle.

**État du serveur au 21 août** : production et préprod à égalité, témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable). Tous les bancs joués aujourd'hui sont verts,
`verifier_heros` compris — la promesse est revenue.
