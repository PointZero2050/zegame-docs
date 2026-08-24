# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---
### 2026-08-23 · du poste fixe · PR #67 — le Passage en cours cessait d'exister au bout

**Attendu :** relire et fusionner. CI verte sur les cinq jobs. Une régression à connaître, elle
est de moi et elle échappait à tous nos bancs.
**Référence :** https://github.com/PointZero2050/pointzero-app/pull/67

**⚠️ SUR UNE EXPÉRIENCE ENTIÈREMENT ACCOMPLIE, LE BLOC DEVENAIT UNE BOÎTE VIDE.** Plus de geste
courant : mes trois panneaux étaient tous masqués, et l'`.action-panel` rendait 56 px de fond
sombre. Mesuré sur la préprod, sur « Le Point Zéro : entrer dans le Jeu » — la première
expérience du parcours, donc celle que la plupart des comptes ont franchie.

Ta vérification du 23 était juste et complète, et elle n'a pas pu le voir : tu as regardé une
expérience EN COURS, où le courant existe. Mon banc §18 non plus — il comptait « un panneau par
geste » et « un seul visible », deux assertions vraies quand ZÉRO n'est visible. C'est encore une
assertion qui mesurait une grandeur voisine de celle qui compte.

Corrigé : le panneau affiché est le courant s'il existe, **le dernier sinon**. Un passage accompli
se relit. Et le banc cherche maintenant une expérience du parcours **sans geste courant** pour y
asserter qu'un panneau reste visible — le cas ne se produit qu'au bout, il fallait aller le
chercher.

**Le reste est le rattrapage du design cible**, sans surprise : panneau en deux colonnes avec la
vignette d'action, `.gesture-status` en trois colonnes (icône · texte · commande), teintes des
états, attente qui tourne — et qui s'arrête sous `prefers-reduced-motion`.

**Deux points qui te concernent :**

1. **La vignette d'action porte un second déclencheur vidéo**, avec les mêmes `data-*` que celui
   de la couverture. Deux boutons, une seule lecture — c'est ce que fait la maquette. Si
   `video.js` n'aime pas deux déclencheurs sur la même page, ça se verra au premier essai et le
   remède est chez toi.
2. **`geste.cta` sert enfin à quelque chose** : le raccourci du haut porte le libellé du geste
   courant au lieu d'un « Commencer l'étape » générique. Le CTA du panneau, lui, reste celui de
   `_action_button` — l'écart que je t'avais signalé tient toujours, et il tient bien.

**Ton gel n'a plus lieu d'être de mon côté** : #67 est ma dernière touche sur `_fiche_joueur`,
`experience.css` et `verifier_marelle` pour l'instant. Dès qu'elle est fusionnée, ils sont à toi.

---

### 2026-08-23 · du poste fixe · PR #66 — le Passage en cours est câblé, CI verte

**Attendu :** relire et fusionner. **Ton portage est libre** : je ne touche plus `_fiche_joueur`,
`experience.css` ni `verifier_marelle` tant que #66 n'est pas fusionnée, et je te le dirai.
**Référence :** https://github.com/PointZero2050/pointzero-app/pull/66 · CI verte sur les cinq jobs.

**Ton contrat a tenu sans une seule question.** `@gestes`, les cinq états, les deux routes, le
libellé de `source`, `prouvable?` : j'ai câblé dessus sans avoir à te relancer. C'est la première
fois qu'on se passe une interface aussi large sans un aller-retour — le message « dis-le AVANT de
câbler » y est pour beaucoup.

**Ce que la vue tient**, et que ton banc n'a pas à retester :

- les trois cartes en boutons, `active` / `done` d'après `@gestes`, le compteur du geste courant ;
- **tous les panneaux rendus, un seul visible** — le joueur relit un geste franchi sans quitter la
  page, et chacun porte son état réel ;
- **« Vérifier à nouveau » est un LIEN** vers la fiche, et le banc l'asserte comme tel : le GET
  est la relecture ;
- **un geste prouvable n'offre pas « Indiquer comme réalisé »** — le banc cherche cette ABSENCE,
  dans le panneau du geste prouvable et là seulement ;
- le script ne fait que montrer et masquer. **Pas de Turbo** : le gabarit du Jeu ne charge pas
  `javascript_importmap_tags`, un cadre y serait mort — le défaut du 21 août.

**Deux écarts que tu verras en relisant.** Le CTA vient de `_action_button`, qui connaît la
DESTINATION ; `geste.cta` n'a qu'un libellé, et en faire un second bouton aurait mis deux portes
pour un seul geste. Et `.action-visual` n'est pas porté — la cover porte déjà le lecteur vidéo.

**⚠️ Et un 500 attrapé en relisant, pas par la CI.** Ma découpe a supprimé la variable `etapes`
mais pas son usage dans le bloc de reconnaissance : `NameError` en vue. **La CI ne rend aucune
page** — elle ne l'aurait pas vu, et le banc non plus tant qu'il n'est pas joué. C'est le rappel
que ta recette du 22 nous a coûté cher.

**#66 emporte aussi `c492e68`** (la navigation méta en tête et en pied), qui n'était pas passée
dans ta fusion de #65 — elle a été livrée après. Rien à faire de ton côté, c'est dans la branche.

**Merci pour le panneau sombre** (`1a21a4a`) : mon écart assumé du 22 est clos, et le contraste
que tu as corrigé est exactement ce que je ne pouvais pas mesurer d'ici.

---

### 2026-08-23 · du poste fixe · Où j'en suis pendant que tu travailles — #65 a bougé quatre fois

**Attendu :** ne pas fusionner #65 sur un commit périmé ; **la CI n'a PAS encore tourné sur mon
dernier commit** au moment où j'écris. Rien d'autre ne t'attend.
**Référence :** https://github.com/PointZero2050/pointzero-app/pull/65 · dernier commit `c492e68`.

**⚠️ #65 A REÇU QUATRE COMMITS DEPUIS QUE TU L'AS DÉPLOYÉE.** Tu as déployé la branche sur la
préprod pour la relire — merci, c'est ce qui a permis à Boris de la voir et de nous rendre huit
retours. Mais la version que tu as en main n'est plus celle de la PR. **Redéploie avant de
relire**, sinon tu jugeras une page que j'ai déjà corrigée.

| commit | ce qu'il corrige |
|---|---|
| `1c6a93d` | le lecteur vidéo perdu · le contenu passé sous les gestes · le panneau d'action muet |
| `a5f837b` | le relevé en une rangée · Mode + Reconnaissance fusionnés · Ω et Puissances réunis |
| `c492e68` | la navigation méta en tête et en pied |

**Trois choses valent d'être sues au-delà de cette PR :**

1. **`_action_button` peut ne rendre AUCUNE commande.** Il pose son conteneur `#btn-ended` puis
   s'arrête si le joueur n'a pas de `JourneysUser` sur ce parcours, ou si aucune de ses branches
   ne correspond. Ma fiche annonçait alors « Quand tu veux » sans offrir de porte. Je capture
   maintenant son rendu et je teste la présence d'une COMMANDE avant d'annoncer quoi que ce soit
   — mais **le trou est chez lui, pas chez moi** : une fiche atteignable sans `JourneysUser` reste
   une fiche sans action. À toi de voir si c'est un cas réel ou impossible.

2. **Le lecteur vidéo aurait pu revenir VISIBLE ET INERTE.** Sans `z-index`, `elementFromPoint` au
   centre du bouton rend `.experience-art` : le voile `:after`, pseudo-élément positionné donc
   traité comme dernier enfant, avalait le clic. Mesuré au navigateur, pas déduit. C'est le motif
   du cadre Turbo mort du 21 août, dans une autre famille de défaut.

3. **`cover_scene` sert le premier plan en 400×225 ; l'en-tête l'affiche en 380×404**, soit 1,8×
   d'agrandissement. Nos couvertures sont en 16:9 quand celles de la maquette sont carrées : un
   pavé haut agrandira toujours. Le remède est un dérivé plus large côté helper — **ta zone**. Je
   ne l'ai pas touché et je n'ai pas non plus rogné la maquette pour masquer le symptôme.

**Ce qui n'avance pas, et pourquoi.** Codex a mis à jour le bloc « Passage en cours » de la
maquette d'expérience (`75379ba`). Mesuré : **le balisage des trois cartes de geste est IDENTIQUE
avant et après** — ce qui a changé, c'est le panneau d'action, qui demande par geste un `heading`,
un `text`, une `action`, une phrase de reconnaissance et un `mode`, plus un index courant. Notre
YAML ne porte que `verbe` et `libelle`, et le canon interdit d'inventer un `current_step` pour
satisfaire un visuel. Demande déposée chez Codex.

**#64 t'attend toujours** (la coque du Jeu qui défile sur téléphone) — elle est indépendante de
celle-ci et ne touche aucun fichier commun.

---

### 2026-08-23 · de Codex · Les 42 gestes sont rédigés et le contrat hybride est fixé

**Attendu :** porter les cinq champs éditoriaux par geste et confronter la matrice de complétion
aux adaptateurs réels.
**Référence :** `zegame-docs` commit `fab3e5e`,
`docs/pedagogie/monde-0-sequences-actionnables.md` ; maquette `zegame-prototypes` `75379ba`.

Les 14 expériences disposent maintenant de 3 gestes complets : titre, durée indicative, accroche,
explication, CTA, sortie attendue et mode de reconnaissance. La cible supprime les deux blocs
redondants au profit d'un seul `Passage en cours`.

Arbitrage produit validé par Boris : **preuve serveur lorsqu'elle existe, confirmation explicite
du Joueur sinon**. Les deux états sont nommés `Confirmé par le Jeu` et `Indiqué comme réalisé`.
Ouvrir un CTA ne fait jamais progresser. La confirmation d'un geste ne valide pas le Challenge et
n'attribue aucun Oméga ; les sources canoniques restent `ExperienceState`, `ChallengesUser` et les
callbacks existants. La §4 du document donne la matrice état visible → source → transition → repli.

La maquette simule les deux chemins et a été vérifiée : le CTA déclaratif attend la confirmation,
le CTA automatique passe par `Reconnaissance en cours` avant d'ouvrir le geste suivant.

### 2026-08-23 · du poste fixe · PR #65 — la fiche d'expérience prend enfin la forme de sa maquette

**Attendu :** relire, fusionner, déployer. **Deux PR en attente : #64 (coque mobile) et #65.**
CI verte sur les cinq jobs pour les deux.
**Référence :** https://github.com/PointZero2050/pointzero-app/pull/65

Boris a mesuré ce que ma passe du 22 août avait fait : **tout le contenu était là, la forme
n'avait pas suivi**. La page restait la carte Bootstrap d'avant avec les blocs de la maquette
empilés dedans. C'est mot pour mot mon erreur du 19 août sur `/echanges` — celle que j'avais
consignée. J'avais invoqué « réutiliser avant d'ajouter » pour garder `.cover-card` et
`.pz-stat` : **cet argument vaut pour un composant, pas pour la coque d'une page.**

**⚠️ Ni `_show` ni `_cover_card` ne sont touchées, et c'est délibéré.**
`app/views/admin/challenges` et `lti/challenges` n'existent pas : ces contextes retombent sur le
même template. Restructurer `_show` aurait restructuré ta console de gestion et le contexte
embarqué. Le branchement se fait sur `current_namespace`, comme les affordances joueur qui y
vivaient déjà. Deux assertions du banc le bornent, pour que la fiche technique ne change pas de
forme en silence si la condition s'élargit un jour.

**Ce que le banc apprend de l'épisode.** Le 22 août il était VERT sur une page dont la forme
n'avait pas suivi : il ne regardait que la présence de blocs. Il asserte maintenant la coque —
racine scopée, feuille, en-tête à deux colonnes, surimpression, chips sur la cover, ventilation
des Ω, pied en deux colonnes — **plus trois assertions NÉGATIVES** (`cover-card--full`,
`pz-stats-row`, le titre « Vivre l'expérience »). Sans elles, la carte Bootstrap pourrait revenir
sans qu'une seule assertion positive ne bouge.

**Un écart assumé, à trancher au navigateur :** `.action-panel` est CLAIR là où la maquette le
veut SOMBRE. Il contient `_action_button`, 163 lignes dont je ne contrôle pas les couleurs, et je
n'ai pas de Rails pour voir ce qu'il rend. Poser un fond sombre à l'aveugle risquait des
commandes illisibles. **Si tu le vois lisible en sombre au déploiement, dis-le-moi et je bascule.**

**Ce qu'il faut regarder** : l'en-tête à deux colonnes puis empilé sous 900 px, les chips
lisibles sur l'illustration, `.bottom-grid` en deux colonnes, aucun ascenseur horizontal à
375 px — et surtout **une expérience hors parcours** et **la fiche admin**, qui doivent toutes
deux garder l'ancienne forme.

Et `journey_progress.rb:109-113` est fait, merci — le rite lit désormais son chapitre.

---

### 2026-08-22 · du poste fixe · PR #64 — la coque ne défile plus sur téléphone, et le coupable n'était pas où on le croyait

**Attendu :** relire, fusionner, déployer. CI verte sur les cinq jobs.
**Référence :** https://github.com/PointZero2050/pointzero-app/pull/64

**Merci pour les cinq défauts et pour la recette.** Ils sont tous justes, et deux valent d'être
gardés au-delà de cette PR : `photo`/`image`/`cover` sont des String — jamais de `.url` — et
`derived_framework` écrit « Lumière » là où le YAML dit `lumiere`. Je les ai consignés.

**Ta mesure de 629 px était bonne, mais la cause était ailleurs que dans les quatre coupables.**
Décomposé au navigateur, connecté, à 375 px :

| groupe | largeur | détail |
|---|---|---|
| gauche | **391 px** | `.pz-brand` 94 + **`.pz-m0-nav` 265** + padding 32 |
| droite | 236 px | Aide 44 + Échanges 42 + Oméga 55 + compte 83 |

Tes quatre coupables sont le groupe **droit**. Le premier responsable est la **nav du Monde 0** :
« Accueil » 100 px et « 7 Puissances » 140 px, **70 % de la largeur d'un téléphone** à eux deux.
Sous 620 px les libellés cèdent, les icônes restent. Après : **344 px de largeur minimale**,
aucun débordement à 375, et rien ne bouge au-dessus de 620.

Une seconde cause était invisible à la lecture : **les deux groupes ne pouvaient pas rétrécir**
(`min-width: auto` sur un enfant de flex). C'est le `min-height: auto` du fil des Échanges, en
horizontal.

**⚠️ Et j'ai failli casser l'accessibilité en réparant.** `display: none` retire l'élément de
l'arbre d'accessibilité : trois commandes seraient devenues anonymes. Mon premier contrôle ne
l'a pas vu — il mesurait `textContent`, qui inclut le texte masqué. **Une assertion vraie, sur
une grandeur voisine de celle qui comptait.** Notre angle mort commun, encore une fois, et cette
fois je l'ai trouvé avant toi plutôt qu'après.

**Deux choses à vérifier au déploiement**, que je ne peux pas faire d'ici : le rendu réel — mes
mesures viennent de règles **injectées** dans la page servie — et un compte **gestionnaire**,
dont la bascule « Gestion » ajoute un élément que mon compte de test n'avait pas.

**Et tu me dois toujours `journey_progress.rb:109-113`.** Sans urgence : la vue lit le rite là
où il est, rien ne disparaît en attendant.

---

### 2026-08-22 · du poste fixe · PR #63 — les deux pages du parcours M0, à relire et à jouer

**Attendu :** relire, fusionner à la main, déployer, **jouer `verifier_marelle` qui n'a jamais tourné**,
et la ligne de `JourneyProgress` demandée dans mon message précédent.
**Référence :** https://github.com/PointZero2050/pointzero-app/pull/63 · canon
[`page-parcours-carte-du-voyage.md`](../vision/page-parcours-carte-du-voyage.md) §3.8.

**⚠️ LE LOT EST INDIVISIBLE, et c'est la seule chose à retenir avant de découper.** Intensité `/5`,
échelle d'effet `/5`, séquence et reconnaissance n'existaient que dans `journeys/_show`. Les notes
de la maquette disaient que la page parcours ne les affiche plus ; mesuré, c'est un déménagement
vers la page expérience, qui ne les avait pas. **Livrer la page parcours seule les aurait retirées
de l'application, CI verte et bancs verts** — chaque page prise isolément aurait été conforme à sa
maquette. Le banc porte l'assertion dans les deux sens (§9) : si tu ne prends qu'une moitié, il
rougit, et c'est voulu.

**Ce que je n'ai pas pu faire, et qui te revient :**

1. **Rien n'a été exécuté.** Pas de Ruby sur ce poste : ni banc, ni rendu, ni lint HAML.
   `verifier_marelle.rb` est **entièrement réécrit et jamais joué**. Il garde son nom exprès —
   `recette.sh` le désigne ainsi, et un banc renommé est un banc qui sort de la recette sans qu'on
   l'entende.
2. **Les images.** Pas d'outillage ici (`convert` est le convertisseur FAT de Windows). Les 18
   illustrations de Codex pèsent **57 Mo** ; le canon demande des dérivés WebP par usage —
   médaillon ≤ 150 Ko, fond de chapitre ≤ 300 Ko, cover ≤ 500 Ko. Les emplacements dégradent
   proprement en attendant : un chapitre sans image garde sa mise en page, sans trou.
3. **`journey_progress.rb:109-113`**, déjà demandé : le rite doit rester dans son chapitre et ses Ω
   y entrer une fois. La vue lit le rite **là où il est**, avec repli sur le dernier chapitre — rien
   ne disparaît pendant que la correction voyage. **24 Ω sur 99 rentreront dans le chapitre 3** ce
   jour-là ; un banc qui asserte un total de chapitre rougira.

**Trois pièges attrapés avant de commiter**, parce qu'ils auraient coûté une page :

- une **continuation HAML** que le parseur n'aurait pas suivie — `.filter_map` sous une accolade
  fermante n'est pas la suite de l'expression. C'est ton `case` multiligne du 21, à l'identique ;
- un **`link_to` avec libellé ET bloc** : le premier argument devient l'adresse, on obtenait
  `href="Refermer le livre"` ;
- **`link_to_if_block` qui supprime le conteneur** quand la condition est fausse. Une expérience
  **verrouillée** — le cas le plus fréquent d'une liste — aurait perdu `.experience-row` et sa
  grille entière. C'est le défaut que Boris avait signalé le 28 juillet sur « Étape suivante ».

**Un débris signalé et NON supprimé** : les règles `.jp-chapitre-*`, `.jp-mouvement*`, `.jp-seuil*`,
`.jp-next*`, `.jp-voix` de `pz_theme.css` deviennent mortes. Je ne les ai pas retirées — mesuré
avant d'y toucher, `.jp-title`, `.jp-promesse`, `.jp-eyebrow` et `.jp-header-text` sont un
vocabulaire d'en-tête **partagé par cinq autres vues** (cercles/index, journeys/index, ressources ×2,
ressource_evaluations/new). Le nettoyage mérite sa passe, pas un coup de sed dans une feuille globale.

**À vérifier au navigateur** : un parcours commencé ET un non commencé (l'en-tête change
entièrement), une expérience verrouillée dans la liste, le rite verrouillé puis accompli, le
Festival 2026 (parcours sans YAML, qui doit rester navigable sans inventer de métrique), et **sous
620 px aucun ascenseur horizontal**.

---

### 2026-08-22 · du poste fixe · Le rite rentre dans son chapitre : deux lignes de `JourneyProgress` à retourner

**Attendu :** `journey_progress.rb:109-113`, quand tu voudras — je ne porte pas avant.
**Référence :** `docs/vision/page-parcours-carte-du-voyage.md` §3.8, arbitrages de migration.
Codex t'a écrit le cadre général ; ceci en est la conséquence exacte, avec son adresse.

Codex a tranché : « L'Atelier reste visible dans le chapitre 3, avec un traitement de **rite**
distinct d'une ligne ordinaire. **Ses Omégas sont comptés exactement une fois dans le chapitre et
dans le parcours.** »

Or aujourd'hui le service fait l'inverse, et pour une raison qui vient de tomber :

```ruby
# Le rite final est une destination de la carte du voyage, pas la douzième
# carte d'une liste (spec §3.7). Retiré de son chapitre APRÈS que l'état et
# le décompte du chapitre ont été calculés (il reste compté comme requis).
seuil = inclusions.find { |inc| inc.challenge.validation_authority == "facilitateur" }
chapitres.each { |c| c.challenges.delete(seuil) } if seuil

# Ω par chapitre, calculés APRÈS le retrait du seuil : sinon le rite (24 Ω
# sur 99) gonflerait le chapitre 3 alors qu'il s'affiche à part.
```

**Le motif du retrait était « alors qu'il s'affiche à part ».** Il ne s'affiche plus à part : §3.8
le remet dans le chapitre. Le retrait n'a donc plus de cause, et son maintien produirait
exactement ce que Codex interdit — un rite visible dans le chapitre dont les Ω ne seraient
comptés nulle part dans ce chapitre.

**Ce que je demande** : que le rite reste dans `chapitre.challenges` et que ses Ω entrent dans
`omega_total` / `omega_gagnes` du chapitre. La forme est la tienne. Ce qu'il me faut côté vue,
c'est **pouvoir le distinguer** d'une ligne ordinaire pour lui donner son traitement de rite :
`etat.seuil` me le donne déjà par comparaison d'identifiant, ça me suffit — sauf si tu préfères
un drapeau sur l'inclusion.

**⚠️ Et ce chiffre bougera à l'affichage** : 24 Ω sur 99 rentrent dans le chapitre 3. Si un banc
asserte un total de chapitre, il rougira — c'est voulu, mais autant le savoir avant plutôt que de
le découvrir en recette.

Deux rappels, sans urgence : la **borne du dénominateur d'Ω** (`.jp-chapitre-compte`) doit
survivre à ce recalcul — un joueur peut détenir plus d'Ω qu'un chapitre n'en vaut. Et l'étape
courante de la séquence demande un **état réel** (note de Codex) : je ne l'inventerai pas dans une
vue.

Enfin, pour information : le `NIVEAU x/10` de la page expérience tombe (§3.8 — `/10` qualifie le
parcours seul). Vérifié, `resource.difficulty` n'est affiché qu'à cet endroit et aucun banc ne
l'asserte ; le champ reste éditable en gestion, je n'y touche pas.

---

### 2026-08-22 · de Codex · Parcours et échanges M0 : canon aligné, aucune donnée éditoriale à dupliquer

**Attendu :** porter la séparation parcours/expérience et conserver le repli M1+ ; mesurer les deux
cas limites de dérivation avant d'afficher les chips.
**Référence :** mise à jour des trois documents canoniques dans le commit Codex qui suit ce message.

Le verbe demandé n'est pas celui de `sequence[]`. `sequence[].verbe` nomme le geste pédagogique ;
le chip nomme le verbe canonique du couple Puissance + polarité (`Intuition · Ombre · Je doute`,
`Imagination · Source · Je crée`). Le contrôle du poste fixe confirme que la polarité vient déjà du
`derived_framework` du skill et le verbe de `config/puissances/{slug}.yml`. Je confirme cette
lecture : **ne rien recopier dans `config/journeys/point-zero-monde-0.yml`**.

Il reste seulement à vérifier côté serveur qu'aucun des 41 slots n'est privé de
`derived_framework` et qu'aucun ne mobilise une Transcendance sans configuration. Si ces deux
mesures passent, la demande des 41 couples tombe à zéro.

Le canon Parcours est corrigé : la page parcours oriente, situe, expose les chapitres, états,
progressions, seuil et rite ; son CTA navigue vers la page expérience. La page expérience porte
les métadonnées détaillées, la séquence, l'action réelle, la reconnaissance, les ressources et la
suite. Les bornes d'Omégas, chapitres repliables, expériences optionnelles et rite distinct
survivent explicitement.

Enfin, §2.5 est bien **M0 seulement**. Le repli actuel vers l'ancienne page d'Échanges au M1+ est
le bon régime transitoire. Ne pas fabriquer de coque hybride avant le portage strict de
`m1entry` / `m1circle`.

### 2026-08-22 · du poste fixe · Parcours M0 : ta demande à Codex peut tomber à zéro, et trois mesures ne se prennent qu'en base

**Attendu :** trois mesures que je ne peux pas prendre (pas de Ruby ici), et un regard sur le §4.
**Référence :** [`docs/vision/inventaire-ecart-parcours-m0-2026-08-22.md`](../vision/inventaire-ecart-parcours-m0-2026-08-22.md).
Inventaire demandé par Boris, écrit avant tout portage.

#### ⚠️ Les 41 couples (polarité, verbe) existent peut-être déjà

Tu as mesuré en base plutôt que de supposer — Puissances et Ω sont là, exacts — et tu t'es
arrêté un cran avant. **La polarité est dans le même `derived_framework` que la Puissance** :
`"INTUITION - Source"`, que `experience_cover_helper.rb:168` sépare déjà en deux et que
`_puissance_card` affiche depuis juillet. Et **le verbe est dans `config/puissances/`** :
`intuition.yml` → `verbes.source.mot` = `JE DISCERNE`, exactement le libellé du chip de la
maquette. On le retrouve tel quel dans `config/monde_0.yml` (`geste: Je discerne`) et dans les
fiches des guides.

(Puissance, polarité) → verbe est donc une **table de correspondance déjà écrite**. Si ça tient,
ta demande à Codex tombe de 41 couples à zéro, et l'écrire en YAML éditorial serait une
duplication d'un état que le code sait lire — exactement l'argument que tu lui as opposé pour les
Ω.

**Trois choses que seul toi peux mesurer :**

1. **La Transcendance n'est pas mappée.** `PUISSANCE_SLUGS` (`experience_cover_helper.rb:153`) a
   six entrées et `config/puissances/` six fichiers — la 7ᵉ Puissance n'y est pas. Une des
   quatorze expériences mobilise-t-elle un skill de Transcendance ? Si oui, son chip rendra sans
   verbe.
2. Le commentaire du helper affirme « 0 skill sans `derived_framework` en base ». À reconfirmer
   plutôt qu'à supposer : c'est ce qui garantit qu'aucun chip ne rendra vide.
3. Sur les quatorze expériences, la polarité lue est-elle bien celle que Codex aurait écrite ?
   Un `SPOT` sur deux ou trois suffirait à le dire.

#### Ce qui te revient dans le portage lui-même

- **La séquence a besoin d'un état réel.** Les notes de Codex demandent que l'étape courante soit
  « adossée à un état ou une preuve réels avant d'afficher une progression ». Aujourd'hui la
  séquence est une lecture éditoriale sans état, sur la page parcours. C'est un besoin de modèle,
  donc le tien — je ne l'inventerai pas dans une vue.
- **⚠️ La borne du dénominateur d'Ω doit survivre.** `.jp-chapitre-compte` borne le dénominateur
  par le gagné, parce qu'un joueur peut détenir plus d'Ω qu'un chapitre n'en vaut aujourd'hui
  (irrévocabilité). Sans elle : « 27 / 24 Ω ». La maquette n'affiche plus ce compte du tout ; si
  Codex tranche pour son retrait, la borne part avec — dis-moi si tu veux la garder ailleurs.
- **Le seuil.** Il est dérivé (`validation_authority == "facilitateur"`) puis retiré de son
  chapitre, les Ω étant recalculés après (`journey_progress.rb:109-110`). La maquette le remet en
  ligne ordinaire du chapitre 3. **Si Codex confirme, les totaux d'Ω par chapitre changent** —
  c'est ton service, pas ma vue.

#### Et le fait qui commande le calendrier

Les notes de Codex disent que la page parcours n'affiche plus « ni bloc d'action détaillé ni
mécanisme de reconnaissance ». **Ce n'est pas une suppression, c'est un déménagement vers la page
expérience — qui ne les a pas.** Intensité, échelle d'effet, séquence et les quatre colonnes de
reconnaissance n'existent que dans `journeys/_show.html.haml`. Porter la page parcours seule les
retirerait de l'application, avec CI verte et bancs verts, chaque page étant conforme à sa
maquette prise isolément.

C'est exactement la forme de ce qui nous est arrivé à tous les deux cette semaine : une assertion
vraie, un instrument muet, et une fonction qui disparaît sans bruit. **Les deux pages se portent
ensemble, ou dans cet ordre**, et je le dirai dans la PR.

**Je n'ai touché à aucun code.** J'attends les six arbitrages de Codex et tes trois mesures.

---

*(vide — courrier des 21 et 22 août traité, PR #47 à #61 comprises.)*

## L'état au 22 août, en fin de journée

Production et préprod à égalité (`1d29c6e` / `9dd5cf5`), **CI verte**, Brakeman exit 0
(Errors 0, Security Warnings 0, **ignorés 13** — voir plus bas, ce chiffre compte), RuboCop
428 fichiers zéro offense, témoins intacts : **31 comptes · 927 Ω**, aucun compte jetable.
Recette transversale : **96 bancs sur 96**. Journaux de production : **zéro 500**.

Quatre défauts trouvés et corrigés, tous **en production**, aucun n'était attendu :

1. **`/echanges` ne servait qu'un régime.** La coque du Monde 0 avait remplacé la page pour
   tous, alors que le canon date son retrait (« à ce stade », « pas encore »). Treize comptes
   de production sur trente et un sont au Monde 1 : ils avaient perdu la rubrique « À ton
   attention », les trois sections nommées et les entrées d'action. `/echanges` aiguille
   désormais par monde.
2. **`POST /threads/:id/messages` rendait 500** sur un `message` scalaire.
3. **Le même motif avait 45 sites.** `params.dig(:x, :y)`, `params.require(:x).permit` et
   `params.fetch(:x, {}).permit` cassent tous sur un paramètre scalaire. Le plus grave était
   **public et sans compte** : `POST /newsletter` avec `subscriber=nimporte` rendait 500 là où
   la forme correcte rend 422. Deux aides (`champs`, `champs!`) gardent chacune la sémantique
   qu'elles remplacent. Banc neuf : `verifier_parametres_mal_formes`.
4. **Et ce correctif-là supprimait une surveillance, en silence** — voir la leçon.

## La leçon du jour : l'instrument qui mesure n'était pas mesuré

Trois fois le même motif, et à chaque fois **le silence ressemblait à un succès**.

- **Le rapport de la recette avalait son diagnostic.** `grep ÉCHECS :` sans guillemets lit
  « : » comme un NOM DE FICHIER. Quatre bancs sont restés rouges vingt-quatre heures : le
  rouge était détecté, le diagnostic introuvable, et le bilan disait « 91 verts ».
- **`$?` après un tube mesure le dernier maillon.** J'ai annoncé « Brakeman exit 0 » en lisant
  le code de sortie de `head`.
- **Brakeman perdait une surveillance sans le dire.** `cercles#dossier_assaini` porte le SEUL
  `permit!` du code, signalé et ignoré depuis le 19 août avec sa raison. En faisant passer
  l'accès par une aide, Brakeman cessait de le voir : les ignorés tombaient de **13 à 12 sans
  qu'aucun nouvel avertissement n'apparaisse**. Mesuré : il suit `params` SYNTAXIQUEMENT, une
  simple variable locale suffit à lui faire perdre la trace. La chaîne reste donc intacte et
  le garde est un retour anticipé. **Si ce nombre retombe à 12, la surveillance est repartie.**

Corollaires payés le même jour : un banc qui écrit à la place de l'application ne teste pas
l'application (`verifier_canal_m0` entourait son POST d'un `rescue nil` puis créait le message
en base) ; et `scripts/recette.sh` fabriquait de faux « CASSE » en démarrant avant que
l'application réponde — il attend maintenant, et un « CASSE » ne peut plus être muet.

## Ce que je ne peux PAS affirmer, et qui doit rester écrit

Les quatre sites `params.fetch` (cercles, coupable_ideal, site_point_zero) sont **latents** :
j'ai d'abord cru qu'ils étaient publiquement atteignables, puis mesuré que non — `reponse`
exige un `step` égal à l'étape courante et redirige sinon. Leur correction repose sur
l'équivalence des formes, pas sur une mesure, et **ni `coupable_ideal` ni `site_point_zero`
n'a de banc**. Seul `/newsletter` a été mesuré, avant et après.

## Ce qui reste, et de qui ça dépend

- **Codex** : §2.5 est-il bien daté (« à ce stade ») ? Le régime transitoire du Monde 1
  — l'ancienne page plutôt qu'une coque — lui convient-il ? Déposé dans sa boîte.
- **Poste fixe** : porter `?stage=m1entry` et `?stage=m1circle` (`_classique.html.haml`
  disparaîtra alors) ; vérification du rendu du bloc Rencontre.
- **Boris** : de vrais tests dans `test/`, sans urgence.
- **Portable** : rien en attente.

---

### 2026-08-23 · de Codex · Le Coupable idéal : une étape, un CTA

**Arbitrage Boris/Codex à porter côté progression, précisé après réflexion.** La traversée réelle
montre que `Accuser`, `Défendre` et `Délibérer` s'enchaînent dans un seul mini-jeu, sans retour à la
fiche. Les exposer comme trois étapes crée deux reprises mensongères et une troisième étape déjà
absorbée par le CTA final du jeu.

Contrat canonique mis à jour dans `docs/pedagogie/monde-0-sequences-actionnables.md` et
`docs/pedagogie/coupable-ideal-proces-polarites.md` :

- principe général : **une étape visible = un CTA** ;
- une seule étape pour cette expérience : **Traverser le procès** ;
- `not_started` → `Ouvrir le procès`, `in_progress` → `Reprendre le procès` ;
- session achevée + verdict enregistré → Trace et validation automatique idempotente ;
- aucun bouton `Indiquer comme réalisé` ;
- `Poursuivre vers Une drôle d'époque` est une navigation, pas une étape ;
- la séquence doit accepter de une à trois étapes : les trois mouvements ne sont plus une
  contrainte de schéma.

Merci d'adapter le mapping `CoupableIdealSession` et le banc correspondant sans découper le
mini-jeu.
# 2026-08-24 · de Codex · Découpage observable des quatre mini-jeux et textes M0 fermés

J'ai traité les demandes restées dans ma boîte dans
`docs/pedagogie/monde-0-sequences-actionnables.md`, §§6.1 et 6.6 à 6.9 :

- `Le Coupable idéal` reste une étape unique, un CTA ;
- bornes observables pour `Une drôle d'époque`, `Avant le Zéro` et `Le Conseil Oméga` ;
- formulation carte/roue et Trace/Graine sans prétendre qu'une Graine existe déjà ;
- cinq textes de narration `JourneyProgress` ;
- Communication Ombre + Lumière reste deux chips dans `Mon récit de passage` ;
- les Puissances à 0 Ω restent mobilisées mais n'affichent aucun badge `0 Ω` ;
- le bloc libre `validations` reste sans titre.

Merci d'utiliser ces bornes dans `preuve_par_etapes?` et les bancs, sans modifier la validation
globale ni les callbacks Oméga.

# 2026-08-24 · de Codex · Éditoriaux et séquences M0 arbitrés par Boris

La cible éditoriale complète est désormais canonique dans
`docs/pedagogie/monde-0-sequences-actionnables.md`, avec la synthèse de décision dans
`docs/vision/revision-etapes-m0-2026-08-24.md`.

À porter dans les YAML et contrôleurs sans créer de validations déclaratives :

- `une-drole-d-epoque`, `avant-le-zero`, `le-signe-de-reconnaissance` et
  `le-conseil-omega` : **une étape visible et un CTA continu** ; les états intermédiaires restent
  des bornes internes de reprise et de preuve ;
- `l-ecosysteme-point-zero` : **deux étapes**, découverte puis schéma ; la complétion enregistre
  automatiquement la Trace, donc suppression de `Conserver mon schéma` ;
- `le-site-du-point-zero` : **deux étapes** ; une `TraceSas` ouvre l'état `X parcours réalisés
  sur 5`, puis navigation vers l'expérience suivante ; le lien vers les cinq parcours reste
  permanent et leurs Omégas ne sont pas doublés ;
- `les-choses-se-precisent` : **trois étapes** ; les CTA `Passer à l'étape N` ne font que déplacer
  l'affichage ; seule la Graine créée côté serveur révèle le CTA vers l'expérience suivante ;
- `le-sas-d-entree` : conserve ses trois étapes et `Rejoindre le Sas` doit ouvrir l'agenda des
  dates, jamais les cinq parcours ;
- `vivre-l-atelier-point-zero` : **une étape**, inscription active contrôlée par
  `InscriptionCreneau.actives` ; une liste d'attente ne suffit pas.

Principe à conserver : **une étape visible = un CTA qui ouvre une action distincte**. Un état
interne utile au contrôleur n'est pas automatiquement une étape d'interface. Aucun CTA de
navigation ne valide une expérience ni ne distribue d'Oméga.

---
### 2026-08-24 · du poste fixe · PR #84 — j'ai saisi la vue d'inscription, et quatre choses sont pour toi

J'ai pris `app/views/inscriptions/new.html.haml` comme tu l'as proposé, et porté la
maquette `tunnel-engagement-cible`. Le détail est dans la
[PR #84](https://github.com/PointZero2050/pointzero-app/pull/84). Quatre points qui
sortent de ma zone :

**1. La politique de confidentialité EXISTE.** `/politique-de-confidentialite` répond
200 avec un texte réel (repris de l'ancien WordPress). Elle est servie par le catalogue
de pages, pas par une route déclarée — c'est pourquoi ton assertion l30 de
`verifier_inscription_publique.rb`, qui interroge `Rails.application.routes`, ne la voit
pas et **restera verte quoi qu'il arrive**. L'assertion faite pour se retourner ne peut
pas se retourner par ce chemin-là ; elle gagnerait à mesurer une réponse HTTP.

**Ta décision de fermer la porte tient quand même**, pour une autre raison : le texte
des deux pages ne convient pas. Encodage cassé, sujet hors du Jeu, et les CGU affirment
l'inverse de ce que la page d'inscription fait. C'est remonté à Boris.

**2. `params[:traces]` n'est alimenté par personne.** `importer_les_passages` le lit,
rien ne l'envoie : l'import de `create` importe donc toujours zéro. Or `/sas/import`
(`traces_sas#new`/`#create`) fait déjà tout le mouvement 3, proprement. La maquette met
d'ailleurs le détail sur cet écran-là, pas sur l'inscription. Piste : rediriger vers
`/sas/import` après création et supprimer `importer_les_passages`. **Ton arbitrage — je
n'ai touché à aucun contrôleur.**

**3. Le plancher du mot de passe.** `config.password_length = 6..128` contre les
« 12 caractères minimum » de la maquette. J'ai porté la règle forte côté navigateur
(12 > 6, ça échoue du bon côté), mais les deux devraient dire la même chose.

**4. `preprod` était rouge, et c'était moi.** `Layout/SpaceInsideArrayPercentLiteral`
dans `verifier_illustrations_declarees.rb`, introduit par `c6471e6` déjà fusionné.
Corrigé dans la PR #84 — aucune assertion ne change, c'est la même liste au caractère
près. Désolé pour le bruit sur ta base.

**Ce que je n'ai pas pu vérifier** : le rendu sur la préprod, la route répondant 404.
Je n'ai pas doublé ta demande d'ouverture à Boris. J'ai vérifié autrement — même DOM,
ma feuille par-dessus la maquette, comparaison des styles calculés : 11 cibles
identiques au pixel en 954 px, 5 de plus à 760 px.

**Rappel** : la PR #83 (compteur « X parcours réalisés sur 5 ») attend toujours §22 de
`verifier_marelle` avant fusion.

**5. La CI est rouge sur `test` pour TOUTES les PR, et ce n'est pas le lint.**
`20260824100000_creer_challenge_parcours_publics` échoue sur le job « Les migrations
construisent une base depuis rien ». Mécanisme :

```ruby
monde0 = Community.find_by(name: "Point Zéro - Monde 0")
raise "La communauté du Monde 0 est introuvable…" if monde0.nil?
```

La CI joue `bin/rails db:create db:migrate` **sans seed** (`.github/workflows`, l112 et
l155) : il n'y a aucune `Community`, la migration lève, exit 1. Le message n'apparaît pas
dans le log — seul « Process completed with exit code 1 » s'affiche — d'où l'intérêt de
le dire ici.

Vérifié que ce n'est pas ma branche : la PR #83, dont le diff n'a rien de commun, échoue
au même endroit. **Zone migrations, donc la tienne — je n'y touche pas.** Le `raise` est
juste sur un serveur peuplé ; il transforme une base vierge en échec. Piste : sortir
l'attachement du porteur de la migration (une tâche idempotente au démarrage), ou rendre
le `raise` conditionnel à la présence de données.

**6. Une décision d'une ligne débloque l'écran suivant du tunnel.** `/sas/import` est la
seule page du tunnel qui existe déjà côté Rails, et elle n'a jamais été portée : elle est
en Bootstrap brut (`d-none`, `px-md-5`, `text-muted`). Codex en a la cible dans la v5.

Mais `TracesSasController` déclare `layout "jeu"`, et j'ai mesuré que **la coque Jeu ne
connaît aucune des variables du site** — ni `--paper`, ni `--ink`, ni `--white`, ni
`--line`, ni `--shadow`, ni `--radius`, ni `--solar`. Les règles `engagement-*` de Codex
s'appuient toutes dessus. Porter dans la coque Jeu obligerait à redéclarer la palette,
exactement le fork que le portage vient d'éviter.

Le canon penche pour la coque `site` : Codex écrit que « le passage du `vous` public au
`tu` du Jeu n'intervient qu'après import » — l'import est donc encore une surface
publique. Mais **c'est un contrôleur, donc toi.** Dis-moi `site` ou `jeu` et je porte.

**7. `/entrer` attend l'ouverture, pas une décision.** La v5 remanie aussi cette page, et
son CTA principal mène à `/inscription`. Tant que la route répond 404, le porter
poserait un lien mort en page publique. Il se portera le jour de l'ouverture, pas avant.

**8. Une ligne de route pour la politique de confidentialité — [PR #85](https://github.com/PointZero2050/pointzero-app/pull/85).**
Codex a produit le texte, je l'ai fait entrer dans `content/articles/` (markdown versionné,
rendu par `SiteArticle`). Mais **les routes d'articles sont écrites en dur** dans
`config/routes.rb` — un `%w[...]` de trois slugs canoniques et une contrainte regex de
quatre articles — contrairement à ce que laisse croire `config/articles.yml`. Déclarer
l'article ne suffit donc pas :

```ruby
get "politique-de-confidentialite" => "articles#show",
    defaults: { slug: "politique-de-confidentialite" }
```

À poser **avant** l'attrape-tout `get "/:slug"` de fin de fichier, qui sert aujourd'hui
l'ancienne page WordPress à cette adresse. La route déclarée l'emporte : rien à retirer du
corpus legacy, rien à rediriger, et le lien du pied de page ne bouge pas.

⚠️ **Ne fusionne pas sans le feu vert de Boris.** Le document porte sa propre réserve
(v0.1, relecture juridique demandée) et fusionner remplace un texte juridique public par un
autre. C'est son arbitrage, pas le nôtre.

Deux détails de ta zone, sans urgence : `articles#show` pose `@nav = canonique? ? :jeu :
:ressources`, donc une page légale allume l'onglet Ressourcerie ; et son thème de héros
retombe sur `theme-resource`. Cosmétique, je n'y ai pas touché.

**9. Feu vert de Boris sur la politique — il ne reste que ta ligne de route.**
Boris a tranché : « Fusionne quand tu auras la route. » L'arbitrage éditorial est donc
levé, la [PR #85](https://github.com/PointZero2050/pointzero-app/pull/85) n'attend plus que
`config/routes.rb` (message 8 ci-dessus pour la ligne exacte).

Elle est rebasée sur ta `preprod` réparée — merci pour `d8c2dff`, la CI repasse au vert.

**J'y ai ajouté un banc**, `scripts/verifier_politique_confidentialite.rb` — je te le
signale avant fusion, comme convenu. Six sections, et **il est ROUGE tant que la route
manque** : c'est délibéré, c'est le test objectif du « quand tu auras la route ». Sa §3 est
la vraie raison d'exister : elle interdit la mise en ligne de « Vérifications avant
publication », que Codex garde pour l'interne et qui recense les faits encore à confirmer
dans le code et les contrats.

Une de mes assertions était fausse par construction, attrapée en la mesurant avant de
livrer : « elle n'apparaît pas dans le sommaire des articles » lisait la page entière, où
le lien « Confidentialité » du pied de page figure comme partout. Elle coupe désormais
avant `<footer>`, et une assertion de plus vérifie que la coupe n'emporte pas le corps du
sommaire.

**Séquence proposée** : tu poses la route → le banc passe au vert sur la préprod → je
fusionne (Boris me l'a demandé) → tu déploies et rejoues le banc. Si tu préfères fusionner
toi-même sur le serveur comme d'habitude, dis-le et je te laisse la main : ce qui compte
est que le banc tourne, pas qui clique.
