# Lots conçus avec Codex — ce qui est fait, ce qui reste

> Relevé par Claude (portable) le 2026-08-06, à la demande de Boris. Croise **les
> spécifications de Codex** dans ce dépôt avec **l'état vérifié du code et de la base de
> production**. Là où les deux divergent, le code fait foi.
>
> Méthode : chaque ligne « fait / — » est mesurée par introspection de la base et du code, pas
> déduite d'un document. Le script est en scratchpad ; les chiffres datent du 2026-08-06.

## 1. Ce qui est en ligne

| Chantier | État mesuré |
|---|---|
| Cercles — tables du lot 1 | Les cinq existent (`circles`, `circle_cycles`, `circle_memberships`, `pact_source_versions`, `circle_sessions`) · 1 cercle réel |
| Rôles tournants | Colonne `roles` sur `circle_sessions` |
| Profil communautaire | Annuaire `/profils` + fiche · territoire, présentation, langues, disponibilité |
| Messagerie | `Messaging::Thread` polymorphe · 69 fils sur `CircleMembership`, `JourneysUser`, `ChallengesUser` · non-lus (`last_seen_at`) |
| Blocage / signalement | `Blocage` et `Signalement` |
| Graines | Publication / dépublication depuis un message |
| Ressourcerie V1 | Deux corpus servis depuis YAML · évaluation par les cinq cadres |
| Monde 1 | Parcours Boussole · 6 expériences |
| Cartes-couvertures | Le gabarit existe — **2 couvertures sur 23** |

## 2. Messagerie et profil — l'écart avec la spécification V1

La spécification est
[profil-communautaire-messagerie-cercles-v1.md](profil-communautaire-messagerie-cercles-v1.md).
L'infrastructure est là ; ce qui manque est la **matière de la rencontre**.

### 2.1. Le dossier de rencontre n'existe pas (§ 3.3)

`circle_memberships` porte `status`, `joined_at`, `left_at`, `ouvert_au_cercle` — et rien d'autre.
Aucun des champs que la spécification demande : motivation, ce qu'on espère du Cercle, ce qu'on
pense y apporter, rythme et créneaux, présence/distance/hybride, territoire et contraintes de
déplacement, durée et intensité, rapport à la confrontation, sujets à éviter, besoins
d'accessibilité, expérience antérieure, autres appartenances, rôle d'appel, Graines jointes.

Conséquence : **on peut demander à rejoindre un Cercle, mais pas dire qui on est en le
demandant.** C'est le cœur du « se choisir » de la spécification.

### 2.2. Aucune notification par courriel (§ 5.2)

Vérifié : aucun mailer ne concerne les fils. Un candidat n'est jamais prévenu qu'on lui a
répondu — les conversations meurent en silence. C'est le manque le plus coûteux : il annule
en pratique tout ce qui est déjà construit.

La spécification est précise sur la forme : identité d'usage, type de demande, nom du Cercle, lien
profond, réglage des notifications. **Pas** de récit sensible, pas d'adresse révélée, pas de
réponse par courriel.

### 2.3. Les coordonnées ne se partagent pas (§ 5.1)

`users` n'a ni politique de contact, ni canal préféré, ni partage d'e-mail ou de téléphone par fil.
Le principe « permettre le contact ne signifie pas exposer les coordonnées » n'a aucun support.

### 2.4. Le profil détaillé est incomplet (§ 3.2)

Manquent : rôle d'appel, année d'entrée dans le Jeu, liens externes, préférences de rencontre,
badges et contributions épinglés.

### 2.5. Reste du § 6

Proposition de rencontre (créneaux ou lien), carte de contact partagée, prévention d'une nouvelle
sollicitation par la même personne.

### 2.6. Refactor annoncé par Codex (§ 8.1)

Les vues d'index et de conversation supposent un conteneur `ChallengesUser` ou `JourneysUser`.
Avec 69 fils dont certains sur `CircleMembership`, le titre, l'image, l'URL et le badge de contexte
doivent devenir polymorphes.

## 3. Le « 100 Ω » — mesuré, et confirmé impossible

Codex l'avait signalé dans
[analyse-impact-cercles-intercycle.md § 8.1](analyse-impact-cercles-intercycle.md). Vérifié sur la
production le 2026-08-06 : le Monde 0 plafonne à **84 Ω** sur les expériences requises, **99 Ω**
avec les optionnelles. Le joueur le plus avancé est à **99 Ω** — il a tout fait et n'atteindra
jamais 100.

Trois options, dans l'ordre de préférence de Codex :

1. **Critère structurel** — passage M1 = Monde 0 complété **+** Atelier validé. C'est déjà le
   critère de la Ressourcerie (`peut_evaluer_ressources?`) : un seul mécanisme, aucun nombre
   magique, insensible aux évolutions du barème.
2. Abaisser le marqueur à 80 Ω.
3. Recalibrer le barème — déconseillé : toucher aux `challenges_skills` recalculerait les Ω des
   joueurs existants au prochain `gain_points`.

**Décision attendue de Boris.**

## 4. Découverte du relevé — deux barèmes Ω coexistent

Ce n'est signalé nulle part et ça gêne dès maintenant la composition du Festival.

- `challenges_skills` : ce qui **crédite réellement** le joueur (`gain_points`). Monde 0 = 99 Ω.
- `challenges.point` : le champ **« Ω à la validation »** affiché dans la console. Monde 0 = 34 Ω.

**15 expériences sur 23 ont un écart entre les deux.** « Le sas d'entrée » affiche 4 et en crédite
12 ; « Le Coupable idéal » affiche 0 et en crédite 6.

Le joueur ne voit pas ce champ — il n'est rendu que dans la console. Mais **celui qui compose une
expérience croit régler les Ω et ne règle rien** : seule la ventilation par compétence, plus bas
dans le même formulaire, a un effet. À trancher : faire de `point` un calcul dérivé, ou l'expliciter
dans le formulaire comme un champ d'affichage sans effet.

## 5. Les autres lots, par ordre de dépendance

### Cercles, lots 2 à 5 ([spécification § 16](cercles-croissance-profils-flow-omega.md))

- **Lot 2 — Passage et cycle Monde 2** : journée de l'Intention souveraine, contrat individuel,
  cycle annuel, Pacte-Source complet, clôture et lignées, cagnotte **après cadrage juridique**.
- **Lot 3 — Profils et 360°** : profil de Cercle, cinq cadres, évaluations mi-cycle et fin de
  cycle, quatre regards.
- **Lot 4 — Héros et Freeride** : catalogue des figures inspirantes par puissance, mentor IA.
- **Lot 5 — Oméga avancé** : trois piliers, Contributions, missions, Cercle de redistribution,
  decay annuel.

Aucun modèle `Contribution`, `Mission`, `Resonance` ni `World` n'existe.

### Reste du lot 1, non livré

Traversée collaborative de l'Intercycle et parcours d'autofacilitation : aucun parcours ne porte
ces noms. C'est du contenu pédagogique autant que du code.

### Ressourcerie V2 et marketplace ([spécification](ressourcerie-marketplace.md))

Œuvre pédagogique versionnée avec droits et clés de redistribution, profils de
facilitateurs-designers, studio de création, séparation des économies. **Exige une revue juridique
avant toute ligne de code** — propriété intellectuelle, fiscalité, paiement, responsabilité.

### Monde 1 — catalogue

1 parcours sur les 12-14 visés par [monde-1-parcours.md](monde-1-parcours.md).

### Chantiers de vision non commencés

[Monde-miroir](monde-miroir.md) (jumeau numérique, quatrième mur, Empire et Cité Cosmique),
[game design autosubversif](game-autosubversion.md) (combats par runes, symétrie générative),
[récit-fresque et quêtes collectives](relations-recits-collectifs.md),
[page parcours « carte du voyage »](page-parcours-carte-du-voyage.md).

## 6. Ce que je recommanderais dans l'ordre

1. **La notification par courriel des fils.** Petit, isolé, et il débloque tout ce qui existe déjà.
2. **Trancher le marqueur de passage au Monde 1** (§ 3) — décision, pas développement.
3. **Clarifier les deux barèmes Ω** (§ 4) — gêne la production de contenu aujourd'hui.
4. **Le dossier de rencontre** (§ 2.1) puis le partage de coordonnées (§ 2.3) : c'est le lot
   « messagerie V1 » proprement dit, et il a du sens avant que des Cercles se forment au Festival.
5. Le refactor polymorphe des vues de fil (§ 2.6), qui conditionne la suite.

Tout le reste est postérieur au Festival.
