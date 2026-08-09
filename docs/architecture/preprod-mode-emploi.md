# Préprod Point Zéro — mode d'emploi

*Montée le 2026-08-05 par l'instance portable, à la demande de l'instance poste fixe qui
travaille les mini-jeux et les pages du site.*

## À quoi elle sert

Vérifier au navigateur un travail avant qu'il touche la production. Elle existe parce qu'un
agent qui livre du code doit pouvoir en voir le rendu réel sans que la moindre erreur atteigne
les 634 abonnés, les 31 comptes ou la billetterie.

## URL

<https://preprod.167-233-210-57.sslip.io>

Accessible en lecture sans mot de passe, en HTTPS, `X-Robots-Tag: noindex, nofollow`
(aucune indexation, aucun risque de doublon SEO avec le vrai site).

`preprod.pointzero2050.com` est également déclaré dans le Caddyfile : le jour où un
enregistrement A pointe vers `167.233.210.57`, le certificat se prend tout seul et l'adresse
fonctionne. Rien à faire d'ici là — `sslip.io` résout le nom en IP sans aucune action DNS.

**Compte de démonstration** : `demo@preprod.local` / `preprod-demo-2026`, administrateur.
Il donne accès au jeu **et** à la console de gestion. Ce n'est le compte de personne : la
préprod ne contient aucun compte réel, et on ne s'y connecte jamais avec une adresse qui
appartient à quelqu'un.

## Ce qu'elle contient — et ce qu'elle ne contient pas

| Présent | Absent, délibérément |
|---|---|
| 3 parcours, 22 expériences, 4 pages | Les 31 comptes joueurs |
| 42 compétences, 13 ressources | Les 634 abonnés newsletter |
| 3 communautés (dont Monde 0) | Les Oméga, messages de Cercle, Graines |
| Le site public et le Sas en entier | Les inscriptions et les paiements |

Sa base de données lui appartient (`preprod-db`), séparée de la production. Elle n'a **ni
identifiants SMTP ni clés Stripe** : un envoi de courriel y est journalisé, pas expédié, et
aucun paiement ne peut y être déclenché même par erreur.

Pour la re-semer après une manipulation : réexécuter `scripts/semer_preprod.rb` (extrait le
contenu de la production, ne copie jamais les tables personnelles).

## Circuit de livraison

La branche `preprod` du dépôt `pointzero-app` est ce que la préprod sert.

**Si l'instance poste fixe a le droit d'écriture** — elle pousse sur `preprod`, prévient,
l'instance portable déploie et relit. C'est le circuit le plus court.

**Sinon** — elle livre un diff (ou les fichiers complets, avec leur chemin) ; l'instance
portable l'applique sur `preprod`, déploie, et donne l'URL à vérifier. Deux échanges au lieu
d'un, mais rien ne bloque.

Dans les deux cas : **la préprod se relit avant que la production soit touchée**, et c'est
l'instance portable qui déploie en production — elle seule porte la clé SSH.

```bash
# côté serveur, déployer la branche preprod (instance portable)
cd /home/deploy/src/pointzero-preprod && git pull --ff-only origin preprod
cd /home/deploy/preprod && docker compose up -d --build preprod-web
```

## Reporter un prototype du Sas

Le report d'un prototype vers l'application est un **script**, pas une reprise à la main :
`scripts/porter_sas.py` dans `pointzero-app`.

```bash
python3 scripts/porter_sas.py humanite   # ou sans argument : les cinq parcours
```

Il lit `zegame-prototypes/parcours-<slug>/` (index.html, styles.css, app.js) et produit la vue
`app/views/sas/<slug>.html.erb` plus les assets dans `public/sas/<slug>/`. Les seules libertés
prises à l'intégration sont énumérées en tête du script et nulle part ailleurs : barre d'auteur
retirée, chemins d'assets réécrits, cartes de l'accueil ouvertes vers les parcours en ligne,
enchaînement d'un parcours au suivant. Si l'une de ces formes disparaît du prototype, le script
s'arrête en le disant — il ne produit pas une page silencieusement amputée.

Le `?v=` des assets est une empreinte de leur contenu : un visiteur ne peut pas se retrouver
avec l'ancien script et le nouveau HTML.

**Le serveur n'a pas accès à `zegame-prototypes`** (sa clé de déploiement est limitée à
`pointzero-app`, et c'est voulu). L'instance portable copie les prototypes depuis son clone
local vers `/home/deploy/src/zegame-prototypes/` avant de lancer le script.

## Promotion vers la production

La préprod n'est pas une antichambre automatique. Une fois le rendu validé sur la préprod par
qui a produit le contenu, l'instance portable reporte la branche sur `main` et déploie. Rien ne
part en production sans cette relecture : celui qui produit ne s'auto-valide pas.

## Rappel de périmètre

Le prototype reste la référence de construction : la préprod montre ce que l'application rend,
elle ne redéfinit pas ce que le prototype a fixé. Si les deux divergent, c'est l'application
qui a tort.

## Accès SSH du poste fixe (2026-08-10, décision Boris)

Le poste fixe dispose désormais d'un accès SSH direct au serveur — clé `boris@sirbey.com`
ajoutée par l'instance portable à la demande de Boris, pour l'import des événements de
l'agenda (https://pointzero2050.com/event/) en préprod.

```bash
ssh deploy@167.233.210.57
```

**Le périmètre ne change pas, seul le chemin change.** Ce que le poste fixe touche :

- `~/src/pointzero-preprod/` — la branche `preprod`, dans les zones convenues ;
- la préprod se reconstruit ainsi (le conteneur COPIE les sources, un simple restart ne
  suffit pas) :

```bash
cd ~/preprod && docker compose build preprod-web && docker compose up -d preprod-web
```

- migrations préprod : `docker exec -e RAILS_ENV=production pointzero-preprod-preprod-web-1 bin/rails db:migrate` ;
- scripts ponctuels : `docker cp fichier.rb pointzero-preprod-preprod-web-1:/tmp/` puis
  `docker exec -e RAILS_ENV=production pointzero-preprod-preprod-web-1 bin/rails runner /tmp/fichier.rb`.

**Ce que le poste fixe ne touche pas** (répartition phase 2, inchangée sur le fond) :

- `~/deploy/` et les conteneurs `pointzero-web-1` / `pointzero-db-1` : la PRODUCTION reste à
  l'instance portable, promotion par cherry-pick après relecture — celui qui produit ne
  s'auto-valide pas ;
- `~/sauvegardes/`, `~/.ssh/`, la configuration Docker et Caddy ;
- les secrets (`.env`) : les lire n'est jamais nécessaire pour la préprod.

Convention de commits inchangée : `[Codex]` ou `[Claude]` selon l'instance, sur la branche
`preprod` uniquement. Avant de commencer : `git -C ~/src/pointzero-preprod fetch && git status`
— l'instance portable travaille sur le même clone.
