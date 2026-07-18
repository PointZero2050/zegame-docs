# Atlas des archétypes — direction artistique et pilote

> Ajout Codex - 2026-07-18. Cette note accompagne le premier lot d'essai produit avec OpenAI pour la page de détail d'une Puissance. Les fichiers sont des PNG circulaires à fond transparent, prêts à être intégrés par Claude.

## Périmètre

La grille actuelle comprend **27 archétypes pour chacune des six Puissances polaires**, soit 162 images potentielles. La Transcendance décrit l'état global du Moteur et ne possède pas à ce stade une grille équivalente de 27 figures.

Le pilote ne cherche pas encore à couvrir les 27 figures du Désir. Il teste neuf médaillons répartis sur trois amplitudes :

- O1-L1 : faible amplitude ;
- O2-L2 : amplitude médiane ;
- O3-L3 : amplitude forte ;
- chaque amplitude est déclinée en bloque, intermediaire et libre.

## Format livré

- PNG RGBA, fond réellement transparent ;
- carré de 512 x 512 px ;
- médaillon circulaire centré ;
- aucun texte, logo, bordure d'interface ou état de sélection intégré ;
- fichier affichable entre 80 et 120 px dans l'interface ;
- détails importants concentrés dans la zone centrale.

L'application doit ajouter elle-même les bordures, ombres, états sélectionnés et effets de survol. Les sources de génération restent plus grandes ; seules les versions optimisées sont placées dans le dépôt.

## Grammaire visuelle

- collage néoarchaïque en papier découpé ;
- figure adulte archétypale, anguleuse et expressive ;
- palette du Désir : corail, rouge, or solaire, turquoise profond, charbon et papier chaud ;
- vocabulaire : feu intérieur, graine, sève, pulsation, contention, extinction et renaissance ;
- plan humain explicite dominant, plan symbolique intégré à environ 20-25 % ;
- silhouette, visage, mains et action principale lisibles en miniature.

Les états ne forment pas une échelle esthétique. Libre ne signifie ni plus beau, ni plus jeune, ni plus lumineux. La différence porte sur la capacité de circulation entre Ombre et Lumière. Le genre, l'origine, l'âge, la morphologie ou le handicap ne doivent jamais coder le blocage ou la valeur morale.

## Lot pilote du Désir

| ID | Archétype | Fichier |
|---|---|---|
| desir-o1-l1-bloque | Le Désir sous permission | [desir-o1-l1-bloque.png](assets/atlas/desir/pilot/desir-o1-l1-bloque.png) |
| desir-o1-l1-intermediaire | L'Élan en éveil | [desir-o1-l1-intermediaire.png](assets/atlas/desir/pilot/desir-o1-l1-intermediaire.png) |
| desir-o1-l1-libre | Le Gardien du rythme | [desir-o1-l1-libre.png](assets/atlas/desir/pilot/desir-o1-l1-libre.png) |
| desir-o2-l2-bloque | Le Funambule captif | [desir-o2-l2-bloque.png](assets/atlas/desir/pilot/desir-o2-l2-bloque.png) |
| desir-o2-l2-intermediaire | Le Navigateur du Désir | [desir-o2-l2-intermediaire.png](assets/atlas/desir/pilot/desir-o2-l2-intermediaire.png) |
| desir-o2-l2-libre | Le Danseur d'intensité | [desir-o2-l2-libre.png](assets/atlas/desir/pilot/desir-o2-l2-libre.png) |
| desir-o3-l3-bloque | Le Brasier affamé | [desir-o3-l3-bloque.png](assets/atlas/desir/pilot/desir-o3-l3-bloque.png) |
| desir-o3-l3-intermediaire | Le Phénix initiatique | [desir-o3-l3-intermediaire.png](assets/atlas/desir/pilot/desir-o3-l3-intermediaire.png) |
| desir-o3-l3-libre | Le Vivant total | [desir-o3-l3-libre.png](assets/atlas/desir/pilot/desir-o3-l3-libre.png) |

Le mapping machine est disponible dans [manifest.json](assets/atlas/desir/pilot/manifest.json).

## Critères du test d'intégration

1. Vérifier la lisibilité à la taille réellement utilisée dans la fiche.
2. Comparer les trois états sans afficher leur libellé.
3. Vérifier que les détails symboliques ne produisent pas de bruit visuel.
4. Tester les images sur fonds clair, beige et sombre.
5. Mesurer le poids et le temps de chargement d'une fiche contenant plusieurs médaillons.
6. Décider après intégration si la livraison finale reste en 512 px ou descend à 384 px.

