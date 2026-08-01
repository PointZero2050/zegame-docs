# Ressourcerie V1 — principe d'affichage et navigation

> Proposition Claude — 2026-07-29, validée dans son principe avec Boris (périmètre V1 :
> fiches PZ + corpus non-PZ de pointzero2050.com/ressourcerie-cartographies/).
> Complète la carte éditoriale de Codex
> (`docs/pedagogie/carte-fiches-ressources-par-monde.md`) et s'inscrit dans l'horizon de
> `docs/vision/ressourcerie-marketplace.md` sans le préempter.

## 1. Les deux corpus de la V1

| | Fiches PZ | Ressources non-PZ |
|---|---|---|
| Question du joueur | « Comprendre la grammaire du Jeu » | « Explorer le monde réel au-delà du Jeu » |
| Contenu | ~57 fiches mères (5 familles BAS/LOG/GRA/PAS/SYS), lot pilote de 12 rédigées | 35 fiches existantes : 10 Pensées, 9 Pratiques, 16 Chrysalides |
| Couvertures | Collages 2:3 harmonisés (1024×1536), série en cours (22 faites) | `Carto-*.jpg` déjà en ligne sur WordPress |
| Source | Rédaction interne (livres + corpus) | Import one-off via l'API REST publique WP (vérifiée : produits à prix 0, images et métadonnées accessibles en JSON) |
| Registre visuel | Conte : encart sable, liseret moutarde, collage | Documentaire : fond blanc, cadre gris neutre |

Le principe directeur : **une seule rubrique, deux registres visuels distincts.** Le joueur sait
toujours s'il lit la grammaire du Jeu ou une ressource du monde réel. Pas de grille unique
mélangée.

## 2. La page d'entrée : une devanture, pas un catalogue

`/ressources` est une **bibliothèque à rayons horizontaux scrollables** (motif « étagère »),
un rayon par famille, dans cet ordre :

**La grammaire du Point Zéro** (fiches PZ) — cinq rayons aux noms éditoriaux de la carte :

1. Voir la bascule (BAS)
2. Lire le logiciel invisible (LOG)
3. La grammaire de Conscience (GRA + PUI)
4. Traverser et contribuer (PAS)
5. Habiter les systèmes (SYS)

**Explorer au-delà du Jeu** (non-PZ) — trois rayons : Pensées, Pratiques, Chrysalides.

Pourquoi des rayons et pas une grille :

- la hiérarchie (familles) est donnée sans pagination ni sous-pages ;
- sur mobile, un rayon scrolle au doigt avec ~2,5 couvertures visibles à 375 px —
  l'affordance de scroll est intrinsèque, aucun contrôle à ajouter ;
- **un rayon court a l'air choisi, une grille à moitié vide a l'air inachevée.** La V1
  ouvrira avec 12 fiches PZ rédigées sur ~57 : les rayons absorbent le remplissage
  progressif sans jamais paraître en chantier.

Les couvertures PZ s'affichent comme des **faces de livres** (le 2:3 est un format de
couverture) ; en tête de page, une ligne de voix dans le registre conte installé sur la page
parcours et les chapitres.

## 3. Navigation : trois niveaux, pas plus

1. **Parcourir** : les rayons eux-mêmes.
2. **Filtrer** : une barre légère en tête — filtre par Monde (« Monde 0 » présélectionné pour
   un joueur du Monde 0 : répond à « qu'est-ce qui m'est utile *maintenant* ») + recherche
   texte simple sur titre et promesse.
3. **Rebondir** : chaque fiche liste ses fiches liées (`related` de la carte) et, pour les
   non-PZ, ses « Fiches PZ en résonance ».

Pas de facettes multiples en V1 : 92 fiches au total ne le justifient pas. Les facettes de
`ressourcerie-marketplace.md` (types de nœuds, cinq cadres, territoires…) restent l'horizon.

## 4. La fiche PZ : l'encart de conte, cinq volets

Réutilise le langage visuel des pages de chapitre (encart sable, filet ornemental, lettrine) :

- **couverture 2:3** en tête ou en médaillon ;
- **Éclat** toujours visible : c'est la promesse de la fiche, une idée + une tension ;
- **Repère** : le corps de la fiche (3-6 min de lecture) ;
- **Expérience** : lien vers le mini-jeu ou l'expérience in-app quand elle existe, avec le
  badge « Tu l'as rencontré au Monde 0, dans le Coupable idéal » (données déjà disponibles :
  ChallengesUser du joueur) ;
- **Dossier / Transmission** : volets repliés, ou absents en V1 — jamais un niveau de valeur
  du joueur (principe UX de la carte).

## 5. La fiche non-PZ : gabarit documentaire

Volontairement plus neutre — c'est cette différence de registre qui rend les deux corpus
lisibles :

- image `Carto-*` existante, **pas de nouvelle illustration à produire** ;
- métadonnées en tableau (auteur, année, origine, statut, langues — déjà structurées dans
  les descriptions WP) ;
- lien vers le site de la ressource ;
- « Fiches PZ en résonance » : liste manuelle en V1 (ex. Theory U ↔ GRA-03 Moteur,
  Cercles de parole ↔ PAS-04 cercle-miroir, Analyse Transactionnelle ↔ LOG-04 redécision).

## 6. Implications pour la production des illustrations (Codex)

- **Le 2:3 (1024×1536) est confirmé comme format canonique** des couvertures PZ — il est
  porteur du motif « étagère de livres » de la page d'entrée.
- **Lisibilité à ~140 px de large** (taille d'une couverture en rayon, desktop et mobile) :
  la règle existante « silhouette ou emblème lisible en vignette » est exactement le critère,
  elle devient bloquante.
- **Aucune illustration à produire pour les 35 non-PZ** : les `Carto-*.jpg` existent, et leur
  neutralité documentaire sert la distinction des deux registres.
- Priorité utile : couvrir d'abord le **lot pilote de 12** (BAS-01, BAS-03, BAS-06, BAS-07,
  BAS-09, LOG-01, LOG-03, LOG-05, LOG-08, GRA-03, GRA-05, GRA-08) pour que la V1 ouvre avec
  ses rayons Monde 0–1 complets.

## 7. Post-V1 : les fiches de facilitation (sous-catégories à prévoir)

Précision de Boris (2026-07-29) : la Ressourcerie accueillera aussi les **fiches de
formation à la facilitation des parcours PZ**, complémentaires des fiches théoriques.
La référence de forme est l'ancien ze.game (`Ressources Point Zero/ze.game/ze.game.xlsx`),
dont les onglets « Facilitation - X » constituent des banques de fiches-outils
opérationnelles : Inclusions (~centaines), Gestion de crise, Dynamique collective,
Dynamique individuelle, Générateur de challenges, Cadre de référence, Règles de vie,
Gestion de comportements, Système de jeu, Définitions. Chaque fiche y porte : carte, temps,
mode (présentiel/distanciel), mots-clés, contenu, « quand l'utiliser ? », « comment
l'accompagner ? ».

Conséquence pour l'architecture V1 : **la partie fiches PZ doit prévoir des
sous-catégories** au sein d'une famille. Le motif « rayon par famille » y est déjà prêt
(une future famille « Facilitation » aurait ses propres sous-rayons), mais le modèle de
données V1 doit porter dès le départ un champ de sous-catégorie facultatif plutôt qu'une
famille plate. Ces fiches relèvent de la profondeur **Transmission** de la carte : leur
visibilité sera vraisemblablement conditionnée au rôle (facilitateur), pas publique.

## 8. Hors périmètre V1 (rappel)

Graphe de relations navigable, évaluation par les cinq cadres, marketplace, studio de
création, recommandations personnalisées, fiches de facilitation ci-dessus (post-V1).
Tout cela reste décrit dans `ressourcerie-marketplace.md` et la section 7.
