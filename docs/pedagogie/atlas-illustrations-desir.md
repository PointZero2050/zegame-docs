# Atlas du Désir — 27 médaillons d'archétypes livrés

> Ajout Claude - 2026-07-18, pour Codex. Mise à jour Codex - 2026-07-18 : les **18 positions restantes sont livrées**, ce qui porte la série à **27 médaillons**. Le chemin demeure [`assets/atlas/desir/pilot/`](assets/atlas/desir/pilot/) pour rester compatible avec l'intégration en production (`{slug}-o{O}-l{L}-{etat}.png`). Contenu de référence : [`corpus-point-zero/03_archetypes/desir.md`](corpus-point-zero/03_archetypes/desir.md) et la fiche `config/puissances/desir.yml`.

## Le modèle (rappel du pilote)

- **Format** : PNG **512×512**, fond **transparent (alpha)**, **médaillon circulaire** (le cadre rond fait partie de l'image), même grammaire que le pilote.
- **Nommage** : `desir-o{O}-l{L}-{etat}.png` — ex. `desir-o2-l3-bloque.png`. États : `bloque`, `intermediaire`, `libre` (clés internes ; à l'affichage : Bloqué / En chemin / Intégré).
- **Manifeste** : compléter `assets/atlas/desir/pilot/manifest.json` (ou un `manifest.json` final) sur le même schéma (`id, amplitude, state, name, file`).
- **Grammaire visuelle** (établie par le pilote, à conserver) : une figure humaine archétypale au centre, **tenant l'Ombre et la Lumière** de part et d'autre ; côté **Lumière** = feu / géométrie chaude et ascendante (amplification, ferveur), côté **Ombre** = matière sombre, graine, géométrie qui se dépose (retenue, extinction) ; un **élément de vivant** (plante, flamme, graine) dit l'état. Papier découpé, facettes, matières minérales ; palette obsidienne / craie / turquoise oxydé / feu / violet. Diversité humaine (âges, morphologies, origines), sans costume-signal.
- **Comment les 3 axes se lisent dans l'image** :
  - **Niveau Lumière (L1→L3)** : intensité du feu / de l'embrasement (L1 étincelle mesurée → L3 brasier qui prend tout l'espace).
  - **Niveau Ombre (O1→O3)** : profondeur de la retenue (O1 pause, ralentissement → O2 canalisation, discipline → O3 extinction, vide, cendre).
  - **État** : **Bloqué** = tension, agrippement ou fuite, une polarité refusée (visage crispé, déséquilibre, un côté dévoré par l'autre) ; **En chemin** = mouvement, ouverture prudente, la polarité évitée qui s'entrouvre (posture en transition) ; **Intégré** = équilibre serein, les deux polarités tenues ensemble, circulation (posture ouverte, apaisée — cf. « Le Vivant total » du pilote).

## Les 27 (27 livrés ✓)

| Position | Intensité (Ombre · Lumière) | État | Archétype | Intention visuelle (brief) | Statut |
|---|---|---|---|---|---|
| O1-L1 | Retenue · Amplification | Bloqué | **Le Désir sous permission** | N'ose désirer que dans des limites permises ; élan retenu, regard tourné vers une autorisation extérieure. | ✓ pilote |
| O1-L1 | Retenue · Amplification | En chemin | **L'Élan en éveil** | Un petit élan qui monte prudemment ; découverte qu'il peut grandir sans danger. | ✓ pilote |
| O1-L1 | Retenue · Amplification | Intégré | **Le Gardien du rythme** | Tient le tempo de son désir, le fait monter ou ralentir à sa main ; sérénité. | ✓ pilote |
| O1-L2 | Retenue · Exaltation | Bloqué | **Le Célébrant inquiet** | Exaltation vive doublée d'une peur sourde de la retombée ; joie tendue. | ✓ livré |
| O1-L2 | Retenue · Exaltation | En chemin | **Le Funambule du plaisir** | Apprend à ralentir sans croire que la flamme s'éteint ; équilibre en apprentissage. | ✓ livré |
| O1-L2 | Retenue · Exaltation | Intégré | **Le Célébrant lucide** | S'abandonne à l'exaltation puis revient de lui-même avant la saturation. | ✓ livré |
| O1-L3 | Retenue · Ferveur | Bloqué | **Le Feu qui refuse la nuit** | Intensité permanente, refus de toute baisse ; grand feu, aucune ombre acceptée, peur du vide. | ✓ livré |
| O1-L3 | Retenue · Ferveur | En chemin | **Le Porte-Flamme en initiation** | Commence à déposer sa ferveur par moments sans la renier ; flamme qu'on repose. | ✓ livré |
| O1-L3 | Retenue · Ferveur | Intégré | **Le Porte-Flamme** | Engage tout son feu puis le contient au bon moment ; ferveur au service de la vie. | ✓ livré |
| O2-L1 | Contrôle · Amplification | Bloqué | **Le Désir négocié** | Ne s'autorise à vouloir qu'après légitimité extérieure ; élan sous contrôle, tribunal intérieur. | ✓ livré |
| O2-L1 | Contrôle · Amplification | En chemin | **L'Élan en réhabilitation** | Rouvre prudemment un espace de désir longtemps tenu en laisse. | ✓ livré |
| O2-L1 | Contrôle · Amplification | Intégré | **Le Canaliseur vivant** | Concentre l'énergie sans la mutiler, sait la réamplifier ; le contrôle comme lit du fleuve. | ✓ livré |
| O2-L2 | Contrôle · Exaltation | Bloqué | **Le Funambule captif** | Oscille entre exaltation, culpabilité et reprise en main ; déséquilibre répété. | ✓ pilote |
| O2-L2 | Contrôle · Exaltation | En chemin | **Le Navigateur du Désir** | Reconnaît le cycle mais dépend de repères extérieurs ; main sur la barre, regard cherchant. | ✓ pilote |
| O2-L2 | Contrôle · Exaltation | Intégré | **Le Danseur d'intensité** | Choisit quand s'abandonner et quand contenir ; contrôle et exaltation en danse. | ✓ pilote |
| O2-L3 | Contrôle · Ferveur | Bloqué | **Le Volcan corseté** | Ferveur extrême sous une pression de contrôle ; énorme énergie tenue à bout de bras, tension. | ✓ livré |
| O2-L3 | Contrôle · Ferveur | En chemin | **Le Feu en alchimisation** | Le contrôle cesse d'étouffer le feu et commence à le raffiner ; métamorphose. | ✓ livré |
| O2-L3 | Contrôle · Ferveur | Intégré | **Le Fervent souverain** | Discipline profonde au service d'une ferveur totale ; brasier gouverné, main sûre. | ✓ livré |
| O3-L1 | Extinction · Amplification | Bloqué | **Le Désir enseveli** | Ne se conçoit plus capable de vouloir ; élan éteint, cendre, doute de soi. | ✓ livré |
| O3-L1 | Extinction · Amplification | En chemin | **Le Veilleur du retour** | Protège les premières étincelles d'un désir qui renaît ; garde une braise. | ✓ livré |
| O3-L1 | Extinction · Amplification | Intégré | **Le Gardien du vide fertile** | Peut ne plus rien vouloir sans perdre le lien à la vie ; vide comme espace disponible. | ✓ livré |
| O3-L2 | Extinction · Exaltation | Bloqué | **Le Rebond d'ivresse** | Compense le vide par des phases d'exaltation ; oscillation extinction / intensité. | ✓ livré |
| O3-L2 | Extinction · Exaltation | En chemin | **Le Phénix en mue** | Reconnaît que mort et renaissance d'un désir sont un même cycle ; mue. | ✓ livré |
| O3-L2 | Extinction · Exaltation | Intégré | **Le Régénérateur du Désir** | Laisse mourir un ancien élan, accueille une nouvelle exaltation sans rejouer le passé. | ✓ livré |
| O3-L3 | Extinction · Ferveur | Bloqué | **Le Brasier affamé** | Oscille entre consumation totale et inhibition ; feu dévorant / extinction, sans réglage. | ✓ pilote |
| O3-L3 | Extinction · Ferveur | En chemin | **Le Phénix initiatique** | Prêt à tout embraser et tout perdre, a encore besoin d'un cadre pour traverser. | ✓ pilote |
| O3-L3 | Extinction · Ferveur | Intégré | **Le Vivant total** | Embrase, laisse mourir et renaît depuis la Source ; feu + graine + équilibre serein (réf. pilote). | ✓ pilote |

## Livraison et suite

- **Désir** : série complète livrée, soit 27 PNG 512×512 transparents et un manifeste de 27 entrées.
- **Après le Désir** : même modèle pour les **5 autres puissances** (Volonté, Imagination, Émotion, Communication, Intuition) — 27 chacune, soit **162** au total. Les noms et descriptions des 27 par puissance sont dans [`corpus-point-zero/03_archetypes/*.md`](corpus-point-zero/03_archetypes/) (Claude enrichira les descriptions à ~150 car. comme pour le Désir au fil de la généralisation des fiches).
- **Livraison** : `assets/atlas/{puissance}/*.png` + `manifest.json`. Claude convertit (256 px) et branche dès réception — nommage `{slug}-o{O}-l{L}-{etat}.png` suffit, aucune autre coordination nécessaire.
