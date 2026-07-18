# Atlas de l'Émotion — 27 médaillons d'archétypes à générer

> Ajout Claude - 2026-07-18, pour Codex. Même modèle que les atlas [Désir](atlas-illustrations-desir.md) (livré, intégré) et [Imagination](atlas-illustrations-imagination.md) (en génération). La fiche `/puissances/emotion` est en ligne ; dès livraison je convertis (256 px) et je branche — chemin dérivé automatiquement (`emotion-o{O}-l{L}-{etat}.png`), repli sur l'illustration ronde du pôle en attendant. Contenu de référence : [`corpus-point-zero/03_archetypes/emotion.md`](corpus-point-zero/03_archetypes/emotion.md) et la fiche `config/puissances/emotion.yml` (descriptions validées).

## Le modèle (identique aux pilotes précédents)

- **Format** : PNG **512×512**, fond **transparent (alpha)**, **médaillon circulaire** (le cadre rond fait partie de l'image).
- **Nommage** : `emotion-o{O}-l{L}-{etat}.png` — ex. `emotion-o2-l3-bloque.png`. États : `bloque`, `intermediaire`, `libre` (clés internes ; affichage : Bloqué / En chemin / Intégré).
- **Livraison** : `assets/atlas/emotion/*.png` + `manifest.json` (schéma `id, amplitude, state, name, file`, comme le Désir).
- **Grammaire visuelle** (celle de la série, teinte dominante **vert cœur** pour l'Émotion — chakra du cœur) : une figure humaine archétypale au centre, **tenant l'Ombre et la Lumière** de part et d'autre. Papier découpé, facettes, matières minérales ; diversité humaine, sans costume-signal.
  - Côté **Lumière — JE VIBRE** (ouverture, résonance) : le cœur qui rayonne, des ondes/fils reliant à l'autre, l'eau/l'océan de la communion (L1 Passion : se laisser toucher, une flamme intime → L2 Fusion : entrer dans le ressenti de l'autre, deux figures qui se confondent → L3 Communion : le cœur ouvert au champ collectif, un océan sans rivage).
  - Côté **Ombre — JE PROTÈGE** (distance, contenance) : la juste distance, le cadre tenu, le givre/cristal protecteur (O1 Détachement : prendre du recul, un pas en arrière serein → O2 Dissociation : contenir et différencier les flux, une membrane, un cadre → O3 Glaciation : suspendre la résonance, un point de calme gelé au cœur de la tempête).
  - **Source / centre** : le cœur vivant qui reçoit et revient au présent (un cœur qui bat, une figure paisible et reliée).
  - **État** : **Bloqué** = déséquilibre — soit submergé/emporté par l'émotion (le côté Lumière déborde et noie), soit coupé/gelé (le côté Ombre a éteint toute résonance) ; **En chemin** = la circulation s'amorce, le dégel ou l'ancrage commence, posture en transition ; **Intégré** = ressentir ET se contenir en équilibre — s'ouvrir puis revenir à soi, entier (posture ouverte, sereine — écho au « Cœur total »).

## Les 27 (à générer)

| Position | Intensité (Ombre · Lumière) | État | Archétype | Intention visuelle (brief) |
|---|---|---|---|---|
| O1-L1 | Détachement · Passion | Bloqué | **Le Sensible sous contrôle** | Ressent, mais garde la main sur le volume ; s'autorise l'émotion à petite dose, de peur d'être emporté. |
| O1-L1 | Détachement · Passion | En chemin | **Le Cœur en apprivoisement** | Découvre que prendre du recul n'oblige pas à couper le ressenti ; apprivoise au lieu de tenir à distance. |
| O1-L1 | Détachement · Passion | Intégré | **Le Témoin sensible** | Ressent pleinement en gardant l'espace pour répondre juste ; la distance éclaire l'émotion au lieu de la couper. |
| O1-L2 | Détachement · Fusion | Bloqué | **L'Empathe inquiet** | Absorbe les émotions des autres jusqu'à saturation ; ne se détache qu'une fois débordé. |
| O1-L2 | Détachement · Fusion | En chemin | **L'Empathe en différenciation** | Apprend à distinguer ce qui vient de lui de ce qu'il capte ; tout ce qu'il ressent ne lui appartient pas. |
| O1-L2 | Détachement · Fusion | Intégré | **L'Empathe ancré** | Ressent avec l'autre sans devenir l'autre ; fusionne le temps d'un lien, puis revient à lui, distinct. |
| O1-L3 | Détachement · Communion | Bloqué | **Le Cœur sans rivage** | S'ouvre sans limites mais confond la moindre distance avec la fin de l'amour ; se perd dans ce qu'il aime. |
| O1-L3 | Détachement · Communion | En chemin | **L'Amoureux océanique en ancrage** | Apprend à revenir à lui après une ouverture totale ; l'océan de la communion ne l'engloutit plus. |
| O1-L3 | Détachement · Communion | Intégré | **Le Cœur océanique** | Communie profondément puis retrouve sa singularité intacte ; l'immensité ne le dissout plus. |
| O2-L1 | Dissociation · Passion | Bloqué | **Le Fonctionnel anesthésié** | Compartimente l'affect pour rester efficace, mais oublie de rouvrir la porte ; l'émotion mise de côté n'est jamais reprise. |
| O2-L1 | Dissociation · Passion | En chemin | **Le Cœur dégelé** | Rouvre peu à peu l'accès à sa sensibilité longtemps sous cloche ; l'affect recommence à circuler. |
| O2-L1 | Dissociation · Passion | Intégré | **Le Contenant sensible** | Suspend son affect le temps de tenir un cadre, puis revient l'accueillir ; contient sans s'anesthésier. |
| O2-L2 | Dissociation · Fusion | Bloqué | **Le Sauveur alternant** | Fusionne avec la souffrance jusqu'à l'épuisement, puis coupe net ; oscille entre tout donner et tout fermer. |
| O2-L2 | Dissociation · Fusion | En chemin | **Le Régulateur en alchimisation** | Apprend à contenir la charge sans l'absorber ni s'en couper ; transforme ce qu'il reçoit au lieu de le subir. |
| O2-L2 | Dissociation · Fusion | Intégré | **Le Régulateur empathique** | Rejoint la tempête d'un autre puis l'aide à regagner la rive ; entre dans le feu sans y brûler. |
| O2-L3 | Dissociation · Communion | Bloqué | **Le Sauveur universel** | Porte la souffrance du monde entier en ignorant ses limites ; sa communion sans discernement le vide. |
| O2-L3 | Dissociation · Communion | En chemin | **Le Grand Cœur en discernement** | Apprend à aimer largement sans se croire responsable de tout ; choisit désormais ce qu'il porte. |
| O2-L3 | Dissociation · Communion | Intégré | **Le Gardien de la communion** | Ouvre le cœur d'un groupe entier tout en contenant et différenciant les flux ; nul ne s'y noie. |
| O3-L1 | Glaciation · Passion | Bloqué | **La Machine mentale** | A suspendu toute vie émotionnelle au profit du fonctionnement ; la glace protège, mais plus rien ne le touche. |
| O3-L1 | Glaciation · Passion | En chemin | **Le Veilleur du dégel** | Laisse quelques émotions revenir sans savoir combien accueillir ; veille au bord du dégel, prudent mais vivant. |
| O3-L1 | Glaciation · Passion | Intégré | **Le Veilleur impassible** | Atteint un calme radical face à l'insupportable, puis laisse l'émotion revenir ; l'impassibilité reste réversible. |
| O3-L2 | Glaciation · Fusion | Bloqué | **L'Amant polaire** | Ne connaît que la fusion totale ou la coupure glacée ; entre l'incandescence et le gel, aucun milieu tenable. |
| O3-L2 | Glaciation · Fusion | En chemin | **Le Cœur en résurrection** | Traverse un hiver relationnel sans conclure que le lien est mort ; le froid peut être une saison, non une fin. |
| O3-L2 | Glaciation · Fusion | Intégré | **Le Régénérateur affectif** | Laisse mourir une forme de lien pour qu'il renaisse autrement ; la glaciation devient un passage, pas une tombe. |
| O3-L3 | Glaciation · Communion | Bloqué | **Le Cœur apocalyptique** | Oscille sans transition entre communion absolue et glaciation totale ; tout-fusion ou grand gel, rien entre. |
| O3-L3 | Glaciation · Communion | En chemin | **L'Amant initiatique** | Prêt à tout ressentir puis tout laisser se taire, s'il est accompagné ; traverse les extrêmes comme une initiation. |
| O3-L3 | Glaciation · Communion | Intégré | **Le Cœur total** | Peut tout ressentir, tout laisser mourir, rouvrir son cœur sans rien retenir ; l'amour circule sans capturer. |

## Suite

Après l'Émotion, restent **Volonté, Communication, Intuition** (27 chacune) — noms et descriptions dans [`corpus-point-zero/03_archetypes/*.md`](corpus-point-zero/03_archetypes/). Claude branche chaque livraison automatiquement (`{slug}-o{O}-l{L}-{etat}.png`).
