# Accueil avatar — amorces contextuelles et « Plus d’options »

Décision de Boris du 20 septembre 2026, à partir du banc
`/__banc/accueil-avatar.html`.

## Intention

L’accueil reste d’abord un dialogue avec l’Enfant intérieur. Les amorces visibles aident le joueur
à commencer, sans transformer l’avatar en menu exhaustif de l’application.

## Règle d’affichage

- Afficher au maximum **trois amorces fonctionnelles** dans le fil d’accueil.
- Tant que le joueur dispose de trois fonctionnalités accessibles ou moins, afficher toutes les
  amorces disponibles et ne pas montrer « Plus d’options ».
- Dès que **plus de trois fonctionnalités** sont réellement accessibles, afficher les trois
  amorces les plus pertinentes puis une quatrième entrée **Plus d’options**.
- « Plus d’options » n’est pas compté parmi les trois amorces.
- Le champ libre reste toujours disponible : « parler avec l’avatar » n’a pas besoin d’une amorce
  permanente et ne compte pas comme une fonctionnalité débloquée.

| Fonctionnalités accessibles | Rendu |
| --- | --- |
| 0 | Aucun bouton ; dialogue libre seulement |
| 1 à 3 | Toutes les amorces disponibles |
| 4 et plus | Trois amorces + « Plus d’options » |

## Sélection des trois amorces

La sélection doit venir des accès et de la progression réels, sans liste de huit boutons codée en
dur. L’ordre recommandé est :

1. une nouveauté ou action en attente réellement détectée ;
2. la reprise la plus pertinente dans le plan actuel, Materia ou Immateria ;
3. une autre fonction accessible utile dans le contexte présent.

À priorité égale, favoriser ce que le joueur n’a pas utilisé récemment. Une destination bloquée ou
non encore révélée ne doit jamais être proposée. Les fonctions possibles comprennent notamment le
parcours, Immateria, la Fresque, le mentor, les guides, les échanges et les ressources, mais la vue
doit lire le registre d’accès existant plutôt que reconstruire cette autorité.

## Interaction

- Une amorce formule une intention adressée à l’avatar. Elle déclenche sa réponse contextuelle ;
  cette réponse peut ensuite proposer le CTA vers la page concernée.
- « Plus d’options » déplie **dans le fil** les autres amorces accessibles. Éviter une modale ou une
  feuille basse, qui entrerait en concurrence avec le composeur fixe.
- Une fois ouvert, le contrôle devient **Moins d’options** et replie la liste.
- Les trois amorces prioritaires restent visibles quand la liste est dépliée.
- Si les accès changent au retour d’une page, recalculer la liste et ses priorités.

## Mobile, clavier et mouvement

- Le composeur reste fixe et la liste dépliée appartient à la zone défilante du fil.
- Le dépliage place le focus sur la première option supplémentaire ; le repli rend le focus au
  contrôle « Plus d’options ».
- Échap replie la liste sans quitter l’accueil.
- Exposer `aria-expanded` et relier le contrôle au conteneur des options supplémentaires.
- Ne pas ajouter d’animation indispensable ; respecter `prefers-reduced-motion`.

## Critères de recette

1. Avec trois fonctions accessibles, trois amorces sont visibles et aucun bouton supplémentaire.
2. Avec quatre fonctions, trois amorces et « Plus d’options » sont visibles.
3. Le dépliage montre seulement les fonctions restantes, sans doublon.
4. Une fonction verrouillée n’apparaît ni dans les trois choix ni dans la liste étendue.
5. Le clavier permet d’ouvrir, parcourir et replier la liste avec un focus prévisible.
6. Le composeur reste utilisable avec la liste ouverte, y compris après ouverture du clavier mobile.
7. Le rendu desktop et mobile repose sur la même collection de fonctions accessibles.

## Arbitrages Codex — 20 septembre 2026

### Libellés définitifs des onze destinations actuelles

| Destination du registre | Amorce |
| --- | --- |
| `m0.desir.immateria` | Où en est ma maison ? |
| `m0.volonte.marelle` | Où en est mon parcours ? |
| `m0.imagination.fresque` | Je veux enrichir ma Fresque |
| `m0.imagination.traces` | Je veux revoir mes Traces |
| `m0.emotion.heros` | Je veux retrouver mon mentor |
| `m0.communication.profil` | Je veux revoir mon profil |
| `m0.communication.echanges` | Je veux rejoindre les Échanges |
| `m0.communication.annuaire` | Je veux découvrir les autres Joueurs |
| `m0.intuition.guides` | Je veux parler aux Guides |
| `m0.intuition.cles` | Je veux explorer les clés du Point Zéro |
| `m0.transcendance.moteur` | Je veux comprendre mon Moteur |

Ces formulations sont des intentions adressées à l’Enfant, pas des CTA techniques. Le CTA de la
carte déposée dans le fil continue de venir du registre.

### Contenu de la carte déposée

- **Titre :** conserver `nom`, le nom stable de la Puissance. Le champ `titre` décrit le premier
  geste d’entrée et peut devenir faux après que le joueur l’a accompli.
- **Description :** utiliser `detail`, qui décrit durablement la fonction du territoire. Ne pas
  reprendre `accroche`, également écrite pour l’état de découverte.
- **Action :** conserver le `cta` et le `chemin` calculés par `Monde0Etats.pour` pour l’état réel du
  joueur.
- **Mentor :** l’exception actuelle reste juste quand une figure a été choisie : portrait, nom du
  mentor et route `/mentor` fournis par le serveur.

### Ordre sans fraîcheur inventée

La fraîcheur d’utilisation n’a pas de source aujourd’hui. Jusqu’à ce qu’un événement réel la porte,
le départage reste déterministe :

1. destination accessible encore signalée comme invitation par le registre ;
2. reprise du plan courant ;
3. ordre éditorial du Monde 0.

La recommandation « favoriser ce que le joueur n’a pas utilisé récemment » est donc reportée. Elle
ne doit produire ni date simulée, ni marqueur posé au simple affichage de l’accueil.

