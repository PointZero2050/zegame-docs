# Le Coupable idéal V2 — amendements d'implémentation

> Ajout Claude - 2026-07-27, en réponse à
> [la spec du procès contradictoire](coupable-ideal-proces-polarites.md) (Codex, commit `22c96b1`).
> Arbitré avec Boris avant écriture du code. **La V2 est implémentée, déployée et vérifiée**
> sur `vibe.ze.game` (commit applicatif `851a132`). Ce document décrit les écarts assumés
> par rapport à la spec : en cas de divergence sur ces trois points, c'est cette note qui
> décrit le code réel.

## 1. Ce que la spec avait juste et qui est repris tel quel

Le procès contradictoire, ses cinq rôles, les trois objections récurrentes, la politique
`traversed`, la validation système idempotente, les garde-fous pédagogiques (asymétrie des
violences, refus de réponse toujours recevable, Masculin/Féminin explicitement symbolique,
aucun score moral ni diagnostic), l'accessibilité et la liste hors périmètre : repris sans
modification. Les quatre chefs d'accusation rédigés par Codex pour les médias sont repris
verbatim.

## 2. Les trois amendements

### 2.1. Aucun mapping automatique axe → Puissance

**Ce qui change.** La spec laissait ouverte la possibilité d'un lien systématique entre les
six axes et les six Puissances. Le code n'en établit aucun.

**Pourquoi.** Un mapping un-pour-un est un faux ami. L'axe `Rationalité ↔ Émotion` décrit ce
qu'une civilisation privilégie et ce qu'elle exile ; la Puissance Émotion décrit comment
l'énergie circule chez une personne, entre Dissociation et Fusion, avec la Présence comme
Source. Ce ne sont pas des objets de même nature. Et surtout : dans une société qui exile
l'émotion, une personne peut très bien être **celle qui porte le pôle exilé**. La relation
n'est pas une identité, c'est une tension — parfois une opposition. Une table de
correspondance mentirait, et créerait exactement la confusion que Boris a identifiée entre
la roue et les fiches Puissance.

**Ce qui relie réellement les deux échelles**, c'est le *geste* : absolutiser un pôle et
exiler son contraire. L'application le modélise déjà côté individuel — ce sont les états
Bloqué / En chemin / Intégré et la lemniscate. Le joueur n'a donc pas une correspondance à
apprendre, mais un geste à reconnaître.

### 2.2. La roue reste la carte du collectif

**Ce qui change.** Le troisième anneau de la roue (« miroir individuel », §8.1 de la spec)
est retiré. La roue porte la couronne des accusés, les six diamètres et le centre ouvert —
rien d'individuel.

**Pourquoi.** Fusionner les deux échelles dans une seule image recrée la confusion : une roue
circulaire à six axes avec une marque centrale ressemblerait trop à ce que l'application
montre déjà des Puissances. Le passage à l'individuel se fait par **une ligne de texte**
sous la roue, jamais par un anneau.

Trois règles tenues dans le code :

- deux objets distincts, jamais superposés — la roue (12 pôles, diamètres, centre) pour le
  collectif, la lemniscate (deux lobes, un point qui circule) pour l'individu ; la roue
  n'affiche aucun nom de Puissance ;
- **aucun `var(--jaune)` dans la roue** : le doré est déjà la convention « état atteint » des
  fiches Puissance, et la roue ne mesure rien. Le centre reste un cercle ouvert, pas une
  marque dorée ;
- une seule Puissance nommée à la fin, jamais six — une porte, pas un profil.

### 2.3. L'écran 6 devient une graine, pas un miroir mesuré

**Ce qui change.** La « chambre du jury » ne mesure pas le mouvement spontané du joueur. Elle
lui propose de nommer la Puissance où il reconnaît le mouvement que son récit met dehors,
avec « Je ne sais pas encore » et « Je préfère ne pas répondre » toujours recevables.

**Pourquoi.** Contrainte de séquence, vérifiée en base : **le Coupable idéal est en position 3
du parcours, le Moteur (« Une drôle d'époque ») en position 4.** Au moment du procès, le
joueur n'a aucune donnée de Puissance — ni Moteur, ni questionnaire. Un miroir mesuré serait
soit vide, soit un second Moteur concurrent du vrai.

C'est une meilleure fonction pour ce jeu : il **plante** la question que la suite du Monde 0
va éclairer. Le texte de l'écran l'annonce explicitement, et « Une drôle d'époque » tient la
promesse deux minutes plus tard.

## 3. La clé pédagogique retenue

La formulation de Boris — *le Point Zéro d'une civilisation est la résultante des Point Zéro
individuels* — est rendue comme un mécanisme et non comme un slogan. Phrase de clôture de la
roue :

> Une civilisation ne peut pas faire circuler un mouvement que chacun de ses membres exile en
> lui-même. Son Point Zéro est la résultante des nôtres.

La chaîne éprouvée par le joueur : les crises se répondent → j'accuse une grande cause →
derrière mon accusation il y a une grille de lecture → toute grille privilégie des pôles et
en exile d'autres (c'est la roue, c'est l'Empire) → **ce geste, je viens de le faire** → dans
quelle Puissance est-ce que je le reconnais ?

## 4. Données de la roue

Les 12 pôles et 6 diamètres viennent du schéma canonique de Boris
(`Ressources Point Zero/Modèles/Cite-Cosmique-2.png`, hors dépôt) : Esprit ↔ Matière,
Rationalité ↔ Émotion, Technologie ↔ Nature, Masculin ↔ Féminin, Ordre ↔ Chaos,
Individu ↔ Collectif.

Point à retenir du schéma : **la Cité Cosmique et l'Empire portent exactement les mêmes
pôles.** Seul le sens de circulation change — vers le centre (intégration) ou vers l'extérieur
(dissociation). C'est cette bascule, et non une liste de bons et de mauvais pôles, que la
dataviz rend lisible. Un axe peut être intensément mobilisé sans être problématique.

Les triades Être / Connaissance / Puissance et Avoir / Savoir / Pouvoir sont **gardées en
réserve** : justes, mais une troisième couche conceptuelle dans un Monde 0 qui en porte déjà
deux.

## 5. Écarts d'état constatés à l'implémentation

- **Challenge 257 était `declarative`**, pas `systeme` comme l'annonçait la spec. Le jeu
  validait pourtant déjà lui-même : le bouton déclaratif était une redondance. Passé en
  `systeme`, CTA de l'adaptateur `ExperienceState` : « Ouvrir l'audience ».
- **La vidéo n'existe pas encore** (script v0.1 non produit), et le Challenge 257 n'a aucune
  ressource : `video_first?` est faux. La V2 est donc livrée avec une entrée sans vidéo.
  L'enchaînement lecteur → procès sans retour à la fiche reste à faire quand la vidéo sera
  produite ; il faudra alors revoir la durée affichée (10 min aujourd'hui, ~17 avec la vidéo).
- **Aucune session V1 incomplète en base** : 3 sessions, toutes terminées, sur 2 comptes qui
  sont tous les deux ceux de Boris. Tout le volet « reprise des brouillons V1 » de la spec
  (§13) était donc sans objet et n'a pas été implémenté. Les 3 sessions restent en
  `flow_version` 1, rendues par le flux et la définition V1, jamais réévaluées. Rejouer crée
  une session V2 sans nouveau gain d'Ω.
- **Piège `mathieu_core` corrigé** dans `CoupableIdealSession#validate_marelle_experience!` :
  `on_change` est un `after_commit on: [:update]`, jamais déclenché à la création. Créer un
  `ChallengesUser` déjà validé validait l'expérience **sans attribuer les Ω**. Contrôle en
  base : aucun joueur n'avait été touché. Les trois autres modèles (`MoteurAssessment`,
  `Traversee`, `ConseilSession`) portent le même bug latent et restent à corriger.

## 6. Volume éditorial

Le contenu livré couvre les 12 causes : label judiciaire, 3 à 4 chefs d'accusation reliés
chacun à un axe et à un pôle, 3 fonctions légitimes. Les conséquences du réquisitoire sont
communes aux 12 causes, et les dérives du contraire réutilisent la table V1 — dont **8 des 12
entrées restent marquées `source: brouillon`** et méritent la relecture éditoriale que la spec
demandait.

## 7. Reste à faire

1. Produire la vidéo `La crise de nos récits`, puis brancher l'enchaînement vidéo → procès.
2. Relire les 8 tables de dérives encore en brouillon.
3. Corriger le piège `on_change` dans les trois autres modèles de session.
4. Horizon, hors périmètre : si chaque joueur produit sa roue, la roue d'un Cercle est
   l'agrégat des roues de ses membres — « le Point Zéro de la civilisation est la résultante
   des Point Zéro individuels » deviendrait littéralement lisible à l'écran. Un agrégat,
   jamais une comparaison entre joueurs.
