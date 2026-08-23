# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-23 · du portable · La matrice que tu demandais, mesurée — et deux de tes lignes se corrigent

**Attendu :** un arbitrage sur la roue, une confirmation sur le Conseil.
**Référence :** preprod `9974467` · banc `scripts/verifier_traces_parcours.rb` ·
ton [canon](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/canon-traces-parcours.md)

Ton canon est appliqué. La matrice `surface → résultat persistant → événement → famille`, telle
que tu l'exigeais avant tout code, **mesurée expérience par expérience** :

| surface | résultat persisté | événement | famille | matière |
|---|---|---|---|---|
| 5 quiz | `experience_quiz_attempts.result` | `status → completed` | Production | `result["titre"]` · `result["note"]` |
| le-coupable-ideal | `coupable_ideal_sessions.result` | `completed_at` | Production | `result["phrase"]` · Puissance dans `result["graine"]` |
| avant-le-zero | `traversees.fin_id` | `completed_at` | Production | le label de la fin et son 1ᵉʳ paragraphe |
| le-conseil-omega | `conseil_sessions.engagement` (text) | `completed_at` | Production | le texte libre du joueur |
| une-drole-d-epoque | `moteur_assessments` | `completed_at` | Diagnostic | déjà lu |
| 5 expériences sans surface | — | — | — | **écarts nommés par le banc**, jamais comblés |

**Aucune écriture éditoriale n'a été nécessaire** : ce que le joueur lit à l'écran est
exactement ce que le registre garde. C'est la meilleure nouvelle de la mesure.

**Ta ligne sur la roue est appliquée à la lettre** (§6) : la roue est une Production
automatique, la Puissance nommée à la chambre du jury voyage dans `donnees["graine"]`, et
**aucune section de Profil n'est née** — le banc l'asserte en comptant les vues.

**Deux points pour toi :**

1. **« Conserver cette roue » → « Voir cette Trace »** : la Trace existe désormais, le
   remplacement du bouton est donc débloqué. C'est une vue (poste fixe) et un libellé (toi) —
   je ne touche ni l'un ni l'autre. Dis-moi si le libellé exact est bien « Voir cette Trace ».
2. **L'engagement du Conseil** : je l'ai classé Production (texte libre écrit par le joueur,
   colonne `text`, la seule matière de cette expérience qui ne se relisait nulle part). Sa
   posture reste un Positionnement, comme avant. Confirme ou corrige — c'est la seule ligne de
   la matrice que j'ai tranchée sans toi.

**Ce que le canon interdit et que je n'ai pas fait** : aucune filiation Trace → Graine n'est
simulée (§4) ; les Graines, messages, réactions et dialogues de Guides restent hors du
registre, et le banc le vérifie explicitement.

Toujours ouverts chez toi : les **6 gestes sans porte** (Atelier, Sas, constellation) et la
correspondance **étapes de quiz ↔ gestes** pour les 4 autres quiz.

### 2026-08-23 · du portable · « Conserver cette roue dans ton Profil » ne conserve rien, et je ne sais pas ce qu'elle devrait conserver

**Attendu :** dire ce que « conserver la roue » produit — ou retirer la promesse.
**Référence :** preprod `7ac8967` · `config/coupable_ideal_v2.yml:350` · banc `verifier_chaine_m0.rb`.

Boris a signalé que ses mini-jeux ne laissaient rien. Mesure : la fin du procès du Coupable
idéal offre trois choix, et **deux d'entre eux annonçaient une conservation qui n'avait pas
lieu** :

| choix | ce que la page DIT | ce qui se passait |
|---|---|---|
| `bouton_graine` — « Garder une phrase pour ma Graine » | « Ta phrase est conservée pour ta Graine. » | rien — **corrigé, la Graine est semée** |
| `bouton_profil` — « Conserver cette roue » | « Cette roue est conservée dans ton Profil. » | rien, **et je ne corrige pas** |
| `bouton_rien` | « Rien n'a été conservé au-delà de cette page. » | juste |

Pour la roue, je m'arrête : **aucune vue de profil n'affiche cette roue aujourd'hui**, et ce
que « conserver » doit y produire n'est pas déductible du code. Trois issues, à toi :

1. **Une Trace** — mais le territoire de la roue serait lequel ? Et l'arbitrage de Boris du
   16 août a justement retiré Imagination des Traces (« doit produire une Graine, pas une
   Trace »). Une roue de procès n'est ni Désir ni Intuition, les deux seuls territoires qui
   écrivent aujourd'hui.
2. **Une section du Profil** — alors il faut dire ce qu'elle montre : la roue entière ? le
   pôle fort et le pôle exilé ? la Puissance nommée à la chambre du jury ?
3. **Retirer la promesse** — le choix disparaît, il n'en reste que deux. C'est propre, et
   c'est peut-être le bon si la roue vit déjà assez dans la restitution qu'on peut rouvrir.

Accessoirement, une chose que la mesure a rendue visible : à la « chambre du jury », le joueur
**nomme une Puissance** où il reconnaît le mouvement exilé. Cette réponse est stockée dans les
réponses de la session et sert la restitution — elle ne va nulle part ailleurs. Si tu veux
qu'elle nourrisse la Puissance nommée, c'est une décision à prendre, pas un oubli à réparer.

Toujours ouverts chez toi : les **6 gestes sans porte** (Atelier, Sas, constellation) et la
correspondance **étapes de quiz ↔ gestes** pour les 4 autres quiz.

### 2026-08-23 · du portable · Six gestes n'ont pas de porte, et je ne veux pas la deviner

**Attendu :** nommer la surface de six gestes — ou dire qu'ils restent déclaratifs.
**Référence :** banc `scripts/verifier_chaine_m0.rb`, qui marche les 14 expériences du M0.

Balayage complet demandé par Boris. Sur 42 gestes, 36 ont maintenant une adresse derrière leur
CTA (l'adaptateur de l'expérience, ou une adresse évidente : « Dialoguer avec mon mentor »
→ `/mentor`, « Relire mes Traces » → `/mes-traces`, « Planter ma Graine » → `/fresque`).

**Six désignent une surface dont l'adresse n'est pas devinable.** Elles restent SANS bouton —
c'est assumé et le banc le dit, mais c'est ton arbitrage :

| expérience | geste | CTA | la surface visée existe-t-elle ? |
|---|---|---|---|
| les-choses-se-precisent | 1 | « Relire ma constellation » | aucune route « constellation » — est-ce `/immateria` ? `/mes-traces` ? |
| le-sas-d-entree | 2 | « Ouvrir les repères du Sas » | `/sas/:slug` existe — lequel ? |
| le-sas-d-entree | 3 | « Conserver mon intention » | s'écrit-elle quelque part, ou est-ce déclaratif ? |
| vivre-l-atelier-point-zero | 1 | « Préparer l'Atelier » | seule route : `/evenements/:id/ateliers/:id` — quel événement ? |
| vivre-l-atelier-point-zero | 2 | « Voir le cadre de l'Atelier » | idem |
| vivre-l-atelier-point-zero | 3 | « Retrouver les informations de l'Atelier » | idem |

Trois réponses possibles pour chacun : **une adresse** (je la câble), **« déclaratif »** (le CTA
disparaît du YAML, le geste se confirme à la main — un libellé qui promet une porte inexistante
vaut moins que pas de libellé), ou **« à construire »** (ça devient une demande de page).

Rappel du message précédent, toujours ouvert : la correspondance étapes de quiz ↔ gestes pour
les 4 autres quiz — même logique, ta matrice décide, la mécanique suit.

### 2026-08-23 · du portable · Tes quiz couvrent plus de gestes que ta matrice ne le dit — mesure à arbitrer

**Attendu :** dire jusqu'où étendre. J'ai corrigé le seul cas SANS ambiguïté, le reste attend
ton mot.
**Référence :** preprod `f0dc35b` · ta matrice §3, lignes « Reconnaissance ».

Boris a buté sur le geste 3 d'« entrer dans le Jeu » : « Conserver mon Hypothèse » sans porte.
Mesure : le quiz `la-chaine-invisible` porte les étapes **[mission, chaine, hypothese, seuil]** —
l'Hypothèse s'écrit dans le quiz, la preuve existait. Ta ligne disait « événement
d'enregistrement à ajouter » ; corrigé côté mécanique, le `completed` du quiz prouve maintenant
les gestes 2 ET 3 de cette expérience.

**Les autres quiz semblent couvrir leurs gestes aussi**, et je n'ai PAS étendu sans toi :

| expérience | tes gestes | étapes du quiz |
|---|---|---|
| le-signe-de-reconnaissance | Choisir · Composer · Décider | mission, situation, composition, envoi, signe |
| l-ecosysteme-point-zero | Découvrir · Relier · Produire | mission, fragments, liens, manque, schema |
| le-site-du-point-zero | Explorer · Éprouver · Cartographier | mission, repere_1, repere_2, langage, feedback, geste, produire, carte |
| decouvrir-les-formats | Clarifier · Comparer · Produire | mission, intention, format, geste, boussole |

Si tu confirmes une correspondance (ex. signe : les trois gestes vivent dans le quiz → rangs
[1,2,3] prouvés par `completed`), je l'étends à la ligne. Si un geste vit HORS du quiz (une
exploration libre avant, par exemple), dis lequel — il restera déclaratif. Ta matrice §3 est la
référence ; la mécanique la suit, elle ne la devine pas.

### 2026-08-23 · du poste fixe · « Passage en cours » : cinq champs par geste manquent, et un état que le canon interdit

**Attendu :** cinq champs éditoriaux par geste, ou un mot disant qu'on s'en passe.
**Référence :** ta maquette `experience-monde-0-cible/?step=1&r=passage-v1`, commit `75379ba`.
Demande venue de Boris, qui m'a chargé de porter « juste le bloc Trois gestes ».

**J'ai mesuré ta mise à jour avant de porter quoi que ce soit, et le résultat surprend :
le balisage des trois cartes de geste est IDENTIQUE avant et après.** `git show 75379ba` ne
touche que `NOTES.md` et `app.js`, jamais `styles.css`, et la ligne `steps.innerHTML` rend le
même `<button class="step"><span>N</span><div><small>VERBE</small><b>titre</b>…` qu'avant. Le
seul ajout aux cartes est un `<em>${s.time}</em>`.

**Ce qui a réellement changé, c'est le panneau d'action** — et c'est là que ça coince.

#### Ce que ton nouveau bloc demande, et ce que la base porte

| ce que `?step=1` affiche | source dans l'application |
|---|---|
| `VERBE` et le libellé du geste | ✅ `sequence[].verbe` et `sequence[].libelle` |
| la durée du geste (`4 min`) | ❌ rien |
| le titre du geste (`La vidéo d'introduction`) | ❌ rien — `libelle` en tient lieu |
| `heading` (« Entre immédiatement dans la question. ») | ❌ rien |
| `text` (les deux lignes qui suivent) | ❌ rien |
| `action` (« Regarder l'introduction → ») | ❌ rien |
| `recognition` (« Lorsque tu reviens, indique… ») | ❌ rien |
| `mode` : `declared` ou `proof` | ❌ rien **par geste** |
| l'index du geste courant | ⚠️ **interdit** |

Notre `config/journeys/point-zero-monde-0.yml` porte exactement ceci, et rien d'autre :

```yaml
    sequence:
      - {verbe: Regarder, libelle: l'introduction}
      - {verbe: Relier, libelle: la chaîne invisible}
      - {verbe: Formuler, libelle: une Hypothèse de seuil}
```

#### ⚠️ Et l'index courant, c'est toi qui l'as interdit

Ton propre invariant, inscrit au canon : « La maquette `?step=2` illustre la séquence mais ne
constitue pas une source d'état. Tant qu'un index courant ne peut pas être dérivé d'une action,
d'une preuve ou d'un état métier existant, les trois gestes sont présentés comme une carte de
l'expérience sans en déclarer un en cours. **Aucun `current_step` générique ne doit être créé
uniquement pour satisfaire le visuel.** »

Or « PASSAGE EN COURS · GESTE 1 SUR 3 », les états `active` / `done` des cartes, le compteur
« Geste 1 sur 3 » et l'enchaînement du panneau reposent tous sur cet index. **Je ne le fabrique
pas.** Si ta mise à jour vaut aussi révision de cet invariant, dis-le explicitement — c'est un
arbitrage, pas une déduction, et il engage un besoin de MODÈLE chez le portable (une preuve par
geste, pas seulement par expérience).

#### Ce que je fais en attendant

Rien de plus : les trois cartes rendent déjà `verbe` + `libelle` dans la forme de ta maquette,
sans état déclaré, et le panneau d'action porte l'état RÉEL de l'expérience — accomplie, en
attente de reconnaissance, commencée, ou à réaliser. C'est ce que la donnée permet de dire.

**Deux voies, et le choix est le tien :** ou tu écris les cinq champs par geste (42 gestes pour
les 14 expériences du Monde 0), ou le bloc reste au niveau de l'EXPÉRIENCE et la séquence garde
son rôle de carte. La seconde ne coûte rien et tient déjà ; la première demande de l'éditorial
ET un état métier par geste.

---

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
