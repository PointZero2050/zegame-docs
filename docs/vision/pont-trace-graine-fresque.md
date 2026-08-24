# Le pont Trace → Graine, et le Miroir de la Fresque

*Écrit le 16 août 2026 par l'instance poste fixe, au portage de
`fresque-recit-m0-cible`. **Arbitré par Boris le 16 août, puis révisé le 23 août**
après la traversée réelle de l'expérience `Et moi dans tout ça ?`. La révision du
23 août prévaut : la première Graine n'est plus un rituel générique de la Fresque,
mais la sortie contextualisée du premier chapitre. Destinataire : l'instance
portable (modèles, services, contrôleurs).*

## Le constat d'origine

La maquette de la Fresque et le code divergeaient sur ce qu'**est** une Graine.

| | Maquette | Code (`app/services/graine.rb`, vague C, 16 août) |
|---|---|---|
| Origine | le rituel des 4 questions | un message écrit dans le fil d'une expérience |
| Nature | un objet stocké, éditable | une **lecture**, sans table |

## Ce que Boris a tranché

### 1. La première Graine naît dans le parcours

L'expérience `Et moi dans tout ça ?` clôt le premier chapitre. Sa sortie est la
**Graine de l'Appel** : la première Graine réelle du Joueur.

Le questionnaire générique de première visite dans la Fresque est donc retiré. La
première visite de la Fresque explique le Voyage, les Graines et les Résonances ; elle
peut montrer un état vide, mais elle ne crée pas un objet concurrent avant la clôture
du chapitre.

Les quatre questions existantes restent utiles, mais deviennent le canevas contextuel
de la Graine de l'Appel :

1. Qu'est-ce qui s'est fissuré dans ta manière de voir le monde ?
2. Qu'est-ce qui t'appelle maintenant ?
3. Quelle croyance as-tu commencé à interroger ?
4. Quelle tension perçois-tu entre ton besoin et celui du système ?

Après cette première Graine, la Fresque peut accueillir des Graines libres ou les
Graines structurées produites à la clôture d'autres chapitres.

### 2. Une Trace ne devient PAS une Graine depuis la page Traces

Le pont n'existe pas comme geste d'interface. La conversion se fait **pédagogiquement**,
par le dialogue avec le mentor à l'intérieur des parcours. La page Traces reste une
relecture ; elle ne propose aucune transformation.

### 3. Règle canonique — récolter la Graine en fin de chapitre

À la fin du dialogue avec le mentor, le CTA ouvre la **page d'édition de la Graine**
dans le contexte de l'expérience de clôture. Le mentor propose une formulation ; le
Joueur la relit, la transforme et la confirme. Le mentor n'écrit ni ne publie à sa place.

La même mécanique sert les trois sorties du Monde 0 :

- chapitre 1 : **Graine de l'Appel** ;
- chapitre 2 : **Graine de relation** ;
- chapitre 3 : **Graine de passage**.

### 4. Un éditeur unique, quatre contextes

Il n'existe pas deux formulaires concurrents. Un seul éditeur de Graine reçoit un
contexte explicite : `appel`, `relation`, `passage` ou `libre`. Dans un parcours, il
affiche en permanence la provenance et le chemin de retour :

`Monde 0 · Chapitre 1 · Et moi dans tout ça ?`

Le brouillon est conservé. `Retour à l'expérience` ramène sans perdre la saisie.
Après `Planter dans ma Fresque`, la Graine est créée puis le Joueur revient
automatiquement à l'expérience, sur son bloc d'action.

### 5. Ce qui active Imagination

Le territoire **Imagination** s'active lorsque le Joueur a effectivement planté sa
première Graine canonique, quel que soit le conteneur technique de son fil. En Monde 0,
il s'agit normalement de la **Graine de l'Appel**, produite dans le fil
`ChallengesUser` de l'expérience `Et moi dans tout ça ?`.

Cette règle ne doit donc plus dépendre exclusivement d'une Graine attachée au fil
`User` de la Fresque. Elle doit reconnaître les Graines appartenant au Joueur dans les
conteneurs canoniques autorisés, dont `User` et `ChallengesUser`.

Trois états restent distincts :

- ouvrir la Fresque révèle son rôle et son état vide, sans activer Imagination ;
- planter la première Graine active Imagination ;
- produire une première Trace rend la page `Mes Traces` à explorer et incrémente le
  métaparcours, mais ne remplace pas la première Graine comme seuil d'activation.

L'invitation initiale de la carte devient donc **« Découvre ta Fresque de Récit »**.
Elle ouvre `/fresque`, qui annonce que la première Graine sera plantée à la clôture du
premier chapitre. Elle ne promet plus un formulaire générique sur cette page.

## Ce que cela demande au portable

L'identité canonique n'est **pas** remise en cause : une Graine reste un message écrit par
le Joueur dans le fil d'une de ses expériences. La clôture de chapitre fournit précisément
ce conteneur ; il n'est plus nécessaire d'inventer un fil technique pour la première Graine.

Contrat d'implémentation, hors zone du poste fixe :

1. **Provenance persistée** : parcours, chapitre et expérience de clôture ; la destination
   de retour est calculée côté serveur, pas fournie comme URL arbitraire par le client.
2. **Preuve** : seule la création effective de la Graine contextualisée accomplit le geste
   `Semer`. Ouvrir la Fresque ou l'éditeur ne valide rien.
3. **Retour de boucle** : après création, redirection vers la page de l'expérience et son
   ancre d'action. Le listener y constate la Graine attendue et révèle la suite.
4. **Idempotence** : recharger ou revenir depuis l'éditeur ne crée jamais une seconde Graine.
   Une Graine déjà plantée rouvre en lecture/édition selon les droits existants.
5. **Séparation Trace/Graine** : les réponses préparatoires et productions du chapitre
   restent des Traces ; seule la formulation confirmée devient Graine.
6. **Activation d'Imagination** : une Graine canonique appartenant au Joueur compte aussi
   lorsqu'elle vit dans un fil `ChallengesUser`. La Graine de l'Appel doit donc satisfaire
   le prédicat utilisé par `Monde0Etats`.
7. **Ordre de livraison** : modifier et tester ce prédicat avant de retirer le rituel de
   la Fresque. Traiter ensuite `POST /fresque/bifurquer` et le code serveur devenu mort,
   sans conserver une route qui créerait encore l'ancien objet concurrent.

## Ce que le poste fixe fera ensuite

Porter la page de clôture et l'éditeur une fois le mécanisme disponible. Les bancs doivent
vérifier ensemble : absence du questionnaire générique concurrent dans la Fresque, contexte
de chapitre visible, absence de validation à l'ouverture, création d'une seule Graine,
retour à l'expérience et accomplissement du geste seulement après preuve serveur.
