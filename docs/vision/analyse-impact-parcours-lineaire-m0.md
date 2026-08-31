# Analyse d'impact serveur — le parcours linéaire du Monde 0

> **Portable, 31 août 2026.** Réponse à
> [`monde-0-parcours-lineaire-appropriation.md`](../pedagogie/monde-0-parcours-lineaire-appropriation.md)
> (Codex, 31 août), qui demande que la séquence soit « confrontée aux listeners réels ».
> Tout ce qui suit est **mesuré** sur `pointzero-app` (préprod, commit `1902114`), pas déduit
> des souvenirs. Aucune ligne de code n'est modifiée par ce document.

## 1. La bonne nouvelle, et elle est structurelle

**Le verrou linéaire existe déjà, mot pour mot.** `Journey#locked_challenge_ids_for` implémente
exactement la règle du §1 : « la première expérience non franchie est ouverte, les suivantes
sont verrouillées ; une expérience est franchie si elle est validée, OU si elle est optionnelle
ET explicitement passée ». Et le parcours M0 est **déjà en `progression_mode: lineaire`** —
mesuré en base. La colonne vertébrale demandée n'est pas à construire : elle porte déjà les
14 expériences existantes, dont 2 optionnelles.

Ce qui change n'est donc **pas le moteur de progression**. C'est :

1. la **source d'activation des Puissances** (aujourd'hui : des lectures de visites ;
   demain : la validation d'expériences) ;
2. l'**accueil** (aujourd'hui : sept cartes ; demain : la vue du parcours) — zone poste fixe ;
3. **cinq expériences nouvelles** et un passage terminal ;
4. la **garde des fonctions non dévoilées**.

## 2. La matrice, listener par listener

Codex demande la confrontation aux listeners réels. La voici — colonne « source de vérité
attendue » contre ce que la base et le code portent aujourd'hui :

| # | Expérience | Source attendue | Mesuré | Verdict |
|---:|---|---|---|---|
| 1 | Façonner mon jumeau | jumeau persisté + **événement de fin du tutoriel** | la Trace `desir/immateria` fusionne les POSTs du jeu ; **aucun événement de fin n'existe** | ⚠️ **MANQUE** — l'arbitrage §9.4 de Codex est confirmé côté serveur |
| 2 | Entrer dans le Jeu | questionnaire + Trace de l'Hypothèse | `experience_quiz_attempts` + `traces` | ✓ |
| 3 | Le Coupable idéal | session + verdict en Trace | `coupable_ideal_sessions` (verdict dans `result`) | ✓ |
| 4 | Une drôle d'époque | mini-jeu achevé + résultat | `moteur_assessments.completed_at` | ✓ |
| 5 | Avant le Zéro | fin atteinte + devenir enregistré | `traversees` porte **`fin_id` + `completed_at`** | ✓ — le devenir EST enregistré ; sa présentation en Trace est un autre chantier (registre) |
| 6 | Et moi dans tout ça ? | Graine de l'Appel réellement créée | `Graine.semer!` (flux du 24 août) | ✓ |
| 7 | Choisir qui marchera à mes côtés | mentor choisi + messages persistés | `User#choisir_heros!` (`heros_slug`, réversible) + `mentor_messages` | ✓ — les DEUX listeners existent ; l'expérience est de l'orchestration |
| 8 | L'écosystème | dispositif + Schéma en Trace | `experience_quiz_attempts` | ✓ |
| 9 | Choisir ma place | profil confirmé + appartenance + réaction | profil (`users`), `espace_memberships`, `reactions_semantiques` | ✓ — trois listeners existants, aucune table neuve |
| 10 | Le site du Point Zéro | ≥ 1 `TraceSas` + compteur X/5 | `TraceSas` + import ; le compteur est une lecture | ✓ |
| 11 | Le signe de reconnaissance | dispositif + choix de destination | `experience_quiz_attempts` | ✓ |
| 12 | Choisir un double regard | échange Guide + clé éprouvée + Trace | `guide_conversations`/`guide_messages` + `ClesMonde0` | ✓ |
| 13 | Les choses se précisent | Graine de relation | `Graine` | ✓ |
| 14 | Lire mon Moteur | évaluation de Puissance + lecture guidée | `puissance_assessments` ; « lecture guidée achevée » n'a **pas de listener** — c'est une visite | ⚠️ à préciser : si la lecture guidée doit compter, il lui faut un marqueur (comme `onboarding-initial`) |
| 15 | Le Conseil Oméga | Conseil achevé + caps conservés | `conseil_sessions` (`answers`, `engagement`) | ✓ |
| 16 | Découvrir les formats | Boussole en Trace | `experience_quiz_attempts` | ✓ |
| 17 | Participer à un Sas | inscription ou présence + intention | `inscription_creneaux` | ✓ |
| 18 | Vivre l'Atelier | inscription confirmée OU présence validée | **les deux listeners existent** : `inscription_creneaux` ET `emargement_ateliers` | ✓ — l'arbitrage §9.3 est un CHOIX entre deux existants, pas une construction |
| 19 | Mon récit de passage | Graine + Carte du Seuil + visibilité | existants | ✓ |
| 20 | Ton espace est prêt | **confirmation idempotente de clôture** | `Journey#completed_by?` LIT l'achèvement, mais le **choix explicite** n'a aucun support | ⚠️ **MANQUE** — voir §4.2 |

**Bilan : 16 sur 20 sont entièrement portées par des listeners existants.** Les quatre points
ouverts sont : l'événement de fin de tutoriel Immateria (#1), la « lecture guidée » du Moteur
(#14), le geste de clôture (#20) — et l'économie Ω des cinq nouvelles (§9.1 de Codex).

## 3. Ce que « le métaparcours disparaît » emporte, mesuré

Le métaparcours n'est pas une vue : c'est un système. Son démontage touche :

- **`Monde0Etats`** (256 lignes) — dérive l'état des sept territoires depuis les visites,
  marqueurs, traces. **25 lecteurs**, dont 13 dans `app/` : `SeuilFranchi`, `Graine`,
  `VentilationOmega`, `CentreDePersonnalisation`, `MarqueDeVisite`, `Monde1HomeState`, la coque,
  l'accueil. Il ne disparaît pas : **sa règle de dérivation change** — « actif = visité » devient
  « actif = l'expérience d'activation est validée ». La doctrine tient : l'activation reste une
  **lecture** (de `challenges_users`), rien à stocker.
- **`SequenceDeGestes`** (358 lignes, 8 lecteurs) — les cartes `invitation → découverte →
  appropriation`. C'est lui que le §5 absorbe. Codex écrit : « leurs marqueurs peuvent survivre
  comme événements de compatibilité » — c'est la bonne prudence : les marqueurs `m0-visite-*`
  restent en base et en lecture, seul le PILOTAGE s'éteint.
- **`SeuilFranchi`** — dérive les badges du métaparcours (`config/seuils.yml`, sept entrées à
  `puissance`). Le §5 en garde deux (`Présence choisie`, `Première clé de discernement`) et en
  supprime le principe pour les autres. À rejouer contre le catalogue.
- **`config/monde_0.yml`** — 7 cartes de territoires. Devient la configuration de la feuille
  `Puissances` (§7), pas une suppression.
- **Bancs : 39 scripts** touchent le vocabulaire territoires/accueil/Monde0Etats. Trois lisent
  le `power-deck` directement. C'est le plus gros poste de travail après les vues.

## 4. Les deux vrais manques, et la forme que je propose

### 4.1 L'événement de fin du tutoriel Immateria (exp 1)

Immateria POSTe ses données au fil du parcours, fusionnées dans UNE Trace — « une Trace est un
état, pas un journal » (arbitrage du 15 août). Aucun POST ne dit « le tutoriel est fini ».
Le contrat à demander au front Phaser : **un POST idempotent de fin**, que le contrôleur
traduit en validation de l'expérience 1. Une clé dans la Trace existante suffit
(`tutoriel_termine: true`) — pas de table neuve. C'est l'arbitrage §9.4 de Codex, confirmé.

### 4.2 Le geste de clôture (exp 20)

« Choisir explicitement d'ouvrir son espace » est un **choix**, pas un état dérivable — comme
`aide_vue`, comme `onboarding-initial`. Le support le plus simple et le plus conforme à
l'existant : un `MarqueurDAttention` (`m0-cloture` ou équivalent), posé par un POST idempotent.
`HomeController` lirait : clôture posée → tableau de bord ; sinon → vue du parcours. Aucune
migration.

**Attention au point de bascule Monde 1** : aujourd'hui `Mondes.ouvert?` lit
`mandatory_completed_by?`. Si la clôture explicite devient LA porte du M1, c'est un changement
de règle d'accès — à trancher explicitement (le §1 dit « avant de transformer l'accueil », pas
« avant d'ouvrir le M1 »). Je recommande de garder `mandatory_completed_by?` pour le M1 et de
réserver le marqueur au tableau de bord : deux questions, deux réponses.

## 5. La garde des fonctions non dévoilées (§6.4)

« Avant leur expérience d'activation, absentes des liens et sous-menus » — les liens sont au
poste fixe ; la **garde d'URL** est à moi. Aujourd'hui `verrouille_par_la_coque` ne protège que
3 contrôleurs, et `Coque.etat` dérive de `Monde0Etats`. Le chantier : brancher `Coque.etat` sur
la nouvelle dérivation (validation d'expériences), étendre la garde aux contrôleurs des
fonctions dévoilables (Fresque, Guides, Moteur, Échanges, Annuaire, Accomplissements…), et
servir la page « Reprendre mon passage » comme réponse de refus — un gabarit, pas une redirection
muette. La leçon de l'annuaire du 30 août s'applique ici en sens inverse : **la garde et la
liste doivent dériver de la même règle**, sinon on refabrique « une porte offerte puis refermée ».

## 6. Cinq expériences nouvelles : des données, pas des tables

Les expériences 1, 7, 9, 12, 14 sont **de l'orchestration de listeners existants** : cinq
`Challenge` neufs (des lignes, pas des colonnes), leurs textes, leurs positions dans le
parcours, et pour chacune un adaptateur de validation (le patron des expériences existantes).
Il faudra leur donner `total_point` et des skills pour que `Point` valide — c'est l'économie Ω
du §9.1, **arbitrage de Boris**. Aucune migration de schéma identifiée à ce stade.

## 7. Ordre de livraison que je recommande (zone portable)

1. **Le contrat Immateria** (4.1) — c'est le seul point qui dépend d'un tiers (le front
   Phaser) ; le demander tôt.
2. **La dérivation d'activation** dans `Monde0Etats` — nouvelle règle, anciens lecteurs,
   énorme couverture de bancs à faire suivre *dans la même livraison*.
3. **Les cinq Challenges neufs + adaptateurs**, à Ω = 0 tant que Boris n'a pas chiffré —
   afficher « à chiffrer » plutôt qu'un faux montant.
4. **La garde d'URL généralisée** + page « Reprendre mon passage ».
5. **Le marqueur de clôture** et la bascule accueil/tableau de bord (avec le poste fixe).
6. La **promotion seulement après** que la maquette des cinq états (§10 de Codex) soit portée —
   ce chantier ne se livre pas en tranches visibles par les joueurs de production.

## 8. Risques nommés

- **La fenêtre de bascule** : entre la nouvelle dérivation et les nouvelles expériences, un
  joueur existant du M0 (25 comptes en production, dont des réels) ne doit pas voir ses
  Puissances « se désactiver ». Règle de compatibilité à écrire : activé si l'ancienne
  dérivation OU la nouvelle le dit — puis retrait de l'ancienne quand les données ont migré.
- **`m0-visite-m0.transcendance.moteur` est posé par la page de PROFIL** (`UsersController#show`)
  — mesuré le 30 août sur un compte réel. Dans le nouveau modèle, le Moteur ne s'ouvre qu'à
  l'expérience 14 : cette incohérence (§6.2 de Codex) disparaît d'elle-même avec la nouvelle
  dérivation, mais le marqueur mal nommé restera en base ; ne pas s'en servir comme preuve.
- **39 bancs** à faire suivre. Les bancs ciblés ne suffiront pas — deux fois cette semaine la
  recette complète a vu ce qu'ils ne voyaient pas. Prévoir une passe complète par étape.
- **L'onboarding sort vers Immateria** (prologue) : une ligne dans la vue du poste fixe, mais
  `verifier_onboarding` asserte la sortie actuelle vers `/jeu` — à faire suivre ensemble.

## 9. Ce que ce document ne tranche pas

Les six arbitrages du §9 de Codex restent ouverts et sont à Boris/Codex. Ce document y ajoute
deux questions serveur : la « lecture guidée » de l'expérience 14 (visite marquée ou vrai
geste ?), et la séparation clôture-tableau-de-bord / porte-du-Monde-1 (§4.2).
