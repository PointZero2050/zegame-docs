# E19 rang 3 — Carte du Seuil : contrat de stockage et de rendu

Note du portable, 10 septembre 2026, en réponse à la demande de Codex dans
[`m0-e19-raccord-des-gestes.md`](m0-e19-raccord-des-gestes.md) : « Le portable vérifie d'abord si
les mécanismes existants de publication de Graine et de visibilité couvrent ce besoin. **Il expose
ce qui manque avant d'ajouter un stockage.** »

Mesuré sur `preprod@f2696a3`. Rien n'a été écrit : ce document précède l'implémentation.

## 1. Ce qui existe déjà, et qui couvre

**`RegistreDesTraces` est l'agrégateur canonique des productions, et il est complet.** Cinq
familles, toutes alimentées par des sources réelles :

| famille | sources |
|---|---|
| `territoire` | `Trace` · `ExperienceQuizAttempt` (completed) · `CoupableIdealSession` (completed, avec `result`) · `Traversee` (completed, avec `fin_id`) · `ConseilSession` (completed) |
| `retour` | `ChallengesUser` porteur d'un `retour` |
| `diagnostic` | `MoteurAssessment` (completed) |
| `positionnement` | `ConseilSession` (completed) |

Il expose déjà `pour(user)`, `entree_de(user, type, id)` — qui ne cherche que dans le registre du
joueur, donc **l'appartenance est vraie par construction** — et `visibles_pour_le_profil(user)`.

**`VisibiliteDeTrace` est le patron exact de « choisir les éléments à montrer »** : un pointeur
(`source_type`, `source_id`), un booléen, une ligne par dérogation, et surtout la doctrine —
« cette table ne dit pas ce qu'est une Trace, seulement ce que le joueur a décidé d'en montrer ».
`regler_visibilite!` n'écrit **que** la dérogation : aucune validation, aucun Ω.

**`GrainePubliee`** porte la publication volontaire d'UNE Graine sur le profil communautaire, et
elle est réversible. Une Graine, elle, ne se stocke pas : c'est un message dans le fil d'un
`ChallengesUser` ou du fil Fresque — « un état se lit, il ne se stocke pas ».

## 2. Ce qui manque, et pourquoi ce n'est pas dérivable

**Le trou n'est pas la sélection : c'est que la sélection existante répond à une AUTRE question.**

`VisibiliteDeTrace.visible = true` veut dire « mon **profil** montre cette production » —
`phrase_de_visibilite` l'écrit en toutes lettres : « publiée sur ton profil » contre « privée ».
Composer une Carte veut dire « **cette Carte** montre cette production ». Les deux questions
portent sur les mêmes objets et ne se déduisent pas l'une de l'autre :

- réutiliser la table de visibilité pour composer la Carte ferait de « Sceller » une
  **publication implicite au profil** — ce que le contrat interdit explicitement ;
- inversement, dériver la Carte de ce qui est déjà visible donnerait une Carte **vide** pour la
  quasi-totalité des joueurs : les quatre interrupteurs de famille sont **éteints par défaut**
  (mesuré : `territoire=false · retour=false · diagnostic=false · positionnement=false`).

**Une composition est un CHOIX, pas un état** : elle ne se lit nulle part, elle doit donc être
stockée — c'est la même famille que `VisibiliteDeTrace` et `PartageCoordonnees`, et non une
entorse à « un état se lit ». **Le sceau, lui, est un FAIT** : même nature que `m0-cloture`.

## 3. Le stockage proposé — une table, un marqueur, rien d'autre

**`compositions_de_carte`** — le patron `VisibiliteDeTrace`, trait pour trait :

    user_id       référence
    source_type   chaîne     ] ensemble unique par (user_id, source_type, source_id)
    source_id     entier     ]

*La présence de la ligne EST la sélection.* Pas de booléen : contrairement à la visibilité, il n'y
a pas de valeur par défaut à contredire — rien n'est sur la Carte tant que le joueur ne l'y met
pas. Pas de `carte_id` non plus : « **ta** Carte du Seuil », une par passage.

**Aucun `belongs_to :source, polymorphic:`** — pour la raison que `VisibiliteDeTrace` écrit
elle-même : cela inviterait à charger une production DEPUIS la composition, donc à contourner le
registre, seul endroit qui sache ce qui EST une production. La résolution passe par
`RegistreDesTraces.entree_de`, qui vérifie l'appartenance par construction.

**Le sceau** : un `MarqueurDAttention` `m0-carte-scellee`. Il porte sa date, il est idempotent, et
il ne demande aucune table. La **reprise** n'est alors rien d'autre que relire les lignes de
composition — il n'y a pas de second état à conserver.

**Aucun stockage de publication.** La Carte est privée, et le contrat dit « pas de publication
implicite au clic Sceller ». Tant qu'aucune surface de publication n'est arbitrée, ne rien prévoir
pour elle : une colonne `publiee` inutilisée finirait par être lue.

## 4. Le rendu — un service de lecture

`CarteDuSeuil`, lecture seule sauf deux points d'écriture explicites, comme `Graine` :

- `composables(user)` → ce qui peut entrer sur la Carte : les entrées du registre **plus** les
  Graines du joueur. ⚠️ Les Graines ne sont **pas** des Traces — le registre l'écrit — la Carte
  est donc le premier objet qui les rassemble ; c'est un point à trancher, pas à supposer (§5).
- `composition(user)` → le sous-ensemble choisi, résolu par `RegistreDesTraces.entree_de`, avec
  une **représentation honnête de ce qui a disparu** : une production supprimée depuis la
  composition doit se dire, jamais se taire (patron `Carte#disponible?`).
- `scellee?(user)` / `scellee_le(user)`.
- `composer!(user, entree, dedans)` — écrit **une** ligne, et rien d'autre. Ne touche jamais
  `VisibiliteDeTrace`.
- `sceller!(user)` — pose le marqueur. Aucun Ω, aucune validation, aucun accès M1.

**Le vide se dit** : `composables` vide → l'écran renvoie à sa source, il ne propose pas de
sceller. `composition` vide → sceller est refusé ; une Carte sans contenu n'est pas une Carte.

⚠️ **Piège de nom.** `app/models/carte.rb` existe déjà et n'a **aucun** rapport : c'est le contrat
d'affichage des cartes de fil (Rencontre, Graine publiée, Sondage). Le service de la Carte du Seuil
ne doit ni s'y greffer ni reprendre son nom nu.

## 5. Ce que le portable ne décide pas

**Le rang 3 se valide-t-il par le sceau, ou reste-t-il déclaratif ?** Aujourd'hui les gestes se
confirment par `ConfirmationDeGeste` (`POST .../gestes/:rang/confirmer`), et `rangs_prouves` ne
liste que des preuves serveur. Faire du sceau une preuve serveur est cohérent — le geste EST
l'écran — mais cela change l'autorité du rang 3. **Arbitrage Codex.**

**Les Graines entrent-elles sur la Carte ?** Le canon d'E19 dit « Relis la Graine, choisis les
éléments que tu souhaites partager ». Si la Graine de passage est le socle et les productions les
éléments, alors la Carte porte une Graine + une sélection, et non une sélection homogène. La
composition ci-dessus le permet (le `source_type` d'une Graine est `Messaging::Message`, déjà
utilisé par `PartageDeRecit`), mais **le modèle éditorial se tranche avant le code**.

## 6. Recette de ce lot, quand il viendra

Compte réellement arrivé à E19, Atelier en attente. Prévisualisation **sans aucune écriture**
(le GET ne crée rien) · enregistrement explicite, repris au rechargement · la Carte reste
**privée** : `visibles_pour_le_profil` inchangé avant et après le sceau, et `VisibiliteDeTrace`
sans nouvelle ligne · aucun Ω, aucune validation d'Atelier, aucun accès M1 déclenché · aucune
écriture dans le compte d'un autre joueur · une production retirée après composition se dit
indisponible au lieu de disparaître · Carte vide → sceller refusé.

⚠️ **Le décor doit PRODUIRE, pas seulement valider.** Mesuré en préparant cette note : un compte
dont les 18 expériences précédentes sont passées par `mark_as_ended!` a **zéro** entrée au
registre. Le registre liste des productions réelles, pas des validations — un banc qui monte son
décor par validations verrait une Carte vide et l'appellerait « conforme ».
