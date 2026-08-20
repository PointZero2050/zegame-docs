# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · du portable · Ta bascule des badges est portée — et deux points de ta demande étaient déjà résolus

**Attendu :** trancher (avec Boris) la conséquence visible du §3 ci-dessous. Le reste est fait.
**Référence :** préprod `ff1a931` · `verifier_seuils_bascule.rb`, 9 assertions vertes ·
badges, accomplissements, canal_m0, accueil_m0 verts.

**1. Le point technique que ta consigne supposait résolu, et qui ne l'était pas.** « Ne retire
ni ne renomme aucun ancien *Dialogue ouvert* » ne peut PAS se tenir en supprimant l'entrée du
catalogue : **un seuil est une lecture, pas une ligne stockée**. Retirer l'entrée l'effacerait
rétroactivement du profil de ses détenteurs. J'ai donc ajouté une borne `avant:` — la
condition ne répond vrai que si le fait est antérieur à la bascule. L'acquis reste exactement
à qui l'avait, et ne s'accorde plus jamais. Le banc l'éprouve dans les deux sens.

**2. « Garantir l'absence de double Oméga » : il n'y a rien à garantir.** Mesuré avant
d'écrire — **aucune entrée du catalogue ne porte de montant** (`omega`, `points`). Un seuil
CONSTATE, il ne récompense pas. La garantie que tu demandais est structurelle, et le banc
l'asserte désormais pour qu'elle le reste.

**3. ⚠️ Une conséquence visible de ton canon, que je ne tranche pas.** Tu demandes la
reconnaissance **rétroactive** du seuil Intuition sur le marqueur `m0-dialogue-guides`, ET la
conservation de *Dialogue ouvert*. Les deux ensemble donnent à un détenteur historique **deux
sceaux pour un même geste** : l'ancien conservé, le nouveau reconnu. Sans double récompense —
mais visible sur son profil. Zéro joueur est concerné aujourd'hui (mesuré) ; la question reste
entière pour demain. À toi et Boris.

**Ce que j'ai porté, tel que tu l'as écrit** : « Présence choisie » à la confirmation du
Profil — le seuil récompense le geste de CHOISIR ce qu'on montre, plus celui d'entrer quelque
part ; et « Première clé de discernement » au premier échange abouti avec un Guide, sur le
marqueur qui existait déjà : il change de territoire, pas de nature.

**Un seuil que je n'ai PAS touché, faute d'instruction** : `m0_intuition` — « Clé conservée »,
la première clé assimilée. Ton message nomme « les dix clés » (qui restent un accomplissement
d'appropriation) mais pas celui-ci. Je préfère le laisser et te demander plutôt que de le
retirer d'une déduction.

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
