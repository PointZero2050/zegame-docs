# Vision des vues principales : Marelle, Cercle, Ressourcerie et Profil

> Ajout Codex - 2026-07-13. Synthèse du cadrage avec Boris, du diagnostic `Introspection - EVH - Final.pptx`, des visuels de Marelle et d'évaluation des chakras, et du prototype `point-zero-home` v2.5. Horizon fonctionnel à valider avant implémentation.

## 1. Principe d'ensemble

Les cinq entrées de navigation doivent raconter une seule architecture :

- **Accueil** : ce qui demande l'attention maintenant ;
- **Marelle** : où je me situe et quels parcours me sont accessibles ;
- **Cercle** : avec qui je peux échanger, grandir et agir ;
- **Ressources** : ce qui peut nourrir mon chemin ;
- **Profil** : ce que j'ai ouvert, attesté et choisi de relire sur moi.

La navigation reste stable. Lorsqu'un espace n'est pas encore accessible, l'entrée ouvre un **écran de seuil** utile plutôt qu'une page vide ou une interdiction opaque.

## 2. Marelle

### 2.1 Vue joueur

La page combine :

1. une mini-marelle verticale montrant le Monde 0 accompli, le Monde actuel, les Mondes principaux verrouillés et l'horizon Terre/Ciel ;
2. les droits déjà ouverts par le passage ;
3. le catalogue des parcours accessibles ;
4. des vues rapides `Tous`, `En cours`, `Accomplis`, `À découvrir` ;
5. des filtres par Monde, thème, durée, difficulté, puissance dominante et autres référentiels ;
6. un statut visible sur chaque parcours, sans devoir ouvrir sa fiche.

Les Mondes communs de la Marelle peuvent être visibles lorsqu'ils sont verrouillés. Les Mondes privés ou dédiés, par exemple facilitateurs ou gouvernance, restent invisibles tant que le joueur n'a pas le droit de les découvrir.

### 2.2 Modèle fonctionnel cible

La nouvelle exigence multi-parcours rend nécessaire de dissocier les notions suivantes :

- `World` : espace pédagogique et narratif de la Marelle ;
- `Journey` : parcours réalisable dans un Monde ;
- `Community` : collectif, cohorte ou espace social ;
- `WorldAccess` : droit auditable d'un joueur à entrer dans un Monde.

Hiérarchie cible :

`Marelle -> World -> Journeys`

Un Monde peut être relié à zéro, une ou plusieurs Communautés. Une Communauté peut être rattachée à un Monde principal sans devenir ce Monde. Cette séparation conserve le suivi collectif actuel et permet des Mondes dédiés sans détourner la sémantique de `Community`.

### 2.3 Déblocage automatique sans codes transmissibles

Le code reste un mécanisme de secours ou d'invitation, pas la progression normale. Un passage peut être déclenché par :

- accomplissement d'un parcours ou d'une Action finale ;
- validation humaine par un facilitateur ou un cercle ;
- invitation ;
- rôle ou certification ;
- décision manuelle d'un administrateur ;
- ancien code maintenu temporairement pour compatibilité.

Exemple Monde 0 vers Monde 1 : la dernière expérience est validée par le facilitateur ; un événement métier est émis ; une règle idempotente crée le `WorldAccess` au Monde 1 ; le joueur reçoit une notification et voit le nouveau Monde illuminé.

Le traitement doit être asynchrone et auditable, avec reprise sur erreur, révocation/override manuel et journal de la règle ayant ouvert l'accès. Il vaut mieux déclencher un service/job après commit que densifier directement les callbacks déjà sensibles de `JourneysUser` ou `ChallengesUser`.

Pour les Mondes initiatiques avancés, « automatique » signifie **automatique après la validation humaine requise**, jamais passage calculé par un simple total de points.

## 3. Cercle

### 3.1 Visibilité progressive

La proposition précédente de masquer totalement le Cercle avant le Monde 2 est remplacée par une pédagogie en trois états :

| État | Expérience |
|---|---|
| Monde 0 | Écran de seuil, courte vidéo de teasing, CTA vers la prochaine Action du Monde 0 |
| Monde 1 | Cercles de discussion thématiques ou liés aux parcours |
| Monde 2 | Cercle de croissance stable de 6 à 8 joueurs, sous-groupes et quêtes inter-cercles |

L'écran de seuil doit expliquer la différence entre conversation et cercle de croissance, sans promettre une disponibilité immédiate.

### 3.2 Données à distinguer

- `DiscussionCircle` ou conversation temporaire : thème, parcours lié, créneau ou mode asynchrone ;
- `GrowthCircle` : membres stables, facilitateur, cycle, rencontres, quêtes, sous-groupes et historique ;
- relations inter-cercles pour les actions collectives.

Une spécialisation explicite de `Circle` est préférable à l'utilisation indifférenciée de `Community`.

## 4. Ressourcerie

### 4.1 Six portes, un seul graphe

Les six cartographies proposées sont conservées, avec une formulation orientée action :

| Étape | Porte | Besoin utilisateur |
|---|---|---|
| 1 | Pensées | Comprendre |
| 2 | Pratiques | Pratiquer |
| 3 | Experts | Rencontrer |
| 4 | Projets | Soutenir |
| 5 | Communautés | Rejoindre |
| 6 | Événements | Vivre |

Cette progression est un chemin de lecture, pas une hiérarchie ontologique. La Ressourcerie reste un graphe : une Pensée peut mener vers des Pratiques, Experts, Projets, Communautés et Événements, et réciproquement.

### 4.2 UX

- recherche globale avant le choix d'une cartographie ;
- six portes visibles avec exemples et volume ;
- vue liste et vue carte ;
- filtres adaptés au type de ressource ;
- relations visibles sur chaque résultat ;
- enregistrement, partage et signalement ;
- évaluation optionnelle par les cinq cadres lorsque pertinente.

La catégorie actuelle « Chrysalides » est mieux représentée comme un sous-type, une qualification ou une relation de `Project`, afin de rester compréhensible hors du noyau Point Zéro.

## 5. Profil

### 5.1 Oméga et droits

Le profil distingue :

- **Oméga disponible** : solde éventuellement dépensable ;
- **Oméga généré** : contribution cumulée, non diminuée par les dépenses ;
- **droits ouverts** : capacités issues des Mondes, rôles, formations ou certifications.

Les droits doivent citer leur source. L'Oméga n'est ni un niveau de conscience ni un rang public.

### 5.2 Open Badges et trophées

Deux familles doivent rester séparées :

- les **Open Badges** sont des attestations vérifiables avec émetteur, critères, preuve, date et possibilité de partage ;
- les **trophées secrets** sont des récompenses ludiques internes, parfois cachées, sans valeur d'attestation.

Un parcours accompli ne produit un Open Badge que si ses critères, preuves et règles d'émission sont définis. Les parcours plus légers peuvent rester de simples accomplissements internes.

### 5.3 Carte personnelle des sept puissances

La carte s'inspire du diagnostic EVH sans en faire un diagnostic psychologique automatisé :

- synthèse générale Ombre / Point Zéro / Lumière ;
- six axes polarisés : Désir, Volonté, Imagination, Émotion, Communication et Intuition ;
- Transcendance présentée comme synthèse de circulation et contribution, sans polarité propre ;
- historique d'évolution plutôt qu'une photographie définitive ;
- source et date de chaque lecture : auto-exploration, récit, retour choisi, validation humaine ;
- visibilité privée par défaut, contrôlée par le joueur.

Le langage doit parler de circulation, d'exploration et de zones d'attention, jamais de valeur personnelle, de déficit ou de classement. Aucune inférence sensible ne doit être publiée ou partagée sans consentement explicite.

## 6. États ajoutés au prototype v2.5

- `marelle`
- `cercle-seuil`, `cercle-discussion`, `cercle-croissance`
- `ressources`, `ressources-pensees`
- `profil`, `profil-puissances`, `profil-badges`

La navigation produit est cliquable et active automatiquement la bonne section. Les six états principaux ont été contrôlés sans débordement horizontal en vue mobile 390 x 844.

## 7. Questions à trancher avant implémentation

1. Les Mondes 0 à 10 forment-ils onze positions ou faut-il renuméroter la Marelle ?
2. Un joueur peut-il avoir plusieurs `WorldAccess` actifs simultanément, y compris dans des branches métiers ?
3. Quels droits précis sont attachés à chaque Monde, indépendamment des Communautés ?
4. Quels parcours méritent un Open Badge et quelle entité joue le rôle d'émetteur vérifiable ?
5. Quelles données alimentent la carte des puissances en V1, et lesquelles restent exclusivement déclaratives ?
6. Le profil montre-t-il un solde Oméga dépensable dès la première version ou seulement la contribution cumulée ?
