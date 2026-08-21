# Guides dans Intuition — conversations, métaparcours et badges de seuil

> **Ajout Codex — 2026-08-20. Amendement canonique.**
> Cette note déplace la résidence des Guides de Communication vers Intuition et précise les effets
> sur le métaparcours, les conversations et les badges. Elle complète
> [espace-echange-m0-conservation-guides.md](espace-echange-m0-conservation-guides.md). La décision
> antérieure d’un fil unique demeure l’état applicatif actuel ; la cible décrite ici introduit un
> historique de conversations et doit faire l’objet d’une analyse d’impact avant portage.

## 1. Décision

Les Guides résident dans **Intuition — Je discerne**.

- le Professeur Sirbey porte le regard de la Lumière : il relie, structure et donne de la hauteur ;
- le Docteur Z.E.R.O. porte le regard de l’Ombre : il doute, révèle les contradictions et soulève
  ce qui reste sous le tapis.

La forme de leur interaction est conversationnelle, mais sa finalité n’est pas la mise en relation
entre Joueurs. La Communication accueille donc les échanges humains, tandis que l’Intuition
accueille les deux regards qui aident à lire le Jeu et le Point Zéro.

## 2. Architecture UX cible

### 2.1. Une page de référence dans Intuition

La page **Guides** devient l’adresse stable des conversations :

- panneau latéral d’historique, repliable ;
- création d’un nouveau dialogue ;
- titre généré automatiquement puis modifiable ;
- archivage et suppression ;
- citations intégrées au texte de la réponse lorsque le Guide en mobilise ;
- bascule entre Professeur et Docteur dans un même fil.

> **Ajout Codex — arbitrage du 20 août 2026.** La page n’affiche pas d’encart ou de pastille
> nommant une source précise tant que le serveur ne sait pas tracer les documents réellement
> mobilisés pour produire chaque réponse. Une liste déduite du corpus entier ou choisie
> éditorialement créerait une fausse promesse de traçabilité. Un affichage structuré des sources
> pourra revenir avec un véritable suivi de citations ; jusque-là, seules les citations présentes
> dans le texte de la réponse font foi.

Changer de voix ne crée pas automatiquement une nouvelle conversation. Le fil insère un marqueur
narratif clair — par exemple « Le Docteur reprend le fil » — puis transmet le même historique à la
voix choisie.

Le dévoilement reste progressif : le premier écran demande seulement de choisir un regard et de
commencer. `Nouveau dialogue` apparaît après le premier échange ; l’historique latéral devient utile
et visible à partir du deuxième fil. Recherche, dossiers et classement avancé sont reportés.

Le titre est généré par le LLM **une seule fois**, après la première réponse. Cet appel entre dans
le plafond LLM partagé. Il ne bloque jamais le dialogue : plafond atteint, lenteur ou échec, la
conversation s’ouvre avec un titre dérivé du premier message. Une génération tardive ne remplace
jamais un titre déjà modifié par le Joueur.

### 2.2. Une bulle transversale après découverte

Après le premier échange réussi, les Guides restent accessibles en bas de chaque page :

- reprise du fil actif ;
- quelques messages récents et champ de réponse ;
- changement de regard ;
- `Ouvrir la conversation` ;
- `Nouveau dialogue`.

La bulle est un raccourci vers le même système, jamais une seconde messagerie. Sur mobile, elle
devient une feuille plein écran ; l’historique reste accessible par un bouton ou un tiroir.

Depuis une page fonctionnelle, la conversation peut recevoir un contexte explicite et révocable,
par exemple `Contexte utilisé : Ma Fresque de Récit ×`. Aucun contexte n’est ajouté silencieusement.

### 2.3. Suppression et mémoire

Trois gestes restent distincts :

1. archiver une conversation la retire de la liste courante sans l’effacer ;
2. supprimer une conversation efface ses messages selon la politique annoncée ;
3. gérer ce que les Guides peuvent relire relève du centre **Personnalisation et mémoires**.

La suppression d’un fil ne retire ni un badge déjà acquis, ni l’accès à la bulle, ni les autres
conversations. Si toutes les conversations sont supprimées, le Joueur peut en ouvrir une nouvelle.

Les conversations sont conservées sans limite propre tant que le compte existe, jusqu’à leur
suppression volontaire par le Joueur. Deux gestes doivent rester disponibles : supprimer une
conversation précise et tout effacer en une fois. La suppression du compte efface l’ensemble selon
les garanties déjà définies pour le fil actuel.

Cette cible amende la politique de fil unique décrite le 18 août. Avant code, il faut trancher la
migration des messages existants vers une première conversation et aligner export, suppression du
compte, sauvegardes et journalisation.

## 3. Effet sur le métaparcours du Monde 0

### 3.1. Intuition

La première séquence devient :

```text
Choisir un regard
→ mener un premier échange significatif
→ activer la bulle transversale
→ découvrir une première fiche Point Zéro
→ répondre à son questionnaire et conserver une Trace
→ explorer les événements
```

Après le premier échange, la carte Intuition ne reste pas figée sur les Guides. Elle affiche un
usage courant — reprendre une conversation — jusqu’à ce que l’invitation suivante, par exemple une
fiche Point Zéro, la réactive avec son illustration dédiée.

### 3.2. Communication

La séquence devient :

```text
Configurer mon Profil communautaire
→ entrer dans l’Espace d’échange du Monde 0
→ se présenter ou produire une première Résonance
→ découvrir l’Annuaire
→ demander un échange individuel, avec approbation
```

Le retrait des Guides rend la progression plus lisible : Communication commence quand le Joueur
choisit ce qu’il rend visible et entre effectivement en relation avec d’autres personnes.

### 3.3. Monde 1

Les Guides restent dans Intuition et leur bulle reste transversale. Le Monde 1 n’oblige pas à les
redécouvrir. Intuition ouvre ensuite les ressources externes, les Personnes Sources et les premières
lectures systémiques. Communication ouvre les espaces du Seuil et du Cercle, puis les gestes
collectifs.

### 3.4. Libellés canoniques des deux cartes de départ

Ces textes remplacent les bases antérieures du fichier de configuration Monde 0.

#### Communication — base Profil communautaire

- **titre** : `Choisis ce que tu montres de toi`
- **accroche** : `Avant d’entrer dans la communauté, décide depuis quelle place tu veux être découvert.`
- **CTA** : `Composer mon profil`
- **retour après appropriation** : `Revoir mon profil`
- **texte déplié** : `Choisis ce que les autres Joueurs découvrent de toi. Cette présence ouvre l’Espace d’échange, puis l’Annuaire.`
- **badge de seuil** : `Présence choisie`, attribué lorsque le Joueur confirme son Profil
  communautaire et ses choix de visibilité. Une simple ouverture ou prévisualisation ne suffit pas.

Après confirmation du Profil, la carte se réouvre ainsi :

- **titre** : `Entre dans l’Espace d’échange`
- **accroche** : `Tu sais maintenant ce que tu montres de toi. Découvre les voix des autres Joueurs.`
- **CTA** : `Entrer dans l’Espace d’échange`

Après que le Joueur a rejoint l'Espace d'échange, la carte se réouvre une seconde fois :

- **titre** : `Découvre qui joue déjà`
- **accroche** : `Des milliers de chemins possibles. Des personnes bien réelles. Découvre celles qui ont choisi de prendre place dans le Jeu.`
- **CTA** : `Explorer l’Annuaire`

Cette troisième invitation ne crée pas un nouveau badge de seuil. Elle révèle un usage durable
de Communication après le geste fondateur déjà reconnu par **Présence choisie**.

#### Intuition — base Guides

- **sur-titre de la page Guides** : `INTUITION · PREMIER REGARD`
- **titre** : `Choisis par quel regard commencer`
- **accroche** : `Le Professeur Sirbey éclaire la carte. Le Docteur Z.E.R.O. en révèle les angles morts. Ils t’expliqueront comment trouver ta place dans l’écosystème dans leur style… inimitable.`
- **CTA** : `Choisir un regard`
- **badge de seuil** : `Première clé de discernement`, attribué après un premier échange complet
  avec le Professeur ou le Docteur : un message du Joueur et une réponse du Guide ont été
  persistés avec succès.

Après le premier échange abouti, la carte se réouvre vers Point Zéro :

- **titre** : `Apprends à voir ce qui agit derrière ce que tu vois`
- **accroche** : `Dix clés pour entrer dans la grammaire du Point Zéro. Lis, mets à l’épreuve, puis garde ce qui change réellement ton regard.`
- **CTA** : `Découvrir les clés du Point Zéro`

L’Observatoire reste une destination cible d’Intuition, mais n’entre ni dans le YAML ni dans le
sous-menu tant qu’il ne possède pas de route, de contrôleur et de page. Il pourra être révélé au
Monde 1 ou plus tard sans modifier la résidence générale du territoire.

Dans la liste compacte des sept Puissances, les trois repères d’Intuition sont
**`Point Zéro · guides · ressources`**. `Point Zéro` reste la tête du territoire ; `guides` rend
visible la nouvelle porte ; `ressources` rassemble les fiches, événements et horizons sans
surcharger la navigation. Communication affiche symétriquement
**`Échanges · profil communautaire · annuaire`**.

### 3.5. Contrat de la destination Événements

`Événements` désigne ici une page interne au Jeu. Le lien d’Intuition ne cible pas l’index public
`/evenements`, rendu avec la coque du site. Il attend un index dédié — par exemple
`/jeu/evenements` — avec le layout du Jeu, le sous-menu Intuition et les mêmes sources de données
que les événements existants. Le contrat complet et les critères de recette sont fixés dans
[lot-editorial-coque-m0-2026-08-20.md](lot-editorial-coque-m0-2026-08-20.md).

## 4. Badges de seuil

### 4.1. Règle générale

> **Arbitrage Boris — 2026-08-20.** Un badge de seuil reconnaît le geste fondateur qui fait entrer
> dans une Puissance. Les étapes internes suivantes font évoluer la carte et ouvrent des usages,
> sans multiplier les badges de seuil. La constellation canonique reste donc composée d’un seuil
> par Puissance.

Le déplacement des Guides recompose les seuils de Communication et d’Intuition :

- **Communication — Présence choisie** : confirmer son Profil communautaire et ses choix de
  visibilité ;
- **Intuition — Première clé de discernement** : mener un premier échange complet avec l’un des
  deux Guides.

Les accomplissements plus avancés restent possibles, mais ne sont pas des badges de seuil.
**Première grammaire acquise**, obtenu après les dix clés Point Zéro, devient ainsi un
accomplissement d’appropriation dans Intuition.

### 4.2. Premier échange avec les Guides : seuil d’Intuition

Le premier échange complet active le territoire Guides, la bulle transversale et le badge de seuil
**Première clé de discernement**. Échanger avec un seul Guide suffit : le seuil reconnaît l’entrée
dans le discernement, pas l’exploration exhaustive des deux voix.

Événement recommandé pour cette transition :

```text
premier message du Joueur persisté
+ première réponse du Guide persistée avec succès
= Guides découverts, bulle activée et seuil Intuition franchi
```

Ne déclenchent pas cette transition : visiter la page, choisir une voix, créer un fil vide, ouvrir
la bulle, changer de Guide, archiver ou supprimer une conversation.

L’événement métier doit être idempotent, par exemple `first_guide_exchange_completed_at`. Il ne
valide aucune expérience. Le seuil constate le geste sans attribuer d’Oméga ; cette absence de
montant fait partie du contrat à tester.

Un badge caché **Le Double Regard** pourra reconnaître plus tard un dialogue réel avec le
Professeur et avec le Docteur. Il n’est ni un seuil, ni une condition du Monde 0, ni un prérequis
d’ouverture.

### 4.3. Communication

La sortie des Guides libère le premier seuil de Communication pour une action proprement
relationnelle :

| Geste | Effet | Condition |
|---|---|---|
| Profil communautaire confirmé | badge de seuil **Présence choisie** | le Joueur enregistre ses choix de visibilité et sa présentation minimale |
| Entrée dans l’espace | état de carte et nouvel usage courant | adhésion effective et autorisée à l’espace ; une prévisualisation ne suffit pas |
| Annuaire découvert | état de carte, sans badge obligatoire | première visite de l’Annuaire |
| Demande d’échange | pas de badge de seuil en M0 | demande consentie envoyée puis traitée selon les droits |

Le Profil est le geste fondateur de Communication : le Joueur choisit la place depuis laquelle il
sera découvert avant d’entrer en relation. L’Espace d’échange et l’Annuaire poursuivent ensuite le
métaparcours sans créer de nouveaux seuils.

### 4.4. Intuition après les Guides

Lire une fiche ne suffit pas à créer un accomplissement d’appropriation. La soumission du
questionnaire produit une Trace et alimente l’état `clé assimilée`. Le sceau historique
**Clé conservée** ne constitue plus un badge de seuil : la première clé est une étape du
métaparcours, déjà rendue visible par la Trace. L’accomplissement
**Première grammaire acquise** reste conditionné à dix clés assimilées. Les événements restent
accessibles sans badge de simple visite ; une inscription ou une participation réelle pourra
recevoir son propre accomplissement si le système sait la vérifier.

## 5. Migration et recette

### 5.1. Migration sans perte

- **un geste ne produit jamais deux sceaux visibles** ;
- l’audit du 20 août ne trouve aucun détenteur réel de **Dialogue ouvert** : l’entrée peut donc
  sortir du catalogue actif et son marqueur `m0-dialogue-guides` devient la source unique du seuil
  Intuition **Première clé de discernement** ;
- si un détenteur apparaissait entre l’audit et la mise en production, **Dialogue ouvert** serait
  conservé comme équivalent historique du seuil Intuition et empêcherait l’affichage simultané de
  **Première clé de discernement** ; il compterait une seule fois dans la constellation ;
- **Clé conservée** sort des badges de seuil. S’il n’a aucun détenteur, il peut sortir du catalogue
  actif ; sinon il reste un accomplissement historique sans compter dans la constellation ;
- **Première grammaire acquise** reste acquis et visible comme accomplissement d’appropriation ;
- le seuil Communication **Présence choisie** est obtenu au prochain enregistrement confirmé du
  Profil, ou reconnu à partir d’une confirmation déjà persistée, sans rejouer les callbacks ;
- migrer l’ancien fil commun comme première conversation, sans en dupliquer les messages.

Immédiatement avant modification de `config/seuils.yml`, refaire l’audit des détenteurs réels de
**Dialogue ouvert** et **Clé conservée**. La migration doit distinguer l’équivalence d’un état
historique, l’affichage d’un sceau et son comptage dans la constellation.

### 5.2. Critères d’acceptation

1. Les Guides apparaissent dans le sous-menu Intuition et plus dans Communication.
2. La bulle et la page dédiée lisent et écrivent dans les mêmes conversations.
3. Le passage Professeur ↔ Docteur conserve le fil et ajoute un marqueur visible.
4. Une visite, un choix de voix ou un fil vide ne donne aucun badge.
5. Le premier échange complet active une seule fois la bulle et le seuil Intuition.
6. Supprimer une conversation ne retire aucun accomplissement ni l’accès aux Guides.
7. Un échange Guide ne produit jamais deux sceaux visibles et les seuils n’attribuent aucun Oméga.
8. Communication commence par le Profil communautaire, puis l’Espace d’échange.
9. La page explique clairement différence entre archive, suppression et mémoire.
10. Les droits, l’export et les suppressions sont testés avant activation de l’historique multiple.

## 6. Analyse d’impact requise

Avant implémentation, compléter la matrice pour `GuideMessage` ou son successeur, conversations,
propriétaire, voix active, historique, sources, consentements, export, suppression du compte,
sauvegardes et attribution des badges. La page et la bulle ne doivent pas fabriquer un second
système de messages ni contourner les droits de la messagerie existante.
