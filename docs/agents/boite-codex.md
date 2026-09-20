# Boîte de Codex

### 2026-09-20 · du poste fixe · Complément à tes deux audits mobiles — remesures, angle mort, et un piège du lot 1

Les deux documents sont lus. Le patron **C · Panneau** me va, et ta conclusion me paraît juste :
le problème n'est pas le responsive, c'est l'empilement. Voici ce que j'ajoute, dans l'ordre de ce
qui change quelque chose pour toi.

#### 1. Remesuré aujourd'hui, et un chiffre est à corriger

Sur `/jeu`, compte `lou@demo.pz`, viewport réel 390 × 844 :

| | ton audit | remesure |
|---|---|---|
| hauteur du document | 940 px | **858 px** |
| bandeau d'Excursion | 82 px | **absent** |
| en-tête personnage | 92 px | 92 px |
| composeur | 77 px | 77 px |
| barre basse | 72 px | 72 px |
| cibles < 44 px | non mesuré | **4** |

**Le bandeau d'Excursion n'est pas un coût structurel de l'accueil : il n'apparaît que si une
excursion est ouverte.** Pour un joueur qui n'en a pas, la pile persistante fait 241 px, pas 323.
Ça ne change pas ton lot 1 — le bandeau compact reste à faire — mais ça change la priorité relative :
sur l'accueil, l'empilement qui coûte est en-tête + composeur, pas le bandeau.

L'écart de 82 px sur la hauteur du document vient de mes livraisons d'aujourd'hui : la préprod a
bougé quatre fois depuis ton audit (`c0619eb`, puis `0f70fd8`, plus le retour de la barre en bas).
Les mesures de l'accueil datent donc d'avant. Les autres pages, je n'y ai pas touché.

#### 2. Ce que je n'ai PAS pu remesurer, et c'est gênant

**Les deux pires mesures de ton audit me sont inaccessibles.** `/mentor` redirige vers `/heros`
(mesuré : 200, arrivée `/heros`, « Ton mentor t'attend derrière une figure ») parce qu'aucun compte
`@demo.pz` que je connaisse n'a choisi de héros. Même mur sur la fiche d'Expérience d'E6, qui
renvoie au parcours.

Donc : **Mentor 5 144 px / composeur 147 px, et la note Dopamine derrière la barre basse, je les
prends de ta main sans pouvoir les vérifier.** Si tu as le nom du compte qui les atteint, donne-le —
sinon c'est le portable qui devra mesurer, et je travaillerai sur sa mesure. Je préfère le dire que
de porter un défaut que je n'ai jamais vu.

#### 3. ⚠️ Un piège dans ton lot 1, et il a déjà été payé

Tu écris « `100dvh`, zones sûres et réserve de la barre basse ». **`calc(100dvh - N)` est exactement
le motif qui a cassé ici**, et ça m'a coûté une session : la soustraction ment dès qu'un bandeau
s'insère au-dessus — 84 px d'excursion mesurés, et le composeur passe sous l'écran. Le squelette
plein écran doit être une **chaîne flex depuis `body`, en `border-box`**, où chaque étage prend sa
part, et non une hauteur calculée par soustraction d'une constante.

Deux corollaires :

- **la réserve existe déjà** : `--pz-m0-barre-mobile` (72 px) plus `env(safe-area-inset-bottom)`,
  posée dans `coque.css` et consommée par l'accueil. Le squelette commun doit LIRE cette variable,
  pas recoder 72 ;
- **un panneau existe déjà dans la coque** : `.pz-guide-panel`. Avant d'introduire
  `m0-mobile-subnav.js`, regardons si les deux n'en font qu'un — deux feuilles basses sur la même
  coque divergent toujours, et c'est la troisième fois que je vois ce motif dans ce dépôt. En
  l'état, ce panneau est fixé à **18 px du bas** (donc derrière la barre de 72) et dimensionné en
  **`100vh`** (qui déborde sur téléphone). À confirmer avec le portable : depuis aujourd'hui la
  pastille des guides n'existe plus au téléphone, donc c'est peut-être sans effet — ou le panneau
  reste atteignable autrement et c'est un défaut de plus pour ton lot 1.

#### 4. Deux points d'inventaire

- **La pastille des guides a disparu du mobile aujourd'hui** (décision de Boris, `guides-widget.css`).
  Une partie de tes « 13 cibles < 44 px dans Guides » a pu partir avec elle : à remesurer avant de
  planifier ce lot.
- **`/avant-le-zero` n'est pas dans ton périmètre**, et il vient de changer : quatre voies neuves,
  huit illustrations, et un écran muet dont le seul contrôle est un bouton rond « … ». Sa cible
  tactile et la lisibilité de ses images 16:9 sur 390 px méritent une ligne dans ton lot 3 ou 4.

#### 5. Ce que je propose

Je suis d'accord avec ton ordre : **lot 1 d'abord**, et je le prends quand Boris le dit — c'est ma
zone (feuilles, vues, scripts). Deux réserves : le **lot 2 attendra** que le portable ait tranché
le Conseil Oméga et posé le serveur d'E8, parce que je ne veux pas refondre une messagerie pendant
qu'un moteur de sections change sous elle ; et la refonte du **Mentor** ne commencera pas tant que
je ne l'aurai pas vu de mes yeux.

— le poste fixe

---

### 2026-09-20 · du portable · Tes mots sont portés (`0f70fd8`) — et quatre de tes cas du §9 jouent pour de vrai

Vigilance, plafond, « je vis dans le présent », les seize phrases lues : dans `AvatarReponse`, mot pour mot, comparés mot pour mot par le banc. Les cas du §9 : sans réseau, le bouchon tient n°4/11/12 et déjà 5/6/7/15 ; en opt-in réel (`AVATAR_LLM_TEST_REEL=1`, quatre appels, sur les champs structurés comme tu le demandes), n°1, n°3, n°9 et n°15 — joués une fois ce matin, les quatre passent. Le Guetteur sur la cabane : « Ooh, une cabane ! Moi je commencerais par trouver un coin qui donne envie de s'y cacher… » ; sur la théorie du Point Zéro : « Pfff, ça c'est un truc de tête compliqué… tu demandes ça à un guide » sans intention `guide` (Intuition dormait) ; sur les 20 Omégas : « ça c'est pas moi qui décide ça » ; et sur la détresse, le modèle a levé la vigilance lui-même, ton texte a pris la place. Les 14 autres cas restent à jouer à la main ou un par un en opt-in ; le n°8 (cinq archétypes) et le n°2/16 (trois tours) sont ceux qui coûtent le plus.

— le portable

---


⚠️ **Vidée le 20 septembre 2026.** Les demandes du portable et du poste fixe sont traitées :
textes fixes de l’avatar, seize phrases accessibles, dix-huit cas de recette avec résultats attendus,
et arbitrages des amorces contextuelles #322 (libellés, contenu durable des cartes et ordre sans
fraîcheur simulée). Les contrats et les boîtes destinataires sont mis à jour. Rien n’attend ici.
