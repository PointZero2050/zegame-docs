# Analyse fonctionnelle — impacts back/front

<!-- Ajout Claude, 2026-07-12, sur demande de Boris (retours wireframe accueil v1) -->

Ce document est le registre d'analyse d'impact : chaque nouvelle page ou fonctionnalité front y est modélisée avec ses impacts sur le backoffice, les modèles de données et la cohérence d'ensemble. **Règle de travail : aucune page ne passe en implémentation sans sa ligne d'analyse ici.** Claude et Codex le tiennent à jour ; les arbitrages restent à Boris.

Contexte : ces impacts visent la **future application dédiée Point Zéro** (décision du 2026-07-12, cf. [accueil-point-zero.md](accueil-point-zero.md) §13). La question de ce qui est partagé avec ze.game (modèles, gems, base, comptes) reste ouverte.

## 1. Registre des impacts identifiés

### F1 — Module News

**Origine front** : bloc "À la une" sur l'accueil (état nouveau joueur, extensible aux autres états).

| Aspect | Impact |
|---|---|
| Modèle | Nouvelle entité `News` : titre, corps, lien, image, dates de publication/expiration, flag `featured` |
| Backoffice | CRUD News + choix de la featured news (une seule à la fois ?) |
| Front | Bloc "À la une" (featured) ; à décider : liste des news non-featured (où ?) |
| Questions | Une news par communauté/monde ou globale ? Qui peut publier ? |

### F2 — Mode de progression d'un parcours (libre / linéaire)

**Origine front** : Monde 0 linéaire (une Action accomplie ouvre la suivante) ; parcours actuels libres.

| Aspect | Impact |
|---|---|
| Modèle | Champ `progression_mode` sur Journey : `libre` (défaut, comportement actuel) / `linéaire` |
| Backoffice | Option dans la page de gestion d'un parcours |
| Front | Mode linéaire : Actions verrouillées 🔒 après l'Action courante ; vue "parcours entier" avec états fait/en cours/verrouillé |
| Logique | Le déverrouillage suit l'ordre `challenges_journeys.position` ; définir l'interaction avec `auto_validated` (validation pédagogique bloque-t-elle la suite ?) |
| Lien vision | Modes envisagés dans [accueil-point-zero.md](accueil-point-zero.md) §7 (séquentiel/libre/guidé/conditionnel/temporel) — commencer par libre/linéaire |

### F3 — Parcours obligatoire (tutoriel de Monde)

**Origine front** : chaque Monde s'ouvre par un petit parcours de base servant de tutoriel.

| Aspect | Impact |
|---|---|
| Modèle | Flag `mandatory` sur Journey + rattachement Journey → Monde (préfigure la hiérarchie Marelle → Monde → parcours) |
| Backoffice | Option "parcours obligatoire" dans la gestion d'un parcours |
| Front | Le parcours obligatoire non accompli masque/verrouille le reste du Monde ; l'accueil le met en avant |
| Questions | Un seul obligatoire par Monde ? Que voit un joueur qui saute le tutoriel d'un Monde déjà exploré ? |

### F4 — Marelle : passage mono-parcours → multi-parcours

**Origine front** : Monde 0 = un seul parcours ; dès le Monde 1, choix multiple. L'entrée "Marelle" de la nav correspond à une page type `/journeys`.

| Aspect | Impact |
|---|---|
| Modèle | Notion de Monde (au minimum un attribut sur Journey ; modèle `World` seulement si nécessaire, cf. [marelle-mondes.md](marelle-mondes.md) §3) |
| Front | Page Marelle = catalogue de parcours du Monde courant + pédagogie explicite du passage ("tu peux désormais mener plusieurs parcours de front") |
| UX | Moment de seuil à soigner : l'arrivée au Monde 1 change la règle du jeu |

### F5 — Récit, Graines de Récit et mentors IA

**Origine front** : remplace le feedback actuel. À la fin d'un parcours ou à des étapes-clés, le joueur fait le point avec un mentor IA (héros d'une bibliothèque de mentors) et produit un **Graine de Récit**. Les résonances des autres joueurs germent sur les Graines.

| Aspect | Impact |
|---|---|
| Modèle | `Mentor` (bibliothèque : nom, personnage, prompt/persona, visuel) ; `StorySeed` (auteur, parcours/étape source, contenu issu de la conversation, mentor, visibilité) ; résonances rattachées aux Graines (évolution de la messagerie actuelle ou nouvel objet) |
| Backoffice | Gestion de la bibliothèque de mentors ; configuration des déclencheurs (fin de parcours / étapes-clés d'un parcours long) |
| IA | Conversation mentor = intégration LLM (nouveau composant technique — API, coûts, modération) ; le joueur valide/corrige la Graine produit (garde-fou : l'IA n'impose jamais le sens, cf. [relations-recits-collectifs.md](relations-recits-collectifs.md) §2) |
| Existant | Un exemple de mentor existe dans le parcours Monde 0 actuel de vibe.ze.game — à documenter comme référence |
| Lien vision | Concrétise le "récit-fresque" ([relations-recits-collectifs.md](relations-recits-collectifs.md)) : Grain ≈ bloc narratif |

### F6 — Oméga (Cosmo Coin Oméga)

**Origine front** : indicateur de progression manquant. Monnaie de conscience = points des Actions + progression dans les 7 puissances. Représentation : lemniscate Lumière — Point Zéro — Ombre, animée selon l'amplitude.

| Aspect | Impact |
|---|---|
| Modèle | À articuler avec `Point` existant (points par compétence) : l'Oméga est-il la somme des points, ou un calcul distinct intégrant les 7 puissances ? Les 7 puissances doivent-elles devenir des données structurées (aujourd'hui : noms de compétences "PUISSANCE : ASPECT") ? |
| Front | Composant lemniscate réutilisable (chip compacte + carte détaillée) ; animation d'amplitude Ombre/Lumière à définir en fonction de données réelles |
| Garde-fou | L'Oméga ne doit pas devenir un score de conscience public ni un classement ([monde-miroir.md](monde-miroir.md) §13) ; c'est le "mana" de la vision — vocabulaire à unifier (mana vs Oméga) |
| Prototype | Première interprétation visuelle dans le proto `point-zero-home` (état `monde0`) |

### F7 — Mode événement d'un parcours

**Origine front** : page Festival-direct. Les expériences d'un événement correspondent à un parcours, avec un mode d'affichage et des champs spécifiques.

| Aspect | Impact |
|---|---|
| Modèle | Flag/mode `event` sur Journey + champs par Action : `format`, `salle`/`lieu`, référentiels multiples (7 puissances, 5 cadres...) + **`Session`** : un même atelier proposé plusieurs fois dans la journée (tranche horaire, capacité et compteur de participants PAR session) |
| Facilitateurs | Rattachement d'un ou plusieurs facilitateurs à une expérience ; interface de **validation en masse** (principalement : valider la présence réelle à l'atelier) ; pas de bouton feedbacks côté joueur en mode événement |
| Vue détail | Réutilise la vue Action existante (type journeys/.../challenges/...) sans le bouton FEEDBACKS, avec ajout Format / Lieu / Tranche horaire et sélecteur de créneau |
| Backoffice | Statut « événement » activable sur un parcours → les expériences s'affichent en mosaïque (au lieu de linéaire) ; gestion des salles et des sessions ; suivi des compteurs ; rattachement des facilitateurs |
| Front | Affichage mosaïque (grille filtrable) au lieu de la liste ; états disponible/recommandé/vécu/à intégrer/complet ; compteur "8/15" visible |
| Technique | Compteur de participants = donnée temps réel (SSE existant réutilisable ?) ; contraintes jour J : cache, QR codes, charge (cf. [accueil-point-zero.md](accueil-point-zero.md) §9) |
| Deadline | Festival confirmé le 1er octobre — chemin critique |

### F8 — Vocabulaire

| Décision | Détail |
|---|---|
| Challenge → **Action** | Retenu (lien sociétariat : en entrant dans la Marelle, les joueurs deviennent sociétaires du Point Zéro et génèrent des Oméga). "Expérience" conservé pour les moments vécus en événement. À confirmer définitivement avant implémentation. |
| Feedback → **Graine de Récit + résonances** | Cf. F5 |
| Points → **Oméga (Ω)** | Cf. F6 |

### F9 — Inscription événement et rattachement du billet

<!-- Ajout Codex, 2026-07-13 -->

**Origine front** : états `festival-inscription`, `festival-lier` et `festival-confirme` du wireframe v2.1. Le joueur doit passer de « intéressé » à « inscrit » même si l'adresse e-mail de son compte diffère de celle de l'achat.

| Aspect | Impact |
|---|---|
| Modèle | `EventRegistration` séparé du compte : événement, fournisseur (`woocommerce`/`stripe`/manuel), identifiants externes de commande et de billet, statut de paiement, statut de rattachement, `user_id` nullable, code/jeton à usage unique, date de check-in |
| Identité | **Stratégie en 4 niveaux (Boris, 2026-07-13 — on contrôle entièrement la billetterie WP)** : ① rattachement automatique par jeton de contexte quand l'achat part de l'appli (zéro saisie) ; ② lien magique « Activer mon billet dans l'appli » dans l'e-mail de confirmation ; ③ rapprochement assisté : consigne « utilisez le même e-mail » sur la billetterie + proposition de rattachement à confirmer quand un billet non lié porte l'e-mail du compte ; ④ code/QR en dernier recours (billet offert, autre adresse). L'e-mail seul ne relie jamais automatiquement — il suggère, l'utilisateur confirme |
| Backoffice | Pour chaque événement : mode d'inscription, URL externe, identifiant fournisseur, dates de vente, capacité, URL de retour ; recherche et rattachement manuel d'un billet ; resynchronisation ; journal d'erreurs |
| Front | CTA « M'inscrire », retour après paiement, « J'ai déjà un billet », confirmation, billet disponible hors connexion ; l'état inscrit pilote la priorité de l'accueil |
| Pont WordPress | Extension légère côté WordPress pour conserver un identifiant de contexte dans la commande, notifier l'appli lors d'un changement de statut et produire un retour signé. L'API Event Tickets permet l'accès authentifié aux participants ; les webhooks WooCommerce peuvent notifier les changements de commande |
| Exploitation | Vérifier le statut WooCommerce qui déclenche la création et l'envoi du billet. Event Tickets Plus attend par défaut une commande `completed`, avec possibilité de choisir d'autres statuts dans ses réglages d'intégration |
| Paiement natif | Alternative ultérieure avec Stripe Checkout et webhook idempotent. L'appli devient alors propriétaire des produits, prix, taxes, remboursements, stocks, billets et support de paiement |
| Sécurité | Vérifier les signatures, rendre les traitements idempotents, ne jamais exposer les identifiants de commande comme preuve suffisante, expirer les jetons de rattachement et journaliser les changements d'utilisateur |

**Décision proposée pour le Festival pilote** : conserver Event Tickets Plus + WooCommerce + Stripe et développer le pont d'identité. La billetterie native n'est à envisager qu'après mesure des limites réelles du tunnel existant et confirmation d'un besoin récurrent multi-événements.

Références techniques officielles : [intégration Event Tickets + WooCommerce](https://theeventscalendar.com/knowledgebase/woocommerce-integration-feature/), [API REST Event Tickets](https://theeventscalendar.com/knowledgebase/event-tickets-rest-api/), [webhooks WooCommerce](https://developer.woocommerce.com/docs/best-practices/urls-and-routing/webhooks/), [Stripe Checkout et fulfillment](https://docs.stripe.com/checkout/fulfillment).

### Décisions UX transverses (Boris, 2026-07-13)

- **Cercles masqués tant que non pertinents** : aucune section « cercle » dans l'interface tant que le joueur n'a pas effectivement rejoint le monde qui les introduit (Monde 2). Retirés de l'accueil Monde 0 et de l'après-Festival dans le proto v2.2.
- **Vocabulaire : « Graine de Récit »** (et non « Grain ») — on sème une Graine, les résonances y germent.

## 2. Vue d'ensemble — dépendances entre chantiers

```text
F2 (libre/linéaire) ──┐
F3 (obligatoire)  ────┼── prérequis du Monde 0 jouable
F6 (Oméga)        ────┘
F5 (Récit/mentors) ── indépendant, gros chantier IA — peut suivre
F1 (News)          ── indépendant, petit — quick win
F7 (mode événement)── chemin critique Festival (1er octobre)
F9 (inscription)   ── chemin critique avant F7 — identité et billet
F4 (Marelle multi) ── nécessaire seulement à l'ouverture du Monde 1
```

Ordre suggéré : **F9** (inscription et billet, à éprouver en premier) → **F1 + F2 + F3** (socle Monde 0, petits chantiers backoffice) → **F7** (expériences du Festival) → **F6** (Oméga, nécessite arbitrage 7 puissances) → **F5** (Récit/IA) → **F4** (Monde 1).

## 3. Décisions transverses (Boris, 2026-07-12)

1. **Base de données séparée.** La nouvelle appli Point Zéro ne partage pas la BDD de ze.game. Nouveau compte sur les stores (Apple/Google) dédié au Point Zéro. Mention « powered by ze.game » dans l'appli, et **SSO** entre les deux plateformes (chantier technique à cadrer : ze.game comme fournisseur d'identité ? OIDC ?).
2. **Oméga vs Mana : les deux, à des niveaux différents.** « Oméga » (Cosmo Coin Oméga) est la monnaie du monde IRL ; « Mana » est celle du monde-miroir. Les docs de vision utilisant « mana » restent valides pour le monde-miroir uniquement.
3. **7 puissances : référentiel existant de l'app.** Les compétences actuelles au format « PUISSANCE : ASPECT » avec framework « Point Zéro - Puissance - Lumière/Ombre » servent de base — pas de nouvelle couche de données pour la V1. Approfondissement théorique dans [sept-puissances.md](sept-puissances.md).

## 4. Questions ouvertes restantes

1. Architecture SSO : protocole, sens de la fédération (ze.game IdP ?), partage ou non des comptes existants.
2. Compteurs temps réel du Festival : SSE existant ou solution dédiée ?
3. Si BDD séparée : comment le Monde 0 actuel (données dans vibe.ze.game) migre-t-il vers la nouvelle appli ?
4. Quel mécanisme WordPress porte le contexte du compte applicatif jusqu'au billet : métadonnée de commande, champ participant dédié ou jeton de rattachement créé après paiement ?
5. Quelle source fait foi pour les capacités : stock global de billets WordPress, réservations d'expériences dans l'appli, ou deux niveaux distincts ?
6. Combien d'événements payants par an justifieraient le remplacement de WooCommerce par une billetterie Stripe native ?
