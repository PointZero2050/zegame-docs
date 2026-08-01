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

## 7 sexies. Import du corpus réalisé — 2026-08-01

Les 138 contenus et l'intégralité des médias sont dans l'application.

### Contenus

- **105 pages + 33 articles** importés dans `content/legacy/`, versionnés avec l'application
  (3 Mo). Commit `8731edf`.
- Traitements appliqués à l'import, en plus de l'assainissement des iframes injectées :
  **71 balises `<script>` retirées** (elles pointaient vers des ressources WordPress
  condamnées), **14 formulaires WordPress retirés** et remplacés par un commentaire
  `<!-- FORMULAIRE WORDPRESS RETIRE - a reconstruire en natif -->` — ces 14 pages sont la
  liste de travail des formulaires à refaire —, et réécriture de toutes les URL absolues
  `pointzero2050.com` en chemins relatifs.
- **Les contenus sont servis à leur URL d'origine** (`/comprendre-question-1`,
  `/les-cadres-systemiques`…). C'est le point important pour le référencement : **la majorité
  du corpus n'a besoin d'aucune redirection 301**. Le plan de redirections ne portera que sur
  les pages supprimées ou renommées.
- Mise en œuvre : modèle `LegacyPage` (lecture du manifeste JSON, sans base de données),
  `LegacyPagesController`, et une route attrape-tout `get "/:slug"` sous contrainte — la
  contrainte vérifie l'existence du slug dans le manifeste, ce qui empêche cette route de
  masquer les futures routes de l'application. Un slug inconnu renvoie bien 404.
- Un sommaire provisoire est servi en racine, le temps de la reprise éditoriale.

### Médias

- **2 106 fichiers rapatriés, 315 Mo, aucun échec.** Ils correspondent aux 807 médias
  WordPress et à leurs variantes de taille.
- Ils vivent dans `/home/deploy/media` sur le serveur, **hors du dépôt et hors du contexte de
  construction Docker** (315 Mo auraient été renvoyés au démon Docker à chaque build et
  gonflé l'image), montés en lecture seule sur `/rails/public/media`. Exclus par `.gitignore`
  et `.dockerignore`. Commit `ca429e1`.
- Leur sauvegarde est assurée par les instantanés Hetzner. À terme, un stockage objet serait
  plus propre si le volume croît.

### Pièges rencontrés

- Les fichiers produits par PowerShell portent un **BOM UTF-8** que `JSON.parse` refuse. Le
  modèle lit désormais avec `read(encoding: "bom|utf-8")`, qui absorbe le BOM proprement.
- Le corpus contient encore le balisage WPBakery (`vc_row`, `wpb_wrapper`). Sans la feuille de
  style du thème, les pages s'affichent sans mise en forme mais restent lisibles et complètes.
  C'est assumé : la reprise éditoriale et graphique se fera page par page.

### Reste à faire sur ce volet

- Créer le dépôt distant et y pousser (voir ci-dessous).
- Reconstruire les 14 formulaires en natif.
- Reprendre la mise en forme, ensemble par ensemble.

## 7 septies. Site en ligne — 2026-08-01

**https://new.pointzero2050.com** est servi en HTTPS, certificat Let's Encrypt obtenu.

- **DNS résolu.** L'enregistrement avait été saisi comme `new.pointzero2050.com` dans le champ
  « sous-domaine » d'OVH, qui y ajoute la zone : le nom réellement publié était
  `new.pointzero2050.com.pointzero2050.com`. Corrigé en saisissant `new` seul. À retenir pour
  la bascule du domaine principal.
- **Dépôt distant** : https://github.com/PointZero2050/pointzero-app (privé, organisation
  PointZero2050). Le serveur pousse via une **clé de déploiement dédiée** en lecture/écriture
  (`~/.ssh/id_ed25519_github` sur le serveur, empreinte
  `SHA256:bU+nwnSo210nEJI6Wd3Y6Ug59HIJD8ddSuNVBaSW2Ts`). Aucun identifiant GitHub personnel
  n'est stocké sur le serveur.

### Corrections apportées après première vérification en ligne

1. **URL en protocole relatif.** Le filtre de réécriture ne couvrait que `https?://` et
   laissait passer les `//pointzero2050.com/…`, qui auraient cassé à l'extinction de
   WordPress. Corrigé : **82 médias supplémentaires** ont été découverts et rapatriés, soit
   **2 188 fichiers, 344 Mo**. Il ne reste que 7 références au domaine, toutes dans
   `test-658`, une page de test destinée à la suppression.
2. **Entités HTML des titres.** `CGI.unescapeHTML` ne décode que les entités XML de base :
   les titres contenant `&rsquo;` s'affichaient tels quels. Décodage confié à Nokogiri.

### Limite connue : Slider Revolution

Les images des sliders **ne survivent pas à l'export REST**. Leur balisage ne contient que des
placeholders (`dummy.png` en `src` comme en `data-lazyload`) ; les visuels réels vivent dans
les tables du plugin et sont injectés par son JavaScript, que nous avons retiré. Sur une page
comme `/comprendre-question-1`, cela représente 28 images fantômes, à côté de 11 images de
contenu qui, elles, s'affichent correctement.

Conséquence : si un visuel de slider a une valeur éditoriale, il faudra le récupérer dans la
base WordPress ou le recréer. La reprise éditoriale prévoyant de toute façon de nouveaux
visuels issus du corpus Point Zéro (fiches pédagogiques, atlas), l'impact est limité — mais la
décision doit être prise **avant l'extinction de WordPress**, après quoi ces visuels seront
perdus.

## 7 octies. Lettre d'information et billetterie — 2026-08-01

Commit `8fccd01`. Les deux domaines sont construits et testés ; il ne manque que les clés.

### Lettre d'information

- Table `Subscriber` **possédée par l'application** : source de vérité, segmentable par
  étiquettes. Brevo n'est qu'un tuyau d'envoi.
- **Double opt-in** : tant que la personne n'a pas cliqué, elle n'est pas contactable. Un
  réabonnement après désinscription repasse par la confirmation.
- **Désinscription en un clic, sans authentification** — obligation légale, et cela ne doit
  jamais demander d'effort.
- `BrevoClient` **inerte tant que `BREVO_API_KEY` est absente** : l'inscription fonctionne
  quand même, la synchronisation est rejouée par `SynchroniseSubscriberJob` (Solid Queue,
  5 tentatives espacées).
- **633 abonnés MailPoet importés** : 568 confirmés, 36 désabonnés, 23 en rebond, 6 en
  attente. Les statuts de refus sont conservés — sans quoi un réimport rendrait ces personnes
  à nouveau contactables. Les dates d'abonnement et de confirmation sont reprises comme
  preuves de consentement. La tâche `mailpoet:import` est idempotente.

### Billetterie

- `Event` et `Registration`. Gratuit : inscription confirmée immédiatement. Payant :
  **Stripe Checkout**, aucune donnée de carte ne transite par l'application, qui reste donc
  hors périmètre PCI.
- **La confirmation vient exclusivement du webhook signé**, jamais de la redirection du
  navigateur — celle-ci n'est pas une preuve de paiement et peut ne jamais être atteinte.
  Le webhook est idempotent : Stripe rejoue ses événements.
- Référence de billet unique et non devinable (`PZ-XXXXXXXX`), conformément au principe du
  cadrage Festival : c'est le billet, et non l'adresse e-mail, qui fait foi.
- Capacité, complet, clôture des inscriptions et cases à cocher newsletter gérés et testés.

### Piège rencontré, à retenir

**Ne jamais nommer une colonne `format`** : elle masque `Kernel#format` et fait échouer tout
appel de formatage dans le modèle avec un `ArgumentError` obscur. La colonne a été renommée
`categorie`.

### Il ne manque que les clés

À fournir par Boris, jamais dans un dossier synchronisé ni dans un dépôt — elles se posent
dans `/home/deploy/deploy/.env` (droits 600) :

| Variable | Où l'obtenir |
|---|---|
| `BREVO_API_KEY` | Brevo → SMTP & API → clés API |
| `BREVO_LIST_ID` | identifiant de la liste « Newsletter Point Zéro 2050 » à recréer dans Brevo |
| `SMTP_*` | Brevo → SMTP & API → identifiants SMTP (pour ActionMailer) |
| `STRIPE_SECRET_KEY` | **clé neuve**, l'actuelle vient d'une installation compromise |
| `STRIPE_WEBHOOK_SECRET` | créé en déclarant le webhook vers `/webhooks/stripe` |

Reste également à configurer ActionMailer en production (relais SMTP Brevo) et à déclarer le
point d'entrée du webhook côté Stripe.

## 7 nonies. Brevo et Stripe branchés et vérifiés — 2026-08-01

### Brevo

- Compte : Point Zero 2050 (`boris@sirbey.com`). Relais SMTP `smtp-relay.brevo.com:587`,
  identifiant `b40bf6001@smtp-brevo.com`.
- Liste **« Newsletter Point Zero 2050 », identifiant 3**, créée par l'API.
- Vérifié : authentification SMTP réussie **sans envoi de courriel** (session ouverte puis
  fermée) ; synchronisation d'un contact de test vers la liste réussie, contact supprimé
  ensuite des deux côtés.
- Attention : Brevo distingue la **clé SMTP** (`xsmtpsib-`, mot de passe du relais) et la
  **clé API** (`xkeysib-`, pour les contacts). Les deux sont nécessaires et ne sont pas
  interchangeables.

### Stripe

- Compte Point Zero 2050, **mode test**. Webhook créé et actif vers
  `https://new.pointzero2050.com/webhooks/stripe`, sur `checkout.session.completed` et
  `checkout.session.expired`. *(Nom généré par Stripe : « charming-triumph » — à renommer.)*
- Chaîne complète vérifiée sans saisir aucun numéro de carte, en signant un événement avec le
  vrai secret de webhook :

| Étape | Résultat |
|---|---|
| Création de l'inscription | `en_attente` |
| Session Checkout réelle (25 000 c. EUR) | créée, statut `en_attente_paiement` |
| Webhook signé `checkout.session.completed` | HTTP 200, inscription **confirmée**, `payment_intent` enregistré |
| **Rejeu** du même événement | HTTP 200, `confirmee_le` **inchangé** — idempotence vérifiée |
| **Signature invalide** | **HTTP 400**, rejeté |

### Piège Docker Compose

Les variables d'un fichier `.env` ne sont lues que pour la **substitution dans compose.yml** ;
elles ne descendent pas dans le conteneur. Il faut déclarer `env_file:` sur le service, faute
de quoi la configuration reste invisible côté application — sans aucun message d'erreur.

### Domaine authentifié et envoi vérifié — 2026-08-01

`pointzero2050.com` est **authentifié et vérifié** chez Brevo. Un courriel réel a été
**délivré** depuis `bonjour@pointzero2050.com`, en passant par le vrai code de production
(`SubscriptionMailer`).

Enregistrements en place dans la zone OVH : `brevo-code` à l'apex, les deux CNAME DKIM
`brevo1._domainkey` et `brevo2._domainkey`, le CNAME du sous-domaine de marque
`em → em-pointzero2050-com.brand.brevosend.com`, et un DMARC unique avec `rua`.

**Le SPF n'a pas eu à être modifié** et reste `v=spf1 include:mx.ovh.com -all` : avec le
sous-domaine de marque, c'est `em` qui porte le chemin de retour et son propre SPF,
l'alignement DMARC se faisant par le DKIM. Le risque d'écrasement redouté ne s'est pas
matérialisé.

Choix du sous-domaine : **`em`**, et surtout pas `mail` que Brevo suggérait — `mail` est déjà
un CNAME vers `ssl0.ovh.net` qui sert les boîtes aux lettres, l'écraser aurait coupé la
réception.

#### Deux pannes silencieuses rencontrées, à connaître

1. **Deux enregistrements DMARC** coexistaient. La norme prévoit que plusieurs enregistrements
   DMARC équivalent à **aucun** : les destinataires ignorent la politique, et Brevo refusait
   d'authentifier avec un message générique. Un seul doit subsister.
2. **`ApplicationMailer` généré par Rails contient `default from: "from@example.com"` en
   dur**, valeur qui **prime sur `config.action_mailer.default_options`**. Rails signalait un
   envoi réussi et Brevo rejetait le message (« sender not valid »). Seule la consultation du
   journal d'envoi Brevo l'a révélé — la vérification côté application était trompeuse.

*Leçon générale : pour l'e-mail, un succès côté application ne prouve rien. La seule preuve
est l'événement `delivered` chez le fournisseur.*

### Reste à faire sur ce volet

- Les anciens enregistrements MailPoet (`mailpoet1._domainkey`, `mailpoet2._domainkey`) seront
  à retirer **après** l'extinction de WordPress, pas avant.
- Confirmer l'adresse d'expédition, réglée sur `bonjour@pointzero2050.com`.
- ~~Synchroniser les 568 abonnés confirmés vers la liste Brevo.~~ **Fait le 2026-08-01** :
  568 contacts poussés, **0 échec**, 209 s. Contrôle croisé concordant — 568 en base marqués
  synchronisés, 568 dans la liste Brevo, 0 en liste noire. Les **59 refus** (36 désabonnés,
  23 rebonds) et les 6 non confirmés n'ont pas été poussés : ils restent en base comme
  mémoire du refus, sans jamais être contactables.
- Décision Boris (2026-08-01) : **les visuels Slider Revolution sont abandonnés**, il en a des
  copies. Plus rien ne retient l'extinction de WordPress de ce côté.
- Au passage en production : remplacer la clé standard par une **clé Stripe limitée**
  (écriture sur les sessions Checkout, lecture sur les paiements) — si elle fuite, elle ne
  permet ni remboursement ni virement.
- Supprimer `C:\Temp\brevo.txt`, qui contient encore les clés Brevo en clair.

## 8. Questions bloquantes

Il n'en reste qu'une, mais elle conditionne la bascule finale :

1. **Qui a la main sur le DNS de `pointzero2050.com`** — chez quel registrar, et qui détient
   les accès à la zone ? Sans cela, tout le reste peut être prêt sans pouvoir basculer.

Deux éléments à fournir dès que possible, non bloquants pour démarrer :

2. Accès au tableau de bord Stripe (pour générer les clés neuves) — par Boris lui-même,
   jamais transmis en clair dans ce dossier ni dans les dépôts.
3. Choix du fournisseur d'hébergement, si différent de celui de `vibe.ze.game`.
