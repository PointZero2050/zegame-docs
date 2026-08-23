# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-23 · du portable · §6 câblé — et le régime FIN s'applique, ton moteur l'expose

**Attendu :** valider une formulation que tu n'as pas arbitrée. Le reste est en préprod.
**Référence :** préprod `da20c25` · bancs `verifier_gestes` §7ter, `verifier_chaine_m0`.

Tes sept arbitrages sont appliqués. Deux méritent un mot.

**§6.2 — c'est le régime FIN qui vaut.** Tu ouvres deux voies : la preuve globale confirme les
trois gestes « si le moteur n'expose que `completed` », la correspondance fine s'applique
« lorsqu'un état intermédiaire persistant est disponible ». **Le nôtre l'est** :
`ExperienceQuizAttempt#answers` porte la clé de chaque étape répondue. J'ai donc câblé ton
tableau §6.2 étape par étape — un geste s'allume quand SES étapes sont répondues, et le joueur
voit sa séquence avancer *pendant* qu'il joue. `completed` reste le filet qui confirme les trois
ensemble, et aucun geste n'est jamais déduit de la seule ouverture.

**§6.1 — deux formulations à toi, pas à moi.** Tu donnes le texte du renoncement, que j'ai posé
tel quel. Deux écarts que je te soumets :

1. **La V1 montre une CARTE, pas une roue.** Sa phrase dit donc « Ta carte est conservée dans
   tes Traces… ». Recopier « roue » sur un écran qui n'en montre pas m'a semblé pire qu'adapter
   le mot. Corrige si tu préfères l'uniformité.
2. **Le cas où la phrase EST gardée** n'était pas arbitré, et l'ancienne phrase ne disait rien
   des Traces. J'ai écrit : « Ta roue est conservée dans tes Traces. Ta phrase est gardée pour
   ta Graine. » — même principe que le tien, les deux objets nommés. Ta plume décide.

**§6.4 — rien codé, comme tu le demandes.** Le Sas et l'Atelier attendent une association
canonique qui n'existe pas ; aucun identifiant n'est en dur, les cinq CTA restent absents.

**§6.5 fait** : `Retours reçus` → `Bilans d'expérience`, en famille et à l'unité. La clé
technique `:retour` ne bouge pas, elle est le suffixe d'une colonne.

Toujours en attente, sans urgence : le titre (ou son absence) du bloc des `validations`, remonté
sous le contenu éditorial.

### 2026-08-23 · du portable · Le bloc des validations n'a plus de titre — en veux-tu un ?

**Attendu :** un mot, ou rien. **Référence :** production `f41d30f`.

En retirant « Comment ce passage sera reconnu » (demande de Boris), un `%p.eyebrow` portant ce
même titre était resté sur le bloc voisin — celui des `validations`, le détail éditorial libre
qui MIGRE sous le contenu de l'expérience. Le titre réaffichait donc à l'identique ce qu'on
venait de supprimer.

Je l'ai retiré : le bloc se tient désormais **sans titre**, comme « À quoi t'attendre » à côté.
C'est un choix par défaut, pas une décision éditoriale — si ce contenu mérite un intitulé
propre (il est libre, parfois substantiel, et il parle de la manière dont l'expérience est
reconnue), c'est ta plume.

Toujours en attente chez toi, sans urgence :
- la formulation « Aucune phrase n'a été gardée pour ta Graine. » (message précédent) ;
- les **6 gestes sans porte** (Atelier, Sas, constellation) ;
- la correspondance **étapes de quiz ↔ gestes** pour les 4 autres quiz.

### 2026-08-23 · du portable · État des lieux pour ta passe avec Boris : ce que la base porte, et ce qu'elle ne porte pas

**Attendu :** rien à faire — c'est une référence, mesurée en production ce jour, pour que la
passe ne reparte pas de suppositions.

#### 1. Les tables de progression, en entier

```
ChallengesUser : challenge_id, user_id, end_at, validated_at, retour
Point          : user_id, challenge_id, skill_id, point
ChallengesSkill: challenge_id, skill_id, point
JourneysUser   : journey_id, user_id, end_at, validated_at
```

**Il n'y a rien d'autre.** Pas de table d'étape, pas de colonne d'étape, aucune trace de « où
en est le joueur DANS une expérience ». La granularité de la base s'arrête à l'expérience.

#### 2. La mécanique actuelle, de bout en bout

- `mark_as_ended!` pose `end_at`. Sur changement de `end_at`, `set_validated_at` pose
  `validated_at` **si l'expérience est auto-validée**.
- Sur changement de `validated_at`, `gain_points` écrit les Ω : une ligne `Point` par compétence
  liée, **en copiant** `challenges_skills.point` au moment du gain.
- `restart!` remet `end_at` à nil et **ne révoque rien** — décision Boris du 28 juillet : « une
  validation acquise ne se révoque JAMAIS ».
- ⚠️ **Corrigé ce 23 août** : `gain_points` faisait `destroy_all` puis recréait depuis la valeur
  du jour. Un rejeu après qu'un admin eut baissé une valeur RETIRAIT des Ω acquis — mesuré, 6 → 3.
  Il garde désormais le maximum : un rejeu peut profiter au joueur, jamais lui reprendre.
- Le parcours Monde 0 est **linéaire** : `locked_challenge_ids_for` verrouille l'aval.
- Dans l'interface, le bouton « J'ai réalisé cette expérience » n'existe **que tant que `end_at`
  est nul**. « Revoir ou refaire » renvoie au mini-jeu et laisse `ChallengesUser` intact.

#### 3. Ce que le YAML déclare DÉJÀ par expérience — ne pas le respécifier

`intensity`, `effect_scale`, `minimum_world`, `modality`, `prerequis`, `intensity_note`,
`effect_note`, `sequence`, plus `auto_validated`, `validation_authority` et `omegas`, que le
portable a versionnés hier après deux dérives entre préprod et production.

`sequence` porte **deux champs** par geste : `verbe` et `libelle`. Les quatre autres de ta
maquette (`title`, `time`, `heading`, `text`, `action`) n'existent nulle part — c'est l'objet de
mon message précédent.

#### 4. ⚠️ Ce qui décide de l'« étape courante » : neuf expériences sur quatorze ont une preuve

Toutes déclarent **3 gestes**. Mais `ExperienceState::ADAPTERS` ne connaît une preuve réelle que
pour neuf d'entre elles :

| preuve réelle | aucune preuve |
|---|---|
| entrer-dans-le-jeu · coupable-ideal · drole-d-epoque · avant-le-zero · ecosysteme · site-du-point-zero · signe-de-reconnaissance · conseil-omega · decouvrir-les-formats | **et-moi-dans-tout-ca** (mentor) · **les-choses-se-precisent** · **le-sas-d-entree** · **vivre-l-atelier** (facilitateur) · **mon-recit-de-passage** |

Et la preuve, quand elle existe, ne couvre **qu'un seul des trois gestes** — celui qui porte le
mini-jeu ou le QCM. « Regarder la vidéo » n'en a aucune, le code le dit : « une vidéo regardée ne
prouve rien côté serveur ».

Autrement dit : une progression par étape adossée aux seules preuves laisserait **cinq
expériences entièrement muettes** et, sur les neuf autres, **deux gestes sur trois** sans état.
C'est la contrainte dure de ta note — je la mets sous tes yeux plutôt que de te laisser
l'arbitrer à l'aveugle.

#### 5. Ce que `JourneyProgress` calcule, sans rien stocker

`prochaine`, `requis_total`, `requis_faits`, `omega_gagnes`, `omega_restants`, `chapitres`,
`accompli`, `seuil`, `preparations`, `narration`. Aucune table, aucun `save` : « un état se lit,
il ne se stocke pas ».

#### 6. Puissances, polarités et verbes : déjà dérivables, rien à écrire

`skill.derived_framework` porte « PUISSANCE - Polarité » ; `config/puissances/{slug}.yml` porte
`verbes.{polarite}.mot`. Exemple réel, « Le Coupable idéal » : Imagination · Lumière · JE RÊVE ·
2 Ω. Les 42 slots du parcours sont complets — vérifié, aucun sans `derived_framework`, aucun
sans verbe.

#### 7. La dette qui traîne

`narration` : cinq clés possibles (`seuil_ouvert`, `depart`, `dernier_chapitre`, `courant`,
`en_chemin`), **zéro texte déclaré**. La mécanique existe depuis toujours, la voix n'a jamais eu
de mots, et la règle CSS qui l'habillait était morte sans que personne le voie.

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
