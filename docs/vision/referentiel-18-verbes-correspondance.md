# Correspondance du référentiel vers les 18 verbes

Note Codex — 11 septembre 2026. Demande de Boris : six Puissances, trois verbes par Puissance, un référentiel commun sans distinction privé/public entre ses compétences. Cette livraison établit la correspondance ; elle ne migre pas la base.

## Table cible

Les verbes et les 36 libellés d’amplitude sont extraits des six fiches `config/puissances/{slug}.yml` à la révision `8c3b3cb5e3b36a0a16854bcf1fbecd99de42df9d` de pointzero-app/preprod. Ce sont des correspondances de vocabulaire, pas la preuve que chaque libellé existe actuellement comme Skill en base. La Source est identifiée par son cadre : ses six noms historiques ont été complétés depuis l'inventaire du portable du 11 septembre.

| Puissance | Orientation | Compétence cible | Anciens libellés regroupés |
|---|---|---|---|
| Désir | Ombre | JE CONTIENS | Retenue / Contrôle / Inhibition |
| Désir | Source | JE SUIS | DÉSIR : INTENTION |
| Désir | Lumière | J'EMBRASE | Amplification / Exaltation / Ferveur |
| Volonté | Ombre | JE SERS | Service / Dévouement / Sacrifice |
| Volonté | Source | JE DÉCIDE | VOLONTÉ : SOUVERAINETÉ |
| Volonté | Lumière | JE DIRIGE | Initiative / Leadership / Domination |
| Imagination | Ombre | JE RÉALISE | Réalisme / Conformité / Vacuité |
| Imagination | Source | JE CRÉE | IMAGINATION : CRÉATION |
| Imagination | Lumière | JE RÊVE | Projection / Inspiration / Vision folle |
| Émotion | Ombre | JE DISTANCIE | Détachement / Dissociation / Glaciation |
| Émotion | Source | JE RESSENS | ÉMOTION : PRÉSENCE |
| Émotion | Lumière | JE COMMUNIE | Passion / Fusion / Communion |
| Communication | Ombre | J'ÉCOUTE | Écoute / Effacement / Silence |
| Communication | Source | JE M'EXPRIME | COMMUNICATION : EXPRESSION |
| Communication | Lumière | JE CAPTIVE | Persuasion / Séduction / Envoûtement |
| Intuition | Ombre | JE DOUTE | Ouverture / Suspension / Non-savoir |
| Intuition | Source | JE DISCERNE | INTUITION : DISCERNEMENT |
| Intuition | Lumière | JE CROIS | Conviction / Certitude / Foi totale |

## Règle de rattachement

Une compétence cible est identifiée par le couple **Puissance + Ombre/Source/Lumière**, avec un verbe affiché. Les clés du CSV sont des clés de correspondance proposées, pas des identifiants Rails existants. Le contexte de Puissance reste affiché avec le verbe.

Pour une ancienne compétence, vérifier son `derived_framework`, son nom et son contenu. Si ces trois éléments concordent, la rattacher au même couple Puissance/polarité : ses amplitudes 1, 2 et 3 convergent vers un seul verbe. Une compétence Source reste Source ; ne pas la répartir entre Ombre et Lumière.

Exemples attestés par le diagnostic portable : Skill #91 « COMMUNICATION : EXPRESSION », cadre `Communication - Source`, correspond à **Communication · JE M’EXPRIME** ; Skill #96 « INTUITION : DISCERNEMENT », cadre `Intuition - Source`, correspond à **Intuition · JE DISCERNE**. Leur rattachement privé/public courant doit être relu après l’accord de publication transmis le 10 septembre : il ne détermine pas la cible sémantique.

Un nom manquant à cette table, un cadre vide/inconnu ou une contradiction entre nom et cadre est un cas à examiner, pas une correspondance automatique. Ne pas rapprocher des noms par ressemblance et ne pas affecter par défaut à Source. La Transcendance reste hors des 18 ; ne pas créer de compétence polaire pour elle.

## Ce que cela conserve

L’expérience propose d’exercer un verbe ; elle ne promet pas de produire une amplitude. Les amplitudes demeurent dans les fiches, questionnaires et récits d’accompagnement. Aucun résultat d’évaluation, degré Ombre/Lumière ou état de circulation n’est recalculé par cette correspondance.

Les Ω conservent leur valeur et leur provenance réelle (joueur, expérience, attribution). Ils reconnaissent le geste selon les règles existantes ; ils ne deviennent pas une mesure d’amplitude. Les totaux par joueur, expérience, Puissance et polarité doivent rester identiques.

Le référentiel cible est commun aux expériences Point Zéro : 18 compétences utilisables sans choix privé/public. Cela ne supprime pas globalement les droits des communautés ni la confidentialité des données personnelles. Le mécanisme technique de ce référentiel commun devra être analysé avant implémentation.

## Analyse d’impact préalable à la migration

La lecture du code montre que `User#power_breakdown` agrège les points par `skills.derived_framework` et que `RestitutionM0` en extrait la Puissance. Conserver les cadres exacts indiqués dans le CSV permet de préserver cette lecture. Les noms seuls ne suffisent pas.

`Skill` possède des relations avec `points` et `challenges_skills` déclarées `dependent: :destroy`. **Ne supprimer aucune ancienne compétence pour effectuer un simple regroupement** : cela pourrait supprimer les liens et l’historique. Préparer d’abord un plan de conservation ou de transfert contrôlé de chaque référence, avec une trace de l’ancien identifiant et du libellé historique.

Si une expérience utilise plusieurs anciennes compétences convergeant vers le même verbe, inventorier les lignes, leur montant et leurs règles : ne pas dédupliquer en perdant des Ω, ni réattribuer les Ω déjà gagnés. Vérifier aussi les attributions dynamiques, notamment « Lire mon Moteur », et toutes les sélections de Skill par cadre, nom ou identifiant. Les correspondances ne doivent pas dépendre d’un `find_by` ambigu entre plusieurs lignes du même cadre.

## Complément demandé au portable : inventaire en lecture seule

Produire une ligne par Skill existant, y compris ceux sans utilisation : id, nom, framework, derived_framework, communauté et visibilité courante, cible proposée, statut de correspondance et raison. Joindre une table des rattachements par expérience (id/slug, Skill, montant et champs de règle réellement présents), ainsi que les nombres et sommes des Point par Skill et par expérience. Aucun nom de joueur ni autre donnée personnelle dans la livraison partagée.

Signaler les doublons par cadre, les variantes de noms, les cadres hors des 18 et les collisions de rattachements après regroupement. Distinguer le référentiel en base de ses descriptions pédagogiques : les 36 amplitudes restent documentées même lorsqu’elles ne sont plus des compétences attribuables.

La table sémantique est complète pour les six fiches ; l’inventaire id-par-id et la simulation des totaux sont nécessaires pour rendre la migration exécutable. Aucun changement de base, de modèle, de validation ou de droits n’est effectué dans cette livraison.

## Sources

- [Configurations des Puissances à la révision examinée](https://github.com/PointZero2050/pointzero-app/tree/8c3b3cb5e3b36a0a16854bcf1fbecd99de42df9d/config/puissances).
- [Modèle Skill](https://github.com/PointZero2050/pointzero-app/blob/8c3b3cb5e3b36a0a16854bcf1fbecd99de42df9d/app/models/skill.rb), [agrégation du joueur](https://github.com/PointZero2050/pointzero-app/blob/8c3b3cb5e3b36a0a16854bcf1fbecd99de42df9d/app/models/user.rb), [restitution](https://github.com/PointZero2050/pointzero-app/blob/8c3b3cb5e3b36a0a16854bcf1fbecd99de42df9d/app/services/restitution_m0.rb).
- Diagnostic portable des Skills #91/#96 : [historique partagé](https://github.com/PointZero2050/zegame-docs/commit/076a890).

## Complément : inventaire reçu et contrôlé

Les 42 identifiants sont désormais reliés aux 18 cibles dans [la correspondance par identifiant](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-par-identifiant.csv). Le [contrôle détaillé](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-controle-inventaire.md) distingue les 96 Ω statiques de M0, ses 4 Ω dynamiques et les 10 Ω hors parcours. La migration reste à préparer ; la correspondance id-par-id est complète pour cet export.
