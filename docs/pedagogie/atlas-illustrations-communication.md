# Atlas de la Communication — série complète de 27 médaillons

> Ajout Codex - 2026-07-18. Les 27 médaillons ont été produits avec OpenAI, détourés, normalisés en PNG RGBA 512 x 512 et livrés dans [`assets/atlas/communication/`](assets/atlas/communication/). Le mapping machine est disponible dans le [`manifest.json`](assets/atlas/communication/manifest.json).

> Brief initial Claude - 2026-07-18. Même modèle que les atlas précédents. La fiche `/puissances/communication` dérive automatiquement le chemin `communication-o{O}-l{L}-{etat}.png`. Contenu de référence : [`corpus-point-zero/03_archetypes/communication.md`](corpus-point-zero/03_archetypes/communication.md) et la fiche `config/puissances/communication.yml`.

## Le modèle (identique aux pilotes précédents)

- **Format** : PNG **512×512**, fond **transparent (alpha)**, **médaillon circulaire** (le cadre rond fait partie de l'image).
- **Nommage** : `communication-o{O}-l{L}-{etat}.png` — ex. `communication-o2-l3-bloque.png`. États : `bloque`, `intermediaire`, `libre` (clés internes ; affichage : Bloqué / En chemin / Intégré).
- **Livraison** : `assets/atlas/communication/*.png` + `manifest.json` (schéma `id, amplitude, state, name, file`, comme le Désir).
- **Signe de série** : deux arcs de papier ouverts se font face autour d'un intervalle central, avec un point dans chaque ouverture. Ce canal relie visuellement écoute et expression sans recourir à la bulle de dialogue.
- **Grammaire visuelle** (celle de la série, teinte dominante **bleu gorge** pour la Communication — chakra 5) : une figure humaine archétypale au centre, **tenant l'Ombre et la Lumière** de part et d'autre. Papier découpé, facettes, matières minérales ; diversité humaine, sans costume-signal.
  - Côté **Lumière — JE CAPTIVE** (persuasion, séduction, envoûtement) : la parole qui rayonne, ondes sonores, la bouche/le souffle qui porte, l'auditoire attiré (L1 Persuasion : arguments clairs, un trait net qui relie → L2 Séduction : un récit qui enroule et attire, des volutes → L3 Envoûtement : la parole magnétique qui transforme la perception d'une foule, un halo hypnotique).
  - Côté **Ombre — J'ÉCOUTE** (écoute, effacement, silence) : l'oreille qui reçoit, la signature retirée, la bouche close/le doigt sur les lèvres (O1 Écoute : recevoir et reformuler, deux figures reliées par l'écoute → O2 Effacement : porter la parole d'un autre, une figure qui s'estompe pour amplifier une voix → O3 Silence : suspendre le langage, un espace vide protecteur, un secret gardé).
  - **Source / centre** : l'acte de rendre partageable — une figure sereine, souffle/verbe équilibré entre dire, écouter et se taire.
  - **État** : **Bloqué** = déséquilibre — soit une parole qui capture/manipule (envoûtement, charme anxieux, oracle opaque), soit un silence subi/une voix confisquée (le silencieux blessé, le porte-parole sans voix) ; **En chemin** = la circulation s'amorce, l'un ose porter sa parole, l'autre apprend à se taire et écouter (posture en transition) ; **Intégré** = exprimer ET recevoir en équilibre — faire naître un monde par la parole puis se taire pour le rendre libre (posture ouverte, sereine — écho au « Verbe total »).

## Les 27 livrés

| Position | Intensité (Ombre · Lumière) | État | Archétype | Intention visuelle (brief) |
|---|---|---|---|---|
| O1-L1 | Écoute · Persuasion | Bloqué | **Le Débatteur défensif** | Écoute pour préparer sa réponse et protéger sa position ; le dialogue est un duel. |
| O1-L1 | Écoute · Persuasion | En chemin | **Le Dialoguant en éveil** | Accepte que la conversation transforme sa pensée ; écouter peut le faire changer d'avis sans le diminuer. |
| O1-L1 | Écoute · Persuasion | Intégré | **Le Verbe réciproque** | Parle pour être compris et écoute pour découvrir ce que sa parole ignorait ; l'échange le nourrit. |
| O1-L2 | Écoute · Séduction | Bloqué | **Le Charmeur inquiet** | S'adapte aux attentes pour obtenir adhésion ; séduit par peur du rejet plus que par désir de relier. |
| O1-L2 | Écoute · Séduction | En chemin | **Le Narrateur en réciprocité** | Apprend à toucher sans fabriquer un personnage ; il peut plaire en restant lui-même. |
| O1-L2 | Écoute · Séduction | Intégré | **Le Charmeur attentif** | Rend son message désirable en restant ouvert à l'effet produit ; séduit sans manipuler, l'autre reste libre. |
| O1-L3 | Écoute · Envoûtement | Bloqué | **Le Tribun captif** | Cherche l'adhésion, vit la contradiction comme une rupture ; a besoin de subjuguer pour exister. |
| O1-L3 | Écoute · Envoûtement | En chemin | **L'Orateur en résonance** | Apprend que l'impact ne garantit ni vérité ni consentement ; émouvoir une foule n'est pas la convaincre justement. |
| O1-L3 | Écoute · Envoûtement | Intégré | **L'Orateur magnétique** | Transforme l'espace par la parole sans réduire l'auditoire au rôle de réceptacle ; soulève sans capturer. |
| O2-L1 | Effacement · Persuasion | Bloqué | **Le Porte-parole sans voix** | Défend les autres mais ne formule jamais sa propre position ; porte toutes les paroles sauf la sienne. |
| O2-L1 | Effacement · Persuasion | En chemin | **Le Messager en affirmation** | Distingue la parole qu'il transmet de la sienne ; réapprend qu'il a, lui aussi, quelque chose à dire. |
| O2-L1 | Effacement · Persuasion | Intégré | **Le Porte-parole fidèle** | Prête sa voix sans la perdre ; porte la parole d'un autre avec loyauté tout en pouvant parler en son nom. |
| O2-L2 | Effacement · Séduction | Bloqué | **Le Caméléon relationnel** | S'adapte si bien qu'il ne sait plus qui parle en lui ; à force d'épouser toutes les formes, il a perdu la sienne. |
| O2-L2 | Effacement · Séduction | En chemin | **Le Médiateur en incarnation** | Traduit entre les parties sans devenir le produit de la relation ; reste quelqu'un en servant le lien. |
| O2-L2 | Effacement · Séduction | Intégré | **Le Maïeuticien juste** | Aide l'autre à découvrir et formuler sa propre parole ; accouche ce que l'autre portait sans le dire. |
| O2-L3 | Effacement · Envoûtement | Bloqué | **Le Miroir ensorcelant** | Renvoie au groupe son propre désir pour capter l'autorité de parler en son nom ; flatte pour devenir sa voix. |
| O2-L3 | Effacement · Envoûtement | En chemin | **Le Héraut en discernement** | Apprend à porter un récit collectif sans se l'approprier ; servir une voix commune n'est pas la confisquer. |
| O2-L3 | Effacement · Envoûtement | Intégré | **Le Porte-Verbe collectif** | Donne une voix puissante à une pluralité sans l'effacer ; fait entendre un ensemble sans le réduire à lui. |
| O3-L1 | Silence · Persuasion | Bloqué | **Le Silencieux blessé** | Retient sa parole car elle lui semble dangereuse ou irrecevable ; son silence est une cicatrice, non un choix. |
| O3-L1 | Silence · Persuasion | En chemin | **Le Messager libéré** | Retrouve peu à peu une parole longtemps interdite ; ose de nouveau, prudemment, ce qu'il taisait par peur. |
| O3-L1 | Silence · Persuasion | Intégré | **Le Gardien de l'indicible** | Sait ce qui doit rester tu et le moment où le silence doit s'ouvrir ; son mutisme est une garde, non une fuite. |
| O3-L2 | Silence · Séduction | Bloqué | **Le Séducteur muet** | Utilise le mystère et l'inaccessibilité pour contrôler la relation ; tient l'autre par ce qu'il ne dit pas. |
| O3-L2 | Silence · Séduction | En chemin | **Le Mystère en ouverture** | Apprend à devenir lisible sans perdre la profondeur du silence ; se montre un peu sans se croire vidé de son aura. |
| O3-L2 | Silence · Séduction | Intégré | **Le Maître de la présence** | Communique par le corps, le rythme et des mots rares sans créer de confusion ; sa présence parle plus fort que ses phrases. |
| O3-L3 | Silence · Envoûtement | Bloqué | **L'Oracle opaque** | Alterne parole absolue et silence impénétrable pour renforcer son autorité ; règne par ce qu'on ne saisit jamais de lui. |
| O3-L3 | Silence · Envoûtement | En chemin | **Le Verbe initiatique** | Apprend à créer et dissoudre les récits sans confondre mystère et pouvoir ; traverse le dire et le taire comme une épreuve. |
| O3-L3 | Silence · Envoûtement | Intégré | **Le Verbe total** | Fait naître un monde par la parole, puis se tait pour le rendre libre ; dit sans capturer, se tait sans abandonner. |

## Suite

Après la Communication, reste **Intuition** (27) — noms et descriptions dans [`corpus-point-zero/03_archetypes/intuition.md`](corpus-point-zero/03_archetypes/intuition.md). Ce sera la dernière des six puissances polaires du Moteur. Claude branche chaque livraison automatiquement (`{slug}-o{O}-l{L}-{etat}.png`).
