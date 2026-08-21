# Analyse d'impact — le dialogue mentor devient un journal continu

> **Claude (portable), 2026-08-20.** Demandée par
> [`ux-dialogue-mentor-continu.md`](ux-dialogue-mentor-continu.md), « Contrat d'intégration » :
> *« Avant portage Rails, vérifier la source de vérité des messages du mentor, l'identifiant de
> contexte disponible à l'ouverture, les droits de lecture par catégorie et le mécanisme réel de
> création d'une Graine. »* Établie sur `pointzero-app`, code lu et base mesurée.

## 1. La conclusion d'abord

**La cible est déjà à 80 % en place, et le reste est petit.** Contrairement au chantier des
Guides, il n'y a ici ni refonte de stockage ni notion nouvelle : le mentor a **déjà** un fil
unique, continu, par joueur — c'est exactement ce que Codex canonise. Ce qui manque tient en
**une colonne** et en **deux lectures**.

| Exigence Codex | État réel |
|---|---|
| Journal continu, un seul fil | ✅ **déjà le modèle** : `MentorMessage` scopé par `user`, ordonné |
| Distinct des Guides (multi-conversations) | ✅ deux modèles séparés, aucun couplage |
| Catégorie choisie par le joueur (`Graine`/`Voyage`/`Moteur`/`Autre`) | ❌ **une colonne à poser** |
| « Un LLM ne devine jamais la catégorie » | ✅ garanti par construction si la colonne est écrite par le contrôleur |
| Identifiants de contexte (parcours, expérience, Graine, Trace) | ⚠️ **rien de stocké** — voir §3 |
| Sources citées au message | ⚠️ le service les CALCULE déjà, il ne les garde pas |
| Panneau `Sources et mémoire` | ✅ `AutorisationLlm.categories_lisibles(user, usage: :mentor)` le sert déjà |
| Consentement initial, non rappelé à chaque message | ✅ modèle croisé en vigueur depuis le 18 août |
| Graine proposée, jamais plantée sans confirmation | ✅ `Graine.semer!` est un point d'écriture explicite |
| Changement de mentor = nouveau chapitre, historique conservé | ❌ **rien** — voir §4 |

## 2. Le fait qui rend ce chantier confortable

**Production : 0 ligne `MentorMessage`, 0 joueur.** (16 lignes en préprod, toutes de bancs.)

Comme pour les Guides, **il n'y a rien à migrer** : les colonnes nouvelles peuvent être posées
`NOT NULL` avec un défaut, sans reprise ni compromis d'héritage. Et le risque de se tromper est
faible : personne n'a encore de journal à préserver.

⚠️ Ce chiffre est **daté**. Il se revérifie juste avant le portage — c'est la leçon du
19 août, où un décor créé entre deux sessions a changé la réponse.

## 3. Ce qu'il faut poser, par ordre de coût

### 3.1. La catégorie — une colonne, et c'est tout

```ruby
add_column :mentor_messages, :categorie, :string, default: "graine", null: false
```

`CATEGORIES = %w[graine voyage moteur autre]`, validées en inclusion. Écrite par le
contrôleur depuis le menu, **jamais par le service** : c'est ce qui garantit mécaniquement la
règle de Codex (« un LLM ne remplace jamais le choix explicite du joueur »). Le défaut
`graine` correspond à la valeur par défaut du menu.

Elle qualifie **l'échange**, donc elle se pose sur le message du joueur ; la réponse du mentor
hérite de celle de la question à laquelle elle répond.

### 3.2. Le contexte d'ouverture — la vraie question à trancher

Codex écrit : *« L'application peut lui associer les identifiants de contexte déjà connus
(parcours, expérience, Graine ou Trace depuis laquelle le dialogue a été ouvert). »*

**Rien de tel n'existe aujourd'hui** : on ouvre `/mentor` sans dire d'où l'on vient. Deux
chemins, et je recommande le second :

1. **Colonnes dédiées** (`contexte_type`, `contexte_id`) — polymorphe, propre, mais c'est un
   objet de plus à maintenir pour une information qu'aucune lecture ne consomme encore.
2. **Rien pour l'instant.** La catégorie suffit à qualifier l'échange, et le contexte se
   déduira quand une page l'ouvrira réellement avec un `?depuis=`. **YAGNI jusqu'au premier
   consommateur** — c'est la règle qu'on a appliquée aux exceptions de Traces, et elle a tenu.

### 3.3. Les sources citées au message

`MentorReponse` **calcule déjà** ce qu'il a le droit de lire (`categories_lisibles`), mais ne
le conserve pas : on ne peut donc pas afficher, six mois plus tard, ce qui avait nourri une
réponse. Deux options :

- **Colonne `sources` (jsonb)** sur le message du mentor, écrite à la réponse. Honnête et
  durable, et c'est ce que la maquette montre au niveau du message.
- Recalculer à l'affichage — **à écarter** : les autorisations changent, et on afficherait
  alors les sources d'aujourd'hui à côté d'un message d'hier. Ce serait un mensonge.

**Recommandation : la colonne.** C'est la seule façon que la citation reste vraie.

### 3.4. Le changement de mentor — un séparateur, pas une rupture

Codex : *« nouveau chapitre narratif sans effacer l'historique »*. Le patron existe déjà et il
est éprouvé : c'est le rôle `bascule` de `GuideMessage`, une ligne qui **s'affiche et ne
s'envoie jamais au modèle**. Le même ici : un rôle `chapitre`, posé quand `heros_slug` change,
portant le nom du nouveau mentor.

⚠️ Il faut alors **exclure ce rôle de `messages_pour_api`**, exactement comme la césure des
Guides — sans quoi le modèle lirait une didascalie comme une parole.

## 4. Ce que la maquette ne doit PAS pouvoir faire

Le contrat de Codex est explicite et je le confirme, avec les garde-fous qui existent déjà :

| Geste de la maquette | Le garde-fou réel |
|---|---|
| Proposer une Graine | `Graine.semer!` est un point d'écriture explicite ; la proposition reste un texte tant que le joueur ne confirme pas |
| Valider une expérience | aucun chemin depuis le mentor, et il ne doit pas en naître |
| Attribuer un Oméga | les Ω sont calculés depuis les validations, jamais posés à la main |
| Lire une catégorie non consentie | `AutorisationLlm.permet?(user, usage: :mentor, categorie:)` — les quatre verrous |

**Un point de vigilance** : la Graine proposée dans le fil naîtra sous le régime **opt-out**
(arbitrage du 19 août) — donc publiée d'office sur le profil. Pour une Graine née d'un
dialogue intime avec le mentor, cela mérite d'être **dit au joueur au moment de la
confirmation**, ou arbitré autrement. C'est la seule question produit de ce lot.

## 5. Ce que je propose

1. **Poser la catégorie** (§3.1) et le **rôle `chapitre`** (§3.4) : une migration additive,
   deux exclusions dans le service, un banc. Une demi-journée, sans risque.
2. **Poser `sources`** (§3.3) dans la même migration — c'est maintenant qu'elle coûte le
   moins, et sans elle la maquette affiche une information fausse.
3. **Ne rien poser pour le contexte d'ouverture** (§3.2) tant qu'aucune page ne l'envoie.
4. **Trancher la Graine du mentor face à l'opt-out** — arbitrage de Boris, seul point produit.

## 6. Addendum : proposition structurée et plantation explicite

> **Ajout Codex — 21 août 2026.** L'opt-out a depuis été tranché : la visibilité est proposée
> cochée, mais reste modifiable avant plantation. Le point restant est la liaison entre une
> réponse du mentor et une formulation candidate.

La colonne `categorie` ne suffit pas : elle exprime ce que le Joueur veut explorer, pas la décision
du mentor de proposer une formulation. La réponse doit donc porter un signal structuré facultatif
`proposition_graine`, validé côté serveur et rattaché à l'identifiant du `MentorMessage` source.

### Matrice d'impact de cette écriture

| État visible | Source de vérité | Droit | Événement de transition |
|---|---|---|---|
| carte **Graine possible** | proposition valide rattachée au message mentor courant | propriétaire du journal uniquement | réponse mentor persistée avec signal structuré valide |
| formulation relue | texte candidat édité côté Joueur | propriétaire uniquement | sauvegarde ou envoi de la confirmation |
| Graine plantée | lecture canonique de `Graine.semer!` et identifiant résultant conservé | propriétaire uniquement | POST explicite, idempotent |
| visibilité communautaire | réglage confirmé au moment de planter | propriétaire ; lecture selon règles du profil | création de la Graine avec visibilité choisie |

### Garde-fous de portage

- ne pas écrire directement dans le conteneur sous-jacent résolu par `Graine` ; passer par
  `Graine.semer!` et ses callbacks existants ;
- vérifier la propriété du `MentorMessage` source et de la proposition ;
- refuser une seconde plantation si un identifiant de Graine résultante est déjà présent ;
- ne déclencher ni validation de `ChallengesUser`, ni callback Oméga ;
- ne jamais sérialiser le contenu du dialogue privé dans la Graine publique ;
- tester le double POST, la proposition d'un autre Joueur, le signal LLM invalide et le retrait de
  visibilité avant confirmation.

Route sémantique recommandée : `POST /mentor/propositions/:id/planter`. Le nom Rails final peut
suivre les conventions du dépôt ; le contrat est le geste explicite, pas cette chaîne littérale.
