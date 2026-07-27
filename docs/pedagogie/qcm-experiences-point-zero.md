# QCM d'expérience — spécification V1 et pilote « Le site du Point Zéro »

> Ajout Codex - 2026-07-27. Spécification fonctionnelle et technique validée dans son principe
> par Boris. Elle est destinée à Claude pour cadrer l'implémentation. Aucun code applicatif ni
> serveur n'a été modifié par cette décision.

## 1. Décision

Point Zéro peut proposer des QCM dans certaines expériences, à condition de ne pas les réduire à
des contrôles scolaires de mémorisation.

Le QCM sert trois fonctions possibles :

| Famille | Fonction | Mode de reconnaissance |
|---|---|---|
| Repérage | Vérifier un acquis objectif nécessaire pour agir | Seuil explicite, feedback et nouvelles tentatives |
| Discernement | Comparer plusieurs lectures plausibles d'une situation | Traversée complète, sans score de conscience |
| Cartographie | Relier ressources, acteurs, besoins, Puissances ou gestes | Production d'une carte ou d'une trace |

Le premier pilote est l'expérience obligatoire **Le site du Point Zéro**, actuellement annoncée à
9 Ω dans le Monde 0. Elle devient une enquête active et une mini-cartographie de la constellation,
pas un questionnaire sur l'arborescence ou le vocabulaire du site.

## 2. Principes pédagogiques non négociables

1. Une question part autant que possible d'une situation, d'un indice ou d'une décision concrète.
2. Les distracteurs restent plausibles ; une réponse juste ne fait pas face à trois caricatures.
3. Chaque choix évalué reçoit une explication : ce qu'il permet de voir et ce qu'il laisse de côté.
4. Plusieurs réponses peuvent être recevables lorsque la situation l'exige.
5. Les tentatives sont sans chronomètre, classement, humiliation ni perte d'Oméga.
6. Un résultat ne devient jamais un profil psychologique, politique ou un « niveau de conscience ».
7. Les Oméga reconnaissent la traversée ou un acquis démontré, jamais chaque bonne réponse.
8. Une IA peut proposer des questions ou un feedback formatif ; elle n'est pas seule juge d'une
   production personnelle, relationnelle ou sensible.
9. Le joueur sait avant de commencer comment le passage sera reconnu.
10. Un QCM formatif privilégie une reprise ciblée et expliquée plutôt qu'un échec global.

La voix reste adulte et légèrement décalée. Employer `À revoir` ou une explication située plutôt
que `Mauvaise réponse`.

## 3. Périmètre V1

### Inclus

- un moteur minimal réutilisable par plusieurs expériences ;
- définitions éditoriales versionnées en YAML ;
- choix unique, choix multiple et réponse courte ;
- feedback par option et débrief par question ;
- tentative persistée et reprenable ;
- deux politiques : `traversed` et `threshold` ;
- restitution déterministe ;
- validation système idempotente de l'expérience ;
- intégration avec `ExperienceState` et le CTA de prochaine action ;
- pilote complet « Le site du Point Zéro ».

### Hors périmètre

- éditeur visuel dans l'administration ;
- branchements conditionnels arbitraires ;
- banque aléatoire de questions ;
- chronomètre, classement ou compétition ;
- génération dynamique par IA en production ;
- analyse psychométrique ;
- correction sémantique automatique des réponses libres ;
- moteur générique de preuves ET/OU ;
- publication automatique de la Carte de constellation ;
- refonte globale de `Challenge`, `ChallengesUser` ou de l'attribution des points.

## 4. Pilote — fonction de l'expérience

L'expérience fait passer le joueur de la consultation d'un site à la reconnaissance d'un
écosystème : pensées, pratiques, Chrysalides, personnes, Cercles et événements peuvent entrer en
résonance avec son Appel.

Objectif observable :

> Repérer au moins deux ressources ou acteurs de natures différentes, qualifier le lien possible
> avec son Appel et choisir, ou différer consciemment, un premier geste relationnel.

La durée cible doit être vérifiée avec le contenu réel du site. Elle ne reste pas artificiellement
fixée à 45 minutes si le nouveau parcours peut être traversé en 12 à 20 minutes.

## 5. Parcours UX du pilote

### États et CTA

| État | Indication | CTA principal | Action secondaire |
|---|---|---|---|
| Non commencé | Étape 1 sur 2 · Explorer | `Explorer le site du Point Zéro` | `Comprendre la mission` |
| Tentative créée | Étape 2 sur 2 · Relier | `Composer ma constellation` | `Rouvrir le site` |
| En cours | Cartographie en cours | `Reprendre ma constellation` | `Rouvrir le site` |
| Réponses complètes | Ta carte est prête | `Produire ma Carte de constellation` | `Modifier mes choix` |
| Validé | 9 Ω gagnés | `Voir ma Carte de constellation` | `Continuer le parcours` |

Le lien vers le site s'ouvre dans un nouvel onglet ou une nouvelle fenêtre clairement annoncée.
La tentative commence sur l'écran de mission, pas au simple chargement de la fiche détaillée.

### Écran 0 — La mission

> Le site du Point Zéro n'est pas un texte sacré à réciter — l'humanité dispose déjà d'un stock
> raisonnable de textes sacrés et de mots de passe oubliés.
>
> Explore-le comme un territoire. Cherche au moins deux ressources ou acteurs de natures
> différentes qui pourraient éclairer, déplacer ou soutenir ton Appel.

Actions :

- `Explorer le site` ;
- `J'ai commencé mon exploration` ;
- `Reprendre plus tard`.

Le bouton d'exploration n'est pas une preuve de lecture et ne valide rien.

### Écran 1 — Deux repères dans la constellation

Le joueur renseigne deux repères. Pour chacun :

- nom ou titre court, obligatoire ;
- lien facultatif ;
- catégorie obligatoire :
  - pensée ou ressource ;
  - pratique ;
  - Chrysalide ou projet ;
  - personne ou expert ;
  - Cercle ;
  - événement.

Les deux catégories doivent être différentes. Le système ne prétend pas vérifier automatiquement
que le contenu externe a réellement été consulté. Il vérifie seulement que la trace demandée est
complète et cohérente.

Microcopy :

> Deux repères différents suffisent. Il ne s'agit pas de reconstituer Internet avant le déjeuner.

### Écran 2 — La nature du lien

Question à choix multiples :

> En quoi ces découvertes pourraient-elles entrer en relation avec ton Appel ?

- elles mettent des mots sur une intuition ;
- elles offrent une pratique à expérimenter ;
- elles montrent une réalisation concrète ;
- elles apportent une polarité ou une lecture qui me manque ;
- elles ouvrent une relation possible ;
- je ne sais pas encore, mais quelque chose résonne.

Au moins un choix est requis. Aucun choix n'est scoré.

### Écran 3 — Le langage de l'autre

Question de discernement :

> Un projet semble poursuivre une intention proche de la tienne, mais utilise un langage très
> différent. Quel premier mouvement paraît le plus fécond ?

1. `L'écarter : il ne partage probablement pas la même vision.`
2. `L'adopter : l'intention commune suffit.`
3. `Identifier ce qui résonne, ce qui diffère et ce qui reste à éprouver.`
4. `Lui demander d'adopter d'abord le vocabulaire du Point Zéro.`

Feedbacks :

- **1 — protection de la cohérence** : ce mouvement évite la confusion, mais peut transformer une
  différence de langage en incompatibilité de fond avant toute rencontre ;
- **2 — accueil de la proximité** : ce mouvement reconnaît l'élan commun, mais risque d'effacer des
  divergences réelles et leurs conséquences ;
- **3 — circulation recommandée** : ce mouvement conserve la résonance et la différence comme deux
  informations utiles ; il ne garantit pas l'accord, mais permet de l'éprouver ;
- **4 — langage commun imposé** : ce mouvement cherche à faciliter la coordination, mais peut faire
  du vocabulaire Point Zéro un nouveau récit hégémonique.

La réponse 3 est la réponse de référence pour un futur QCM à seuil. Dans ce pilote formatif, les
quatre choix permettent de poursuivre après lecture du feedback. Ils ne génèrent aucun score
politique ou moral.

### Écran 4 — Rendre le lien possible

Question à choix unique :

> Quel geste pourrait transformer l'un de ces repères en relation ?

- conserver la ressource ;
- expérimenter une pratique ;
- contacter une personne ;
- demander une mise en relation ;
- rejoindre un événement ;
- partager la découverte à un destinataire choisi ;
- aucun geste pour l'instant.

`Aucun geste pour l'instant` reste une réponse valide. Point Zéro ne force ni exposition publique,
ni prise de contact, ni publication sur un réseau social.

### Écran 5 — Carte de constellation

La restitution est déterministe et privée par défaut :

> **Deux repères sont entrés dans ta constellation.**
>
> `[Repère 1]` t'apporte `[nature du lien choisie]`.
> `[Repère 2]` ouvre `[nature du lien choisie]`.
>
> Ton prochain geste possible : `[geste choisi]`.
>
> Une constellation ne te demande pas d'être d'accord avec toutes ses étoiles. Elle commence
> lorsqu'elles deviennent assez visibles pour que tu puisses choisir un lien.

Actions :

- `Conserver cette carte` ;
- `Modifier mes choix` ;
- `Continuer le parcours`.

La V1 conserve la carte dans la tentative privée. Elle ne la publie pas dans un fil, un Profil ou
une communauté. Un futur rattachement à une Graine de relation exige un consentement séparé.

## 6. Règle de validation du pilote

La politique est `traversed`, pas `threshold`.

L'expérience est achevée lorsque :

1. deux repères nommés ont été enregistrés ;
2. leurs catégories sont différentes ;
3. au moins une nature de lien a été choisie ;
4. la question de discernement a été soumise et son feedback rendu disponible ;
5. un geste, y compris `aucun geste pour l'instant`, a été choisi ;
6. la Carte de constellation a été produite par une action explicite du joueur.

À cet instant seulement :

- la tentative reçoit `completed_at` ;
- le mécanisme de validation système existant est appelé une seule fois ;
- la `ChallengesUser` correspondante est validée selon le chemin métier existant ;
- les 9 Ω sont attribués une seule fois ;
- `ExperienceState` devient `validated`.

Une simple ouverture du site, de la fiche ou du QCM ne valide rien.

## 7. Architecture technique recommandée

### 7.1. Principe

Créer un petit moteur indépendant des modèles sensibles, puis raccorder sa complétion au mécanisme
de validation déjà utilisé par les sessions Point Zéro.

Ne pas ajouter de callback de points dans le nouveau modèle. Ne pas appeler directement
`gain_points`. Réutiliser le chemin idempotent existant après inspection de
`validate_marelle_experience!`, `ChallengesUser#set_validated_at` et de leurs callbacks dans
`mathieu_core`.

### 7.2. Définition YAML

Emplacement proposé :

`config/experience_quizzes/le-site-point-zero-v1.yml`

Structure indicative :

```yaml
key: le-site-point-zero
version: 1
challenge_slug: le-site-du-point-zero
completion_policy: traversed
evaluator: site_point_zero

questions:
  - id: repere_1_nom
    type: short_text
    required: true
  - id: repere_1_categorie
    type: single_choice
    required: true
    options: []
  - id: repere_2_nom
    type: short_text
    required: true
  - id: repere_2_categorie
    type: single_choice
    required: true
    options: []
  - id: liens
    type: multiple_choice
    min_selections: 1
    options: []
  - id: langage_autre
    type: single_choice
    required: true
    options: []
  - id: prochain_geste
    type: single_choice
    required: true
    options: []
```

Les textes, options, feedbacks et fragments de restitution vivent dans le YAML. Les règles propres
à la constellation — catégories différentes et construction du résultat — restent dans un
évaluateur dédié, par exemple `ExperienceQuizzes::SitePointZeroEvaluator`.

Le chargeur sélectionne la version la plus récente pour une nouvelle tentative et conserve les
anciens fichiers tant qu'une tentative peut encore les référencer. Une nouvelle version ne remplace
donc pas physiquement la précédente.

Ne pas créer dès la V1 un DSL générique capable d'exprimer toute logique conditionnelle. Extraire
une règle seulement lorsqu'une seconde expérience démontre qu'elle se répète.

Le chargeur valide au boot ou par une tâche dédiée :

- unicité des identifiants de questions et d'options ;
- présence des feedbacks requis ;
- types autorisés ;
- cohérence de la politique de complétion ;
- version positive ;
- existence du Challenge ciblé, au minimum lors du contrôle de déploiement.

### 7.3. Tentative persistée

Créer une table séparée, nom indicatif `experience_quiz_attempts`, afin de ne pas densifier
`ChallengesUser` :

| Champ | Rôle |
|---|---|
| `user_id` | Joueur authentifié |
| `challenge_id` | Expérience concernée |
| `quiz_key` | Définition utilisée |
| `definition_version` | Version figée au début de la tentative |
| `status` | `draft`, `completed` ou `passed` |
| `answers` JSONB | Réponses par identifiant stable |
| `result` JSONB | Restitution déterministe et références conservées |
| `score` nullable | Réservé aux politiques `threshold` |
| `completed_at` | Traversée terminée |
| `passed_at` | Seuil atteint, le cas échéant |
| timestamps | Audit minimal |

Prévoir les index usuels sur utilisateur, Challenge, clé et statut. Plusieurs tentatives peuvent
exister ; une seule tentative `draft` est reprise pour un même utilisateur, Challenge, clé et
version. Claude doit choisir et tester la contrainte compatible PostgreSQL plutôt que laisser la
concurrence créer deux brouillons.

Le modèle n'a aucun callback vers les points ou la progression.

### 7.4. Services et contrôleur

Découpage indicatif, à adapter après lecture du code actuel :

- `ExperienceQuizDefinition` — charge et valide le YAML ;
- `ExperienceQuizAttempt` — persistance sans effet secondaire métier ;
- `ExperienceQuizEvaluator` — normalise, vérifie et construit feedback/résultat ;
- `ExperienceQuizzes::SitePointZeroEvaluator` — règles et restitution du pilote ;
- `ExperienceQuizCompletion` — transaction idempotente vers la validation existante ;
- contrôleur fin exposant mission, questionnaire, sauvegarde et résultat ;
- vues HAML réutilisables pour choix unique, multiple, texte court et feedback.

Les paramètres soumis sont filtrés à partir de la définition. Un identifiant d'option inventé par
le client est rejeté. Respecter la convention applicative `reponses[...]`, pas `answers[...]`, sauf
si l'audit du nouveau contrôleur démontre qu'un namespace isolé est préférable et sans ambiguïté.

### 7.5. Intégration avec `ExperienceState`

L'adaptateur devient générique lorsqu'un QCM est configuré pour le Challenge :

| Trace | État |
|---|---|
| aucune tentative | `not_started` |
| tentative `draft` | `in_progress` |
| réponses requises complètes, carte non produite | `evidence_ready` |
| politique humaine future, demande envoyée | `submitted` |
| `ChallengesUser` validée | `validated` |

La validation déjà acquise dans `ChallengesUser` gagne toujours : elle ne doit jamais être annulée
par l'absence d'une tentative QCM, notamment pour les joueurs historiques.

### 7.6. Politique `threshold` pour les futurs QCM

Le moteur peut préparer, sans l'utiliser pour le pilote :

```yaml
completion_policy: threshold
passing_score: 80
```

Règles :

- seules les questions explicitement `graded` entrent dans le score ;
- le seuil est annoncé avant de commencer ;
- chaque tentative affiche les explications ;
- le joueur peut recommencer sans perdre de points ;
- l'événement de complétion n'est émis qu'au premier seuil atteint ;
- une nouvelle tentative après réussite sert à revoir, pas à recréer des Oméga.

Réserver ce mode aux acquis objectifs : sécurité, règles d'un rôle, fonctionnement vérifiable ou
prérequis. Ne pas l'utiliser pour mesurer une posture, une opinion ou une résonance.

## 8. Analyse d'impact obligatoire avant implémentation

### `Challenge`

- Identifier le Challenge par son slug réel ; ne pas supposer son id.
- Passer l'autorité du pilote à `systeme` seulement lorsque le QCM et son adaptateur sont déployés.
- Vérifier l'interaction avec `auto_validated`, dérivé de `validation_authority`.
- Ne pas ajouter de colonne `quiz_key` sans démontrer que le mapping YAML par slug est insuffisant.

### `ChallengesUser`, progression et Oméga

- Ne pas ajouter de callback dans `ChallengesUser`.
- Réutiliser la validation métier existante dans une transaction idempotente.
- Tester qu'un double POST, un rafraîchissement ou deux onglets n'attribuent jamais 18 Ω.
- Une expérience obligatoire non terminée continue de bloquer la suivante selon les règles du
  parcours linéaire.
- Une tentative ne vaut ni validation, ni accomplissement, ni Oméga avant la Carte finale.
- Revoir une Carte validée ne retire aucun point.
- Recommencer doit être distingué de revoir et suivre la règle actuelle de confirmation avant
  toute perte éventuelle.

### Joueurs historiques

- Conserver toutes les validations et tous les Oméga déjà acquis sur « Le site du Point Zéro ».
- Ne créer aucune tentative fictive rétroactive.
- Pour un joueur déjà validé, afficher `Voir la nouvelle enquête` ou `Voir ma constellation` selon
  ce qui existe, sans bloquer le parcours ni reprendre ses 9 Ω.
- Documenter explicitement le comportement retenu avant la migration ou le changement d'autorité.

### Données et confidentialité

- La Carte est privée par défaut.
- Ne pas publier automatiquement les liens, noms de personnes ou gestes choisis.
- Limiter les réponses courtes et les URLs à une taille raisonnable ; normaliser sans exécuter ni
  prévisualiser du HTML fourni par le joueur.
- Ne pas envoyer les réponses à un modèle d'IA dans la V1.
- Prévoir la suppression avec le compte selon la politique applicative.

### Versionnement

- Une tentative commencée reste liée à sa `definition_version`.
- Un changement éditorial mineur peut garder la version ; tout changement d'options, de correction,
  de seuil ou de règle de restitution incrémente la version.
- Ne jamais réévaluer silencieusement une ancienne tentative avec une nouvelle définition.

### Dépendances et serveur

- Lire les callbacks réels de `mathieu_core` avant de brancher la complétion.
- Faire un backup DB avant toute migration.
- Tout nouveau fichier Ruby chargé au boot exige un restart Puma.
- Après déploiement d'un YAML mémoïsé, effectuer les deux restarts prévus par la passation.
- Vérifier dans le navigateur intégré, authentifié, sur ordinateur et mobile.
- Toute écriture, migration ou déploiement sur `vibe.ze.game` exige l'autorisation explicite de
  Boris au moment de l'implémentation ; la présente demande autorise la spec, pas le déploiement.

## 9. Accessibilité et responsive

- formulaires utilisables entièrement au clavier ;
- `fieldset` et `legend` pour chaque question ;
- cases et radios portant un libellé complet ;
- feedback annoncé aux lecteurs d'écran ;
- aucune information portée uniquement par la couleur ;
- zones tactiles suffisantes à 390 px ;
- ordre logique conservé sans JavaScript ;
- sauvegarde et soumission fonctionnelles sans glisser-déposer ;
- lien externe annoncé ;
- focus placé sur le titre du feedback après soumission ;
- message d'erreur relié à la question concernée.

## 10. Critères d'acceptation du pilote

1. La fiche affiche `Explorer le site du Point Zéro` avant tout bouton de complétion déclarative.
2. Le joueur peut commencer, quitter et reprendre sans perdre ses réponses.
3. Deux repères nommés et de catégories différentes sont requis.
4. Les options soumises sont vérifiées côté serveur à partir de la définition versionnée.
5. Les quatre réponses à la question du langage donnent un feedback spécifique.
6. Aucun score, classement ou diagnostic de personnalité n'est affiché.
7. `Aucun geste pour l'instant` permet de terminer.
8. La Carte est déterministe, modifiable avant finalisation et privée par défaut.
9. Aucun Oméga n'est attribué avant la production explicite de la Carte.
10. La première complétion valide l'expérience et attribue exactement 9 Ω.
11. Les soumissions répétées n'ajoutent aucun point.
12. Les joueurs déjà validés conservent validation, progression et Oméga.
13. La suite du parcours se déverrouille selon les règles existantes après validation.
14. Le CTA et `ExperienceState` reflètent correctement chaque état.
15. Le parcours est utilisable au clavier, sur lecteur d'écran et à 390 px.
16. Les tests couvrent la définition YAML, l'évaluateur, la reprise, l'idempotence, les paramètres
    forgés, la concurrence de brouillons et la compatibilité historique.

## 11. Plan d'implémentation proposé à Claude

1. Auditer le Challenge réel, `ExperienceState`, les quatre sessions existantes,
   `validate_marelle_experience!`, `ChallengesUser` et les callbacks de `mathieu_core`.
2. Produire l'analyse d'impact finale et la liste exacte des fichiers avant édition.
3. Sauvegarder DB et code si Boris autorise ensuite l'implémentation serveur.
4. Créer la migration et le modèle de tentative sans callback métier.
5. Créer le chargeur/validateur YAML et les composants de formulaire accessibles.
6. Écrire l'évaluateur dédié et les textes du pilote.
7. Brancher `ExperienceState` et les CTA.
8. Brancher la complétion idempotente sur la validation existante.
9. Préserver explicitement le comportement des joueurs historiques.
10. Exécuter les tests, déployer après autorisation, redémarrer Puma et vérifier dans le navigateur.
11. Committer sous préfixe `[Claude]` et mettre à jour `PASSATION-CLAUDE.md`.

## 12. Définition de terminé

Le pilote est terminé lorsque le joueur peut explorer, reprendre, produire sa Carte, recevoir le
feedback, valider une seule fois les 9 Ω et continuer le parcours ; lorsque les validations
historiques restent intactes ; lorsque tous les critères d'accessibilité et d'idempotence sont
testés ; et lorsque la passation documente la migration, le backup, les commits et les vérifications
en ligne.

## 13. Références canoniques

- [Matrice de révision du Monde 0](monde-0-matrice-revision.md) — fonction et validation cible de
  l'expérience ;
- [Moteur de validation pédagogique](../vision/validation.md) — niveaux d'enjeu, preuves et
  idempotence ;
- [Parcours du Monde 1](../vision/monde-1-parcours.md) — grammaire `Voir → Manipuler → Relire` et
  principes des quiz formatifs ;
- [Cartes-couvertures et prochaines actions](../vision/cartes-experiences-freeride.md) — CTA,
  `ExperienceState` et séparation entre action, trace, validation et récompense ;
- [Voix Point Zéro](../vision/voix-point-zero.md) — ton éditorial et dosage de l'humour.
