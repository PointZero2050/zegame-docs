# Plan de développement général — v2, paliers par Monde jusqu'à décembre 2026

<!-- [Claude] v1 le 2026-08-10 (horizons). v2 le 2026-08-11, demande Boris : distribution
     de la charge entre les trois agents (l'instance desktop reçoit des modules de
     développement), objectif « coque fonctionnelle » fin décembre 2026, premier palier au
     Festival, priorité Monde 0 > Monde 1 > Monde 2, modèle Claude par sprint. -->

**Objectif.** Une **coque fonctionnelle fin décembre 2026** : la navigation cible réelle
(grammaire du dévoilement validée le 11 août) portée en Rails, chaque destination existant
dans l'un des quatre états du contrat (`invisible / annoncée / lecture / ouverte`), les
Mondes 0 et 1 pleinement jouables, le Monde 2 amorcé. Premier palier au **Festival du
1er octobre** — le [plan Festival](plan-developpement-vers-festival.md) reste la loi de ses
trois premiers sprints ; rien ne passe devant son chemin critique.

**Règle de priorité.** Le Monde 0 prime sur le Monde 1, qui prime sur le Monde 2, etc. Un
module du Monde N+1 ne mobilise personne tant qu'un module du Monde N attendu au même
palier n'est pas tenu — à l'exception des pages de teasing, qui sont précisément la manière
canonique d'exister avant d'ouvrir.

**Les dates sont des bornes, pas un rythme** *(précision Boris, 2026-08-11)*. En pratique,
le travail avance autant que possible dès août : il est très possible d'être fortement en
avance sur le calendrier annoncé. Ce qui fait foi dans ce plan, c'est **l'ordre des
sprints** (un sprint = un lot de dépendances satisfaites, pas quinze jours) et **le graphe
des dépendances fonctionnelles** (§4). Un sprint s'ouvre dès que le précédent est tenu et
que ses préalables sont livrés — si c'est trois jours après, tant mieux. Les dates du §3
sont donc des bornes AU PLUS TARD, garanties par les paliers ; seules deux contraintes
restent calendaires par nature : le Festival du 1er octobre et son gel du 15 septembre.

---

## 1. Amendement à la répartition — l'instance desktop développe des modules

*(Décision Boris, 2026-08-11 — étend l'accord de phase 2 du 2026-08-04.)*

L'instance Claude desktop (poste fixe) était sous-sollicitée : éditorial, site, Sas,
relecture. Elle a pourtant fait ses preuves au-delà (import WordPress, catégories et
`phare` sur le modèle Event, DA v4 — dix commits relus et promus sans reprise entre le 8 et
le 10 août). Elle reçoit désormais **des modules applicatifs à développer**, dans un cadre
qui préserve l'invariant « celui qui produit ne s'auto-valide pas » :

| Règle | Détail |
|---|---|
| **Un module = un périmètre borné** | vues, contrôleurs, CSS/JS et contenus du module, dans son namespace (`app/views/<module>/`, `<module>_controller.rb`) — un seul agent par zone, comme toujours |
| **Les fondations restent au portable** | modèles, migrations, règles de droits, routes sensibles, jobs, config serveur. Quand un module du desktop a besoin d'une donnée, le portable livre D'ABORD le modèle et son contrat d'accès (le patron `ContexteDeFil`/`Carte`) ; le module le consomme |
| **Livraison sur `preprod`** | commits `[Claude]` du poste fixe, sa clé SSH, son périmètre serveur inchangé (jamais `~/deploy/`, jamais la prod) |
| **Assemblage par le portable** | relecture, banc de vérification (l'app des bancs négatifs vaut pour tous), branchement dans la coque, promotion en production |
| **Codex reste hors du code Rails** | maquettes, specs, corpus éditorial, revues — le processus en trois temps (revue Claude → corrections Boris → consolidation Codex) s'applique à chaque module avant son ouverture réelle |

## 2. Les paliers

| Palier | Date | Contenu | Critère de sortie |
|---|---|---|---|
| **P1 — Festival** | 1er octobre | Monde 0 + billetterie + jour J (périmètre du plan Festival) | un participant réel traverse billet → Sas → Monde 0 → ateliers → après-Festival sans assistance |
| **P2 — Coque réelle, Monde 0 complet** | fin octobre | la navigation du dévoilement portée en Rails ; toutes les destinations en teasing ou mieux ; Monde 0 entièrement servi dedans ; guides LLM v1 | un joueur Monde 0 ne voit QUE son Monde, et chaque porte fermée explique ce qu'elle ouvrira |
| **P3 — Monde 1 complet** | fin novembre | Cercles autofacilités au complet dans la coque, messagerie étape B (composeur +, Actions/Décisions/Mémoire), agenda, annuaire enrichi, profil unifié | un Cercle pilote fonctionne sans WhatsApp ni outil externe, décisions et mémoire comprises |
| **P4 — Coque fonctionnelle, Monde 2 amorcé** | fin décembre | Freeride + ligne de jeu, héros & mentors v1, préférences d'attention, recherche globale ; tout le reste `annoncée`/`lecture` avec sa vraie page | les cinq portes sont réelles à tous les Mondes ; aucun bouton mort ; bancs verts sur l'ensemble |

Ce qui n'est PAS dans ces paliers (donc pas en 2026, sauf décision contraire) : économie
Ω transactionnelle, reconnaissance rituelle, gouvernance du Commun, place de marché
juridiquement ouverte, académie/habilitations, organisations, monde-miroir, épreuve des
runes. Ils existeront fin décembre **en pages d'annonce ou en lecture**, conformément au
contrat de coque — c'est une existence honnête, pas une absence.

## 3. Les sprints (deux semaines) — qui, quoi, quel modèle

Les modèles suivent la doctrine : Sonnet 5 par défaut, **Opus 5 / Fable 5** pour
l'architecture et les droits, Haiku 4.5 pour le mécanique. Codex n'est pas un modèle
Claude ; ses tâches n'en portent pas.

### Sprint 1 · 12-25 août — « La vente ouvre » *(palier P1)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | Rotation Stripe + test de paiement bout-en-bout ; appui à Boris pour publier/cocher phare/composer la journée ; **R6a** (les Échanges nommés sur l'accueil du Jeu) ; import WhatsApp si l'export arrive | Sonnet 5 (Fable 5 pour l'import WhatsApp) |
| Desktop | Monde 0 éditorial + finalisation Sas v2 ; **premier module dev : les pages de teasing** (gabarit « ce que c'est, ce qu'on y fera, ce qui l'ouvre » — vues pures, zéro droit, la brique de base du dévoilement) | Sonnet 5 |
| Codex | **R11 faite et arbitrée** ; **trois configurations de barre mobile R6b produites** ; **traversée Festival R2 produite** — arbitrages Boris R6b/R2 en attente | — |
| Boris | Arbitrages Festival vague 0 ; catégories de périmètre §8 | — |

### Sprint 2 · 26 août - 8 sept — « Le jour J est prêt »

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | Rejouer `repetition_50` sur la vraie journée ; QR `festival-lier` ; mode opératoire DNS répété à blanc ; correctifs de la répétition | Sonnet 5 (Opus 5 pour la bascule DNS) |
| Desktop | Module **Aide & recours v1** (numéros d'urgence avant connexion, orientation, personnes ressources — contenu et vues ; le signalement/blocage EXISTE déjà côté portable, il le branche) | Sonnet 5 |
| Codex | **R10** matrice droits × états des modules Festival ; consolidation post-arbitrages de Boris (3e temps) | — |

### Sprint 3 · 9-22 sept — « Gel et répétition générale » *(gel le 15)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | Stabilisation, bancs complets, répétition générale, checklist feu vert, astreinte | Sonnet 5 |
| Desktop | Recette utilisateur complète en préprod (peau de joueur), corrections éditoriales dernière minute | Sonnet 5 (Haiku 4.5 pour les micro-correctifs) |
| Codex | Rien sur le chemin critique — **spec Proposition/Décision/Action v0.1 produite**, arbitrages fonctionnels avec Boris puis consolidation | — |

**→ 1er octobre : PALIER 1.**

### Sprint 4 · 2-15 oct — « Le portage de la coque » *(palier P2)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **La coque réelle en Rails** : les cinq portes, le contexte de Monde côté serveur (le `PZ_SHELL_CONTEXT` de Codex devient un vrai objet de session, les droits restant aux contrôleurs), états `annoncée/lecture/ouverte` câblés | **Fable 5** — LE chantier architectural du trimestre |
| Desktop | Toutes les **pages de teasing réelles** sur le gabarit du sprint 1 (une par destination fermée, chaque Monde) ; pastille **guides LLM : l'UI** (le backend suit au sprint 5) | Sonnet 5 |
| Codex | Spec P/D/A finalisée ; **corpus des guides** (sources, ton Professeur/Docteur, limites F19) | — |

### Sprint 5 · 16-29 oct — « Monde 0 complet dans la coque »

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **Guides LLM backend** (F19 : RAG sur le corpus, citations, garde-fous, effacement sur écrans sensibles) ; **`ActivityItem`** (F21) et ses trois projections | **Opus 5** (guides = IA + sécurité ; ActivityItem = transversal) |
| Desktop | Module **Ressourcerie vivante v1** (lecture : deux corpus, profondeurs, « Pourquoi maintenant ? » — le modèle de données existe, c'est un chantier de vues) | Sonnet 5 |
| Codex | Fiches héros éditoriales (biographies sourcées) ; revue du portage de coque (1er temps du cycle suivant) | — |

**→ fin octobre : PALIER 2.**

### Sprint 6 · 30 oct - 12 nov — « Monde 1 : les objets de la messagerie » *(palier P3)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **B3** composeur « + » et transformation message → objet (F22-F23 : Proposition, Action) ; **F20 `Meeting`** modèle + API (généralisation de `PropositionDeRencontre`) | **Fable 5** |
| Desktop | Module **Annuaire enrichi : l'UI** (recherche multi-critères, cartes — le périmètre d'autorisation des requêtes est livré par le portable en début de sprint) | Sonnet 5 |
| Codex | Maquette place de marché unifiée (R3 appliquée) ; spec reconnaissance (préalable F25) | — |

### Sprint 7 · 13-26 nov — « Monde 1 : décisions et mémoire »

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **B4** vues Fil/Actions/Décisions/Mémoire (F24) ; **B5** migration de l'objection ; assemblage annuaire + agenda | **Opus 5** |
| Desktop | Module **Agenda vivant : l'UI** (journée unifiée, calendrier — sur l'API Meeting du sprint 6) ; **profil unifié : les couches visuelles** (lemniscates, fresque — sa zone DA) | Sonnet 5 |
| Codex | Revue croisée du Monde 1 (1er temps) ; corpus Ressourcerie complété | — |

**→ fin novembre : PALIER 3 — un Cercle pilote quitte WhatsApp, tout compris.**

### Sprint 8 · 27 nov - 10 déc — « Monde 2 s'amorce » *(palier P4)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **Freeride + ligne de jeu** (F18/F4 : main de trois cartes, teasing aux Mondes 0-1 conformément à l'arbitrage) ; préférences de notification + digest | **Opus 5** |
| Desktop | Module **Héros & mentors v1** (catalogue + fiches complètes sur le gabarit Q&R §VIII — éditorial + vues ; le choix réversible de figure est un petit modèle que le portable livre) | Sonnet 5 |
| Codex | États `lecture`/`annoncée` rédigés pour tous les modules d'horizon (économie, gouvernance, académie…) ; spec économie Ω (préalable 2027) | — |

### Sprint 9 · 11-24 déc — « La coque fonctionnelle »

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **Recherche globale** d'objets (droits !) ; assemblage final ; matrice états réelle vérifiée porte par porte ; suite complète des bancs | **Opus 5** |
| Desktop | Passe **DA + voix** globale (R9, sur libellés gelés) ; accessibilité (R10 côté réel) | Sonnet 5 |
| Codex | Consolidation finale de la coque (3e temps) ; bilan des écarts maquette/réel module par module (R7 inversée) | — |

### Sprint 10 · fin décembre — recette du palier 4

Recette croisée complète (chaque agent teste la zone d'un autre), correctifs, passation
d'année. **→ 31 décembre : PALIER 4 — la coque fonctionnelle.**

## 4. Le graphe des dépendances fonctionnelles — la colonne vertébrale du plan

Les sprints du §3 sont la LINÉARISATION de ce graphe, pas l'inverse : si les crédits et le
rythme le permettent, tout ce dont les préalables sont satisfaits peut s'ouvrir sans
attendre sa quinzaine. Trois chaînes indépendantes avancent en parallèle (une par agent) ;
elles ne se rejoignent qu'aux nœuds marqués.

```
CHAÎNE MESSAGERIE / OBJETS (la plus longue — commande le palier 3)
  variante R11 (FAITE) ──▶ arbitrage intention par fil (FAIT) ──▶ spec P/D/A (Codex+Boris)
      ──▶ B3 composeur + F22/F23 (portable, Fable) ──▶ B4 vues + F24 (portable, Opus)
      ──▶ B5 migration objection ──▶ [PALIER 3]

CHAÎNE COQUE / NAVIGATION (commande les paliers 2 et 4)
  contrat de coque (fait) ──▶ gabarit teasing (desktop) ──▶ portage coque Rails
      (portable, Fable) ──▶ ┬─ pages de teasing par destination (desktop)
                            ├─ guides LLM : UI desktop ──▶ backend portable (Opus)
                            ├─ ActivityItem F21 (portable, Opus) ──▶ 3 projections
                            └─ branchement de CHAQUE module desktop ──▶ [PALIER 4]

CHAÎNE MODÈLE → UI (le contrat portable/desktop, un couple par module)
  F20 Meeting (portable) ──▶ UI agenda (desktop)
  scope de recherche annuaire (portable) ──▶ UI annuaire (desktop)
  modèle figure/choix de héros (portable) ──▶ Héros & mentors (desktop)
  corpus guides (Codex) ──▶ backend guides (portable) ──▶ pastille (desktop)

INDÉPENDANTS (ouvrable à tout moment, aucun préalable)
  R6a Échanges sur l'accueil · rotation Stripe · import WhatsApp (attend l'export)
  · Ressourcerie vivante v1 (modèle existant) · Aide & recours v1 (contenu)
  · préférences notifications + digest · fiches héros éditoriales (Codex)
```

Contraintes calendaires irréductibles (les seules) :

1. **Le gel Festival (15 sept - 1er oct)** : aucun chantier post-Festival ne touche `main`
   pendant cette fenêtre ; préprod reste ouverte — les chaînes continuent d'y avancer.
2. **Les arbitrages de Boris** sont les seuls nœuds non parallélisables : la barre
   mobile (R6b) d'abord — R11 est levé —, les préalables F25 ensuite (reconnaissance, économie) s'il veut
   déverrouiller 2027 tôt.

## 5. Méthode (inchangée) et charge

La cadence lot construit-vérifié-promu, les bancs négatifs, la règle F, GitHub source de
vérité, un agent par zone — tout tient. S'y ajoute : **chaque module du desktop entre dans
la coque par une relecture du portable**, et le cycle en trois temps (Claude → Boris →
Codex) scelle chaque palier avant le suivant.

Charge indicative par sprint : portable 1 gros chantier + l'assemblage ; desktop 1 module
+ sa part éditoriale ; Codex 1-2 livrables de spec/maquette. C'est la vélocité constatée
des trois dernières semaines, pas un pari.
