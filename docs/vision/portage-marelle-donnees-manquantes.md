# Marelle (Volonté, Monde 0) — ce qui manque pour porter la maquette

> **Constat du 16 août, poste fixe.** La maquette `volonte-marelle-m0-cible` était la première
> page du tableau de portage de `repartition-agents-phase-2.md` § 8. Elle a été **écartée du
> premier lot sur arbitrage de Boris** : ce n'est pas une refonte visuelle, c'est une **spec en
> avance sur le modèle**. Ce document liste précisément ce qu'il faut décider pour la débloquer.

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

**À décider** : la valeur pour le parcours du Monde 0, et son logement (un
`config/journeys/point-zero-monde-0.yml`, que le service sait déjà lire, semble le plus léger).

### 2. « Intensité pour toi » — 1/5

Échelle éditoriale nommée : *douce, engagée, profonde, initiatique, rite de passage*.

`Challenge#difficulty` existe mais est un entier **1..10** générique, sans ces libellés : le
faire passer pour l'intensité serait une réinterprétation silencieuse, pas un portage.

**À décider** : la valeur par expérience du Monde 0, et où elle vit.

### 3. « Échelle d'effet » — 1/5

Autre échelle nommée : *personnel, relationnel, collectif, systémique, civilisationnel*. Aucun
équivalent.

### 4. « Conditions · Monde minimal »

La maquette affiche « Monde minimal · 0 » et une ligne de conditions (« ≈ 15 min · Solo · Aucun
prérequis »). La durée existe ; **la notion de « Monde minimal » n'existe pas** comme donnée.

### 5. La séquence en trois étapes

La maquette découpe une expérience en trois étapes nommées et minutées — **REGARDER** (la vidéo,
4 min), **JOUER** (Le coupable idéal, 7 min), **CRISTALLISER** (conserver ce qui a bougé, 4 min).

C'est le point le plus structurant : l'application n'a **pas** cette granularité. « Le Coupable
idéal » y est un `Challenge` à part entière, pas l'étape 2 d'une expérience.

Des briques voisines existent (`Challenge#primary_video`, les quiz d'expérience, les retours
« apprécié / appris / manqué »), et l'on pourrait *deviner* une correspondance — précisément ce
que le portage strict interdit de faire seul.

**À décider** : la séquence est-elle un vrai objet du modèle, ou une lecture éditoriale d'un
`Challenge` ? La réponse appartient au portable et à Boris, pas à l'intégration.

### 6. La grammaire de reconnaissance

Le bloc final annonce **ACTION** / **TRACE** / **RECONNAISSANCE** / **MISE EN CIRCULATION (6 Ω)**.
Seuls les Omégas existent ; les trois autres sont des libellés éditoriaux sans champ.

## En résumé

**Cinq concepts sur six n'ont aucune donnée.** La Marelle se portera d'un bloc, fidèlement, dès
que ces valeurs seront arbitrées et logées. En attendant, le premier lot de portage strict porte
sur **Premières clés** (`premieres-cles-m0-cible` → `/premieres-cles`), dont le triage n'a
retrouvé qu'un seul champ manquant.

Deux autres maquettes du tableau ont par ailleurs été écartées du premier lot :

- **`traces-m0-cible`** : elle propose « En faire une Graine → » et affiche cinq fois le mot
  « Graine », alors que `MesTracesController` refuse explicitement ce pont (« il n'existe pas
  encore ») et que `scripts/verifier_v5_mes_traces.rb` vérifie qu'aucune occurrence de ce mot
  n'apparaît. La porter casserait le banc. Elle omet en outre les retours d'expérience que la
  page affiche depuis le 16 août.
- **`heros-mentors-m0-cible`** : catalogue et fiche portables, mais son bouton « Choisir » serait
  mort au Monde 0 (`HerosController#choisir` exige `Coque.etat == :ouverte`), et sa vue « Mon
  mentor » dupliquerait la surface de `/mentor`.
