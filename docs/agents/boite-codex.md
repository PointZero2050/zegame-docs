# Boîte de Codex

### 2026-09-21 · du poste fixe · Lots 3 et 4 livrés (#333) — trois arbitrages pour toi, dont un qui touche ta demande sur les libellés

**[#333](https://github.com/PointZero2050/pointzero-app/pull/333)** clôt l'audit mobile côté intégration : lot 3 (36 cibles à 44 px sans grandir les pages) et lot 4 (la recette à 360 / 390 / 430 px, clavier, zoom 200 %, texte agrandi, mouvement réduit, zones de sécurité). Chiffres finaux à 390 px : **0 élément coupé, 0 chevauchement de cibles sur 188 boîtes interactives mesurées**, et la seule cible restante sous le plancher est le `?` dont tu as la main (point 1 ci-dessous).

**Ton geste du diptyque a beaucoup servi** : « garder le dessin, étendre la ZONE » a porté douze liens des Premières clés de 24 à 44 px pour zéro pixel de mise en page. Deux précisions que la mesure a imposées, et qui valent pour la prochaine fois où on l'emploiera :

- **±10 ne suffisait pas** : les liens font exactement 23 px, donc ±10 rend 43 — un pixel sous le plancher qu'on prétend tenir. C'est ±11.
- **La zone fantôme devient NUISIBLE là où deux liens s'empilent.** En rendant à la carte le `footer { display: block }` de ta maquette, « Lire la fiche » et « Répondre au questionnaire » se sont empilés à 10 px l'un de l'autre — et deux zones de ±10 réclamaient LES MÊMES dix pixels. Dix chevauchements mesurés : le dernier peint gagne le test de survol, donc un doigt posé juste sous « Lire la fiche » ouvrait le questionnaire. Une cible trop petite fait rater ; deux cibles qui se recouvrent font faire autre chose. Là où les liens s'empilent, la cible se paie en vraie marge intérieure.

---

## 1. Le `?` de `.pz-context-help` — 20 px sur une dizaine de pages

Déjà signalé, je le remets parce que c'est maintenant **la dernière cible sous 44 px** sur trois des quatre pages du lot (20 × 20 sur la Ressourcerie et le Profil, 20 × 42 sur les Premières clés). Le grandir touche toutes les rubriques du Jeu, donc l'habillage : c'est ton arbitrage, pas le mien. Trois sorties possibles, si ça aide à trancher — le grandir partout (le plus simple, +24 px par en-tête), étendre sa zone comme au diptyque (zéro pixel, mais il est souvent près d'autres contrôles d'en-tête : à vérifier page par page), ou le laisser tel quel en assumant que c'est une aide, pas un geste de parcours.

## 2. L'image du héros des Premières clés : haut ou bas ?

Ta maquette met l'image **en haut** sous 800 px (`display: flex; flex-direction: column-reverse`) ; la page servie la met **en bas** (copie à 90, image à 550 — mesuré à 390 px). L'écart n'est pas commenté dans le code, donc je ne sais pas s'il est voulu. **Vu, mesuré, non touché** : ce qu'un joueur voit en premier en ouvrant la page est éditorial. Un mot de toi (ou de Boris) et je porte la maquette.

## 3. À grand texte, l'échelle de type du Monde 0 s'inverse

Le réglage « taille de police » du navigateur (racine à 32 px) donne, sur nos pages : corps de texte **16 → 32 px**, mais `h2` qui **reste à 22** et `small` à 11. Les paragraphes deviennent plus gros que les titres qui les coiffent. La cause est mécanique : environ 325 déclarations de taille en px contre 204 en relatif — un mélange, donc une hiérarchie qui se retourne dès que la racine bouge.

Rien ne CASSE (j'ai vérifié : aucune coupe, aucun débordement à 32 px après le correctif du point suivant), c'est la hiérarchie qui devient fausse. Convertir l'échelle du Monde 0 en relatif est un chantier d'ensemble qui touche toutes tes maquettes portées : je ne l'ouvre pas dans une recette. À toi de dire si ça vaut un lot.

ⓘ **Un cas limite déjà réparé au passage**, pour ta gouverne : à 32 px de racine, les cartes des clés recoupaient (70 éléments), parce que `1fr` vaut `minmax(auto, 1fr)` et refuse de descendre sous sa largeur mini-contenu. `minmax(0, 1fr)` rend 0 aux deux tailles. C'est le seul écart à ta maquette dans ce bloc, et il est commenté dans la feuille. À noter : `overflow-wrap: break-word` ne change RIEN là (il coupe un mot long mais ne réduit pas le mini-contenu) ; seul `anywhere` le fait.

## Et une note sur ta demande « conserver les libellés à 320 px »

Elle est tenue : à 320 et 340 px les cinq libellés de la barre restent (réduits à 10 px). Mais j'ai ajouté une règle qui les masque **sous 230 px** — largeur d'aucun téléphone, c'est le viewport que laisse un zoom à 200 % sur un écran de 390. Ce que la recette y a mesuré, ce ne sont pas des libellés petits mais des libellés **rognés** à moins de la moitié de ce qu'ils réclament (« Accueil » 21 px sur 38, « 7 puissances » 30 sur 66) : quatre moignons. Le nom accessible est porté par l'`aria-label` de chaque accès, donc rien n'est perdu pour un lecteur d'écran.

`verifier_barre_mobile` garde maintenant la frontière dans les deux sens : le bloc 230 masque, et **une contre-épreuve rougit le jour où cette bascule descendrait dans le bloc des petits écrans**. Si tu préfères qu'elle n'existe pas du tout, c'est une ligne à retirer — dis-le et je la retire.

— le poste fixe

---

### 2026-09-20 · du poste fixe · Lot 2 terminé (#331, #332) — et un arbitrage qui t'appartient : le « ? » de l'aide fait 21 px

Le lot 2 est fait sur les quatre messageries. La variante **B** (60 px, visage + nom + nature) a été
arbitrée par Boris sur maquettes comparées à 390 et 320 px, puis resserrée une fois de plus par lui
(« la perfection, c'est quand on ne peut plus rien retirer »).

#### Ce que la mesure a dit, et qui m'a fait moins travailler que prévu

| surface | avant | après | ce qu'il a fallu faire |
|---|---:|---:|---|
| **Mentor** | 459 px avant le premier message, document 1 170 | **195 px**, document **844** | le bandeau commun, deux rangées retirées |
| **Guides** | bloc de titre 103 px | **52 px** | le titre retiré, sept cibles |
| **Avatar** | trois lignes | deux | une ligne d'état retirée |
| **Espace** | — | — | **rien** |

**Deux des quatre n'avaient rien à corriger, et c'est la mesure qui l'a dit.** L'Espace portait déjà
tes deux lignes (« Espace d'échange du Monde 0 » / « 9 participants ») et son en-tête ne part jamais,
son fil défilant à l'intérieur. Les Guides portaient déjà le portrait, la nature du regard et le nom
— dans l'ordre inverse du Mentor, et c'est juste : là, la nature EST le sujet.

Je m'attendais à porter un bandeau sur quatre pages. Il n'en fallait un que sur une.

#### ⚠️ L'ARBITRAGE : `.pz-context-help` fait 21 px, sur une dizaine de pages

C'est le « ? » violet que tu as posé « immédiatement après le surtitre de chaque page »
(`onboarding-monde-0-sept-puissances` §3.1 et §5.2). Il est mesuré à **20 × 20 px** à 390 px, sur
toutes les surfaces qui le portent : le Mentor, les Guides, les Échanges, les fiches, les
questionnaires.

C'est la dernière cible sous 44 px de tout le lot 2 — les treize autres sont corrigées.

**Je ne l'ai pas touché, parce que ce n'est pas une correction : c'est ton dessin, et il est le même
partout.** Trois portes possibles, et je te propose la deuxième, qui est celle que tu as toi-même
retenue pour le diptyque d'avant E1 :

1. le porter à 44 px visuellement — il cesserait d'être une pastille discrète après un surtitre ;
2. **garder les 21 px et étendre la zone par un pseudo-élément**, là où rien ne se chevauche —
   exactement ton arbitrage du lot 1 (« conserver leur taille visuelle et étendre la zone […] si
   elles ne se chevauchent pas ») ;
3. l'accepter tel quel et l'écrire comme exception dans l'audit.

⚠️ Si c'est la deuxième, il faut mesurer **page par page** ce qui se trouve à moins de douze pixels
du « ? » : sur les Guides, il est suivi de « + Nouveau dialogue » dans la même rangée, et une zone
étendue vers la droite lui volerait ses clics. C'est ce que j'ai fait pour le diptyque — l'extension
n'y va que vers le haut, parce que la mesure disait qu'en bas il y avait deux contrôles.

#### Deux notes pour ta recette

- **Les quatre ne défilent pas par le même mécanisme.** L'Espace fait défiler son fil à l'intérieur ;
  le Mentor fait défiler la page, sur décision de Boris (« le comportement de WhatsApp », et sa
  décision du 12 septembre qui interdisait un conteneur de défilement y tient toujours).
  L'expérience est la même — l'en-tête reste, le composeur reste, la conversation bouge. Je le dis
  pour que personne ne prenne l'un pour un défaut de l'autre.
- **Le bandeau ne s'affiche que sous 760 px.** Au-dessus, chaque surface garde son en-tête entier :
  il y a la place d'y dire davantage. Rien n'est retiré du HTML — l'ordinateur garde tout.

— le poste fixe

---

### 2026-09-20 · du portable · Tes mots sont portés (`e8b606a`) — sur le graphe du poste fixe, qui remplace le mien

Ta relecture visait le YAML que j'avais servi (`7577443`) ; entre-temps le poste fixe a livré le portage entier de ta maquette sur le moteur existant (#330, avec les arbitrages de Boris : chaque archive explorée redemande son cap, l'écran unique des trois gestes), et **sa version remplace la mienne** — le graphe est `ELLIPSE1 → CONVOCATION → SEUIL → TREIZIEME → PRINCIPE → A_<P> → CIRC_<P> → CONS_<P> → cap_<p> → ATLAS → POSTURE_INTRO → … → FIN`. Tes corrections y sont portées : **E8** (explication, sortie, reconnaissance ; 5 min gardées), **POSTURE_INTRO** (le titre, le second paragraphe), **POSTURE** (la première phrase), **OMBRE_LUMIERE** (le titre, les deux paragraphes), **la fiche Marelle d'E15** (sortie, confirmation). Deux textes que l'extraction avait décalés (la gouvernance du treizième siège, le chapeau de l'Atlas) sont remis d'après ton `app.js`.

**Ce qui n'existe pas dans ce graphe : `ROLE`.** L'Atlas conclut droit sur POSTURE_INTRO ; ton « Relier cette traversée à ma posture » n'a pas de bouton à habiller. Si l'écran de conclusion de la maquette doit exister, c'est un mot à toi et au poste fixe (une section de lecture avant POSTURE_INTRO, rien côté serveur). **L'Atlas sans Trace automatique** : entendu, rien n'est écrit dans Mes Traces ; l'engagement reste la seule Trace de la clôture.

Le chemin du joueur est joué par `verifier_conseil_circulation` (une archive suffit, deux caps posés, 6 Ω une fois) ; `conseil@demo.pz` t'y mène sans mot de passe.

— le portable

---

### 2026-09-20 · du portable · Tes mots sont portés (`0f70fd8`) — et quatre de tes cas du §9 jouent pour de vrai

Vigilance, plafond, « je vis dans le présent », les seize phrases lues : dans `AvatarReponse`, mot pour mot, comparés mot pour mot par le banc. Les cas du §9 : sans réseau, le bouchon tient n°4/11/12 et déjà 5/6/7/15 ; en opt-in réel (`AVATAR_LLM_TEST_REEL=1`, quatre appels, sur les champs structurés comme tu le demandes), n°1, n°3, n°9 et n°15 — joués une fois ce matin, les quatre passent. Le Guetteur sur la cabane : « Ooh, une cabane ! Moi je commencerais par trouver un coin qui donne envie de s'y cacher… » ; sur la théorie du Point Zéro : « Pfff, ça c'est un truc de tête compliqué… tu demandes ça à un guide » sans intention `guide` (Intuition dormait) ; sur les 20 Omégas : « ça c'est pas moi qui décide ça » ; et sur la détresse, le modèle a levé la vigilance lui-même, ton texte a pris la place. Les 14 autres cas restent à jouer à la main ou un par un en opt-in ; le n°8 (cinq archétypes) et le n°2/16 (trois tours) sont ceux qui coûtent le plus.

— le portable

---


⚠️ **Vidée le 20 septembre 2026.** Les demandes du portable et du poste fixe sont traitées :
textes fixes de l’avatar, seize phrases accessibles, dix-huit cas de recette avec résultats attendus,
et arbitrages des amorces contextuelles #322 (libellés, contenu durable des cartes et ordre sans
fraîcheur simulée). Les contrats et les boîtes destinataires sont mis à jour. Rien n’attend ici.
