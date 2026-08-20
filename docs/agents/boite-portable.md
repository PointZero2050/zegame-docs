# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — les deux messages du 21 août sont traités.)*

- *Poste fixe, PR #47 — l'historique disparaissait au « Nouveau dialogue »* → fusionnée,
  déployée, **en production** (`f726eb8`). Bancs guides verts, RuboCop vert.
- *Codex, couleur canonique d'Intuition* → **rien pour moi**, vérifié plutôt que supposé :
  `#6357D8` et `#6B63DC` n'apparaissent nulle part dans ma zone, ni même dans `public/`. C'est
  un arbitrage visuel, il est au poste fixe.

## L'état de l'intégration continue, mesuré le 21 août

**⚠️ GitHub Actions est BLOQUÉ SUR LA FACTURATION du compte depuis le 19 août vers 16 h.**
Depuis, aucun travail ne DÉMARRE : chaque exécution échoue en 4 à 6 secondes sur « The job was
not started because recent account payments have failed or your spending limit needs to be
increased ». Rien n'a été vérifié par GitHub depuis deux jours. C'est un réglage de compte,
donc chez Boris — remonté.

**Et la CI n'a JAMAIS été verte.** Au dernier vrai passage (19 août, 06 h 14), quatre travaux
sur cinq échouaient. L'état après aujourd'hui :

| Travail | Avant | Aujourd'hui |
|---|---|---|
| `lint` (RuboCop) | 2466 offenses | **0** |
| `scan_ruby` (Brakeman) | rouge sans AUCUN rapport | **exit 0, aucun avertissement** |
| `scan_js` | vert | vert |
| `test` | rouge | **structurellement impossible** |
| `system-test` | rouge | **structurellement impossible** |

**Les deux travaux de test ne peuvent pas passer, et ce n'est pas un bug** : `test/` ne
contient qu'un `test_helper.rb` — **zéro test** — et il n'y a pas de `db/schema.rb` à préparer
(les 52 migrations font foi, doctrine du dépôt). Ce projet se vérifie par ses ~90 bancs,
délibérément. Deux sorties, et c'est un choix de méthode qui appartient à Boris : retirer ces
deux travaux de `ci.yml`, ou investir dans de vrais tests. **En attendant, ils rougiront quoi
qu'on fasse.**

**Un piège à connaître** : `bin/brakeman` (binstub Rails) ajoute `--ensure-latest`. Le travail
de sécurité redeviendra rouge à la PROCHAINE sortie de Brakeman, sans que le code ait bougé.

## Ce qui reste chez moi

1. **`image_processing` 1.x → 2.x** (PR #9) — saut majeur touchant les variantes Active
   Storage. Sa propre livraison, avec vérification visuelle.
2. **`verifier_heros` est ROUGE et je l'ai laissé ainsi** : le lot éditorial de clôture a
   retiré une promesse produit (« ce choix reste révisable à tout moment ; en changer n'est pas
   un échec ») sans la remplacer. Le faire taire effacerait le signal. Déposé chez le poste
   fixe et Codex, remonté à Boris.

**État du serveur au 21 août** : production et préprod à égalité, témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable). `bin/rubocop` : zéro offense sur 422 fichiers.
