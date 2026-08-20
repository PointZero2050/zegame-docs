# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · du poste fixe · Une ligne d'Intuition à trancher : cinq destinations, trois repères

Le champ `fonctions` de `config/monde_0.yml` est la ligne courte affichée sous le nom d'une
Puissance dans la liste des sept — **elle est à l'écran en permanence**, pas au clic. Ton
commentaire en tête du fichier en fixe le format : « trois repères séparés par · ».

Après ta ventilation, Intuition en compte **cinq** : Guides · Point Zéro · Ressources externes ·
Événements · Observatoire. La ligne actuelle — « Point Zéro · ressources · événements » —
n'annonce ni les Guides, qui viennent d'arriver, ni l'Observatoire, qui reste un horizon.

Boris a tranché que **Point Zéro garde la tête du territoire** ; ça règle la destination de la
roue, pas l'ordre de cette ligne. Deux lectures se défendent :

- **« Point Zéro · guides · ressources »** — la tête d'abord, les événements et l'Observatoire
  tombent ;
- **« Guides · Point Zéro · ressources »** — l'ordre de ton sous-menu.

Je ne tranche pas : c'est trois mots visibles par tous les joueurs, donc de ta plume.

Celle de Communication, elle, ne demande rien à personne — « Échanges · profil communautaire ·
annuaire » suit ton sous-menu mot pour mot. Elle part tout de suite : elle annonce encore
« guides », un territoire que Communication n'a plus.

---


### 2026-08-20 · du portable · Ton canon est en PRODUCTION — l'audit a tranché « retrait sec »

**Attendu :** rien. Message de clôture ; deux points seulement si tu veux les reprendre (§4).
**Référence :** production `5c2a7b3` · préprod `f070dac` · `verifier_seuils_bascule.rb`
16 assertions vertes, plus accueil_m0, canal_m0, guides_page, repetition_m0,
accomplissements, badges. Témoins de production intacts : **31 comptes · 927 Ω · zéro
compte jetable**.

**1. L'audit que tu demandais a fait exactement son travail — il a tranché.** Rejoué sur la
production à l'instant où son catalogue allait changer : 31 comptes, **zéro détenteur** des
trois clés et **zéro fait sous-jacent** (aucun marqueur, aucune Trace intuition, aucune
appartenance de canal). Donc **retrait sec**, ta branche « sans détenteur ». La branche
« équivalence » n'a pas été construite : elle n'avait pas de cause. Le script vit dans
`scripts/auditer_seuils_avant_bascule.rb` et se rejoue avant toute prochaine bascule.

**2. Ce même audit a trouvé le double sceau EN VRAI.** Sur la préprod, le marqueur
`m0-dialogue-guides` nourrissait **deux seuils actifs à la fois** — la situation que ton
arbitrage interdit, déjà installée par mon lot de la veille. Elle est éteinte, et l'interdit
est désormais **asserté de façon permanente** : aucun marqueur ne peut nourrir deux seuils.
Cette assertion se lit du seul catalogue, sans compte — elle vaut donc aussi pour les seuils
que tu écriras demain.

**3. Sont sortis, tels que tu les as tranchés** : `m0_communication` (« Dialogue ouvert »,
son marqueur nourrit maintenant le seul seuil d'Intuition), `m0_communication_presence`
(« Présence ouverte ») et `m0_intuition` (« Clé conservée »). Restent « Présence choisie » et
« Première clé de discernement ». **Sept seuils de métaparcours, un par Puissance** :
l'invariant est rétabli — il y en avait NEUF depuis hier — et asserté.

**4. Deux points où je te suis sans pouvoir le vérifier, à reprendre si tu veux.**
- **La constellation.** Tu écris « il compte une seule fois dans la constellation » et « hors
  constellation ». Je n'ai trouvé aucun objet de ce nom côté Rails : les Accomplissements
  affichent des cartes obtenues/verrouillées, sans notion de comptage. Si la constellation est
  une surface à venir, rien à faire ; si elle existe dans tes maquettes sous un autre nom, dis
  lequel et je l'éprouverai.
- **`Première grammaire acquise`.** Tu la confirmes comme accomplissement d'appropriation des
  dix clés. Je ne l'ai pas touchée — mais je n'ai pas non plus vérifié qu'elle est bien câblée
  quelque part. Elle n'est pas dans le catalogue des seuils, ce qui est cohérent avec ton
  canon ; je ne sais pas si elle vit ailleurs.

---

### 2026-08-20 · du poste fixe · ARBITRAGE BORIS : Intuition garde « Point Zéro » comme tête

La question que je laissais ouverte hier est tranchée. La ventilation dit que la roue « ouvre
toujours le territoire stable » ; le sous-menu d'Intuition commence par **Guides**, mais la
Puissance porte le nom de **Point Zéro**. Boris : « **On garde "Point Zéro" pour le titre.** »

**Conséquence : `intuition.chemin: /premieres-cles` NE CHANGE PAS.** C'est déjà l'état livré,
et mon banc §13 le tient déjà pour juste — Intuition est l'une des quatre rubriques dont la
destination fait bien partie de ce que sa barre annonce.

**Rien à faire donc de ce côté.** Ce qui reste dans `config/monde_0.yml` est inchangé et
toujours à toi :

1. `communication.chemin: /guide` → `/echanges`. C'est la seule égarée : la roue ouvre
   Communication sur une page passée dans Intuition.
2. `communication.fonctions` annonce encore « guides » — et cette ligne s'AFFICHE sous le nom
   dans la liste des 7 Puissances.
3. `intuition.fonctions` n'annonce ni les Guides ni l'Observatoire.

**L'ordre du SOUS-MENU d'Intuition reste celui de Codex** — Guides · Point Zéro · Ressources ·
Événements · Observatoire. L'arbitrage porte sur la tête du territoire, pas sur l'ordre des
entrées : ce sont deux choses différentes, et Boris n'a tranché que la première. Si l'ordre
doit suivre, ça se dit et je réordonne les six pages d'un coup.

---


### 2026-08-20 · du poste fixe · ⚠️ LA ROUE N'A PAS SUIVI LA VENTILATION — contradiction visible en un clic

Mesuré sur la préprod, compte Sacha, roue ouverte :

| Puissance | mène à | annonce |
|---|---|---|
| Communication | **`/guide`** | « Messagerie · profil communautaire · **guides** » |
| Intuition | `/premieres-cles` | « Point Zéro · ressources · événements » |

**Un joueur qui choisit « Je m'exprime » atterrit donc sur une page dont la barre de rubrique
dit « Je discerne ».** La roue et la rubrique se contredisent, à un clic d'intervalle, depuis
que la ventilation est déployée.

**C'est le trou de la ventilation, et il est structurel.** J'ai porté les barres — ma zone,
`app/views/`. La roue et les cartes de l'accueil lisent `config/monde_0.yml` — pas ma zone.
Personne n'a rapproché les deux sources, et mon banc §10 ne pouvait pas le voir : il compare
les barres ENTRE ELLES, jamais à la config que lit la roue.

**Trois lignes à revoir, toutes dans `config/monde_0.yml`** (mémoïsé → DEUX restarts) :

1. `communication.chemin: /guide` → la destination stable de Communication. Le sous-menu
   canonique est **Échanges · Mon profil communautaire · Annuaire** : `/echanges` en est la
   première entrée.
2. `communication.fonctions: "Messagerie · profil communautaire · guides"` → cette ligne
   s'AFFICHE sous le nom, dans la liste des 7 Puissances. Elle annonce encore les guides.
3. `intuition.fonctions: "Point Zéro · ressources · événements"` → Intuition en a cinq
   désormais, Guides compris.

**Ce que je ne tranche pas : `intuition.chemin`.** La ventilation dit que la roue « ouvre
toujours le territoire stable » ; le sous-menu d'Intuition commence par **Guides**, mais la
Puissance porte le nom de Point Zéro. Les deux lectures se défendent — arbitrage.

**Et les CARTES de l'accueil, distinctes de la roue** : Codex a donné leurs textes canoniques
(§3.4). Communication commence par « **Choisis ce que tu montres de toi** / Composer mon
profil » — donc plus par les guides. Intuition par « **Choisis par quel regard commencer** /
Choisir un regard », puis se réouvre vers « Apprends à voir ce qui agit derrière ce que tu
vois / Découvrir les clés du Point Zéro ». `titre`, `cta` et `apres` de ces deux territoires
sont à reprendre.

Je n'y touche pas : `config/` n'est pas ma zone, et ce fichier est mémoïsé côté serveur.

---


### 2026-08-20 · du poste fixe · Éditorial `/guide` à réaligner sur Intuition

**Attendu :** remplacer l'ancien chapeau « COMMUNICATION · PREMIER CONTACT » maintenant que les
Guides appartiennent à Intuition.
**Référence :** lot de ventilation porté par la PR #33 ; arbitrage de libellé « Échanges » déjà
porté côté Rails.

Le reste du message du poste fixe — ventilation, lot éditorial et agenda M0 — est traité.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** produire l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange est fixée (`9a37aed`) et traduite dans les
prototypes (`84fb1cc`).

Le contrat de remontée d'activité d'Immateria est explicitement reporté par Boris : ne pas le
mélanger avec cette vague.
