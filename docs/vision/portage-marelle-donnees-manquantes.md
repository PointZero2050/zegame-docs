# Marelle (Volonté, Monde 0) — ce qui manque pour porter la maquette

> **Constat du 16 août, poste fixe.** La maquette `volonte-marelle-m0-cible` était la première
> page du tableau de portage de `repartition-agents-phase-2.md` § 8. Elle a été **écartée du
> premier lot sur arbitrage de Boris** : ce n'est pas une refonte visuelle, c'est une **spec en
> avance sur le modèle**. Ce document liste précisément ce qu'il faut décider pour la débloquer.

> **Mise à jour Codex — 2026-08-16. Arbitrage obtenu.** Boris a validé le principe et demandé le
> chiffrage complet. La puissance du parcours est fixée à **3/10** ; les intensités, effets,
> conditions et séquences des quatorze expériences sont désormais définis dans
> [Monde 0 — puissance, intensité, effet et séquences d'expérience](../pedagogie/monde-0-puissance-intensite-effet.md).
> La recommandation V1 est un YAML versionné lu comme métadonnée éditoriale, sans réinterpréter
> `Challenge#difficulty` et sans créer de machine de progression concurrente. Le portage n'est donc
> plus bloqué par un arbitrage éditorial ; il reste soumis à l'analyse d'impact normale des zones
> `Journey` / `Challenge` / progression.

## Pourquoi ce n'est pas un simple portage

La règle du portage strict suppose que la maquette dise **la même chose** que l'application, en
mieux dessiné. Ici, la maquette introduit un **système d'indicateurs** qui n'existe nulle part
dans le code : ni colonne, ni YAML de configuration, ni service.

Porter quand même laisserait deux issues, toutes deux mauvaises : inventer des valeurs — ce que
la doctrine interdit (« aucune donnée inventée : un contenu manquant reste visiblement manquant
plutôt que comblé ») — ou livrer une page criblée de mentions « à arbitrer ».

## Ce qui existe déjà et se porterait sans rien décider

| Élément de la maquette | Source réelle |
|---|---|
| Chapeau, titre, sous-titre du parcours | `Journey` |
| Faits (« 7 expériences », « ≈ 4 h 30 », « Solo · puis en présence ») | `Journey` + agrégat des `Challenge#duration` |
| Chapitres, expérience suivante, seuil, accompli | `JourneyProgress.for(journey:, user:)` |
| Omégas gagnés / restants | `JourneyProgress` |
| Vignette et titre d'une expérience | `Challenge` |

## Ce qui n'existe pas — les décisions à prendre

### 1. « Puissance globale du parcours » — 3/10

La maquette l'explique elle-même comme *« une synthèse éditoriale de sa profondeur, de sa durée,
des itérations, des Puissances mobilisées et du potentiel d'impact »*, le niveau 10 correspondant
à *« une transformation capable d'agir à l'échelle mondiale »*.

C'est donc une **valeur écrite à la main, parcours par parcours** — pas un calcul. Rien ne la
porte aujourd'hui : le répertoire `config/journeys/` **n'existe pas**, si bien que
`JourneyProgress.config(slug)` renvoie toujours `nil`.

**Arbitrage obtenu** : valeur **3/10**, portée en V1 par
`config/journeys/point-zero-monde-0.yml`. Cette valeur éditoriale n'est calculée ni depuis les
Omégas, ni depuis une moyenne des expériences.

### 2. « Intensité pour toi » — 1/5

Échelle éditoriale nommée : *douce, engagée, profonde, initiatique, rite de passage*.

`Challenge#difficulty` existe mais est un entier **1..10** générique, sans ces libellés : le
faire passer pour l'intensité serait une réinterprétation silencieuse, pas un portage.

**Arbitrage obtenu** : les quatorze valeurs sont fixées dans la matrice pédagogique liée plus haut
et vivent dans le même YAML versionné. `difficulty` conserve sa sémantique historique.

### 3. « Échelle d'effet » — 1/5

Autre échelle nommée : *personnel, relationnel, collectif, systémique, civilisationnel*. Aucun
équivalent.

**Arbitrage obtenu** : les quatorze valeurs sont fixées dans la matrice pédagogique et portées par
le YAML V1. L'échelle décrit l'effet directement atteignable, pas l'importance du thème abordé.

### 4. « Conditions · Monde minimal »

La maquette affiche « Monde minimal · 0 » et une ligne de conditions (« ≈ 15 min · Solo · Aucun
prérequis »). La durée existe ; **la notion de « Monde minimal » n'existe pas** comme donnée.

**Arbitrage obtenu** : les expériences du parcours portent `minimum_world: 0` et une modalité
éditoriale dans le YAML. La durée continue de venir de `Challenge#duration`, tandis que l'ordre,
le caractère obligatoire et les prérequis restent déduits du Journey réel.

### 5. La séquence en trois étapes

La maquette découpe une expérience en trois étapes nommées et minutées — **REGARDER** (la vidéo,
4 min), **JOUER** (Le coupable idéal, 7 min), **CRISTALLISER** (conserver ce qui a bougé, 4 min).

C'est le point le plus structurant : l'application n'a **pas** cette granularité. « Le Coupable
idéal » y est un `Challenge` à part entière, pas l'étape 2 d'une expérience.

Des briques voisines existent (`Challenge#primary_video`, les quiz d'expérience, les retours
« apprécié / appris / manqué »), et l'on pourrait *deviner* une correspondance — précisément ce
que le portage strict interdit de faire seul.

**Arbitrage obtenu** : la séquence est une lecture éditoriale du Challenge et de son dispositif
interne, jamais un nouvel objet de progression. Elle peut vivre dans le YAML ; les états Rails
existants restent seuls canoniques. Le Challenge `Le Coupable idéal` ne figure donc plus comme
étape interne de l'expérience 1 : il reste l'expérience 2.

### 6. La grammaire de reconnaissance

Le bloc final annonce **ACTION** / **TRACE** / **RECONNAISSANCE** / **MISE EN CIRCULATION (6 Ω)**.
Seuls les Omégas existent ; les trois autres sont des libellés éditoriaux sans champ.

**Décision de portage** : ces libellés sont une projection lisible des dispositifs et autorités de
validation déjà documentés. Ils ne justifient pas de nouveau modèle générique en V1. Toute donnée
manquante reste explicitement absente jusqu'à l'analyse d'impact des validations concernées.

## En résumé

Les cinq concepts initialement manquants disposent maintenant d'un arbitrage éditorial. Claude peut
préparer le portage de la Marelle à partir de la matrice canonique et du contrat YAML V1. Avant de
toucher aux modèles ou aux callbacks, il doit toutefois produire l'analyse d'impact prévue pour les
zones sensibles et confronter les durées proposées aux `Challenge` réels.

Deux autres maquettes du tableau ont par ailleurs été écartées du premier lot :

- **`traces-m0-cible`** : elle propose « En faire une Graine → » et affiche cinq fois le mot
  « Graine », alors que `MesTracesController` refuse explicitement ce pont (« il n'existe pas
  encore ») et que `scripts/verifier_v5_mes_traces.rb` vérifie qu'aucune occurrence de ce mot
  n'apparaît. La porter casserait le banc. Elle omet en outre les retours d'expérience que la
  page affiche depuis le 16 août.
- **`heros-mentors-m0-cible`** : catalogue et fiche portables, mais son bouton « Choisir » serait
  mort au Monde 0 (`HerosController#choisir` exige `Coque.etat == :ouverte`), et sa vue « Mon
  mentor » dupliquerait la surface de `/mentor`.
