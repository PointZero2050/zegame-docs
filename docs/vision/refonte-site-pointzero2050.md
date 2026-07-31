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

Hébergement : Liquid Web / Nexcess (namespace REST `liquidweb/harbor`).

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
- La page newsletter charge 4 iframes `https://div.show/public` — service à identifier dans
  l'admin (probablement un embed vidéo), à supprimer ou internaliser lors de la refonte.

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

## 7. À compléter (audit admin en attente)

L'audit de l'admin WP reste à faire (session authentifiée nécessaire) :

- liste exacte des plugins actifs et versions, licences ;
- volume d'abonnés MailPoet et listes ;
- historique des commandes WooCommerce et réglages Stripe (mode test/live) ;
- utilisateurs WP existants ;
- identification des iframes `div.show` ;
- inventaire complet des pages/articles publiés (y compris brouillons).
