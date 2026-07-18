# Atlas de la Volonté — 27 médaillons livrés

> Ajout Codex - 2026-07-18. Série produite avec OpenAI à partir du référentiel validé dans [`corpus-point-zero/03_archetypes/volonte.md`](corpus-point-zero/03_archetypes/volonte.md). Les fichiers sont prêts pour l'intégration par Claude.
>
> **✅ Intégré par Claude - 2026-07-18.** 27 médaillons convertis en 256 px et déployés dans `public/pz/puissances/atlas/` sur vibe.ze.game ; la fiche `/puissances/volonte` affiche le bon médaillon selon la position/état diagnostiqués (repli sur l'illustration ronde de pôle si ressource manquante). Nommage reçu conforme (`volonte-o{O}-l{L}-{etat}.png`), aucune retouche nécessaire.

## Contrat technique

- 27 PNG RGBA, fond transparent, 512 × 512 px ;
- médaillon circulaire et bord de papier intégrés à l'image ;
- nommage `volonte-o{O}-l{L}-{etat}.png` ;
- états internes `bloque`, `intermediaire`, `libre` ;
- manifeste machine : [`assets/atlas/volonte/manifest.json`](assets/atlas/volonte/manifest.json).

## Grammaire visuelle

- collage néoarchaïque en papier découpé, cohérent avec l'Atlas du Désir ;
- **orange dominant**, décliné en safran, cuivre et orange brûlé ;
- bordeaux profond pour les tensions d'Ombre, complété par charbon, ivoire et papier chaud ;
- triangle vertical comme glyphe principal de la Volonté ;
- chemins, axes, ponts, charges, mandats et gestes de transmission comme vocabulaire secondaire ;
- plan humain explicite à 75-80 %, plan symbolique implicite à 20-25 % ;
- vêtements contemporains archétypaux, sans imagerie militaire ni royauté de fantasy.

La montée d'intensité ne correspond pas à une montée de prestige. Elle se lit dans la portée du cap, le poids de la responsabilité et le degré de contrainte exercé. Les états décrivent la circulation entre action et service : centralisation en état bloqué, apprentissage du partage en état intermédiaire, prise et restitution du pouvoir en état libre.

## Matrice livrée

| Amplitude | Bloqué | Intermédiaire | Libre |
|---|---|---|---|
| O1-L1 | Le Bon Élève | L'Allié en éveil | Le Coopérant souverain |
| O1-L2 | Le Leader défensif | Le Capitaine en apprentissage | Le Leader-serviteur |
| O1-L3 | Le Protecteur autoritaire | Le Conquérant en pacification | Le Gardien du seuil |
| O2-L1 | Le Dévoué sans élan | Le Pilier en émergence | Le Pilier discret |
| O2-L2 | Le Responsable captif | Le Pilote en alchimisation | Le Capitaine solidaire |
| O2-L3 | Le Croisé du bien commun | Le Stratège en conversion | Le Stratège consacré |
| O3-L1 | Le Héros épuisé | Le Souverain en résurrection | Le Serviteur du passage |
| O3-L2 | Le Martyr charismatique | Le Roi blessé en réconciliation | Le Souverain sacrificiel |
| O3-L3 | Le Tyran sacrificiel | Le Roi initiatique | Le Souverain alchimique |

## Points d'intégration

1. Vérifier la lisibilité du triangle et du geste principal entre 80 et 120 px.
2. Tester les médaillons sur fonds clair, beige et sombre.
3. Conserver les effets d'état, bordures et sélections dans l'interface, hors des fichiers.
4. Éviter d'afficher trop de détails textuels autour d'une vignette : l'image porte déjà une narration dense.
5. Prévoir un repli vers l'illustration générique de la puissance si une ressource manque.
