# Marelle Monde 0 — écarts entre la matrice éditoriale et la base

> **Constat du 16 août, poste fixe, au moment de porter la maquette
> `volonte-marelle-m0-cible`.** La matrice
> [monde-0-puissance-intensite-effet.md](../pedagogie/monde-0-puissance-intensite-effet.md)
> demande explicitement (recette § 6, point 7) que « les durées affichées soient confrontées aux
> données réelles avant livraison ». Voici cette confrontation.
>
> **Arbitrage de Boris : la page affiche le RÉEL**, lu depuis `Challenge#duration` et depuis la
> composition effective du `Journey` — conformément à la règle du contrat YAML (« continuer à lire
> la durée depuis `Challenge#duration` lorsqu'elle existe ») et à la doctrine « aucune donnée
> inventée ». Les écarts ci-dessous restent donc **visibles dans l'application** tant qu'ils ne
> sont pas arbitrés. Les corriger touche `Challenge` et `ChallengesJourney` : c'est la zone du
> portable, pas celle de l'intégration.

## Ce qui concorde parfaitement

Les **quatorze expériences** de la matrice ont toutes un `Challenge` en base, dans le **même
ordre**, sans manquant ni surnuméraire. Les trois chapitres (`Page` intercalées en positions 1, 7
et 12) découpent exactement les trois mouvements annoncés — expériences 1-5, 6-9, 10-14. Le
portage n'a donc rien à redécouper : il suffit de **nommer** les mouvements, ce que le YAML
éditorial permet déjà.

Seules divergences de libellé, sans conséquence : la base écrit « Le **s**as d'entrée » (matrice :
« Le **S**as »).

## Écart 1 — les durées : la base est plus courte d'environ 1 h 45

La matrice annonce un parcours obligatoire d'**environ 6 h 30**, Atelier compris. La somme réelle
des `Challenge#duration` vaut **≈ 4 h 47**.

Six expériences sont hors de la fourchette cible :

| # | Expérience | Base | Cible matrice | Écart |
|---:|---|---|---|---|
| 1 | Le Point Zéro : entrer dans le Jeu | 7 min | 8–10 min | −1 à −3 min |
| 2 | Le Coupable idéal | 10 min | 15–20 min | **−5 à −10 min** |
| 4 | Avant le Zéro | 15 min | 20–30 min | **−5 à −15 min** |
| 6 | L'écosystème Point Zéro | 5 min | ≈ 15 min | **−10 min** |
| 9 | Les choses se précisent | 30 min | 15–20 min | **+10 à +15 min** |
| 12 | Le Sas d'entrée | 1 h | 1 h 30 | **−30 min** |

Les huit autres sont dans la fourchette, le plus souvent à sa borne haute.

**À arbitrer** : soit la base est corrigée pour rejoindre les cibles éditoriales, soit la matrice
est révisée d'après les durées réelles constatées. Tant que rien n'est tranché, la page annonce
≈ 4 h 47 — ce qui contredit visiblement le « environ 6 h 30 » du document canonique.

## Écart 2 — « Découvrir les formats » est optionnel en base

La matrice décrit **13 expériences obligatoires et le Sas d'entrée optionnel**. En base, **deux**
expériences portent `required: false` :

- `le-sas-d-entree` (position 15) — conforme à la matrice ;
- `decouvrir-les-formats` (position 14) — **non prévu par la matrice**.

Conséquence mesurable : `JourneyProgress` compte `requis_total = 12`, pas 13, et
`preparations` renvoie `["decouvrir-les-formats", "le-sas-d-entree"]`.

**TRANCHÉ — Boris, 16 août au soir** : « Découvrir les formats » **est bien optionnel**. La
base a raison, c'est la MATRICE qui doit être corrigée. Un joueur achève donc le Monde 0 avec
**12 expériences obligatoires**, et deux préparatifs libres : « Découvrir les formats » et le Sas
d'entrée.

➡️ Action pour Codex ou le portable : corriger
`docs/pedagogie/monde-0-puissance-intensite-effet.md`, qui classe encore cette expérience en
« M0 · obligatoire · 10–15 min ». Rien à changer dans l'application : `JourneyProgress` compte
déjà juste.

## Anomalie relevée en passant — Omégas du chapitre 2

Sans rapport avec le portage, mais constatée pendant l'instruction sur le compte de démonstration :
le **chapitre 2 affiche 112 Ω gagnés pour 24 Ω au total**. Les Omégas gagnés dépassent la somme
des `total_point` des Challenges du chapitre — soit les Ω viennent d'ailleurs (bonus, événement,
attribution manuelle), soit le dénominateur est incomplet.

La vue borne déjà l'affichage pour ne pas montrer un ratio absurde, mais la cause n'est pas
identifiée. À regarder du côté de l'attribution des Ω, hors de la zone d'intégration.

## Ce que le portage fait en attendant

- affiche la **puissance globale 3/10**, valeur éditoriale de la matrice, jamais recalculée ;
- affiche **14 expériences**, et la durée cumulée **réelle** ;
- distingue les optionnelles telles qu'elles sont **en base** (donc deux, pas une) ;
- nomme les **trois mouvements** d'après la matrice ;
- affiche par expérience l'**intensité**, l'**effet** et les **conditions** de la matrice, et sa
  **séquence en trois étapes** — qui reste une lecture éditoriale, sans créer aucun état de
  progression concurrent.
