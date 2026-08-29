# Messagerie Point Zéro — vision cible

> Ajout Codex — 2026-08-09. Cahier des charges produit, UX et architecture destiné à Claude.
> Ce document définit la cible de long terme. Il complète sans annuler
> [Profil communautaire et messagerie des Cercles — V1](profil-communautaire-messagerie-cercles-v1.md),
> qui reste la fondation contextuelle déjà livrée. Toute implémentation exige un audit préalable de
> l'état réel de `pointzero-app`, de ses autorisations, de son stockage et de ses notifications.
>
> La taxonomie détaillée des espaces, leurs droits de création et leur apprentissage progressif sont
> définis dans
> [Espaces de discussion et apprentissage au Monde 1](messagerie-espaces-discussion-monde-1.md).
> La couche opérationnelle Proposition / Décision / Action est détaillée dans
> [Messagerie — spécification Proposition / Décision / Action](messagerie-proposition-decision-action-specification.md).

## 0. Décision directrice

La messagerie Point Zéro ne doit pas être seulement un clone souverain de WhatsApp. Elle devient le
**système nerveux de l'écosystème** : l'endroit où une conversation peut produire de la conscience
partagée, une décision explicite, une action, une mémoire ou une œuvre.

> **Une messagerie qui ne cherche pas à retenir l'attention, mais à faire circuler la Puissance.**

La cible doit néanmoins couvrir suffisamment bien les usages ordinaires de WhatsApp pour que les
Cercles et les équipes de projet puissent réellement le quitter. La singularité Point Zéro vient
ensuite par couches, sans rendre la conversation simple difficile.

## 1. Relation entre la V1 et la cible

La V1 conserve ses décisions structurantes :

- conversations de mise en relation rattachées à un contexte réel ;
- participants et lecteurs explicites ;
- séparation stricte entre contenu des messages et état métier ;
- divulgation progressive des coordonnées et traces personnelles ;
- blocage, signalement et ouverture consentie au Cercle ;
- notifications externes limitées à un retour sécurisé vers l'application.

La cible ajoute progressivement :

1. la **souveraineté fonctionnelle**, permettant de quitter WhatsApp ;
2. la **messagerie capacitante**, reliant les échanges aux actions, décisions et traces ;
3. la **messagerie de Conscience**, offrant des protocoles de polarités, de facilitation et de
   mémoire collective.

La cible ne justifie pas une réécriture immédiate. Les nouvelles primitives doivent prolonger le
socle actuel ou organiser une migration explicite, jamais créer un deuxième système de messages
sans stratégie de convergence.

### 1.1. Premier espace au Monde 0

Le Monde 0 ouvre un espace communautaire volontairement limité. Sa finalité canonique, ses gestes
et son vocabulaire sont fixés dans
[Espace d’échange du Monde 0 et conservation du fil des Guides](espace-echange-m0-conservation-guides.md).
Cet espace prolonge l’expérience par la rencontre et la Résonance ; il ne constitue pas encore la
messagerie complète du Monde 1.

## 2. Principes de conception

1. **Le contexte précède le canal.** Un espace existe pour un Cercle, un projet, une expérience,
   une mission, une candidature, un événement ou une consultation identifiable.
2. **La conversation reste fluide.** Les protocoles Point Zéro sont disponibles, suggérés ou
   déclenchés volontairement ; ils ne transforment pas chaque message en formulaire.
3. **Le message n'est pas l'objet métier.** Une décision, une action, une Graine, un rendez-vous ou
   une Contribution possède ses propres droits, états et historique.
4. **Le vivant et la mémoire sont distincts.** Le Fil accueille l'éphémère ; la Mémoire conserve
   seulement les traces élevées volontairement.
5. **L'IA reflète, elle ne gouverne pas.** Elle propose des synthèses explicables et contestables ;
   elle ne diagnostique pas les personnes et n'arbitre pas seule.
6. **L'engagement n'est pas la captation.** Aucun mécanisme ne récompense le volume, la présence
   continue ou la popularité.
7. **La confidentialité est contextuelle.** Voir un Cercle, un projet ou un profil ne donne jamais
   automatiquement accès à ses conversations.
8. **Le système reste contestable.** Toute synthèse, classification ou règle doit pouvoir être
   corrigée, refusée ou révisée.

## 3. Architecture fonctionnelle en quatre couches

### 3.1. Couche 1 — Conversation souveraine

Le socle nécessaire pour remplacer WhatsApp comprend :

- conversations privées et collectives ;
- réponses à un message et sous-fils lisibles ;
- images, vidéos, fichiers et aperçus enrichis des liens ;
- réactions par emojis ;
- mentions ;
- sondages et votes simples ;
- messages épinglés ;
- recherche ;
- compteurs de non-lus fiables ;
- réglages de notification par espace ;
- mode silencieux, digests et plages de repos ;
- interface mobile et PWA utilisable en conditions réelles ;
- export des données accessibles au joueur.

Les accusés de lecture et la présence en ligne ne sont pas requis par défaut. S'ils existent, ils
sont désactivables et ne deviennent jamais un instrument de pression sociale.

### 3.2. Couche 2 — Contexte et objets d'action

Les messages peuvent référencer des cartes structurées :

- expérience ou parcours ;
- Graine de Récit ;
- demande de Résonance ;
- ressource ou œuvre ;
- événement ou proposition de rendez-vous ;
- mission, besoin ou action collective ;
- proposition et décision ;
- élément du Pacte-Source ;
- projet à rejoindre ou financer ;
- Contribution à examiner.

Une carte est un aperçu d'un objet réel. Elle ne duplique pas dans le message l'état, les droits ou
les données sensibles de cet objet.

### 3.3. Couche 3 — Protocoles Point Zéro

Les espaces peuvent activer des protocoles de Résonance, confrontation, consentement,
reconnaissance, redistribution, cartographie des polarités et passage vers un rituel synchrone.

### 3.4. Couche 4 — Mémoire et miroir IA

Le système aide les membres à distinguer :

- ce qui a été dit ;
- ce qui a été compris ;
- ce qui a été décidé ;
- ce qui doit être fait ;
- ce qui mérite d'être transmis.

L'IA produit des propositions de synthèse reliées à leurs messages sources. Une synthèse ne devient
une trace collective qu'après validation humaine explicite.

## 4. Typologie des espaces

La présente section fixe les quatre grandes familles de navigation. Elle ne remplace pas les
gabarits détaillés et leurs frontières fonctionnelles, documentés dans
[Espaces de discussion et apprentissage au Monde 1](messagerie-espaces-discussion-monde-1.md).

La navigation générale distingue quatre familles :

| Famille | Fonction | Exemples |
|---|---|---|
| **Échanges** | Relations privées et mises en relation | conversation directe, candidature, invitation |
| **Cercles** | Vie des Cercles de croissance | cycle annuel, séance, Pacte-Source, rôles tournants |
| **Projets** | Production et coordination | équipe, mission, événement, œuvre, Chrysalide |
| **Le Commun** | Information et souveraineté collective | annonces, besoins, consultations, Fonds commun |

Un même moteur technique peut servir ces espaces, mais chacun possède des lecteurs, actions,
politiques de conservation et protocoles différents.

### 4.1. En-tête obligatoire d'un espace

L'utilisateur doit toujours pouvoir voir :

- le nom et la finalité de l'espace ;
- son contexte métier ;
- ses participants et lecteurs ;
- son caractère permanent, cyclique ou temporaire ;
- les règles ou le Pacte-Source applicable ;
- son niveau de confidentialité ;
- les actions actuellement ouvertes.

### 4.2. Cycle de vie

Un espace peut être `préparé`, `ouvert`, `en pause`, `clos` ou `archivé`. La clôture interdit de
nouveaux messages sans supprimer l'historique autorisé. La dissolution d'un Cercle ou d'un projet
doit définir explicitement le devenir du Fil, des décisions, des actions et de la Mémoire.

## 5. UX d'un espace collectif

Chaque espace propose trois vues principales. Au Monde 1, l'ancienne séparation entre
Actions et Décisions est remplacée par un seul cycle visible de **Mouvements** :

| Vue | Contenu |
|---|---|
| **Fil** | Messages, médias, réactions, réponses et sous-fils |
| **Mouvements** | Intentions à éclaircir, consentements, tensions, porteurs, échéances et accomplissements |
| **Mémoire** | Graines, apprentissages, accords, synthèses et œuvres conservées |

Le composeur reste d'abord un champ de message. Un bouton d'ajout ouvre :

`Mettre une intention en mouvement · Lancer un sondage · Proposer une rencontre ·
Partager un élément de Récit · Partager une ressource`

`Partager un élément de Récit` ne propose que les objets PZ existants — Graine ou Trace.
`Partager une ressource` ne propose que les apports techniques — fichier ou lien. Le
contrat M1 complet est fixé dans
[Messagerie M1 — mettre une intention en mouvement](messagerie-mouvement-collectif-m1.md).

Sur mobile, le contexte, les lecteurs et l'intention du sous-fil restent accessibles sans occuper
en permanence la moitié de l'écran. Les actions métier ne doivent pas être dissimulées dans le menu
d'un message ordinaire.

## 6. Intentions de conversation

Un espace ou un sous-fil peut déclarer une intention :

- **Explorer** : comprendre, questionner et relier ;
- **Résonner** : exprimer ce qu'un récit, une expérience ou une œuvre met en mouvement ;
- **Coordonner** : répartir les actions et les ressources ;
- **Décider** : faire évoluer une proposition selon un protocole explicite ;
- **Confronter** : travailler une tension ou un désaccord ;
- **Reconnaître** : nommer les apports et incrémenter le récit ;
- **Redistribuer** : évaluer la valeur puis proposer une répartition.

L'intention adapte les cartes et les actions proposées. Elle ne change jamais automatiquement les
droits ni les états métier.

## 7. Réactions sémantiques

Les emojis ordinaires restent possibles. Un second registre offre des réactions dont la
signification est stable :

- `Cela résonne` ;
- `Je soutiens` ;
- `Je nuance` ;
- `Je questionne` ;
- `Je m'engage` ;
- `J'ai une objection` ;
- `J'ai besoin de clarification` ;
- `À transformer en action` ;
- `À garder dans la Mémoire`.

Ces réactions :

- ne génèrent ni score social, ni classement, ni Oméga ;
- peuvent être retirées ;
- sont visibles selon les droits du message ;
- peuvent ouvrir une suite structurée sans la rendre obligatoire.

Une objection peut demander ce qu'elle protège, le risque qu'elle révèle et la condition qui
permettrait de la lever. Elle reste un objet lié à une proposition, jamais un simple emoji négatif.

## 8. Cartes structurées

### 8.1. Contrat commun

Chaque carte affiche au minimum :

- son type et son contexte ;
- son auteur ou porteur ;
- son statut ;
- les personnes habilitées à agir ;
- son action principale ;
- un lien vers l'objet complet ;
- une représentation honnête des données devenues indisponibles.

Le message peut être supprimé ou archivé sans supprimer silencieusement l'objet référencé. La
suppression de l'objet doit laisser une trace minimale lorsque l'intégrité d'une décision ou d'une
action l'exige.

### 8.2. États indicatifs

- Mission : `proposée → prise → en cours → achevée / abandonnée` ;
- Mouvement M1 : `à éclaircir → à consentir → en mouvement → accompli / à poursuivre /
  abandonné / à réviser` ;
- Rencontre : `proposée → disponibilité recueillie → confirmée → passée / annulée` ;
- Graine : `privée → partagée dans ce contexte → élevée dans la Mémoire` ;
- Contribution : `signalée → documentée → examinée → reconnue / à compléter`.

Ces états sont des exemples de cible et non des noms de colonnes imposés.

## 9. Du Fil à la Mémoire

La plupart des messages restent dans le Fil. Les membres autorisés peuvent proposer :

- `Transformer en Graine` ;
- `Mettre une intention en mouvement` ;
- `Ajouter à la Fresque du Cercle` ;
- `Ajouter au Pacte-Source` ;
- `Conserver comme apprentissage` ;
- `Soumettre comme Contribution` ;
- `Proposer à la Ressourcerie`.

La personne à l'origine d'une trace sensible conserve un droit de consentement sur son changement
de contexte. Une conversation privée ou une Graine intime ne devient jamais mémoire collective par
simple vote majoritaire.

La Mémoire distingue :

- sources brutes ;
- synthèses proposées ;
- synthèses validées ;
- décisions ;
- actions ;
- apprentissages ;
- œuvres et ressources produites.

## 10. Cartographie des polarités

Lorsqu'une tension le justifie, un participant ou un facilitateur peut ouvrir une carte de
polarités liée au sous-fil :

1. quelles positions ou forces sont en tension ?
2. qu'est-ce que chaque pôle cherche à protéger ?
3. quelle qualité porte-t-il ?
4. quelle Ombre apparaît lorsqu'il devient exclusif ?
5. quels besoins et récits le soutiennent ?
6. quelle proposition pourrait faire circuler les qualités des deux pôles ?

L'interface ne réduit pas la tension à `pour / contre`, ne suppose pas que la vérité est au milieu et
ne produit pas un score de dépolarisation des personnes. Elle peut représenter les contributions
autour des pôles et les propositions d'intégration au Point Zéro.

## 11. Les cinq Cadres comme lecture collective

Les vues collectives peuvent être relues selon :

- **Relationnel** : liens, place, confiance, conflit — traduction de la Volonté ;
- **Sens** : intention, récit, orientation — traduction de l'Imagination ;
- **Gouvernance** : décisions, consentements, responsabilités — traduction de l'Émotion ;
- **Opérationnel** : actions, moyens, rythmes — traduction de la Communication ;
- **Apprenance** : questions, retours et transformations — traduction de l'Intuition.

Le système peut signaler un manque structurel observable, par exemple :

> Plusieurs actions sont attribuées, mais aucune décision explicite n'est enregistrée.

Il ne doit jamais conclure qu'une personne ou un Cercle a une Puissance faible à partir de ses
messages. Toute donnée utilisée ultérieurement dans une évaluation des Puissances exige un processus
séparé, explicite et contestable.

## 12. Décisions et consultations

### 12.1. Protocoles possibles

- sondage simple ;
- vote de préférence ;
- classement de propositions ;
- consentement avec objections argumentées ;
- consultation ouverte ;
- estimation d'effort, de risque ou d'impact ;
- allocation d'un budget fictif ou réel ;
- orientation du Fonds du Commun ;
- délégation temporaire d'un mandat.

### 12.2. Invariants

Une décision conserve :

- proposition et versions ;
- protocole choisi ;
- électorat ou participants éligibles figés au moment pertinent ;
- anonymat ou publicité annoncés avant participation ;
- ouverture et clôture ;
- contributions, objections et réponses ;
- résultat brut ;
- éventuelle pondération, affichée séparément ;
- décision finale et date de révision ;
- journal d'audit.

La pondération par Oméga n'est jamais le réglage par défaut des décisions ordinaires d'un Cercle.
Elle ne s'applique que dans les domaines de souveraineté explicitement définis, notamment les
consultations du Commun et l'orientation financière. Les réponses brutes et pondérées restent
visibles en parallèle.

## 13. Passer de l'écrit au rituel

Une messagerie consciente doit reconnaître ses limites. Depuis un échange, les membres peuvent :

- proposer une réunion ;
- ouvrir un Cercle de confrontation ;
- demander une médiation ;
- solliciter un facilitateur ;
- ouvrir une constellation ;
- mettre le fil en pause ;
- transformer le fil en ordre du jour.

Le système peut suggérer un passage synchrone à partir de signaux structurels — longueur, répétition,
objections non traitées — mais ne l'impose jamais comme sanction et ne qualifie pas les personnes.

## 14. Miroir IA

### 14.1. Fonctions autorisées

À la demande, un mentor ou LLM spécialisé peut :

- résumer un fil avec renvoi vers les sources ;
- distinguer faits, interprétations, besoins et propositions ;
- relever décisions, actions, responsables et échéances ;
- identifier les questions ou objections non traitées ;
- préparer un ordre du jour ;
- proposer une cartographie des polarités ;
- relire la conversation par les cinq Cadres ;
- produire un résumé pour les absents ;
- proposer plusieurs reformulations d'un message conflictuel ;
- préparer une synthèse à soumettre à validation.

### 14.2. Interdits

Le LLM ne doit pas :

- diagnostiquer une personne ou son niveau de conscience ;
- attribuer des intentions cachées ;
- calculer une compatibilité psychologique ;
- désigner un coupable ;
- décider ou clore une objection seul ;
- attribuer automatiquement des Omégas ;
- publier une synthèse comme vérité collective sans validation ;
- exploiter silencieusement une conversation privée dans un autre contexte.

### 14.3. Exigences UX et données

- invocation visible et volontaire ;
- périmètre des messages analysés annoncé ;
- résultat identifié comme proposition IA ;
- sources consultables ;
- correction et contestation possibles ;
- politique de conservation distincte ;
- aucun profil psychologique latent construit à partir des conversations.

## 15. Souveraineté, confidentialité et sécurité

### 15.1. Doctrine

- hébergement et sous-traitants documentés ;
- aucune publicité ni revente de données ;
- export individuel et collectif selon les droits ;
- suppression et conservation compréhensibles ;
- chiffrement en transit et au repos ;
- lecteurs explicites et testés négativement ;
- pièces jointes soumises aux mêmes droits que leur message ;
- liens de partage externes désactivés par défaut ;
- journalisation des changements de participants et de droits ;
- outils de blocage, signalement et modération distribuée.

Le chiffrement de bout en bout ne doit pas être promis sans modèle de menace et arbitrage avec la
recherche, les aperçus, la modération et les fonctions IA côté serveur. Des espaces à confidentialité
renforcée pourront exiger une architecture distincte et renoncer à certaines fonctions.

### 15.2. Divulgation progressive

Chaque trace conserve :

- son auteur ;
- son contexte d'origine ;
- ses lecteurs ;
- les consentements qui ont permis son déplacement ;
- les limites honnêtes de révocation après lecture ou export.

## 16. Économie de l'attention et Oméga

La cible refuse :

- score d'activité ;
- classement des personnes les plus visibles ;
- séries quotidiennes ;
- récompense du nombre de messages ou de réactions ;
- flux algorithmique optimisé pour l'engagement ;
- notifications pour chaque micro-interaction ;
- Oméga attribué automatiquement à une conversation.

Une action née dans la messagerie peut devenir une Contribution ou produire des Omégas seulement
lorsqu'elle est transformée en objet documenté et évaluée selon le processus collectif prévu. Le Fil
peut fournir des preuves ; il ne constitue jamais à lui seul la validation.

## 17. Notifications et rapport au temps

Chaque espace propose au minimum :

- toutes les notifications ;
- mentions et actions me concernant ;
- digest périodique ;
- silencieux ;
- plages de repos ;
- urgence réservée à des rôles et usages explicitement définis.

Le digest doit privilégier : décisions ouvertes, objections qui appellent une réponse, actions
assignées, rendez-vous et nouvelles traces de Mémoire — pas le volume brut de messages.

## 18. Modèle conceptuel cible

Les noms exacts restent à aligner avec `pointzero-app` après audit :

```text
MessagingSpace
├── context polymorphe : Cercle, Projet, Événement, Expérience, Consultation...
├── memberships : participants, rôles, droits, notification
├── channels / threads
│   ├── intention et cycle de vie
│   ├── messages et réponses
│   ├── reactions ordinaires et sémantiques
│   ├── attachments / media assets
│   └── structured references vers objets métier
├── decisions / consultations
├── action_items / missions
├── memory_traces
└── ai_runs / synthesis_proposals
```

Invariants :

- droits portés par la participation explicite à l'espace et affinables par sous-fil ;
- références structurées plutôt que HTML opaque ;
- états métier hors du message ;
- décisions et consentements auditables ;
- pièces jointes privées par défaut ;
- suppression en cascade interdite lorsqu'elle détruirait une décision ou une trace réglementaire ;
- absence d'analyse transversale des personnes sans finalité et consentement explicites.

## 19. Accessibilité et mobile

- navigation clavier complète ;
- textes alternatifs et transcription des médias ;
- lecteur vidéo et audio accessible ;
- contraste indépendant des couleurs Ombre/Lumière ;
- équivalent textuel de toute carte de polarités ;
- cibles tactiles suffisantes ;
- composer utilisable à une main ;
- chargement progressif des médias ;
- brouillons locaux récupérables ;
- fonctionnement acceptable en connexion intermittente ;
- pas de geste tactile comme unique moyen d'action.

## 20. Trajectoire de livraison

### Étape A — Souveraineté fonctionnelle

Objectif : permettre au Cercle cœur et à quelques projets pilotes de quitter WhatsApp.

- espaces de groupe ;
- réponses et sous-fils ;
- images, vidéos, fichiers et liens ;
- emojis et réactions ;
- sondages ;
- mentions, recherche, non-lus et notifications ;
- mobile/PWA ;
- import manuel ou conservation externe assumée de l'historique WhatsApp ;
- sécurité, sauvegarde et export.

### Étape B — Messagerie capacitante

- espaces Cercles, Projets et Commun ;
- vues Fil / Actions / Décisions / Mémoire ;
- cartes d'expérience, Graine, rencontre, mission et proposition ;
- réactions sémantiques ;
- décisions au consentement ;
- transformation explicite d'un message en objet ou trace.

### Étape C — Messagerie de Conscience

- cartographie des polarités ;
- lecture par les cinq Cadres ;
- protocoles de confrontation, reconnaissance et redistribution ;
- miroir IA sourcé et validable ;
- continuité avec Fresque, Contributions et Ressourcerie ;
- consultations du Commun et pondérations Oméga après expérimentation.

## 21. Priorités différenciantes recommandées

Après le socle WhatsApp, les trois fonctions Point Zéro à livrer en premier sont :

1. **réactions sémantiques**, peu coûteuses mais immédiatement distinctives ;
2. **cartes structurées**, fondation de toutes les continuités avec le Jeu ;
3. **transformation en action, décision ou trace**, qui empêche le Fil de devenir un puits sans
   mémoire.

La cartographie avancée des polarités et le miroir IA viennent ensuite : leur valeur dépend de la
qualité des objets, droits et traces construits auparavant.

## 22. Critères d'acceptation de la vision cible

1. Un Cercle pilote peut fonctionner sans WhatsApp pour ses échanges et médias ordinaires.
2. Un projet peut distinguer conversation, actions, décisions et mémoire sans dupliquer les données.
3. Tout espace affiche clairement contexte, lecteurs et finalité.
4. Une carte structurée reflète l'objet source et respecte ses droits.
5. Une décision conserve protocole, participants, objections, résultat et historique.
6. Une Graine ou conversation privée ne change jamais de contexte sans consentement approprié.
7. Une réaction ne produit ni classement, ni Oméga, ni score de conscience.
8. L'utilisateur peut régler le rythme des notifications et utiliser un digest.
9. Le système sait proposer un passage au synchrone sans sanction ni diagnostic.
10. Toute synthèse IA est sourcée, révisable et explicitement validée avant mémoire collective.
11. Les droits sont testés négativement entre espaces, Cercles et communautés.
12. Les médias et fonctionnalités structurées restent utilisables sur mobile et accessibles.
13. L'utilisateur peut exporter les données auxquelles il a légitimement accès.
14. Aucun flux algorithmique de captation ou récompense de volume n'est introduit.
15. La V1 de mise en relation et les fils d'expérience continuent de fonctionner sans régression.

## 23. Analyse d'impact obligatoire avant code

Claude doit d'abord auditer dans la cible actuelle :

- modèles de fils, messages, participants, réponses et notifications ;
- implémentation migrée de la messagerie V1 des Cercles ;
- autorisations positives et négatives ;
- temps réel, pièces jointes, stockage et analyse antivirus ;
- PWA, cache et comportement hors ligne ;
- e-mails et notifications futures ;
- modèles existants de Graine, Résonance, Badge, Contribution, Projet, Mission et Événement ;
- décisions et protocoles déjà présents dans les Cercles ;
- politiques de suppression, export, sauvegarde et restauration ;
- faisabilité d'une migration progressive sans seconde boîte de réception ;
- arbitrage entre chiffrement renforcé, recherche, modération et IA.

L'audit doit produire :

1. une carte de l'existant dans `pointzero-app` ;
2. les écarts par rapport à l'étape A ;
3. un modèle de droits ;
4. une proposition de migration ;
5. une stratégie de tests et de retour arrière ;
6. une estimation séparée pour A, B et C.

Aucune migration, aucun déploiement et aucun envoi réel n'est autorisé par cette spécification.

## 24. Questions encore ouvertes

- Faut-il importer une partie des historiques WhatsApp ou commencer avec des espaces neufs ?
- Quelles conversations autorisent les messages privés directs hors contexte ?
- Quelles limites de taille, durée et conservation pour les médias ?
- Les accusés de lecture sont-ils absents, optionnels ou activés par espace ?
- Quel niveau de chiffrement est requis selon les catégories d'espace ?
- Qui peut ouvrir un protocole de confrontation ou de redistribution ?
- Qui valide une trace dans la Mémoire d'un Cercle ou d'un projet ?
- Quelles décisions du Commun peuvent utiliser une pondération Oméga ?
- Quel cadre juridique s'applique aux exports, archives et décisions financières ?
- Quels usages IA peuvent être exécutés localement ou par un fournisseur souverain ?

Ces questions doivent être arbitrées par prototypes et pilotes. Elles ne doivent pas être résolues
par des choix techniques implicites.
