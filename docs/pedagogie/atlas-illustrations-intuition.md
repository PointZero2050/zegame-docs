# Atlas de l'Intuition — 27 médaillons d'archétypes à générer

> Ajout Claude - 2026-07-18, pour Codex. **Dernière des six puissances polaires du Moteur.** Même modèle que les atlas [Désir](atlas-illustrations-desir.md), [Volonté](atlas-illustrations-volonte.md), [Imagination](atlas-illustrations-imagination.md), [Émotion](atlas-illustrations-emotion.md) (livrés, intégrés) et [Communication](atlas-illustrations-communication.md) (en génération). La fiche `/puissances/intuition` est en ligne ; dès livraison je convertis (256 px) et je branche — chemin dérivé automatiquement (`intuition-o{O}-l{L}-{etat}.png`), repli sur l'illustration ronde du pôle en attendant. Contenu de référence : [`corpus-point-zero/03_archetypes/intuition.md`](corpus-point-zero/03_archetypes/intuition.md) et la fiche `config/puissances/intuition.yml` (descriptions validées).

## Le modèle (identique aux pilotes précédents)

- **Format** : PNG **512×512**, fond **transparent (alpha)**, **médaillon circulaire** (le cadre rond fait partie de l'image).
- **Nommage** : `intuition-o{O}-l{L}-{etat}.png` — ex. `intuition-o2-l3-bloque.png`. États : `bloque`, `intermediaire`, `libre` (clés internes ; affichage : Bloqué / En chemin / Intégré).
- **Livraison** : `assets/atlas/intuition/*.png` + `manifest.json` (schéma `id, amplitude, state, name, file`, comme le Désir).
- **Grammaire visuelle** (celle de la série, teinte dominante **indigo 3e œil** pour l'Intuition — chakra 6) : une figure humaine archétypale au centre, **tenant l'Ombre et la Lumière** de part et d'autre. Papier découpé, facettes, matières minérales ; diversité humaine, sans costume-signal.
  - Côté **Lumière — JE CROIS** (conviction, certitude, foi totale) : l'œil qui voit clair, l'étoile/la boussole qui oriente, la carte tracée, la flamme d'une vérité (L1 Conviction : une orientation crédible, un cap qui se dessine → L2 Certitude : une carte stable et structurée, une constellation fixée → L3 Foi totale : un soleil intérieur, un engagement absolu, au risque du dogme aveuglant).
  - Côté **Ombre — JE DOUTE** (ouverture, suspension, non-savoir) : la carte qu'on repose, les hypothèses tenues en suspens, la brume/le vide fertile (O1 Ouverture : accueillir une anomalie, une porte entrouverte → O2 Suspension : plusieurs fils tenus ensemble, une balance d'hypothèses → O3 Non-savoir : abandon des cartes et des catégories, un espace vide et ouvert d'où un paradigme neuf peut surgir).
  - **Source / centre** : l'acte de connaître — un œil serein, une figure qui discerne la cohérence au-delà des apparences, équilibrée entre croire et douter.
  - **État** : **Bloqué** = déséquilibre — soit une certitude fermée/dogmatique qui n'entend plus rien (l'inquisiteur, le certain courtois), soit un doute qui désoriente et paralyse (le chercheur perdu, l'enquêteur paralysé) ; **En chemin** = la circulation s'amorce, l'un accepte de réviser sa carte, l'autre retrouve un fil après la perte des repères (posture en transition) ; **Intégré** = croire ET douter en équilibre — tout consacrer à une vérité puis abandonner toute prétention à la posséder (posture claire, paisible — écho au « Clairvoyant paisible »).

## Les 27 (à générer)

| Position | Intensité (Ombre · Lumière) | État | Archétype | Intention visuelle (brief) |
|---|---|---|---|---|
| O1-L1 | Ouverture · Conviction | Bloqué | **Le Convaincu conditionnel** | Suit une orientation fragile, change de cap selon les voix les plus assurées autour de lui. |
| O1-L1 | Ouverture · Conviction | En chemin | **L'Explorateur d'hypothèses** | Avance avec une hypothèse sans la confondre avec la vérité ; ose s'orienter en sachant qu'il peut se tromper. |
| O1-L1 | Ouverture · Conviction | Intégré | **L'Éclaireur ouvert** | Choisit une direction et reste attentif à ses angles morts ; sa conviction éclaire sans aveugler. |
| O1-L2 | Ouverture · Certitude | Bloqué | **Le Certain courtois** | Écoute poliment les objections sans qu'elles modifient son système ; rien n'entame vraiment sa carte. |
| O1-L2 | Ouverture · Certitude | En chemin | **Le Savant en révision** | Accepte de toucher aux fondations de sa carte ; un savoir solide peut se corriger sans s'effondrer. |
| O1-L2 | Ouverture · Certitude | Intégré | **Le Cartographe vivant** | Structure et transmet un savoir en le maintenant révisable ; la carte n'est jamais confondue avec le territoire. |
| O1-L3 | Ouverture · Foi totale | Bloqué | **Le Missionnaire bienveillant** | Intègre toutes les voies comme étapes vers sa propre vérité ; ouvert en apparence, il ramène tout au sien. |
| O1-L3 | Ouverture · Foi totale | En chemin | **Le Fidèle en dialogue** | Conserve sa foi sans nier les expériences irréductibles à son système ; tient sa vérité sans effacer les autres. |
| O1-L3 | Ouverture · Foi totale | Intégré | **L'Humble Hiérophante** | Témoigne intensément de sa vérité sans l'universaliser ; foi brûlante, et à chacun son chemin. |
| O2-L1 | Suspension · Conviction | Bloqué | **L'Enquêteur paralysé** | Ajoute indéfiniment des hypothèses pour éviter de conclure ; enquêter devient une façon de ne jamais trancher. |
| O2-L1 | Suspension · Conviction | En chemin | **Le Pèlerin des Limbes** | Tient une longue traversée sans réponse et perçoit un premier fil ; supporte le doute assez pour qu'un sens émerge. |
| O2-L1 | Suspension · Conviction | Intégré | **L'Enquêteur orienté** | Suit une piste assez longtemps pour l'éprouver sans en prédéterminer le résultat ; engagé mais prêt au démenti. |
| O2-L2 | Suspension · Certitude | Bloqué | **Le Procès sans verdict** | Reconstruit sans cesse une certitude plus complexe pour éviter l'incertitude ; complexifie plutôt que d'affronter le vide. |
| O2-L2 | Suspension · Certitude | En chemin | **Le Discernant initié** | Distingue ce qu'il sait, ce qu'il suppose et ce qu'il laisse ouvert ; range ses savoirs selon leur solidité. |
| O2-L2 | Suspension · Certitude | Intégré | **Le Cartographe critique** | Formalise un savoir pour qu'il soit vérifié, contesté, amélioré ; sa rigueur invite la critique au lieu de la craindre. |
| O2-L3 | Suspension · Foi totale | Bloqué | **L'Inquisiteur méthodique** | Utilise la rigueur de la recherche pour confirmer une vérité déjà absolue ; la méthode habille sa certitude. |
| O2-L3 | Suspension · Foi totale | En chemin | **Le Révélateur en discernement** | Soumet sa vision à l'épreuve sans la réduire à une opinion ; y croit fort tout en l'exposant à l'examen. |
| O2-L3 | Suspension · Foi totale | Intégré | **Le Gardien de la vérité vivante** | Consacre sa vie à un principe tout en critiquant ses formulations et institutions ; sert sans figer les formes. |
| O3-L1 | Non-savoir · Conviction | Bloqué | **Le Chercheur perdu** | Ne sait plus distinguer signe, projection et vérité ; le non-savoir l'a désorienté, tout semble également possible. |
| O3-L1 | Non-savoir · Conviction | En chemin | **Le Discernant renaissant** | Retrouve un premier fil sans en faire une doctrine ; après la perte des repères, réapprend à s'orienter. |
| O3-L1 | Non-savoir · Conviction | Intégré | **Le Veilleur du mystère** | Peut ne plus rien savoir puis accueillir une orientation modeste ; le vide ne l'effraie plus, il y veille. |
| O3-L2 | Non-savoir · Certitude | Bloqué | **L'Oracle intermittent** | Passe du vide à des certitudes soudaines investies comme absolues ; oscille entre néant et révélations. |
| O3-L2 | Non-savoir · Certitude | En chemin | **Le Sage en déconstruction** | Laisse mourir un paradigme sans précipiter le suivant ; habite l'entre-deux sans combler trop vite le vide. |
| O3-L2 | Non-savoir · Certitude | Intégré | **Le Passeur de paradigmes** | Déconstruit une architecture de savoir et rend une nouvelle carte transmissible ; traverse la nuit pour rapporter du neuf. |
| O3-L3 | Non-savoir · Foi totale | Bloqué | **L'Absolutiste vacillant** | Oscille entre foi totale et effondrement de tout sens ; passe de la vérité absolue au gouffre sans milieu. |
| O3-L3 | Non-savoir · Foi totale | En chemin | **Le Prophète initiatique** | Prêt à traverser révélation et nuit du non-savoir, mais avec un cadre exigeant ; les extrêmes le forment sans le briser. |
| O3-L3 | Non-savoir · Foi totale | Intégré | **Le Clairvoyant paisible** | Peut tout consacrer à une vérité puis abandonner toute prétention à la posséder ; connaît sans s'emparer du connu. |

## Fin de série des six puissances polaires

Avec l'Intuition, les **six puissances polaires du Moteur** sont couvertes côté fiches (Désir, Volonté, Imagination, Émotion, Communication, Intuition). Côté médaillons, restent à générer : **Communication** (liste [ici](atlas-illustrations-communication.md)) et **Intuition** (ce document). Claude branche chaque livraison automatiquement (`{slug}-o{O}-l{L}-{etat}.png`). La 7ᵉ puissance, la **Transcendance** (JE DONNE), est non polaire et relève d'un traitement distinct (pas de fiche O-L à ce stade).
