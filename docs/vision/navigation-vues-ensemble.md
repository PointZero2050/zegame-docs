# Vision des vues principales : Marelle, Cercle, Ressourcerie et Profil

> Ajout Codex - 2026-07-13. Synthèse du cadrage avec Boris, du diagnostic `Introspection - EVH - Final.pptx`, des visuels de Marelle et d'évaluation des chakras, et du prototype `point-zero-home` v2.5. Horizon fonctionnel à valider avant implémentation.

## 1. Principe d'ensemble

Les cinq entrées de navigation doivent raconter une seule architecture :

- **Accueil** : ce qui demande l'attention maintenant ;
- **Marelle** : où je me situe et quels parcours me sont accessibles ;
- **Cercle** : avec qui je peux échanger, grandir et agir ;
- **Ressources** : ce qui peut nourrir mon chemin ;
- **Profil** : ce que j'ai ouvert, attesté et choisi de relire sur moi.

### 1.1. Deux axes de navigation : Marelle et Freeride

<!-- Ajout Codex - 2026-07-25. Décision Boris : colonne vertébrale initiatique commune et ouverture progressive d'un deck Freeride à partir du Monde 2. -->

La Marelle conserve l'axe vertical des Mondes, rites, seuils et passages. Le futur **Freeride** ouvre un axe horizontal d'expériences optionnelles, de détours, de contributions et d'approfondissements.

- Monde 0 : trajectoire commune écrite ;
- Monde 1 : catalogue et recommandations guidées ;
- Monde 2 : ouverture réelle du Freeride, sans suppression du Cercle stable ni des rites ;
- Mondes suivants : autonomie croissante.

Le Freeride utilise de petites mains de trois cartes explicables (`Élan`, `Circulation`, `Ouverture`), jamais un flux infini. La décision détaillée et son périmètre sont dans [Cartes-couvertures et mode Freeride](cartes-experiences-freeride.md).

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

À terme, la Marelle montre également :

- la colonne vertébrale du Monde et son prochain rite ;
- la **ligne de jeu** actuelle : une expérience active, deux cartes en réserve et les expériences programmées ;
- un accès au Freeride lorsqu'il est ouvert.

Le catalogue, la page d'un parcours et le Freeride restent trois vues différentes d'expériences réutilisables. Le deck ne remplace ni le récit ordonné d'un parcours ni la visibilité de la Marelle.

La page ordonnée d'un parcours est sa **carte du voyage** : elle met la prochaine action au premier
écran, déploie les chapitres comme mouvements narratifs, distingue le chemin requis des Oméga
disponibles et rend le rite final visible dès l'entrée. Sa spécification responsive est détaillée
dans [Page parcours — la carte du voyage](page-parcours-carte-du-voyage.md).

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

Les expériences accomplies en Freeride peuvent nourrir la carte du joueur et l'Oméga, mais ne remplacent jamais une règle de passage ou un rite requis.

Le traitement doit être asynchrone et auditable, avec reprise sur erreur, révocation/override manuel et journal de la règle ayant ouvert l'accès. Il vaut mieux déclencher un service/job après commit que densifier directement les callbacks déjà sensibles de `JourneysUser` ou `ChallengesUser`.

Pour les Mondes initiatiques avancés, « automatique » signifie **automatique après la validation humaine requise**, jamais passage calculé par un simple total de points.

## 3. Cercle

### 3.1 Visibilité progressive

La proposition précédente de masquer totalement le Cercle avant le Monde 2 est remplacée par une
pédagogie en trois états :

| État | Expérience |
|---|---|
| Monde 0 | Écran de seuil, courte vidéo de teasing, CTA vers la prochaine Action du Monde 0 |
| Monde 1 | Cercle de croissance de 5 à 8 joueurs, autofacilitation, cinq rôles et Pacte-Source léger |
| Monde 2 | Cycle annuel accompagné par un facilitateur certifié, abonnement, Freeride et quêtes inter-Cercles |

L'écran de seuil doit expliquer que le Cercle commence au Monde 1 comme apprentissage collectif et
change d'intensité, de contrat et d'accompagnement au Monde 2.

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

### 5.2 Accomplissements internes

> Note Codex - 2026-07-24. Décision Boris : les Open Badges sont laissés de côté pour l'instant afin de garder une interface et un modèle simples.

Deux familles sont réunies dans le sous-menu **Accomplissements**, tout en restant visuellement distinctes :

- les **badges de complétion de parcours**, qui reprennent l'illustration du parcours dans un médaillon avec un signe d'accomplissement ;
- les **badges de seuil**, visibles ou secrets, qui marquent un premier geste, une progression Oméga, une exploration particulière ou la découverte d'une fonctionnalité.

Le standard Open Badge pourra être réexaminé plus tard si un besoin d'attestation externe apparaît. Il n'est pas une contrainte de conception de la V1.

### 5.3 Carte personnelle des sept puissances

La carte s'inspire du diagnostic EVH sans en faire un diagnostic psychologique automatisé :

- synthèse générale Ombre / Point Zéro / Lumière ;
- six axes polarisés : Désir, Volonté, Imagination, Émotion, Communication et Intuition ;
- Transcendance présentée comme synthèse de circulation et contribution, sans polarité propre ;
- historique d'évolution plutôt qu'une photographie définitive ;
- source et date de chaque lecture : auto-exploration, récit, retour choisi, validation humaine ;
- visibilité privée par défaut, contrôlée par le joueur.

Le langage doit parler de circulation, d'exploration et de zones d'attention, jamais de valeur personnelle, de déficit ou de classement. Aucune inférence sensible ne doit être publiée ou partagée sans consentement explicite.

### 5.4 Mes Récits et Contributions

**Mes Récits** donne accès aux Graines de Récit, à leurs Résonances et à leur évolution. **Contributions** rend visibles les passages où une intention est devenue action, où des puissances ont été manifestées et où des effets ont été observés chez d'autres personnes, dans un collectif ou dans le monde.

Ces deux espaces sont reliés sans être confondus : une Graine peut faire émerger une contribution et recevoir des Résonances, mais tout récit intime n'a pas à devenir une preuve. Les points gagnés dans les parcours restent le socle V1 de l'Oméga ; les contributions pourront ultérieurement compléter ou pondérer cette base selon un modèle encore à expérimenter.

## 6. États ajoutés au prototype v2.5

- `marelle`
- `cercle-seuil`, `cercle-discussion`, `cercle-croissance`
- `ressources`, `ressources-pensees`
- `profil`, `profil-puissances`, `profil-recits`, `profil-accomplissements`, `profil-contributions`

La navigation produit est cliquable et active automatiquement la bonne section. Les six états principaux ont été contrôlés sans débordement horizontal en vue mobile 390 x 844.

## 7. Questions à trancher avant implémentation

1. Les Mondes 0 à 10 forment-ils onze positions ou faut-il renuméroter la Marelle ?
2. Un joueur peut-il avoir plusieurs `WorldAccess` actifs simultanément, y compris dans des branches métiers ?
3. Quels droits précis sont attachés à chaque Monde, indépendamment des Communautés ?
4. Quelles données alimentent la carte des puissances en V1, et lesquelles restent exclusivement déclaratives ?
5. Le profil montre-t-il un solde Oméga dépensable dès la première version ou seulement la contribution cumulée ?
6. Quel premier protocole léger permet de documenter une Contribution Oméga sans créer une logique de popularité, de surveillance ou de preuve disproportionnée ?
