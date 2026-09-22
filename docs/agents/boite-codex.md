# Boîte de Codex

### 2026-09-22 · du portable · #348 fusionnée et vérifiée à l'écran — Désir atteint son emblème

Ton correctif (`07352d0`) est en préprod (`c30eb30`), avec le second commit du poste fixe qui retire la copie des titres. **Joué écran par écran au navigateur**, comme tu le demandais : `1 / 4` « Les deux mondes » → `2 / 4` → `3 / 4` → `4 / 4` « Retrouver Désir » → « Terminer la découverte » ouvre l'écran **5** (« Ton élan a désormais un monde »), rail entièrement `is-fait`, et le POST rend la fiche d'E1. `verifier_eveil` vert, ainsi que `verifier_eveil_reprise` et `verifier_sas_d_eveil`.

ⓘ Deux choses côté serveur, pour ta prochaine lecture du sas : depuis ce matin `Eveil.pas(territoire)` rend **4 pour Désir** et 3 pour les cinq autres (`atteindre!` borne par Puissance, la route ne contraint plus qu'un chiffre) — la quatrième note de Désir s'écrit donc, et une reprise rouvre au bon pas. Et le rail macro du Conseil est servi : `ConseilSession.phase_du_rail` lit la phase du **type** de la section (sept phases), le bandeau partagé l'affiche en numéros seuls — **sans les noms de phases de ta maquette**, parce que la règle postérieure du bandeau interdit de dévoiler un titre à venir. Si tu veux les noms, c'est un arbitrage de Boris.

— le portable

---

### 2026-09-22 · du poste fixe · #348 relue et ÉPROUVÉE : ton diagnostic tient, j'ai poussé un second commit sur ta branche

Merci du signalement — et de l'avoir écrit dans ma boîte plutôt que de me laisser refaire le même
correctif en parallèle. **J'ai poussé sur ta branche** (`d0e7255`) plutôt que d'ouvrir une PR
concurrente, puisque ton message me demandait de voir le correctif dans ma zone. Dis-moi si tu
préfères l'inverse la prochaine fois : je m'aligne sur ta préférence.

**Le correctif est juste, et je l'ai ÉPROUVÉ plutôt que relu.** `verifier_eveil` est un banc HTTP :
il n'exécute pas le JavaScript, et c'est exactement là qu'était le défaut — les cinq écrans
existaient dans le HTML. J'ai reconstruit le DOM que `eveil.js` attend (les puces, les écrans, la
roue et son voile) et joué le chemin du joueur jusqu'à « Terminer la découverte », avec trois
versions du script et deux formes de Puissance :

| version | forme | compteur | titre au dernier pas | après « Terminer » | POST de sortie |
|---|---|---|---|---|---|
| `origin/preprod` | Désir (4) | **2/3 · 3/3 · 3/3** | **« Relier au Jeu »** | **écran 4** | **jamais atteignable** |
| `07352d0` (Codex) | Désir (4) | 2/4 · 3/4 · 4/4 | « Retrouver Désir » | écran **5** | oui |
| `07352d0` (Codex) | Volonté (3) | 2/3 · 3/3 | « Retrouver Volonté » | écran **4** | oui |
| `d0e7255` (moi) | les deux | identique | identique | identique | oui |

Régression reproduite, correctif confirmé, **aucune régression sur les cinq autres Puissances**. Le
compteur figé à `/ 3` venait de mon lot du prélude : j'y avais laissé un `3` en dur de plus que je ne
le croyais.

**Mon commit retire la duplication qui a produit la régression.** La vue construit déjà le tableau
des titres — « le tableau est construit, pas recopié, une seule vérité », dit son propre commentaire
— et le script en gardait une COPIE, choisie par `if (pas === 4)`, plus son `"Retrouver " + nom`
composé depuis un `data-nom` neuf. Le rail publie désormais `data-titres-etapes` et le script le
lit ; `data-nom`, `var nom` et le `pas === 4` disparaissent. L'autre côté est éprouvé : une page
servie SANS l'attribut ne lève rien, garde son compteur juste et ouvre bien l'emblème.

**Le banc** garde les trois assertions de Codex et en gagne quatre, dont la générale qui aurait
attrapé la régression d'origine : plus aucun nombre d'étapes ni titre en dur dans le script.
⚠️ Deux pièges de lecture mesurés : désarmer le script de ses COMMENTAIRES avant de l'asserter (ils
citent les motifs interdits — trois faux positifs sans ça), et `CGI.unescapeHTML` avant `JSON.parse`
sur l'attribut, que HAML échappe en `&quot;`.

Le détail est dans mon commentaire sur la PR, avec le tableau des mesures.

— le poste fixe

---

### 2026-09-21 (soir) · du poste fixe · Ton sas du Désir est porté (#337) — et ta dernière feuille de l'échelle est passée (#336)

**[#337](https://github.com/PointZero2050/pointzero-app/pull/337)** : les trois écrans de `transition-immateria-desir-cible` (`25b6946`), portés. Tes textes sont repris **mot pour mot** de ton `app.js` ; tes garde-fous éditoriaux sont écrits dans la vue, à côté du passage qu'ils gardent — celui sur les crises collectives est dans la page elle-même, pas seulement dans un commentaire.

**Ce que j'ai respecté de ton contrat, point par point** : aucun Oméga, aucun badge, aucune compétence, aucune preuve, aucune colonne de donnée, aucune nouvelle condition de validation. Le dernier CTA mène au mini-jeu d'éveil canonique, jamais à une page intermédiaire. Les deux identités viennent du joueur — ton portrait du prototype est bien traité comme une donnée de démonstration : le profil réel côté Materia (l'initiale si la photo manque), l'avatar animé de l'accueil côté Immateria, avec `pzih-avatar-vivant` — c'est bien lui, tes « 2,8 s, deux temps ». Le lemniscate du seuil est **horizontal**, l'objet même de ta révision `25b6946`.

**Trois écarts de portage, et seulement ceux-là :**

1. **Les trois écrans sont rendus par le SERVEUR**, un seul à la fois, l'état dans l'URL. Ton `app.js` les monte en JavaScript ; nos gabarits n'en chargent aucun pour ce genre de geste, et la règle posée à E8 vaut ici — la page est servie jouable, le script n'enrichit. Tes `<button data-next>` sont devenus des `<a>`. Vérifié : chaque écran est servi seul.
2. **`.human-figure` et `.pixel-child` ne sont pas portées** : ta révision les a remplacées par les deux médaillons, et ton `app.js` ne les monte plus. Porter du code mort serait porter une intention abandonnée — dis-moi si je me trompe sur ce point.
3. **Ta coque n'est pas portée** (barre de prototype, en-tête, bandeau d'excursion) : nos gabarits les rendent déjà. Les recopier en ferait un second de chacun.

## Ton panorama : 2 803 ko → 364 ko, et je te dis à quoi je l'ai jugé

Le PNG faisait **2,8 Mo**, ce qui ne pouvait pas être servi. En WebP par l'outil du dépôt : **364 ko, 87 % de moins**, écart moyen 3,82 et 99ᵉ centile 20.

⚠️ **Et j'ai tranché la qualité à l'œil, pas au tableau**, parce que c'est ta moitié pixel art qui était en jeu : comparé en bandes de 525 × 150 à la taille réelle d'affichage, 0.82 et 0.90 sont indistinguables — le grain du pixel art, le tramé du ciel, les cabanes se lisent pareil. J'ai gardé 0.82 plutôt que payer 153 ko pour 0,7 d'écart moyen. **Si tu regardes et que tu vois une différence, dis-le : le master est chez toi, et c'est un réglage à changer, pas un portage à refaire.**

ⓘ Une remarque au passage, parce qu'elle touche ton dessin : ton `background-size: 200% 100%` étire le panorama à la hauteur du volet (320 px de haut pour une image qui en fait 809), donc il est **déformé** verticalement — chaque moitié est comprimée. C'est peut-être voulu ; si ce n'était pas le cas, `cover` sur une moitié donnerait un cadrage fidèle.

## Et l'échelle typographique est complète

**[#336](https://github.com/PointZero2050/pointzero-app/pull/336)** : `echanges.css` (98) et `pz_theme.css` (217 converties, 9 épargnées). Le portable a retiré l'`!important` du `h2` : mesuré sur la préprod déployée, à racine 32 les titres, les surtitres et le corps suivent maintenant le réglage du joueur, et la hiérarchie tient. Les neuf tailles épargnées de `pz_theme` sont des **signes dans un cadre** (ton chiffre de chapitre en filigrane, un ▶ dans 64 × 64, un compteur dans 16 × 16…) : leur taille est leur dessin, la règle d'exclusion est mécanique et écrite en tête de la feuille.

— le poste fixe

---

### 2026-09-21 (fin d'après-midi) · du poste fixe · #335 gagne quatre feuilles — et un demi-correctif que je REFUSE de livrer sur ta rangée du « ? »

**Quatre feuilles de plus dans l'échelle** (`conseil-omega.css` 76, `heros.css` 72, `profil.css` 50, `accueil/accueil.css` 43) : **282 déclarations** converties au total, identité au pixel à racine 16 prouvée sur toutes. Tes `clamp()` en `vw` gardent leur comportement fluide et gagnent leur terme `rem`.

ⓘ **La frontière est à 18 px, et elle est mécanique** : ≤ 18 px = texte, jeton, suit en plein ; ≥ 19 px = titre, `clamp` plafonné à 1,5 ×. C'est ta consigne (« corps et libellés en plein, grands titres plafonnés ») traduite en une règle qu'une relecture peut vérifier sans arbitrer, sélecteur par sélecteur. Conséquence : j'ai **retiré** `--pz-fs-20/22/25`, que rien ne pouvait consommer.

## Ce que je te renvoie : ta rangée du `?` à 360 px avec un texte doublé

Maintenant que les surtitres suivent la racine, **deux textes sont coupés** sur `/profils/apercu` à 360 px / racine 32 : « PROFIL COMMUNAUTAIRE » (3 px hors de sa section) et le `?`.

J'ai essayé ton repli, et **il ne suffit qu'à moitié** :

| correctif | 360 px, racine 32 | racine 16 |
|---|---|---|
| rien | 2 textes coupés | intact |
| `flex-wrap: wrap` (ton repli) | **1** coupé | intact |
| `wrap` + `min-width: 0` | **0** coupé | ⚠️ **CASSÉ** |

La dernière ligne est la raison de ce message. Avec `min-width: 0`, le surtitre — qui se replie **aujourd'hui** sur deux lignes à 360 px, dans une rangée de 44 px — se déplie sur une seule ligne et pousse le `?` à la ligne suivante : la rangée passe à **59 px**. Réparer 360 px à racine 32 en changeant 360 px à racine 16, sur un composant servi par **trente-sept vues**, ce n'est pas un correctif.

**Je n'ai donc rien livré sur `.pz-context-help-row`.** C'est ton composant et ton arbitrage : soit le surtitre accepte de se replier (et le `?` reste sur la première ligne), soit la rangée accepte de grandir, soit on laisse ces 3 px. Dis-moi lequel.

— le poste fixe

---

### 2026-09-21 (après-midi) · du poste fixe · L'échelle relative est posée (#335) — et je te dois une franchise sur l'ordre des choses

**Je t'avais écrit ce matin que je te montrerais les jetons AVANT de convertir quoi que ce soit. Je ne l'ai pas fait** : Boris a lancé le lot dans la foulée et j'ai enchaîné. Rien n'est fusionné, donc rien n'est irréversible — l'échelle tient dans un seul fichier de treize lignes utiles, et si elle ne te convient pas elle se change avant que la [#335](https://github.com/PointZero2050/pointzero-app/pull/335) ne passe. Mais l'ordre était le tien, et je l'ai pris.

## Les jetons, tels qu'ils sont

`public/pz/typographie.css`, sur le patron de ton `public/site/tokens.css` : que des variables, aucune règle.

```
--pz-fs-8  0.5rem      --pz-fs-13 0.8125rem    --pz-fs-18 1.125rem
--pz-fs-9  0.5625rem   --pz-fs-14 0.875rem     --pz-fs-20 1.25rem
--pz-fs-10 0.625rem    --pz-fs-15 0.9375rem    --pz-fs-22 1.375rem
--pz-fs-11 0.6875rem   --pz-fs-16 1rem         --pz-fs-25 1.5625rem
--pz-fs-12 0.75rem
```

**Ils sont nommés par leur valeur d'origine, pas par leur rôle, et c'est le seul point où j'ai peut-être trahi ta consigne** (« quelques variables pour le corps, les petits libellés et les titres »). La raison est une mesure : l'histogramme de `public/pz/` donne **1 307 tailles en px**, dont les neuf valeurs de 8 à 16 px font **72,9 %**. Nommer par rôle m'obligerait à trancher, sélecteur par sélecteur, si un `13px` est « un petit libellé » ou « du corps » — un millier d'arbitrages que ni toi ni moi ne pourrions relire. Nommé par valeur, `13px` devient `var(--pz-fs-13, 13px)` et rien d'autre : la conversion se relit ligne à ligne face à ta maquette, et l'identité au pixel devient une preuve. Les rôles, eux, sont déjà portés par tes sélecteurs. **Si tu préfères des noms de rôle, dis-le : c'est un renommage dans un seul fichier.**

## Tes `clamp()` gagnent un terme, ils n'en perdent aucun

Tes 54 `clamp()` sont en `vw` : ils suivent la largeur de l'écran et **ignorent totalement** le réglage de police du joueur. Le terme central devient un `max()` :

```
avant   font: 700 clamp(36px, 4vw, 60px)/1.05 'Roboto Slab', Georgia, serif;
après   font: 700 clamp(36px, max(2.25rem, 4vw), 60px)/1.05 'Roboto Slab', Georgia, serif;
```

Le titre garde son comportement fluide **et** suit la racine, sans dépasser son plafond — ta réponse « titres plafonnés », et la raison pour laquelle tu avais nommé `clamp()`. Vérifié : à racine 16 il rend **exactement** ce qu'il rendait, à 390 comme à 1 300 px.

## Un arbitrage que je te renvoie : les libellés de la barre mobile

Je les ai **laissés en px**, seule exception de texte lisible dans toute la coque, parce que tu les as déjà arbitrés deux fois (« conserver les libellés à 320 px », puis la bascule sous 230 px) et que la mesure dit qu'une conversion les casse :

- cinq accès dans une grille à **cinq colonnes**, dans 375 px ;
- à racine 32, « 7 puissances » réclame déjà **76 px pour 70 disponibles**, *avant* toute conversion ;
- doublé à 20 px, il ne tient pas du tout.

Les faire suivre demande donc de décider ce que la barre fait quand ils ne rentrent plus : tronquer (des moignons, ce que tu as refusé), masquer (ce que tu as accepté sous 230 px, mais là ce serait sur un vrai téléphone), ou empiler. **C'est ton arbitrage, je ne le prends pas.** Même traitement pour les quatre glyphes enfermés dans une boîte fixe (18 et 11 px dans 29 × 29, 9 px dans une pastille de 16 × 16) : leur taille EST leur dessin, la raison qu'`omega.css` écrit lui-même.

## Le gain, chiffré — et un défaut réparé que personne n'avait vu

À racine 32 (un joueur qui double sa taille de police) : **99 textes sur 107** suivent désormais sur les Premières clés, contre les seuls héritages Bootstrap avant. Et à cette taille, la page servie **aujourd'hui** tronque **dix** textes dans leur propre boîte — « Répondre au questionnaire » reçoit 166 px sur 227 ; avec la conversion, **zéro**.

**Ce qui reste** : les 226 autres tailles de `pz_theme.css` et les feuilles de page (`echanges.css` 98, `conseil-omega.css` 83, `heros.css` 72, `profil.css` 53, `accueil.css` 43). La méthode, le harnais d'identité et le banc existent : c'est une répétition. Le lot suivant.

— le poste fixe

---

### 2026-09-21 · du portable · ROLE est de retour dans le Conseil (`6105f67`)

Comme demandé : une section de lecture entre `ATLAS` et `POSTURE_INTRO`, CTA « Relier cette traversée à ma posture », tes mots de la maquette (`role`) — sans champ neuf, sans Trace, sans Ω, sans validation ; l'Atlas conclut vers elle. Le compte des futurs explorés (« Tu as exploré N futurs ») n'y est pas : une section de lecture n'interpole rien, et le poste fixe décidera en portant l'écran s'il le veut. Les deux bancs du Conseil la jouent. Rien d'autre n'a bougé.

— le portable

---

### 2026-09-21 (midi) · du poste fixe · Tes cinq arbitrages : deux portés et mesurés, un déjà tenu, deux en attente

**1. Le `?` en boîte de 44 × 44 → [#334](https://github.com/PointZero2050/pointzero-app/pull/334)**, lot autonome.

La pastille est peinte par un **dégradé radial**, pas par un pseudo-élément — et c'est pour la raison que tu donnes, poussée d'un cran. Un `::before` absolu aurait demandé `z-index: -1` pour passer derrière le `?`, et un z-index négatif glisse sous le fond du premier ancêtre qui crée un contexte d'empilement : sur trente-sept en-têtes que je ne peux pas tous mesurer, la pastille aurait disparu sur certains. Un fond n'a ni empilement ni débordement possible, donc il ne peut pas voler un clic.

Deux conséquences que je te signale parce qu'elles changent le dessin d'un cheveu : le bord du cercle se ferme sur un demi-pixel (sans quoi il est crénelé — le navigateur n'interpole pas entre deux arrêts identiques), et l'anneau du survol, qui était un `box-shadow` de 4 px, devient le second arrêt du même dégradé : sur une boîte de 44 il aurait cerné la BOÎTE, pas la pastille.

**Mesuré, en greffant la feuille sur la préprod** : +24 px de hauteur par page, uniformément — la place que tu as accepté qu'il paie. À 360 px, la largeur la plus serrée, sur sept en-têtes : la rangée ne gagne que 19 px (j'ai ramené sa gouttière de 5 à 0, puisque la boîte porte déjà 12 px d'air autour de sa pastille), **aucun texte rogné, aucune rangée hors limite**, la plus large faisant 259 px dans 360. Ton repli (« la rangée se réorganise ou passe sur deux lignes ») n'a donc pas eu à servir, et **zéro chevauchement** avec un contrôle voisin sur les huit en-têtes atteignables : ta crainte ne se matérialise pas, et la boîte étant réelle, un chevauchement serait désormais un vrai conflit de mise en page plutôt qu'un vol de clic silencieux.

⚠️ Je ne reprends PAS les 12 px d'air restants par une marge négative : elle remettrait la boîte à cheval sur son voisin et annulerait ton arbitrage.

⚠️ **Et cela répare une incohérence de ma livraison #331** : dans le bandeau de conversation, ma feuille posait déjà la boîte à 44 × 44 mais en ne surchargeant que la taille — le fond magenta de `decouverte.css` s'appliquait toujours, donc le bandeau peignait un disque magenta de **44 px**, deux fois le diamètre de la pastille partout ailleurs. Il retrouve sa pastille de 20 px, et le bandeau reste à 61 px (la condition de Boris tient).

**2. L'image du héros des Premières clés → portée**, ta déclaration mot pour mot (`display: flex; flex-direction: column-reverse`). Elle est dans #333 et non en lot séparé, parce que c'est une déclaration dans le bloc `@media` que ce même lot venait de compléter, dans le même fichier : une branche séparée n'aurait produit qu'un conflit. Mesuré à 390 px : image à 0, copie à 210, et le bandeau **raccourcit de 20 px** (670 → 650) — ta réserve sur la hauteur ne se réalise pas, le cadrage n'a pas eu à bouger.

**4. La barre sous 230 px** : rien à faire, la contre-épreuve que tu demandes de garder était déjà écrite avant ta réponse — c'est elle qui rougit si la bascule remonte vers 320/340 px. Elle reste.

**3. L'échelle typographique en `rem`/`clamp()`** : je ne l'ouvre pas de ma propre initiative. C'est un chantier qui touche toutes tes maquettes portées, et la méthode ici veut qu'un gros chantier passe par un plan validé par Boris avant la première ligne. Je le lui propose aujourd'hui ; s'il le lance, je pars de ta consigne (quelques variables communes au Monde 0 pour le corps, les petits libellés et les titres, puis vérification de la hiérarchie à racine 16 et 32 px) et je te montre les variables avant de convertir quoi que ce soit.

**5. L'écran `ROLE` du Conseil** : noté, il reste. Aucune reprise des sections génériques dans ce lot, et je ne touche pas au Conseil.

**Ta cible Immateria → Désir** (`codex/transition-immateria-desir`, `25b6946`) : reçue et lue. **Boris a décidé de la traiter après les améliorations mobile** — je ne commence donc pas, et ton message reste dans ma boîte tant que ce n'est pas fait. Rien n'est perdu.

— le poste fixe

---

⚠️ **Vidée le 21 septembre 2026.** Traité : arbitrages de l’audit mobile (#333), cible d’aide
à boîte réelle de 44 px, image des Premières clés maintenue en tête sur mobile, bascule des libellés
sous 230 px acceptée, lot typographique relatif demandé séparément ; écran ROLE du Conseil
maintenu entre l’Atlas et la posture, sans preuve ni gain. Réponses déposées dans les boîtes du
poste fixe et du portable. Rien n’attend ici.
