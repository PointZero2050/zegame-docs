# Relevé éditorial de la boîte du 24 octobre 2026

> Note Codex. Sept messages récents traités, sans modification du code applicatif
> ni du serveur. Les anciens messages informatifs restent dans la boîte.

## Réponses et livraisons

| Demande | Suite donnée |
|---|---|
| #486, page après limite | [Texte proposé](../site/textes-limite-de-tentatives-2026-10-24.md), sans délai inventé et avec retour générique à l’accueil. [Réponse PR](https://github.com/PointZero2050/pointzero-app/pull/486#issuecomment-6383741218). |
| #480, revalidation CGU | Phrase reçue conservée. La note d’origine est alignée : versions et dates uniquement en tête de `/cgu`. [Réponse PR](https://github.com/PointZero2050/pointzero-app/pull/480#issuecomment-6383741376). |
| A9, textes stores | [Premier brouillon](../site/stores-textes-captures-brouillon-2026-10-24.md) : champs, description, notes de revue et choix de captures. À arbitrer par Boris ; aucun formulaire de store rempli. |
| Bascule production | Compte rendu `6e1c1c9` et dates effectives CGU 1.1 / politique 1.2 au 24 octobre reçus. Pas de nouvelle recette de production par Codex. |
| #477, une résonance | Consigne conservée au mot près ; maquette alignée sur le remplacement/retrait. |
| #477, un smiley | Même règle indépendante. [Réponse commune PR](https://github.com/PointZero2050/pointzero-app/pull/477#issuecomment-6383741523). |
| #475, CTA et compteurs | Diff relu, conforme au complément demandé. [Accusé dans la PR](https://github.com/PointZero2050/pointzero-app/pull/475#issuecomment-6383741698). |

## Maquette actualisée

Branche `codex/messagerie-m1-popup-unique-20261018`, commit poussé
[`dc0b727`](https://github.com/PointZero2050/zegame-prototypes/commit/dc0b727).
Rendu partagé `compact.js`, consignes, libellés accessibles et notes.
Un smiley et une résonance au maximum par personne et message ; un autre choix
remplace le précédent dans la même catégorie, retoucher le sien le retire.
Les deux catégories restent indépendantes. « Tes résonances » reste le titre.
Le bandeau de compact.html reprend « J’exprime », conformément au canon reçu.

Épreuve locale au navigateur sur un message vide : smiley A → B → retrait,
total 1 → 1 → 0 ; résonance Ombre → Lumière → retrait, total 1 → 1 → 0.
`node --check compact.js` et diff propres. La correction des accords du singulier
a été vérifiée en source/syntaxe après ces gestes. Aucun comportement du serveur
n’est déduit de ces tests du simulateur.

## Suite du dossier stores

Le brouillon n’annonce ni notification native, ni hors-ligne, ni parcours futurs
comme déjà disponibles. L’accès public, les droits numériques du billet Festival,
la version candidate et les comptes de revue restent à fixer avant soumission.
Les captures proposées doivent venir du binaire soumis avec comptes fictifs,
pas des maquettes. Les identifiants de revue restent hors du dépôt partagé.
