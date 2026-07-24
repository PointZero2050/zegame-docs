# Application Point Zéro autonome — stratégie Festival 2026

> Ajout Codex — 2026-07-24. Décision opérationnelle validée par Boris. Ce document est le cadrage canonique de la trajectoire vers le New Civilization Festival du **1er octobre 2026**. En cas de contradiction, il prévaut sur les recommandations antérieures relatives au maintien durable de `mathieu_core` ou au report de l'application autonome.

## 1. Décision et résultat attendu

Point Zéro sera livré comme une **application Rails autonome**, issue du travail validé dans `vibe.ze.game`, mais capable d'être installée, déployée et exploitée sans les gems privées `mathieu_core` et `mathieu_core_messaging`.

Les invariants sont les suivants :

- le dépôt privé de l'application est `PointZero2050/zegame-app` et sa branche de référence actuelle est `pointzero` ;
- `vibe.ze.game` reste le bac à sable de validation produit jusqu'à la bascule ;
- l'application Festival possède sa propre base de données et son propre cycle de déploiement ;
- le comportement métier et les parcours déjà validés sont conservés : il ne s'agit pas d'une réécriture fonctionnelle à blanc ;
- seules les capacités effectivement utilisées des gems privées sont remplacées, par des composants standards ou du code applicatif explicite ;
- l'application conserve la mention « powered by ze.game ».

## 2. Périmètre Festival à figer

Le périmètre fonctionnel doit être figé avant de transformer l'extraction technique en chantier généraliste. Chaque élément est classé dans l'une des trois catégories suivantes :

| Catégorie | Règle |
|---|---|
| **Indispensable le 1er octobre** | Nécessaire au parcours réel d'un participant ou à l'exploitation du Festival ; fait partie du chemin critique et reçoit des tests de bout en bout. |
| **Utile si stabilisé** | Intégré uniquement s'il ne menace ni l'autonomie technique ni la répétition générale. |
| **Après Festival** | Conservé dans la vision et les prototypes, mais absent du chemin critique de livraison. |

L'arbitrage doit couvrir au minimum : inscription et rattachement du billet, accueil Festival, Monde 0, expériences et réservations, validation/progression, profil et Oméga, Monde 1, Bloc 4, administration minimale, statistiques et messagerie.

Tant que cet arbitrage n'est pas écrit, **Monde 1 et Bloc 4 peuvent continuer à être éprouvés dans le bac à sable, mais ne doivent pas retarder le premier parcours autonome de bout en bout**.

## 3. Deux pistes de travail synchronisées

Le travail avance sur deux pistes, avec des zones de modification explicites :

1. **Validation produit dans `pointzero` / `vibe.ze.game`** : itérations UX et métier courtes, démontrables et réversibles.
2. **Autonomie Festival dans une branche dédiée** : caractérisation de l'existant, retrait progressif des dépendances privées, base séparée, déploiement et répétitions.

La branche `pointzero` reste une référence déployable. La branche d'autonomie, proposée sous le nom `festival-standalone`, est créée seulement après sauvegarde du code et de la base et après inventaire précis des dépendances.

Les changements issus du bac à sable sont reportés vers la branche Festival de manière choisie. Les deux branches ne doivent pas recevoir simultanément des refontes concurrentes des mêmes zones.

## 4. Méthode d'extraction

L'extraction part du code existant. Elle ne cherche pas à reproduire l'intégralité des gems privées.

### Étape 1 — Caractériser avant de remplacer

Ajouter des tests autour des comportements nécessaires au Festival, notamment :

- authentification, autorisations et rôles ;
- `Journey`, `Challenge`, `JourneysUser` et `ChallengesUser` ;
- progression, validation, points et Oméga ;
- envoi ou affichage des messages réellement utilisés ;
- parcours participant mobile, depuis la connexion jusqu'au profil.

Ces tests décrivent le contrat observable à préserver pendant l'extraction.

### Étape 2 — Remplacer seulement les usages réels

| Besoin utilisé | Cible autonome |
|---|---|
| Authentification | Devise configuré dans l'application |
| Autorisations | CanCanCan conservé localement ou Pundit, après inventaire |
| URLs lisibles | `friendly_id` si nécessaire |
| Fichiers et images | Active Storage |
| Callbacks métier | Callbacks/services Rails explicites et testés |
| CRUD et filtres d'administration | Contrôleurs, vues et scopes applicatifs minimaux |
| Messagerie | Fonction réduite au périmètre Festival ; le reste est différé |
| Déploiement | Configuration appartenant au dépôt Point Zéro |

Le premier jalon technique est une **tranche verticale autonome** : connexion → ouverture d'une expérience → action/validation → progression visible dans le profil. Ce parcours doit fonctionner sur une installation propre sans accès aux dépôts privés.

## 5. Comptes, données et billetterie

- La base Point Zéro est séparée de celle de ze.game.
- Le transfert initial est une migration contrôlée et rejouable d'un sous-ensemble explicitement défini : comptes nécessaires, contenus Point Zéro et progression utile.
- Il n'y a pas de synchronisation bidirectionnelle permanente entre les deux bases pour le Festival.
- Le rapprochement de comptes doit être documenté et auditable. Le SSO n'entre dans le chemin critique que s'il est confirmé indispensable au périmètre figé.
- La billetterie existante Event Tickets Plus + WooCommerce + Stripe reste la source d'achat recommandée pour le Festival.
- Un billet unique, et non l'adresse e-mail, constitue la preuve de rattachement à un compte. Le pont applicatif doit prévoir retour signé ou code/QR, idempotence et rattachement manuel de secours.
- Une répétition de migration sur une copie de données précède obligatoirement la bascule réelle.

## 6. Calendrier de référence

Ce calendrier est une ligne de base de pilotage ; tout glissement doit être compensé par une réduction explicite du périmètre.

| Période | Résultat attendu |
|---|---|
| **24–31 juillet** | Périmètre Festival figé, inventaire des dépendances, sauvegardes, tests de caractérisation prioritaires et branche d'autonomie prête |
| **1–14 août** | Application amorcée sans dépendances privées et première tranche verticale autonome |
| **15–31 août** | Fonctions Festival indispensables intégrées, import de données répétable, administration minimale |
| **1–14 septembre** | Parcours de bout en bout sur mobile, charge réaliste, billetterie, sécurité, observabilité et répétition de restauration |
| **15 septembre** | Gel fonctionnel cible |
| **16–30 septembre** | Corrections bloquantes uniquement, répétition générale, préparation de bascule et de repli |
| **1er octobre** | Exploitation Festival |

## 7. Bascule, critères de feu vert et repli

La mise en production autonome reçoit un feu vert seulement si :

- une installation propre fonctionne sans `mathieu_core` ni `mathieu_core_messaging` ;
- les parcours Festival indispensables passent sur mobile et dans le navigateur cible ;
- l'import de données est rejouable et ses contrôles de cohérence sont documentés ;
- sauvegarde et restauration de la base ont été répétées ;
- erreurs, disponibilité et capacité sont observables le jour J ;
- responsables, procédure de déploiement et procédure de repli sont identifiés.

Jusqu'au feu vert, `vibe.ze.game` demeure une solution de repli fonctionnelle. La bascule ne détruit ni sa base ni son code. Le domaine final, l'hébergement et la fenêtre exacte de bascule restent à décider.

## 8. Arbitrages encore requis

1. Classer chaque fonction dans les trois catégories de périmètre, en particulier Monde 1 et Bloc 4.
2. Choisir l'URL, l'hébergement et le responsable d'exploitation.
3. Confirmer si un SSO est réellement indispensable au Festival.
4. Définir précisément les comptes, contenus et progressions importés.
5. Fixer le contrat du pont WooCommerce/billet et les procédures de support.
6. Nommer le décideur du feu vert et l'équipe présente le jour J.

## 9. Traçabilité

Ce cadrage complète [accueil-point-zero.md](accueil-point-zero.md) et [impacts-fonctionnels.md](impacts-fonctionnels.md). Il remplace, pour la trajectoire Festival, la recommandation historique de [../architecture.md](../architecture.md) consistant à conserver les gems privées comme socle durable.

La logique reste incrémentale : préserver le domaine applicatif déjà construit, sécuriser son comportement par des tests, puis retirer progressivement les dépendances d'infrastructure qui empêchent l'autonomie.
