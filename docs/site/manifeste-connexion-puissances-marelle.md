# Manifeste de connexion — Puissances, Marelle et approfondissements

> **Ajout Codex — 2026-08-03.**
>
> Document d'intégration éditoriale destiné à Claude. Il décrit comment raccorder les nouveaux
> contenus au site, aux cinq parcours publics et au corpus historique. Il ne prescrit aucune
> modification du modèle de données ni du code Rails.

## 1. Objectif

Le site doit pouvoir expliquer le Livre II sans exiger d'entrer immédiatement dans le Jeu :

- le **Moteur** donne la grammaire ;
- les **sept Puissances** nomment les fonctions vivantes ;
- les **Cadres** montrent leur traduction collective ;
- la **Marelle** organise leur dépolarisation dans le temps et à plusieurs échelles ;
- les articles appliqués permettent à chaque public de reconnaître un problème concret.

Ces contenus ne constituent pas un second tunnel. Ils forment la bibliothèque profonde vers
laquelle les parcours donnent une boussole.

## 2. Graphe éditorial canonique

```text
Accueil
├── Comprendre
│   ├── Les cinq parcours publics
│   ├── Corpus Livre I conservé
│   └── Comment nous réveiller ?
│       ├── Le Moteur et les sept Puissances
│       ├── La Marelle, un dépolarisateur géant
│       └── Des Puissances aux Cadres
├── Agir
│   ├── Monde 0 dans l'application
│   └── Se dépolariser sans renoncer à ses convictions
└── Porter
    ├── Autodiagnostic projet ou organisation
    ├── Transformations qui reproduisent ce qu'elles combattent
    ├── Chrysalides : la métamorphose interdite
    └── Gouverner une société polarisée
```

## 3. Pages à intégrer

| Route cible | Fichier source | Nature | Emplacement principal | CTA principal |
|---|---|---|---|---|
| `/le-moteur-et-les-sept-puissances/` | `le-moteur-et-les-sept-puissances.md` | canonique | Le Jeu / Comprendre | parcours 5 puis Monde 0 |
| `/la-marelle-depolarisateur-geant/` | `marelle-depolarisateur-geant.md` | canonique | Le Jeu / Agir | Sas puis Monde 0 |
| `/des-puissances-aux-cadres/` | `des-puissances-aux-cadres.md` | canonique | Le Jeu / Porter | autodiagnostic |
| `/ressources/transformations-reproduisent-ce-qu-elles-combattent/` | `article-organisations-transformations.md` | article | Ressourcerie / Organisations | autodiagnostic |
| `/ressources/chrysalides-metamorphose-interdite/` | `article-chrysalides-metamorphose.md` | article | Ressourcerie / Chrysalides | porte Porter |
| `/ressources/se-depolariser-sans-renoncer/` | `article-citoyens-se-depolariser.md` | article | Ressourcerie / Citoyens | parcours 4 |
| `/ressources/gouverner-une-societe-polarisee/` | `article-pouvoirs-publics-polarisation.md` | article | Ressourcerie / Pouvoirs publics | rendez-vous |

Les routes sont des cibles éditoriales. Claude peut les adapter aux conventions de la pile,
mais les URL historiques restent prioritaires lorsqu'une page existante est réellement
remplacée.

## 4. Raccord aux cinq parcours publics

Les parcours restent autosuffisants. Les recommandations finales ouvrent la profondeur sans la
rendre obligatoire.

| Parcours | Recommandation canonique | Approfondissement contextuel |
|---|---|---|
| Qu'arrive-t-il à l'humanité ? | La Marelle, un dépolarisateur géant | corpus des cycles et des dix manifestations |
| Quels sont les scénarios du futur ? | La Marelle, un dépolarisateur géant | pages des 25 scénarios et de l'intercycle |
| Quelles forces ont façonné nos croyances ? | Le Moteur et les sept Puissances | pratico-inerte, récits et croyances |
| Qu'est-ce qui nous paralyse ? | Le Moteur et les sept Puissances | article citoyen ; article organisation selon la porte choisie |
| Comment nous réveiller ? | les trois pages canoniques | article correspondant au public déclaré |

Règle d'affichage : trois recommandations maximum à la fin d'un parcours — une page canonique,
une page profonde du Livre I et une action. Ne pas produire une liste de douze liens qui
retransformerait la boussole en annuaire.

## 5. Raccord au corpus historique

- `/comprendre-question-5/` devient la **page-charnière** : constat du Livre I, aperçu des
  Puissances, puis choix entre les trois pages canoniques.
- `/les-cadres-systemiques/` est conservée et révisée à partir de
  `des-puissances-aux-cadres.md`. Son URL historique est préférable à la création d'un doublon
  si son contenu et son gabarit le permettent.
- La page historique **La métamorphose interdite** reste un article daté. Le nouveau texte peut
  soit la réviser sur place, soit devenir son prolongement actuel ; décider après comparaison
  du corps exporté.
- `/le-point-zero/` conserve sa fonction de définition générale de l'écosystème et renvoie vers
  les trois pages, sans absorber tout leur contenu.
- `recit-la-marelle.md` demeure le récit court et imagé. La page « dépolarisateur géant » est
  son approfondissement conceptuel et appliqué.
- Les pages du Livre I ne sont ni masquées ni supprimées. Les parcours les ordonnent et les
  recommandent.

## 6. Navigation recommandée

### Navigation principale

Ne pas ajouter sept entrées au menu. Conserver les trois portes et les ensembles validés.

Sous **Le Jeu**, créer un hub léger :

1. Le Point Zéro ;
2. Le Moteur et les sept Puissances ;
3. La Marelle ;
4. Les Cadres et les Cercles ;
5. L'économie Oméga.

Sous **Ressourcerie**, ajouter des filtres éditoriaux non exclusifs : `Citoyens`,
`Organisations`, `Chrysalides`, `Pouvoirs publics`, en plus des catégories de ressources.

### Navigation contextuelle

Chaque page canonique comporte :

- un fil d'Ariane ;
- une carte « avant / après » vers les deux autres pages canoniques ;
- au plus deux articles appliqués ;
- un seul CTA primaire, choisi selon la porte d'entrée du visiteur.

Le contexte de porte peut être conservé en session ou dans l'URL. Il personnalise le CTA, pas
la doctrine ni le contenu canonique.

## 7. Composant visuel commun

Prévoir un composant interactif sobre permettant de changer d'échelle :

**Moi → Cercle → Organisation → Projet → Société**.

À chaque échelle, il affiche :

- une tension concrète ;
- la Puissance concernée ;
- le Cadre collectif lorsqu'il s'applique ;
- un exemple d'expérience ;
- le lien vers l'approfondissement pertinent.

Sur mobile, une seule échelle est ouverte à la fois. Le composant ne calcule aucun « niveau de
conscience » et ne prétend pas établir un diagnostic personnel à partir de quelques clics.

## 8. Règles éditoriales et fonctionnelles

1. Définir immédiatement la dépolarisation : ni neutralité, ni centrisme, ni relativisme.
2. Conserver exactement les cinq correspondances Puissance–Cadre.
3. Présenter Désir comme Racine et Transcendance comme Couronne, jamais comme deux Cadres de plus.
4. Ne publier aucune correspondance entre les cinq lectures du site et les Mondes de la Marelle.
5. Ne pas exposer la cosmogonie sur le site public.
6. Ne pas employer les diagnostics pour classer des personnes ou conditionner des droits.
7. Distinguer contenu `Actif`, dispositif `Expérimental` et horizon annoncé.
8. Conserver les URL historiques dès qu'elles portent déjà une intention équivalente.
9. Centraliser les relations « contenu lié » dans une configuration éditoriale afin d'éviter
   les cartes dupliquées et les liens divergents.
10. Les parcours publics peuvent mémoriser localement leur complétion ; les traces personnelles
    durables et les contributions restent dans l'application, avec information et consentement.

## 9. Critères d'acceptation pour Claude

- Les sept nouveaux contenus sont accessibles depuis un hub ou une recommandation, sans être
  tous injectés dans le menu principal.
- La fin du parcours 5 propose les trois pages canoniques et un CTA adapté à la porte choisie.
- Les autres parcours recommandent au maximum trois suites pertinentes.
- Les pages restent lisibles sans connaître le vocabulaire du Point Zéro.
- Les correspondances Puissance–Cadre sont exactes partout.
- « Dépolariser » est explicité avant toute promesse d'application.
- Les liens vers le corpus historique conservent les URL existantes ou disposent d'une
  redirection documentée.
- La vue mobile ne présente pas plus d'une idée principale et d'un CTA primaire par écran.
- Aucun score automatique de conscience individuelle, collective ou civique n'est introduit.

## 10. Ordre d'intégration recommandé

1. intégrer les trois pages canoniques et leur navigation croisée ;
2. raccorder la sortie du parcours 5 ;
3. ajouter les recommandations aux quatre autres parcours ;
4. intégrer les quatre articles appliqués ;
5. réviser `/comprendre-question-5/` et `/les-cadres-systemiques/` sur leurs URL historiques ;
6. prototyper ensuite le composant multi-échelle, sans bloquer la publication des textes.
