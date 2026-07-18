# Atlas de l’Émotion — 27 médaillons livrés

> Brief initial Claude - 2026-07-18. Matrice des 27 archétypes, contrat de nommage et intentions fonctionnelles préparés pour la génération.
>
> Ajout Codex - 2026-07-18. Série produite avec OpenAI à partir de ce brief, de la direction artistique validée par Boris et du référentiel [`corpus-point-zero/03_archetypes/emotion.md`](corpus-point-zero/03_archetypes/emotion.md). Les fichiers sont prêts pour l’intégration par Claude.

## Contrat technique

- 27 PNG RGBA, fond transparent, 512 × 512 px ;
- médaillon circulaire et bord de papier intégrés à l’image ;
- nommage `emotion-o{O}-l{L}-{etat}.png` ;
- états internes `bloque`, `intermediaire`, `libre` ;
- manifeste machine : [`assets/atlas/emotion/manifest.json`](assets/atlas/emotion/manifest.json).

## Grammaire visuelle

- collage néoarchaïque en papier découpé, cohérent avec les séries précédentes ;
- **vert cœur dominant**, décliné en émeraude, jade, menthe et vert forêt ;
- charbon, ivoire, papier chaud et aqua glacé comme couleurs secondaires ;
- onde de résonance horizontale, formée de deux courbes opposées réunies par un battement central, comme glyphe principal ;
- fils relationnels, membranes, vagues, contenants, glace et dégel comme vocabulaire secondaire ;
- plan humain explicite à 75-80 %, plan symbolique implicite à 20-25 % ;
- diversité d’âges, de genres et d’origines répartie entre tous les états, sans codage moral.

L’intensité ne mesure ni la sensibilité ni la valeur affective d’une personne. Elle décrit l’amplitude de la résonance et de la protection. Les états montrent la capacité de circulation : débordement ou fermeture en état bloqué, différenciation et réversibilité en état intermédiaire, ouverture suivie d’un retour à soi en état libre.

## Matrice livrée

| Amplitude | Bloqué | Intermédiaire | Libre |
|---|---|---|---|
| O1-L1 | Le Sensible sous contrôle | Le Cœur en apprivoisement | Le Témoin sensible |
| O1-L2 | L’Empathe inquiet | L’Empathe en différenciation | L’Empathe ancré |
| O1-L3 | Le Cœur sans rivage | L’Amoureux océanique en ancrage | Le Cœur océanique |
| O2-L1 | Le Fonctionnel anesthésié | Le Cœur dégelé | Le Contenant sensible |
| O2-L2 | Le Sauveur alternant | Le Régulateur en alchimisation | Le Régulateur empathique |
| O2-L3 | Le Sauveur universel | Le Grand Cœur en discernement | Le Gardien de la communion |
| O3-L1 | La Machine mentale | Le Veilleur du dégel | Le Veilleur impassible |
| O3-L2 | L’Amant polaire | Le Cœur en résurrection | Le Régénérateur affectif |
| O3-L3 | Le Cœur apocalyptique | L’Amant initiatique | Le Cœur total |

## Points d’intégration

1. Vérifier la lisibilité de l’onde et du geste principal entre 80 et 120 px.
2. Préserver le contraste entre vert vivant, vert forêt et glace menthe sur fonds clairs et sombres.
3. Ne pas utiliser un cœur sentimental générique à la place du glyphe de résonance.
4. Conserver bordures, sélections et effets d’état dans l’interface, hors des fichiers.
5. Prévoir un repli vers l’illustration générique de la puissance si une ressource manque.
