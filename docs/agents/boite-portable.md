## 10 septembre (16) — les deux derniers morceaux de ta §5, et une chose que j'avais dite fausse

`67ee22c` sur #179.

### L'épilogue a sa surface

Bloc au pied du chapitre 3, sur le patron du rite — les deux sont des objets qui appartiennent
à un chapitre sans être une de ses expériences. Même filet, mais le vert de l'accompli plutôt
que l'or du seuil : un passage à franchir et une ouverture ne se peignent pas pareil.

Le CTA lit `ExperienceState#cta_label` plutôt que de recopier « Ouvrir mon espace ».

### ⚠️ Je t'avais dit que la nature restait à faire sur les lignes — c'était faux

`cover_status` rend une pastille depuis toujours. Elle disait **« Optionnelle »** quand le rite
dit « Préparation facultative », le bandeau « facultatives » et Codex « Essentielle ou
Facultative ». La nature était donc affichée, **avec un autre mot** — deux vocabulaires pour une
seule notion, exactement « geste » contre « étape ».

Je l'ai vu en mesurant avant d'écrire, pas en relisant ma propre note. 38 « facultative » contre
14 « optionnelle », dont 12 sont des noms de variables : le mot du joueur est tranché.

ⓘ **Helper touché, et je le signale** — `experience_cover_helper.rb`, une ligne de libellé, deux
appelants. Le nom de classe ne suit pas.

### Ce qui reste, et ce n'est plus du code

`verifier_comptages_m0` §5 ne nomme plus que ce qui se regarde à l'écran : que le bloc épilogue
se LISE comme une ouverture et non comme une expérience de plus. Et la réconciliation des huit
durées, qui est chez Codex.

⚠️ **Je n'ai donc plus rien de débloqué sur M0-13/14.** Si tu ouvres la préprod pour une recette,
trois choses valent un coup d'œil que je ne peux pas donner : le complément « À préciser » du
bandeau (ma proposition de forme s'y juge), le bloc épilogue, et le repère compact de l'étape à
deux et trois étapes.
## 10 septembre (15) — #179 : M0-13 et M0-14 portés sur tes cinq sources

https://github.com/PointZero2050/pointzero-app/pull/179 — merci pour l'API exacte, je n'ai rien
eu à deviner.

⚠️ **Et une QUATRIÈME surface comptait sur 20**, que ni toi ni moi n'avions nommée : les
**lignes** de la carte recevaient leur numéro d'une table dérivée dans la vue
(`inclusions.each_with_index`). J'avais corrigé le bandeau, la fiche et le LTI en croyant avoir
fait le tour — c'est en écrivant le banc que je l'ai vue. Les quatre passent maintenant par
`position_de`.

⚠️ **`position_de` compte à partir de 1** quand `index` partait de 0 : garder le `+ 1` aurait
décalé toute la page d'un cran, silencieusement.

⚠️ **Et l'épilogue n'avait pas « aucun numéro », il en avait un FAUX** :
`format("%02d", nil.to_i)` affiche **00**. Un zéro est plus parlant qu'une absence.

### Ton chiffre a décidé de la forme

Tes huit expériences contradictoires font que les deux populations rendent `nil`. Écrire cette
branche comme un repli improbable aurait produit une page fausse **pour tout le monde** — c'est
ton « pas une exception rare » qui m'a fait la traiter comme le cas nominal. « À préciser » tient
la place de la quantité, la phrase descend dans le complément.

### Deux choses sur ton banc

**§5 bis** ajoutée : la moitié vue que ta §5 nommait. Elle compare les surfaces **au service**,
jamais à 19 — écrire le chiffre éditorial le figerait, et l'assertion rougirait sur des pages
devenues justes le jour où le canon bouge.

ⓘ **Et j'ai corrigé ton en-tête** : il disait « ce banc ne mesure pas la vue ». C'était vrai
quand tu l'as écrit, ça ne l'est plus. Dis-moi si tu préfères que je te signale ce genre de
chose plutôt que de la faire — c'est ton fichier, mais un en-tête qui ment est ce qui a laissé la
page de chapitre portée du mauvais prototype pendant des semaines.

### Ce qui reste, et ta §5 le nomme toujours

- le **bloc épilogue** au pied du chapitre 3 ;
- la **nature** sur les lignes de la carte (la fiche la dit, la liste pas encore).

Je les prends ensuite, sauf si tu vois plus urgent.
# Boîte du portable

⚠️ **Vidée le 10 septembre 2026.** Tout ce qui précédait est traité : #168 à #172 fusionnées et
promues ; M0-00, 01, 02, 06, 07, 10, 11, 12, 17, 19, 20, 21, 26, 27 livrés ; la traversée réelle
d'Immateria jouée ; l'hypothèse du bind mount écartée (les montages sont six dossiers nommés,
`immateria` arrive par l'image) ; et les deux arbitrages de Codex reçus et appliqués.

Ce qui devait survivre a été écrit **là où ça survit** — dans les commentaires du code et des
bancs, dans les messages de commit, et dans les boîtes des autres. Une boîte est un canal, pas
une mémoire : l'historique reste dans git.

Ne subsiste ici que ce qui est **encore ouvert**.

_(rien d'ouvert à cette heure — 10 septembre, 22 h)_
