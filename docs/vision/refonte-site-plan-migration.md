# Migration du site — plan opérationnel

> Rédigé par Claude le 2026-08-01. Fait suite à la décision de Boris : **priorité à la
> migration complète, dans les jours qui viennent** ; le nettoyage de l'infection WordPress
> (confirmée par Wordfence) est écarté au profit de l'extinction du site infecté. Une passe
> sécurité dédiée aura lieu plus tard.
> Cadrage amont : [refonte-site-pointzero2050.md](refonte-site-pointzero2050.md) et
> [refonte-site-revision-editoriale.md](refonte-site-revision-editoriale.md).

## 1. État réel constaté (2026-08-01)

- **La branche `festival-standalone` n'existe pas.** `zegame-app` ne contient que `master`,
  `pointzero`, `codex/finition-puissances` et `codex/pensees-visuels-series`. L'application
  autonome décrite dans [application-festival-2026.md](application-festival-2026.md) n'est pas
  commencée, alors que le calendrier de référence la prévoyait prête au 31 juillet.
- **Il n'existe donc aucune application cible où poser le site aujourd'hui**, sinon le bac à
  sable `vibe.ze.game`, qui dépend de `mathieu_core` et partage la base de ze.game.
- **Contradiction canonique à trancher** : `application-festival-2026.md` §5 pose que « la
  billetterie existante Event Tickets Plus + WooCommerce + Stripe reste la source d'achat
  recommandée pour le Festival ». L'option A décidée le 2026-07-31 la déplace vers l'appli.
  La décision de Boris est postérieure et mieux informée (compromission avérée, ventes non
  commencées, une seule commande de test) — mais l'écart doit être acté explicitement, pas
  subi.

## 2. Recommandation : le site public est la première tranche autonome

Un site public **n'a besoin d'aucune capacité de `mathieu_core`** : ni authentification, ni
`Journey`, ni `Challenge`, ni progression. C'est donc la tranche verticale autonome la moins
chère à livrer, et elle sert trois objectifs d'un coup :

1. elle éteint le site compromis rapidement ;
2. elle amorce concrètement l'application autonome exigée pour le Festival, au lieu de la
   repousser ;
3. elle porte la billetterie en Stripe Checkout, donc supprime la dépendance WooCommerce.

Périmètre technique de la tranche : pages de contenu versionnées, formulaire de contact,
inscription newsletter, événements et inscriptions gratuites, billetterie payante par Stripe
Checkout, redirections 301. Rails 8 sans gems privées, base propre, déploiement propre.

## 3. Le vrai chemin critique est éditorial, pas technique

Le risque de calendrier n'est pas la brique Rails : c'est la reprise de 105 pages et 33
articles. **Règle proposée pour ne pas bloquer la bascule** : le corpus Livre I migre *en
masse et tel quel*, assaini mais non réécrit ; la reprise de surface se fait ensuite, en
ligne, page par page. Seules les pages neuves (accueil, portes, jeu d'auto-positionnement,
Récit, porte Chrysalides) sont rédigées avant bascule — c'est le lot 1, déjà livré, plus les
lots 2 et 3.

Corollaire : l'import doit **filtrer les iframes injectées** (`div.show`) au passage, sur les
105 pages et 33 articles. C'est non négociable : sans ce filtre, on transporte l'infection
dans la pile neuve.

## 4. Séquence proposée

| Étape | Contenu | Dépend de |
|---|---|---|
| 0 | Sauvegardes : export DB WordPress complet, export MailPoet CSV avec listes et étiquettes, copie des 807 médias | — |
| 1 | Création de la branche/app autonome, squelette Rails 8, déploiement à blanc | Q1 ci-dessous |
| 2 | Import assaini du corpus (pages + articles + médias), en conservant les URLs | étape 0 |
| 3 | Pages neuves (lots 1 à 3), navigation à trois portes, jeu d'auto-positionnement | contenu rédigé |
| 4 | Formulaires : contact, newsletter | Q3 ci-dessous |
| 5 | Événements + inscriptions gratuites + billetterie Stripe Checkout | Q2 ci-dessous |
| 6 | Bascule DNS, redirections 301, extinction de WordPress | tout ce qui précède |

## 5. Point Stripe

Les clés Stripe **live** sont stockées dans la base d'un site compromis. Pour la nouvelle
application, ne pas recopier ces clés : **générer des clés neuves depuis le tableau de bord
Stripe et révoquer les anciennes au moment de l'extinction de WordPress**. C'est gratuit,
immédiat, et cela referme le seul vecteur à conséquence financière directe — sans nécessiter
la passe sécurité complète que Boris a reportée.

## 5 bis. Décisions Boris — 2026-08-01

1. **Objectif confirmé** : migrer *l'ensemble* des fonctionnalités WordPress vers un outil
   dédié, intégré au workflow de l'application.
2. **La billetterie bascule maintenant.** Motif : peu d'inscrits aux événements aujourd'hui,
   le flux ne reprend qu'en septembre. `application-festival-2026.md` §5 a été amendé en
   conséquence.
3. **Clés Stripe** : nouvelles clés pour l'application, révocation des anciennes à
   l'extinction de WordPress.

## 6. Hébergement — recommandation

**Un serveur dédié à Point Zéro, distinct de `vibe.ze.game`, avec la même pile.**

Le site et l'application ne font qu'un : la question n'est donc pas « où héberger le site »
mais « où vit l'application Point Zéro autonome ». La réponse ne peut pas être le bac à sable
ze.game, pour quatre raisons :

- l'autonomie vis-à-vis de ze.game est l'objet même du chantier, y compris juridiquement
  (Point Zéro et ze.game sont deux structures) ;
- la base séparée est déjà exigée par le cadrage Festival ;
- `vibe.ze.game` est un bac à sable de validation produit : il doit rester cassable. Un site
  public avec paiement ne peut pas partager ce sort ;
- le 1er octobre concentrera du trafic et des paiements sur quelques heures.

Pile recommandée, identique à l'existant pour que le savoir-faire soit transférable : un VPS
Linux, PostgreSQL, Puma derrière Caddy, Rails 8. **Déploiement par Kamal** (défaut Rails 8,
plus simple que Capistrano pour une application neuve sans historique) — sauf si l'habitude
Capistrano de l'équipe pèse davantage que la simplicité, auquel cas garder Capistrano :
sous contrainte de temps, la cohérence vaut mieux que la nouveauté.

`vibe.ze.game` reste le bac à sable produit. L'hébergement mutualisé OVH du WordPress actuel
peut être résilié après la bascule, ce qui compense une partie du coût.

### Fournisseur recommandé : Hetzner, sur un compte propre à Point Zéro

Constat du 2026-08-01 : **`vibe.ze.game` tourne déjà chez Hetzner** (91.99.189.249,
Falkenstein, Allemagne) et **`pointzero2050.com` chez OVH en mutualisé** (164.132.235.17,
Gravelines). Le choix devient simple.

Reprendre **Hetzner** :

- l'équipe y opère déjà `vibe.ze.game` : la pile Caddy + PostgreSQL + Puma + Rails 8 y est
  éprouvée, rien de nouveau à apprendre sous contrainte de temps ;
- meilleur rapport prix/puissance d'Europe, et couple éprouvé avec Kamal ;
- Allemagne, donc Union européenne : la question RGPD ne se pose pas.

**Mais sur un compte Hetzner appartenant à Point Zéro**, distinct de celui de ze.game.
L'autonomie visée est aussi juridique et comptable : la facture, les accès et les sauvegardes
doivent appartenir à la structure qui exploite l'application. Même fournisseur, compte séparé.

Dimensionnement conseillé : un **CX32 ou CPX31** (4 vCPU, 8 Go, ~80 Go SSD), de l'ordre de 8 à
15 € par mois, largement suffisant pour le site, l'application et le pic du 1er octobre.
Activer l'option de sauvegarde automatique (+20 %, quelques euros) : c'est l'assurance la
moins chère du projet. Les 807 médias tiennent sur le disque, sans stockage objet.

Alternative si la juridiction française devait devenir un critère explicite — par exemple à la
demande d'un partenaire institutionnel : un VPS OVH à Gravelines ou Roubaix, où Boris possède
déjà un compte. Rapport prix/puissance inférieur, mais défendable. À ne retenir que si le
critère est posé ; sinon Hetzner.

## 7. Newsletter — recommandation

**Le fichier d'abonnés appartient à l'application ; l'envoi est délégué à un spécialiste.**

Tout construire en interne serait cohérent sur le papier, mais la délivrabilité e-mail est un
métier ingrat et permanent : SPF, DKIM, DMARC, réputation d'IP, gestion des rebonds, plaintes
pour spam, désinscription conforme. C'est plusieurs semaines de travail et une charge
d'exploitation définitive, pour un bénéfice nul du point de vue du joueur.

L'intégration recherchée par Boris ne vient pas de l'outil d'envoi : elle vient de la
**propriété du fichier**. Le schéma retenu est donc :

- l'application détient la table des abonnés et leur consentement — c'est la source de vérité,
  segmentable par Monde, progression, Cercle, événement ;
- un fournisseur d'envoi reçoit les contacts et gère campagnes, délivrabilité, rebonds et
  désinscriptions.

**Fournisseur recommandé : Brevo.** Société française, données en Union européenne (RGPD),
API correcte, et surtout il couvre à la fois les campagnes et les e-mails transactionnels —
or l'application en aura besoin de toute façon pour les billets, les confirmations
d'inscription et les comptes. Un seul fournisseur au lieu de deux.

Réserve budgétaire à connaître : le palier gratuit de Brevo plafonne à 300 envois par jour,
insuffisant pour un envoi unique à 634 contacts. Il faut prévoir un forfait d'entrée de gamme,
de l'ordre de quelques dizaines d'euros par mois.

Migration : export MailPoet en CSV avec listes et étiquettes (Newsletter Point Zéro 2050,
Webinaire Organisations, Formats PZ, Master class, Import 16/02/26), import dans
l'application **et** chez le fournisseur. Conserver les preuves de consentement — date
d'inscription et statut — et ne pas réimporter les 36 désabonnés ni les 23 adresses en rebond
dans les listes d'envoi.

## 7 bis. Étape 0 réalisée — export et assainissement du corpus (2026-08-01)

- **DNS** : Boris a la main sur toutes les zones, Point Zéro et ze.game. Plus de bloquant.
- **Export MailPoet** fourni par Boris : `Vibe Coding/migration/MailPoet_export.csv`, 633
  lignes. Colonnes : e-mail, prénom, nom, temps d'abonnement, temps de confirmation, état de
  la liste, état global, liste. Les preuves de consentement (dates d'abonnement et de
  confirmation, statut) sont présentes — condition nécessaire à une reprise conforme.
- **Corpus WordPress exporté et assaini** dans `Vibe Coding/migration/export-wp/` :
  105 pages + 33 articles = **138 fichiers HTML**, 2,7 Mo, plus un `manifest.csv`
  (type, id, slug, titre, URL, date de modification, taille, injections retirées, résiduel).
  Chaque fichier porte un en-tête de traçabilité en commentaire.
- **Assainissement vérifié** : **3 014 occurrences d'iframes injectées `div.show` retirées,
  0 résiduelle**. Les 8 iframes légitimes (YouTube) sont intactes — le filtre ne vise que les
  iframes dont la source contient `div.show`, il ne touche pas les autres embeds.
- Ampleur réelle de l'infection : **71 des 138 contenus étaient touchés**. Les plus atteints
  sont les pages vitrines — Chrysalides (186 injections), Ressourcerie (172), accueil (169),
  Explorateurs (167), Vaisseaux (161).
- Script d'export reproductible (PowerShell, API REST publique, aucune écriture côté
  WordPress) : à rejouer juste avant la bascule pour capturer les dernières modifications.

## 7 ter. ⚠️ Secrets déposés dans un dossier synchronisé

`Vibe Coding/migration/stripe.txt` contient une clé Stripe. Ce dossier est synchronisé par
Dropbox, ce que la consigne de sécurité du projet interdit explicitement (CLAUDE.md :
« jamais de mot de passe, clé privée ou token dans ce dossier ni dans les repos »). Le fichier
n'a pas été ouvert.

Recommandations :

- ne pas transmettre la clé par fichier : les clés vivent dans les identifiants chiffrés Rails
  (`config/credentials.yml.enc`) ou dans les variables d'environnement du serveur, saisies
  directement par Boris ;
- **supprimer `stripe.txt`** une fois la clé posée sur le serveur ;
- comme la clé actuelle provient d'une installation compromise, elle doit de toute façon être
  remplacée par une clé neuve puis révoquée (§5) — sa fuite éventuelle devient alors sans
  conséquence.

`MailPoet_export.csv` contient par ailleurs les données personnelles de 633 personnes. À
supprimer du dossier synchronisé après import, en conservant l'original côté MailPoet jusqu'à
l'extinction de WordPress.

## 7 quater. Infrastructure livrée — 2026-08-01

Serveur Point Zéro créé et provisionné, sur le compte Hetzner propre à Point Zéro.

| Élément | Valeur |
|---|---|
| Nom | `pointzero-app-01` (id 157902593) |
| Type | **cx33** — 4 vCPU x86, 8 Go RAM, 80 Go SSD |
| Localisation | Falkenstein (fsn1), Allemagne |
| Système | Ubuntu 26.04 LTS, noyau 7.0 |
| IPv4 | `167.233.210.57` |
| IPv6 | `2a01:4f8:c015:16f3::/64` |
| Sauvegardes | automatiques activées (+20 %) |
| Pare-feu | `pointzero-web` (id 11401908) — entrant 22/80/443 + ICMP uniquement |

**Coût réel : 10,69 € HT / mois** (serveur 8,49 + IPv4 0,50 + sauvegardes 1,70), soit
12,83 € TTC. *Note : le `cpx31` évoqué au §6 coûtait 17,49 € HT pour les mêmes 4 vCPU et 8 Go —
le `cx33` est deux fois moins cher à performance égale, avec 80 Go de disque au lieu de 160.*

Configuration appliquée :

- fuseau horaire Europe/Paris, système entièrement à jour, redémarrage effectué ;
- utilisateur **`deploy`** (sudo sans mot de passe, membre du groupe `docker`) ;
- authentification SSH **par clé uniquement** — mot de passe désactivé, `root` en
  `prohibit-password` ;
- `unattended-upgrades` actif pour les correctifs de sécurité ;
- `fail2ban` actif ;
- **Docker 29.1.3** installé et utilisable par `deploy`, en vue d'un déploiement **Kamal**
  (défaut Rails 8 ; ni Ruby ni Caddy à installer sur l'hôte, `kamal-proxy` gère le TLS).

### Accès

- Clé privée : `~/.ssh/id_ed25519_pointzero` sur le poste de Boris — **hors Dropbox**,
  distincte de la clé ze.game. À sauvegarder par un canal sûr, jamais dans un dépôt.
- Connexion : `ssh -i ~/.ssh/id_ed25519_pointzero deploy@167.233.210.57`
- Clé publique enregistrée dans le projet Hetzner sous le nom `pointzero-app`
  (empreinte `6a:c3:ea:89:20:7c:f4:60:3f:86:ca:69:27:9a:aa:e2`).

### Jeton API

Un jeton Hetzner Read & Write est utilisé par les scripts d'exploitation, lu depuis un fichier
local hors Dropbox et jamais affiché. **À révoquer dans la console à la fin du chantier**
(Security → API tokens), ou à conserver si l'on veut garder l'exploitation scriptable.

## 7 quinquies. Application Rails livrée — 2026-08-01

Le squelette de l'application autonome tourne en production sur `pointzero-app-01`.

| Élément | Valeur |
|---|---|
| Chemin | `/home/deploy/src/pointzero-app` (dépôt git local, commit `0bac7af`) |
| Rails / Ruby | **8.1.3.1 / 4.0.6** |
| Base | PostgreSQL 17 en conteneur ; 4 bases créées (`pointzero_production` + `_cache`, `_queue`, `_cable`) |
| Options | `--database=postgresql --css=sass --javascript=importmap` |
| Jobs / cache | Solid Queue, Solid Cache, Solid Cable |
| Déploiement | `/home/deploy/deploy` : `compose.yml` + `caddy/Caddyfile` + `.env` (droits 600) |
| Santé | `/up` répond 200 depuis le proxy |

### Révision d'une décision : Compose plutôt que Kamal

J'avais recommandé Kamal (défaut Rails 8). À la mise en œuvre, deux contraintes non anticipées
sont apparues : **aucun Ruby ni Docker sur le poste de Boris** — tout se fait donc sur le
serveur — et Kamal exige un **registre d'images authentifié** plus une clé SSH du serveur vers
lui-même. Cela ajoutait un registre privé, un htpasswd et une seconde paire de clés, pour
aucun bénéfice sur une machine unique où l'on développe aussi.

Retenu : **Docker Compose + Caddy**. Le `Dockerfile` de production généré par Rails est
inchangé, Caddy obtient et renouvelle les certificats Let's Encrypt tout seul, et le
déploiement se résume à `docker compose build web && docker compose up -d`. On perd le
déploiement sans coupure et le retour arrière en une commande ; c'est acceptable avant
l'ouverture, et la bascule vers Kamal restera possible le jour où il y aura une intégration
continue et un registre.

### Deux corrections rencontrées, à connaître pour la suite

1. **`DATABASE_URL` ne suffit pas en Rails 8.** Il ne s'applique qu'à la connexion primaire ;
   `cache`, `queue` et `cable` retombaient sur une socket Unix locale et faisaient échouer
   `db:prepare`. `config/database.yml` déclare désormais les quatre bases explicitement, à
   partir de `DB_HOST`, `POSTGRES_USER`, `POSTGRES_PASSWORD` et `POSTGRES_DB`.
2. **Les valeurs par défaut de `ENV.fetch` sont obligatoires** : `assets:precompile` s'exécute
   pendant la construction de l'image, sans les variables d'environnement de production. Un
   `ENV.fetch("POSTGRES_USER")` sans repli casse le build.

### Reste bloqué : le DNS

`new.pointzero2050.com` renvoie **NXDOMAIN** depuis les serveurs faisant autorité d'OVH
(`ns20.ovh.net`) comme depuis les résolveurs publics. Let's Encrypt échoue donc à valider le
domaine et Caddy réessaie toutes les deux minutes. **Aucune action ne sera nécessaire côté
serveur** : dès que l'enregistrement sera visible, le certificat sera émis automatiquement.
À vérifier dans la zone OVH du domaine (l'enregistrement A `new` → `167.233.210.57`).

### Question ouverte : le dépôt distant

Le code est versionné localement sur le serveur mais n'a pas encore de dépôt distant. Deux
options : une branche `festival-standalone` dans `zegame-app` comme le prévoyait le cadrage
Festival, ou un **nouveau dépôt `PointZero2050/pointzero-app`**. Recommandation : le nouveau
dépôt, car il ne s'agit pas d'une extraction de l'application ze.game mais d'une base neuve
dans laquelle la logique Point Zéro sera portée ensuite. À trancher par Boris.

## 8. Questions bloquantes

Il n'en reste qu'une, mais elle conditionne la bascule finale :

1. **Qui a la main sur le DNS de `pointzero2050.com`** — chez quel registrar, et qui détient
   les accès à la zone ? Sans cela, tout le reste peut être prêt sans pouvoir basculer.

Deux éléments à fournir dès que possible, non bloquants pour démarrer :

2. Accès au tableau de bord Stripe (pour générer les clés neuves) — par Boris lui-même,
   jamais transmis en clair dans ce dossier ni dans les dépôts.
3. Choix du fournisseur d'hébergement, si différent de celui de `vibe.ze.game`.
