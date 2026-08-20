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
- titre automatique modifiable ;
- archivage et suppression ;
- affichage des sources publiques utilisées ;
- bascule entre Professeur et Docteur dans un même fil.

Changer de voix ne crée pas automatiquement une nouvelle conversation. Le fil insère un marqueur
narratif clair — par exemple « Le Docteur reprend le fil » — puis transmet le même historique à la
voix choisie.

Le dévoilement reste progressif : le premier écran demande seulement de choisir un regard et de
commencer. `Nouveau dialogue` apparaît après le premier échange ; l’historique latéral devient utile
et visible à partir du deuxième fil. Recherche, dossiers et classement avancé sont reportés.

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
- **badge du territoire** : `Présence ouverte`, attribué uniquement lors de l’entrée effective
  dans l’Espace d’échange, jamais à la confirmation du Profil.

Après confirmation du Profil, la carte se réouvre ainsi :

- **titre** : `Entre dans l’Espace d’échange`
- **accroche** : `Tu sais maintenant ce que tu montres de toi. Découvre les voix des autres Joueurs.`
- **CTA** : `Entrer dans l’Espace d’échange`

#### Intuition — base Guides

- **titre** : `Choisis par quel regard commencer`
- **accroche** : `Le Professeur Sirbey éclaire la carte. Le Docteur Z.E.R.O. en révèle les angles morts. Ils t’expliqueront comment trouver ta place dans l’écosystème dans leur style… inimitable.`
- **CTA** : `Choisir un regard`
- **badge du territoire** : `Première grammaire acquise`, attribué uniquement après les dix clés
  assimilées. Le premier échange avec un Guide ne porte aucun badge.

Après le premier échange abouti, la carte se réouvre vers Point Zéro :

- **titre** : `Apprends à voir ce qui agit derrière ce que tu vois`
- **accroche** : `Dix clés pour entrer dans la grammaire du Point Zéro. Lis, mets à l’épreuve, puis garde ce qui change réellement ton regard.`
- **CTA** : `Découvrir les clés du Point Zéro`

L’Observatoire reste une destination cible d’Intuition, mais n’entre ni dans le YAML ni dans le
sous-menu tant qu’il ne possède pas de route, de contrôleur et de page. Il pourra être révélé au
Monde 1 ou plus tard sans modifier la résidence générale du territoire.

## 4. Badges de seuil

### 4.1. Règle générale

Le déplacement des Guides ne crée ni ne déplace aucun badge existant. Dans les prototypes de
référence, le dialogue avec les Guides n’attribue pas de badge : **Présence ouverte** est obtenu lors
de l’entrée effective dans l’Espace d’échange, et **Première grammaire acquise** après l’assimilation
des dix clés Point Zéro. Ces deux accomplissements conservent leur Puissance et leur condition.

Le principe général reste : une page déplacée ne recrée pas un accomplissement, un état historique
n’est jamais rejoué et aucun gain d’Oméga n’est rappelé.

### 4.2. Premier échange avec les Guides : état de découverte, sans badge

Le premier échange complet active le territoire Guides et la bulle transversale. C’est un état de
dévoilement de l’interface, pas un accomplissement récompensé.

Événement recommandé pour cette transition :

```text
premier message du Joueur persisté
+ première réponse du Guide persistée avec succès
= Guides découverts et bulle activée
```

Ne déclenchent pas cette transition : visiter la page, choisir une voix, créer un fil vide, ouvrir
la bulle, changer de Guide, archiver ou supprimer une conversation.

L’événement métier doit être idempotent, par exemple `first_guide_exchange_completed_at`. Il ne
valide aucune expérience et n’attribue ni badge ni Oméga.

Un badge caché pour avoir réellement dialogué avec les deux regards pourra être envisagé plus tard.
Il n’est ni une condition du Monde 0, ni un prérequis d’ouverture.

### 4.3. Communication

La sortie des Guides libère le premier seuil de Communication pour une action proprement
relationnelle :

| Geste | Effet | Condition |
|---|---|---|
| Profil communautaire confirmé | état intermédiaire du métaparcours, sans badge | le Joueur enregistre ses choix de visibilité et sa présentation minimale |
| Entrée dans l’espace | badge de seuil **Présence ouverte** | adhésion effective et autorisée à l’espace ; une prévisualisation ne suffit pas |
| Annuaire découvert | état de carte, sans badge obligatoire | première visite de l’Annuaire |
| Demande d’échange | pas de badge de seuil en M0 | demande consentie envoyée puis traitée selon les droits |

`Présence ouverte` reste le badge canonique de l’Espace d’échange défini dans
[espace-echange-m0-conservation-guides.md](espace-echange-m0-conservation-guides.md). La
configuration du Profil est l’invitation qui y conduit ; elle ne multiplie pas les récompenses.

### 4.4. Intuition après les Guides

Lire une fiche ne suffit pas à créer un badge d’appropriation. La soumission du questionnaire
produit une Trace et alimente l’état `clé assimilée`. Le badge **Première grammaire acquise** reste
conditionné à dix clés assimilées. Les événements restent accessibles sans badge de simple visite ;
une inscription ou une participation réelle pourra recevoir son propre accomplissement si le
système sait la vérifier.

## 5. Migration et recette

### 5.1. Migration sans perte

- ne migrer aucun badge à cause du déplacement des Guides ;
- conserver `Présence ouverte` dans Communication et `Première grammaire acquise` dans Intuition ;
- ne jamais réattribuer ces badges et ne jamais rappeler les callbacks d’Omégas ;
- migrer l’ancien fil commun comme première conversation, sans en dupliquer les messages.

### 5.2. Critères d’acceptation

1. Les Guides apparaissent dans le sous-menu Intuition et plus dans Communication.
2. La bulle et la page dédiée lisent et écrivent dans les mêmes conversations.
3. Le passage Professeur ↔ Docteur conserve le fil et ajoute un marqueur visible.
4. Une visite, un fil vide ou un premier échange ne donne aucun badge.
5. Le premier échange complet active la bulle une seule fois.
6. Supprimer une conversation ne retire aucun accomplissement ni l’accès aux Guides.
7. `Présence ouverte` et `Première grammaire acquise` restent visibles sans double gain d’Omégas.
8. Communication commence par le Profil communautaire, puis l’Espace d’échange.
9. La page explique clairement différence entre archive, suppression et mémoire.
10. Les droits, l’export et les suppressions sont testés avant activation de l’historique multiple.

## 6. Analyse d’impact requise

Avant implémentation, compléter la matrice pour `GuideMessage` ou son successeur, conversations,
propriétaire, voix active, historique, sources, consentements, export, suppression du compte,
sauvegardes et attribution des badges. La page et la bulle ne doivent pas fabriquer un second
système de messages ni contourner les droits de la messagerie existante.
