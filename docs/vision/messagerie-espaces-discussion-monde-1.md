# Messagerie Point Zéro — espaces de discussion et apprentissage au Monde 1

> Ajout Codex — 2026-08-09. Spécification produit, UX et architecture destinée à Claude.
> Elle approfondit [Messagerie Point Zéro — vision cible](messagerie-point-zero-vision-cible.md)
> en distinguant les types d'espaces, les intentions de fils, les droits de création et la
> progression pédagogique du Monde 1. Elle ne constitue pas une autorisation de coder ou de migrer
> sans audit préalable de `pointzero-app`.

## 0. Décision structurante

Il faut distinguer deux niveaux qui ne doivent pas être confondus dans le modèle ni dans l'UX :

1. **l'espace** définit qui se réunit, pour quoi, pendant combien de temps et avec quels droits ;
2. **le fil** définit l'intention momentanée d'une conversation dans cet espace.

Un Cercle de croissance reste donc un seul espace même lorsqu'il ouvre successivement un fil
informel, une confrontation, une décision, une redistribution ou un débrief d'expérience.

> **Les espaces donnent un cadre aux relations. Les fils accueillent différentes intentions. Les
> cartes transforment les paroles en objets. La Mémoire conserve ce qui mérite de survivre au flux.**

Cette séparation évite deux dérives :

- un groupe unique où annonces, décisions, actions et conversations deviennent illisibles ;
- une prolifération d'espaces créés pour chaque protocole ou sujet ponctuel.

## 1. Les quatre dimensions d'un espace

Tout espace doit rendre explicites quatre dimensions indépendantes :

### 1.1. Finalité

- relation ;
- croissance ;
- apprentissage ;
- fonction ;
- projet ou mission ;
- événement ;
- information communautaire ;
- consultation ou décision ;
- médiation ou processus sensible.

### 1.2. Population et droits

- privé entre deux personnes ;
- invitation limitée ;
- membres d'un Cercle ou d'une équipe ;
- cohorte inscrite ;
- communauté ou Monde ;
- ensemble de l'écosystème ;
- lecteurs publics éventuels.

Voir l'espace, lire son contenu, rejoindre, publier, inviter, modérer et décider sont des droits
distincts. La découvrabilité ne donne jamais implicitement un droit de lecture.

### 1.3. Temporalité

- libre ;
- éphémère ;
- liée à un cycle ;
- liée à une formation ;
- liée à un projet ;
- liée à un événement ;
- permanente mais réévaluée périodiquement.

### 1.4. Autorité

- espace libre créé par des joueurs ;
- espace créé automatiquement par le système ;
- espace confié à un porteur ou à des gardiens ;
- espace officiel de l'écosystème ;
- espace de décision régi par un mandat explicite.

## 2. Taxonomie cible des espaces

| Type | Finalité principale | Temporalité | Création indicative |
|---|---|---|---|
| **Échange individuel** | relation, accompagnement, mise en relation | libre | tout joueur selon les droits de contact |
| **Groupe informel** | échange temporaire entre quelques joueurs | libre ou éphémère | tout joueur |
| **Cercle de croissance** | individuation, Marelle, Pacte-Source | cycle annuel ou continuité choisie | système lors de la constitution |
| **Cercle fonctionnel** | tenir une fonction de l'écosystème | mandaté ou permanent | organisation ou joueurs habilités |
| **Projet ou mission** | produire une œuvre, un service ou un événement | jusqu'à clôture | porteur ou mandat collectif |
| **Cohorte d'apprentissage** | formation, parcours ou pratique partagée | durée pédagogique | système, formateur ou facilitateur |
| **Événement ou territoire** | préparer et prolonger une rencontre réelle | borné ou réévalué | organisateur ou rôle territorial |
| **Consultation du Commun** | examiner et décider une question précise | temporaire et clôturé | autorité de gouvernance définie |
| **Espace communautaire** | accueillir, informer et relier | permanent | rôle éditorial ou administration |
| **Espace sensible temporaire** | médiation, confrontation ou redistribution | fermé après résolution | participants, facilitateur ou protocole |

Ces types sont des **gabarits fonctionnels**, pas nécessairement dix classes ou tables. Claude doit
proposer après audit la représentation la plus simple permettant de porter leurs différences de
droits, cycle de vie et interface.

## 3. Définitions et frontières

### 3.1. Échange individuel

Conversation privée entre deux personnes, issue par exemple :

- d'une candidature ou invitation ;
- d'un profil communautaire ;
- d'une demande de Résonance ;
- d'un accompagnement ;
- d'un lien de projet ou de Cercle.

Une conversation directe hors contexte ne doit pas ouvrir automatiquement l'accès aux coordonnées,
Graines, Puissances détaillées ou autres espaces de la personne.

### 3.2. Groupe informel

Petit groupe créé librement pour échanger sans structure métier lourde. Il propose initialement :

- Fil ;
- médias et liens ;
- réactions ;
- sondage simple ;
- participants explicites.

Les vues Mouvements ou Mémoire peuvent être activées ensuite si le groupe se structure. Une
transformation en Projet ou Cohorte doit conserver l'historique et rendre visible le changement de
finalité.

### 3.3. Cercle de croissance

Le Cercle de croissance a pour finalité première l'individuation de chacun de ses membres et leur
progression dans la Marelle. Son espace est lié :

- au cycle et à ses membres ;
- au Pacte-Source ;
- aux cinq rôles tournants ;
- aux séances ;
- aux Graines et Résonances partagées avec le Cercle ;
- aux décisions, actions et apprentissages du collectif ;
- à la Mémoire du cycle.

Le fait d'ouvrir ponctuellement une médiation, une stratégie ou une redistribution ne transforme pas
le Cercle de croissance en Cercle fonctionnel : il ouvre un fil ou protocole spécialisé dans son
espace.

### 3.4. Cercle fonctionnel

Le Cercle fonctionnel tient une responsabilité ou un service :

- Communication PZ ;
- Ressourcerie ;
- accueil des nouveaux joueurs ;
- Festival ;
- gouvernance d'une fonction ;
- facilitation ou accompagnement.

Il possède :

- une fonction explicite ;
- un domaine de responsabilité ;
- un mandat et des limites ;
- des membres ou rôles ;
- des décisions et actions ;
- une redevabilité envers une organisation ou le Commun ;
- une règle de renouvellement ou de dissolution.

Tout espace collectif doit rester capacitant, mais la croissance des membres n'est pas ici la
finalité première : elle est une condition de tenue consciente de la fonction.

### 3.5. Projet ou mission

L'espace Projet relie :

- intention et impact recherché ;
- porteur et équipe ;
- besoins et ressources ;
- actions, responsables et échéances ;
- décisions ;
- risques et polarités ;
- financement éventuel ;
- livrables et critères de clôture ;
- apprentissages et retour au Commun.

Il est clos ou transformé lorsque son résultat est atteint, abandonné ou institutionnalisé. Il ne
doit pas rester indéfiniment dans la boîte active par inertie.

### 3.6. Cohorte d'apprentissage

Une Cohorte rassemble les participants d'une formation, d'un parcours ou d'une pratique :

- formation des facilitateurs ;
- tutoriel collectif du Monde 1 ;
- groupe de pratique de la Marelle ;
- cercle de pairs d'un métier PZ ;
- participants d'un atelier long.

Elle est plus structurée qu'un groupe informel, sans posséder nécessairement l'engagement et le
Pacte-Source d'un Cercle de croissance.

### 3.7. Événement ou territoire

Un espace d'événement peut s'ouvrir avant, pendant et après la rencontre pour :

- informations pratiques ;
- questions ;
- mise en relation consentie ;
- préparation et missions ;
- ressources ;
- retours et traces.

Un territoire n'obtient un espace permanent que lorsqu'une activité réelle le justifie. La simple
présence d'un territoire sur plusieurs profils ne doit pas créer automatiquement un groupe vide.

### 3.8. Consultation du Commun

Une consultation est ouverte autour d'une question précise et possède :

- dossier de contexte ;
- autorité qui consulte ;
- personnes éligibles ;
- protocole ;
- calendrier ;
- propositions et objections ;
- résultat brut et éventuelle pondération ;
- décision finale ;
- date de révision ;
- archive durable.

Une consultation clôturée rejoint la Mémoire du Commun au lieu de rester un groupe de discussion
permanent.

### 3.9. Espace communautaire

Il faut distinguer au moins deux modes :

#### Publication

`Actus PZ` est principalement un canal officiel. Les rôles éditoriaux publient ; les joueurs lisent
et réagissent. Chaque publication peut ouvrir un fil de discussion dédié afin que les échanges ne
noyent pas les informations suivantes.

#### Accueil et Agora

`Bienvenue aux nouveaux joueurs` permet présentation, questions et mise en relation. Il peut être
guidé et modéré, avec des sujets récurrents et une mémoire de réponses utiles. Il n'est pas une
suite indifférenciée d'annonces officielles.

### 3.10. Espace sensible temporaire

Une médiation, confrontation, redistribution ou investigation sensible doit pouvoir disposer d'un
espace temporaire avec :

- participants et lecteurs strictement explicités ;
- finalité et protocole ;
- facilitateur ou gardien du cadre ;
- durée ;
- règle de confidentialité ;
- trace finale consentie ;
- clôture explicite.

Le contenu sensible ne devient pas automatiquement lisible par le Cercle, le projet ou
l'organisation d'origine.

## 4. Intentions de fils

Dans chaque espace, un fil peut être :

- **Informer** ;
- **Explorer** ;
- **Résonner** ;
- **Coordonner** ;
- **Décider** ;
- **Confronter** ;
- **Reconnaître** ;
- **Redistribuer** ;
- **Capitaliser**.

L'intention adapte l'aide au composeur, les cartes et les actions disponibles. Elle ne change ni
les participants ni les droits sans action explicite.

Exemples :

- le Cercle de croissance ouvre un fil `Confronter` sur une tension ;
- Communication PZ ouvre un fil `Coordonner` pour une campagne ;
- un Projet ouvre un fil `Décider` sur un choix de prestataire ;
- Bienvenue ouvre un fil `Explorer` pour les questions du Monde 1 ;
- une Consultation ouvre un fil `Capitaliser` après sa clôture.

L'interface ne doit pas autoriser une profondeur infinie de fils imbriqués. Un niveau de réponse et
un niveau de sous-fil identifié suffisent pour préserver la lisibilité mobile.

## 5. Création guidée

L'application ne commence pas par demander un type technique. Elle demande :

> **Que veux-tu rendre possible ?**

Choix proposés :

- parler avec une personne ;
- réunir quelques joueurs ;
- grandir ensemble dans la durée ;
- apprendre ou pratiquer ensemble ;
- porter une fonction ;
- réaliser un projet ;
- organiser un événement ;
- consulter la communauté ;
- publier une information.

Le système propose ensuite un gabarit et demande les seules informations nécessaires :

1. intention et résultat attendu ;
2. nom de l'espace ;
3. personnes pouvant voir, rejoindre et publier ;
4. personne ou rôle qui en prend soin ;
5. durée ou date de réévaluation ;
6. ce qui doit rester après la fermeture ;
7. rythme de notification conseillé.

Avant la création, l'application recherche les espaces proches et propose de les rejoindre lorsque
leur finalité correspond. Elle ne bloque pas mécaniquement toute création similaire : deux projets
proches peuvent légitimement coexister.

## 6. Droits de création et d'évolution

| Action | Droit cible indicatif |
|---|---|
| ouvrir un échange individuel | joueur autorisé à contacter la personne |
| créer un groupe informel | tout joueur, avec protections anti-sollicitation |
| créer le Cercle de croissance | parcours de constitution ou administration |
| ouvrir un fil dans son Cercle | membre selon le Pacte-Source |
| créer un Projet ou une Mission | porteur ou membre mandaté |
| créer un Cercle fonctionnel | organisation ou gouvernance habilitée |
| créer une Cohorte | responsable de formation ou système |
| créer un espace d'Événement | organisateur habilité |
| publier dans un canal officiel | rôle éditorial |
| ouvrir une Consultation du Commun | autorité de souveraineté définie |
| ouvrir un espace sensible | participants concernés, facilitateur ou protocole |

Créer, administrer, inviter, retirer un membre, archiver et supprimer sont des permissions
distinctes. Un gardien du cadre n'est pas automatiquement propriétaire souverain des contenus.

## 7. Cycle de vie et prévention de la prolifération

Chaque espace possède :

- finalité ;
- gardien ou porteur ;
- date de création ;
- dernier usage significatif ;
- durée ou date de revue ;
- état `préparé / ouvert / en pause / clos / archivé` ;
- politique de conservation ;
- destination de sa Mémoire.

Règles proposées :

- un groupe informel inactif est proposé à l'archivage, jamais supprimé silencieusement ;
- un Projet demande une décision de clôture ou de transformation ;
- un Cercle fonctionnel revoit périodiquement son mandat ;
- un espace d'Événement bascule après la date vers une phase de retours et mémoire ;
- une Consultation se ferme automatiquement à la date annoncée, sous réserve des règles du
  protocole ;
- un Cercle de croissance conserve la mémoire de chaque cycle sans mélanger les nouveaux membres
  avec les conversations privées d'un cycle antérieur.

## 8. Accueil des Échanges

L'application ne présente pas une boîte uniforme triée uniquement par dernier message. Elle organise
les engagements :

1. **Mon Cercle** — prochain rendez-vous, décision ouverte, rôle et action attendue ;
2. **Mes échanges** — conversations privées et groupes informels ;
3. **Mes projets** — équipes, missions et échéances ;
4. **Le Commun** — informations officielles et consultations ;
5. **À découvrir** — espaces visibles mais non rejoints.

La priorité repose sur :

- mention ;
- action attribuée ;
- objection appelant une réponse ;
- décision ou consultation bientôt close ;
- prochain rendez-vous ;
- demande de consentement ;
- nouveau message privé.

Le volume brut de non-lus ne suffit pas à définir l'importance. Les espaces silencieux ou suivis en
digest ne doivent pas créer une dette psychologique permanente.

## 9. Apprentissages au Monde 1

Le Monde 1 enseigne progressivement que la messagerie est un premier exercice des Cadres collectifs,
pas seulement un outil de conversation.

### 9.1. Phase 1 — Avant le Cercle

Après quelques expériences individuelles du tutoriel, le joueur réalise trois gestes :

1. répondre à un échange individuel contextualisé ;
2. se présenter dans `Bienvenue aux nouveaux joueurs` ;
3. produire une première Résonance au message d'un autre joueur.

Objectifs :

- distinguer parole privée, parole communautaire et trace partagée ;
- régler ses notifications ;
- comprendre qui peut lire ;
- expérimenter l'accueil et la réciprocité.

Ces gestes ne donnent aucun Oméga pour le seul fait de publier.

### 9.2. Phase 2 — Rituel d'entrée dans le Cercle

Lors de la constitution du Cercle, chaque membre :

- consulte la finalité du Cercle ;
- lit et consent le Pacte-Source léger ;
- vérifie les membres et lecteurs ;
- choisit son rythme de notification ;
- publie une **Graine de présence** ;
- répond à un autre membre par une Résonance ;
- découvre les cinq rôles tournants ;
- identifie le prochain rendez-vous.

La Graine de présence n'oblige pas à livrer une donnée intime. Elle peut simplement répondre à :

> Qu'est-ce que j'apporte aujourd'hui, et de quoi ai-je besoin pour pouvoir être présent ?

### 9.3. Phase 3 — Les cinq gestes des Cadres

Le parcours collectif d'autofacilitation fait pratiquer cinq gestes :

| Cadre | Puissance | Geste dans la messagerie |
|---|---|---|
| **Relationnel** | Volonté | accueillir une parole et produire une Résonance |
| **Sens** | Imagination | formuler et amender une intention collective |
| **Gouvernance** | Émotion | prendre une petite décision par consentement |
| **Opérationnel** | Communication | transformer une proposition en action attribuée |
| **Apprenance** | Intuition | conserver un apprentissage dans la Mémoire |

La progression ne mesure pas le nombre de messages. Elle vérifie la réalisation de gestes et objets
explicites : Résonance, intention, décision, action et trace de Mémoire.

### 9.4. Phase 4 — Rôles tournants

Les cinq gardiens de l'autofacilitation peuvent disposer d'indications légères dans l'espace :

- le gardien du Relationnel observe circulation de la parole, accueil et tensions ;
- le gardien du Sens rappelle l'intention et aide à relier les récits ;
- le gardien de la Gouvernance aide à expliciter propositions, consentements et responsabilités ;
- le gardien de l'Opérationnel veille aux actions, moyens, rythmes et échéances ;
- le gardien de l'Apprenance aide à formuler retours et apprentissages.

Ils ne deviennent ni modérateurs absolus, ni propriétaires des messages. Le rôle principal peut être
soutenu par un binôme d'appui. Les rôles et leurs droits effectifs doivent rester distincts.

### 9.5. Phase 5 — Du Cercle au projet

Lorsque les gestes fondamentaux sont acquis, le Cercle ouvre ou rejoint une petite Mission. Le
parcours rend explicite :

> **Le Cercle nous aide à grandir ensemble. Le Projet nous permet d'agir ensemble.**

Une proposition née dans le Cercle peut devenir une carte Projet ou Mission. La nouvelle équipe et
ses droits sont explicites ; l'ensemble de la conversation du Cercle n'est jamais copié dans le
Projet.

### 9.6. Aides contextuelles

Le Professeur Sirbey peut introduire les règles, droits et outils. Le Docteur Z.E.R.O. peut révéler
avec humour les contradictions habituelles : parler sans décider, décider sans attribuer, agir sans
apprendre ou accumuler des groupes morts.

Les aides doivent être :

- brèves ;
- déclenchées lors du premier geste ;
- refermables ;
- disponibles à nouveau ;
- fondées sur l'état observable de l'espace, jamais sur un diagnostic psychologique.

## 10. Passages entre espaces

Un objet peut circuler sans déplacer automatiquement toute la conversation :

- un message devient proposition de Projet ;
- une Graine est partagée avec un Cercle ;
- une action du Cercle rejoint une Mission ;
- une décision d'un Projet est publiée au Commun ;
- un apprentissage est proposé à la Ressourcerie ;
- une actualité ouvre un fil de discussion ;
- une tension ouvre un espace sensible temporaire.

Chaque passage affiche :

- objet déplacé ou référencé ;
- contexte source et destination ;
- auteur de l'action ;
- lecteurs supplémentaires ;
- consentement éventuel ;
- lien retour vers la source lorsque les droits le permettent.

## 11. Modèle conceptuel

Les noms exacts restent à déterminer après audit :

```text
DiscussionSpace
├── kind / template
├── context polymorphe
├── purpose
├── authority / mandate
├── lifecycle et retention policy
├── visibility / join / publication policies
├── memberships et rôles
└── ConversationThread
    ├── intention
    ├── participants additionnels éventuels
    ├── messages et réponses
    ├── structured references
    └── état ouvert / clos / archivé
```

Invariants :

- `kind` ne suffit jamais à autoriser l'accès ;
- les participants explicites restent la base des espaces privés ;
- l'intention du fil n'est pas une nouvelle classe d'espace ;
- les objets métier gardent leurs propres états ;
- changer de gabarit exige une transition historisée ;
- l'archivage ne détruit ni décision, ni consentement, ni preuve ;
- la recherche respecte les mêmes droits que l'affichage direct.

## 12. Critères d'acceptation

1. Un joueur comprend la différence entre espace et fil sans vocabulaire technique.
2. Créer un espace commence par une finalité, pas par une liste de canaux.
3. Le Cercle de croissance et le Cercle fonctionnel ont des finalités et cycles de vie distincts.
4. Une spécialisation ponctuelle du Cercle ne crée pas automatiquement un nouvel espace permanent.
5. `Actus PZ` sépare publication officielle et discussions associées.
6. `Bienvenue` permet accueil et questions sans exposer les conversations privées.
7. Un Projet peut être clos et produire une Mémoire sans rester dans la boîte active.
8. Une Consultation clôturée conserve un dossier auditable.
9. Les droits de voir, lire, rejoindre, publier, inviter et administrer sont distincts.
10. Tout espace indique finalité, lecteurs, gardien et temporalité.
11. Les groupes informels inactifs sont proposés à l'archivage sans suppression automatique.
12. Au Monde 1, le joueur pratique les cinq gestes sans être récompensé pour le volume de messages.
13. Les cinq rôles tournants assistent le cadre sans devenir propriétaires du contenu.
14. Une transition Cercle → Projet ne copie aucune conversation privée implicitement.
15. L'accueil priorise engagements et décisions plutôt que le seul nombre de non-lus.
16. Toutes les surfaces restent utilisables sur mobile et au clavier.

## 13. Lots recommandés

### S0 — Audit et modèle de droits

- relever les espaces et conteneurs réellement présents dans `pointzero-app` ;
- cartographier conversations privées, Cercles, événements, projets et annonces existants ;
- vérifier participants, lecteurs, recherche, notifications et suppressions ;
- proposer le modèle minimal de `DiscussionSpace` ou équivalent ;
- produire les tests d'isolation négatifs.

### S1 — Gabarits fondamentaux

- échange individuel ;
- groupe informel ;
- Cercle de croissance ;
- publication communautaire ;
- accueil Monde 1 ;
- navigation organisée par engagements.

### S2 — Action et apprentissage

- Projet ou Mission ;
- Cohorte ;
- vues Mouvements et Mémoire ;
- transitions explicites entre objets et espaces ;
- parcours des cinq gestes du Monde 1.

### S3 — Gouvernance et fonctions

- Cercle fonctionnel ;
- Consultation ;
- espace sensible temporaire ;
- mandats, clôture et audit ;
- protocoles avancés prévus dans la vision cible.

Les lots S0 à S3 doivent être articulés avec les étapes A à C de la vision cible. Ils ne constituent
pas quatre demandes de développement immédiates.

## 14. Questions ouvertes

- Taille maximale et durée par défaut des groupes informels ?
- Les conversations directes libres sont-elles accessibles dès le Monde 0, le Monde 1 ou selon un
  consentement de contact ?
- Qui peut transformer un groupe informel en Projet ou Cohorte ?
- Un Cercle fonctionnel possède-t-il toujours un mandat formel et une organisation de rattachement ?
- Quels espaces sont automatiquement rejoints à l'entrée dans un Monde ou une communauté ?
- Qui valide la Mémoire d'un espace communautaire ou fonctionnel ?
- Les espaces territoriaux sont-ils créés par seuil d'activité, sur demande ou par mandat ?
- Quel contenu d'un cycle de Cercle reste visible aux membres qui partent ou arrivent ensuite ?
- Comment nommer les cinq rôles numériques sans les réduire à des fonctions de modération ?

Ces arbitrages doivent être prototypés avec un Cercle pilote et une équipe projet réelle.
