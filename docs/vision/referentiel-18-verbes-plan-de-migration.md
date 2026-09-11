# Référentiel des 18 verbes — plan de migration réversible

Note du portable, 11 septembre 2026. Réponse à la demande de Codex dans
[`referentiel-18-verbes-controle-inventaire.md`](referentiel-18-verbes-controle-inventaire.md) :
« préparer le plan de migration réversible : choix explicite des 18 identifiants canoniques ou
création de nouvelles lignes, traitement des anciennes lignes et de toutes leurs références,
conservation des libellés historiques, sélection unique par cadre, mise à disposition commune du
référentiel ». **Aucune écriture serveur** : ce document précède la migration et attend les
arbitrages de sa §6.

## 1. Ce qui référence une compétence — mesuré, pas supposé

Tout ce qui, en base et dans le code, tient une `Skill` (`main@` du 11 septembre) :

| où | comment | ce que le regroupement doit garantir |
|---|---|---|
| `challenges_skills.skill_id` | 52 lignes, montant `point` | chaque ligne suit son cadre ; aucune collision (Codex) |
| `points.skill_id` | 1 ligne, 5 Ω, sur #62 | provenance conservée, totaux inchangés |
| `skills.community_id` | 42 lignes, 2 communautés | droits des espaces préservés |
| `User#power_breakdown` | agrège par `derived_framework` | invariant si les cadres sont conservés |
| `RestitutionM0` | Puissance = préfixe du cadre | idem |
| `GainDynamique` | `Skill.find_by(derived_framework: "#{nom} - Source")` | **une seule** compétence par cadre, sinon `find_by` ambigu |
| `TraceSas.attribuer_omegas!` | `Skill.find_by(name:)` depuis `config/sas.yml` | les cinq noms du YAML doivent résoudre après regroupement |
| `Challenge#skill_visibility` | refuse un Skill dont la communauté n'est pas `default` | c'est **le** mécanisme public/privé à traverser |
| `gestion/experiences` | `Skill.where(community_id: [celle de l'expérience, nil])` | le référentiel commun doit y apparaître |
| `Challenge.import` | `Skill.find_or_create_by!(community_id:, name:)` | un import ne doit pas recréer une amplitude |

Deux faits que l'inventaire ne montrait pas :

- **`config/sas.yml` crédite cinq compétences par leur nom**, dont deux **privées** :
  `ÉMOTION : DÉTACHEMENT` (#79) et `VOLONTÉ : INITIATIVE` (#81). Donc **JE DISTANCIE et JE DIRIGE,
  « sans rattachement statique », reçoivent des Ω par les parcours du Sas** — comme JE CRÉE par
  « Lire mon Moteur ». Trois des cinq verbes sans rattachement ont un chemin d'acquisition.
- Aucun nom de Skill n'est en double toutes communautés confondues : `find_by(name:)` est
  aujourd'hui non ambigu. Il le resterait après regroupement **si les noms historiques sont
  conservés** — et cesserait de l'être si l'on renommait en verbes (deux Skills « JE SERS »).

## 2. Le choix : 18 canoniques parmi les 42, les 24 autres deviennent des amplitudes

Je recommande **de ne créer aucune ligne** et de désigner, par cadre, une compétence
**canonique** parmi les existantes. Raisons : les six Sources sont déjà seules sur leur cadre
(rien à choisir) ; pour les douze cadres Ombre/Lumière, une seule des trois porte des
rattachements dans huit cas ; et moins de références bougent (seules les lignes qui pointent une
non-canonique). Créer 18 lignes neuves déplacerait les 52 rattachements et le Point, pour la même
identité sémantique.

**Règle de désignation**, mécanique et consignée : par cadre, la compétence qui porte **le plus de
rattachements** ; à égalité, **le plus de Points** ; à égalité, **l'identifiant le plus bas**. Sur
les données du 11 septembre, cela donne :

| cadre | canonique | verbe | les deux autres, amplitudes |
|---|---|---|---|
| Désir - Ombre | #61 CONTRÔLE (0 ratt., id le plus bas) | JE CONTIENS | #74 RETENUE, #75 INHIBITION |
| Désir - Source | #62 INTENTION | JE SUIS | — |
| Désir - Lumière | #73 FERVEUR (2 ratt.) | J'EMBRASE | #71 AMPLIFICATION (1 ratt.), #72 EXALTATION |
| Volonté - Ombre | #59 SERVICE (5) | JE SERS | #82 DÉVOUEMENT (1), #83 SACRIFICE |
| Volonté - Source | #60 SOUVERAINETÉ | JE DÉCIDE | — |
| Volonté - Lumière | #81 INITIATIVE (id le plus bas ; **crédité par le Sas**) | JE DIRIGE | #84 LEADERSHIP, #85 DOMINATION |
| Imagination - Ombre | #63 RÉALISME (id le plus bas) | JE RÉALISE | #89 CONFORMITÉ, #90 VACUITÉ |
| Imagination - Source | #86 CRÉATION | JE CRÉE | — |
| Imagination - Lumière | #64 PROJECTION (8) | JE RÊVE | #87 INSPIRATION, #88 VISION FOLLE |
| Émotion - Ombre | #66 DISSOCIATION (id le plus bas) | JE DISTANCIE | #79 DÉTACHEMENT (**crédité par le Sas**), #80 GLACIATION |
| Émotion - Source | #76 PRÉSENCE | JE RESSENS | — |
| Émotion - Lumière | #65 PASSION (4) | JE COMMUNIE | #77 FUSION, #78 COMMUNION |
| Communication - Ombre | #67 ÉCOUTE (4) | J'ÉCOUTE | #94 EFFACEMENT, #95 SILENCE |
| Communication - Source | #91 EXPRESSION | JE M'EXPRIME | — |
| Communication - Lumière | #68 PERSUASION (4) | JE CAPTIVE | #92 SÉDUCTION, #93 ENVOÛTEMENT |
| Intuition - Ombre | #70 OUVERTURE (6) | JE DOUTE | #99 SUSPENSION, #102 NON-SAVOIR |
| Intuition - Source | #96 DISCERNEMENT | JE DISCERNE | — |
| Intuition - Lumière | #69 CONVICTION (4) | JE CROIS | #97 CERTITUDE (1), #98 FOI TOTALE |

⚠️ Deux cadres méritent un regard humain plutôt que la règle : **Émotion - Ombre**, où la règle
désigne #66 DISSOCIATION alors que c'est #79 DÉTACHEMENT que le Sas crédite ; et **Volonté -
Lumière**, où #81 INITIATIVE tombe juste parce que son id est le plus bas. La règle est
mécanique ; le choix final est éditorial (§6).

## 3. Ce qui change en base — additif, journalisé, réversible

**Migration 1 — schéma, sans données.** Sur `skills` : `canonique` (booléen, faux), `verbe`
(chaîne), `remplacee_par_id` (entier, nul). Sur `challenges_skills` et `points` :
`skill_origine_id` (entier, nul). Un index unique partiel `skills(derived_framework) WHERE
canonique` — c'est **la base** qui garantit « une seule par cadre », pas une convention. Rien ne
bouge encore.

**Étape de données — un script, avec simulation d'abord** (`SIMULATION=1`, patron de
`importer_inscrits_wordpress.rb`) :
1. rejouer l'inventaire sur données fraîches ; **s'arrêter** si un Skill, un rattachement ou une
   collision est apparu depuis le 11 septembre ;
2. marquer les 18 canoniques (règle §2 ou choix humain), poser `verbe` depuis
   `referentiel-18-verbes-correspondance.csv`, poser `remplacee_par_id` sur les 24 autres ;
3. pour chaque `challenges_skills` et `points` dont le Skill est remplacé : écrire
   `skill_origine_id = skill_id`, puis `skill_id = remplacee_par_id`. **Aucune ligne supprimée,
   aucune fusionnée** — Codex a vérifié qu'aucune expérience ne porte deux Skills du même cadre,
   donc l'index `(challenge_id, skill_id)` ne peut pas se heurter ;
4. témoins avant/après, **tous** : nombre de `challenges_skills` (52), somme des montants (106),
   nombre de `points` (1) et somme (5), et les totaux **par joueur, par expérience, par Puissance
   et par polarité** — un seul total global ne suffit pas (Codex). Ils doivent être identiques,
   par construction.

**Les 24 amplitudes** restent des `Skill`, avec leur nom, leur cadre, leur communauté : ce sont
les descripteurs de degré des fiches de Puissance. Elles ne sont plus **rattachables** (§4), elles
restent **lisibles**. Aucune suppression — `Skill` détruit ses Points et rattachements en cascade.

**Réversibilité.** Un script `defaire_regroupement.rb` : `skill_id = skill_origine_id` là où il
est posé, puis `skill_origine_id`, `remplacee_par_id`, `verbe`, `canonique` remis à nul/faux ;
mêmes témoins. La migration 1 se retourne par `down`. Rien n'ayant été supprimé, le retour est
complet.

## 4. Le référentiel commun — sans publier le cercle, sans toucher aux droits

Le mécanisme public/privé, aujourd'hui, c'est `Challenge#skill_visibility` (une expérience
publique refuse un Skill dont la communauté n'est pas `default`) et la liste de
`gestion/experiences` (les Skills de la communauté de l'expérience). Trois Sources canoniques
sont privées (#86, #91, #96). Deux voies :

- **(a) déplacer les 18 canoniques dans la communauté publique.** Simple, mais c'est *publier*
  trois Skills du cercle pédagogique — l'accord de Boris couvre #91 et #96, pas #86 — et cela
  confond deux notions : appartenir au référentiel commun, et appartenir à une communauté.
- **(b) faire du drapeau `canonique` la définition du référentiel commun.** `skill_visibility`
  accepte un Skill si sa communauté est `default` **ou** s'il est canonique ; `gestion/experiences`
  liste les Skills de la communauté **plus** les canoniques ; `GainDynamique` et `TraceSas`
  cherchent parmi `Skill.canonique`. Les 24 amplitudes gardent leur communauté et leurs droits ; le
  cercle pédagogique n'est pas publié ; aucune communauté ne perd rien.

Je recommande **(b)** : c'est exactement « un référentiel commun de 18 compétences utilisables
sans choix privé/public » sans « supprimer globalement les droits des communautés ». L'accord
ponctuel sur #91/#96 y est absorbé : ils deviennent canoniques, pas publics.

## 5. Le code qui suit, et ses bancs

- `GainDynamique` : `Skill.canonique.find_by(derived_framework:)` — non ambigu par l'index.
- `TraceSas` : `Skill.find_by(name:)` puis, si `remplacee_par_id`, la canonique — ou mettre
  `config/sas.yml` à jour vers les clés cibles. Je préfère la seconde : le YAML nomme ce qu'il
  crédite, il ne devrait pas nommer une amplitude.
- `Challenge.import` : `find_or_create_by!` doit chercher parmi les canoniques avant de créer.
- Affichage : le `verbe` pour une canonique, le nom historique pour une amplitude — là où le
  joueur les voit (fiche, restitution), c'est la zone du poste fixe.
- **Banc `verifier_referentiel_18`** : exactement 18 canoniques, une par cadre (et l'index le
  tient) ; totaux par cadre égaux à l'inventaire de référence ; une expérience publique accepte
  une canonique privée et refuse une amplitude privée ; la liste de gestion porte les 18 ;
  `GainDynamique` et le Sas résolvent sans ambiguïté ; **rejouer `verifier_intensites`,
  `verifier_omegas_*`, `verifier_traces_parcours` et `verifier_restitution_m0`** — ceux qui lisent
  les Ω par cadre ou par nom.

## 6. Ce qui reste à arbitrer avant d'écrire

1. **Désignation des canoniques** : la règle mécanique de la §2, ou un choix éditorial — au moins
   pour Émotion - Ombre (DISSOCIATION vs DÉTACHEMENT, crédité par le Sas) et Volonté - Lumière.
2. **#86 CRÉATION** : l'accord de Boris vaut-il pour elle comme pour #91/#96 ? Avec la voie (b),
   elle devient canonique sans être publiée ; le mot reste à obtenir.
3. **Le nom affiché au joueur** : le verbe seul, ou « verbe · nom historique » pendant une
   transition — décision d'affichage, zone du poste fixe.
4. **`config/sas.yml`** : mettre à jour ses cinq noms vers les cibles, ou résoudre par
   `remplacee_par_id`. Je recommande la mise à jour, dans la même livraison.

Rien de tout cela n'est exécuté. L'ordre proposé : arbitrages → migration 1 → simulation sur
données fraîches → écriture → bancs → préprod → recette transversale → production.

---

## 7. Plan complété après la relecture de Codex (11 septembre, soir)

Réponse à [`referentiel-18-verbes-relecture-plan.md`](referentiel-18-verbes-relecture-plan.md).
Ce qui suit **remplace** les points des §3 à §6 qu'il contredit ; le reste tient. Toujours
**aucune écriture serveur** : cette section précède une pull request (diff reviewable) et une
simulation sans écriture.

### 7.0 Ce que la relecture tranche, et que je prends tel quel

- Les **18 couples sont communs, #86 CRÉATION compris** — arbitrage 2 de la §6 clos.
- Affichage **Puissance · VERBE**, sans amplitude — arbitrage 3 clos ; le nom historique reste
  dans la traçabilité et les descriptions pédagogiques.
- `sas.yml` désigne les **clés cibles** (`emotion.ombre`, `volonte.lumiere`…), mêmes montants,
  mêmes conditions — arbitrage 4 clos.
- La **table mécanique** de la §2 est acceptée (#66 et #81 compris) **à condition d'être
  figée** : elle devient une constante revue dans le script, et le script **s'arrête** si les
  données ne lui correspondent plus. Elle n'est plus recalculée. — arbitrage 1 clos, sauf le
  regard humain sur Émotion - Ombre et Volonté - Lumière, qui reste ouvert mais n'empêche rien
  (changer une ligne de la table, c'est changer une constante avant la première exécution).

### 7.1 Le verbe ne se stocke pas, il se lit — un champ de moins

Mesuré ce soir : les six `config/puissances/<slug>.yml` portent déjà `verbes.<pôle>.mot`, et
les dix-huit mots sont **exactement** ceux de `referentiel-18-verbes-correspondance.csv`. Un
`derived_framework` (« Émotion - Ombre ») désigne un couple (puissance, pôle) ; le verbe s'en
déduit. **La colonne `verbe` du §3 est retirée** : une valeur recopiée en base à côté de sa
source YAML finirait par diverger, et « un état se lit, il ne se stocke pas » vaut aussi pour
une configuration. `Skill#verbe` lit le YAML ; `Skill#libelle` rend « Puissance · VERBE » pour
une canonique, et le nom historique pour une amplitude.

Correction 2 de Codex, par construction : **les 36 descriptions d'amplitude ne sont pas dans
`skills`**. Elles vivent dans `intensites.<pôle>.{1,2,3}` et `pouvoirs.<pôle>.{1,2,3}` des six
YAML — les trois degrés de chaque pôle, y compris ceux dont le nom sert d'identifiant à une
canonique (FERVEUR reste le degré 3 de Désir - Lumière, pas la définition de J'EMBRASE). Les 42
lignes gardent leur `name` et leur `description` ; rien n'y est réécrit.

### 7.2 Correction 1 — un référentiel de 18, pas 18 plus les anciennes

La règle n'est pas « canonique ou publique » mais **« jamais une amplitude remplacée »** — c'est
`remplacee_par_id` qui exclut, pas `canonique` qui autorise. Ainsi un éventuel référentiel hors
Point Zéro (aucun aujourd'hui : les 42 Skills sont dans les 18 cadres) n'est pas restreint par
ricochet.

| producteur | règle après bascule | où elle vit |
|---|---|---|
| nouveau rattachement (`ChallengesSkill`) | refuse un Skill remplacé, à la création ou au changement de `skill_id` | validation modèle — donc gestion, saisie directe d'identifiants et import |
| nouvelle attribution (`Point`) | idem | validation modèle — donc `set_validated_at`, `GainDynamique`, `TraceSas` |
| sélecteur de gestion | liste `Skill.rattachables` (non remplacées) de la communauté **plus** les canoniques | `Gestion::ExperiencesController` |
| `Challenge#skill_visibility` | une expérience publique accepte une canonique privée ; refuse toujours une amplitude privée ; une amplitude remplacée est refusée en amont | validation modèle |
| import | une référence se **résout** : clé cible (`desir.ombre`) → canonique ; nom historique → sa canonique via `remplacee_par_id` (alias explicite) ; inconnue → **l'import s'arrête et nomme la valeur**. Plus jamais de `find_or_create_by!` | `Skill.resoudre!` |

Les lectures historiques (`Point` et `ChallengesSkill` déjà écrits, `skill_origine_id`) restent
lisibles selon les droits existants ; rien n'est caché.

### 7.3 Correction 3 — deux fenêtres de retour, nommées

- **Fenêtre (a) — avant toute nouvelle écriture.** Le script écrit un **journal** JSON
  (`tmp/regroupement-18-<env>-<horodatage>.json`) : pour chaque ligne modifiée, table, id,
  champs **avant** et **après** ; pour chaque Skill, drapeaux avant/après ; l'empreinte de
  `config/sas.yml` avant/après. `defaire_regroupement_18.rb` relit ce journal, **vérifie que
  chaque ligne est encore dans son état « après »** — sinon il s'arrête : une activité a eu
  lieu, on est en fenêtre (b) — puis restaure exactement l'état « avant ». Il ne restaure pas
  « une clé étrangère » : il restaure le journal.
- **Fenêtre (b) — après reprise d'activité.** Retour de **code** seulement, schéma additif
  conservé. Les lignes écrites après la bascule visent une canonique — une compétence ordinaire,
  avec son cadre : l'ancien code les lit sans rien changer. Elles n'ont pas d'amplitude
  d'origine et **n'en recevront jamais une inventée**. Aucun `down` de données n'est annoncé
  pour cette fenêtre ; aucun Point n'est supprimé pour permettre un retour.

Le script est **transactionnel** (une transaction, `LOCK TABLE challenges_skills, points IN
EXCLUSIVE MODE` le temps de la bascule — 53 lignes, quelques millisecondes — pour qu'aucune
attribution concurrente ne s'écrive entre les témoins), **rejouable** (une ligne déjà déplacée
— `skill_origine_id` posé et `skill_id` canonique — est sautée, jamais réécrite ; une seconde
exécution déplace 0 ligne et rend les mêmes témoins), et **s'arrête sur divergence** (un Skill
absent de la table figée, un cadre qui ne correspond pas, un Skill apparu depuis).

### 7.4 Correction 4 — ordre de déploiement, environnements nommés, contraintes

**Livraison A — schéma additif + code compatible + script + simulation** (une PR sur
`preprod`, relue avant fusion) :

- migration : `skills.canonique` (booléen, faux), `skills.remplacee_par_id` (FK → `skills`),
  `challenges_skills.skill_origine_id` et `points.skill_origine_id` (FK → `skills`) ; index
  unique partiel `skills(derived_framework) WHERE canonique` ; contraintes `remplacee_par_id <>
  id` et `NOT (canonique AND remplacee_par_id IS NOT NULL)`. Le « même cadre » et « la cible est
  canonique » (donc pas de chaîne ni de cycle : une canonique n'est jamais remplacée) sont des
  validations du modèle **et** des contrôles du script — SQL ne les exprime pas sur deux lignes.
- code **compatible dans les deux états** : `GainDynamique` et `TraceSas` résolvent par
  `Skill#cible` (la canonique désignée si elle existe, sinon le Skill lui-même) — avant
  désignation, comportement **identique** à aujourd'hui, donc aucune requête ne cherche une
  canonique avant qu'elle existe ; les validations de 7.2 sont inertes tant que
  `remplacee_par_id` est nul partout.
- `scripts/regrouper_referentiel_18.rb` — **simulation par défaut**, `ECRIRE=oui` pour écrire.
  La partie lecture (table figée, divergences, lignes à déplacer, témoins par joueur / par
  expérience / par Puissance / par polarité) tourne **sans le schéma** : c'est ce qui permet de
  joindre à la PR une simulation faite sur les données de production, en lecture seule.
- banc `verifier_referentiel_18` : les **18 cadres attendus** (l'ensemble, pas un compte), une
  canonique par cadre et l'index qui le tient ; aucune ligne de `points` ni `challenges_skills`
  ne vise un Skill remplacé ; chaque `skill_origine_id` a le cadre de son `skill_id` ; refus d'un
  rattachement et d'un Point sur une amplitude remplacée (publique #74, privée #94) ; une
  expérience publique accepte #91 canonique privée ; la liste de gestion porte les 18 ;
  `GainDynamique` et les cinq portes du Sas résolvent la cible ; rejeu sans double gain ;
  seconde exécution du script = 0 ligne.

**Livraison B — bascule des lecteurs** (seconde PR, après A appliquée et données regroupées) :
`config/sas.yml` vers les cinq clés cibles ; le sélecteur de gestion ; `Skill#libelle` posé sur
la fiche et la restitution — la vue est au poste fixe, le libellé est fourni.

**Séquence, environnement par environnement :**

| # | où | quoi | témoin |
|---|---|---|---|
| 1 | production, lecture seule | simulation du script (données fraîches) jointe à la PR A | 0 divergence, lignes à déplacer, témoins avant |
| 2 | préprod | fusion A, migration, **simulation**, puis `ECRIRE=oui`, journal, **seconde exécution** | témoins identiques avant/après, 0 ligne au rejeu |
| 3 | préprod | `defaire_regroupement_18.rb` depuis le journal, puis regroupement à nouveau | retour exact, puis état regroupé |
| 4 | préprod | fusion B, recette transversale | `TOUT EST VERT` |
| 5 | production | sauvegarde vérifiée, promotion A, migration, simulation, écriture, journal conservé hors du conteneur | témoins identiques |
| 6 | production | promotion B, recette transversale | `TOUT EST VERT` |

Les nombres 52 et 5 de l'inventaire ne sont **pas** des attendus du banc : les témoins se
capturent à chaque exécution, avant et après, sur les données du moment.

### 7.5 Recette (la liste de Codex, reprise telle quelle)

Attributions statiques et dynamiques · cinq portes Sas · import (clé, alias, inconnue) · ancien
identifiant public et privé refusés pour un nouveau rattachement · provenance historique ·
conservation des totaux par joueur / expérience / Puissance / polarité · absence de double gain
au rejeu · simulation puis seconde exécution · retour arrière fenêtre (a) éprouvé, fenêtre (b)
décrite. Couverture des verbes : statique (13 cadres), dynamique (JE CRÉE par Lire mon Moteur ;
JE DISTANCIE et JE DIRIGE par le Sas), effectivement enregistrée (à lire en base, jamais
déduite) — trois lectures distinctes, jamais confondues.
