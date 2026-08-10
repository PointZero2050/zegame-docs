# Plan de développement général — sur la base de la revue UX-cible

<!-- [Claude] 2026-08-10, demande Boris. S'appuie sur : revue-ux-cible-consolidee.md,
     plan-developpement-vers-festival.md (qui reste le plan DIRECTEUR jusqu'au 1er
     octobre), application-festival-2026.md (décision opérationnelle), audit-s0-messagerie
     et l'état réel de la production (S1 complet, B1-B2 livrés). -->

**Règle de lecture.** Jusqu'au 1er octobre, le
[plan Festival](plan-developpement-vers-festival.md) prévaut : rien ici ne doit retarder
son chemin critique. Le présent plan organise tout le reste — l'itération des maquettes,
la suite de la messagerie, la généralisation des modules, les systèmes lourds — en
horizons successifs, avec pour chaque chantier son porteur et le modèle Claude adapté.

## 0. Qui fait quoi — la répartition (rappel + extension)

La répartition phase 2 (actée le 2026-08-04, amendée le 2026-08-10) reste la loi :

| Acteur | Territoire | Ne touche jamais |
|---|---|---|
| **Instance portable** (Claude, ce plan) | `pointzero-app` entier, serveur Hetzner, TOUS les déploiements et promotions en production, bancs de vérification | — |
| **Instance poste fixe** (Claude) | `zegame-prototypes`, `zegame-docs`, et dans `pointzero-app` : `content/articles/`, `app/views/site/`, `public/sas/` ; préprod par sa clé SSH ; `~/maquettes/` | modèles, migrations, config serveur, billetterie, contrôleurs applicatifs, `~/deploy/`, production |
| **Codex** | maquettes (`zegame-prototypes`), documents de vision, specs rédigées avec Boris | le code Rails |
| **Boris** | arbitrages, tests utilisateurs, éditorial final, feu vert | — |

Invariant : **celui qui produit ne s'auto-valide pas** — les livraisons du poste fixe et
de Codex sont relues et promues par l'instance portable ; les revues de l'instance
portable sont lisibles par tous dans `zegame-docs`.

Modèles Claude — doctrine constante : **Sonnet 5** par défaut (chantiers contenus, spec
claire) ; **Opus 5 / Fable 5** pour les chantiers multi-fichiers, architecturaux ou
touchant les droits ; **Haiku 4.5** pour les micro-tâches mécaniques.

---

## Horizon 0 — Festival (maintenant → 1er octobre) · PRIORITAIRE ABSOLU

Le détail vit dans le plan Festival (vagues 0-3). Répartition et modèles :

| Chantier | Porteur | Modèle | Échéance |
|---|---|---|---|
| Arbitrage des 3 catégories de périmètre (§8 décision Festival) | **Boris** | — | cette semaine |
| Publier l'événement Festival, le cocher « phare », composer la journée (créneaux) | **Boris** (console) + portable en appui | Haiku 4.5 (appui console) | avant fin août |
| Rotation de la clé Stripe restreinte + vérification bout-en-bout du paiement | **Portable** | Sonnet 5 | avant vente réelle |
| Rejouer `repetition_50` sur la vraie journée composée | **Portable** | Sonnet 5 | après composition, puis avant gel |
| Bascule DNS (mode opératoire existant) + certificats | **Portable** | Opus 5 | date à fixer par Boris |
| Monde 0 impeccable : éditorial, guides, contenus | **Poste fixe** | Sonnet 5 | continu jusqu'au gel |
| Sas v2 : validation visuelle puis promotion | **Poste fixe** livre → **portable** promeut | Sonnet 5 | avant gel |
| QR codes `festival-lier` (impression) | **Portable** | Haiku 4.5 | hors chemin critique |
| Import WhatsApp du Cercle cœur (attend l'export `.txt` de Boris) | **Portable** | Fable 5 / Opus (données réelles, parsing, attribution des auteurs) | quand l'export arrive |

## Horizon 1 — Maquette-cible : itération courte (en parallèle, sans code Rails)

**Décision cadre du 2026-08-10 : la coque EST la navigation cible réelle**, au terme d'un
processus en trois temps qui devient une règle de gouvernance —
**revue Claude → corrections par Boris → consolidation finale avec Codex**. Aucune maquette
ne devient cible sans avoir traversé les trois temps. L'investissement dans R1 et R9 est
donc justifié : ce sont des travaux sur la future navigation de production.

| Chantier | Porteur | Modèle | État |
|---|---|---|---|
| R1 sélecteur « Monde 0/1/2+ » dans la coque | **Codex** | — | confirmé et renforcé — l'écart le plus structurant |
| R2 traversée « Vivre le Festival » | **Codex**, sur l'état réel fourni par le portable | — | à faire ; seule traversée datée |
| R3 la Place de marché absorbe les Missions du Commun | **Codex** | — | **tranché** (Boris, 2026-08-10) |
| R11 variante « intention PAR FIL » à comparer | **Codex** | — | **nouveau** — conditionne la spec Proposition/Décision/Action |
| R5 vocabulaire de l'Ω : « compte », jamais « score » ; traitement discret | **Codex** | — | **amendé** : l'Ω reste en permanence ; corriger la NOTES annuaire |
| R6b configurations de barre mobile à tester | **Codex** | — | en attente des tests de Boris |
| R4 source d'attention unique ; badge numérique retiré de la topbar | **Codex** | — | à faire |
| R7 chapitre « état réel / projeté » par module | **Portable** fournit l'inventaire → **Codex / poste fixe** l'intègrent | Sonnet 5 (inventaire) | patron du module messagerie |
| R10 matrice droits × états + accessibilité (modules Festival d'abord) | **Codex** avec relecture **portable** | Opus 5 (relecture droits) | recommandé par Codex lui-même |
| R9 passe DA + voix sur coque et modules Festival | **Poste fixe** | Sonnet 5 | après gel des libellés |
| Tests utilisateurs des traversées (un par rôle) + configurations de menu | **Boris** + Cercle cœur | — | après R1/R2/R6b |
| **R6a — Échanges visibles sur l'accueil du Jeu RÉEL** | **Portable** | Sonnet 5 | **décidé, actionnable tout de suite** — voir Horizon 2 |

## Horizon 2 — Messagerie étape B, suite (le cœur applicatif qui continue)

La messagerie est le seul grand chantier applicatif SANS dépendance aux tests de la
maquette : sa vision-cible est écrite, S1 + B1 + B2 sont livrés. Ordre de l'audit S0.

| Chantier | Porteur | Modèle | Préalable |
|---|---|---|---|
| **R6a — les Échanges sur l'accueil du Jeu** (engagements « À ton attention » déjà construits en S1-A4 ; aujourd'hui les Échanges ne figurent QUE dans l'icône de la barre) | **Portable** | Sonnet 5 | **aucun — décidé le 2026-08-10** |
| Spec Proposition / Décision / Action (+ lignes F19-F21 au registre) | **Codex + Boris** rédigent, **portable** relit la faisabilité | Fable 5 (relecture) | **R11** (arbitrage intention par fil / par message) |
| B3 — le composeur « + » : transformer un message en objet (Graine existe, puis Proposition/Action) | **Portable** | Fable 5 (architecture, cartes B2 comme socle) | la spec ci-dessus |
| B4 — vues Fil / Actions / Décisions / Mémoire par espace | **Portable** | Opus 5 | B3 |
| B5 — migration de l'objection B1 vers l'objet Décision | **Portable** | Sonnet 5 | B4 |
| Préférences de notification par espace + digest (cible §17, `EspaceMembership.notification`) | **Portable** | Sonnet 5 | aucun |
| Recherche globale d'objets (au-delà des messages : cartes, sondages, espaces) | **Portable** | Opus 5 (périmètre de droits) | B3 |

## Horizon 3 — Généraliser ce qui existe déjà (post-Festival, court)

Chaque module ci-dessous a un embryon réel en production — la généralisation est un lot
contenu, pas une invention.

| Chantier | Existant réel | Porteur | Modèle |
|---|---|---|---|
| `Meeting` généralisé (agenda vivant V1) | `PropositionDeRencontre` (mises en relation) | **Portable** | Opus 5 |
| `ActivityItem` — source d'attention unique (R4) | Engagements S1-A4 + boîte d'Échanges | **Portable** | Opus 5 (transversal) |
| Profil unifié (couches + visibilité par couche) | Profil + lemniscates + seuils F13 | **Portable** (structure) + **poste fixe** (DA) | Sonnet 5 |
| Annuaire enrichi (recherche multi-critères, mêmes droits que les cartes) | Annuaire + profils publiés | **Portable** | Sonnet 5 |
| Centre de consentement (agrégation en lecture des choix existants) | Partage de coordonnées, visibilités, blocages | **Portable** | Opus 5 (droits) |
| Export de compte complet (RGPD, au-delà du fil) | Export de fil A10 | **Portable** | Sonnet 5 |

## Horizon 4 — Systèmes nouveaux (specs et juridique AVANT tout code)

Aucun de ces chantiers ne démarre sans sa spec validée et, où la revue l'exige, son
cadrage juridique. L'ordre interne dépendra des tests utilisateurs de l'Horizon 1.

| Chantier | Préalable bloquant | Porteur build | Modèle |
|---|---|---|---|
| Économie Ω : orientation, Fonds, cagnottes | gouvernance exacte des consultations (Q&R §X) ; chiffres à confirmer | **Portable** | Fable 5 |
| Reconnaissance : rituel, enveloppe, consentement | spec du rituel (canon 31/07 §11-15) | **Portable** | Fable 5 |
| Gouvernance du Commun : consultations pondérées | idem + doctrine de pondération | **Portable** | Fable 5 |
| Place de marché | **frontières juridiques** (marketplace/prestation/dons), rôles, TVA | **Portable** | Fable 5 |
| Académie & habilitations | critères de qualification (NOTES héros/académie) | **Portable** | Opus 5 |
| Organisations & Sas des organisations | offre commerciale réelle | **Portable** | Opus 5 |
| Héros & mentors, mentor IA & Fresque | politique éditoriale des figures ; coûts IA | **Portable** | Fable 5 |

## Horizon 5 — Horizon du Jeu (après pilote)

Monde-miroir et épreuve autosubversive restent des prototypes à éprouver avec le Cercle
cœur (ce que la cible prescrit elle-même). **Codex** les fait vivre en maquette ; aucun
portage applicatif avant un pilote concluant et une spec. Modèle du moment venu : Fable 5.

---

## Méthode transverse (inchangée, éprouvée sur 25+ lots)

1. **La cadence** : un lot = construit en préprod → banc de vérification négatif → suite
   des bancs sœurs → commit `[Claude]`/`[Codex]` → relecture croisée → sauvegarde →
   promotion en production par l'instance portable → passation.
2. **La règle F** : aucun objet métier nouveau sans sa ligne dans
   `impacts-fonctionnels.md` (R8).
3. **Un agent par zone**, `git fetch` avant reprise, GitHub source de vérité (jamais la
   copie Dropbox).
4. **Les maquettes sont la référence visuelle figée** ; l'app ne les contredit jamais —
   et depuis la revue : les NOTES disent l'écart réel/projeté, l'app documente en retour
   ce qu'elle a livré (le patron du module messagerie, dans les deux sens).

## Ce que ce plan attend de Boris maintenant

*(Les 5 questions de la revue UX ont été arbitrées le 2026-08-10 — voir
[revue-ux-cible-consolidee.md](revue-ux-cible-consolidee.md) §4. Reste :)*

1. Les **arbitrages Festival** (vague 0 du plan Festival) — la seule urgence datée.
2. Les **deux arbitrages différés**, une fois les maquettes produites par Codex :
   l'intention **par fil** ou par message (variante R11 à comparer), et la
   **configuration de barre mobile** (R6b) — plus la sous-question du compte d'Ω :
   **actifs** (recommandé) ou cumul historique ?
3. L'**export WhatsApp** du Cercle cœur, quand tu veux lancer l'import.
4. Le **go** sur la spec Proposition/Décision/Action avec Codex (Horizon 2), qui dépend de
   l'arbitrage R11 — c'est le prochain chantier applicatif structurant après le Festival.
