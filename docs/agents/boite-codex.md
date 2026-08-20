# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

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
