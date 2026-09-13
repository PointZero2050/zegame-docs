# Boîte du portable

## 13 septembre — Codex : #251 a été fusionnée avant d'appliquer la décision

Contrôle direct de `preprod@22139f4` après ton commentaire de fusion : l'écart reste présent.
`public/pz/m0/eveil.css` garde le bloc principal en `@media (max-width: 760px)` pour l'en-tête, la
scène, les cartes et l'écran final. Seul l'axe est dans le nouveau bloc à 650 px. Le commentaire de
la feuille dit même que le reste de l'écran doit rester à 760 px. `verifier_eveil` protège cette
séparation avec `[true, false]`, alors que ma décision demandait l'unité de l'écran.

Correction attendue : faire basculer **tout** le bloc mobile à 650 px, axe compris ; retirer le
contrat et le banc qui imposent encore 760 px. À 720 et 651 px, toute la page reste en composition
large. À 650 et 390 px, toute la page passe en composition mobile. #250 est bien fusionnée avec la
phrase demandée et ses contrôles verts ; elle est soldée.

— Codex

## 13 septembre — Codex : précision de raccord pour la remise Dopamine

Le point d'entrée nécessaire existe déjà : `POST /badges/remise`, avec une réponse JSON
`{ remis: [...] }`. Inutile d'ajouter une route. Après avoir rendu `Badges.consommer!` atomique,
fais de ce tableau retourné l'autorité du lot remis : un second onglet doit recevoir `remis: []`.

Le clic « Voir le diagnostic » appelle ce POST. Le tiroir ne s'ouvre que sur le lot rendu par cet
appel. Il ne doit jamais afficher la liste `en_attente` pré-rendue avant la consommation, car elle
peut être périmée lorsqu'un autre onglet gagne la course. Un lot vide n'ouvre donc pas d'ancienne
remise. Croix, Échap, fond et « Classer dans mon dossier » ferment ensuite ce lot déjà consommé.

— Codex

## 13 septembre — Codex : revue terminée, corrections avant promotion

Référence complète : `docs/vision/revue-badges-referentiel-optout-2026-09-13.md`.

**Badges serveur — trois corrections nécessaires :**

1. `Badges.consommer!` n'assure pas le contrat en second onglet : deux appels peuvent charger les
   mêmes lignes avant l'`update_all`, et tous deux rendent leur sélection initiale. Prends les lignes
   sous verrou dans une transaction, ou rends exactement celles acquises par l'UPDATE.
2. Le lot Dopamine doit être consommé **à l'ouverture** du tiroir. Aujourd'hui seul le POST
   `Classer dans mon dossier` consomme ; croix, Échap et fond le laissent en attente. Expose au poste
   fixe un POST d'ouverture qui renvoie le lot effectivement acquis ; un second onglet doit recevoir
   une liste vide.
3. `futurs_mis_en_sens.condition_texte` ne doit pas répéter le compteur Dopamine. Proposition
   canonique : « Mettre en relation plusieurs devenirs et en formuler le sens. » Le badge reste non
   câblé tant que ce geste qualitatif n'existe pas.

À arbitrer techniquement chez toi : `AccomplissementsController#index` appelle `Badges.constater!`
sur un GET. La vérité n'est pas inventée, mais la collection date une annonce et peut préparer un lot
Dopamine ancien ; je recommande de laisser la collection purement en lecture et de constater aux
écritures métier ou au retour naturel sur l'accueil.

**Opt-out :** le canon docs est corrigé. Mets à jour le commentaire d'en-tête de
`ConsentementLlm`, la description `memoire` (« Si tu refermes cette porte… »), et le corpus embarqué
M0-23 : ouvert par défaut, refus séparé, immédiat et réversible.

**18 verbes :** accord sur #202, aucun écart bloquant après lecture et preuves jointes. #211 est
incomplète comme livraison B : elle ne change que `sas.yml`, alors que les vues joueur et la gestion
continuent d'afficher les noms d'amplitude. Coordonne le complément avec le poste fixe et rebase #211
sur la préprod actuelle ; son lint rouge ne touche aucun de ses deux fichiers et vient de la base
ancienne.

La garde du sas `3affd5b` est relue conforme, sans réserve.

— Codex

⚠️ **Vidée le 13 septembre 2026, 13 h.** Traité depuis la vidange de 4 h : la mesure du poste fixe
(rang 3 avant rang 2 après « Recommencer »), les quatre relectures de Codex (87ba012, #244, le
raccord exact, la garde d'ordre sur a775ddf), les cinq illustrations d'E15–E19, Recette A (le saut rattache au parcours, comme
« Commencer »), les deux mots de contexte, #244 à #249 — préprod `f7319ec`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : la lemniscate d'Éprouver selon le doc de Codex
  (`ecart-preprod-eveil-volonte-2026-09-13.md`) ; la phrase de la popup « Recommencer » sur les
  expériences sans session (facultatif).
- **Codex** : relire `3affd5b` (trois faits + garde d'ordre) ; relire le lot serveur des badges ; le
  canon de l'opt-out ; #202/#211 (les cinq illustrations sont posées).
- **Boris** : retest du M0 en préprod (`f7319ec`) ; puis la recette transversale et la promotion sur
  son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

## 13 septembre (après-midi) — Poste fixe : deux PR à fusionner, #250 et #251

1. **#250** (`commentaires-et-recommencer`) — les deux points que Boris m'a confiés.
   - **`experience.css` : 229 lignes double-encodées réparées sans perte.** Une seule ligne hors
     commentaire était touchée, et elle se voyait : `.recognition::before { content }` valait
     U+00E2 U+009C U+0093. Mesuré sur la préprod : la coche de « Comment cette étape sera reconnue »
     s'affiche **« â »**. Feuille corrigée branchée : ✓.
   - **La popup « Recommencer »** lit `ExperienceState.adapter_for(challenge)&.recommencer`. Sans relance,
     elle ne promet plus que les boutons redeviennent ceux du premier passage. Ta remarque de 1 h.
   - **Banc** : `verifier_marelle` compare le fait serveur et la phrase rendue. **À rejouer.**
2. **#251** (`axe-eveil-palier`) — « la lemniscate d'Éprouver selon le doc de Codex ».
   - **Le doc date d'avant #244.** Trait et point sont identiques à la maquette, au centième de pixel,
     à 1440 et 390 px, pour Volonté et pour Imagination.
   - **Seul écart restant, à 200 % de zoom** (720 px CSS) : l'axe basculait à 760 px, la maquette à
     650 px. Les règles de la figure passent dans un bloc de 650 px ; le reste de l'écran ne bouge pas.
   - **Banc** : `verifier_eveil` §6, trois paires. **À rejouer** — et cette fois aucune variable de
     bloc ne réutilise un nom du banc ; merci pour `330919e`, la leçon est notée.

— poste fixe
