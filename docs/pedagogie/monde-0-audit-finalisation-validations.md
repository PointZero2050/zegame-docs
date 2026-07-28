# Monde 0 — audit de finalisation et validations manquantes

> **Ajout Codex — 2026-07-28.** Audit en lecture seule de la production `vibe.ze.game`,
> confronté à `origin/pointzero` au commit `916500d` et aux orientations pédagogiques déjà
> documentées. Ce document est une spécification de reprise pour Claude ; il n'atteste pas que les
> corrections proposées sont déjà déployées.

## 1. Résumé de décision

Le Monde 0 est structurellement en place : 14 expériences, 13 obligatoires, le Sas optionnel,
99 Ω au total dont 87 Ω obligatoires. Les mini-jeux, le QCM du Site PZ, la page de parcours, la
navigation verrouillée et les illustrations archétypales sont déployés.

La finalisation n'est cependant pas seulement éditoriale. Quatre expériences obligatoires ne
produisent encore aucune trace d'apprentissage propre :

- `Le Point Zéro : entrer dans le Jeu` : regarder une vidéo puis déclarer l'avoir fait ;
- `L'écosystème Point Zéro` : regarder une vidéo puis déclarer l'avoir fait ;
- `Le signe de reconnaissance` : poster publiquement une phrase codée sur LinkedIn puis le déclarer ;
- `Découvrir les formats` : regarder une vidéo puis le déclarer.

La cible proposée est :

| Expérience | Geste d'apprentissage | Trace produite | Validation |
|---|---|---|---|
| Le Point Zéro : entrer dans le Jeu | Reconstituer la chaîne crise → récits → polarisation → transformation intérieure | **Hypothèse de seuil** | Système, après contenu consommé et interaction terminée |
| L'écosystème Point Zéro | Relier des fragments de natures différentes et nommer ce qui circule | **Schéma de circulation** | Système, à la production explicite de la trace |
| Le signe de reconnaissance | Composer un signe relationnel juste, puis choisir librement son mode d'envoi | **Signe prêt à envoyer** | Système sur la production ; envoi réel facultatif et reconnu séparément |
| Découvrir les formats | Comparer, choisir ou différer consciemment un prochain passage | **Boussole de passage** | Système sur la trace ; inscription WordPress = preuve automatique alternative |

Le point commun n'est donc pas un QCM ajouté partout. Chaque expérience reçoit le CTA et la preuve
qui correspondent à sa nature.

## 2. État réel constaté en production

### 2.1. Écarts transversaux à corriger avant de déclarer le Monde 0 finalisé

1. **Onze fiches contiennent encore l'ancienne consigne `FEEDBACKS` et imposent ou suggèrent un
   partage à la communauté.** Elle doit disparaître de toutes les validations. Une Graine privée
   suffit aux fins de chapitre ; un partage est toujours un choix ultérieur.
2. **Trois mini-jeux à validation réellement automatique sont encore étiquetés
   `À confirmer par toi` en base** : `Une drôle d'époque`, `Avant le Zéro` et `Le Conseil Oméga`.
   Leur `validation_authority` doit devenir `systeme`. Le comportement est protégé par
   `ExperienceState`, mais le contrat affiché au joueur est faux.
3. **Une vidéo marquée principale rend immédiatement disponible `J'ai réalisé cette expérience`.**
   La reprise de lecture est locale au navigateur et ne constitue pas une preuve serveur. Pour les
   vidéos d'appel à faible enjeu, un événement de fin peut suffire ; pour les vidéos pédagogiques,
   il faut surtout une trace courte après la vidéo.
4. **Les trois fins de chapitre ne disposent pas encore d'une vraie Graine structurée.** L'UX
   vérifie seulement la présence d'au moins un message du joueur dans le fil avant d'autoriser la
   déclaration. Cela ne garantit ni proposition du mentor, ni édition, ni validation explicite de
   la Graine.
5. **Les textes de validation et les ressources ne reflètent pas toujours le mécanisme réellement
   déployé.** Exemples : ancien mini-jeu externe encore attaché à `Une drôle d'époque`, ancienne
   ressource externe attachée à `Avant le Zéro`, ancien questionnaire décrit sur la fiche du Site PZ.
6. **Inscription et participation sont encore confondues dans la fin du parcours.** Une inscription
   peut prouver un choix de format ; seule une présence, un check-in ou une confirmation humaine
   peut reconnaître le Sas ou l'Atelier vécu.

### 2.2. Revue des 14 expériences

| # | Expérience | État | Reste à faire |
|---:|---|---|---|
| 1 | Le Point Zéro : entrer dans le Jeu | Partiel | Produire la coda/transition vers le procès ; retirer `FEEDBACKS` ; ajouter le micro-passage `La chaîne invisible` après la vidéo. |
| 2 | Le Coupable idéal | Fonctionnel | Produire et intégrer `La crise de nos récits` ; porter la durée vers environ 17 min ; relire les dérives marquées `source: brouillon`. |
| 3 | Une drôle d'époque | Fonctionnel, métadonnées fausses | Passer l'autorité à `systeme` ; retirer l'ancien mini-jeu externe et les anciennes validations. |
| 4 | Avant le Zéro | Fonctionnel, métadonnées fausses | Passer l'autorité à `systeme` ; retirer la ressource historique et `FEEDBACKS`. |
| 5 | Et moi dans tout ça ? | Transition en place, Graine incomplète | Remplacer le simple message par le cycle mentor → proposition → édition → `Valider ma Graine de l'Appel`. |
| 6 | L'écosystème Point Zéro | À refondre | Remplacer le contenu réducteur site/Sas/LinkedIn, produire `La constellation`, ajouter le Schéma de circulation. |
| 7 | Le site du Point Zéro | Fonctionnel | Aligner le texte de validation sur l'enquête et la Carte de constellation ; supprimer l'ancien questionnaire et `FEEDBACKS`. |
| 8 | Le signe de reconnaissance | À refondre | Supprimer LinkedIn et la phrase-signal comme voie unique ; ajouter le compositeur de signe. |
| 9 | Les choses se précisent | Transition en place, Graine incomplète | Implémenter la Graine de relation structurée, privée par défaut. |
| 10 | Le Conseil Oméga | Fonctionnel, métadonnées fausses | Passer l'autorité à `systeme`. |
| 11 | Découvrir les formats | À refondre | Produire `La chaise vide` ou une vidéo dédiée aux formats ; ajouter Boussole, agenda réel et preuve d'inscription. |
| 12 | Le Sas d'entrée | Optionnel, preuve faible | Conserver optionnel ; à terme, valider la présence et non l'inscription. |
| 13 | Vivre l'Atelier Point Zéro | Bon principe | Conserver la validation facilitateur ; retirer `FEEDBACKS` ; vérifier le lien d'inscription et distinguer réservation/présence. |
| 14 | Mon récit de passage | Transition en place, Graine incomplète | Implémenter la Graine de passage structurée après l'Atelier, sans partage imposé. |

Restent aussi les textures propres aux trois chapitres sur la page du parcours. Elles sont
secondaires par rapport aux incohérences de validation et de contenu.

## 3. Expérience 1 — Le Point Zéro : entrer dans le Jeu

### 3.1. Acquis recherché

Comprendre l'hypothèse d'entrée du Point Zéro avant de la mettre à l'épreuve dans `Le Coupable
idéal` : les crises visibles forment un système, ce système est aussi soutenu par des récits devenus
inadaptés, les contre-récits peuvent recréer une polarisation symétrique, et le Point Zéro collectif
commence par une capacité individuelle à accueillir et faire circuler ses propres polarités.

Cette expérience ne doit ni produire un profil ni demander au joueur de désigner déjà son coupable.
Le Procès porte cette exploration. Ici, il s'agit seulement de vérifier que le seuil conceptuel a
été franchi.

### 3.2. Parcours UX — La chaîne invisible

1. CTA de couverture : `Regarder Bienvenue dans le Point Zéro`.
2. La vidéo reste l'objet principal, en grand format. La coda annoncée dans le fil rouge relie
   explicitement crise, récits, polarisation et transformation intérieure.
3. À la fin : `Recomposer le passage`.
4. Le joueur remet quatre cartes dans l'ordre :
   - `Les crises visibles forment un même système.`
   - `Nos récits collectifs ne correspondent plus entièrement au réel.`
   - `Le contraire absolutisé peut reproduire ce qu'il voulait dépasser.`
   - `Le Point Zéro collectif commence aussi par la circulation en chacun de nous.`
5. En cas d'ordre différent, pas de rouge ni d'échec : les cartes s'animent pour montrer la chaîne,
   avec une explication d'une phrase par articulation.
6. Question finale : `Quelle hypothèse acceptes-tu de garder ouverte pendant la traversée ?`
   Le joueur choisit l'une des quatre cartes ou `Je ne sais pas encore — je garde la question`.
7. Restitution légère : **Hypothèse de seuil**.
8. CTA de sortie : `Ouvrir l'audience du Coupable idéal`.

L'ensemble dure 45 à 90 secondes. Il sert de charnière entre la vidéo et le premier vrai format
interactif, sans créer un deuxième questionnaire ni répéter le Procès.

### 3.3. Condition de validation

```text
contenu consommé
ET chaîne recomposée ou révélée après une tentative
ET hypothèse de seuil choisie
```

`Contenu consommé` signifie :

- vidéo regardée à au moins 90 % en temps cumulé, mesuré côté lecteur puis enregistré sur le
  serveur ;
- **ou** transcription accessible ouverte, parcourue, puis même interaction terminée.

Le temps cumulé évite qu'un saut direct à la dernière seconde suffise. Cette mesure reste un indice
de visionnage, pas une prétendue preuve de compréhension ; la courte interaction porte la trace
d'apprentissage. En cas de blocage technique du lecteur ou d'un outil d'assistance, une action
`La vidéo ne fonctionne pas pour moi` doit ouvrir la transcription sans bloquer le parcours.

La validation est système, sans score et sans bonne opinion. Toute hypothèse finale, y compris
`Je ne sais pas encore`, est recevable. Revoir la vidéo ou refaire la chaîne ne retire ni n'ajoute
d'Ω.

## 4. Expérience 6 — L'écosystème Point Zéro

### 4.1. Acquis recherché

Comprendre que l'écosystème n'est ni un catalogue ni une communauté de plus, mais une mise en
circulation entre des fragments déjà actifs : pensées, pratiques, Chrysalides/projets, experts,
Cercles et événements.

Cette expérience apprend la **logique du lien**. L'expérience suivante, `Le site du Point Zéro`,
applique ensuite cette logique à des ressources et acteurs réels. Elles ne doivent pas produire
deux fois la même Carte de constellation.

### 4.2. Parcours UX

1. CTA de couverture : `Voir La constellation`.
2. À la fin de la vidéo : `Relier les fragments`.
3. Afficher les six familles sous forme de cartes ou d'astres.
4. Le joueur en choisit au moins trois et crée au moins deux liens.
5. Pour chaque lien, il choisit ce qui peut circuler : idée, pratique, expérience, relation,
   ressource, soutien ou autre.
6. Une question courte : `Qu'est-ce qui manquerait pour que cette constellation devienne vivante ?`
7. CTA final : `Produire mon Schéma de circulation`.

Il n'existe ni combinaison correcte unique ni score. Le feedback explique la fonction des liens
choisis et peut signaler une constellation très homogène : « Tu as relié trois fragments de même
nature. Que changerait l'arrivée d'une pratique, d'une personne ou d'un projet ? »

### 4.3. Condition de validation

Validation système lorsque la trace contient :

- au moins trois fragments ;
- au moins deux natures différentes ;
- au moins deux relations ;
- une circulation qualifiée ;
- une limite ou un manque nommé, y compris `Je ne sais pas encore`.

La validation reconnaît la construction de la carte, jamais une opinion particulière.

## 5. Expérience 8 — Le signe de reconnaissance

### 5.1. Acquis recherché

Passer d'une résonance intérieure à un geste relationnel qui reconnaît l'autre sans l'enrôler.
Le joueur apprend la différence entre :

- **reconnaître** : dire précisément ce qui a été reçu ;
- **résonner** : nommer ce que cela met en mouvement en soi ;
- **inviter** : ouvrir une possibilité sans fabriquer une dette ni exiger une réponse.

Le mot-clé secret et la publication LinkedIn obligatoire contredisent cet acquis : ils favorisent
le signal d'appartenance et l'exposition publique plutôt que la relation consentie.

### 5.2. Parcours UX

1. CTA : `Composer un signe`.
2. Choisir la situation : remercier l'auteur d'une ressource, contacter une personne, demander une
   mise en relation, répondre à un projet, inviter à un événement ou autre.
3. Composer le signe en trois blocs courts :
   - `Ce que j'ai reconnu…`
   - `Ce que cela met en mouvement chez moi…`
   - `La porte que j'ouvre, sans obligation…`
4. Vérification de justesse, sans IA juge : destinataire compréhensible, intention explicite,
   absence de phrase codée imposée, possibilité réelle de ne pas répondre.
5. Restitution : **Signe prêt à envoyer**.
6. Choix séparé : `L'envoyer maintenant`, `Le garder pour plus tard`, `Choisir un autre geste`.

Les canaux peuvent être un message privé, un e-mail, une mise en relation, un commentaire, une
inscription à un événement ou, plus tard, la messagerie ze.game. LinkedIn reste une possibilité,
jamais la norme.

### 5.3. Condition de validation

La production explicite du `Signe prêt à envoyer` valide l'apprentissage. L'envoi réel est une
trace d'action additionnelle : automatique pour un geste interne à ze.game, déclarative pour un
canal externe tant qu'aucun retour signé n'existe.

Ce découplage évite deux impasses : forcer une interaction publique pour obtenir 6 Ω, ou prétendre
que ze.game sait vérifier un message envoyé sur une plateforme tierce.

Ne pas conserver le nom, l'adresse ou le texte intégral du destinataire si cela n'est pas nécessaire.
Une version locale ou un brouillon privé chiffré est préférable ; la trace de validation peut se
limiter au type de geste et à sa date.

## 6. Expérience 11 — Découvrir les formats

### 6.1. Acquis recherché

Savoir choisir un **prochain passage adapté**, plutôt que mémoriser un catalogue. La fiche doit
répondre à quatre questions :

- Quelle intention est la mienne maintenant ?
- Quel degré d'immersion et de relation me convient ?
- Quelles contraintes réelles dois-je respecter ?
- Quel est mon prochain geste, y compris différer consciemment ?

### 6.2. Parcours UX — Boussole de passage

1. CTA vidéo : `Découvrir les façons d'entrer`.
2. CTA après vidéo : `Trouver mon prochain passage`.
3. Choisir une intention : comprendre, rencontrer, expérimenter, approfondir, transmettre.
4. Comparer les formats disponibles avec durée, modalité, intensité collective, prérequis,
   prochaine date et éventuel prix. La taxonomie éditoriale reste dans ze.game ; les dates et places
   viennent de WordPress.
5. Choisir un format, ou `Pas maintenant` en précisant la condition qui rendrait le passage juste.
6. Produire la **Boussole de passage** : intention, format envisagé, raison, prochain geste et date
   de réexamen éventuelle.
7. Si une date convient : `Voir les dates` puis `M'inscrire`.

La page WordPress expose déjà des événements à venir, leurs dates, leur modalité, la gratuité et
le nombre de places restantes. Elle utilise visiblement The Events Calendar / Event Tickets ;
l'API officielle propose des endpoints distincts pour les événements, les billets et les
participants. Le namespace et les droits réellement activés sur ce WordPress doivent encore être
confirmés avant développement.

### 6.3. Règle de validation recommandée

Deux preuves alternatives :

```text
Boussole de passage produite
OU
inscription WordPress confirmée et rattachée au joueur
```

Une inscription peut préremplir la Boussole et valider `Découvrir les formats`, car elle manifeste
un choix réel. Elle **ne valide jamais** `Le Sas d'entrée` ni `Vivre l'Atelier Point Zéro` : ces
expériences reconnaissent une présence ou une participation, pas une réservation.

Le choix `Pas maintenant` reste valide s'il produit une condition ou une date de réexamen. Rendre
l'inscription obligatoire bloquerait les joueurs quand aucune date, modalité, localisation ou
capacité financière ne leur convient, et transformerait une expérience d'orientation en tunnel de
conversion.

## 7. Intégration WordPress recommandée

### 7.1. Architecture cible

Préférer une intention signée et un retour événementiel à un rapprochement silencieux par e-mail :

```text
ze.game crée RegistrationIntent (jeton opaque, joueur, expérience, expiration)
    → redirection vers l'événement WordPress avec le jeton
    → WordPress conserve le jeton dans l'inscription
    → inscription confirmée
    → callback signé vers ze.game
    → preuve idempotente external_registration_confirmed
    → validation de Découvrir les formats si elle n'était pas déjà acquise
```

Le callback comporte au minimum : identifiant externe de l'inscription, identifiant de
l'événement, type de format, statut, horodatage, jeton d'intention, timestamp de signature et
signature HMAC. La clé reste côté serveur. Un index unique sur `(provider, external_id)` garantit
l'idempotence et empêche le rejeu.

Conformément à la règle déjà actée, une annulation ultérieure est enregistrée mais ne retire pas
les Ω acquis. Elle peut seulement modifier l'état opérationnel de l'inscription.

### 7.2. MVP et solutions de repli

| Niveau | Solution | Coût | Limite |
|---|---|---:|---|
| V0 | Boussole seule, lien sortant vers WordPress | Faible | Pas de preuve d'inscription |
| V1 | Synchronisation serveur authentifiée des participants Event Tickets | Moyen | Rapprochement par e-mail, délai, données personnelles |
| V2 recommandée | Jeton d'intention + callback signé | Moyen | Petit développement WordPress nécessaire |
| Repli | Code de confirmation à usage unique dans l'e-mail d'inscription | Faible à moyen | Une action manuelle de plus |

Pour un appel serveur à serveur, utiliser une Application Password WordPress dédiée, révocable et
limitée à l'intégration ; jamais le mot de passe principal ni un secret dans le navigateur. Les
données de participants de Event Tickets nécessitent une authentification et ne doivent pas être
rendues publiques.

Références techniques :

- [WordPress — authentification de l'API REST](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/)
- [WordPress — Application Passwords](https://developer.wordpress.org/advanced-administration/security/application-passwords/)
- [The Events Calendar / Event Tickets — REST API](https://theeventscalendar.com/knowledgebase/event-ticket-rest-api/)

## 8. Socle technique minimal dans ze.game

Ne pas construire maintenant tout le moteur universel de validation. Ajouter un socle réutilisable
pour ces trois expériences :

```text
ExperienceEvidence
  user_id
  challenge_id
  kind                threshold_hypothesis | ecosystem_map | recognition_sign | format_compass | external_registration
  status              draft | completed | confirmed | cancelled
  data                 JSONB minimal et versionné
  source               player | ze_game | wordpress
  external_id          nullable
  completed_at
  created_at / updated_at
```

Contraintes : unicité adaptée au type de preuve, schéma de données versionné, aucune donnée sensible
dans `data` sans nécessité, service de complétion idempotent. `ExperienceState` peut recevoir trois
adaptateurs supplémentaires dont `completed_check` interroge ces preuves.

La complétion doit appeler un service métier explicite, pas ajouter un nouveau callback dispersé
dans `Challenge` ou `ChallengesUser`. Ce service :

1. verrouille ou retrouve le `ChallengesUser` concerné ;
2. n'agit que si la preuve exigée est complète ;
3. pose `end_at` et `validated_at` selon l'autorité ;
4. attribue les Ω une seule fois ;
5. ne révoque jamais une validation acquise lors d'un rejeu, d'une édition ou d'une annulation.

## 9. Analyse d'impact obligatoire avant implémentation

Zones sensibles touchées : `Challenge`, `ChallengesUser`, progression du `Journey`, attribution des
points, `ExperienceState`, routes/contrôleurs des expériences et éventuel job de synchronisation.

Risques à tester :

- double attribution des Ω après répétition d'un callback WordPress ;
- création de plusieurs `ChallengesUser` pour un même joueur et une même expérience ;
- validation d'une expérience d'un autre parcours portant le même slug ;
- inscription annulée qui révoque à tort une validation acquise ;
- e-mail WordPress différent de l'e-mail ze.game ;
- événement supprimé, complet ou sans date disponible ;
- indisponibilité de WordPress qui bloque le parcours ;
- confusion entre `confirmed`, `attended` et `checked_in` ;
- exposition d'une liste de participants ou d'un secret API au navigateur ;
- CTA suivant débloqué avant que la transaction de validation soit terminée.

## 10. Ordre de réalisation proposé à Claude

### Lot A — cohérence immédiate, sans nouveau moteur

1. Corriger les autorités de validation des trois mini-jeux déjà automatiques.
2. Réécrire les blocs `Comment ce passage sera reconnu` des 14 fiches.
3. Supprimer toutes les consignes `FEEDBACKS` et les partages imposés.
4. Retirer ou remplacer les ressources historiques devenues fausses.
5. Aligner durées, CTA et textes sur les dispositifs réellement déployés.

### Lot B — quatre micro-expériences

1. Socle `ExperienceEvidence` et service idempotent.
2. Chaîne invisible et Hypothèse de seuil de la première expérience.
3. Schéma de circulation de l'écosystème.
4. Compositeur du signe de reconnaissance.
5. Boussole de passage, d'abord sans dépendance WordPress.
6. Tests unitaires, requêtes et parcours complet mobile.

### Lot C — WordPress

1. Spike en lecture seule : confirmer versions, namespaces REST, modèle Event Tickets, statuts et
   méthode actuelle d'inscription.
2. Arbitrer V1 synchronisée ou V2 callback signé.
3. Ajouter journal d'intégration, idempotence, reprise sur erreur et minimisation des données.
4. Tester inscription, doublon, annulation, événement complet et indisponibilité distante.

### Lot D — fils narratifs encore manquants

1. Produire et intégrer `La crise de nos récits`.
2. Produire `La constellation`.
3. Produire ou réaffecter `La chaise vide` à l'ouverture du chapitre 3.
4. Finaliser les trois Graines structurées et les textures de chapitre.

## 11. Critères d'acceptation globaux

- Chaque expérience obligatoire indique avant l'action ce qui sera fait, ce qui sera produit et
  comment le passage sera reconnu.
- Aucun joueur n'est obligé de publier, contacter un inconnu ou s'inscrire à un événement pour
  poursuivre le Monde 0.
- Aucun mini-jeu terminé n'est encore présenté comme une simple autovalidation.
- Aucune mention `FEEDBACKS` ne subsiste dans les 14 fiches.
- Les quatre nouvelles traces sont privées par défaut, consultables et rejouables.
- La première expérience ne peut plus être validée par un clic disponible avant la vidéo ; la
  transcription et l'interaction offrent une voie accessible équivalente.
- Le rejeu n'ajoute ni ne retire d'Ω.
- Une inscription WordPress valide au plus `Découvrir les formats` ; présence au Sas et à l'Atelier
  restent deux preuves distinctes.
- Une panne de WordPress ne bloque pas la production de la Boussole ni la progression.
- Les événements externes sont authentifiés, idempotents, auditables et minimisent les données
  personnelles.
