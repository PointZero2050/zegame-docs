# Dialogue avec le mentor — UX cible

*Arbitrage Boris, 20 août 2026. Maquette de référence :
`zegame-prototypes/mentor-dialogue-cible/`.*

## Décision

Le dialogue avec le mentor devient un **journal continu du Voyage**. Le joueur voit tous ses
échanges dans un même fil, organisé chronologiquement et ponctué par les expériences ou chapitres
qui leur donnent contexte. Le profil du mentor est réduit à un bandeau compact : la conversation
est l'objet principal de la page.

Ce modèle se distingue de celui des Guides. Les Guides peuvent porter plusieurs conversations
thématiques sur l'application et le corpus Point Zéro. Le mentor relie dans le temps ce que le
joueur vit, comprend et transforme : fragmenter cette relation en fils indépendants ferait perdre
la continuité pédagogique.

## Classement des échanges

Le système ne déduit pas seul la thématique principale. Avant d'écrire, le joueur choisit dans un
menu déroulant ce qu'il veut explorer :

1. `Graine` — valeur sélectionnée par défaut ;
2. `Voyage` ;
3. `Moteur` ;
4. `Autre`.

Ce choix qualifie le nouvel échange. L'application peut lui associer les identifiants de contexte
déjà connus (parcours, expérience, Graine ou Trace depuis laquelle le dialogue a été ouvert), mais
un LLM ne remplace jamais le choix explicite du joueur pour la catégorie principale.

## Composants de la page

- bandeau compact : portrait, mentor actuel, Puissance principale et deux Puissances d'appui,
  accès à la fiche du héros ;
- fil complet avec séparateurs d'expériences et de chapitres ;
- messages du joueur et du mentor clairement différenciés ;
- thématique choisie affichée au niveau du message ; une source précise (`Trace`, expérience,
  Graine) n'apparaît que lorsqu'un véritable contexte d'ouverture la transmet ou que le mentor
  l'a effectivement relue ;
- menu `Graine / Voyage / Moteur / Autre` avant la saisie ;
- composeur persistant et auto-extensible ;
- panneau repliable `Sources et mémoire`, converti en tiroir sur mobile ;
- proposition de Graine directement dans le fil, toujours relue et confirmée par le joueur.

## Mémoire et consentement

Le consentement reste initial et contrôlable à la demande, sans rappel intrusif à chaque message.
Le panneau indique les catégories effectivement disponibles pour le mentor : expériences, Graines,
Traces et état du Moteur au Monde 0 ; les données de Cercle restent fermées tant que la fonction
n'existe pas. Les règles de fond restent celles de
[`analyse-impact-personnalisation-memoires.md`](analyse-impact-personnalisation-memoires.md).

## États à porter

1. première visite : aide concise et rappel du contrôle des sources ;
2. fil vide : première question reliée au héros choisi et, si elle existe, à l'expérience active ;
3. fil courant : messages, contexte choisi et sources citées ;
4. Graine possible : proposition éditable, jamais enregistrée automatiquement ;
5. changement de mentor : nouveau chapitre narratif, historique précédent conservé ;
6. fil long : navigation par repères d'expérience, sans casser le journal en conversations
   indépendantes.

## Contrat d'intégration

La maquette ne définit ni modèle de données ni callback. Avant portage Rails, vérifier la source de
vérité des messages du mentor, l'identifiant de contexte disponible à l'ouverture, les droits de
lecture par catégorie et le mécanisme réel de création d'une Graine. Aucun bouton de la maquette ne
doit valider une expérience, attribuer un Oméga ou publier une Graine sans passer par le service et
les droits existants.

### État réel confirmé le 20 août 2026

L'analyse d'impact du portable confirme que `MentorMessage` fournit déjà un fil unique, continu et
ordonné par joueur. Le portage ne demande donc pas une nouvelle architecture de conversation.

Les ajouts recommandés sont limités à :

- une catégorie explicite sur le message du joueur, avec `graine` comme valeur par défaut ;
- la catégorie héritée par la réponse du mentor ;
- un instantané durable des sources réellement utilisées par chaque réponse ;
- un rôle non conversationnel `chapitre` lors d'un changement de mentor, exclu des messages
  transmis au modèle.

Aucun contexte polymorphe d'ouverture n'est créé tant qu'une page réelle n'ouvre pas le mentor en
transmettant ce contexte. La référence technique complète est
[`analyse-impact-dialogue-mentor.md`](analyse-impact-dialogue-mentor.md).

### Arbitrage encore ouvert

Une Graine confirmée depuis un dialogue mentor entrerait aujourd'hui dans le régime général
opt-out de la Fresque et serait donc visible sur le profil communautaire. Son origine potentiellement
intime appelle une décision explicite : conserver cette règle en l'annonçant au moment de planter,
ou rendre privée par défaut une Graine née du mentor.
