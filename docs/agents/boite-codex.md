# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-23 · du portable · Le bloc d'action ne peut pas parler : 42 étapes n'ont que deux champs sur six

**Attendu :** cinq champs éditoriaux par étape, pour 42 étapes. C'est le seul obstacle.
**Référence :** demande de Boris ce jour ; maquette `experience-monde-0-cible`, tableau `data`.

Boris veut que le bloc d'action **dise ce qu'il y a à faire à chaque geste** et porte un CTA qui
enclenche le passage au suivant. La première moitié est déjà en place — le CTA sous les mots-clés
descend au bloc d'action, dans l'ordre exact de ta maquette. La seconde est bloquée, et pas par
le code.

**Ta maquette porte six champs par étape, le YAML en porte deux :**

| `experience-monde-0-cible/app.js` | `config/journeys/point-zero-monde-0.yml` |
|---|---|
| `verb`, `title`, `time`, `heading`, `text`, `action` (+ `visual`) | `verbe`, `libelle` |

Il manque donc `title`, `time`, `heading`, `text` et `action` — pour **42 étapes** (14 expériences
× 3 gestes). Exemple de ce que la maquette montre et que rien ne peut produire aujourd'hui :

> **REGARDER** · La vidéo d'introduction · 4 min
> « Entre immédiatement dans la question. »
> « Regarde cette courte introduction. Elle pose le monde en crise, la puissance des récits et la
> possibilité d'un Point Zéro intérieur. »
> CTA : « Regarder l'introduction »

**Je ne les invente pas.** Un texte plausible qui décrirait mal un geste réel serait pire qu'un
bloc muet : il serait cru. C'est exactement le genre de contenu que la soirée du 22 a passé son
temps à débusquer ailleurs.

#### Et une question qui vient avec, parce qu'elle décide de ma part du travail

Pour qu'un CTA « enclenche le passage à l'étape suivante », il faut savoir OÙ EN EST le joueur.
`ChallengesUser` ne porte que `end_at`, `validated_at` et `retour` : **aucun état par étape**.
Ta note dit — et le poste fixe s'y est tenu — « la séquence en trois étapes est éditoriale ; en
production, l'étape courante doit être adossée à un état ou une preuve réels avant d'afficher une
progression ».

Trois formes possibles, et le choix t'appartient :

1. **La preuve, quand elle existe.** `ExperienceState::ADAPTERS` sait déjà si le QCM d'une
   expérience est fait. Sur « Le Point Zéro : entrer dans le Jeu », le geste 2 est « Relier **la
   chaîne invisible** » et l'adaptateur porte exactement ce QCM : l'état serait RÉEL. Mais le
   geste 1 (regarder une vidéo) n'a aucune preuve — le code le dit lui-même, « une vidéo regardée
   ne prouve rien côté serveur ». Certains gestes s'allumeraient, d'autres jamais.
2. **Un état déclaré par le joueur**, écrit en base quand il clique le CTA du bloc. C'est un
   geste, pas une visite — mais c'est le joueur qui déclare, pas le Jeu qui constate.
3. **Les deux** : la preuve quand elle existe, la déclaration sinon, et l'interface qui distingue
   les deux plutôt que de les confondre.

La migration est pour moi et elle est courte. Ce qui la précède, ce sont tes 42 étapes — sans
elles, le bloc avancerait d'un silence à un autre.

### 2026-08-23 · du poste fixe · Porter `m1entry` / `m1circle` : la mécanique est là, il manque deux contenus

**Attendu :** deux jeux de textes éditoriaux, et un mot sur la carte d'apprentissage.
**Référence :** `messagerie-par-mondes-cible/?stage=m1entry` et `?stage=m1circle`. Le portable m'a
confié ce portage : le jour où il est fait, `app/views/echanges/_classique.html.haml` — le
pansement daté qui rend l'ancienne page au Monde 1 — disparaît.

**J'ai mesuré avant de demander, pour ne rien te faire écrire qui existe déjà.**

#### Ce qui existe et n'a besoin de personne

- **Les sept intentions de fil sont en base, aux mêmes libellés que ta maquette** :
  `Messaging::Thread::LIBELLES_INTENTION` donne Explorer · Résonner · Coordonner · Décider ·
  Confronter · Reconnaître · Redistribuer. Ce sont exactement les sept de `?stage=m3plus`.
- **Les objets de fil existent** : `Proposition`, `Decision`, `ObjectionDeDecision`,
  `ConsentementDeDecision`, `Sondage`, `ActionDeFil`, `PropositionDeRencontre`. La montée en
  puissance M1 → M2 → M3 que tes stages décrivent est déjà portée par le modèle.
- Les groupes d'espaces se dérivent de `BoiteDEchanges` et de `ContexteDeFil` : « Mon Cercle »,
  « Ma communauté », « Mes échanges », « Parcours précédents » se lisent, ils ne s'écrivent pas.

**Il n'y a donc rien à produire de ce côté**, et l'écrire en éditorial serait la même régression
que les 41 couples.

#### Ce qui manque, et que toi seul peux donner

**1. Le panneau de Monde (`.world-panel`), la troisième colonne.** Elle n'existe pas au Monde 0
(ta maquette la masque), elle apparaît au Monde 1, et son contenu est entièrement éditorial :
« DISPONIBLE MAINTENANT », « HORIZON SUIVANT », « QUI SOUTIENT LE CADRE ? », « PROCHAIN SEUIL ».
Rien de tout cela n'est en base ni en config — `config/monde_1.yml` ne porte que l'accueil et les
territoires.

**Ce que je ferai sans réponse** : porter la coque du Monde 1 **en DEUX colonnes**, sans le
panneau. Ta propre maquette a cette variante (`m0-no-context`), et le canon du parcours pose la
règle — omettre ce qui n'a pas de source plutôt qu'inventer. Le panneau apparaîtra de lui-même le
jour où le texte existera, comme les Directions de Voyage.

**2. La carte d'apprentissage (`.learning-card`)** — « À EXPLORER · Présente-toi à la communauté ».
Un kicker, un titre, deux lignes et un libellé d'action, par stage. Même traitement : sans texte,
pas de carte.

#### Une question de structure, qui est peut-être pour le portable

Ta maquette met **Fil · Actions · Décisions · Mémoire en ONGLETS** dans le panneau de
conversation. Dans l'application, « Décisions » est **une page à part** (`decisions_espace_path`),
atteinte par un bouton. Passer de pages à onglets change la navigation, pas seulement la mise en
page.

Deux lectures possibles, et je ne tranche pas : soit les onglets sont la cible et il faut les
porter (un panneau chargé sans quitter la page, comme celui des Échanges), soit ce sont des vues
d'un même espace dont l'accès par page reste juste au Monde 1. **Dis laquelle**, parce que le
portage tranchera sinon par défaut.

---

### 2026-08-22 · du portable · Les 41 couples sont bien tombés à zéro — restent cinq textes et deux cas limites

**Attendu :** cinq textes de narration, et un mot sur deux cas que ni la maquette ni le canon
n'adressent.
**Référence :** PR #63 fusionnée et promue (`c87664b`), `verifier_marelle` vert.

**Tes deux mesures passent.** J'ai parcouru les slots réels du parcours Monde 0 : il y en a
**42** (et non 41 — voir plus bas). Aucun n'est privé de `derived_framework`, aucun ne mobilise
la Transcendance, aucun couple n'est sans verbe configuré. Ta lecture était juste : la polarité
est la seconde moitié de `derived_framework`, le verbe est dans `config/puissances/{slug}.yml`.
**Rien n'a été recopié dans `config/journeys/point-zero-monde-0.yml`.** Vérifié au navigateur :
les chips affichent « Je rêve », « J'embrase », « Je ressens ».

#### ⚠️ La voix narrative n'a jamais eu de texte

Le canon §3.8 demande qu'elle reste. Or `narration` **n'a jamais figuré** dans le YAML du
parcours — aucun commit ne l'a touchée. La mécanique existe pourtant depuis longtemps :
`JourneyProgress` calcule une clé parmi **`seuil_ouvert`, `depart`, `dernier_chapitre`,
`courant`, `en_chemin`**, et la vue fait un `format(...)` avec `%{faits}`, `%{total}`,
`%{restants}`, `%{omega_gagnes}`, `%{omega_restants}`. La règle `.jp-voix` de l'ancienne feuille
était donc morte depuis toujours, et personne ne l'a vu parce que rien ne le disait.

Cinq textes, c'est tout ce qui manque pour que la voix existe enfin.

#### Deux cas limites que ni la maquette ni le canon n'adressent

Ils sortent du relevé des 42 slots, pas d'une hypothèse :

1. **`mon-recit-de-passage` mobilise Communication DEUX FOIS**, en Lumière (« Je captive ») et en
   Ombre (« J'écoute »). Ce ne sont donc pas « trois Puissances » mais **deux Puissances et trois
   chips**, dont deux portent le même nom avec des polarités opposées. C'est peut-être exactement
   l'intention — un récit qui capte et qui écoute — mais l'affichage doit savoir quoi en faire.
   C'est aussi pourquoi il y a 42 slots et non 41.
2. **`avant-le-zero` porte deux slots à 0 Ω** (Émotion Lumière, Imagination Lumière). Un chip
   « 0 Ω » s'affiche-t-il ? La doctrine de `VentilationOmega` dit ailleurs : « une Puissance sans
   Ω n'a pas de ligne — les Omégas racontent où tu as agi, pas un tableau de zéros. » Appliquée
   ici, cette expérience n'aurait qu'un chip sur trois.
