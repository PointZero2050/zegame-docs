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

## 6. Questions bloquantes

1. **Où le nouveau site tourne-t-il ?** Seconde application Rails sur le serveur
   `vibe.ze.game` derrière Caddy, ou hébergement neuf dédié à Point Zéro ? Et qui a la main
   sur le DNS de `pointzero2050.com` (registrar, zone) ?
2. **La billetterie bascule-t-elle bien maintenant**, contre la recommandation de
   `application-festival-2026.md` §5 ? Si oui, ce document doit être amendé pour rester
   canonique.
3. **Vers quoi part la newsletter ?** Table interne + fournisseur d'envoi (Brevo, Mailjet…),
   ou plateforme externe qui reprend les 634 contacts ? Cela conditionne la forme de l'export.
