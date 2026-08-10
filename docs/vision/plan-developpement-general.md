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
claire) ; **Opus 4.8 / Fable 5** pour les chantiers multi-fichiers, architecturaux ou
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
| Bascule DNS (mode opératoire existant) + certificats | **Portable** | Opus 4.8 | date à fixer par Boris |
| Monde 0 impeccable : éditorial, guides, contenus | **Poste fixe** | Sonnet 5 | continu jusqu'au gel |
| Sas v2 : validation visuelle puis promotion | **Poste fixe** livre → **portable** promeut | Sonnet 5 | avant gel |
| QR codes `festival-lier` (impression) | **Portable** | Haiku 4.5 | hors chemin critique |
| Import WhatsApp du Cercle cœur (attend l'export `.txt` de Boris) | **Portable** | Fable 5 / Opus (données réelles, parsing, attribution des auteurs) | quand l'export arrive |

## Horizon 1 — Maquette-cible : itération courte (en parallèle, sans code Rails)

Objectif : rendre la maquette testable honnêtement AVANT d'en dériver du code. Tout se
joue dans `zegame-prototypes` et `zegame-docs` — zéro recouvrement avec l'app.

| Chantier | Porteur | Modèle | Note |
|---|---|---|---|
| Réponses aux 5 questions d'arbitrage de la revue | **Boris** | — | conditionne R1/R3/R4/R5/R6 |
| R1 sélecteur « Monde 0/1/2+ » dans la coque | **Codex** | — | l'écart le plus structurant |
| R2 traversée « Vivre le Festival » | **Codex**, sur l'état réel fourni par le portable | — | la seule traversée datée |
| R7 chapitre « état réel / projeté » par module | **Portable** fournit l'inventaire (doc) → **Codex/poste fixe** l'intègrent aux NOTES | Sonnet 5 (inventaire) | patron du module messagerie |
| R3-R6 corrections (porte des besoins, attention, Ω topbar, porte mobile) | **Codex** après arbitrages | — | — |
| R9 passe DA + voix sur coque et modules Festival | **Poste fixe** | Sonnet 5 | sa zone (DA v4, site) ; après gel des libellés |
| R10 matrice droits × états + accessibilité (modules Festival d'abord) | **Codex** avec relecture **portable** | Opus 4.8 (relecture droits) | recommandé par Codex lui-même |
| Tests utilisateurs des traversées (un par rôle) | **Boris** + Cercle cœur | — | après R1/R2 |

## Horizon 2 — Messagerie étape B, suite (le cœur applicatif qui continue)

La messagerie est le seul grand chantier applicatif SANS dépendance aux tests de la
maquette : sa vision-cible est écrite, S1 + B1 + B2 sont livrés. Ordre de l'audit S0.

| Chantier | Porteur | Modèle | Préalable |
|---|---|---|---|
| Spec Proposition / Décision / Action (+ lignes F19-F21 au registre) | **Codex + Boris** rédigent, **portable** relit la faisabilité | Fable 5 (relecture) | maquette messagerie comme référence |
| B3 — le composeur « + » : transformer un message en objet (Graine existe, puis Proposition/Action) | **Portable** | Fable 5 (architecture, cartes B2 comme socle) | la spec ci-dessus |
| B4 — vues Fil / Actions / Décisions / Mémoire par espace | **Portable** | Opus 4.8 | B3 |
| B5 — migration de l'objection B1 vers l'objet Décision | **Portable** | Sonnet 5 | B4 |
| Préférences de notification par espace + digest (cible §17, `EspaceMembership.notification`) | **Portable** | Sonnet 5 | aucun |
| Recherche globale d'objets (au-delà des messages : cartes, sondages, espaces) | **Portable** | Opus 4.8 (périmètre de droits) | B3 |

## Horizon 3 — Généraliser ce qui existe déjà (post-Festival, court)

Chaque module ci-dessous a un embryon réel en production — la généralisation est un lot
contenu, pas une invention.

| Chantier | Existant réel | Porteur | Modèle |
|---|---|---|---|
| `Meeting` généralisé (agenda vivant V1) | `PropositionDeRencontre` (mises en relation) | **Portable** | Opus 4.8 |
| `ActivityItem` — source d'attention unique (R4) | Engagements S1-A4 + boîte d'Échanges | **Portable** | Opus 4.8 (transversal) |
| Profil unifié (couches + visibilité par couche) | Profil + lemniscates + seuils F13 | **Portable** (structure) + **poste fixe** (DA) | Sonnet 5 |
| Annuaire enrichi (recherche multi-critères, mêmes droits que les cartes) | Annuaire + profils publiés | **Portable** | Sonnet 5 |
| Centre de consentement (agrégation en lecture des choix existants) | Partage de coordonnées, visibilités, blocages | **Portable** | Opus 4.8 (droits) |
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
| Académie & habilitations | critères de qualification (NOTES héros/académie) | **Portable** | Opus 4.8 |
| Organisations & Sas des organisations | offre commerciale réelle | **Portable** | Opus 4.8 |
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

1. Les **arbitrages Festival** (vague 0 du plan Festival) — la seule urgence datée.
2. Les **5 réponses** de la revue UX (coque réelle ou outil de test ; intention par fil ou
   par message ; porte des besoins ; porte mobile ; visibilité de l'Ω).
3. L'**export WhatsApp** du Cercle cœur, quand tu veux lancer l'import.
4. Le **go** sur la spec Proposition/Décision/Action avec Codex (Horizon 2) — c'est le
   prochain chantier applicatif structurant après le Festival.
