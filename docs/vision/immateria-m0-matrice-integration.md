# Immateria et Monde 0 matrice d’intégration

**Proposition de conception — Codex, 19 septembre 2026.** Cette note traduit les décisions de
Boris sur le nouvel accueil et l’Enfant intérieur en un contrat d’intégration pour le Monde 0.
Elle ne constate aucun contrôleur, événement ou badge déjà livré. Les preuves serveur restent à
relire dans `pointzero-app` avant toute implémentation.

## 0. Périmètre de la première version pour les stores

**Décision de Boris, 19 septembre 2026.** La première version publiée porte uniquement le seuil
nécessaire pour installer Immateria dans l’application :

1. l’introduction obligatoire d’E1 dans le foyer ;
2. la descente dans la cave et la rencontre des premiers Gardiens ;
3. la remontée au foyer et la fin réelle du tutoriel ;
4. le retour vers le nouvel accueil à deux plans ;
5. le premier badge Immateria **Une flamme à soi**, signalé par l’avatar et classé dans
   `Mes Accomplissements`.

Les autres pièces, leurs quêtes et les sept autres badges proposés par cette note constituent une
mise à jour ultérieure. Elles restent décrites afin de préserver la direction d’ensemble, mais ne
font pas partie du lot de publication initial.

### Contenu minimal du nouvel accueil

La première version doit déjà montrer :

- la moitié Immateria avec l’avatar dans l’aperçu du foyer, son nom, son statut d’Enfant intérieur
  et le CTA **Rejoindre Immateria** ;
- la moitié Materia avec l’Expérience en cours, le joueur, ses Omégas et le CTA
  **Continuer mon parcours** ;
- le lemniscate animé comme articulation entre les deux plans ;
- le composeur de dialogue avec un accueil de l’avatar et des amorces liées au désir présent ;
- le signalement du premier badge, sans modale automatique ;
- le menu principal **Accueil · Parcours · 7 Puissances · Échanges**.

Le parcours, les cartes de Puissances et la page finale du Monde 0 restent en place. Le nouvel
accueil ne les remplace pas : il devient le sas quotidien entre Materia et Immateria.

### Dialogue de première version

La validation d’E1 et la remise du badge ne doivent pas dépendre d’un modèle conversationnel. Le
premier lot peut utiliser un accueil scripté et des réponses de repli déterministes. Si le dialogue
IA est inclus, il reste une couche d’enrichissement : une indisponibilité réseau ou du service ne
doit jamais empêcher le joueur de rejoindre Immateria ou de continuer son parcours.

### MageOS dans la première version

L’économie des MageOS n’étant pas encore définie, la première version ne doit pas afficher un
solde numérique arbitraire ni simuler des gains. Deux traitements restent sûrs : masquer le
compteur jusqu’à sa première source réelle, ou afficher un état non chiffré **MageOS en sommeil**
avec une courte explication. Le choix visuel reste à arbitrer avant le portage final de l’accueil.

### Données à conserver dès le premier lot

La première version doit rendre durables, sans inventer les futures pièces :

- l’archétype choisi ;
- l’apparence et le nom de l’avatar ;
- le désir fondamental et la réponse sur sa place actuelle ;
- les formulations protectrices explicitement validées dans la cave ;
- la fin terminale et idempotente d’E1 ;
- la date d’obtention et l’état de présentation du badge **Une flamme à soi** ;
- la version du script E1 ayant produit ces données.

Les éveils de Puissance déjà conservés par Materia suffiront à initialiser les portes lors de la
mise à jour des autres pièces. Il ne faut pas créer dès maintenant de faux états `visited` ou
`quest_completed` pour des pièces qui n’existent pas encore.

### Critères de sortie du premier lot

- une traversée complète d’E1 sur mobile et ordinateur revient au nouvel accueil ;
- quitter puis reprendre le foyer ou la cave retrouve le dernier état durable ;
- un double clic, un rechargement ou un second onglet ne valide pas deux fois E1 et ne remet pas
  deux fois le badge ;
- le premier badge apparaît dans la catégorie Immateria et peut être présenté par l’avatar une
  seule fois ;
- continuer le parcours Materia reste possible après E1 sans autre visite d’Immateria ;
- le dialogue indisponible possède un repli lisible ;
- clavier, lecteur d’écran, mouvement réduit et petit écran conservent les actions essentielles ;
- aucune donnée intime de la cave n’est publiée ou rendue communautaire par défaut.

## 1. Décision directrice

L’entrée dans Immateria est obligatoire en E1 parce que la Marelle reste un jeu d’enfant et que la
rencontre avec l’Enfant intérieur en constitue le seuil. Après E1, l’exploration d’Immateria devient
facultative.

Le parcours principal reste porté par Materia. Lorsqu’une Expérience éveille une Puissance, sa
pièce devient disponible dans la maison. Le joueur peut la visiter immédiatement, plus tard ou ne
pas la visiter. Son absence ne bloque jamais l’Expérience suivante, la clôture du Monde 0 ou
l’ouverture d’un Monde ultérieur.

La maison conserve les échos des Expériences accomplies. Une pièce **déverrouillée** n’est pas une
pièce **visitée** ; une pièce visitée n’est pas une quête **accomplie**. Les badges Immateria ne
reconnaissent que les actions réellement vécues dans le monde miroir.

La première révélation de la cosmogonie — des personnages qui semblent sortir de leur routine et
s’interroger sur leur monde — commence au Monde 1. Le Monde 0 peut seulement en semer quelques
anomalies discrètes, sans les expliquer.

## 2. Ce que la matrice relie et ce qu’elle ne confond pas

La matrice distingue quatre faits :

1. le geste Materia réellement reconnu par le contrôleur de l’Expérience ;
2. l’éveil d’une Puissance et l’ouverture durable de son territoire ;
3. la transformation correspondante de la maison ;
4. la quête facultative réellement accomplie dans Immateria.

La ventilation des Omégas d’une Expérience peut mobiliser plusieurs compétences. Elle ne doit pas
servir à déduire la pièce ouverte. La maison écoute l’événement d’éveil déjà reconnu par le Jeu,
jamais une somme de points ou une simple visite de page.

Les six Puissances centrales possèdent trois compétences canoniques. Le geste d’éveil du Monde 0
présente d’abord leur Source :

| Puissance | Compétence Source présentée au seuil |
|---|---|
| Désir | **JE SUIS** |
| Volonté | **JE DÉCIDE** |
| Imagination | **JE CRÉE** |
| Émotion | **JE RESSENS** |
| Communication | **JE M’EXPRIME** |
| Intuition | **JE DISCERNE** |

Transcendance reste hors du référentiel des 18 compétences. Elle désigne la circulation entre les
six Puissances et garde son verbe d’accès **JE DONNE**. Le tutoriel du premier cap, déjà validé,
est son geste pédagogique dans E14.

Références : [parcours linéaire du Monde 0](https://github.com/PointZero2050/zegame-docs/blob/main/docs/pedagogie/monde-0-parcours-lineaire-appropriation.md), [référentiel des 18 verbes](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-correspondance.md), [premier cap et Transcendance](https://github.com/PointZero2050/zegame-prototypes/tree/8b4bd79/cap-transcendance-m0-cible).

## 3. Géographie fonctionnelle de la maison

Les noms ci-dessous sont des noms de production proposés. Le hall, la chambre et la cave disposent
déjà de sources graphiques ; les autres pièces demandent encore un choix de décor.

| Espace | Fonction dans la maison | État après E1 |
|---|---|---|
| **Hall et foyer** | Désir, nom de l’Enfant, flamme fondamentale et accueil | éveillé par E1 |
| **Atelier des décisions** | Volonté, choix, direction et capacité de commencer | porte fermée mais visible |
| **Chambre des possibles** | Imagination, élans, Graines et formes à venir | visible, encore endormie |
| **Jardin sensible** | Émotion, relation, présence et ce qui touche | porte fermée |
| **Salon des voix** | Communication, expression, écoute et liens avec les autres maisons | porte fermée |
| **Observatoire** | Intuition, doute, discernement et lecture des signes | porte fermée |
| **Puits de lumière ou toit** | Transcendance et circulation des six pièces | inaccessible |
| **Cave des Gardiens** | peurs protectrices et décisions anciennes ; espace transversal | visitée en E1, trois Gardiens anonymes possibles |

La cave n’est pas une huitième Puissance. Elle est le sous-sol commun de la maison. Les trois
verbes de chaque Puissance enrichiront plus tard sa pièce par des objets, interactions ou passages ;
ils ne créent pas dix-huit pièces supplémentaires.

## 4. États à conserver séparément

Pour chaque pièce ou quête, le produit doit pouvoir distinguer :

| État | Sens |
|---|---|
| `eligible` | le fait Materia nécessaire existe ; la pièce peut être ouverte |
| `unlocked` | l’ouverture a été appliquée à la maison de manière idempotente |
| `notified` | l’avatar a signalé cette nouveauté au moins une fois |
| `visited` | le joueur est réellement entré dans la pièce |
| `quest_started` | la quête Immateria a produit un premier état durable |
| `quest_completed` | la condition terminale propre à la quête existe |
| `badge_presented` | l’avatar a présenté le badge Immateria obtenu |

Ces noms décrivent une sémantique. Ils ne préjugent ni d’une table, ni d’un modèle Rails, ni de
clés définitives. L’analyse d’impact du portable devra d’abord vérifier ce que les Traces,
marqueurs et reçus existants couvrent déjà.

Un `GET`, l’ouverture d’une porte ou l’affichage d’un dialogue ne peut jamais poser
`quest_completed`. La condition terminale doit être explicite et idempotente.

## 5. Matrice des vingt passages du Monde 0

Les titres et l’ordre suivent le parcours linéaire courant. Les quêtes Immateria et les titres de
badges sont des propositions éditoriales à tester dans le script et les maquettes.

| # | Passage Materia et fait reconnu | Éveil ou compétence | Écho automatique dans la maison | Quête Immateria | Badge Immateria proposé |
|---:|---|---|---|---|---|
| **E1** | **Façonner mon jumeau** — archétype, avatar, nom intime, désir, croyances protectrices et fin réelle du tutoriel | Désir · **JE SUIS** | l’Enfant apparaît ; le foyer s’allume ; la maison, la chambre et la cave existent ; trois socles peuvent recevoir les premiers Gardiens | **Retrouver la flamme** — c’est le tutoriel obligatoire lui-même, pas une quête facultative supplémentaire | **Une flamme à soi** — fin réelle d’E1 |
| **E2** | **Le Point Zéro entrer dans le Jeu** — introduction, Chaîne invisible et Hypothèse de seuil ; sas de découverte achevé | Volonté · **JE DÉCIDE** | la porte de l’Atelier s’ouvre ; l’Hypothèse apparaît comme une direction encore provisoire | **Choisir une première direction** — déplacer un repère vers une action simple sans transformer l’Hypothèse en promesse définitive | **La porte que j’ai choisie** |
| **E3** | **Le Coupable idéal** — procès achevé et verdict conservé | aucune nouvelle Puissance | un masque ou un fragment de roue apparaît dans la cave ; un Gardien peut réagir sans être nommé | aucune quête autonome en M0 ; l’objet peut être observé | aucun nouveau badge |
| **E4** | **Une drôle d’époque** — premier miroir atteint et résultat conservé | aucune nouvelle Puissance | un miroir se forme dans le hall et reflète parfois la maison autrement | observation libre, sans validation | aucun nouveau badge |
| **E5** | **Avant le Zéro** — un devenir atteint et conservé | aucune nouvelle Puissance | une fenêtre de la Chambre montre le devenir traversé ; les autres restent des possibles | rejouer un devenir reste une action Materia | aucun badge Immateria ; les badges de parcours existants gardent leur rôle |
| **E6** | **Et moi dans tout ça** — trois questions, réponse libre et Graine de l’Appel réellement créée | Imagination · **JE CRÉE** | la Chambre des possibles s’éveille ; la Graine prend une forme symbolique inachevée | **Donner une forme à l’élan** — choisir et placer dans la Chambre un objet symbolique issu de la Graine | **La chambre rêve tout haut** |
| **E7** | **Choisir qui marchera à mes côtés** — mentor choisi, première question enregistrée, découverte pédagogique achevée | Émotion · **JE RESSENS** | le Jardin sensible s’ouvre ; l’écho de la première question devient onde, plante ou lumière | **Écouter ce qui répond** — observer trois réactions possibles et choisir celle qui mérite d’être gardée, sans diagnostic | **Quelque chose m’a touché** |
| **E8** | **L’écosystème Point Zéro** — constellation parcourue et Schéma de circulation enregistré | aucune nouvelle Puissance | un mobile relie les pièces déjà ouvertes et révèle les portes encore muettes | manipulation libre du mobile | aucun nouveau badge |
| **E9** | **Choisir ma place parmi les autres** — Profil composé, appartenance et réaction persistées, découverte pédagogique achevée | Communication · **JE M’EXPRIME** | le Salon des voix s’ouvre ; une fenêtre donne sur les lumières des autres maisons | **Donner une voix à la maison** — choisir une phrase, un son ou un signe par lequel l’avatar se présente aux voisins | **La maison a une voix** |
| **E10** | **Le site du Point Zéro** — au moins un parcours public réellement accompli | aucune nouvelle Puissance | les parcours accomplis apparaissent comme livres, cartes ou objets consultables dans le Salon | aucune quête distincte ; chaque parcours conserve son propre badge | aucun doublon Immateria |
| **E11** | **Le signe de reconnaissance** — signe composé et destination choisie ; passage facultatif | aucune nouvelle Puissance | le signe rejoint la porte, la boîte aux lettres ou un mur du Salon | placer le signe reste une animation de retour, sans nouvelle preuve | aucun nouveau badge |
| **E12** | **Choisir un double regard** — Guide choisi, échange réel, première clé éprouvée et découverte pédagogique achevée | Intuition · **JE DISCERNE** | l’Observatoire s’ouvre ; la clé devient une lentille qui ne donne jamais une lecture unique | **Regarder sans conclure** — observer une forme ambiguë, conserver deux lectures possibles ou choisir « je ne sais pas » | **Une fenêtre dans la nuit** |
| **E13** | **Les choses se précisent** — relecture, échange mentor et Graine de relation créée | aucune nouvelle Puissance | la Graine de relation relie deux objets ou deux lumières dans le Jardin et le Salon | interaction libre avec ce lien | aucun nouveau badge |
| **E14** | **Lire mon Moteur** — première évaluation enregistrée, tutoriel du premier cap accompli et dévoilement final | Transcendance · **JE DONNE**, hors des 18 | le puits de lumière ou le toit s’ouvre ; un lemniscate relie les six pièces ; le cap choisi apparaît en pointillés | **Faire respirer la maison** — faire circuler une lumière depuis la pièce choisie vers le centre puis vers une autre pièce | **La maison respire** |
| **E15** | **Le Conseil Oméga** — caps conservés et Rôle d’appel choisi ou laissé ouvert | aucune nouvelle Puissance | une chaise vide et les caps apparaissent dans le hall ou l’Atelier | observation et déplacement libres, sans second arbitrage | aucun nouveau badge |
| **E16** | **Découvrir les formats** — Boussole conservée ; passage facultatif | aucune nouvelle Puissance | la Boussole rejoint l’Atelier des décisions | consultation libre | aucun nouveau badge |
| **E17** | **Participer à un Sas Point Zéro** — inscription, participation et intention selon les preuves réelles ; passage facultatif | aucune nouvelle Puissance | une lampe ou un feu de rencontre apparaît dans le Salon seulement après la preuve prévue par le contrat | écouter l’écho de la rencontre, sans prétendre enregistrer son contenu | aucun nouveau badge |
| **E18** | **Vivre l’Atelier Point Zéro** — inscription active ; présence réelle validée plus tard | aucune nouvelle Puissance | avant présence : invitation posée près de la porte ; après présence : trace collective dans le hall | aucune quête Immateria avant la présence réelle | aucun badge Immateria ; le seuil **Premier atelier vécu** reste gardé par le Professeur |
| **E19** | **Mon récit de passage** — Graine, Carte du Seuil privée et scellement réel | circulation des sept territoires, sans nouvelle compétence | la Carte du Seuil apparaît dans le hall et relie les objets réellement produits pendant M0 | **Accrocher la Carte** — choisir son emplacement, parcourir ses liens puis confirmer ce que l’Enfant veut garder visible dans la maison | **Le chemin est entré dans la maison** |
| **E20** | **Ton espace est prêt** — clôture explicite et idempotente de M0 | aucune nouvelle Puissance | la maison passe au présent ; l’avatar distingue les échos anciens des nouvelles quêtes | aucune quête supplémentaire ; l’accueil propose Materia et Immateria à égalité | badge de parcours **Point Zéro Monde 0**, sans doublon Immateria |

## 6. Catalogue minimal des badges Immateria du Monde 0

La catégorie **Immateria** s’ajoute à Parcours, Seuils et Dopamine dans
`Mes Accomplissements`. L’avatar en est la voix. Il ne décerne pas une note : il rappelle une
aventure vécue ensemble.

| Clé éditoriale provisoire | Titre | Condition réelle proposée | Présentation par l’avatar |
|---|---|---|---|
| `immateria_flamme` | **Une flamme à soi** | fin terminale d’E1 V2 | au premier retour sur le nouvel accueil |
| `immateria_volonte` | **La porte que j’ai choisie** | quête de l’Atelier des décisions accomplie | au retour de la pièce |
| `immateria_imagination` | **La chambre rêve tout haut** | objet symbolique de la Graine placé | au retour de la pièce |
| `immateria_emotion` | **Quelque chose m’a touché** | écho émotionnel explicitement conservé | au retour de la pièce |
| `immateria_communication` | **La maison a une voix** | signe de présentation de l’avatar conservé | au retour de la pièce |
| `immateria_intuition` | **Une fenêtre dans la nuit** | interaction d’ambiguïté terminée sans réponse imposée | au retour de la pièce |
| `immateria_transcendance` | **La maison respire** | circulation lumineuse terminée | au retour du toit ou du puits de lumière |
| `immateria_carte` | **Le chemin est entré dans la maison** | Carte du Seuil réellement accrochée après son scellement | sur l’accueil, avant ou après E20 |

Les badges non obtenus restent absents de la collection. Une grille de silhouettes verrouillées
transformerait l’exploration facultative en liste de tâches implicite.

Un badge Immateria :

- n’accorde aucun Oméga ;
- n’ouvre aucun droit Materia ;
- ne remplace aucun badge de parcours ou de seuil ;
- ne tombe jamais à la seule ouverture d’une pièce ;
- reste obtenable après la clôture du Monde 0.

Le reçu de badge mémorise seulement que son annonce reste à présenter. La vérité du badge reste la
condition terminale de la quête, selon le même principe que le [contrat M0 des badges](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-badges-attribution-contrat.md).

## 7. Signalement depuis le nouvel accueil

L’avatar regroupe les nouvelles. Il ne produit jamais une modale spontanée ni une série de cartes
à fermer.

### Une seule nouveauté

> « Il y a quelque chose de nouveau dans la maison. Tu veux que je te montre ? »

Actions : **Voir ce qui a changé** · **Pas maintenant**.

### Plusieurs nouveautés

> « Il s’est passé plein de choses pendant que tu vivais là-bas. La maison les a gardées. On n’est
> pas en retard. Tu veux que je te montre une pièce ? »

Actions : **Suivre l’avatar** · **Choisir une pièce** · **Pas maintenant**.

### Badge obtenu

L’avatar présente le badge dans la conversation puis propose **Retrouver mes accomplissements**.
S’il y en a plusieurs, une seule entrée ouvre un récapitulatif du lot. La consommation du reçu
d’annonce doit être atomique afin qu’un rechargement ou un second onglet ne présente pas le même
lot deux fois.

## 8. Rattrapage tardif

Le rattrapage n’est jamais formulé comme une dette.

1. Materia continue d’ouvrir les pièces au rythme des éveils, même si elles ne sont pas visitées.
2. Au retour, toutes les portes éligibles sont visibles mais les quêtes restent non accomplies.
3. L’avatar propose une seule prochaine découverte ou laisse choisir une pièce.
4. Le contenu cosmologique conserve ses prérequis. Un joueur arrivé en M2 peut visiter les pièces
   de M0 dans l’ordre souhaité, mais les scènes du Mystère de M1 restent séquencées.
5. Chaque quête emploie une introduction au passé : « Cette porte s’est ouverte quand tu as
   découvert Émotion. Tu n’étais pas encore venu voir ce que cela avait changé ici. »
6. Les badges sont attribués au moment réel de la quête, jamais rétroactivement à partir du niveau
   Materia.
7. Une fois le dernier écho ancien traité, l’avatar dit simplement : « Maintenant tu sais tout ce
   que je sais. Enfin… presque. »

Le produit doit pouvoir distinguer `unlocked_at`, `visited_at`, `quest_completed_at`,
`notified_at` et `badge_presented_at`. Ces champs sont une expression du besoin ; leur traduction
technique reste à analyser.

## 9. Compatibilité avec les joueurs déjà avancés

Une migration ne doit jamais retirer une validation, des Omégas ou un accès acquis.

Trois populations doivent être auditées :

1. joueurs ayant terminé l’ancien tutoriel et possédant la Trace Immateria historique ;
2. joueurs avancés par les outils de recette sans traversée réelle d’Immateria ;
3. joueurs ayant commencé l’ancien tutoriel sans le terminer.

La Trace historique ne prouve pas automatiquement les nouveaux faits d’E1 V2. Pour un joueur déjà
avancé, la solution la moins coercitive est de conserver sa progression Materia et de proposer une
séquence **Retrouver ton Enfant intérieur** qui initialise le nouvel avatar et la maison sans
reverser les 5 Omégas. Cette séquence devient obligatoire avant la première utilisation du nouvel
accueil Immateria, mais ne referme pas les Mondes ou Expériences déjà accessibles.

Les comptes de recette qui ne possèdent aucune preuve réelle doivent rester identifiables ; leur
état ne doit pas servir de règle de rattrapage pour les joueurs.

## 10. Données et confidentialité

La maison ne reflète que des faits et contenus explicitement produits par le joueur : désir,
réponses, Graines, Traces, choix, quêtes et objets symboliques. Elle ne déduit pas un état intime à
partir d’un score ou d’un dialogue libre.

Le désir, les croyances protectrices, les échanges avec l’avatar et les Gardiens restent privés par
défaut. Une suppression ou modification de la donnée source doit avoir un traitement visible :
l’objet peut devenir indisponible ou être réactualisé, mais il ne doit pas continuer à citer un
contenu supprimé.

Le dialogue de l’avatar peut proposer des routes déjà autorisées. Il ne crée pas de contrôleur,
n’ouvre pas une Puissance et ne valide pas une quête par interprétation libre. Les CTA sont fournis
par une liste blanche issue de l’état serveur.

## 11. Contrat minimal pour l’analyse d’impact du portable

Avant implémentation, le portable doit établir pour chaque ligne d’éveil :

- le fait métier actuel qui ouvre la Puissance ;
- le moment exact où ce fait devient durable ;
- l’événement ou service pouvant alimenter Immateria sans double écriture ;
- les joueurs historiques concernés ;
- la stratégie idempotente de création de l’état de maison ;
- les effets d’un rejeu, d’une suppression de Trace et d’un changement de choix ;
- le reçu d’annonce et sa consommation atomique ;
- les bancs qui protègent les Ω, la progression et l’absence de validation par `GET`.

Le poste fixe pourra ensuite porter les états visuels de la maison et du nouvel accueil. La maquette
reste une simulation : elle ne doit ni stocker la progression dans le navigateur, ni fabriquer les
badges, ni interpréter les Traces.

## 12. Arbitrages encore nécessaires

1. noms et plans définitifs des quatre nouvelles pièces, du toit et de leurs transitions ;
2. micro-interactions terminales des six quêtes facultatives ;
3. titres et graphismes définitifs des huit badges Immateria ;
4. économie des MageOS : sources, usages et absence de conversion avec les Omégas ;
5. stockage du résumé de dialogue de l’avatar et capacité du joueur à le corriger ou le supprimer ;
6. traitement éditorial exact des anciens joueurs au premier affichage du nouvel accueil.

Ces arbitrages ne remettent pas en cause la matrice des éveils. Ils doivent être tranchés avant le
portage des quêtes et des badges, pas avant la réalisation du socle événementiel et des états de
pièce.
