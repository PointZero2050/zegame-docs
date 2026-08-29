# Messagerie M1 — inventaire de la surface existante

*Relevé du poste fixe, 29 août 2026. Compagnon de
[`messagerie-mouvement-collectif-m1.md`](messagerie-mouvement-collectif-m1.md) (Codex), dont
le §11 réserve l'analyse d'impact au portable.*

## Ce que ce relevé est, et ce qu'il n'est pas

Codex demande une analyse d'impact avant tout portage, et elle appartient au portable :
modèles, callbacks, droits par gabarit, notifications, Mémoire, Omégas. **Ce document ne
fait pas cette analyse.** Il relève l'autre moitié, celle qui est dans ma zone et que
personne n'avait écrite : **ce que le joueur voit et peut faire aujourd'hui**, mesuré dans
le code et vérifié à l'écran sur la préprod.

Tout ce qui suit est mesuré, pas estimé. Les chiffres sont reproductibles.

---

## 1. Les objets : douze modèles, cinq machines à états, vingt-six états

| Geste visé (Codex) | Modèles qui le portent aujourd'hui | États |
|---|---|---|
| Mettre une intention en mouvement | `Proposition`, `VersionDeProposition` | 6 |
| ” | `Decision`, `ConsentementDeDecision`, `ObjectionDeDecision` | 5 + 4 |
| ” | `ActionDeFil` | 6 |
| Lancer un sondage | `Sondage`, `OptionDeSondage`, `VoteDeSondage` | ouvert / clos |
| Proposer une rencontre | `PropositionDeRencontre`, `DisponibiliteDeRencontre`, `DossierDeRencontre` | 5 |

**Vingt-six états répartis sur cinq machines qui ne partagent aucun mot.** La cible de
Codex en compte quatre : `À éclaircir → À consentir → En mouvement → Accompli`.

Deux nuances que l'analyse devra trancher :

- **`Objection` n'est pas un pair.** Codex la nomme comme l'une des quatre commandes, mais
  structurellement c'est un enfant de `Decision` (`belongs_to :decision`), au même titre que
  `ConsentementDeDecision`. « Les tensions vivent dans cette carte » (§4) décrit donc déjà
  l'état du modèle, ce n'est pas un changement.
- **`Decision` porte deux axes**, pas un : `ETATS` (5) **et** `RESULTATS` (`adoptee`,
  `a_retravailler`). Une décision close se lit « Adoptée » ou « Close — à retravailler ».
  Le joueur voit donc six statuts issus de la seule `Decision`.

---

## 2. La carte est DÉJÀ unique — et c'est la trouvaille principale

`app/models/carte.rb` (208 lignes) définit un contrat commun — `cle`, `type_libelle`,
`titre`, `statut_libelle`, `porteur`, `corps`, `disponible?`, `chemin_pour`,
`actions_pour` — et `Carte.pour(objet)` encarte **six** types : Rencontre, Graine,
Sondage, Proposition, ActionDeFil, Decision.

`app/views/shared/_carte_objet.html.haml` (23 lignes) est le **seul** rendu de carte de
l'application. Tout objet collectif y passe.

**Et les six types sont visuellement indiscernables.** La vue émet
`class: "pz-carte--#{carte.cle}"` — donc `pz-carte--proposition`, `--decision`, `--action`,
`--sondage`, `--rencontre`, `--graine`. J'ai cherché ces modificateurs dans toutes les
feuilles du dépôt : **aucun n'est stylé**. Huit règles existent pour `.pz-carte*`
(`application.scss` l. 857-880), aucune ne cible un type. Aucun script ne les vise non plus.

> **Conséquence pour la cible.** « Une seule carte traverse le cycle » est déjà vrai du
> rendu. Ce qui distingue les objets à l'écran n'est pas la forme, c'est **le texte** :
> `type_libelle` (« Proposition », « Décision », « Action »…) et `statut_libelle`. La
> convergence visuelle est faite ; celle du vocabulaire ne l'est pas.
>
> Corollaire utile : les six classes `pz-carte--*` sont du balisage mort disponible. Si la
> cible veut distinguer les états du Mouvement, l'accroche existe déjà et ne casse rien.

---

## 3. Ce que le joueur peut créer, et où

Codex nomme **cinq** gestes dans le « + ». Voici ce qui existe, vérifié à l'écran sur
`/espaces/559` (compte `nino`, préprod) :

| Geste Codex | Existe ? | Où, aujourd'hui |
|---|---|---|
| Mettre une intention en mouvement | éclaté en **4** | « Créer une proposition », « Créer une action », « Consigner une décision déjà prise » (Gardien seul), et objecter depuis la carte |
| Lancer un sondage | oui | « Créer un sondage » — **pas** dans le « + » |
| Proposer une rencontre | oui | **dans le « + »** — le seul déjà à sa place |
| Partager un élément de Récit (Graine ou Trace) | **non** | aucune surface : 18 vues parlent de Graine, **zéro** dans `threads/` ou `espaces/` |
| Partager une ressource (fichier ou lien) | à moitié | « Joindre des fichiers » dans le « + » ; **le lien n'existe pas** (`LiensExternes` est un modèle de *profil*, plafonné à 10 URL) |

### Le « + » contre les quatre disclosures

Le panneau « + » du composeur (`threads/_composer.html.haml`) offre **deux** gestes.
Les quatre créateurs d'objets vivent ailleurs : rendus **après** le composeur dans
`espaces/show.html.haml` (l. 253-274), sous forme de quatre `<details>` empilés, ordonnés
par `ordre_des_objets(@thread.intention)`.

Mesuré au navigateur en 1440 × 900 : le composeur porte `order: 3` dans le flex
`.workspace`, donc il est peint en dernier ; les quatre `<details>` s'empilent
immédiatement au-dessus (707 → 815 px) et **défilent avec le fil**, alors que le composeur
reste épinglé (`position: sticky`, 816 → 899 px). Ils sont donc atteignables, mais
seulement au bas du fil.

Le commentaire du composeur (l. 57-59) prévoit déjà la suite : « Au Monde 0, un seul geste :
joindre des fichiers. Il s'étoffera (sondage, proposition, action) sans changer de forme —
c'est pour cela que c'est un menu et non un bouton de pièce jointe. » **La forme cible est
donc déjà en place ; ce sont les entrées qui manquent.**

⚠️ Une contrainte structurelle à connaître avant de déplacer quoi que ce soit : le panneau
« + » vit **dans** le `form_with` du composeur. Un `<form>` imbriqué est invalide — les
navigateurs suppriment l'intérieur en silence, et le geste paraîtrait posé sans jamais
partir. C'est pourquoi « Proposer une rencontre » est un **lien** qui ouvre le formulaire
par l'URL, et non un formulaire. Les trois gestes à rapatrier devront suivre le même
idiome.

### Deux autres portes

- Depuis un message : `→ Proposition` et `→ Action`
  (`threads/_message.html.haml` l. 217-218), via `?transformer=<id>&objet=…`.
  Aucune porte équivalente vers Décision, Sondage ou Rencontre.
- Le badge de retour : `« Proposition : <titre> »` / `« Action : <titre> »` (l. 222) —
  un des rares endroits où le mot « Proposition » est affiché au joueur.

---

## 4. Les deux vues secondaires que « Mouvements » remplace

| Vue | Sections |
|---|---|
| `actions_de_fil/index.html.haml` — « Mes actions » (`/echanges/actions`) | À accepter · En cours · Terminées |
| `decisions/index.html.haml` — « Décisions » (`/espaces/:id/decisions`) | À préparer · Ouvertes · Closes et à réviser |

**Deux vues, six sections → une vue, cinq sections.** Les deux rendent déjà
`shared/carte_objet` avec `Carte.pour` : la vue « Mouvements » est un **re-sectionnement de
l'existant**, pas une vue neuve.

Attention au périmètre : « Mes actions » est **transversale** (toutes les actions du joueur,
tous espaces confondus — c'est une entrée du panneau `/echanges`) tandis que « Décisions »
est **par espace**. Les fusionner demande de trancher laquelle des deux portées gagne —
Codex ne le dit pas.

---

## 5. Le coût mesuré

| | Nombre |
|---|---|
| Modèles portant les cinq gestes | 12 |
| États à faire converger | 26 (+ l'axe `résultat` de `Decision`) |
| Vues touchées | 20 |
| Routes dédiées à ces objets | 28 |
| **Assertions de bancs nommant un objet collectif** | **231, réparties sur 29 bancs** |

Les bancs les plus exposés : `verifier_b4_decisions` (30 assertions sur 37),
`verifier_b3_composeur` (21/36), `verifier_mentor` (19/44), `verifier_reliquat_v1` (16/35),
`verifier_rencontre` (16/19), `verifier_sondages` (16/18).

*(Comptage : toute assertion `verifie` dont le bloc de trois lignes nomme proposition,
décision, action de fil, objection, sondage, rencontre, consentement, `pz-carte` ou
`creer_`. Reproductible.)*

Notre règle tient ici plus qu'ailleurs : **un balisage asserté qui change → le banc change
dans la même livraison.** À 231 assertions, ce n'est pas une finition : c'est une part du
chantier, à chiffrer d'emblée.

---

## 6. Ce que je recommande de ne pas refaire

1. **Ne pas redessiner la carte.** Elle est déjà unique, déjà unifiée, déjà sans style par
   type. Le travail est du vocabulaire, pas du dessin.
2. **Ne pas créer une vue « Mouvements » à côté.** Les deux index existants ont la même
   mécanique ; les re-sectionner coûte moins et ne laisse pas de doublon derrière.
3. **Ne pas déplacer les créateurs sans traiter le `<form>` imbriqué.** Le piège est
   silencieux : la page paraît juste et le geste ne part pas.
4. **Ne pas commencer par le CSS.** Rien de ce qui distingue les objets à l'écran n'est
   dans une feuille.

## 7. Ce qui reste sans réponse, et pour qui

- **Pour le portable** (§11 de Codex) : callbacks, droits par gabarit `échange` / `groupe` /
  `cercle`, notifications, Mémoire, Omégas, et la portée des deux index à fusionner.
- **Pour Codex** : « Partager un élément de Récit » n'a aujourd'hui **aucune** surface de
  fil. Est-ce une Graine déjà publiée qu'on cite, ou une Graine qu'on sème depuis le fil ?
  Les deux demandent des objets différents. Même question pour le lien de la ressource, qui
  n'existe nulle part côté fil.
