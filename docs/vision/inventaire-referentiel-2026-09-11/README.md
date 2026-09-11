# Inventaire du référentiel de compétences — 11 septembre 2026

Complément portable à [`referentiel-18-verbes-correspondance.md`](../referentiel-18-verbes-correspondance.md),
demandé par Codex. **Lecture seule** sur la production (`pointzero-web-1`, code `main@e0a8f9d`
+ données du 11 septembre au matin) : aucune écriture, aucun compte créé, aucune donnée
personnelle — les Ω sont agrégés, jamais nommés. Script : `scripts/inventaire_18_verbes.rb`
(à commiter avec ce dossier).

## Fichiers

| fichier | contenu |
|---|---|
| `skills.csv` | **42 lignes**, une par Skill : id, nom, framework, derived_framework, communauté, visibilité, nombre de rattachements, Points (nombre, Ω), clé cible, verbe cible, **statut**, raison |
| `rattachements.csv` | **52 lignes**, une par `ChallengesSkill` : expérience (id, slug, `total_point`), Skill, **montant** (`point`), clé cible |
| `points_par_experience.csv` | Points réellement gagnés, par expérience : nombre, Ω, joueurs distincts (comptés, pas nommés) |
| `simulation.csv` | Totaux par cadre : Ω promis par les expériences, Ω gagnés en base, appartenance aux 18 |
| `cas_a_examiner.txt` | doublons par cadre, variantes de noms, collisions, statuts |

La règle de correspondance est celle de la note : **par le cadre** (`derived_framework`), jamais
par ressemblance de nom ; le nom sert à *vérifier*. Un cadre Source est rattaché à sa cible Source
et son nom historique est consigné tel quel. Aucun rapprochement automatique, aucune affectation
par défaut.

## Ce que la base contient — et c'est plus propre que prévu

**42 Skills, tous dans les 18 cadres.** Statuts : `correspond` × 36, `Source — nom inventorié` × 6.
**Aucune** contradiction nom/cadre, **aucun** cadre vide ou hors table, **aucune** variante de nom.

Chaque cadre Ombre et Lumière porte **exactement trois** Skills — les trois amplitudes de la table
de Codex, sans exception ni manque. Ce sont donc bien 36 amplitudes qui convergent vers 12 verbes.

**Les six Sources**, dont la note demandait le nom sans le deviner :

| Puissance | Skill | nom historique | visibilité | rattachements | Ω gagnés |
|---|---|---|---|---|---|
| Désir | #62 | INTENTION | publique | 3 | **5** |
| Volonté | #60 | SOUVERAINETÉ | publique | 3 | 0 |
| Imagination | #86 | CRÉATION | **privée** | **0** | 0 |
| Émotion | #76 | PRÉSENCE | publique | 4 | 0 |
| Communication | #91 | EXPRESSION | **privée** | 1 | 0 |
| Intuition | #96 | DISCERNEMENT | **privée** | 1 | 0 |

Trois Sources sur six sont privées. Deux d'entre elles sont rattachées à une expérience du
parcours (rangs 9 et 12) — c'est le cas EXPRESSION/DISCERNEMENT du diagnostic du 10 septembre. La
troisième, **Imagination · JE CRÉE, n'est rattachée à rien**.

## Rattachements et collisions

**52 rattachements**, dont 47 sur les 20 expériences du parcours (14 en portent 3, 4 en portent 1,
`lire-mon-moteur` et l'épilogue n'en portent aucun — le premier attribue dynamiquement, comme la
note le prévoit) et 5 sur des challenges hors parcours (`test-1` × 4, `servir-une-cause` × 1).

**Aucune collision** : aucune expérience n'est rattachée à deux Skills qui convergeraient vers le
même verbe. Le regroupement ne fusionnerait donc aucune ligne et ne dédupliquerait aucun Ω.

**Cinq verbes ne sont exercés par aucune expérience** : Désir · JE CONTIENS, Volonté · JE DIRIGE,
Imagination · JE RÉALISE, Imagination · JE CRÉE, Émotion · JE DISTANCIE. C'est un fait éditorial,
pas une anomalie de données — mais la note dit « l'expérience propose d'exercer un verbe », et
cinq des dix-huit n'ont aujourd'hui aucune expérience pour le proposer.

## Simulation des totaux

La cible étant **le cadre**, les totaux par cadre sont invariants par construction. Ce qui aurait
pu bouger, c'est ce qui vit sur un cadre hors des 18 : **rien** — 0 Ω promis, 0 Ω gagné.

| | Ω |
|---|---|
| promis par les expériences (somme des `ChallengesSkill.point`) | **106** |
| gagnés en base (somme des `Point`) | **5** |
| hors des 18 | **0** |
| joueurs ayant des Ω | 1 |

Les 5 Ω gagnés sont sur `faconner-mon-jumeau` → Désir - Source (#62 INTENTION). La production a
été remise à zéro le 31 août : c'est l'unique attribution depuis.

`User#power_breakdown` et `RestitutionM0` agrègent par `derived_framework` : conserver les cadres
exacts du CSV cible préserve ces deux lectures sans les toucher.

## Ce que cet inventaire ne décide pas

- **La mécanique du « référentiel commun sans privé/public ».** Aujourd'hui `Challenge#skill_visibility`
  refuse tout Challenge public rattaché à un Skill privé ; c'est ce qui gèle l'édition des rangs 9
  et 12. Supprimer la distinction *dans le référentiel* sans toucher aux droits des espaces demande
  une analyse du modèle, pas un `update`. La publication ponctuelle des deux Sources, préparée le
  10 septembre, **n'a pas été exécutée** — elle est devenue une question de migration, pas de
  rattachement.
- **La forme du regroupement.** `Skill` détruit ses `points` et `challenges_skills` en cascade : le
  plan de conservation ou de transfert, avec trace de l'ancien id et du libellé, précède toute
  suppression. Cet inventaire donne la liste id par id qu'un tel plan doit reprendre.
- **Le sort des 36 amplitudes comme descripteurs.** Elles restent documentées ici avec leur id et
  leur cadre ; ce qu'elles deviennent dans les fiches de Puissance est un travail de vues.
