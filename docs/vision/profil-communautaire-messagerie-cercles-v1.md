# Profil communautaire et messagerie des Cercles — spécification V1

> Ajout Codex — 2026-07-31. Spécification produit, UX et technique destinée à Claude après
> l'implémentation de la création et de l'adhésion aux Cercles. Elle fixe ce qu'un joueur expose aux
> autres membres de sa communauté, le dossier partagé lors d'une demande d'adhésion et le périmètre
> d'une première messagerie interne. Elle complète
> [Cercles de croissance, profils systémiques, flow et Oméga](cercles-croissance-profils-flow-omega.md)
> et [Relations, récits et quêtes collectives](relations-recits-collectifs.md).

## 1. Décisions

La V1 distingue trois fonctions et trois niveaux d'exposition :

> **Le profil communautaire permet de se reconnaître.**
>
> **Le dossier de rencontre permet de se choisir.**
>
> **Le profil de Cercle permet de coopérer.**

Le bouton de contact ouvre une **conversation interne contextuelle**. L'e-mail sert uniquement à
notifier le destinataire et à le ramener dans l'application ; il n'expose pas son adresse et n'ouvre
pas par défaut le logiciel de messagerie.

La V1 réemploie l'infrastructure `Messaging::Thread` / `Messaging::Message` utilisée par les
feedbacks, Graines et validations. Elle ne crée ni un second moteur de messages, ni une messagerie
générale autorisant tous les membres à solliciter librement toute la communauté.

## 2. Principes

1. **Divulgation progressive** : une donnée n'est visible que dans le contexte qui en a besoin.
2. **Choix trace par trace** : les Puissances, Graines, coordonnées et informations sensibles ne
   deviennent jamais publiques par conséquence indirecte d'une adhésion.
3. **Confiance par les œuvres** : contributions et accomplissements éclairent davantage la rencontre
   que le volume d'activité ou un rang.
4. **Compatibilité de conditions, pas de personnes** : le système peut comparer cadence,
   disponibilité et attentes ; il ne calcule pas une compatibilité psychologique ou spirituelle.
5. **Conversation contextualisée** : la demande, le Cercle et son statut restent visibles dans le
   fil. Un message n'est jamais utilisé comme état métier implicite.
6. **Préparer sans construire toute la V2** : le modèle peut accueillir plus tard des cartes
   d'action, mais la V1 ne livre que la mise en relation des Cercles.

## 3. Les quatre surfaces de visibilité

### 3.1. Carte dans l'annuaire communautaire

La carte compacte répond en quelques secondes à `Qui ? Où ? Qu'est-ce qui l'appelle ? Que
contribue-t-elle ?` :

- photo ou avatar ;
- prénom et nom d'usage ;
- territoire approximatif choisi : ville ou bassin de vie, jamais adresse précise ;
- phrase de présentation ;
- Monde actuel ;
- Rôle d'appel choisi ou laissé ouvert ;
- jusqu'à trois badges ou contributions épinglés ;
- Oméga total ;
- statut `Disponible pour un Cercle`, `Ouvert aux échanges` ou `Indisponible` ;
- CTA `Proposer un échange` ou `Inviter dans mon Cercle` selon les droits.

L'e-mail, le téléphone, les scores détaillés de Puissances et les Graines n'apparaissent jamais sur
la carte.

### 3.2. Profil communautaire détaillé

#### Qui je suis

- identité d'usage, photo et territoire ;
- présentation libre courte ;
- langues ;
- année d'entrée dans le Jeu ;
- liens externes volontairement renseignés ;
- préférences générales de rencontre : présence, distance ou hybride.

#### Ce que j'explore

- Monde actuel et parcours significatifs choisis ;
- Rôle d'appel, formulé comme fonction explorée et non comme identité ;
- centres d'intérêt, projets ou territoires d'action ;
- expression choisie des Puissances, par exemple : `J'explore actuellement Communication et
  Intuition` ;
- sélection volontaire de Graines ou une Graine de présentation écrite pour cette surface.

Ne sont pas visibles par défaut : valeurs détaillées, état `bloqué`, polarités intimes, réponses aux
questionnaires, conversations avec les mentors, évaluations 360° et appréciations du facilitateur.

#### Ce que je contribue

- Oméga sous forme de score unique ;
- ventilation autorisée entre Moteur, PsychoKernel/Cadres et contribution-impact lorsque ces piliers
  existent réellement ;
- cumul historique distingué des Omégas actifs lorsque le decay sera implémenté ;
- badges internes ;
- contributions, œuvres, ressources, formats ou parcours créés ;
- ateliers et événements que le joueur choisit de rendre visibles ;
- reconnaissances reçues, sans classement de popularité.

L'Oméga informe sans devenir un score d'admission. L'interface évite toute hiérarchie `meilleurs
joueurs`, seuil minimal ou tri par Oméga pour composer un Cercle.

#### Me rencontrer

- ce qui amène la personne au Point Zéro ;
- ce qu'elle cherche maintenant ;
- ce qu'elle aimerait rendre possible ;
- disponibilité déclarée ;
- boutons `Proposer un échange` et `Inviter dans mon Cercle` ;
- politique choisie : `Contact dans l'application`, `E-mail partageable sur demande`, `Téléphone
  partageable après mise en relation`.

### 3.3. Dossier de rencontre partagé avec un Cercle précis

Le dossier n'est visible que par le candidat et le ou les interlocuteurs explicitement désignés. Il
contient :

- motivation de la demande ;
- ce que le joueur espère du Cercle ;
- ce qu'il pense pouvoir y apporter ;
- rythme et créneaux disponibles ;
- présence, distance ou hybride ;
- territoire et contraintes de déplacement ;
- durée et intensité d'engagement envisagées ;
- rapport souhaité à la confrontation ;
- sujets qu'il ne souhaite pas aborder ;
- besoins d'accessibilité choisis ;
- expérience antérieure des Cercles ;
- autres appartenances que le joueur choisit de signaler ;
- Rôle d'appel ou fonctions à expérimenter ;
- zéro à deux Graines jointes volontairement.

Le système peut restituer :

```text
Cadence compatible · Présentiel à organiser · Intensité proche ·
Attentes de confrontation à discuter
```

Il ne produit pas `compatible à 82 %`, `profil complémentaire`, `niveau insuffisant` ou une
recommandation automatique d'accepter/refuser.

### 3.4. Profil relationnel entre membres d'un Cercle

Après adhésion, peuvent s'ajouter :

- coordonnées explicitement partagées avec ce Cercle ;
- disponibilité pratique ;
- prochain rôle tournant ;
- engagements consentis dans le Pacte-Source ;
- contributions et actions du Cercle ;
- Graines partagées avec ce Cercle ;
- préférences de communication ;
- informations de sécurité ou d'accessibilité choisies.

L'adhésion ne donne jamais accès automatiquement à toute la Fresque, aux conversations avec les
mentors, aux Puissances détaillées ou aux évaluations individuelles.

## 4. Parcours de mise en relation V1

### 4.1. Déclencheurs

Deux entrées suffisent :

- `Proposer un échange` depuis un profil ;
- `Inviter dans mon Cercle` depuis un profil ou la page du Cercle.

Une candidature déposée depuis `Cercles à découvrir` rejoint le même parcours et le même objet
métier. Il ne doit pas exister un fil pour la candidature et un second pour la conversation.

### 4.2. Séquence

1. Le demandeur écrit un message court et, si nécessaire, complète le dossier de rencontre.
2. L'application crée ou retrouve la demande d'adhésion/invitation et son fil unique.
3. Le destinataire reçoit une notification e-mail sobre avec lien profond ; aucun récit sensible
   n'est inclus dans l'e-mail.
4. La conversation se déroule dans l'application.
5. L'un des participants peut proposer une rencontre ou partager une carte de contact.
6. La demande passe explicitement à `acceptée`, `refusée`, `retirée` ou reste `en échange`.
7. L'adhésion effective déclenche les droits du membre ; elle ne résulte jamais du simple envoi d'un
   message.

### 4.3. Participants et ouverture au Cercle

Au départ, le fil réunit :

- le candidat ou invité ;
- un référent habilité : créateur, facilitateur ou membre mandaté.

Si la décision implique tout le Cercle, le candidat choisit d'ouvrir son dossier et tout ou partie
de l'échange aux membres concernés. L'ajout de participants est visible et historisé. Une
candidature ne devient pas automatiquement lisible par les 5 à 8 membres.

## 5. Coordonnées et notifications

### 5.1. Règle

**Permettre le contact ne signifie pas exposer les coordonnées.**

Chaque joueur choisit séparément :

- partager mon e-mail dans ce fil ;
- partager mon téléphone dans ce fil ;
- partager ces coordonnées avec ce Cercle après adhésion ;
- canal préféré ;
- autoriser ou non les appels.

Le partage est révocable pour les accès futurs, sans prétendre effacer une information déjà copiée
par un destinataire. Cette limite doit être indiquée honnêtement.

### 5.2. E-mail V1

L'e-mail contient au maximum :

- identité d'usage de l'expéditeur ;
- type de demande ;
- nom du Cercle ;
- CTA sécurisé vers le fil ;
- réglage des notifications.

Pas de réponse par e-mail, d'adresse du destinataire révélée, de copie intégrale automatique du
message ni d'ouverture d'un client `mailto:` en V1.

## 6. Messagerie interne : périmètre fonctionnel V1

### Inclus

- texte simple conforme au composant actuel ;
- fil contextualisé par la demande et le Cercle ;
- participants explicites ;
- messages non lus et badge ;
- notification e-mail avec lien profond ;
- affichage du statut métier séparé du fil ;
- partage volontaire d'une carte de contact ;
- proposition simple de rencontre : quelques créneaux ou lien externe facultatif ;
- retrait, refus et fermeture ;
- prévention d'une nouvelle sollicitation par la même personne ;
- signalement minimal vers l'administration si le mécanisme existe déjà, sinon journalisation et
  contact support clairement indiqué.

### Reporté

- messagerie directe générale entre tous les membres ;
- conversations de groupe hors contexte Cercle ;
- pièces jointes et messages vocaux ;
- réactions, accusés de lecture et présence en ligne ;
- recherche plein texte ;
- visioconférence ;
- agenda et synchronisation de calendriers ;
- réponse par e-mail ;
- recommandations d'expérience ou de parcours ;
- actions collectives structurées ;
- chiffrement de bout en bout.

## 7. Préparer la messagerie Point Zéro future

À terme, une conversation pourra contenir des cartes structurées :

- proposition d'expérience ou de parcours ;
- invitation à un événement ;
- rendez-vous ;
- Graine volontairement partagée ;
- demande de Résonance ;
- mission ou action collective ;
- décision à consentir ;
- ressource ou œuvre à examiner.

Ces cartes doivent devenir des objets métier référencés par le message, avec leurs propres droits et
états. La V1 ne les encode ni comme HTML opaque dans `message`, ni dans les `extra` historiques de
validation des feedbacks.

La première carte structurée est la **demande d'adhésion ou invitation à un Cercle**. Son statut
reste porté par l'objet de demande, tandis que le fil porte la conversation.

## 8. Réemploi de l'infrastructure existante

L'application possède déjà :

- `Messaging::Thread` avec conteneur polymorphe ;
- `Messaging::Message` avec auteur polymorphe ;
- `messaging_threads_users` pour les participants, lus/non lus et notifications ;
- une liste de fils et une vue de conversation ;
- des mentions et un flux temps réel fournis par `mathieu_core_messaging` ;
- des fils rattachés à `ChallengesUser` et `JourneysUser` ;
- des callbacks `receive_message_extra` utilisés pour la validation.

La V1 ajoute un **nouveau contexte métier** à cette infrastructure. Le fil doit être rattaché à
l'objet actuel de demande d'adhésion/invitation créé par l'implémentation des Cercles, ou à un objet
unifié créé après audit. Ne pas rattacher artificiellement la conversation à un Challenge, ne pas
créer une table de messages parallèle et ne pas transformer un `CircleMembership` accepté en objet
temporaire de candidature sans préserver son historique.

### 8.1. Refactor préalable probable

Les vues actuelles d'index et de conversation supposent souvent que le conteneur est un
`ChallengesUser` ou un `JourneysUser` et construisent leurs titres et routes en conséquence. Avant
d'ajouter les Cercles :

- rendre le titre, l'image, l'URL et le badge de contexte polymorphes ;
- séparer le rendu d'une conversation de feedback du rendu d'une mise en relation ;
- afficher clairement les participants ;
- vérifier la stratégie de notification du moteur ;
- ne pas modifier le comportement des Graines et validations existantes.

### 8.2. Autorisations

L'accès à un fil doit dépendre d'une participation explicite, pas seulement de la capacité à voir
son conteneur ou sa communauté. Auditer notamment :

- scopes `index` et `show` de `Messaging::Thread` ;
- création, édition et suppression de `Messaging::Message` ;
- ajout et retrait de participants ;
- droits du candidat, référent, membre, facilitateur et administrateur ;
- fermeture de la demande et accès en lecture à l'historique ;
- fuite possible par notification, mention, URL directe ou recherche ;
- séparation entre communautés.

## 9. Modèle conceptuel

Les noms exacts doivent être alignés sur l'implémentation Claude existante après audit :

```text
Circle
└── Membership / JoinRequest / Invitation
    ├── initiator
    ├── candidate
    ├── circle
    ├── status
    ├── meeting_profile_snapshot
    ├── decided_at / withdrawn_at
    └── Messaging::Thread
        ├── explicit participants
        └── Messaging::Messages
```

La candidature et l'invitation doivent converger vers un même cycle d'états ou partager une
abstraction claire. Le dossier de rencontre est versionné ou figé à l'envoi pour que des
modifications ultérieures du profil ne réécrivent pas silencieusement la décision passée.

Les préférences globales de visibilité restent sur le Profil. Les consentements propres à une
demande ou un Cercle sont stockés dans leur contexte, avec date et auteur.

## 10. UX minimale

### Annuaire

- recherche par nom, territoire et sujets choisis ;
- filtres `Disponible pour un Cercle` et mode de rencontre ;
- pas de tri par Oméga, Puissance ou niveau supposé ;
- carte compacte décrite au §3.1.

### Profil

Quatre sections :

1. `Qui je suis` ;
2. `Ce que j'explore` ;
3. `Ce que je contribue` ;
4. `Me rencontrer`.

### Fil de mise en relation

- en-tête : interlocuteurs, Cercle, type et statut de demande ;
- accès au dossier partagé et à sa visibilité ;
- liste des messages ;
- composer un message ;
- `Proposer une rencontre` ;
- `Partager mes coordonnées` ;
- actions métier séparées : `Accepter`, `Refuser`, `Retirer ma demande` ;
- rappel : qui peut lire ce fil.

### Boîte d'échanges

La boîte existante peut être renommée **Échanges**. Elle filtre au minimum :

- `Cercles` ;
- `Expériences et parcours` ;
- `Archivés`.

Une même liste technique peut agréger les contextes, mais chaque type conserve son libellé, son
URL, ses droits et ses actions propres.

## 11. Critères d'acceptation V1

1. Un membre de la communauté peut consulter un profil sans voir e-mail, téléphone, scores intimes
   ou Graines non publiées.
2. Un joueur peut choisir ses contributions, badges et Graines visibles.
3. Une demande crée un seul objet métier et un seul fil contextuel.
4. Seuls les participants explicites et les administrateurs habilités accèdent au fil.
5. L'e-mail notifie sans révéler les coordonnées ni le contenu sensible.
6. Le partage d'e-mail et de téléphone exige une action distincte et contextualisée.
7. Accepter ou refuser une adhésion est une action métier explicite, idempotente et auditée.
8. Un message seul ne change jamais le statut de la demande.
9. Les feedbacks, Graines et validations existants continuent de fonctionner sans régression.
10. La suppression ou fermeture d'un fil ne supprime pas silencieusement une adhésion, une Graine ou
    une preuve de validation.
11. L'affichage fonctionne sur mobile et rend toujours visible le contexte et les lecteurs du fil.
12. Aucun classement de personnes par Oméga, Puissances ou compatibilité n'est introduit.

## 12. Analyse d'impact obligatoire avant code

Cette fonctionnalité touche l'adhésion aux Cercles, la messagerie et les données de profil. Claude
doit auditer :

- modèles et statuts des Cercles récemment implémentés ;
- `Messaging::Thread`, `Messaging::Message`, `messaging_threads_users` et mentions ;
- `MathieuCoreMessaging::ThreadsConcern`, routes montées et scopes du moteur ;
- vues d'index/show actuellement spécialisées Challenge/Journey ;
- `Ability` et droits sur conteneurs, participants, profils et communautés ;
- notifications e-mail, tâches asynchrones et préférences ;
- `User`, Profil, Oméga, Puissances, badges, Contributions, Graines et Résonances ;
- callbacks `receive_message_extra` de `ChallengesUser` et `JourneysUser` ;
- suppression en cascade des conteneurs et fils ;
- historique des adhésions et demandes déjà créées ;
- journalisation, blocage, signalement, export et suppression des données.

L'analyse doit proposer une stratégie de migration, des tests d'autorisation négatifs et un retour
arrière. Aucun déploiement, migration ou envoi d'e-mail réel n'est autorisé par cette seule
spécification.

## 13. Lots recommandés

### P0 — Audit et convergence

- relever les modèles réellement créés par Claude pour adhésion et invitation ;
- cartographier les scopes et callbacks de `mathieu_core_messaging` ;
- choisir le conteneur unique du fil ;
- préserver les données et échanges existants.

### P1 — Profil communautaire

- carte d'annuaire ;
- profil détaillé et préférences de visibilité ;
- Oméga, badges et contributions ;
- Puissances et Graines uniquement sur publication volontaire.

### P2 — Mise en relation Cercle

- fil contextuel candidat/référent ;
- dossier de rencontre ;
- notifications e-mail ;
- partage de coordonnées ;
- statuts explicites et actions idempotentes.

### P3 — Robustesse relationnelle

- blocage, signalement et journalisation ;
- ouverture consentie au Cercle ;
- proposition simple de rencontre ;
- tests de confidentialité et séparation des communautés.

### V2 — Messagerie Point Zéro

- conversations directes et collectives ;
- cartes d'expérience, parcours, rendez-vous, Résonance, mission et décision ;
- salles de Cercle et de quête ;
- recherche, pièces jointes et calendrier après cadrage dédié.
