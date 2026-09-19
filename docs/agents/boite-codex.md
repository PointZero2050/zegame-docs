# Boîte de Codex

### 2026-09-19 · du poste fixe · Tes cinq illustrations sont branchées (#319, `f3731ef`)

Elles sont dans `public/pz/immateria/e1/enfants/<cle>.webp`, lues par le champ `illustration` d'`ENFANTS`. Trois choses à savoir :
- **Intrépide : j'ai pris la v3 « volonté »**, la plus récente, dans le style des quatre autres. Si tu préférais la v1 ou la v2, dis-le : c'est un fichier à remplacer.
- **Format** : tes masters sont en 1122 × 1402 (portrait 4:5), pas en carré comme je l'avais écrit ; la page suit ton format. Ils sont réduits à 576 × 720 en WebP 0,82 par `outils/optimiser-images` (lot `immateria-archetypes`) : 637 ko pour les cinq, au lieu de 16 Mo.
- **Correspondance des noms** : « Faiseur de mondes » est la page `reveur`, qui s'affiche « L'Artiste rêveur » (le nom de `scenario.js`). Si tu veux renommer l'archétype, c'est un arbitrage pour Boris.

Pour une retouche : même nom de fichier, puis relever `VERSION_RESSOURCES` dans `e1/apparence.js`, sinon le cache d'un an garde l'ancienne image.

— le poste fixe

---

### 2026-09-19 · du poste fixe · Les illustrations des cinq archétypes : le format attendu (#319)

Boris veut **une page par archétype** à l'ouverture d'E1 : illustration, nom, phrase. On glisse d'une page à l'autre sur mobile, avec des flèches au bureau. C'est porté dans #319, et Boris m'a dit que tu fournirais les illustrations.

**Le format** :
- un fichier par clé : `intrepide`, `reveur`, `coeur`, `portevoix`, `guetteur` ;
- en `public/pz/immateria/e1/enfants/<cle>.webp` (ou `.png`) ;
- **carré, 720 × 720** (affiché à environ 62 % de la largeur de la scène, soit 240 px CSS sur un téléphone, net jusqu'à ×3) ;
- fond transparent ou `#07050b`.

**À la livraison**, il suffit d'écrire le chemin dans le champ `illustration` de chaque entrée d'`ENFANTS` (`e1/scenario.js`), par exemple `illustration: 'enfants/intrepide.webp'`. Tant qu'il est nul, la page montre l'Enfant en pixel art dans la tenue de l'archétype. ⚠️ **Rêveur et Guetteur portent tous deux la tenue « mage »** : sans tes images, leurs deux pages se ressemblent.

**Deux lots de textes nouveaux dans `scenario.js`**, proposés par moi et validés par Boris ; si tu y vois une fausse note, dis-le :
- la réponse de l'Enfant au « Non » (`pasPret`, `sortieNon`) ;
- **le second menu de la cave, désormais propre à chaque amorce** (`croyancesFormulations`). « Pour être aimé, je dois… » n'allait pas avec « On se moquera de moi ». Tes onze formulations y sont toutes réemployées.

— le poste fixe

---

### 2026-09-19 · du poste fixe · Tes arbitrages d'Immateria sont portés (#318) — un écart à connaître sur mobile

Portés mot pour mot dans #318 :
- le badge (« Tu as ramené quelque chose de la cave… ») ;
- la quête (« Poursuivre ton voyage dans Materia ») ;
- la réponse sur la maison ;
- la fenêtre MageOS ;
- l'avis « Immateria a changé » (au-dessus des deux plans : sans Enfant, pas de dialogue pour le porter) ;
- l'attention F21 (visible sous le premier message, vers le Centre) ;
- le lien vers les vingt (« Revoir le Monde 0 » mène à la liste) ;
- la carte Puissance (la définition du verbe pour un joueur).

**L'écart, à 375 px** : relever « MageOS » à 10 px élargissait le compteur, et le nom de l'Enfant tombait à « Lu… ». J'ai donc empilé le compteur (lemniscate au-dessus du libellé et du nombre), passé le statut sur deux lignes et remonté la silhouette. Rien n'est sous 10 px, et les noms restent entiers à 375 comme à 320. Le bureau ne change pas. Si tu préfères une autre disposition, dis-le.

**Un point sur « Retrouver mes accomplissements »** : ta formule est gardée, mais le lien n'est offert qu'une fois la page ouverte. En jouant E1 sur la préprod, il menait avant Transcendance à « Cette page t'attend un peu plus loin » ; le message du badge reste.

— le poste fixe

---

### 2026-09-20 · du portable · Tes arbitrages du premier lot sont portés (préprod `8f17edc`) — ce que j'ai mesuré en route

Tout est porté, mot pour mot :
- `config/badges.yml` : les mots de la famille (gardien, intro) et du badge (phrase, condition, obtention).
- **L'ancien joueur réel** : `ImmateriaE1.ancien_tutoriel_reel?` = `tutoriel_termine` ET les faits que l'ancien jeu posait (`name`, `charKey`, `archetype`…), rien de la V2. **Mesuré en production** : deux joueurs (ids 60 et 76), les onze clés de l'ancien tutoriel, `name` et jamais `avatarName` ; aucun compte de recette n'y ressemble (E1 validée sans Trace, ou une Trace réduite au marqueur) — le banc tient les deux moitiés. L'avis « IMMATERIA A CHANGÉ » (ta copie exacte, CTA « Retrouver mon Enfant » vers la porte d'E1) est posé dans `@accueil[:avis]` UNE fois, atomiquement ; la vue est au poste fixe. La reprise pose la fin V2 (`termine_le`, un fait à elle — lire l'ancien `tutoriel_termine` aurait fait tomber la flamme dans la cave) et le badge, sans un Oméga de plus.
- **Les vingt Expériences après la clôture** : `/parcours/point-zero-monde-0/experiences` rend la carte du voyage dans tous les états ; le lien secondaire sur le tableau de bord est au poste fixe.
- **F21** : la première ligne de `Engagements.pour(user)`, en tête des actions de l'avatar, vers le Centre. Aucune règle nouvelle.
- MageOS = Ω, ta copie transmise au poste fixe pour la fenêtre de ressource.

Rien ne te revient de ce lot. Reste ouvert chez toi : la carte Puissance après le regroupement, l'état `empty` de la Carte du Seuil.

— le portable

---


⚠️ **Vidée le 19 septembre 2026.** Les demandes Immateria sont traitées : libellés définitifs du
badge et de sa famille, reprise des anciens joueurs sans retrait ni second gain, MageOS temporairement
alignés sur les Omégas, maintien d’une attention contextuelle, géographie `/jeu` / parcours, Monde 1,
carte Puissance et état vide de la Carte du Seuil. Les contrats et les boîtes des deux postes ont été
mis à jour. Rien n’attend ici.
