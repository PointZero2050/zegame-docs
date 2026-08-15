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
juridiquement ouverte, académie/habilitations, organisations, **le monde-miroir dans
Rails**, épreuve des runes. Ils existeront fin décembre **en pages d'annonce ou en
lecture**, conformément au contrat de coque — c'est une existence honnête, pas une
absence.

**Amendement du 12 août (bloc canonique `5bf587c`, analyse
[analyse-impact-coque-cinq-puissances-grand-jeu.md](analyse-impact-coque-cinq-puissances-grand-jeu.md))** —
deux ajouts qui ne déplacent aucun palier :

- **Coque v2 « les cinq verbes »** (`Discerner · Décider · Relier · Créer · Ressentir`) :
  correspondance 1:1 avec les cinq portes en production (ids stables, libellés = données
  de registre), trois destinations changent de porte (ressourcerie, héros, agenda →
  Discerner), plus le portail-teaser du miroir, la page Omégas et les cinq futurs v0.
  Séquence imposée : **maquettes (desktop + Codex) → recette de navigation (§8.8 de
  coque-cinq-puissances) → portage préprod → promotion APRÈS le Festival** — le renommage
  des portes est la chose la plus visible qu'on puisse faire à l'application, et rien de
  développé en août n'est rendu visible pour le Festival.
- **Grand Jeu / monde-miroir** : quatrième chaîne du graphe (§4), autonome. Le premier
  livrable est le **prototype 2D autonome** (grand-jeu-monde-miroir-cible §15) dans
  zegame-prototypes — il ne touche pas Rails, simule la validation, et se juge sur une
  seule hypothèse : le joueur comprend-il que sa transformation réelle modifie le destin
  de son double ? Les six préalables du §18 (analyses d'impact Omégas/decay/droits,
  consentement, contrat d'événements, architecture) restent des portes fermées tant que
  le prototype n'a pas prouvé la boucle.

## 3. Les sprints (deux semaines) — qui, quoi, quel modèle

Les modèles suivent la doctrine : Sonnet 5 par défaut, **Opus 5 / Fable 5** pour
l'architecture et les droits, Haiku 4.5 pour le mécanique. Codex n'est pas un modèle
Claude ; ses tâches n'en portent pas.

### Sprint 1 · 12-25 août — « La vente ouvre » *(palier P1)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | Rotation Stripe + test de paiement bout-en-bout ; appui à Boris pour publier/cocher phare/composer la journée ; **R6a** (les Échanges nommés sur l'accueil du Jeu) ; import WhatsApp si l'export arrive | Sonnet 5 (Fable 5 pour l'import WhatsApp) |
| Desktop | Monde 0 éditorial + finalisation Sas v2 ; **premier module dev : les pages de teasing** (gabarit « ce que c'est, ce qu'on y fera, ce qui l'ouvre » — vues pures, zéro droit, la brique de base du dévoilement) | Sonnet 5 |
| Codex | **R11 faite et arbitrée** ; **R6b arbitrée : option C, « Échanges au centre »** ; **traversée Festival R2 produite** — revue Boris R2 en attente | — |
| Boris | Arbitrages Festival vague 0 ; catégories de périmètre §8 | — |

**Ajout du 12 août, en parallèle du chemin critique Festival** : le desktop et Codex
traduisent le bloc canonique du 12 août en **maquettes** — (a) la barre des cinq verbes
et la collision « Créer »/bouton `+` sur mobile, (b) l'emplacement de la Couronne
(portail miroir) hors des cinq portes, (c) les actions contextuelles du `+`, (d) le
teaser Monde 0 du miroir (préalable §18.4). Ces maquettes sont le préalable du sprint 4
révisé ; rien n'en devient visible pour le Festival.

**RÉVISION DU 15 AOÛT (Boris)** — le travail de maquettage a débouché sur une
consolidation plus profonde que prévu : le **lot onboarding Monde 0** (doc canonique
[onboarding-monde-0-sept-puissances.md](onboarding-monde-0-sept-puissances.md), 25
commits Codex dans zegame-prototypes, 9 prototypes `*-m0-cible` + coque `m0-shell`).
L'accueil devient un **métaparcours des sept Puissances** (cartes d'appel + roue), qui
**amende la barre des cinq verbes** : les cinq intentions restent une cartographie
fonctionnelle, la navigation visible passe par les sept Puissances. Conséquences :

- la **cible de fin août** devient : Monde 0 pleinement fonctionnel et engageant sur ce
  modèle, **mis en ligne AVANT le Festival** (renversement assumé de la règle « rien
  d'août visible au Festival » — pour ce lot uniquement, décision Boris du 15 août) ;
- les chantiers ouverts le 12 août (coque v2 « cinq verbes », lot sprint 4) sont
  **suspendus** en l'état : la coque v2 sera redéfinie sur la base du métaparcours une
  fois le Monde 0 en ligne ;
- le portage Rails du lot est cadencé par l'analyse du portable du 15 août (voir
  PASSATION-CLAUDE.md, session du 15 août) : l'essentiel du backend existe déjà en
  production (Marelle, Ressourcerie 10 fiches, héros 42 figures, Moteur/questionnaires,
  badges, Graines, Espaces, barème Ω) — le chantier est un chantier de **vues et d'un
  petit modèle d'état** (Traces, popups vues, états de cartes), pas de modèles lourds ;
- gel du 15 septembre inchangé : la cible de fin août laisse deux semaines de recette.

**Répartition d'août révisée (15 août)** — trois lignes de charge parallèles :

| Acteur | Charge d'ici fin août | Détail |
|---|---|---|
| **Portable** | **Portage Rails du lot Monde 0** (le chemin critique) | Ordre : coque `m0-shell` en HAML (en-tête, roue, pastille Ω) → Intuition + Transcendance (backend le plus complet, boucle Trace incluse) → accueil métaparcours (a besoin des états des territoires) → le reste. Plus les modèles transverses : Traces généralisées, popups « vues » côté serveur, états de cartes, et — après arbitrage fournisseur — modèle de consentement par catégorie + mémoire des conversations (tables chez nous, page joueur « visible, éditable, désactivable »). |
| **Desktop** | **Banc de comparaison Claude/GPT des personnages** (détaché du chemin critique) + suite éditoriale des maquettes | Harnais autonome (prototype dans zegame-prototypes, contrat d'intégration habituel) : transpose les prompts des GPTs existants, fait passer les MÊMES scénarios limites aux deux API (joueur en détresse, joueur provocateur, question intime, 40e message avec mémoire rejouée), sort les réponses côte à côte pour lecture par Boris. Sert ensuite de banc de non-régression du ton. **Règle absolue : aucune clé d'API dans le dossier Dropbox ni dans les repos** — variable d'environnement locale uniquement. |
| **Codex** | **Scénarios limites + corpus — FAIT le 16 août** | Les huit scénarios du banc ont reçu leur version éditoriale agnostique du mentor. Le corpus compte 30 fiches M0 et 21 fiches M1 ; les sources citables sont des titres publics sans chemin interne. Prochaine action : recette qualitative et synchronisation du lot M1 côté application. |

Séquence du chantier « personnages LLM » : banc comparatif (desktop, FAIT) →
**arbitrage fournisseur par Boris : CLAUDE, acté le 15 août** (mentors ET guides) →
consentement + mémoire + appel (portable, **FAIT le 15 août**, `zegame-app` preprod
`2e7a88a` : `ConsentementLlm` opt-in par catégorie, `MentorMessage` mémoire effaçable
par le joueur, `PlafondLlm` robinet unique guides+mentors, `MentorReponse` incarnant la
figure choisie, pages `/mentor` et `/mentor/consentements`) → branchement des guides
FAIT aussi (F19 Palier 1, le corpus Codex est en prod ; voir PASSATION du 15 août).

**Mise à jour du 16 août : le goulot éditorial n'est plus l'absence de corpus.** Les voix
des six mentors sont portées par les prompts du banc, les huit scénarios sont éditorialisés et
le corpus guide couvre M0 et M1. Restent : intégrer le lot M1 sans exposer les chemins de dépôt,
rejouer le banc de non-régression, puis faire la lecture qualitative de Boris avant toute
visibilité élargie.

### Sprint 2 · 26 août - 8 sept — « Le jour J est prêt »

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | Rejouer `repetition_50` sur la vraie journée ; QR `festival-lier` ; mode opératoire DNS répété à blanc ; correctifs de la répétition | Sonnet 5 (Opus 5 pour la bascule DNS) |
| Desktop | Module **Aide & recours v1** (numéros d'urgence avant connexion, orientation, personnes ressources — contenu et vues ; le signalement/blocage EXISTE déjà côté portable, il le branche) | Sonnet 5 |
| Codex | **R10 produite** : matrice droits × états des modules Festival ; consolidation après les deux arbitrages Boris (fenêtre D+7, accès intervenant aux retours anonymisés) | — |

### Sprint 3 · 9-22 sept — « Gel et répétition générale » *(gel le 15)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | Stabilisation, bancs complets, répétition générale, checklist feu vert, astreinte | Sonnet 5 |
| Desktop | Recette utilisateur complète en préprod (peau de joueur), corrections éditoriales dernière minute | Sonnet 5 (Haiku 4.5 pour les micro-correctifs) |
| Codex | Rien sur le chemin critique — **spec Proposition/Décision/Action v0.1 produite**, arbitrages fonctionnels avec Boris puis consolidation | — |

**→ 1er octobre : PALIER 1.**

### Sprint 4 · 2-15 oct — « La coque v2 : les cinq verbes » *(palier P2)*

*(Le portage initial de la coque — l'ancien contenu de ce sprint — a été réalisé le
12 août avec deux mois d'avance, prod `80931d2`. Sa fenêtre accueille la coque v2, dont
la promotion en production ne pouvait de toute façon pas précéder le Festival.)*

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **Portage de la coque v2** sur les maquettes validées : renommage + sous-titres + symboles par Monde, les 3 déplacements de destinations (attention à `verifier!` : au plus une annoncée par porte et par Monde), portail-teaser du miroir (Couronne), page Omégas transversale, cinq futurs v0 (YAML + vue Discerner). Recette de navigation §8.8 avant, banc `verifier_coque` étendu après. **Préprod jusqu'au 2 octobre, promotion post-Festival.** | **Opus 5** (registre + droits, mais l'architecture est déjà en place) |
| Desktop | Toutes les **pages de teasing réelles** sur le gabarit du sprint 1 (une par destination fermée, chaque Monde) ; pastille **guides LLM : l'UI** (le backend suit au sprint 5) | Sonnet 5 |
| Codex | Spec P/D/A finalisée *(FAITE en avance — toute la chaîne B3-B5 est en prod depuis le 12 août)* ; **corpus des guides** (sources, ton Professeur/Docteur, limites F19 — la ligne de partage Professeur=réel / Docteur=miroir posée par grand-jeu-monde-miroir-cible §3 s'y écrit) | — |

### Sprint 5 · 16-29 oct — « Monde 0 complet dans la coque »

| Acteur | Charge | Modèle |
|---|---|---|
| Portable | **Guides LLM backend** (F19) — **réalisé en avance le 15 août pour le palier 1**, avec les deux voix retenues par Boris. Corpus M0 ingéré ; corpus M1 livré le 16 août, à synchroniser et recetter. Pas de RAG vectoriel : le corpus curaté tient dans le prompt. ‖ **`ActivityItem`** (F21) et ses trois projections — **FAIT** | **Sonnet 5** suffit ; la difficulté restante est la recette éditoriale et l'intégration progressive de la pastille. |
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
| Desktop | Module **Héros & mentors v1** — **OUVRABLE MAINTENANT** (12 août, en avance sur ce sprint : le petit modèle est livré, `User#choisir_heros!(slug)` / `#heros_choisi?`, aucun catalogue ni contrôleur côté portable — voir détail dans la passation du 12 août) : catalogue + fiches complètes sur le gabarit Q&R §VIII (biographie, faits, lecture PZ, 3 Puissances-phares, don, Ombre, cadre nécessaire, parcours associés), éditorial + vues, patron Ressourcerie (YAML, sans table). Portée v1 : catalogue lisible + choix personnel — PAS la mécanique mentor IA/Freeride (Q44), hors périmètre pour l'instant. | Sonnet 5 |
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
  variante R11 (FAITE) ──▶ arbitrage intention par fil (FAIT) ──▶ spec P/D/A (FAITE, Codex)
      ──▶ audit Claude (FAIT — voir audit-proposition-decision-action.md : droits/carte/mandat
          déjà réutilisables tels quels ; colonne « intention du fil » à poser AVANT le
          composeur ; ActivityItem hors périmètre B3)
      ──▶ arbitrages Boris §13 (FAITS, 12 août — les 5 recommandations retenues telles quelles)
      ──▶ B3 FAIT (12 août, prod ec29987) : intention du fil + Proposition + Action +
          transformation de message + cartes, 34 contrôles verts — voir la spec §11
      ──▶ B4 FAIT (12 août, prod 3018869) : Décision par consentement (gabarit cercle,
          électorat figé, objection à trois champs, consignation validée par un autre
          membre), vues Mes actions + Décisions du Cercle, versions de Proposition,
          3 engagements nouveaux — 36 contrôles verts
      ──▶ B5 FAIT (12 août, prod a93d114) : le double registre est clos — l'objection
          quitte la palette des réactions (8 restent), les anciennes conservées et gelées
          avec provenance « ancien registre », 13 contrôles verts
      ──▶ CHAÎNE COMPLÈTE — la messagerie capacitante du [PALIER 3] est livrée côté
          objets ; les trois couples modèle→UI de la chaîne 3 sont livrés côté
          portable (héros, annuaire, F20 Meeting) — restent leurs UI (desktop)
          et le profil unifié

CHAÎNE COQUE / NAVIGATION (commande les paliers 2 et 4)
  contrat de coque (fait) ──▶ gabarit teasing (desktop, FAIT) ──▶ portage coque Rails
      (FAIT, 12 août, prod 80931d2 : registre config/coque.yml + service Coque à 4 états,
       5 portes + destbar + barre mobile option C, VerrouDeCoque — le teasing remplace la
       redirection-alerte sur Cercles/Annuaire, /a-venir/:id pour les horizons,
       PZ_SHELL_CONTEXT v1, 31 contrôles + 11 bancs verts. Premier module desktop
       BRANCHÉ dans le registre : Héros & mentors, relu et promu le même jour)
      ──▶ ┬─ pages de teasing par destination (desktop, OUVRABLE — le gabarit et la
          │   mécanique sont en prod, il reste l'éditorial fin par destination)
          ├─ guides LLM : UI desktop ──▶ backend portable (Opus)
          ├─ F21 source d'attention (FAIT, 12 août, prod 51c7eb0) ──▶ les 3 projections
          │   sont en place ; arbitrage Boris : lecture élargie, PAS de journal
          │   (les objets métier sont l'archive) — seul `vu` est persisté
          └─ branchement de CHAQUE module desktop ──▶ [PALIER 4]

CHAÎNE MODÈLE → UI (le contrat portable/desktop, un couple par module)
  F20 Meeting (FAIT, 12 août, prod 8624117 : contexte polymorphe + disponibilités
      recueillies) ──▶ UI agenda (desktop, OUVRABLE)
  scope de recherche annuaire (FAIT, 12 août) ──▶ UI annuaire (desktop, OUVRABLE)
  modèle figure/choix de héros (FAIT) ──▶ Héros & mentors (desktop, FAIT — relu, branché à la coque, en prod)
  corpus guides (Codex) ──▶ backend guides (portable) ──▶ pastille (desktop)

CHAÎNE GRAND JEU / MONDE-MIROIR (nouvelle, 12 août — autonome, ne touche pas Rails)
  bloc canonique 5bf587c (FAIT, Codex) ──▶ analyse d'impact coque v2 + Grand Jeu
      (FAITE, 12 août — voir analyse-impact-coque-cinq-puissances-grand-jeu.md)
      ──▶ ┬─ maquettes coque v2 (desktop + Codex, EN COURS — sprint 1 amendé)
          │     ──▶ recette de navigation §8.8 ──▶ portage coque v2 (portable,
          │         sprint 4 révisé, préprod) ──▶ promotion POST-FESTIVAL
          ├─ teaser Monde 0 du miroir (desktop, §18.4 — entre dans le lot coque v2)
          └─ prototype 2D autonome §15 (desktop + Codex, zegame-prototypes, réemploi
              du fonds avatar/ — validation SIMULÉE, zéro appel à l'app)
              ──▶ [la boucle est-elle comprise ?] ──▶ SEULEMENT ALORS :
                  analyse d'impact Omégas/decay/droits (portable, §18.1)
                  ──▶ consentement + gouvernance LLM (Codex puis portable, §18.2)
                  ──▶ contrat d'événements réel ↔ miroir (portable, §18.3)
                  ──▶ décision d'architecture temps réel (Boris, §18.6)

INDÉPENDANTS (ouvrable à tout moment, aucun préalable)
  R6a (FAIT) · rotation Stripe (FAIT) · import WhatsApp (différé, attend l'export)
  · Ressourcerie vivante v1 (FAIT) · Aide & recours v1 (FAIT)
  · préférences notifications + digest (FAIT) · fiches héros éditoriales (Codex, FAIT)
  · Héros & mentors v1 (desktop, OUVRABLE — modèle livré 12 août, voir Sprint 8 ci-dessus)
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
