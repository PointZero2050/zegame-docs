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

`vibe.ze.game` reste le bac à sable produit. L'hébergement WordPress actuel (Liquid Web /
Nexcess) peut être résilié après la bascule, ce qui compense une partie du coût.

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

## 8. Questions bloquantes

Il n'en reste qu'une, mais elle conditionne la bascule finale :

1. **Qui a la main sur le DNS de `pointzero2050.com`** — chez quel registrar, et qui détient
   les accès à la zone ? Sans cela, tout le reste peut être prêt sans pouvoir basculer.

Deux éléments à fournir dès que possible, non bloquants pour démarrer :

2. Accès au tableau de bord Stripe (pour générer les clés neuves) — par Boris lui-même,
   jamais transmis en clair dans ce dossier ni dans les dépôts.
3. Choix du fournisseur d'hébergement, si différent de celui de `vibe.ze.game`.
