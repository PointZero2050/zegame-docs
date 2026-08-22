# Monde 0 — puissance, intensité, effet et séquences d'expérience

> **Ajout Codex — 2026-08-16. Arbitrage validé par Boris.** Ce document complète l'audit des
> quatorze expériences et débloque le portage de la maquette `volonte-marelle-m0-cible`. Il fixe
> les valeurs éditoriales du parcours Monde 0 ; il ne modifie ni la progression Rails, ni les
> validations, ni l'attribution des Omégas.

> **Révision — Claude (portable), 2026-08-16 au soir.** Deux arbitrages de Boris modifient ce
> document après sa validation initiale : **l'Atelier Point Zéro passe d'intensité 5 à
> intensité 2**, et la règle des intensités fortes devient **absolue** — elle n'a plus
> d'exception, puisque l'Atelier était la seule. Les trois passages concernés sont corrigés
> ci-dessous et signalés. Le reste du document est inchangé.
> La règle est désormais tenue par le code : `JourneyProgress.intensites_non_encadrees`
> (pointzero-app), vérifiée par `scripts/verifier_intensites.rb` avant chaque déploiement.

## 1. Décisions structurantes

### Puissance globale du parcours : **3/10**

Le Monde 0 constitue une traversée personnelle structurée, mobilise plusieurs Puissances et se
termine par un premier rite collectif. Il ne produit cependant pas encore de Cercle durable,
d'œuvre commune ni d'impact systémique mesuré. Sa puissance globale est donc fixée à **3/10**.

Cette valeur :

- est écrite éditorialement pour le parcours ;
- n'est ni la moyenne des expériences, ni une fonction des Omégas ;
- ne varie pas selon que le Joueur accomplit ou non le Sas optionnel ;
- décrit le potentiel du chemin, jamais la valeur ou le niveau de conscience du Joueur.

Un niveau 4 suppose déjà une transformation relationnelle ou collective durable : Cercle constitué,
Pacte-Source, œuvre commune ou action suivie dans le réel. Le niveau 10 reste réservé à un parcours
susceptible d'agir à l'échelle mondiale ; une expérience isolée ne peut pas l'atteindre.

### Intensité pour le Joueur : **1 à 5**

| Niveau | Libellé | Définition |
|---:|---|---|
| 1 | Douce | Découverte sans exposition personnelle significative |
| 2 | Engagée | Choix personnel, premier geste ou première mise en récit |
| 3 | Profonde | Remise en question ou implication émotionnelle significative |
| 4 | Initiatique | Confrontation structurée nécessitant un cadre renforcé |
| 5 | Rite de passage | Expérience collective tenue par un facilitateur |

Les niveaux 4 et 5 exigent un facilitateur certifié et **ne peuvent être publiés qu'au Monde 2 et
au-delà** (arbitrage Boris du 16 août, qui clôt le point M07 de la matrice d'impact). La règle
est **absolue et sans exception** : une expérience initiatique ou un rite de passage sans
encadrement peut abîmer quelqu'un.

L'Atelier Point Zéro n'y déroge pas — il est passé en **intensité 2**. Il reste le rite collectif
et facilité qui ouvre le Monde 1 : c'est sa MODALITÉ qui le dit, pas son intensité. L'Atelier du
Festival accueille des personnes qui découvrent ; il ne doit ni s'annoncer comme une confrontation
initiatique, ni tomber sous la règle réservée au Monde 2.

> **Piège de vocabulaire.** « Rite de passage » désigne ici le niveau 5 de l'échelle
> d'intensité. D'autres documents — `monde-0-matrice-revision.md` notamment — emploient la
> même expression au sens NARRATIF : l'Atelier est le passage qui ouvre le Monde 1. Les deux
> sens coexistent et ne se confondent pas. L'Atelier est un rite de passage dans le récit, et
> une expérience d'intensité 2 sur l'échelle.

### Échelle d'effet : **1 à 5**

| Niveau | Libellé | Définition |
|---:|---|---|
| 1 | Personnel | L'expérience déplace d'abord le regard, le récit ou le choix du Joueur |
| 2 | Relationnel | Elle peut modifier un lien ou provoquer une rencontre réelle |
| 3 | Collectif | Elle agit sur un groupe qui traverse ou produit quelque chose ensemble |
| 4 | Systémique | Elle modifie durablement un cadre, une organisation ou un écosystème |
| 5 | Civilisationnel | Elle contribue directement à une transformation à très grande échelle |

Le sujet abordé ne détermine pas l'effet. Une vidéo sur une crise civilisationnelle reste à effet
personnel si son résultat observable est seulement un déplacement intérieur.

## 2. Structure globale en trois mouvements

1. **Franchir le seuil — Je pressens** : expériences 1 à 5 ; crises, récits, Moteur, futurs et
   Appel.
2. **Reconnaître la constellation — Je relie** : expériences 6 à 9 ; écosystème, ressources,
   premier geste relationnel et Graine de relation.
3. **Prendre place — Je contribue** : expériences 10 à 14 ; Conseil, formats, rencontre
   collective, Atelier et récit de passage.

La structure canonique comporte **14 expériences**, dont **12 obligatoires** et **deux
optionnelles** : « Découvrir les formats » et le Sas d'entrée. La matrice donnait « Découvrir les
formats » comme obligatoire ; la base la sert en optionnelle, et c'est la base qui fait foi. `Le Point Zéro : entrer dans le Jeu` et `Le Coupable idéal` sont deux Challenges
distincts.

## 3. Matrice des quatorze expériences

**Les durées ci-dessous sont celles de la base**, relevées le 16 août dans `Challenge#duration`
(arbitrage Boris : le réel prime sur la matrice). Ce ne sont donc pas des cibles à atteindre mais
la description de ce que l'application sert déjà. Toute correction se fait en base, puis se
reporte ici — jamais l'inverse.

| # | Expérience | Intensité | Effet | Conditions | Séquence éditoriale en trois étapes |
|---:|---|---:|---:|---|---|
| 1 | **Le Point Zéro : entrer dans le Jeu** | 1 — Douce | 1 — Personnel | M0 · obligatoire · solo · 10 min · aucun prérequis | **Regarder** l'introduction → **Relier** la chaîne invisible → **Formuler** une Hypothèse de seuil |
| 2 | **Le Coupable idéal** | 2 — Engagée | 1 — Personnel | M0 · obligatoire · solo · 10 min · expérience 1 | **Accuser** les coupables idéaux → **Défendre** leurs fonctions → **Délibérer** avec le Réel |
| 3 | **Une drôle d'époque** | 2 — Engagée | 1 — Personnel | M0 · obligatoire · solo · 20 min · expérience 2 | **Choisir** dans les situations → **Rencontrer** le mouvement inverse → **Lire** le premier miroir |
| 4 | **Avant le Zéro** | 3 — Profonde | 1 — Personnel | M0 · obligatoire · solo · 15 min · expérience 3 | **Entrer** dans la dispersion → **Traverser** un devenir → **Revenir** avec une Trace |
| 5 | **Et moi dans tout ça ?** | 2 — Engagée | 1 — Personnel | M0 · obligatoire · solo avec mentor · 20 min · expérience 4 | **Relire** les traces → **Dialoguer** avec le mentor → **Semer** la Graine de l'Appel |
| 6 | **L'écosystème Point Zéro** | 1 — Douce | 1 — Personnel | M0 · obligatoire · solo · 5 min · chapitre 1 achevé | **Découvrir** la constellation → **Relier** trois fragments → **Produire** un Schéma de circulation |
| 7 | **Le site du Point Zéro** | 1 — Douce | 1 — Personnel | M0 · obligatoire · solo connecté · 30 min · expérience 6 | **Explorer** des contenus → **Éprouver** sa compréhension → **Cartographier** deux résonances |
| 8 | **Le signe de reconnaissance** | 2 — Engagée | 2 — Relationnel | M0 · obligatoire après refonte · solo · 15 min · expérience 7 · envoi facultatif | **Choisir** une relation → **Composer** un signe → **Décider** de son canal ou de le conserver |
| 9 | **Les choses se précisent** | 2 — Engagée | 2 — Relationnel | M0 · obligatoire · solo avec mentor · 30 min · expérience 8 | **Relire** la constellation → **Nommer** une relation possible → **Semer** la Graine de relation |
| 10 | **Le Conseil Oméga** | 3 — Profonde | 1 — Personnel | M0 · obligatoire · solo · 25 min · chapitre 2 achevé | **Être convoqué** → **Arbitrer** entre les futurs → **Signer** un Rôle d'appel et des caps |
| 11 | **Découvrir les formats** | 1 — Douce | 1 — Personnel | M0 · **optionnel** · solo · 10 min · expérience 10 · agenda accessible | **Clarifier** son intention → **Comparer** les formats → **Produire** sa Boussole de passage |
| 12 | **Le Sas d'entrée** | 3 — Profonde | 2 — Relationnel | M0 · optionnel · collectif accompagné · 1 h · inscription et présence | **Se présenter** → **Éprouver** une première rencontre → **Clarifier** son intention |
| 13 | **Vivre l'Atelier Point Zéro** | 2 — Engagée | 3 — Collectif | M0 · obligatoire · collectif · 3 h · facilitateur · expériences obligatoires précédentes achevées | **Explorer** les futurs → **Reconnaître** le système en soi → **Franchir** le seuil en Cercle |
| 14 | **Mon récit de passage** | 3 — Profonde | 2 — Relationnel | M0 · obligatoire · solo avec mentor · 30 min · Atelier confirmé | **Rassembler** les traces → **Composer** la Graine de passage → **Sceller** la Carte du Seuil |

Le parcours obligatoire représente **6 h 30 exactement**, Atelier compris — somme des durées de
base, et non une estimation. Les deux expériences optionnelles ajoutent **1 h 10** (Sas 1 h,
Découvrir les formats 10 min) sans modifier la puissance globale ni conditionner le passage.

> **Comment le compte tombe juste.** La somme des durées valait 6 h 27. Plutôt que d'annoncer un
> « environ », Boris a tranché le 16 août : **« Le Point Zéro : entrer dans le Jeu » passe de 7 à
> 10 minutes en base**. C'était la valeur la moins ronde des quatorze, et 10 min était le haut de
> la fourchette que cette matrice donnait à l'origine. Une seule expérience touchée, et le total
> devient un nombre qu'on peut annoncer sans réserve.

## 4. Contrat d'affichage V1

### Au niveau du parcours

- afficher `Puissance globale du parcours · 3/10` ;
- afficher `14 expériences`, et non les 7 expériences fictives de la première maquette ;
- distinguer les 12 expériences obligatoires des deux expériences optionnelles : « Découvrir les
  formats » et le Sas d'entrée ;
- présenter les trois mouvements du parcours ;
- ne jamais recalculer le 3/10 depuis les intensités, les effets, les durées ou les Omégas.

### Au niveau de l'expérience

- afficher l'intensité et son libellé ;
- afficher l'effet et son libellé ;
- afficher le Monde minimal, la durée, la modalité et les prérequis ;
- afficher trois étapes éditoriales lorsque le dispositif les rend réellement vécues ;
- conserver séparément `action`, `trace`, `autorité de reconnaissance` et `Omégas`.

La séquence en trois étapes n'est **pas** une nouvelle machine de progression. Elle constitue la
lecture éditoriale du Challenge et de son dispositif interne. La validation canonique reste portée
par les modèles et services Rails existants. En particulier, le Challenge 1 ne doit plus afficher
`Le Coupable idéal` comme sa deuxième étape : celui-ci est le Challenge 2.

### Verbe de séquence et verbe de Puissance

Deux objets distincts apparaissent dans l'interface :

- `sequence[].verbe` décrit le geste pédagogique de l'étape : `Regarder`, `Relier`, `Semer`, etc. ;
- le verbe affiché à côté d'une Puissance décrit sa polarité mobilisée : par exemple
  `Intuition · Ombre · Je doute` ou `Imagination · Source · Je crée`.

Le second n'est pas rédigé expérience par expérience. Il est dérivé du couple
**Puissance + polarité** depuis `config/puissances/{slug}.yml`. La polarité elle-même est déjà
encodée dans le `derived_framework` de la compétence réelle associée à l'expérience. Les Puissances,
les polarités, les verbes et les montants d'Omégas doivent donc être lus depuis ces sources de
vérité, et non recopiés dans le YAML du parcours.

Avant portage, vérifier seulement les deux cas limites : toutes les compétences mobilisées portent
bien un `derived_framework`, et aucune expérience M0 ne dépend d'une Transcendance dépourvue de
configuration. Si ces contrôles passent, aucun tableau éditorial de 41 couples n'est nécessaire.

## 5. Logement recommandé des données

Pour la V1, utiliser un fichier versionné :

```text
config/journeys/point-zero-monde-0.yml
```

Ce fichier peut porter :

```yaml
version: 1
journey:
  transformation_power: 3
  stages: []
experiences:
  challenge-slug-stable:
    intensity: 1
    effect_scale: 1
    minimum_world: 0
    modality: solo
    sequence: []
```

Règles :

- référencer les Challenges par un slug stable, jamais par un titre éditorial ;
- continuer à lire la durée depuis `Challenge#duration` lorsqu'elle existe ;
- continuer à déduire l'ordre, le caractère obligatoire et les prérequis de la composition réelle
  du `Journey` ;
- ne pas réinterpréter silencieusement `Challenge#difficulty` en intensité ;
- ne dupliquer dans le YAML ni la validation, ni les Omégas, ni l'état du Joueur ;
- ne pas y dupliquer les Puissances, polarités ou verbes déjà dérivables des compétences et de
  `config/puissances/` ;
- prévoir une analyse d'impact avant tout changement de `Journey`, `Challenge`,
  `ChallengesUser`, `JourneysUser`, `JourneyProgress` ou callback `mathieu_core`.

Une migration vers des champs administrables pourra être envisagée lorsque plusieurs parcours
réels auront permis de stabiliser la taxonomie. Le YAML est ici un contrat éditorial V1, pas un
second modèle métier.

## 6. Recette attendue pour Claude

1. La page du parcours affiche 3/10, 14 expériences et trois mouvements.
2. Le Sas est visible comme optionnel et ne bloque ni l'Atelier ni la complétion obligatoire.
3. Chaque expérience affiche les valeurs de cette matrice sans utiliser `difficulty`.
4. L'expérience 1 ne fusionne plus artificiellement avec `Le Coupable idéal`.
5. Une séquence affichée ne crée aucun état de progression concurrent.
6. Aucun clic de maquette n'attribue d'Oméga, ne valide un Challenge ou ne débloque un chapitre.
7. Les durées affichées sont confrontées aux données réelles avant livraison.
8. Les vues mobiles conservent les libellés textuels des deux échelles ; la couleur seule ne porte
   jamais l'information.
