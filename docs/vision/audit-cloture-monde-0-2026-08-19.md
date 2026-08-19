# Audit de clôture du Monde 0 — 19 août 2026

> **Objet.** Distinguer ce qui empêche réellement de considérer le Monde 0 comme bouclé de
> ce qui relève déjà du Monde 1, d'un enrichissement éditorial ou d'un horizon. Cet audit
> actualise le bilan du 16 août à partir de `pointzero-app/origin/main` (`d158ba6`), des
> livraisons signalées dans les boîtes d'agents et des décisions éditoriales déjà actées.
> Il ne vaut pas recette de production connectée : les deux PR de messagerie encore en
> transit doivent être fusionnées, déployées et regardées sur le serveur de travail.

## 1. Verdict

Le **socle fonctionnel du Monde 0 est désormais presque complet** : coque et métaparcours des
sept Puissances, parcours obligatoire, Immateria, Fresque, registre des Traces, six Héros et
mentor, Guides, Ressourcerie, Moteur, Omégas, Accomplissements, profil communautaire et premier
Espace d'échange ont tous une implémentation réelle.

Il reste **deux conditions de clôture produit** :

1. résoudre la contradiction encore visible entre **Fresque, Trace et Graine** ;
2. achever la promotion et la recette des deux derniers gestes de la messagerie M0.

Le reste peut être traité après le gel du Monde 0 sans rendre son parcours incohérent.

## 2. Matrice de clôture

| Zone | État actuel | Verdict M0 | Action restante |
|---|---|---:|---|
| Accueil et roue des sept Puissances | sept cartes reliées à des sources réelles par `Monde0Etats`, deux états de base et destinations incrémentales | **Vert** | recette transversale finale des routes et du responsive |
| Désir / Immateria | jeu servi par Rails, tutoriel, Trace idempotente, retour vers le Jeu | **Vert M0** | le résumé vivant de l'avatar reste reporté avec le contrat Immateria |
| Volonté / parcours | progression structurelle, expériences requises, intensité/effet/puissance éditorialisés, rite facilitateur séparé | **Vert** | rejouer le banc complet après les dernières promotions |
| Imagination / Traces | registre canonique par familles, relecture et retours d'expérience | **Vert** | conserver la page comme registre ; aucun bouton de conversion directe |
| Imagination / Fresque | vraies Graines relues et publiables, mais le rituel « Planter ma première Graine » crée encore une Trace | **Rouge** | porter l'arbitrage du 16 août : le rituel et la saisie libre doivent créer une vraie Graine |
| Émotion / Héros et mentor | six figures M0, choix réversible, fiche, trois Puissances, lemniscate, mentor Claude et mémoire consentie | **Vert M0** | `parcours_associes` vide pour les 48 figures : enrichissement éditorial, non bloquant pour traverser M0 |
| Communication / Guides | deux voix, fil privé continu, suppression et centre de personnalisation | **Vert** | reprendre dans Rails les trois corrections de vérité de la maquette `57960b3` si nécessaire |
| Communication / Espace d'échange | canal M0, profils, réactions, réponses et échange individuel consentis | **Orange** | fusionner/recetter les PR de fin de lot, puis promouvoir |
| Partage d'une Graine | service et droits réels en production ; contrôle d'interface livré en PR | **Orange** | semer une Graine dans le décor, regarder le geste, fusionner et promouvoir la PR |
| Intuition / Point Zéro | dix fiches, lecture avant questionnaire, questionnaire vers Trace, événements | **Vert** | recette des états vide/erreur et des liens de retour |
| Transcendance / Moteur | six évaluations, lemniscates, caps et pages détaillées | **Vert avec mention** | garder les lectures « provisoires » ; ne pas présenter l'alchimisation comme une mesure scientifique |
| Accomplissements | badges de parcours calculés depuis les expériences requises, seuils, visibilité par catégorie | **Vert** | vérifier le respect effectif des deux préférences sur le profil communautaire |
| Omégas M0 | total unique et ventilation par Puissance ; aucune fongibilité ni Fonds anticipé | **Vert** | aucun objectif « un million » ni capacité de financement avant M1 |
| Compte, CGU, personnalisation | compte, sécurité, CGU projet, centre d'autorisations et suppression | **Vert fonctionnel** | validation juridique finale séparée ; aucune 2FA ou liste d'appareils exigée pour M0 |

## 3. Les deux chantiers bloquants

### 3.1. Fermer le contrat Fresque → Graine

La décision canonique est déjà écrite dans
[`pont-trace-graine-fresque.md`](pont-trace-graine-fresque.md) :

- le rituel des quatre questions de la Fresque crée la première **Graine** ;
- les Graines suivantes peuvent naître d'une saisie libre ;
- une Trace ne se convertit jamais par un bouton dans `Mes Traces` ;
- la cristallisation d'une Trace se fait avec le mentor dans un parcours.

Le code courant conserve pourtant `POST /fresque/bifurquer` vers une Trace, tout en affichant
« Planter ma première Graine ». C'est le seul endroit du Monde 0 où un CTA central promet encore
un objet différent de celui qu'il produit. Il faut donc choisir un conteneur canonique pour la
Graine née hors expérience, introduire l'écriture correspondante dans le service `Graine`, puis
faire suivre vue et banc dans la même livraison.

### 3.2. Fermer le lot Communication

Deux livraisons sont encore en transit au moment de l'audit :

- correction des transformations mortes sur un canal ne permettant pas les actions avancées ;
- contrôle de partage d'une Graine vers un Espace autorisé.

La fermeture demande : fusion sur `preprod`, décor avec une vraie Graine, contrôle navigateur
desktop/mobile, bancs, promotion sur `main`, puis purge du décor de démonstration. Aucun nouveau
concept de messagerie n'est requis pour M0.

## 4. Contrôles de sortie

Le Monde 0 peut être déclaré bouclé lorsque les contrôles suivants sont tous vrais :

1. chaque carte de l'accueil ouvre une route réelle et revient dans la coque ;
2. chaque expérience requise possède une action, une preuve et une autorité de validation ;
3. l'expérience d'intensité 4 ou 5 est impossible avant le Monde 2 ;
4. une Graine créée depuis la Fresque apparaît immédiatement dans la Fresque ;
5. une Trace reste une Trace et ne promet aucune conversion automatique ;
6. publier sur son profil et partager dans un Espace restent deux gestes distincts ;
7. le canal M0 ne montre ni sondage, ni Proposition, ni Action, ni Décision, ni financement ;
8. le profil communautaire respecte les préférences de visibilité des badges, Graines et Traces ;
9. les Omégas n'affichent ni dépense, ni transfert, ni million, ni Fonds au Monde 0 ;
10. le passage au Monde 1 dépend de l'accomplissement structurel du parcours obligatoire et du
    rite validé, jamais d'un seuil d'Omégas ;
11. les bancs Monde 0 et une recette navigateur desktop/mobile passent sur la même révision ;
12. préproduction et production servent cette même révision, sans changement non promu.

## 5. Hors blocage, à reprendre après le Monde 0

- remplir `parcours_associes` pour les 48 Héros ;
- définir le contrat d'activité d'Immateria et son résumé vivant ;
- finaliser la formule versionnée d'alchimisation et sa doctrine d'interprétation ;
- enrichir les notifications et le digest ;
- ouvrir Freeride, Cercles, Résonances structurées et outils d'action selon leur Monde ;
- faire valider juridiquement CGU, politique de conservation et mentions de traitements.

## 6. Répartition immédiate recommandée

| Acteur | Prochain geste |
|---|---|
| Portable | fusionner, déployer et recetter les deux PR Communication ; préparer le contrat technique Fresque → Graine |
| Poste fixe | regarder les gestes réels sur le décor, desktop/mobile, puis rendre un verdict de promotion |
| Codex | maintenir la matrice de clôture, vérifier les écarts éditoriaux et traiter ensuite les parcours associés des Héros |
| Boris | aucun nouvel arbitrage nécessaire pour fermer M0 ; la décision Fresque → Graine existe déjà |

