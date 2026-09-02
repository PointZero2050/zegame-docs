# Référentiel : les 7 puissances et le moteur ontologique

> Ajout Claude - 2026-07-12. Synthèse fonctionnelle de `Le Point Zéro - Livre II - Chakras.docx` (source : Boris), orientée conception produit. Complète [marelle-mondes.md](marelle-mondes.md) et [monde-miroir.md](monde-miroir.md) qui mentionnaient les 7 puissances sans les détailler.

## 1. Le référentiel des 7 puissances

Chaque puissance porte un verbe vivant, une fonction, et deux polarités de déséquilibre (Lumière exacerbée / Ombre). L'équilibre n'est pas un juste milieu statique : c'est la **circulation** entre les pôles en passant par le Point Zéro.

| # | Puissance | Verbe | Fonction | Lumière exacerbée | Ombre |
|---|---|---|---|---|---|
| 1 | **Désir** | JE SUIS | Élan vital, vibration originelle (Éros) | Ivresse, démesure (Bacchus) | Honte, retrait, dépression (Thanatos) |
| 2 | **Volonté** | JE VEUX | Souveraineté, direction, persévérance | Domination, toute-puissance | Soumission, servitude, abdication |
| 3 | **Imagination** | JE CRÉE | Espace des possibles, rapport au temps | Dissociation délirante | Aphantasie, pragmatisme strict |
| 4 | **Émotion** | JE RESSENS | Langage énergétique, retour au présent | Chaos, addiction à l'intensité | Mental : anesthésie, coupure |
| 5 | **Communication** | JE M'EXPRIME | Rendre partageable, exprimer les besoins | Manipulation | Mutisme, attente silencieuse |
| 6 | **Intuition** | JE DISCERNE | Accès direct à l'implicite | Dogmatisme, certitude totale | Superstition, crédulité |
| 7 | **Transcendance** | JE DONNE | Redistribution, interface avec le Tout | — (pas de polarité propre : seule l'illusion d'autotranscendance) | — |

**Correspondance avec l'app existante (décision Boris 2026-07-12)** : on part du référentiel déjà en place dans ze.game. Les compétences actuelles suivent le format `PUISSANCE : ASPECT` (ex. « ÉMOTION : PASSION », « COMMUNICATION : ÉCOUTE ») avec un framework `Point Zéro - {Puissance} - {Lumière|Ombre}`. Ce nommage encode déjà puissance + polarité — pas de nouveau modèle de données à créer pour la V1.

## 2. Les cinq états du moteur

Chaque puissance peut être vécue selon cinq états :

1. **Équilibre** — la puissance circule librement (Source unifiée) ;
2. **Extrême de Lumière** — exacerbation (ex. Volonté → domination) ;
3. **Extrême d'Ombre** — abolition (ex. Volonté → abdication) ;
4-5. **Deux états intermédiaires de retour** — la conscience apprend de son excès ou de son abolition et rebascule (ex. le Dieu Conquérant saturé de solitude devient Dieu Pacifique).

Le moteur inverti (blocage) suit quatre phases : **répression → résurgence → décharge → saturation**.

**Échelle produit révisée (Boris, 2026-07-31)** — les profils individuels, de Cercle et
d'organisation emploient cinq niveaux communs : **Entravé · Fragile · En chemin · Intégré · En
flow**. L'interface les synthétise en trois états : **Bloqué** pour les niveaux 1-2, **En chemin**
pour le niveau 3 et **Intégré** pour les niveaux 4-5. Le flow est un état ponctuel observable, pas
un titre acquis. Cette nomenclature remplace l'ancienne échelle **pour la lecture d'UNE
puissance** ; les données historiques doivent rester interprétables lors d'une migration.

**Deux échelles, deux objets — précision de Boris, 2026-08-11.** La phrase ci-dessus a été
lue à tort comme l'abandon pur et simple de l'échelle en cinq familles. Il n'en est rien :
les deux coexistent parce qu'elles ne mesurent pas la même chose.

| Échelle | Ce qu'elle mesure | Où |
|---|---|---|
| **Trois degrés** (Bloqué · En chemin · Intégré) | l'amplitude **dans chacune des Puissances**, prise une à une | lemniscate de chaque Puissance, profils individuel / Cercle / organisation |
| **Dix degrés** (`Blocage · Tiédeur · Alignement · Alchimisation · Hyperconscience`, deux paliers par famille) | la **résultante globale** du Moteur — évaluation plus fine de l'état émergent | indicateur d'alchimisation, grand lemniscate du Moteur |

Les bornes de la résultante sont explicites : le **degré 1** correspond à un Moteur bloqué
partout et limité au niveau 1 ; le **degré 10** à un Moteur à 3 partout et en état intégré.
L'échelle en cinq familles n'est donc pas une nomenclature abandonnée — elle a changé
d'objet : elle ne qualifie plus une puissance isolée, mais la résultante que
[moteur-ontologique-visuel.md](moteur-ontologique-visuel.md) nomme « Moteur global »
(la Transcendance, non nommée comme telle à l'écran).

Ce que cela ne change pas : la résultante reste une **lecture**, jamais un rang ni une note
de valeur ; elle ne se compare pas entre personnes ; le profil d'un Cercle ou d'une
organisation n'est jamais la moyenne de ses membres (cf.
[cercles-croissance-profils-flow-omega.md](cercles-croissance-profils-flow-omega.md) §8) ;
et le principe de la section 3 ci-dessous — *une capacité est un sens de circulation, pas un
score* — vaut pour les deux échelles. Maquette de référence :
`zegame-prototypes/alchimisation-cible/`.

**Implication produit — Oméga et lemniscate** : cette mécanique fonde directement la représentation lemniscate de l'Oméga (cf. [impacts-fonctionnels.md](impacts-fonctionnels.md) F6). Le moteur ontologique EST une circulation permanente Ombre ⇄ Lumière passant par le Point Zéro ; l'amplitude visualisée peut refléter jusqu'où le joueur a exploré chaque polarité de chaque puissance. Les 5 états donnent une grammaire d'animation possible (position sur la boucle, blocage sur un pôle, circulation fluide).

## 3. Une capacité = un sens de circulation, pas un score

Point central pour la pédagogie et la validation :

- Une capacité n'est pas une qualité qu'on possède, mais **une manière de faire circuler une puissance entre ses versants selon la situation**. Un artiste développe la Lumière de l'Imagination ; un auditeur qualité doit développer son Ombre (limiter l'imagination pour vérifier une conformité). Un orateur développe la Lumière de la Communication ; un médiateur son Ombre (écouter, retenir l'intervention).
- Le livre critique explicitement les référentiels de compétences classiques qui « fragmentent l'être en items séparés » (leadership, créativité, écoute...) : un référentiel fondé sur les 7 puissances révèle **où l'énergie circule, se fige, s'exacerbe ou se réprime**.

**Implication produit** : la progression ne devrait pas être une somme de badges par compétence, mais pouvoir montrer l'équilibre/déséquilibre par puissance (les deux polarités d'une même puissance sont déjà distinguées dans le référentiel de l'app). À articuler avec le moteur de validation ([validation.md](validation.md)).

## 4. Les gardiens : fil rouge thématique des Mondes

Le livre associe la traversée des Mondes de la Marelle à des « gardiens » — une croyance limitante par puissance, dans un ordre de descente précis (on ne commence pas par la Racine) :

| Gardien | Puissance | Croyance à traverser | Monde(s) | Fil rouge du Monde |
|---|---|---|---|---|
| 1 | Intuition | « Je dois comprendre avant d'agir » | 0-1 | Réflexivité, discernement, cartographie intérieure — **mantra des Mondes 0-1 : « JE DISCERNE » (Boris, 2026-07-13)** |
| 2 | Communication | « M'exprimer pleinement est impossible » | 2 | Cadre de sécurité : cercles, parole authentique, écoute réelle |
| 3 | Émotion (cœur) | « Si j'ouvre mon cœur, je vais souffrir » | 3 | Confrontation à l'Ombre, accueil des émotions |
| 4 | Imagination | « Je peux créer des mondes, mais pas transformer celui-ci » | 4 | Incarnation de la création dans l'Empire (art, rituel, œuvre) |
| 5 | Volonté | « Mériter demande un effort » | 5 | Se laisser traverser (constellations systémiques, action sans forçage) |
| 6 | Amour de soi | « M'aimer serait de l'égoïsme » | 6 (probable) | Réhabiliter l'amour de soi comme fondement du lien |
| 7 | — | *Non détaillé dans le document lu (probablement le Désir/Racine)* | — | — |

**Apports vs doc existante** : [marelle-mondes.md](marelle-mondes.md) §2 décrit les Mondes par formes d'engagement et rites de passage ; cette table ajoute la **logique intérieure** de chaque Monde (quelle croyance il travaille, quelle puissance il libère). Les deux lectures sont complémentaires et cohérentes (Monde 2 = cercles dans les deux ; Monde 3 = travail de l'Ombre dans les deux).

## 5. Éclairages sur des éléments déjà documentés

- **Docteur Z.E.R.O.** ([game-autosubversion.md](game-autosubversion.md) §3) : le livre précise son origine — figure alchimique née du travail de l'Ombre au niveau du cœur (gardien 3 / Monde 3). Suggestion pour F5 (mentors IA) : les mentors de la bibliothèque pourraient être liés aux gardiens/puissances qu'ils aident à traverser.
- **L'Ombre comme « Lumière non intégrée »** ([monde-miroir.md](monde-miroir.md) §5) : confirmé et approfondi — l'Ombre emmagasine la Lumière non reconnue et « ne veut jamais nous détruire, elle veut être réintégrée ». La boucle des antagonistes (combat → victoire apparente → déplacement → Lumière captive → transformation) est le moteur inverti raconté.
- **Fonctions universelles** : les 7 puissances s'appliquent aussi aux organisations (famille, entreprise, communauté) — pertinent pour l'évaluation des cercles et des communautés (sans jamais devenir un diagnostic automatique, garde-fou maintenu).
- **Émotions primaires** : peur, colère, tristesse, honte, dégoût sont définies comme signaux d'écart au « JE SUIS » — vocabulaire utilisable pour les conversations d'intégration des Graines de Récit.

### Correspondance canonique avec les cinq cadres

> Décision Boris - 2026-07-31. Ces correspondances ne doivent pas être remplacées par une lecture
> fonctionnelle plus intuitive : **Volonté ↔ Relationnel**, **Imagination ↔ Sens**,
> **Émotion ↔ Gouvernance**, **Communication ↔ Opérationnel**, **Intuition ↔ Apprenance**.

La Volonté devient relationnelle dans la co-souveraineté, entre décider, servir et diriger. La
gouvernance relève de l'Émotion parce que le Point Zéro vise à faire du cœur le nouveau centre de
décision, notamment par des dispositifs capables de syntoniser le champ d'information. La chaîne
complète des profils systémiques et du flow est spécifiée dans
[cercles-croissance-profils-flow-omega.md](cercles-croissance-profils-flow-omega.md).

## 6. Garde-fous spécifiques à ce référentiel

Le matériau est puissant et intime. En plus des garde-fous généraux ([monde-miroir.md](monde-miroir.md) §13) :

- Jamais de diagnostic automatique du « blocage » d'un joueur sur une puissance ou un archétype ;
- L'Ombre n'est jamais un score négatif ni une identité assignée ;
- Les états du moteur sont un langage d'auto-exploration proposé au joueur, pas une grille d'évaluation par des tiers ;
- Les contenus touchant sexualité, honte, haine de soi (présents dans le livre) relèvent de l'accompagnement humain, pas de mécaniques de jeu.

---

<!-- Ajout Claude, 2026-07-15 -->
**Voir aussi** : [moteur-ontologique-visuel.md](moteur-ontologique-visuel.md) pour la traduction visuelle de ce référentiel (lemniscate vivant à lobes indépendants, grammaire état/progression, fiche puissance) et le modèle d'interaction piloté par un questionnaire 360°.
