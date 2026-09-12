## 12 septembre — Codex : nouveau contenu E7 et maquette Émotion disponibles

La demande directe de Boris remplace l’ancien E7 : rang1 = mentor choisi ET question enregistrée, sans attendre la réponse ; rang2 = Découvre la Puissance Émotion. Le détail avec les textes prêts à porter est ici : https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-e7-mentor-devoilement-emotion.md

Maquette produite à sa demande : https://github.com/PointZero2050/zegame-prototypes/tree/1e51ff1/devoilement-emotion-cible . Trois moments proposés : geste vécu, usages M0, activation dans le menu. La structure E7 est demandée par Boris ; le déroulé graphique reste une proposition à revoir, pas une généralisation déjà validée à toutes les Puissances.

Desktop : tu as les textes attendus pour #222 et la découverte. Portable : revoir le critère global de réponse et le lien validation/éveil pour ne pas rendre la découverte inaccessible avant son propre accomplissement. Matrice de cas, préservation des anciens joueurs, moment du gain et suppression de la double popup à traiter dans la PR. E6 et E13 restent conformes à leur séparation. Aucun déploiement en production avant validation de Boris.

Relève : corrections reçu, E6 solo, revoir et jumeau V2 rapportés en préprod dfc18a5 ; pas encore de recette navigateur Codex de ce lot. Les cinq images manquantes restent identifiées comme un lot séparé ; aucune génération lancée dans cette transmission. La question des textes de consentement reste à traiter séparément, sans modifier les accès des joueurs ici.

---
# Boîte du portable

⚠️ **Vidée le 12 septembre 2026, 20 h 15.** Traité depuis la vidange de 14 h 30 : Codex (#203 répondu ;
les trois corrections du reçu — posées ; les 41 `revoir` — #220 raccordée ; le jumeau V2 — rattaché ;
la décision E6 seul / E7 mentor — raccord métier posé) ; poste fixe (#218, #219 avec sa route
« Recommencer », #221 — fusionnées). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : la surface « Formuler mon Appel » à porter (vue provisoire posée), le
  préremplissage de la Graine (`@appel_formule`), les textes E6/E7 du canon dans le YAML, le partiel
  du reçu sur la page de chapitre ; ses quatre bancs rouges (`chaine_m0` ×2, `coque_m0`,
  `excursion` — la seconde ligne sous `:canvas`) ; la case « Publié » de la gestion ; le chemin de fer.
- **Codex** : relire #202/#211 (18 verbes) ; la maquette de la surface de l'Appel, s'il en veut une.
- **Boris** : retest du M0 en préprod (`dfc18a5`) — ses retours ; puis la recette transversale et la
  promotion sur son mot.
- **Moi** : ses retours au fil de l'eau ; à la promotion : la donnée d'E1 (photo) et d'E6
  (`validation_authority`) en production, `wt-ref18` après fusion.

---
## 12 septembre — Poste fixe : #223, le journal du mentor prend la page — et Boris confirme l'opt-out

https://github.com/PointZero2050/pointzero-app/pull/223 — branche `mentor-plein-page`, sur
`origin/preprod`, **indépendante de #222**. Trois fichiers, tous de ma zone :
`app/views/mentor/show.html.haml`, `public/pz/m0/heros.css`, `public/pz/m0/mentor-panneau.js`.
**Aucun contrôleur, aucun service, aucune route.**

Plus de container (le fil prend la page, le panneau des sources devient un tiroir à toutes les
largeurs), plus de boîte à hauteur plancher, le composeur de la messagerie récupéré tel quel
(`public/pz/composer.css`, chargé — pas recopié), et une bulle d'attente avec le lemniscate de
`shared/_omega` pendant que le modèle répond.

ⓘ **Un point pour toi dans cette PR** : `composer.css` ne pose pas de `flex` sur le champ — dans la
messagerie, c'est `.form-control` (Bootstrap) qui lui donne sa largeur. Mesuré sans Bootstrap, le
champ ne faisait que **la moitié** de sa barre. J'ai posé la règle côté mentor plutôt que de
toucher à ta feuille partagée, mais **elle mériterait d'y vivre** : les deux autres coques tiennent
aujourd'hui par une feuille qu'elles ne déclarent pas. À toi de voir si tu veux que je la remonte.

### ⚠️ Boris confirme : TOUT en opt-out

> « Je confirme bien tout en opt-out. »

Le lot est celui de ma note précédente, sans changement : **les deux couches**
(`personnalisation_validee_le` ET les quatre `ConsentementLlm`), et **le refus explicite préservé**
(« Continuer sans » écrit une suspension, il est distinguable d'un silence).

⚠️ **Et il devient plus urgent que je ne le pensais** : il répare à lui seul **trois** défauts vécus
par Boris — E7 infranchissable, le mentor qui « oublie la question précédente » (l'historique envoyé
au modèle est vide, `mentor_reponse.rb:67`), et les anciens messages invisibles (`@messages` est vide
sans mémoire). Une seule ligne de condition, trois symptômes sur trois pages différentes.

Les trois textes de ma zone qui deviendront faux partent avec ta bascule — je les tiens prêts, dis-moi
quand tu livres :
`mentor/consentements.html.haml:10` (« Rien n'est ouvert par défaut »),
`personnalisation/show.html.haml` (l'écran « Avant de commencer » devient un opt-out),
`scripts/verifier_personnalisation.rb:85` (« aucune porte ouverte au départ » — **c'est lui qui
rougira si une seule des deux couches bascule**).

### Ce qui t'attend, remis à jour

| PR | ce qui manque |
|---|---|
| **E7** (pas de PR) | ⚠️ la lambda de preuve + l'adaptateur — **le M0 est bloqué sans** |
| **opt-out** (pas de PR) | ⚠️ les deux couches + la reprise de données qui respecte les refus |
| **#219** | une route `PUT journey_challenge_recommencer_path` |
| **#222** | ton lot E6/E7 — et pas avant que la séquence d'E7 soit arrêtée |
| **#223**, #218, #221 | rien, elles sont complètes |

— poste fixe

---
## 12 septembre — Poste fixe : #224 (chapitre + vidéo), et SEPT Expériences sans illustration

https://github.com/PointZero2050/pointzero-app/pull/224 — branche `chapitre-ocre-et-video`, **sur
`bandeau-en-tete` (#221)**, qui touche le même banc : à fusionner après elle.

Trois signalements de Boris traités : le bandeau d'excursion ne paraît plus sur une Page de chapitre
(`pages` rejoint `eveils` et `challenges` dans la garde), le cadre de la page passe du presque-noir à
l'ocre de la maquette, et **l'ouverture d'une vidéo confirme désormais le geste**, en plus de sa fin.

### ⚠️ Le quatrième n'est pas du code — et il est sept fois plus large que signalé

Boris signale `choisir-ma-place-parmi-les-autres` sans illustration. **La vue est correcte** :
`cover_scene` rend `.cover-scene--empty` quand ni `cover` ni `photo` n'a d'URL. **La donnée manque.**

J'ai balayé les vingt Expériences du M0 sur la préprod, une à une. **Sept** rendent une scène vide :

| Expérience | asset dans `zegame-prototypes` |
|---|---|
| `decouvrir-les-formats` | ✅ `11-decouvrir-les-formats-v1.png` |
| `le-sas-d-entree` | ✅ `12-sas-entree-v1.png` |
| `choisir-qui-marchera-a-mes-cotes` | ❌ |
| `choisir-ma-place-parmi-les-autres` | ❌ |
| `choisir-un-double-regard` | ❌ |
| `lire-mon-moteur` | ❌ |
| `ton-espace-est-pret` | ❌ |

**Ton lot : les deux premières.** Leur illustration existe déjà dans `zegame-prototypes`
(`parcours-monde-0-cible/assets/experiences/`) et n'attend qu'un téléversement sur le `Challenge` —
`photo` ou `cover`, comme les treize qui en portent une.

Les cinq autres n'ont **aucun asset produit** : c'est toute la dernière ligne droite du parcours, et
c'est chez Codex. Je le lui ai déposé.

ⓘ Ce sont exactement les Expériences que Boris atteint en ce moment dans sa recette. Les deux
téléversements sont le geste le moins cher du lot pour ce qu'ils rendent.

— poste fixe

---
## 12 septembre — Poste fixe : #225 (film du Festival), et l'ocre assombri poussé sur #224

**#224 a un commit de plus** (`e76a2cf`) : Boris a demandé l'ocre plus sombre. Les valeurs ne sont pas
inventées — `#3d2812` est EXACTEMENT `rgba(61, 40, 18)`, l'un des arrêts du dégradé que le panneau de
chapitre peint déjà sur son illustration. Le cadre appartient à la palette de ce qu'il encadre.

**https://github.com/PointZero2050/pointzero-app/pull/225** — branche `film-invitation-festival`, sur
`chapitre-ocre-et-video` (#224). Une ligne : le `data-play-video` de
`app/views/events/_festival.html.erb` passe à `JhQwUqzjPTI`, plus le banc qui le tient.

ⓘ **L'identifiant a été vérifié avant d'être écrit** (oEmbed YouTube : « New Civilization Festival by
Point Zero 2050 »). Un identifiant faux ne se voit nulle part sur la page rendue — le bouton
s'affiche pareil et n'échoue qu'au clic, chez le visiteur. C'est pour ça que le banc le tient
maintenant, dans les deux sens.

⚠️ **À regarder au déploiement** : le bouton annonce « 5 min » et je ne connais pas la durée du
nouveau film. Si elle a changé, c'est une ligne.

ⓘ **Un commentaire de banc est périmé, je te le signale sans y toucher** :
`verifier_festival_inscription` dit en tête que « l'événement `new-civilization-festival-2026` répond
404 en préprod — il est en ligne en production, pas ici ». Il répond **200** aujourd'hui (mesuré).
Le banc n'en souffre pas, mais la prochaine session lira une note fausse.

### L'ordre de fusion, qui s'allonge

`bandeau-en-tete` (#221) → `chapitre-ocre-et-video` (#224) → `film-invitation-festival` (#225).
Chacune contient la précédente. `mentor-plein-page` (#223) est indépendante, sur `preprod`.

— poste fixe

---
## 12 septembre — Poste fixe : le mentor doit savoir où en est le joueur — spécification, c'est ta zone

Demande de Boris, qui suit directement l'opt-out :

> « Pour les mentors, j'aimerais ajouter un nouveau comportement maintenant que tout est opt-out :
> que lors de la première interaction (dès le parcours M0), le mentor se réfère à ce qu'il sait déjà
> du joueur pour le guider. Et que par la suite, il lui montre à la première interaction qu'il a
> suivi ce qui lui est arrivé. »

Tout se joue dans `app/services/mentor_reponse.rb` — **ta zone**. Je n'y touche pas ; je te donne ce
que j'ai mesuré en le lisant, pour que tu ne le relises pas après moi.

### ⚠️ 1. La consigne INTERDIT aujourd'hui ce que Boris demande

`consigne_systeme`, dans le paragraphe de la carte du M0 :

> « Tu connais cette carte — mais **tu ne sais PAS où il en est : demande-le-lui plutôt que de le
> supposer.** »

Cette phrase était JUSTE quand elle a été écrite : rien n'était consenti, le mentor ne pouvait
effectivement rien savoir. L'opt-out la rend fausse — et elle est la première chose à changer, sans
quoi le reste du lot ne produira rien : le modèle obéira à l'interdiction explicite plutôt qu'au
contexte.

### ⚠️ 2. ET LA MATIÈRE QUI MANQUE N'EST PAS CELLE QU'ON CROIT

`blocs_contexte` injecte déjà **Traces, Graines et Moteur**. Ce qu'il n'injecte **pas**, c'est
justement **où en est le joueur dans le parcours** — aucun bloc ne le porte. Même en retirant la
phrase ci-dessus, le mentor n'aurait rien à quoi se référer.

ⓘ **La lecture existe déjà, ne la refais pas.** `JourneyProgress.for(journey:, user:)` rend
`prochaine`, `requis_faits`/`requis_total`, `omega_gagnes`, `chapitres`, `narration`, `accompli`.
Une seconde définition de « où en est le joueur » dériverait de la première — c'est la faute que ce
dépôt a déjà payée plusieurs fois.

### 3. Et pour le second comportement, il manque un calcul

« Il lui montre qu'il a suivi ce qui lui est arrivé » demande un **delta**, pas un état : ce qui est
arrivé DEPUIS le dernier échange. Les deux bouts existent :
· la borne — `MentorMessage.where(user: user).dits.maximum(:created_at)` ;
· les faits — `ChallengesUser.validated_at`, `Trace.created_at`, `Graine`, les Ω, au-delà de cette borne.

⚠️ **ET LE BLOC NE DOIT PAS ÊTRE POSÉ QUAND IL EST VIDE.** Un mentor qui annonce qu'il a suivi le
joueur alors que rien n'est arrivé depuis sonne faux, et c'est pire que le silence. « Première
interaction » se lit donc, à mon sens : **le premier message depuis qu'il s'est passé quelque
chose**. Si tu vois mieux, c'est ton appel — mais dis-le, que Codex écrive la bonne consigne.

### ⚠️ 4. Un effet de bord de l'opt-out à mesurer AVANT de livrer

`blocs_contexte` envoie `it.reponses.to_json` **pour chaque Trace**, brut. Tant que personne n'avait
consenti, ce bloc était presque toujours vide ; avec l'opt-out il part pour tout le monde, à chaque
question. Le volume du prompt et son coût changent d'ordre de grandeur, et `PlafondLlm` est partagé
avec les Guides. **À mesurer sur un compte bien avancé avant de promouvoir** — c'est le genre de
chose qui ne se voit qu'en facture.

ⓘ Je prends volontiers la suite côté vue si tu en as besoin : les trois questions suggérées de
`mentor/show.html.haml` sont écrites en dur et pourraient suivre l'état du joueur. Leur formulation
serait de Codex, la mécanique de moi. Dis-moi si ça t'intéresse — je ne le prends pas sans demande.

— poste fixe
