# Refonte du site pointzero2050.com — audit initial et cadrage

> Rédigé par Claude le 2026-07-31. Premier audit du site WordPress public en vue de sa refonte
> intégrée à l'application Point Zéro (contenu géré par LLM, tunnel d'engagement contrôlé depuis
> l'appli, sortie de WordPress).

## 1. Intention de Boris

- Le site https://pointzero2050.com/ (WordPress) doit être refondu pour être pleinement intégré à
  l'application Point Zéro.
- Cible : un site géré par un LLM, dont le tunnel d'engagement (découverte → Sas → Atelier →
  entrée dans le Jeu) est contrôlé depuis l'appli PZ et ne passe plus par WordPress.
- L'occasion est saisie pour améliorer design et UX, en accord avec la direction de l'appli
  (registre incarné, progression par expériences, cartes-couvertures, vidéo-first).
- Décision Boris (2026-07-31) : les 2 billets du Festival déjà « vendus » sont des tests ; la
  vente effective ne commence que **fin août 2026**. Il existe donc une fenêtre pour migrer la
  billetterie AVANT l'ouverture des ventes, si on choisit une migration complète.

## 2. État des lieux technique (audit public, 2026-07-31)

Hébergement : **OVH, hébergement mutualisé** (`cluster023.hosting.ovh.net`, IP 164.132.235.17,
Gravelines/Dunkerque). *Correction du 2026-08-01 : l'audit initial concluait à Liquid Web /
Nexcess d'après le namespace REST `liquidweb/harbor`, qui provient en réalité d'un plugin et
non de l'hébergeur.* Le caractère mutualisé de l'hébergement est un élément de contexte pour
la compromission constatée.

| Composant | Outil | Remarque |
|---|---|---|
| Thème | Pro (Themeco) | Builder propriétaire |
| Builders | WPBakery (`js_composer`) + Slider Revolution 6.7.37 | Trois couches de builder au total |
| Événements | The Events Calendar Pro + Event Tickets / Event Tickets Plus | Cœur du workflow |
| Paiement | WooCommerce + passerelle Stripe (+ reviews, ajax filters, load more) | Billetterie Festival |
| Newsletter | MailPoet (formulaire `admin-post.php?action=mailpoet_subscription_form`) | Abonnés stockés dans la base WP |
| Contact | WPForms (page `/contact/`) | Page orpheline : liée nulle part dans le menu |
| Anti-spam / sécurité | CleanTalk, Wordfence | |
| RGPD | Complianz | |
| Divers | GamiPress, Code Snippets, Content Views, Widget Logic, vc-extensions-bundle, WooCustomizer | GamiPress recouvre la gamification de l'appli |

Constats techniques :

- **API REST événements publique et fonctionnelle** : `/wp-json/tribe/events/v1/events` renvoie
  les événements complets (titre, description, lieu, billets). L'appli Rails peut lire le
  calendrier sans modification côté WP — utile pour une phase transitoire.
- L'énumération des utilisateurs REST est bloquée (401) — bon point.
- **Adresse WordPress configurée en `http://`** (champ `url` de `/wp-json/`) alors que le site
  sert en https → redirections et risques de contenu mixte.
- Performance accueil : ~244 requêtes, 51 assets `wp-content`, DOMContentLoaded ≈ 3,7 s avec
  cache. Conséquence directe de l'empilement thème Pro + WPBakery + Slider Revolution.

### ⚠️ Site compromis : injection d'iframes cachées `div.show`

Découvert pendant l'audit admin (2026-07-31) : des **iframes invisibles** (1 px,
`visibility: hidden`) pointant vers `https://div.show/public` sont injectées **dans le contenu
même des pages** (au cœur du HTML WPBakery, y compris à l'intérieur de balises `<h2>`). Étendue
mesurée : **169 occurrences sur l'accueil**, 136 sur `/ecosysteme-introduction/`, 73 sur
`/ressourcerie-les-articles/`, 45 sur `/formats-ateliers-2/`, 1 sur `/contact/` (0 sur
`/comprendre-presentation/`). C'est un motif classique de compromission WordPress (injection en
base dans `post_content`). Conséquences : réputation SEO, risque pour les visiteurs, et surtout
**tout export de contenu vers la nouvelle pile devra être assaini** (filtrer ces iframes lors de
la migration). Actions immédiates recommandées : scan Wordfence complet, vérification des
sauvegardes UpdraftPlus, changement des mots de passe admin (aucun des 6 comptes n'a la 2FA),
signalement à l'hébergeur Liquid Web/Nexcess. La compromission renforce l'argument d'une
migration complète plutôt qu'un maintien prolongé de WordPress.

## 3. État des lieux fonctionnel

### Événements (workflow critique)

- Ateliers Point Zéro présentiels Paris (3 h, gratuits, RSVP, ~15 places), Sas d'exploration
  (1 h 30, gratuits, RSVP), récurrents mensuels.
- **New Civilization Festival, 1er octobre 2026** : billets 250 € via Event Tickets Plus +
  WooCommerce/Stripe ; 2 ventes de test uniquement ; vente réelle à partir de fin août.

### Newsletter

- MailPoet, formulaire dédié `/formulaire-newsletter/` (prénom, nom, e-mail). Liste exportable
  en CSV depuis l'admin. L'envoi dépend de WP tant que la liste n'est pas migrée.

### Contact

- WPForms sur `/contact/` (nom, prénom, e-mail, message), page non référencée dans la
  navigation. Footer réduit à la politique de confidentialité : aucun mailto ni réseau social.

### Contenu

- ~40 pages statiques réparties en 5 rubriques (Comprendre ×6, Écosystème ×8, Ressourcerie ×8,
  Formats ×7, Newsletter), plus une série d'articles de fond « Semaine n/52 » (~10 publiés
  visibles) et d'autres articles conceptuels.
- Trois parcours mis en avant : Explorateur, Chrysalide, Vaisseau (cohérents avec l'écosystème
  documenté dans zegame-docs).

## 4. Constats design / UX

- Accueil : « Événements à la une » en premier écran mais slider vide au chargement ; longs
  paragraphes conceptuels dès l'accueil ; ton encyclopédique.
- Navigation : ~40 entrées de menu, arborescence profonde — une encyclopédie, pas un tunnel
  d'engagement. Aucun parcours guidé « je découvre → je m'inscris à un Sas → j'entre dans le
  Jeu ».
- Langue incohérente : titre du site en anglais (« Give birth to the civilization of
  tomorrow »), slugs anglais (`/events/`), dates mal localisées (« septembre 16, 2025 –
  janvier 16 »), « Read More » au milieu de textes français.
- Esthétique sans lien avec la direction artistique de l'appli (collage néoarchaïque, atlas,
  cartes-couvertures, Moteur lumineux).

## 5. Stratégie de refonte proposée

Trois natures de contenu, trois traitements :

1. **Contenu statique** (pages + articles) : gestion par LLM dans l'appli — pages servies par
   Rails, contenu en fichiers versionnés (même logique que `config/puissances/*.yml` et
   `config/ressources/*.yml`), design aligné sur l'appli.
2. **Événements + inscriptions** : modèles Rails (Event / Registration), RSVP internes, Stripe
   Checkout pour le payant. Bénéfice direct : l'inscription à un format valide automatiquement
   l'expérience « Découvrir les formats » du Monde 0 par simple écriture interne, sans le
   callback signé WordPress envisagé dans l'audit de finalisation du Monde 0
   (https://github.com/PointZero2050/zegame-docs/blob/main/docs/pedagogie/monde-0-audit-finalisation-validations.md).
3. **Newsletter + contact** : export CSV MailPoet puis bascule vers un outil rattaché à l'appli
   (table interne + ESP type Brevo, ou équivalent) ; formulaire de contact natif Rails.

### Séquencement (fenêtre favorable)

La vente réelle des billets du Festival ne commençant que fin août, deux options :

- **Option A — migration complète avant fin août** : la billetterie du Festival ouvre
  directement dans la nouvelle pile (Rails + Stripe). Aucune migration de ventes réelles à
  faire ; les 2 commandes de test sont ignorées. Exigence : le tunnel de vente doit être
  fiabilisé avant l'ouverture des ventes, en parallèle du chantier appli festival (gel
  fonctionnel appli : 15 septembre, cf.
  https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/application-festival-2026.md).
- **Option B — transition douce** : le contenu statique et les nouveaux formats basculent
  d'abord (l'appli lit les événements via l'API REST `tribe/events/v1` pendant la transition),
  WP reste la caisse jusqu'après le festival, puis extinction et redirections.

L'option A est rendue possible par la décision de Boris ; elle évite de maintenir deux systèmes
pendant la période la plus chargée. À arbitrer en fonction de la charge (le chantier appli
festival reste prioritaire).

### Données à migrer (quel que soit le scénario)

- Abonnés MailPoet (export CSV).
- Contenu éditorial : ~40 pages, articles de fond (série 52 semaines), bibliographie,
  cartographies, scénarios.
- Événements récurrents (Ateliers, Sas) et leurs gabarits de description.
- Redirections 301 de toutes les URLs indexées vers la nouvelle arborescence.

## 6. Points de vigilance

- Ne rien casser du tunnel actuel tant que la nouvelle pile n'est pas en production (les Sas et
  Ateliers mensuels continuent de prendre des inscriptions).
- RGPD : conserver les preuves de consentement lors de la migration des abonnés MailPoet ;
  reproduire l'équivalent de Complianz (bannière, registre) côté Rails.
- SEO : inventaire des URLs indexées avant migration, plan de redirections 301.
- Sécurité : les accès (WP, SQL) doivent vivre dans le gestionnaire de mots de passe de Boris,
  pas dans des fichiers synchronisés Dropbox.

## 7. Audit admin (réalisé le 2026-07-31, session Boris, lecture seule)

### Plugins

36 extensions actives (38 installées ; Polylang et WP Mail SMTP inactives), toutes à jour.
Principales : ACF 6.8.6, WPBakery 8.6.1 + All In One Addons + Templatera, Slider Revolution
6.7.37, The Events Calendar 6.17.1 + Pro 7.7.14, Event Tickets 5.29.1 + Plus 6.9.3 (+ extension
Additional Fields), WooCommerce 10.9.4 + Stripe Gateway 10.8.4 + Catalog Mode + StoreCustomizer,
MailPoet 5.34.3 + **MailPoet Premium 5.30.0 (obsolète : fonctionnalités premium désactivées
par MailPoet, avertissement affiché dans l'admin)**, WPForms 2.0.0.2, GamiPress 7.9.9.2,
Wordfence 8.2.2, CleanTalk 6.84 (**période d'essai en fin de vie, relance de paiement**),
Complianz 7.5.1, UpdraftPlus 1.26.6 (sauvegardes), WP Statistics, Code Snippets, Duplicate
Page, Enable Media Replace, Regenerate/Force Regenerate Thumbnails, Favicon RealFaviconGenerator,
Simple Custom CSS, Widget Logic, Content Views, Dossiers.

### Newsletter (MailPoet)

- **634 contacts** : 569 abonné·es actifs, 6 non confirmés, 36 désabonnés, 23 retournés
  (bounces). Quota du plan : 575/1500.
- Listes : « Newsletter Point Zéro 2050 » (633), Test (1), Utilisateurs WordPress (6), 35
  contacts sans liste.
- Étiquettes : Webinaire Organisations (103), Formats PZ (61), Import 16/02/26 (47),
  Master class (14) — à préserver lors de la migration (segmentation).

### Commandes et Stripe

- **1 seule commande WooCommerce** (#4454, Boris, 11 juillet 2026, statut « En cours ») —
  cohérent avec « les billets vendus sont des tests ». Historique à ignorer lors de la
  migration.
- **La passerelle Stripe est en mode LIVE** (mode test décoché). Les clés live sont donc déjà
  configurées ; un « test » de billet payant passe par une vraie transaction. Pour la nouvelle
  pile : réutiliser le même compte Stripe, et faire les tests en mode test.

### Comptes WordPress

6 comptes : 5 administrateurs (admin9878, Boris Sirbey, Fred Angelot, matdaval, philmalbrunot)
+ 1 « Events Administrator » (Sara). **Aucun compte n'a la 2FA active.** À corréler avec la
compromission (§2) : rotation des mots de passe recommandée.

### Volumes de contenu

- 105 pages publiées, 33 articles publiés, 9 événements, 37 produits WooCommerce,
  807 médias.
- Le périmètre éditorial réel à migrer est donc plus large que les ~40 pages du menu :
  inventaire page par page nécessaire (beaucoup de pages hors navigation, comme `/contact/`).

## 8. Prochaines étapes proposées

1. **Traiter la compromission** (§2) : scan Wordfence, nettoyage ou décision d'accélérer la
   migration ; rotation des mots de passe ; 2FA sur les comptes restants.
2. Arbitrer option A (migration complète avant fin août) vs option B (transition douce).
3. Export MailPoet (CSV, avec listes et étiquettes) et inventaire éditorial complet
   (105 pages + 33 articles) avec assainissement des iframes injectées.
4. Concevoir l'architecture cible côté appli (modèles Event/Registration, pages statiques
   versionnées, formulaire contact, newsletter) — en cohérence avec le chantier appli festival.
