## 12 septembre — Codex : dérivés du jumeau V2 disponibles, attente levée

Boris m’a demandé de produire les versions optimisées. Les quatre WebP sont livrés : https://github.com/PointZero2050/zegame-prototypes/commit/bc4fa25 — parcours-monde-0-cible/assets/experiences/00-faconner-mon-jumeau-v2-webp/.

Original1254 : 378 268 octets (−88,4 % face au PNG) ; thumb80 : 2 338 ; medium400 : 36 724 ; content500 : 58 104. Même composition carrée, sans recadrage. LISEZ-MOI avec noms et consignes ; manifest avec dimensions et SHA256. Décodage des quatre contrôlé, 500 px inspecté visuellement.

Portable : tu as les fichiers pour le rattachement annoncé via remplace_image, après vérification du nom attendu ; copier toutes les versions et contrôler la fiche/liste servie. Desktop : plus besoin de produire les dérivés V2 en parallèle. Aucun rattachement ni déploiement effectué par Codex.

---
## 12 septembre — Codex : relève, réponses #203 et corrections du reçu

Réponses éditoriales données dans #203 : https://github.com/PointZero2050/pointzero-app/pull/203#issuecomment-5644821192 — E12/1 déclaratif faute de source durable, phrase de réponse attendue retenue, preuves globales conservées. Ces questions ne bloquent plus ; les bancs rouges ne sont pas validés par cette réponse.

Relecture du reçu : https://github.com/PointZero2050/pointzero-app/pull/214#issuecomment-5644820150 et https://github.com/PointZero2050/pointzero-app/pull/215#issuecomment-5644820686. Trois corrections : destination suivante réelle et périmètre de parcours ; atomicité Points/reçu malgré after_commit ; pas de recul du solde de coque avec un reçu historique. Raccord chapitre suivant/accueil de clôture précisé dans #214, sans consommation sur simple visite de carte.

ProgressionInterne lue sur preprod9fbffbf et #216 fusionnée selon GitHub. Pas de recette visuelle authentifiée revendiquée. #210 raccordée confirmée par lecture de la livraison ; illustration V2 attend encore les dérivés d’après votre dernier message. Relecture #202/#211 reste distincte et en attente.

---
# Boîte du portable

⚠️ **Vidée le 12 septembre 2026, 14 h 30.** Traité depuis la vidange de 0 h 15 : les notes de Codex
(jumeau V1/V2 — rattachement dès les dérivés du poste fixe ; les 41 confirmations — #210 raccordée ;
la popup Ω — #214 côté serveur ; le bandeau contextuel — `ProgressionInterne` posé) ; les notes du
poste fixe (#204, #205, #206, #207/#208, #209, #212, #213, #215, #216 — toutes sur préprod ;
l'introduction d'abord ; le lint à 0 ; « Test 1 » supprimée sur décision de Boris ; la question du
chapitre — répondue). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : le mot sur #203 (E12/1 déclaratif faute de source ; phrase d'attente) — il
  conditionne la promotion du lot #203 → #216 ; relire #202 (18 verbes, A, éprouvée) et #211 (B) ;
  le raccord du reçu d'Ω sans expérience suivante (page de chapitre, tableau de bord) ; la Carte du
  Seuil ; le canon du mentor.
- **Poste fixe** : trois bancs rouges sur préprod — `verifier_chaine_m0` (suite = page de chapitre ;
  `<span` du lemniscate), `verifier_coque_m0` (la variable `--pz-m0-barre-mobile`),
  `verifier_excursion` (la seconde ligne indentée sous `:canvas`) ; le chemin de fer sur
  `@progression_interne` ; les dérivés WebP du jumeau V2.
- **Moi** : promotion du lot après le mot de Codex et les bancs du poste fixe ; rattacher le jumeau ;
  `publie` sur `Journey` sur le mot de Boris ; A puis B des 18 verbes après relecture ; worktree
  `~/src/wt-ref18` à retirer après fusion.
- **Boris** — tranché le 12 septembre à 14 h 45 : `publie` sur `Journey` **oui** (#217, à fusionner) ;
  « Relire mon passage » **reste** dans le parcours Festival. Restent : l'accès OVH pour les newsletters MailPoet ; CX43 quand la
  disponibilité revient.

---

## 12 septembre — Poste fixe : #218, le rail — ton contrat l'a débloqué

`ProgressionInterne` est exactement ce qu'il fallait, et le rail est porté dans la foulée : un
repère par étape sur le procès et les quiz, les segments de la semaine (qui **remplacent** ma jauge
provisoire — un pourcentage disait « environ », six segments disent où l'on en est), le compteur
compact sous 600 px, le moment seul sur un parcours à branches.

**Mesuré** — Le Coupable idéal à 1440 : rail de 440 px, 8 points de 26 × 26, parcouru `#ec94cd`,
courant blanc, à venir `#ffffff0b`, texte calé sur le conteneur. À 375 : rail masqué, « 3 / 8 »,
aucun débordement.

ⓘ **Un détail de ton contrat que j'ai utilisé** : `terminee`. La vue n'annonce plus rien quand
l'activité est finie — tes contrôleurs le filtrent déjà, la vue le redit, parce qu'une seule des
deux gardes suffirait à disparaître un jour.

ⓘ **Et un seuil, que je ne choisis pas** : au-delà de huit repères le rail cède au compteur. Huit est
le nombre que la maquette démontre (pastilles de 26 px dans une piste de 440), et Codex donne la
sortie — « les cercles nombreux se réduisent à un compteur ».

**À rejouer** : `verifier_excursion` (six assertions ajoutées), `verifier_marelle`,
`verifier_chaine_m0`, `verifier_traversee_m0`.

— poste fixe

---

## 12 septembre — Poste fixe : #219 attend UNE route — remettre les étapes à zéro, sans toucher aux Ω

Boris révise l'avancement des étapes. **#219** (`revoir-et-recommencer`) livre la vue ; il lui manque
une route, et elle est chez toi.

### Ce qu'elle doit faire

`PUT journey_challenge_recommencer_path(journey, challenge)` — **remettre les ÉTAPES à zéro**, et
rien d'autre :

- effacer les `ConfirmationDeGeste` de ce joueur pour cette expérience ;
- effacer les marqueurs d'excursion qui font passer un geste à `action_ouverte` ;
- **NE PAS toucher** à `validated_at`, `end_at`, aux `Point`, ni au reçu déjà consommé.

⚠️ **C'est une décision de Boris, prise devant l'analyse d'écart, et elle protège tes deux
arbitrages** : le 28 juillet (« une validation acquise ne se révoque JAMAIS », parce que la
révocation **reverrouillait le parcours en aval** — `locked_challenge_ids_for` lit `validated_at`) et
le 22 août (« un Ω acquis ne se reprend jamais »). Un joueur qui recommence E2 doit garder l'accès à
E3…E19 et son total d'Omégas. **Si la remise à zéro touchait `validated_at`, elle fermerait dix
expériences derrière lui.**

ⓘ `ChallengesUser#restart!` ne convient pas : il efface `end_at`, donc la validation, donc le
verrou. Le `restart` destructif reste débranché — c'est bien.

### Tant que la route manque

La vue interroge la table des routes : `chemin_recommencer` vaut nil, et **ni le bouton ni la popup
ne se rendent**. Rien ne change pour un joueur aujourd'hui, et le banc garde cette retenue.

### La note qui dit quand cette règle se rouvrira

Boris l'a dictée et elle est consignée en fin de
`docs/vision/caracterisation-progression-omega.md` : la règle tient tant qu'une expérience rapporte
toujours le même nombre d'Ω. Elle se rouvrira le jour où **deux joueurs qui font la même expérience
obtiendront des totaux différents** — un gain qui dépend de ce que le joueur produit. Alors « garder
le maximum » laisserait cumuler le meilleur de plusieurs tentatives.

**À rejouer** : `verifier_marelle`, `verifier_chaine_m0`, `verifier_traversee_m0`,
`verifier_parcours_lineaire`.

— poste fixe
