# Boîte du portable

## 13 septembre — Codex : revue de `462092b`, partie serveur soldée

J'ai relu les commits `64c918d`, `87c763e` et `462092b` sur la branche servie.

- `Badges.consommer!` rend uniquement les identifiants acquis par son propre
  `UPDATE … RETURNING` ; le banc à deux connexions prouve union égale au lot et intersection vide.
- `POST /badges/remise` reste l'unique route, en JSON pour l'ouverture et en HTML pour le repli.
- la collection est bien redevenue une lecture ; le seuil des futurs reste qualitatif et non câblé ;
- `MentorReponse#section_contexte`, la mémoire et M0-23 suivent désormais l'opt-out, y compris le cas
  où aucune matière n'est disponible sans révéler si une porte est vide ou refermée.

Aucun écart bloquant trouvé dans cette partie. Restent au poste fixe : le branchement du tiroir sur
le lot JSON, la collection à trois familles avec place secrète anonyme, et le complément responsive
de l'éveil à 650 px. Le référentiel A/B reste séparé et attend son circuit de migration explicite.

— Codex

⚠️ **Vidée le 13 septembre 2026, 15 h.** Traité depuis la vidange de 13 h : la revue de Codex
(badges — consommation atomique, POST d'ouverture, seuil secret qualitatif, collection en lecture ;
opt-out — les trois textes ; 18 verbes — branches rafraîchies, complément B défini), #250 et #251 du
poste fixe — puis les trois notes suivantes de Codex (la consigne active du mentor, une seule route pour la remise, le palier 650 px relayé au poste fixe) — préprod `462092b`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le tiroir Dopamine sur `POST /badges/remise` en JSON (contrat dans sa boîte) ; #251 bis — tout le bloc mobile de l'éveil à 650 px (décision de Codex, relayée) ; la place
  anonyme du badge secret et l'aide « deux mémoires » de la collection ; le complément B des 18 verbes
  (après A, au mot de Boris).
- **Codex** : rien en attente de lui aujourd'hui (revue reçue et intégrée).
- **Boris** : retest du M0 en préprod (`462092b`) ; la fusion de #202 (A, migration additive) sur la
  préprod, puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR dependabot
  (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

## 13 septembre (fin d'après-midi) — Poste fixe : #252 et #253 à fusionner

1. **#252** (`eveil-650-et-phrase`) — la suite de #251 que Codex a demandée, et la phrase de #250.
   - **Tout l'écran d'éveil bascule à 650 px** : un seul palier de largeur dans `eveil.css`.
   - **Mesuré** : à 720 et 651 px, tout reste large (rail, trois colonnes, figure de 285 px) ; à 650 et 390 px, tout est mobile ; aucun débordement.
   - **Popup « Recommencer »** : la phrase est celle de Codex, à la lettre.
   - **À rejouer** : `verifier_eveil` (§6 réécrit) et `verifier_marelle`.
2. **#253** (`badges-revue-codex`) — ton relais de 15 h.
   - **Le tiroir Dopamine** : le clic poste `POST /badges/remise` en JSON et ouvre avec le seul `remis`. Un lot vide n'ouvre rien ; ensuite, tous les gestes ferment. La carte cède la place à une phrase focalisée qui mène à la collection. « Classer » reste le repli sans script.
   - **Mesuré au navigateur**, `fetch` simulé pour ne rien consommer : POST avant l'ouverture, carte périmée retirée, focus conservé.
   - **La collection** : l'aide présente trois mémoires ; un secret non obtenu garde une carte anonyme, inerte (sans `data-badge`).
   - **À rejouer** : `verifier_serie_de_badges` §3 (l'adresse du déclencheur, le POST avant `showModal`) et `verifier_accomplissements`, dont le compte est **retourné** : 18 cartes, places anonymes comprises.
   - **Déjà faits chez toi, rien de mon côté** : le seuil futur (`condition_texte`) et les textes de l'opt-out.

Le complément B des 18 verbes attend ton signal sur A.

— poste fixe

## 13 septembre (soir) — Poste fixe : #252 grossit — le vrai bandeau sur l'éveil, et deux fichiers chez toi à relire

Boris, sur `/parcours/eveil/volonte?etape=3`, pour la énième fois : « c'est encore l'ancienne version du bandeau excursion ». Il avait raison. L'éveil gardait un en-tête maison, sous le menu et avec l'ancien chemin de fer. `verifier_excursion` §6 exigeait en effet « aucun bandeau sur l'éveil », parce que le « Revenir » du partagé y rebouclait.

**Nouveau commit sur #252.** Deux points touchent des fichiers que tu fréquentes :

1. **`layouts/jeu.html.haml`** : `= yield :bandeau_contexte` juste après `render "shared/bandeau_excursion"`. Le bloc est vide partout, sauf sur l'éveil, qui y rend le balisage du partagé avec son propre lien (`@retour` = `Excursion.retour_ou_repli`).
2. **`verifier_excursion` §6** : l'assertion « sur l'écran d'éveil, aucun bandeau » est **retournée**. Le bandeau est là, et son lien ne passe pas par `/excursion/retour`, ce qui garde exactement le défaut d'origine.

**Aussi dans #252 :** au troisième écran, l'arrivée ouvre le vrai menu, et la ligne de la Puissance s'y éveille puis s'allume. « Terminer la découverte → » ferme le menu et ouvre l'emblème. Tout ce que le script ajoute au menu disparaît à la fermeture, et la coque n'est pas touchée.

**À rejouer à la fusion :** `verifier_eveil`, `verifier_excursion`, `verifier_marelle`. Mesuré au navigateur, le détail est dans la PR.

— poste fixe
