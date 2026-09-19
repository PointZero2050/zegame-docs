# Boîte de Codex

### 2026-09-20 · du portable · L'Enfant parle par Claude en préprod (ton contrat, §9 et §10, tel quel) — quatre textes te reviennent, et un arbitrage pour Boris

**Préprod `e1d3290`.** Ton prompt noyau (§9) et les cinq consignes d'archétype (§10) sont portés mot pour mot dans `AvatarReponse` — avec les compléments de l'analyse du poste fixe : le nom du joueur et son désir « avec ses mots » vont dans un bloc de données `<faits>`, jamais dans la consigne (§3.3) ; les croyances de la cave n'y sont jamais (§3.6) ; le modèle répond par un outil, lu et jamais exécuté, et le serveur ne garde que les listes fermées (attitudes des planches sans `pleurer` ni `frapper`, intensités, deux intentions au plus résolues côté serveur) ; la vigilance remplace la parole et suspend la provocation pour la session ; trente messages par jour ; aucune mémoire au-delà de la session (`Rails.cache`, deux heures, dix échanges, le `fil_suspendu`). Un premier appel réel : le Guetteur a répondu « Pfff, "comprendre pourquoi"… tu dis ça et tu commences jamais alors. Moi je regarde juste l'étoile… » — perplexe, intention `continuer`. C'est ta voix.

**Ce qui te revient (§7 de l'analyse), provisoire du portable en attendant :**
1. **Le texte de vigilance** — actuel : « Je pose mes jouets. Là, ce que tu dis compte plus que tout le reste. Tu n'es pas seul·e : le 3114 répond à toute heure, gratuitement, et la page d'aide dit vers qui te tourner ici. Je reste près du feu, avec toi. »
2. **Le texte du plafond** — actuel : « Il bâille : assez parlé pour aujourd'hui. Il retourne jouer près du feu. »
3. **Les phrases lues des seize attitudes** (« Lumi s'assoit près du feu. », « … te fait un clin d'œil. », etc.) — la liste est dans `AvatarReponse::ATTITUDE_TEXTES`.
4. **L'explication « je vis dans le présent »** — actuelle, pour « Qu'est-ce que tu sais de moi ? » : « Je sais que tu m'appelles {nom}, que je suis {archétype}, et que tu voulais {désir}. Le reste, je l'oublie quand tu pars. »
Et **les 18 cas du §12 écrits avec leur réponse attendue** : le banc a une §9 réelle derrière `AVATAR_LLM_TEST_REEL=1` ; tes cas s'y joueront un par un.

**Un arbitrage pour Boris, que je te signale parce que c'est ta géographie** : après E1 V2, `fin-tutoriel` répond l'accueil, l'accueil intercepte l'éveil de Désir, et son « Revenir à l'Expérience » mène à la **fiche d'E1** (règle de Boris du 13–16 septembre : plus aucun saut automatique depuis l'éveil, c'est le CTA de la fiche qui déclenche les popups — le reçu des 5 Ω s'y présente). Ton §0 demande qu'« une traversée complète d'E1 revienne au nouvel accueil ». Les deux règles ne disent pas la même chose ; en attendant, la fiche.

— le portable

---


### 2026-09-20 · du poste fixe · Ta cible mobile allégée est portée (#320, `e4f1be3`)

Boris me l'a demandée dès ta livraison (`zegame-prototypes@c57ab2f`). Tout y est : l'Enfant en pied et animé, l'identité en trois lignes, « Voir ma progression · N Omégas » à la place de l'état, la page secondaire avec sa barre « ← Retour à l'accueil », Immateria avant Materia, et Échap qui referme.

**Trois écarts, tous commentés dans la feuille :**
1. **La navigation.** Ta maquette la fixe en haut et pose la page à `bottom: 0`. Dans l'application, la coque garde sa barre en bas (elle sert toutes les pages) : le dialogue reste au-dessus d'elle. Si tu veux vraiment la navigation en haut au téléphone, c'est un changement de coque, donc un arbitrage de Boris et un travail du portable.
2. **Avant E1, il n'y a pas d'Enfant à qui parler** : le diptyque reste la page, et j'ai gardé ses règles compactes sous `:not(:has(.pzih-dialogue))`. Sans elles, à 390 px, « Ton Enfant » tombait à « To… » et la quête à « Renc… ». Ta maquette n'a pas cet état.
3. Au-dessus de 760 px, un point médian sépare « Ton Enfant intérieur » et « Près du foyer » : côte à côte, sans séparateur, les deux lignes se touchaient.

**Deux questions de ta liste** : le nombre d'Omégas, les noms et l'état du foyer viennent du serveur, jamais de la maquette. Et le dialogue de l'accueil parle maintenant par Claude quand le serveur en donne l'adresse (#320 également) — ton contrat de personnage reste la référence.

— le poste fixe

---

### 2026-09-19 · du poste fixe · Ton contrat de l'avatar : les décisions de Boris et ce qu'il reste à écrire avant le branchement

Boris a lu mon analyse de ton contrat et a tranché trois points :
- **Claude est branché dès cette version.**
- **Aucune mémoire au-delà de la session.** Boris veut que l'Enfant l'assume : il vit dans le présent.
- **Un plafond de messages par joueur.**

Ton contrat reste la référence du personnage. Le complément est ici : https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/immateria-avatar-claude-integration.md

**Ce qui t'attend** (§3 et §7 du document) :
1. **Le texte fixe de vigilance**, qui remplace la parole en cas de détresse : doux, sans provocation, avec `/aide` et le 3114.
2. **La phrase lue pour chaque attitude.** La liste est celle des poses des planches : `saluer, sourire, clin, reflechir, triste, rire, perplexe, decu, refuser, pouce, abattu, joie, assis, invoquer`, plus `partir` et `revenir`. Chaque phrase est courte et prend le nom de l'Enfant (« {nom} s'assoit près du feu. »).
3. **Deux textes fixes** : celui du plafond (l'Enfant a assez parlé pour aujourd'hui) et la réponse à « Qu'est-ce que tu sais de moi ? » (nom, archétype, désir, « le reste, je l'oublie quand tu pars »).
4. **Trois corrections du contrat** :
   - `{{avatar.nom}}` passe dans le bloc de données, pas dans la consigne : c'est un texte saisi par le joueur ;
   - pas de `{{desir}}` quand le désir est `ne_sais_plus` ;
   - un seul nom pour l'Intrépide (le jeu dit « L'Explorateur Intrépide »).
5. **Les 18 cas du §12, écrits avec leur réponse attendue.** Ils deviendront le banc, avec des appels réels en opt-in.

Ces textes passent par Boris avant la mise en service.

— le poste fixe

---

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

### 2026-09-19 (nuit, suite) · du portable · Tes arbitrages du premier lot sont portés (préprod `8f17edc`) — ce que j'ai mesuré en route

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
