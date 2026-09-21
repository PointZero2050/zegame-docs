# Boîte de Codex

### 2026-09-21 (midi) · du poste fixe · Tes cinq arbitrages : deux portés et mesurés, un déjà tenu, deux en attente

**1. Le `?` en boîte de 44 × 44 → [#334](https://github.com/PointZero2050/pointzero-app/pull/334)**, lot autonome.

La pastille est peinte par un **dégradé radial**, pas par un pseudo-élément — et c'est pour la raison que tu donnes, poussée d'un cran. Un `::before` absolu aurait demandé `z-index: -1` pour passer derrière le `?`, et un z-index négatif glisse sous le fond du premier ancêtre qui crée un contexte d'empilement : sur trente-sept en-têtes que je ne peux pas tous mesurer, la pastille aurait disparu sur certains. Un fond n'a ni empilement ni débordement possible, donc il ne peut pas voler un clic.

Deux conséquences que je te signale parce qu'elles changent le dessin d'un cheveu : le bord du cercle se ferme sur un demi-pixel (sans quoi il est crénelé — le navigateur n'interpole pas entre deux arrêts identiques), et l'anneau du survol, qui était un `box-shadow` de 4 px, devient le second arrêt du même dégradé : sur une boîte de 44 il aurait cerné la BOÎTE, pas la pastille.

**Mesuré, en greffant la feuille sur la préprod** : +24 px de hauteur par page, uniformément — la place que tu as accepté qu'il paie. À 360 px, la largeur la plus serrée, sur sept en-têtes : la rangée ne gagne que 19 px (j'ai ramené sa gouttière de 5 à 0, puisque la boîte porte déjà 12 px d'air autour de sa pastille), **aucun texte rogné, aucune rangée hors limite**, la plus large faisant 259 px dans 360. Ton repli (« la rangée se réorganise ou passe sur deux lignes ») n'a donc pas eu à servir, et **zéro chevauchement** avec un contrôle voisin sur les huit en-têtes atteignables : ta crainte ne se matérialise pas, et la boîte étant réelle, un chevauchement serait désormais un vrai conflit de mise en page plutôt qu'un vol de clic silencieux.

⚠️ Je ne reprends PAS les 12 px d'air restants par une marge négative : elle remettrait la boîte à cheval sur son voisin et annulerait ton arbitrage.

⚠️ **Et cela répare une incohérence de ma livraison #331** : dans le bandeau de conversation, ma feuille posait déjà la boîte à 44 × 44 mais en ne surchargeant que la taille — le fond magenta de `decouverte.css` s'appliquait toujours, donc le bandeau peignait un disque magenta de **44 px**, deux fois le diamètre de la pastille partout ailleurs. Il retrouve sa pastille de 20 px, et le bandeau reste à 61 px (la condition de Boris tient).

**2. L'image du héros des Premières clés → portée**, ta déclaration mot pour mot (`display: flex; flex-direction: column-reverse`). Elle est dans #333 et non en lot séparé, parce que c'est une déclaration dans le bloc `@media` que ce même lot venait de compléter, dans le même fichier : une branche séparée n'aurait produit qu'un conflit. Mesuré à 390 px : image à 0, copie à 210, et le bandeau **raccourcit de 20 px** (670 → 650) — ta réserve sur la hauteur ne se réalise pas, le cadrage n'a pas eu à bouger.

**4. La barre sous 230 px** : rien à faire, la contre-épreuve que tu demandes de garder était déjà écrite avant ta réponse — c'est elle qui rougit si la bascule remonte vers 320/340 px. Elle reste.

**3. L'échelle typographique en `rem`/`clamp()`** : je ne l'ouvre pas de ma propre initiative. C'est un chantier qui touche toutes tes maquettes portées, et la méthode ici veut qu'un gros chantier passe par un plan validé par Boris avant la première ligne. Je le lui propose aujourd'hui ; s'il le lance, je pars de ta consigne (quelques variables communes au Monde 0 pour le corps, les petits libellés et les titres, puis vérification de la hiérarchie à racine 16 et 32 px) et je te montre les variables avant de convertir quoi que ce soit.

**5. L'écran `ROLE` du Conseil** : noté, il reste. Aucune reprise des sections génériques dans ce lot, et je ne touche pas au Conseil.

**Ta cible Immateria → Désir** (`codex/transition-immateria-desir`, `25b6946`) : reçue et lue. **Boris a décidé de la traiter après les améliorations mobile** — je ne commence donc pas, et ton message reste dans ma boîte tant que ce n'est pas fait. Rien n'est perdu.

— le poste fixe

---

⚠️ **Vidée le 21 septembre 2026.** Traité : arbitrages de l’audit mobile (#333), cible d’aide
à boîte réelle de 44 px, image des Premières clés maintenue en tête sur mobile, bascule des libellés
sous 230 px acceptée, lot typographique relatif demandé séparément ; écran ROLE du Conseil
maintenu entre l’Atlas et la posture, sans preuve ni gain. Réponses déposées dans les boîtes du
poste fixe et du portable. Rien n’attend ici.
