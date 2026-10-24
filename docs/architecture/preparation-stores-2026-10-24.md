# Préparer les versions stores — liste de contrôle du 24 octobre 2026

> Demande de Boris (23 octobre, comptes Apple et Android créés) : « Quelles sont tes recommandations pour s'assurer que
> l'appli soit solide ? Dernier run de tests, sécurité, etc. ? » Rédigée par le poste fixe. Elle fait suite à
> [l'audit du 22 septembre](publication-stores-audit-2026-09-22.md), qui reste la référence pour la voie choisie
> (Hotwire Native) et pour les exigences des stores.
>
> **Base de départ** : la production est à `6e1c1c9` depuis le 24 octobre, 0 h 19 (bascule M0/M1).
>
> **Comment s'en servir** : chacun coche ce qui est à lui, avec le commit ou la preuve. Un point qui change de
> responsable se dit dans les boîtes. Les arbitrages restent à Boris.

## 0. Mesuré le 24 octobre (avant toute action)

| Constat | Mesure | Gravité |
| --- | --- | --- |
| ✔ Sécurité des en-têtes | CSP **bloquante** en préprod et en production ; HSTS ; `nosniff` ; `X-Frame-Options: SAMEORIGIN` | acquis |
| ✔ Entrées sensibles | `acces-verification` répond **404** en production ; `/monde-zero` et `/echanges` renvoient à la connexion sans session | acquis |
| ✔ Pages exigées par les stores | `/cgu` (1.1), `/politique-de-confidentialite` (1.2), `/suppression-de-compte`, `/up` : 200 | acquis |
| 🔴 **L'intégration continue ne vérifie pas la sécurité** | 40 passages sur 40 en échec, `main` compris. `bin/brakeman` force `--ensure-latest` et s'arrête dès qu'une version plus récente existe (« 8.0.6 is not the latest version 8.1.0 », code 5), AVANT d'analyser. `bundler-audit`, l'étape suivante, ne tourne donc jamais. L'autre rouge est RuboCop (mise en forme). Les tests passent. | **bloquant** |
| 🔴 **Aucune limite de tentatives** | Devise sans `:lockable` ; aucun `rate_limit` sur la connexion, le mot de passe oublié ou l'inscription par billet (Rails 8 le fait, et l'application l'emploie déjà ailleurs : `accords_de_regard`, `discussions`) | **bloquant** |
| ⚠️ Page lourde sur mobile | Fil des Échanges (30 messages) : 577 Ko de HTML compressé à chaque chargement (les `<template>` de chaque carte), plus 566 Ko de feuilles | à traiter |
| ⓘ Pas de suivi d'erreurs | Aucun outil (Sentry ou équivalent) : une erreur JavaScript sur le téléphone d'un joueur reste invisible | à décider |

## 1. Sécurité — avant toute soumission

| # | Action | Responsable | État |
| --- | --- | --- | --- |
| S1 | **Remettre la CI au vert** : retirer `--ensure-latest` (ou mettre Brakeman à jour à chaque passage), puis LIRE et traiter ce que Brakeman et `bundler-audit` trouvent ; corriger RuboCop (`-a`) | portable | ✅ 24 oct. — [#485](https://github.com/PointZero2050/pointzero-app/pull/485) `64cfe0e` : CI 5/5 verte ; Brakeman 0 avertissement (2 notés) ; bundler-audit : crass 1.0.8 ; RuboCop 0 |
| S2 | **Limiter les tentatives** : connexion, mot de passe oublié, inscription par billet, signalements, appels à l'IA (`rate_limit`, ou `:lockable` de Devise) | portable | ✅ 24 oct. — [#486](https://github.com/PointZero2050/pointzero-app/pull/486) `c04cd55` : `rate_limit` (connexion, mot de passe, billets, lettre, inscriptions, IA, signalements) ; `verifier_limites_de_tentatives` |
| S3 | **Un banc transversal des droits** : un compte étranger au fil reçoit 404 sur chaque adresse qui prend un identifiant (messages, réactions, résonances, pièces, aperçus de lien et leur vignette, discussions, Mémoire) | portable | ☐ |
| S4 | **Changer les clés** (Anthropic, Stripe, SMTP) avant l'ouverture publique, et passer un détecteur de secrets sur l'historique des dépôts | portable | ☐ |
| S5 | `acces-verification` à 404 en production, **revérifié à chaque promotion** (banc) | portable | ✅ 24 oct. — 404 en production, vérifié à la promotion `100e3e1` (et au § 6 de chaque promotion) |
| S6 | Plafonds de l'IA (`PlafondLlm`) : vérifier qu'ils couvrent les trois surfaces (Avatar, Guide, Mentor) et les regards invités | portable | ☐ |

## 2. Fiabilité

| # | Action | Responsable | État |
| --- | --- | --- | --- |
| F1 | **Suivi d'erreurs**, serveur et JavaScript (choix de l'outil et de son coût : Boris) | portable + Boris | ☐ |
| F2 | **Restauration éprouvée** d'une sauvegarde (`scripts/repeter_restauration.sh`), plus une sonde sur `/up` qui alerte | portable | ☐ |
| F3 | **Test de charge léger** (quelques dizaines de joueurs simultanés), pour l'afflux qui suit une publication | portable | ☐ |
| F4 | **Retour arrière prêt** : l'image Docker précédente gardée, et la commande écrite | portable | ☐ |
| F5 | **Alléger le fil des Échanges** : les fenêtres des cartes rendues à la demande plutôt qu'en `<template>` dans chaque carte | poste fixe (+ une route du portable si besoin) | ☐ |

## 3. Le dernier passage de tests

| # | Action | Responsable | État |
| --- | --- | --- | --- |
| T1 | **Gel de la version candidate** : on ne fusionne plus que des correctifs | Boris | ☐ |
| T2 | **Recette complète des bancs** (`scripts/recette.sh`), en préprod puis en production, sur CETTE version | portable | ☐ |
| T3 | **Recette à la main sur deux vrais téléphones** (un iPhone ancien, un Android d'entrée de gamme), dont une fois en réseau lent | poste fixe + Boris | ☐ |
| T4 | Parcours de T3 : billet → inscription → connexion ; les cinq parcours du M0 ; Échanges (écrire, réagir, répondre, partager un lien) ; paiement Stripe ouvert HORS de l'application ; suppression de compte ; lien d'un courriel qui rouvre l'application | poste fixe | ☐ |

## 4. Ce que les stores regardent (suite de l'audit du 22 septembre)

| # | Action | Responsable | État |
| --- | --- | --- | --- |
| A1 | **Compte de démonstration permanent** pour la revue (joueur, avancé dans le M0) : adresse et destinataire du courriel | Boris, puis portable | ☐ |
| A2 | **Formulaires de confidentialité** (App Privacy, Data safety) : Anthropic et Stripe déclarés ; voir [l'inventaire de données](donnees-formulaires-stores-2026-09-23.md) | Boris + portable | ☐ |
| A3 | **Classification d'âge** | Boris | ☐ |
| A4 | **Signalement visible depuis chaque surface d'IA** (Apple 1.2) | poste fixe | ☐ |
| A5 | **Définir les produits et circuits de paiement** : Atelier présentiel/en ligne et M1 mensuel/annuel payants ; mise en œuvre selon les règles des stores et les territoires retenus | Boris + portable | ☐ |
| A6 | **Une capacité native assumée** (notifications) pour la règle 4.2 d'Apple | portable | ☐ |
| A7 | `APPLE_TEAM_ID` et `APPLE_BUNDLE_ID` (manquants au 24 septembre) pour les liens qui rouvrent l'application | Boris → portable | ☐ |
| A8 | **Coques Hotwire Native** iOS et Android, puis TestFlight et le test fermé de Google Play | portable | ☐ |
| A9 | Icônes natives, captures par taille d'appareil, textes de fiche et notes de revue | poste fixe + Codex (textes) | Brouillon éditorial prêt ; arbitrage et captures à faire |
| A10 | Session durable dans l'application (`remember_for`, à rallonger et à éprouver) | portable | ☐ |

## 5. Ordre proposé

1. **S1 et S2** : sans eux, on ne sait pas ce qu'on publie, et la connexion est ouverte à l'essai de mots de passe.
2. **Les décisions de Boris** : A1, A3, A7, F1.
3. **Coques et dossier** (A8, A6, A9) en parallèle de S3, F2 et F5.
4. **Gel de la version (T1), puis recettes (T2 à T4)**, puis TestFlight et le test fermé.


## Complément Codex du 24 octobre

A9 : [brouillon des textes, notes de revue et séquence de captures](../site/stores-textes-captures-brouillon-2026-10-24.md).
Statut : proposition transmise, pas soumission prête ni validation de Boris.

**A5 à préciser pour l’offre réelle** : un paiement de billet pour un événement
physique et un paiement ouvrant du contenu numérique relèvent de règles distinctes.
Un navigateur externe ne rend pas tout achat numérique admissible. L’offre du
Festival et les droits M1 associés doivent être explicités avant dépôt, selon
les territoires et programmes retenus. **A6** : une notification ne garantit pas
à elle seule le respect du critère d’utilité de l’application.
[Apple, sections 3.1 et 4.2](https://developer.apple.com/app-store/review/guidelines/),
[Google Play, paiements](https://support.google.com/googleplay/android-developer/answer/9858738?hl=en).


**Précisions directes de Boris, même jour** : M0 gratuit ; Atelier payant, en
présentiel ou en ligne ; M1 par abonnement mensuel ou paiement annuel avec
réduction. Les tarifs et le renouvellement annuel ne sont pas arrêtés dans
ce relevé. La fiche A9 reprend le positionnement validé de jeu en réalité alternée.
