# Corpus joueur des guides Point Zéro

> Ajout Codex — 2026-08-15. Premier lot éditorial destiné au Professeur Sirbey et au
> Docteur Z.E.R.O. Ce dossier ne donne aucun accès applicatif aux guides et ne constitue pas
> un prompt système prêt à mettre en production sans les garde-fous de
> [`politique-de-reponse.md`](politique-de-reponse.md).

## Objet

Ce corpus permet aux deux guides transversaux de répondre aux questions sur :

- le Point Zéro et sa grammaire ;
- le Monde actuellement accessible au Joueur ;
- la page courante et les fonctionnalités déjà dévoilées ;
- les notions nécessaires pour comprendre l'action proposée ;
- les limites du guide et les recours humains disponibles.

Les guides partagent **les mêmes faits, les mêmes sources, les mêmes permissions et la même
mémoire de conversation**. Seule leur opération rhétorique diffère :

- le **Professeur Sirbey** distingue, relie et cartographie ;
- le **Docteur Z.E.R.O.** enquête sur les contradictions et réintègre la qualité captive
  derrière ce qu'il met en cause.

Le choix d'un guide ne doit jamais produire deux vérités.

## Statut du lot

Le premier lot comprend :

1. un [schéma éditorial](schema-fiche.md) ;
2. un [registre hiérarchisé des sources](registre-sources.md) ;
3. une [politique de réponse et de sécurité](politique-de-reponse.md) ;
4. la [voix du Professeur Sirbey](voix-professeur-sirbey.md) ;
5. la [voix du Docteur Z.E.R.O.](voix-docteur-zero.md) ;
6. trente [fiches canoniques du Monde 0](monde-0/fiches.md) ;
7. vingt-et-une [fiches du Monde 1](monde-1/fiches.md), dont les fonctions non livrées sont
   explicitement marquées `horizon` ou `hypothese` ;
8. un [`manifest.yml`](manifest.yml) destiné au filtrage déterministe ;
9. un [banc éditorial](banc-editorial.md) de vingt scénarios ordinaires, limites et sensibles.

## Règle de priorité

En cas de contradiction :

1. une fiche joueur validée et datée prévaut pour la réponse au Joueur ;
2. une décision canonique récente de `docs/vision/` prévaut sur le corpus pédagogique
   candidat ;
3. les livres fondent la doctrine, mais une évolution explicitement actée dans la vision
   produit prévaut pour le fonctionnement actuel du Jeu ;
4. les articles, capsules et spectacles nourrissent l'explication et la voix, sans pouvoir
   modifier seuls une règle du Jeu ;
5. une hypothèse est toujours présentée comme une hypothèse.

Le corpus joueur ne doit jamais être construit en indexant directement tout `docs/vision/`.
Ce dossier contient des arbitrages internes, des fonctions non livrées et des révélations
réservées aux Mondes avancés.

## Sélection au moment d'une question

Le serveur sélectionne les fiches à partir de valeurs énumérées et contrôlées :

```text
Monde du Joueur
+ destination ou page courante
+ droits applicatifs
+ question
→ fiches accessibles et pertinentes
→ réponse dans la voix choisie
→ sources citées
```

Le nom, l'adresse, le profil du Moteur, les Graines, les Traces et les conversations privées
ne sont pas nécessaires pour répondre sur le Point Zéro ou l'interface. Ils ne doivent pas
être joints à l'appel.

## Conventions d'écriture

- Tutoyer le Joueur, comme le reste du Jeu.
- Répondre d'abord à la question posée, en deux à cinq paragraphes courts.
- Distinguer `canonique`, `hypothèse`, `horizon` et `récit symbolique`.
- Citer une ou plusieurs fiches utilisées.
- Citer les sources par leur **titre public lisible uniquement** : aucun chemin de dépôt,
  nom de fichier ou ancre interne ne doit entrer dans le prompt assemblé ni dans la réponse.
- Ne jamais diagnostiquer une personne, une organisation ou une Puissance.
- Ne jamais transformer une métaphore cosmologique en fait scientifique.
- Ne jamais annoncer une fonctionnalité non accessible comme si elle existait déjà.
- Proposer au maximum une prochaine action pertinente.
- Dire `je ne sais pas` lorsque le corpus ne permet pas de répondre.

## Cycle éditorial

Une fiche est proposée par un humain ou un agent, relue par Boris, puis versionnée dans Git.
La validation porte séparément sur :

- le fond ;
- le niveau de dévoilement ;
- les sources ;
- les formulations interdites ;
- les exemples de voix.

Une modification doctrinale ne doit pas être propagée silencieusement. Elle entraîne une
nouvelle revue des fiches liées par le manifeste.

Le registre interne conserve les chemins utiles à la maintenance. Les lignes `Sources` des
fiches joueur, elles, constituent l'export citable : elles ne portent volontairement que des
titres.

### Compatibilité du chargeur

Le manifeste v2 conserve `records_file: monde-0/fiches.md` pour ne pas casser le chargeur du
palier 1 déjà livré. Le nouveau tableau `records_files` est la source canonique multi-Mondes.
Avant d'exposer le corpus M1, le chargeur Rails doit parcourir ce tableau, vérifier que chaque
section possède une entrée de manifeste et filtrer ensuite par `min_world`. Ignorer le tableau
revient à conserver volontairement le seul corpus M0 ; ce n'est pas une erreur silencieuse à
masquer dans la vue.
