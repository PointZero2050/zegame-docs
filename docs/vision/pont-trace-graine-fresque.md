# Le pont Trace → Graine, et le Miroir de la Fresque

*Écrit le 16 août 2026 par l'instance poste fixe, au portage de
`fresque-recit-m0-cible`. **Arbitré par Boris le 16 août au soir** — les décisions
sont intégrées ci-dessous et remplacent les questions ouvertes de la première
version. Destinataire : l'instance portable (modèles, services, contrôleurs).*

## Le constat d'origine

La maquette de la Fresque et le code divergeaient sur ce qu'**est** une Graine.

| | Maquette | Code (`app/services/graine.rb`, vague C, 16 août) |
|---|---|---|
| Origine | le rituel des 4 questions | un message écrit dans le fil d'une expérience |
| Nature | un objet stocké, éditable | une **lecture**, sans table |

## Ce que Boris a tranché

### 1. La Fresque CRÉE des Graines — c'est bien son rôle

« Planter ma première Graine » doit **produire une Graine**, pas une Trace. Le libellé
était juste ; c'est l'implémentation qui ne l'était pas encore.

- **La première Graine** naît des **quatre questions** du rituel (déjà portées).
- **Les suivantes** naissent d'un **champ de saisie libre**.

### 2. Une Trace ne devient PAS une Graine depuis la page Traces

Le pont n'existe pas comme geste d'interface. La conversion se fait **pédagogiquement**,
par le dialogue avec le mentor à l'intérieur des parcours. La page Traces reste une
relecture ; elle ne propose aucune transformation.

### 3. Option souhaitée — récolter la Graine en fin de chapitre

À la fin d'un dialogue avec un mentor, en clôture de chapitre : le mentor propose
**« Veux-tu que je publie cette Graine pour toi ? »**. Si le joueur accepte, il est
basculé vers la **page d'édition de la Graine**, celle-ci étant déjà publiée.

Statut : *souhaité, si possible*. Ce n'est pas un bloquant pour la V1 de la Fresque.

### 4. Le Miroir V1 : pas de LLM

**Décision révisée.** L'arbitrage précédent (les trois formulations demandées au mentor)
est **abandonné pour la V1** : passer par le mentor complique l'ensemble. La V1 garde
**des champs libres remplis par le joueur** pour produire la Graine initiale — c'est-à-dire
exactement ce qui est déjà porté. L'écran des trois propositions n'a donc pas lieu d'être
pour l'instant.

## Ce que cela demande au portable

L'identité canonique n'est **pas** remise en cause : une Graine reste un message écrit par
le joueur dans le fil d'une de ses expériences. Ce qui change, c'est qu'un **second point
d'entrée** doit pouvoir en créer une — la Fresque.

Questions de modèle, hors zone du poste fixe :

1. **À quel fil rattacher une Graine née dans la Fresque ?** Les Graines existantes vivent
   dans le fil d'un `ChallengesUser`. La première Graine du rituel n'est liée à aucune
   expérience. Trois pistes : la rattacher à l'expérience courante du joueur ; créer un
   conteneur d'un nouveau type (`Graine.CONTENEUR` prévoit explicitement ce cas — « Si un
   second conteneur apparaît, il s'ajoute ICI, une seule fois ») ; ou introduire un fil
   « Fresque » propre au joueur.
2. **L'écriture** : la Fresque devient un point de création, alors que `Graine` est
   aujourd'hui un service de **lecture** seule.
3. **Une page d'édition de Graine** est nécessaire pour le point 3 ci-dessus (route +
   action), et servira aussi à la saisie libre des Graines suivantes.

## Ce que le poste fixe fera ensuite

Porter la vue une fois le mécanisme disponible : le champ de saisie libre, la page
d'édition, et le remplacement de l'actuel `POST /fresque/bifurquer` (qui crée une Trace)
par la création d'une Graine. Le banc `verifier_fresque` devra suivre dans la même
livraison — il asserte aujourd'hui que la page **n'invente aucune Graine**, ce qui cessera
d'être vrai, et c'est voulu.
