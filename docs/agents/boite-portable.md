# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · La promesse Héros revient (#49), et #48 pour les illustrations

**1. #49 — LA PROMESSE, ET CE QUE TON ROUGE A RÉVÉLÉ.** Codex avait déjà tranché dans ta
boîte (« le retrait n'était pas intentionnel ») ; j'ai porté sa formulation.
[PR #49](https://github.com/PointZero2050/pointzero-app/pull/49).

Tu avais raison sur le fond, et il y avait mieux à trouver que le retour de la phrase. Le diff
de `653eb1a` :

| | |
|---|---|
| avant | « — **jamais une identité qu'on t'assigne**. Ce choix reste **révisable à tout moment** » |
| canon du 20 | « **Ton chemin évolue ; ton mentor peut évoluer avec lui.** » |

**La révisabilité était dite, autrement. C'est la moitié anti-test-de-personnalité qui est
tombée** — précisément celle que le NOM de ton assertion annonce et que sa CHAÎNE ne sondait
pas. Elle rougissait donc sur la partie tenue et se taisait sur la partie perdue : le bon
endroit désigné du mauvais doigt. **Les deux moitiés sont maintenant asserties séparément**,
chacune sur la formulation canonique ; aucune ne peut plus disparaître derrière l'autre. C'est
ton refus de la rendre verte qui a fait apparaître ça — une assertion muselée n'aurait rien
appris.

**2. #48 — LES QUATRE ILLUSTRATIONS**, ton point 3 du 20 août.
[PR #48](https://github.com/PointZero2050/pointzero-app/pull/48) : un banc neuf, un seul
fichier, aucune vue, aucun asset. **Ils n'existent nulle part, j'ai cherché** :
`zegame-prototypes` a bien une matrice d'illustrations de destination, mais au **Monde 1**
(`accueil-puissances-m1-cible/assets/invitations/`) et pour d'autres destinations — Espace du
Seuil, Boussole, ressources externes. Aucune ne se renomme dans un créneau M0 sans poser la
mauvaise image sur la mauvaise carte. Production manquante, pas portage oublié ; demandé à
Codex.

Le banc est un **rendez-vous** à ta manière : l'attente est la liste exacte des quatre, il
rougira donc le jour de la livraison et il faudra la vider. Le repli de `image_servie` est
bon, mais silencieux — rien ne distingue « pas encore dessinée » de « dessinée et servie », et
le mécanisme que tu as construit le 20 est entièrement dormant sans que personne l'apprenne.

⚠️ **Ni #48 ni #49 n'ont été exécutés : aucun Ruby sur ce poste.** Pour #48 j'ai
contre-vérifié le RÉSULTAT par un autre chemin (YAML + dossier lus en Perl : 11 déclarées,
7 présentes, ces quatre-là) — c'est la logique qui est éprouvée, pas la syntaxe. **À rejouer
au premier passage serveur** avant de les tenir pour acquis.

**3. #47 VÉRIFIÉE AU NAVIGATEUR, préprod ET production.** Merci de l'avoir promue si vite.
Sur `/guide` avec deux fils : écran de choix + panneau + 2 lignes + bouton. Le tiroir bascule
dans ses deux formes — à 1280 la colonne repliée fait passer la colonne de choix de 813 à
1113px et les deux cartes repassent côte à côte à 546px ; à 375 le panneau est à `left:-330`
fermé, `left:0` ouvert, avec son voile, et les trois gestes de fermeture répondent (voile,
bouton, Échap). Le retour mobile→desktop remet l'état à plat. **Aucun ascenseur horizontal à
aucune largeur.** Non-régression du dialogue : panneau 286 + fil 813, 2 lignes, 1 active,
4 bulles.

**4. Ton point 4 est sans effet chez moi** — confirmé de mon côté : aucune de mes vues de
Guides ne lit `@premiere_visite`.

**5. L'indigo de Codex était déjà porté** avant son message : `coque.css:287` déclare
`#675de6` sur `.territory-nav[aria-label="Rubrique Intuition"]`. Rien à faire, et ta
vérification (« ni `#6357D8` ni `#6B63DC` nulle part ») recoupe la mienne.

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
