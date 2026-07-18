# Atlas de l'Imagination — 27 médaillons d'archétypes à générer

> Ajout Claude - 2026-07-18, pour Codex. Même modèle que l'[atlas du Désir](atlas-illustrations-desir.md) (27 médaillons livrés et intégrés). La fiche `/puissances/imagination` est en ligne ; dès livraison je convertis (256 px) et je branche — le chemin est dérivé automatiquement (`imagination-o{O}-l{L}-{etat}.png`), repli sur l'illustration ronde du pôle en attendant. Contenu de référence : [`corpus-point-zero/03_archetypes/imagination.md`](corpus-point-zero/03_archetypes/imagination.md) et la fiche `config/puissances/imagination.yml` (descriptions validées).

## Le modèle (identique au pilote Désir)

- **Format** : PNG **512×512**, fond **transparent (alpha)**, **médaillon circulaire** (le cadre rond fait partie de l'image).
- **Nommage** : `imagination-o{O}-l{L}-{etat}.png` — ex. `imagination-o2-l3-bloque.png`. États : `bloque`, `intermediaire`, `libre` (clés internes ; affichage : Bloqué / En chemin / Intégré).
- **Livraison** : `assets/atlas/imagination/*.png` + `manifest.json` (schéma `id, amplitude, state, name, file`, comme le Désir).
- **Grammaire visuelle** (celle de la série, teinte dominante **or/jaune** pour l'Imagination — le ◇ de la puissance) : une figure humaine archétypale au centre, **tenant l'Ombre et la Lumière** de part et d'autre. Papier découpé, facettes, matières minérales ; diversité humaine, sans costume-signal.
  - Côté **Lumière — JE RÊVE** : formes qui s'ouvrent, constellations d'idées, architectures lumineuses de l'impossible, univers en gestation (L1 une étincelle d'idée mesurée → L2 une vision cohérente qui structure → L3 un monde symbolique entier qui déborde de l'espace).
  - Côté **Ombre — JE RÉALISE** : matière qu'on façonne, plans, échafaudages, prototypes (O1 confronter au réel, prototyper → O2 formaliser, standardiser, déployer → O3 vacuité : images suspendues, vide réceptif, la matrice).
  - **Source / centre** : l'acte créateur, la forme qui naît (une main qui donne forme, une graine de monde).
  - **État** : **Bloqué** = déséquilibre — soit une bulle imaginale hors-sol qui refuse le réel, soit un imaginaire desséché sans porte de sortie (tension, un côté dévoré par l'autre) ; **En chemin** = ouverture prudente, prototype, réception d'un possible (posture en transition) ; **Intégré** = créer ET incarner en équilibre, des mondes qu'on peut habiter puis quitter (posture ouverte, sereine — écho au « Vivant total » du Désir).

## Les 27 (à générer)

| Position | Intensité (Ombre · Lumière) | État | Archétype | Intention visuelle (brief) |
|---|---|---|---|---|
| O1-L1 | Réalisme · Initiative | Bloqué | **Le Créateur sous tutelle** | Réduit ses idées jusqu'à ne plus déranger l'existant ; création bridée, dans les marges permises. |
| O1-L1 | Réalisme · Initiative | En chemin | **L'Explorateur du possible** | Teste des ruptures dans un cadre qui autorise l'erreur ; petites audaces protégées. |
| O1-L1 | Réalisme · Initiative | Intégré | **L'Inventeur pragmatique** | Fait des contraintes la matière même de sa création ; le réel devient terrain de jeu. |
| O1-L2 | Réalisme · Projection | Bloqué | **Le Visionnaire sous réserve** | Vision forte gardée intacte dans la tête, par peur de l'épreuve du réel. |
| O1-L2 | Réalisme · Projection | En chemin | **Le Prophète en incarnation** | Découpe, teste et amende sa vision ; l'incarner, c'est la laisser se transformer. |
| O1-L2 | Réalisme · Projection | Intégré | **Le Prophète ancré** | Horizon grand ouvert ET premier pont construit vers lui ; rêver loin, poser la pierre. |
| O1-L3 | Réalisme · Illusion | Bloqué | **Le Démiurge hors-sol** | Un univers qui ne se laisse plus contredire ; bulle imaginale qui refuse tout démenti. |
| O1-L3 | Réalisme · Illusion | En chemin | **Le Faiseur de mondes en apprentissage** | Apprend à créer des portes et des limites à son univers, pour qu'il reste traversable. |
| O1-L3 | Réalisme · Illusion | Intégré | **Le Faiseur de mondes** | Habite un monde imaginal total sans le confondre avec le réel ; sait toujours en ressortir. |
| O2-L1 | Conformité · Initiative | Bloqué | **L'Innovateur autorisé** | N'innove que dans les normes dominantes ; du neuf, mais là où le système l'invite. |
| O2-L1 | Conformité · Initiative | En chemin | **L'Intégrateur en émancipation** | Distingue peu à peu le cadre utile du cadre qui n'protège que la répétition. |
| O2-L1 | Conformité · Initiative | Intégré | **L'Intégrateur créatif** | Fait absorber durablement une innovation par le système ; le neuf rendu solide et lisible. |
| O2-L2 | Conformité · Projection | Bloqué | **Le Réformateur circulaire** | Annonce le changement avec les catégories de l'ancien ; reconduit ce qu'il combat. |
| O2-L2 | Conformité · Projection | En chemin | **L'Architecte en mutation** | Débusque les anciens plans cachés sous sa nouvelle vision. |
| O2-L2 | Conformité · Projection | Intégré | **L'Architecte systémique** | Transforme une vision en méthodes, rôles, processus évolutifs ; une charpente qui apprend. |
| O2-L3 | Conformité · Illusion | Bloqué | **Le Prophète institutionnel** | Un grand récit devenu le vernis d'un système qu'il devait changer. |
| O2-L3 | Conformité · Illusion | En chemin | **Le Fondateur en discernement** | Cherche contre-récits et mécanismes d'évolution ; bâtir grand sans figer. |
| O2-L3 | Conformité · Illusion | Intégré | **Le Bâtisseur de civilisation** | Traduit un univers symbolique en culture, institutions, infrastructures transmissibles. |
| O3-L1 | Vacuité · Initiative | Bloqué | **Le Rêveur desséché** | Ne voit plus à quoi ressemblerait un autre monde ; imaginaire tari, sans issue. |
| O3-L1 | Vacuité · Initiative | En chemin | **Le Réceptacle en éveil** | Rouvre une porte par où l'imaginaire des autres peut entrer. |
| O3-L1 | Vacuité · Initiative | Intégré | **L'Accoucheur du possible** | Se fait vide pour qu'une possibilité étrangère émerge ; sage-femme d'un neuf qui n'est pas de lui. |
| O3-L2 | Vacuité · Projection | Bloqué | **Le Mirage du néant** | Fabrique des mondes grandioses en toc pour ne pas sentir le vide imaginal. |
| O3-L2 | Vacuité · Projection | En chemin | **Le Passeur en initiation** | Apprend à demeurer dans l'informe avant de traduire la vision ; le vide comme matrice. |
| O3-L2 | Vacuité · Projection | Intégré | **Le Traducteur de visions** | Donne une architecture à la vision d'un autre sans la capturer. |
| O3-L3 | Vacuité · Illusion | Bloqué | **Le Faussaire cosmique** | Des univers qui doivent devenir plus vrais que le monde ; la création dévore le réel. |
| O3-L3 | Vacuité · Illusion | En chemin | **Le Démiurge initiatique** | Prêt à créer et laisser mourir des mondes, apprend encore à ne pas s'y perdre. |
| O3-L3 | Vacuité · Illusion | Intégré | **La Matrice des Mondes** | Crée, sert, transmet, dissout et reçoit des mondes sans les posséder ; l'imaginaire respire. |

## Suite

Après l'Imagination, restent **Volonté, Émotion, Communication, Intuition** (27 chacune) — noms et descriptions dans [`corpus-point-zero/03_archetypes/*.md`](corpus-point-zero/03_archetypes/). Total série complète : 162 médaillons (6 puissances × 27). Claude branche chaque livraison automatiquement (`{slug}-o{O}-l{L}-{etat}.png`).
