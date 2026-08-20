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


### 2026-08-20 · du poste fixe · ⚠️ Le canon « aucun badge aux Guides » contredit un seuil LIVRÉ

Consigne de Codex restée dans ma boîte : « **ne pas afficher un badge à la rencontre des
Guides** » (`guides-intuition-metaparcours-badges.md` §3.4). « Le premier échange complet active
cette bulle mais ne donne aucun badge. `Présence ouverte` reste attaché à l'entrée dans l'Espace
d'échange et `Première grammaire acquise` aux dix clés. »

**Or le seuil existe, il est livré, et il est délibéré :**

- `config/seuils.yml:167` — `m0_communication`, titre **« Dialogue ouvert »**, description
  « Une première question posée aux guides du Jeu », sceau `pluriel`, annonce `bandeau` ;
- `guides_controller.rb:44` pose `m0-dialogue-guides` dès qu'une question est posée, avec un
  commentaire qui nomme explicitement le badge : « le badge "Dialogue ouvert" lit cette clé » ;
- `monde_0_etats.rb:134` et `:178` lisent la même clé pour la carte Communication.

**Je n'y touche pas, et pour trois raisons.** `config/seuils.yml` est le fichier du portable ;
retirer un seuil est un arbitrage produit ; et des joueurs le détiennent peut-être déjà — un
badge qui disparaît d'un profil n'est pas un détail d'affichage.

**Ce qu'il faut trancher**, dans cet ordre : Codex parle-t-il de la cible d'Intuition (où les
Guides changent de fonction) ou de l'état d'aujourd'hui ? Si c'est d'aujourd'hui, que devient le
seuil déjà accordé — retiré, conservé pour ceux qui l'ont, ou renommé ?

Tant que ce n'est pas tranché, l'écart reste : la doctrine dit une chose, l'application en fait
une autre, et les deux sont écrites noir sur blanc.

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
