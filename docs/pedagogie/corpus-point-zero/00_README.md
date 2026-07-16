# Point Zéro — Corpus de référence pour Codex

## Objet du corpus

Ce dossier rassemble l’architecture pédagogique globale élaborée pour l’application Point Zéro. Il doit servir de base de travail à Codex pour :

- modéliser le Moteur de Conscience ;
- structurer les parcours de la Marelle Oméga ;
- construire une bibliothèque d’expériences réutilisables ;
- recommander des déplacements personnalisés ;
- générer des parcours ad hoc lorsque le chemin n’est pas encore balisé ;
- intégrer les verticales civilisationnelles, les organisations et le Commun Point Zéro ;
- créer un Atlas de figures inspirantes et une Assemblée Intérieure personnalisée.

Le corpus décrit une **architecture conceptuelle et fonctionnelle**. Il ne constitue pas encore une spécification psychométrique validée ni un protocole clinique.

## Principe directeur

> Les Puissances indiquent ce qui se transforme. Les états du Moteur indiquent où se situe le joueur. Les déplacements indiquent l’objectif pédagogique. Les Mondes règlent l’intensité. Les verticales indiquent où la transformation s’applique. Le Commun permet de la transmettre et de la faire passer à l’échelle.

## Carte des documents

1. `01_architecture_pedagogique_globale.md` — vision d’ensemble et logique spiralée.
2. `02_moteur_de_conscience.md` — modèle des Puissances, polarités, amplitudes et circulation.
3. `03_archetypes/` — une grille complète par Puissance polaire.
4. `04_marelle_et_progression_des_mondes.md` — répétition des 7 Puissances dans chaque Monde avec intensité croissante.
5. `05_catalogue_parcours_et_experiences.md` — taxonomie des parcours, structure canonique et génération adaptative.
6. `06_verticales_organisations_et_commun.md` — verticales civilisationnelles, Masculin/Féminin, organisations et passage à l’échelle.
7. `07_atlas_figures_et_assemblee_interieure.md` — célébrités, figures mythiques, rôles modèles et avatars composites.
8. `08_specifications_fonctionnelles_application.md` — modules applicatifs, écrans, règles de recommandation et garde-fous.
9. `09_modele_de_donnees.md` — entités, relations et exemples d’objets.
10. `10_backlog_et_questions_ouvertes.md` — décisions à prendre avant industrialisation.
11. `11_evaluation_initiale_moteur.md` — Conseil du Seuil, Appel d’activation, scènes, restitution et garde-fous.
12. `12_mentoring_et_matching_du_moteur.md` — fonctions de mentoring, matching par déplacements et composition des Cercles.
13. `schemas/` — premiers schémas JSON utilisables comme base technique.
14. `assets/` — schémas visuels de référence.

## Conventions centrales

### Les 7 Puissances

- Désir — **JE SUIS**
- Volonté — **JE DÉCIDE**
- Imagination — **JE CRÉE**
- Émotion — **J’AIME**
- Communication — **J’EXPRIME**
- Intuition — **JE CONNAIS**
- Transcendance — **JE DONNE**

### État d’une Puissance polaire

```text
(Puissance, Ombre, Lumière, Maîtrise, Contexte)
```

- Ombre : O1 à O3
- Lumière : L1 à L3
- Maîtrise : `bloque`, `intermediaire`, `libre`
- Contexte : personnel, relationnel, collectif, organisationnel, civilisationnel

### Sens des trois maîtrises

- **Bloqué** : une polarité est refusée, inaccessible ou compulsivement subie.
- **Intermédiaire** : les deux polarités sont reconnues comme visitables, mais le passage dépend encore de ressources complémentaires.
- **Libre** : la personne peut entrer, demeurer, sortir et revenir au Point Zéro de manière intentionnelle et contextualisée.

### Point essentiel

La Source n’est pas une case tiède O0–L0. Elle est la **qualité de circulation consciente** qui peut traverser toute l’amplitude, y compris O3–L3.

## Ordre de travail conseillé pour Codex

1. Implémenter le modèle de données minimal du profil du Moteur.
2. Implémenter le graphe des états et déplacements.
3. Construire l’éditeur d’expériences avec leurs métadonnées de transition.
4. Construire les parcours comme assemblages ordonnés d’expériences.
5. Ajouter le moteur de recommandation déterministe.
6. Ajouter la génération assistée par IA avec validation humaine.
7. Ajouter les figures, rôles modèles et avatars de l’Assemblée Intérieure.
8. Ajouter les preuves, feedbacks et mises à jour progressives du profil.

## Prompt de démarrage possible pour Codex

> Lis l’ensemble du dossier comme une base de connaissances cohérente. Commence par produire un schéma de domaine, une liste d’entités et une architecture modulaire. Ne code pas immédiatement l’interface. Identifie d’abord les invariants, les états, les transitions, les règles de recommandation, les objets versionnés et les zones nécessitant une validation humaine. Utilise les schémas JSON comme brouillons, pas comme contrats définitifs.
