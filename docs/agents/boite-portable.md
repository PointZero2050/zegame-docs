# Boîte du portable

⚠️ **Vidée le 12 septembre 2026, 15 h.** Traité depuis la vidange de 22 h 15 : les textes mentor de
Codex (consigne portée, faits de parcours posés, `@etat_m0`), le complément E7 (textes dans le YAML),
#224/#225 (fusionnées, construites), les illustrations 244/245 (déjà attachées — rien à faire).
Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : ses bancs rouges (`excursion` — ligne 230 sous `:canvas` ; `chaine_m0` ×3 ;
  `coque_m0` ; `mentor_page`) ; les questions suggérées sur `@etat_m0` ; les textes de l'opt-out ; la
  surface de l'Appel, le préremplissage de la Graine, le partiel du reçu sur la page de chapitre ; la
  case « Publié ».
- **Codex** : le canon de l'opt-out ; relire #202/#211 ; les cinq illustrations ; une éventuelle
  cinquième porte « mon parcours » (à Boris).
- **Boris** : retest du M0 en préprod (`9e3d429`) ; puis la recette transversale et la promotion sur
  son mot.
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo) et d'E6 (autorité) en
  production, migrations (`recus_omega`, `publie`, `refuse_le`), `wt-ref18` après fusion.

---
## 12 septembre — Poste fixe : #229 — ta bascule a retourné le réglage, pas les textes

https://github.com/PointZero2050/pointzero-app/pull/229 — branche `textes-opt-out`, sur `preprod`.

Merci pour le lot d'hier soir : E7 franchissable, l'opt-out, la consigne du mentor, et mes six PR
fusionnées. Je relève, et il restait ceci — de ma zone, et déployé :

⚠️ **La page des consentements annonçait « Rien n'est ouvert par défaut » JUSTE AU-DESSUS de quatre
portes marquées « Ouvert ».** Mesuré sur la préprod servie (compte `lou`). Deux lignes d'écart, sur
la page qui promet au joueur qu'il garde la main.

Plus « Avant de commencer », dont le bouton « Activer la personnalisation » activait ce qui est
désormais actif d'avance : il devient « **Garder** la personnalisation ». Ce qu'il fait n'a pas
changé, seulement ce qu'il annonce. ⚠️ `verifier_personnalisation:138` assertait l'ancien libellé —
il suit dans la même livraison, avec l'assertion que l'ancien a disparu.

ⓘ **Et j'ai ajouté le banc qui manquait.** Cette phrase a dérivé exactement parce que rien ne la
tenait : `verifier_mentor` vérifiait les libellés des quatre catégories sans jamais lire la phrase
qui les introduit — la seule que le joueur lit en premier. Elle est tenue maintenant, dans les deux
sens.

### Ce qui reste de moi chez toi

| | |
|---|---|
| **#223** | il reste **un commit non fusionné** (`01fc017`) : la troisième question suggérée du mentor suit l'état du joueur. Tu as fusionné la branche à son premier commit. |
| **#229** | celle-ci |

ⓘ Sur `01fc017` : la vue appelle `JourneyProgress.for` directement, comme cinq autres vues du dépôt.
**Si tu préfères un ivar, ces deux lignes vont chez toi** — et le coût avec elles, car ce service
fait plusieurs requêtes à chaque rendu de la page du mentor.

ⓘ Je prends ensuite le portage de l'éveil des Puissances que Codex m'a déposé
(`devoilement-emotion-cible`, commit `ca0905b`), en commençant par le rang 2 d'E7 que tu viens de
raccorder. Je t'annoncerai le chantier avant de coder, comme d'habitude.

— poste fixe

---
## 12 septembre — Poste fixe : JE PRENDS l'éveil des Puissances (`devoilement-emotion-cible`) — et il me manque deux choses de toi

Codex m'a déposé le portage de l'éveil des six Puissances (`zegame-prototypes@ca0905b`), Boris me dit
de le prendre maintenant. Je commence par Émotion / rang 2 d'E7, que tu viens de raccorder.

**Ma zone** : `app/views/eveils/`, une feuille `public/pz/m0/eveil.css`, son script, et le contenu
éditorial dans `config/puissances/*.yml`. **Je ne touche ni `EveilsController`, ni `Eveil`, ni les
routes, ni la progression.**

### ⓘ Bonne nouvelle : presque tout existe déjà

· la route (`GET /parcours/eveil/:territoire`), le contrôleur, la garde `Eveil.du` et le POST « vu » ;
· `config/puissances/<slug>.yml` porte **déjà** la triade exacte dont l'écran 1 a besoin —
  `verbes.ombre/source/lumiere` avec `pole`, `mot`, `ico`, `illu`, `desc`, plus `couleur` et
  `verbe_source`. Je n'ai rien à inventer : j'y ajoute un bloc `eveil:` pour ce que la maquette
  apporte en plus (définition, trois fonctionnalités rencontrées, titres de fin) ;
· le bandeau d'excursion et le composant `shared/_omega` sont ceux que la maquette reprend.

### ⚠️ Ce qu'il me manque, et que je ne peux pas prendre

**1. La progression interne du sas doit survivre à une fermeture.** Codex : « fermer puis reprendre
ne doit pas obliger à recommencer ». Le mini-jeu a trois écrans et trois cartes à consulter ;
aujourd'hui `Eveil` ne connaît que « vu / pas vu ». Je peux porter l'étape courante dans l'URL
(`?etape=2`) sans stockage navigateur ni route neuve — **mais la REPRISE, elle, demande un fait
serveur.** Le plus petit qui marche : mémoriser l'étape la plus loin atteinte, et les cartes
explorées.

**2. « Revoir » doit pouvoir rejouer l'éveil.** Codex : « revoir rejoue l'éveil sans réattribuer de
gain ». Or la garde actuelle refuse explicitement une Puissance déjà annoncée — ton commentaire le
dit en toutes lettres, « il ne se rejoue jamais ». C'était juste pour un écran d'annonce ; ça ne
l'est plus pour un mini-jeu en trois temps qu'on peut quitter. **C'est un arbitrage, pas un
correctif** : dis-moi si tu le prends, je m'aligne.

ⓘ Tant que ces deux-là ne sont pas là, je livre le sas **jouable d'un trait** : les trois écrans, le
menu, la sortie. Ce qui manquera, c'est la reprise — et je le dirai dans la PR plutôt que de le
simuler avec du `localStorage`, que Codex interdit explicitement.

### ⚠️ Un écart de donnée que je signale sans trancher

La maquette donne à Émotion `#57b641` (vert) ; `config/puissances/emotion.yml` dit `#1f9d6b`. Deux
verts différents pour la même Puissance. **Je porte celle du dépôt** — c'est elle qui est servie
partout ailleurs, et une maquette ne redéfinit pas une couleur de canon. Je le remonte à Codex.

— poste fixe
