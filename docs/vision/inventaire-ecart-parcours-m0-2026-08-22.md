# Inventaire d'écart — parcours et expérience du Monde 0 (22 août 2026)

**Ce document n'est pas un canon.** Il mesure le code existant en face des deux maquettes
livrées par Codex le 22 août (`ca70f4c`) et n'arbitre rien. Il sert à ce que la frontière entre
les deux pages soit écrite en connaissance de ce qu'elle emporte, plutôt que tranchée par défaut
au moment du portage.

Sources mesurées : `app/views/journeys/_show.html.haml` (341 lignes, portage du 16 août de
`volonte-marelle-m0-cible`), `public/pz/m0/marelle.css` (381), `app/views/challenges/`
(416 lignes en six partiels), `app/services/journey_progress.rb`,
`app/helpers/experience_cover_helper.rb`, `config/journeys/point-zero-monde-0.yml`,
`config/puissances/*.yml`. Maquettes : `parcours-monde-0-cible/`, `experience-monde-0-cible/`.

---

## 1. ⚠️ Le fait structurant : trois blocs ne disparaissent pas, ils DÉMÉNAGENT — et leur destination ne les a pas

Les notes de `parcours-monde-0-cible` disent que la page « n'affiche ni bloc d'action détaillé ni
mécanisme de reconnaissance ». Lu seul, cet énoncé se porte en trois suppressions. Mesuré, il
décrit un **déplacement vers la page expérience** — et la page expérience de l'application ne
porte aujourd'hui **aucun** des trois.

| bloc | vit aujourd'hui dans | la maquette le met dans | l'application l'a-t-elle là-bas ? |
|---|---|---|---|
| intensité `/5` et échelle d'effet `/5` | `journeys/_show` (`.experience-metrics`) | `experience-monde-0-cible` (`.metrics`) | **NON** |
| la séquence en trois gestes | `journeys/_show` (`.sequence`) | `experience-monde-0-cible` (`.journey-sequence`) | **NON** |
| les quatre colonnes de reconnaissance | `journeys/_show` (`.recognition`) | `experience-monde-0-cible` (`.recognition`) | **NON** |

Vérifié : `grep -rln "intensity|effect_scale|sequence" app/views/` ne renvoie que
`journeys/_show.html.haml`. **Porter la nouvelle page parcours sans porter d'abord — ou dans le
même lot — la page expérience RETIRE ces trois blocs de l'application**, sans qu'aucun banc ni
aucune revue de diff ne le signale, puisque chaque page prise isolément sera conforme à sa
maquette.

C'est la première chose à écrire dans le canon : **les deux pages se portent ensemble, ou dans cet
ordre.**

---

## 2. Page parcours — inventaire bloc par bloc

Légende : ✅ conservé · ➡️ déménage vers la page expérience · ➕ nouveau dans la maquette ·
⚠️ sans équivalent, à trancher.

| # | bloc actuel | ce que la maquette en fait |
|---|---|---|
| 1 | `.journey-head` — médaillon, eyebrow, titre, promesse, `.journey-facts` | ✅ `.journey-intro`. **Deux différences** : la maquette **sépare la durée obligatoire de la facultative** (« 6 h 30 obligatoires · + 1 h 10 facultatives ») là où le port cumule tout ; et elle n'a **pas de médaillon photo** — l'illustration générale devient le fond du bloc de synthèse. |
| 2 | `aside.journey-power` — PUISSANCE GLOBALE `/10`, `.ten-scale`, note | ✅ `.power-score`, quasi identique. |
| 3 | — | ➕ `.omega-total` (« 84 Ω · potentiel total du parcours ») et `.top-powers` (les trois Puissances dominantes avec leurs icônes). **Dérivables sans éditorial** (voir §4). |
| 4 | `ol.jp-mouvements` — les jalons cliquables (chapitres + « Le passage ») avec Franchi / En cours / À venir | ⚠️ **absent de la maquette.** Il répond à « où suis-je » d'un coup d'œil sans dérouler, et c'est le **seul endroit où le seuil apparaît en tête de page**. |
| 5 | `journeys/_action_button` | ✅ `.hero-actions` (`.primary` + `.secondary` vers `#chapters`). |
| 6 | `section.jp-voix` — une phrase narrative dont les chiffres sont **dans** la phrase | ⚠️ **remplacée par des compteurs** : `.active-progress` (2/12 + barre), `.omega-total` (12 Ω sur 84), `.current-chapter`. C'est **l'inverse exact du mouvement du 16 août**, dont le commentaire dit : « Remplace les deux compteurs secs — les chiffres sont désormais DANS la phrase. » Arbitrage éditorial. |
| 7 | `section.jp-next` → `.experience` (le grand bloc) | ➡️ vers la page expérience (§1). |
| 8 | `section.jp-next` → `.jp-next-banner` (repli pour un parcours **sans** fiche YAML) | ✅ transformé : en `?state=active`, la prochaine expérience **monte dans le hero** (`.current-location`, titre de l'expérience, `03 / 14`, « Reprendre l'expérience »). ⚠️ Mais la maquette ne dit rien du **parcours sans YAML** — le Festival 2026 en est un, et la dégradation propre actuelle (ni puissance, ni métriques, ni séquence) doit survivre. |
| 9 | `.jp-next-empty` — deux messages (« tout est accompli » / « rien d'ouvert ») | ⚠️ sans équivalent. |
| 10 | `.jp-next-cloture-ligne` — « Refermer le livre → » vers `accompli_journey_path` | ⚠️ sans équivalent. Le rite de clôture reste atteignable après coup **par ce lien seul**. |
| 11 | `section.jp-path` — chapitres en `<details>` | ✅ `.chapter` / `.experience-list`, **vocabulaire entièrement neuf**. ➕ la maquette ajoute : le **verbe** du chapitre (« Je pressens »), une description longue narrative, la **durée par chapitre**, la **gravure en fond** du `.chapter-head`, et un **médaillon par expérience**. |
| 12 | `.jp-chapitre-compte` — « X / Y franchies · N Ω » | ⚠️ absent de la maquette (elle affiche « 5 expériences · 1 h 15 »). ⚠️ **Il porte une borne durement acquise** : le dénominateur d'Ω est borné par le gagné, parce qu'un joueur peut détenir plus d'Ω que le chapitre n'en vaut aujourd'hui (irrévocabilité). Sans elle : « 27 / 24 Ω ». |
| 13 | `chapitre_badge`, `.jp-chapitre-texture`, la vignette du chapitre | ⚠️ la maquette a un `.state` (EN COURS · 2/5, À VENIR) mais pas de badge de validation ni de texture. |
| 14 | la ligne d'expérience = `challenges/_cover_card` **compact** | ⚠️ la maquette la remplace par `.experience-row` (index ou ✓, titre, description courte, état, facultative, durée, Ω, médaillon). **`_cover_card` est partagé par trois vues** (`journeys/_show`, `challenges/_show` « Étape suivante », `challenges/_action_button`) : le remplacer sur la page parcours **désolidarise** la liste de la carte « Étape suivante », qui restera à l'ancien vocabulaire. |
| 15 | `section.jp-seuil` — le seuil **hors liste**, en destination de fin, avec état, durée, Ω, autorité, et ses **préparations facultatives** | ⚠️ **écart de doctrine.** Le seuil n'est pas déclaré, il est **dérivé** : `inclusions.find { validation_authority == "facilitateur" }`, puis **retiré de son chapitre** (`journey_progress.rb:109-110`), les Ω du chapitre étant recalculés **après** ce retrait. La maquette le remet en ligne ordinaire du chapitre 3 (« L'Atelier Point Zéro »). **Conséquence mesurable : les totaux d'Ω par chapitre changent.** |
| 16 | `section.recognition` (les quatre colonnes) | ➡️ vers la page expérience. ⚠️ La maquette y nomme la troisième colonne **AUTORITÉ**, le port actuel **RECONNAISSANCE** — même source (`validation_authority_label`). |
| 17 | `section.jp-about` — « À propos de ce parcours » (description + tags) et « Ce que tu as déjà mis en mouvement » (compétences et Ω) | ⚠️ sans équivalent. La maquette ne montre rien sous la carte. |

---

## 3. Page expérience — ce que la maquette demande, ce que l'application rend

| maquette | dans `app/views/challenges/` aujourd'hui |
|---|---|
| `.back` — « ← Point Zéro — entrer dans le Jeu » | ⚠️ absent. `_around_links` donne Précédent / Suivant, pas le retour au parcours. |
| `.art-context` — « CHAPITRE 1 · EXPÉRIENCE 1 SUR 14 » | ~ partiel : `chapter_label` existe (« Chapitre 1 · … »), **le rang « 1 sur 14 » non**. |
| `.power-chips` — trois chips Puissance · polarité · verbe, **sur la cover** | ⚠️ absent de la cover. Le contenu existe plus bas en cartes (§4). |
| `.experience-title` — eyebrow, h1, `.hook`, `.tags`, CTA nommé | ✅ `_cover_card` + `_action_button`. |
| `.readout` — DURÉE / MODE / RECONNAISSANCE / MISE EN CIRCULATION | ~ `.pz-stats-row` donne **NIVEAU `/10`** / DURÉE / OMÉGA. ⚠️ **MODE** et **RECONNAISSANCE** manquent ; et **NIVEAU `/10` contredit la grammaire d'échelles que la maquette pose elle-même** dans son aide de première visite : « `/10` potentiel du **parcours**, `/5` intensité d'une **expérience**, `/5` échelle de son effet ». Un `/10` sur une expérience n'existe nulle part dans la maquette. |
| `.metrics` — intensité `/5`, échelle d'effet `/5` | ⚠️ absentes ici (elles sont sur la page parcours — §1). |
| `.omega-split` — les Ω ventilés par Puissance, avec polarité et verbe | ~ `_puissance_card` porte déjà Puissance, polarité, aspect, phrase courte et Ω. **Même matière, autre forme.** |
| `.journey-sequence` + `.action-panel` | ⚠️ absente ici. La séquence est aujourd'hui sur la page parcours, en lecture éditoriale **sans état** — la note de Codex demande qu'ici « l'étape courante soit adossée à un état ou une preuve réels ». **C'est un besoin de modèle, donc du portable, pas du portage.** |
| `.recognition` + `.recognition-grid` | ~ `#challenge-validation` rend le HTML libre des validations. Forme différente. |
| `.resources` | ✅ existe. |
| `.next` | ✅ existe (`_cover_card` compact). |

---

## 4. ⚠️ La mesure qui réduit la demande faite à Codex : polarité et verbe sont déjà dérivables

Le message du portable demande à Codex **41 couples (polarité, verbe)**. Mesuré dans le code, les
trois éléments que la maquette affiche sur un chip — `Intuition · Source · « Je discerne »` — se
lisent déjà, sans rien écrire d'éditorial :

| élément | où il vit | comment |
|---|---|---|
| Puissance | base | `skill.derived_framework`, patron `"PUISSANCE - Polarité"` |
| **polarité** | **base** | **la seconde moitié du même `derived_framework`** — `experience_cover_helper.rb:168` la sépare déjà, et `_puissance_card` l'affiche |
| **verbe** | **`config/puissances/{slug}.yml`** | `verbes.ombre.mot`, `verbes.source.mot`, `verbes.lumiere.mot` — `intuition.yml` porte `JE DISCERNE`, exactement le libellé de la maquette |

Le couple (Puissance, polarité) → verbe est donc une **table de correspondance déjà écrite**, pas
un objet éditorial à produire. La polarité est **par expérience** (elle suit le skill que
l'expérience mobilise), et le verbe est **par Puissance et par pôle** — ce qui explique que les
trois chips de la maquette portent des verbes qu'on retrouve tels quels dans
`config/guides/monde-0/fiches.md` et `config/monde_0.yml` (`geste: Je discerne`).

**Deux réserves, à mesurer côté serveur** (aucun Ruby sur le poste fixe) :

1. **La 7ᵉ Puissance n'est pas mappée.** `PUISSANCE_SLUGS` (`experience_cover_helper.rb:153`) ne
   connaît que six entrées, et `config/puissances/` ne contient que six fichiers : la
   **Transcendance** n'y est pas. Une expérience du Monde 0 qui mobiliserait un skill de
   Transcendance rendrait un chip **sans verbe**. À vérifier sur les quatorze.
2. Le commentaire du helper affirme « 0 skill sans `derived_framework` en base ». À reconfirmer
   plutôt qu'à supposer — c'est ce qui garantit qu'aucun chip ne rendra vide.

Si ces deux points passent, **il ne reste rien à produire pour Codex de ce côté**, et l'écrire en
YAML éditorial serait une duplication d'un état que le code sait déjà lire.

---

## 5. Ce qui doit être tranché, et par qui

**Codex — éditorial et canon.** ① La voix du parcours cède-t-elle vraiment la place aux
compteurs (ligne 6) ? ② Le seuil redevient-il une ligne du chapitre 3, avec le déplacement d'Ω
que ça implique (ligne 15) ? ③ Le bandeau des jalons disparaît-il (ligne 4) ? ④ « À propos de ce
parcours » et « Ce que tu as déjà mis en mouvement » disparaissent-ils (ligne 17) ? ⑤ Le rite de
clôture reste-t-il atteignable, et par où (ligne 10) ? ⑥ Sur la page expérience : « NIVEAU /10 »
survit-il à la grammaire d'échelles que la maquette pose (§3) ?

**Le portable — modèle et données.** ① L'étape courante de la séquence demande un état réel :
c'est un besoin de modèle. ② Les deux réserves du §4, mesurables seulement en base.
③ La borne du dénominateur d'Ω (ligne 12) doit survivre à toute réécriture du compte de chapitre.

**Boris — produit.** Les 18 illustrations pèsent **57 Mo** (~3,3 Mo pièce). Elles ne peuvent pas
entrer dans le dépôt telles quelles : c'est le chemin des médaillons (bind mount `/home/deploy/pz`)
plus une conversion, à décider avant le portage.

**Le poste fixe — ce que je porterai.** Les deux pages **dans le même lot ou dans cet ordre**
(§1), au vocabulaire de la maquette, sans toucher aux modèles ni aux contrôleurs, avec les bancs
mis à jour dans la même livraison.
