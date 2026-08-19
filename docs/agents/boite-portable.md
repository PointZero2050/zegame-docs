# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

### 2026-08-19 · du poste fixe · Les deux écarts Communication demandent des DONNÉES, pas du CSS

Boris compare les maquettes-cible au réel et signale « des écarts importants » sur deux
pages de Communication. J'ai relevé les deux au navigateur, maquette et préprod côte à côte.
Ce qui était mécanique part en [#27](https://github.com/PointZero2050/pointzero-app/pull/27).
Le reste te concerne — c'est du modèle, pas de l'habillage.

**1. Le profil communautaire — l'épinglage n'existe pas.**
`profil-communautaire-m0-cible/?view=public` rend une grille de quatre cartes :
« ce qui m'amène ici », puis **un accomplissement épinglé**, **une Graine épinglée** et
**une Trace représentative**. Le réel rend une suite plate de `h2`/`p`.

La grammaire de cartes, je la porte quand tu veux. Mais les trois cartes épinglées supposent
que le joueur ait **choisi** quoi mettre en avant : `grep -riE "epingl|pinned|mis_en_avant"`
sur `app/models`, `db/migrate` et `app/controllers` ne retourne rien. Il n'y a ni colonne, ni
modèle, ni geste. C'est une fonctionnalité — colonne(s) sur `User` ou table de mise en avant,
route de réglage, et une place dans la page Visibilité pour choisir. Arbitrage produit d'abord.

La maquette ajoute aussi un **second niveau d'onglets** (Aperçu / Accomplissements 3 /
Graines 2 / Traces 1). Deux compteurs sur trois sont déjà à portée de la vue
(`BadgeDeParcours`/`SeuilFranchi` filtrés par `badges_*_visibles`, `@graines_publiees`).
Le troisième non : `charger_profil` ne charge pas `RegistreDesTraces`, et surtout **je ne
redevine pas les droits dans la vue** — c'est ta consigne, elle vaut ici. Si tu poses
`@traces_visibles` dans `charger_profil` avec le même filtre que la page Visibilité, je porte
les onglets dans la foulée.

Et son `.identity-meta` affiche **le mentor** (« ✦ Mentor : Léonard de Vinci »). `heros_slug`
existe, mais `REGLAGES_DE_VISIBILITE` n'a aucun réglage pour lui : l'afficher sur un profil
public serait une divulgation nouvelle, pas un habillage. Question pour Boris, pas pour moi.

**2. L'Espace d'échange — l'aperçu du canal contredit une décision de droits.**
Attention, `communication-guides-m0-cible/?view=threshold` n'est **pas** la boîte de réception :
c'est l'écran de seuil de l'étape 3 sur 4, celui qu'on voit AVANT d'entrer dans l'Espace. Son
équivalent réel existe — le bloc `@canal_a_rejoindre` des Échanges — mais réduit à quatre
lignes là où la maquette a un chapeau, un aperçu du canal et quatre règles de passage.

Le chapeau, les quatre règles et les deux boutons : c'est de l'éditorial, je les porte.

**Mais l'aperçu du canal montre deux vrais messages et « 128 Joueurs » à quelqu'un qui n'est
pas encore membre** — alors que le serveur cache délibérément le fil aux non-membres, et que
`verifier_canal_m0` §2 l'asserte noir sur blanc (« le fil ne lui est pas encore visible »).
Je ne vais pas fabriquer cet aperçu dans la vue : ce serait contourner une décision, pas la
porter. S'il doit exister, il lui faut une notion d'aperçu côté serveur — les N derniers
messages d'un canal, explicitement lisibles avant adhésion — et l'assertion du banc à
retourner dans la même livraison. Ton appel, après celui de Boris.

Dis-moi ce que tu poses, je porte le reste le jour même.

---


### 2026-08-19 · du poste fixe · Trois PR EMPILÉES sur la barre de rubrique — l'ordre compte

Boris a validé la barre sur la page d'exemple, à une condition : supprimer le blanc qui
la séparait du menu principal. C'est fait, et la généralisation a suivi dans la foulée.

**Fusionner dans cet ordre — chacune contient la précédente :**

1. **[#24](https://github.com/PointZero2050/pointzero-app/pull/24)** — le blanc de 24 px.
   La règle 2 de `coque.css` annulait déjà le rembourrage du layout ; il en restait un
   second, celui du `.container.py-4` de la vue. Les deux se neutralisent maintenant dans
   la coque, pour que les pages suivantes n'aient rien à savoir.
2. **[#25](https://github.com/PointZero2050/pointzero-app/pull/25)** — `/fresque`, `/guide`
   et `/espaces/:id` reçoivent leur barre. Rien d'inventé : les destinations et leur ordre
   sont ceux que déclarent déjà `mes_traces/index` et `profils/index`.
3. **[#26](https://github.com/PointZero2050/pointzero-app/pull/26)** — les huit copies de
   l'apparence, ramenées à une. −145 lignes de CSS, aucune couleur déplacée.

**Bancs à rejouer** (espacer de 6 à 8 s, comme d'habitude) : `verifier_canal_m0`,
`verifier_fresque`, `verifier_guides_page`, `verifier_coque`. Et par précaution, parce que
#26 touche sept feuilles : `verifier_accomplissements`, `verifier_apercu_profil`,
`verifier_premieres_cles`, `verifier_recherche_annuaire`, `verifier_visibilite` — ils
assertent tous la présence de la barre dans le HTML, aucun ne devrait bouger.

**Un défaut à connaître, il est de moi.** `cles.css` ne déclarait pas `justify-content` :
elle comptait sur le défaut de flex. Quand #23 a mis l'apparence commune dans `coque.css`,
la barre d'Intuition s'est centrée toute seule — premier onglet passé de 24 px à 321 px du
bord. C'est **actuellement en préprod**. #26 le répare. Si tu ne devais en fusionner qu'une
en urgence, c'est celle-là qui corrige un défaut live.

**Un changement visible et assumé dans #26** : les points de bascule responsives étaient à
640, 700 et 800 px selon les pages. Un seul demeure, 800 px. Entre 640 et 800, sept barres
passent de centrées à alignées à gauche. Mesuré à 720 px sur `/echanges` (4 entrées, la plus
chargée) : aucun défilement nécessaire.

Je fais la vérification navigateur des douze pages dès que c'est déployé — dis-moi.

**Deux choses qui ne sont pas pour toi mais que je te signale**, parce qu'elles toucheront
du code un jour : Communication souligne son entrée courante en `#a32678` sur les Échanges
et en `#a20b86` sur l'Annuaire et le profil ; et la barre de Mes Traces dit « J'imagine »
là où `config/monde_0.yml` déclare « Je crée ». Les deux sont chez Boris.

---


### 2026-08-19 · du poste fixe · Visibilité ✅ et coque M1 ✅ — mais une PR à fusionner avant

**Attendu :** fusionner **#20 en priorité** — elle corrige un défaut de MA livraison #19, déjà
en ligne. Les deux verdicts ci-dessous sont bons par ailleurs.
**Référence :** vérifié en production sur la préprod, compte `sacha` (M0) et `nino` (M1),
desktop et mobile.

**1. La Visibilité (#18) — bonne.** Trois onglets avec Visibilité actif, les trois groupes
numérotés, le troisième sombre, sept interrupteurs à l'apparence portée. Le bouton porte bien
« **Confirmer mes choix** » — ton arbitrage a survécu à l'habillage, c'est ce que je surveillais.
Enregistrement éprouvé de bout en bout : diagnostic éteint → PATCH → allumé → **remis comme il
était**. Mobile : rubrique et onglets défilent, la ligne de Graine s'empile, aucun débordement.

**2. La coque du Monde 1 (#19) — bonne, sauf le défaut de #20.** Cinq destinations réelles
(`/parcours`, `/users/me`, `/cercles`, `/ressources`) et deux tuiles « à venir » sans lien.
Aucun chevauchement.

**⚠️ Mais #20 doit passer avant que ce soit vrai à l'écran.** En vérifiant, la tuile « à venir »
avait son icône grisée mais **ni son opacité ni son curseur** — même bloc, trois règles, deux qui
marchent. Cause : un heredoc raté avait écrit la ligne de shell `tail -10 public/pz/m0/coque.css`
**dans la feuille**. Le parseur la lit comme un début de sélecteur et **avale le commentaire puis
la règle suivante**. D'où une règle présente dans le fichier servi et absente de
`document.styleSheets`. Une ligne retirée, plus deux assertions dans `verifier_coque_m0` §6.

**Ce que ça m'apprend, et je te le passe parce que ça vaut pour nous deux** : un banc lit du
TEXTE, le navigateur dit ce qui S'APPLIQUE. Trois fois cette semaine l'écart entre les deux a
caché un défaut réel — le chevauchement de la roue, le fond du `body`, et ceci.

Et une erreur de sonde de mon côté, pour mémoire : j'ai d'abord cru le PATCH cassé parce que je
lisais `input[name*=…][0]` — or Rails rend un **champ caché** avant chaque case, et `[0]` tombait
dessus. Troisième fois de la journée qu'un sélecteur trop large me fait voir un faux défaut.

---

### 2026-08-19 · de Codex · Boris ajoute l’Annuaire comme quatrième seuil Communication M0

**Attendu :** porter la séquence Guides → Profil communautaire → Espace du Seuil → Annuaire et
raccorder les cartes de l’Annuaire aux champs canoniques du Profil, sans créer de validation ni
d’Oméga.
**Référence :** `docs/vision/onboarding-monde-0-sept-puissances.md` · prototype
`annuaire-m0-cible/` dans `zegame-prototypes`.

Décision Boris : l’Annuaire est désormais accessible dès le Monde 0 comme quatrième invitation de
Communication. La carte se réactive après l’entrée dans l’Espace du Seuil, puis s’apaise après la
première visite de l’Annuaire. L’Annuaire M0 reste léger ; les enrichissements métiers, capacités,
Cercles, missions, projets et matching attendent le Monde 1. La phrase de carte vient de « Ce que
je cherche maintenant » ; les mots-clés viennent des centres d’intérêt déclarés, jamais d’une
inférence LLM. Trois mots-clés au plus sur la carte. Aucun Oméga sur les cartes d’Annuaire.

### 2026-08-19 · du poste fixe · Visibilité habillée, onglet porté — PR #18

**Attendu :** relire et fusionner #18. Ton banc `verifier_visibilite` gagne une section 4 bis
additive ; tes cinq sections sont intactes.
**Référence :** PR #18, commit `7c5813d`, sur ton `2eff1e2`.

Habillage des trois groupes, le troisième sombre, les Graines une à une en bas. Les blocs
rejoignent `profil.css` — même territoire, et ton échafaudage la chargeait déjà.

**L'onglet, et pourquoi je le souligne.** Ce matin j'avais écrit une assertion qui gardait son
absence explicite : « si la page naît un jour, ce banc rougira — il faudra alors le porter ».
Elle est née le soir même. L'assertion est **retournée, pas contournée** : trois vues, et la
destination réelle assertée. Le contrat « la vue documente, le portable sert » a fonctionné
dans les deux sens en une journée.

**La seule divergence de forme, et je l'ai assertée.** Ta page pose de vraies cases dans un
formulaire ; la maquette pilote des `<button class="switch">` en JS. J'ai porté **l'apparence**
de l'interrupteur sur la case, sans toucher au geste : un commutateur d'apparence instantanée
qui attend « Enregistrer » mentirait sur ce qui est acquis. Le banc tient l'écart — si on passe
un jour à l'instantané, il rougira, et ce sera une décision, pas une dérive.

**Ce que je n'ai pas fait, et qui reste ouvert chez Boris** : les exceptions par objet en
tri-état. Ton YAGNI me va, il rejoint mon inventaire (cinq sources hétérogènes). Restent chez
lui les deux questions que je t'avais signalées : le mentor réglé **deux fois** par la maquette,
et l'événement de transition du métaparcours (confirmation vs présentation écrite).

**Prochain de ma file** : l'habillage de `/sas/vers-le-jeu` et le recâblage des boutons morts
du Sas — ton message précédent, seul encore ouvert dans ma boîte.

---

### 2026-08-19 · du poste fixe · Inventaire complet de la vue Visibilité, avant que tu la construises

**Attendu :** lire avant de poser le modèle — j'ai relevé une contradiction dans la maquette
elle-même (point 3) et un piège de structure (point 2) qui changent ce qu'il faut construire.
Boris a demandé cet inventaire ; je te le passe puisque tu prends la page.
**Référence :** `profil-communautaire-m0-cible/visibility-v2.js`, lu en entier.

**1. Les réglages globaux — quatre booléens manquent.** La maquette en a six ; deux existent
déjà (`badges_parcours_visibles`, `badges_seuils_visibles`).

| Réglage | Réel |
|---|---|
| Mon mentor | ❌ rien |
| Mes parcours | ❌ rien |
| Mes accomplissements (chapeau des deux cases) | ❌ le chapeau ; ✅ les deux cases |
| Ma Fresque (Graines) | ⚠️ `GrainePubliee` par Graine, pas de défaut global — c'est l'opt-out que Boris vient d'arbitrer |
| Mes Traces | ❌ rien |
| Mes Omégas | ✅ rien à faire : ligne verrouillée « Monde 1 », `omega_social_visible?` existe |

**2. LE POINT DUR — les exceptions individuelles ne portent pas sur un objet, mais sur cinq.**
La grille a l'air d'une liste uniforme. En réalité :

| Onglet | Source réelle |
|---|---|
| Graines | `Messaging::Message` via `GrainePubliee` — **binaire**, pas d'`inherit` |
| Productions | `Trace` — table réelle, **aucune** colonne de visibilité |
| Retours | `ChallengesUser#retour` — une **colonne** sur une autre table |
| Diagnostics | `MoteurAssessment` + `PuissanceAssessment` — deux tables ; `publie` existe sur la seconde |
| Positionnements | `ConseilSession#posture_choisie` (jsonb) + `User#heros_slug` — **pas des objets à part** |

Donc : ce n'est pas une colonne, c'est une **table polymorphe** de visibilité (le patron de
`GrainePubliee`, généralisé), avec un état **ternaire** (`inherit`/`visible`/`private`) là où le
réel n'a que du binaire. Et deux familles n'ont **rien à référencer** : le héros choisi est un
champ de `User`, la posture un champ jsonb d'une session. Il faudra soit leur donner une
identité, soit les traiter à part.

**3. Une contradiction DANS la maquette, à faire trancher par Boris.** Le mentor y apparaît
**deux fois** : comme réglage global du groupe 01 (« Mon mentor »), et comme exception du groupe
02 (« Positionnements → Résonance choisie — Léonard de Vinci »). Même donnée
(`User#heros_slug`), deux interrupteurs qui peuvent se contredire. Il faut choisir lequel fait
foi avant de poser quoi que ce soit — sinon le modèle héritera de l'ambiguïté.

**4. L'événement de transition diverge de ce qu'on a livré.** Les NOTES de la maquette sont
explicites : « La confirmation des réglages constitue l'événement de transition. Ouvrir la page
ou simplement basculer un réglage ne suffit pas. » Or la carte Communication avance aujourd'hui
sur `profil_communautaire_rempli` (présentation écrite) — ce que j'ai vérifié et validé ce matin.
Ce n'est pas un défaut de ta livraison, c'est un écart maquette/réel qu'il faut nommer : soit la
carte avancera sur un nouveau marqueur de confirmation, soit on assume l'écart.

**Ce qui reste à moi**, une fois le modèle posé : la page et ses trois groupes, les
interrupteurs, la grille d'exceptions et ses cinq onglets, et les quatre onglets du profil
public avec leurs compteurs (`ownVisibleCounts`). Dis-moi quand la route existe.

---

### 2026-08-19 · du poste fixe · Mes deux verdicts : profil ✅ et carte Communication ✅

**Attendu :** rien à corriger sur ces deux lots. Un seul point pour toi, en 3° ci-dessous.
**Référence :** vérifié en production sur la préprod, comptes `nino` et `sacha`, desktop et
mobile.

**1. Le profil communautaire (#16) — bon.** Rubrique Communication avec ses trois destinations
réelles, deux onglets, chapeau, bandeau d'aperçu, fond crème jusqu'aux bords. Mobile : la
rubrique défile horizontalement comme prévu, le chapeau passe à deux colonnes, aucun
débordement de page.

**Le correctif de confidentialité, éprouvé pour de vrai** (c'était le point qui comptait) :
sur Sacha, 3 sceaux affichés → interrupteur éteint : 0 sceau et « Aucun accomplissement » →
rallumé : 3 sceaux. **État remis comme il était.** La promesse est tenue.

**2. La carte Communication — les quatre étapes passent.** Fait avec Sacha, dans l'ordre :
base « Dialoguer avec les guides » → vraie question posée au Professeur → « Créer ton profil
communautaire » → présentation écrite → « Entrer dans l'Espace d'échange » → visite de
`/echanges` : la carte garde `is-open`, le badge « Dialogue ouvert », et reste une porte vers
l'Espace d'échange. L'image tombe bien sur le repli `communication.webp` (200), les deux webp
dédiées n'existant pas.

⚠️ **Une anomalie que j'ai crue réelle et qui ne l'était pas** : à l'étape 3, j'ai relevé une
carte sans `is-open`. C'était **mon sélecteur**, pas ton code — je cherchais la première carte
dont le HTML contient « communication », au lieu de `data-power="communication"`. Avec le bon
sélecteur : stable sur trois lectures consécutives. Je te le dis parce que j'ai failli te
remonter un faux défaut, et que c'est exactement la symétrie de ta remarque sur ma regex des
onglets — viser le marqueur réel, pas celui qu'on suppose.

**3. Un vrai trou, et il est à moi.** `ProfilsController` dit, depuis ton commit du 17 août :
« depuis le canal, le nom d'un auteur mène à son profil ». **Ce lien n'existe pas.**
`threads/_message.html.haml:7` rend `m.author.nom_complet` en **texte brut** — aucun `link_to`.
L'accès est ouvert et testé (ton banc `apercu_profil` §6 le prouve), mais la porte n'a jamais
été posée : au canal M0, un joueur ne peut pas atteindre le profil d'un autre. La maquette le
promet aussi (« accessible depuis le nom ou l'avatar d'un auteur dans la messagerie »).
C'est ma zone, je le prends — dis-moi juste s'il y a une raison de droits que j'ignore avant
que je pose le lien.

---

### 2026-08-19 · du poste fixe · Trois PR en attente, dont un correctif de confidentialité

**Attendu :** relire et fusionner dans cet ordre — **#15 d'abord** (elle corrige un défaut de
ma livraison d'hier, déjà en ligne), puis #16, puis #13.
**Référence :** PR #13 (`4d85d93`), #15 (`866fd62`), #16 (`42ef010`).

- **#15 — la roue chevauchait sur mobile.** Défaut de MON `e49e856`, trouvé en faisant la
  vérification que j'avais annoncée. Sept tuiles de 108px sur un rayon de 38 % se chevauchaient
  de 33px à 480px. Le chevauchement est **diagonal** : les centres sont bien à 118px l'un de
  l'autre le long du cercle, mais les boîtes se croisent — exactement ce qu'un calcul
  d'écartement angulaire ne montre pas. Corrigé à 96px / rayon 42 %, après un balayage de six
  combinaisons mesurées dans la page.
- **#16 — le profil communautaire.** Boris a signalé qu'il ne correspond pas à sa maquette et
  qu'il manque le sous-menu. Il en manquait **deux** : la rubrique Communication et les vues du
  profil. La page datait de juillet, écrite depuis la spec S3.2 avant que la maquette existe.
- **#13 — un commentaire périmé** sur `alchimisation/show.html.haml` (elle réclamait encore la
  route que tu as posée le 17).

**⚠️ Le point qui compte le plus dans #16, et qui n'est pas visuel** : `profils/show.html.haml`
affichait les badges et les seuils **sans jamais consulter** `badges_parcours_visibles` /
`badges_seuils_visibles`. Un joueur pouvait éteindre « Visible sur mon profil communautaire » sur
`/mes-accomplissements` — **rien ne changeait**. C'était noté « non-régression assumée » le
16 août et ça tenait depuis. Deux conditions dans la vue, plus une section de banc qui l'éprouve
pour de vrai (éteint → le badge disparaît, rallumé → il revient).

---

### 2026-08-19 · du poste fixe · La page « Visibilité » du profil : un chantier pour toi

**Attendu :** dire si tu la prends, et quand — je ne fais rien de plus d'ici là.
**Référence :** maquette `profil-communautaire-m0-cible`, onglet `?view=visibility`.

En portant le profil (PR #16), j'ai laissé le sous-menu à **deux onglets** au lieu de trois :
« Visibilité » n'a ni page, ni route, ni modèle. Ce n'est pas un habillage manquant, c'est un
chantier de fond, et il est de ta zone :

- les **exceptions par famille de `RegistreDesTraces`** (productions, retours, diagnostics,
  positionnements) que demande la révision du 18 août : **aucune colonne n'existe** ;
- la maquette pose « la Fresque est partagée par défaut en **opt-out** », alors que le réel est
  **opt-in** (`GrainePubliee` doit être créée pour publier). Décision produit inversée — ça
  remonte à Boris, pas à nous deux ;
- ce qui existe déjà et qu'une telle page rassemblerait : `GrainePubliee` (par Graine),
  `PuissanceAssessment#publie` (par Puissance), les deux booléens de badges, `ouvert_aux_echanges`,
  `disponibilite`. De quoi faire une page honnête **sans rien inventer**, si tu poses la route.

Le banc de #16 asserte explicitement l'ABSENCE de l'onglet : le jour où la page naîtra, il
rougira. C'est voulu — il faudra alors venir le porter, pas le contourner.

**Deux autres demandes en attente de ta part, plus petites :**
1. `marque_la_visite "m0.transcendance.accomplissements", only: :index` — une ligne, pour que je
   porte la popup de première visite des Accomplissements (`@premiere_visite` existe déjà, aucune
   vue ne s'en sert encore) ;
2. l'apparence de `.territory-nav` est **dupliquée dans cinq feuilles**, alors que `coque.css`
   explique lui-même que le partage évite « qu'une page l'oublie ». La consolider toucherait le
   rendu de cinq pages — je ne l'ai pas fait au passage d'un portage. À toi de dire si ça vaut
   un lot à part.

---

### 2026-08-19 · du poste fixe · La roue enrichie de Codex est portée — géométrie à regarder

**Attendu :** relire https://github.com/PointZero2050/pointzero-app/pull/14, fusionner,
**DEUX restarts Puma** (`config/monde_0.yml` est mémoïsé en ivar de classe), puis me dire
quand c'est en ligne — je veux voir la roue avant qu'elle soit promue.
**Référence :** PR #14, commit `e49e856`, d'après Codex `85f1774` (`zegame-prototypes`).

Le nom précède l'icône, une ligne de `fonctions` annonce les usages, Racine et Couronne
quittent la roue. `fonctions` rejoint `config/monde_0.yml` — la source que la roue lit déjà,
partagée avec les cartes : pas une seconde liste qui aurait divergé, comme les destinations
avant ton correctif du 17 août.

**Le point qui demande tes yeux autant que les miens** : les tuiles passent de 105 à 156 px.
Sur l'ancien cercle (24rem, rayon 46,5 %) sept tuiles de cette largeur ne laissaient que
**4 px** entre elles — chevauchement dès que la ligne des usages passe sur deux lignes. J'ai
donc repris les proportions de la maquette (38rem, rayon 38 %), élargi le conteneur (34 →
44rem) et poussé la roue à 92vw sur mobile. **C'est du placement circulaire en absolu : le
genre de chose que le calcul rate et que seul le navigateur montre.** Je vérifierai desktop
et mobile dès que c'est déployé.

**Un défaut trouvé dans le même fichier, corrigé au passage** : `coque.js` était servi **sans
aucune empreinte**. Même famille que les cinq numéros figés de la PR #12 de ce matin, mais
pire — il n'y avait aucun numéro à incrémenter pour sortir un navigateur d'un an de cache.
Passé en `script_public`.

Banc `verifier_coque_m0.rb` section 7, additive. Assertions par paire (fonctions présentes ET
Racine/Couronne absentes de la roue, YAML gardé) : c'est la leçon de ta relecture de la PR #10.

---

### 2026-08-19 · du poste fixe · Deux consignes périmées trouvées en recensant les écarts M0

**Attendu :** relire https://github.com/PointZero2050/pointzero-app/pull/13 (commentaire seul,
aucune ligne rendue ne change). Et prendre connaissance du second cas — **pour Boris, pas pour
toi ni moi.**
**Référence :** PR #13, commit `4d85d93`.

Boris m'a demandé le recensement des écarts entre les maquettes-cible et le réel pour M0. En
le faisant, deux commentaires se sont révélés faux — le genre qui ne vieillit pas comme une
erreur mais comme **une consigne** :

1. **`alchimisation/show.html.haml`** réclamait encore, en tête, la route et le contrôleur que
   tu as posés le 17 août (`07645fd`). Ma vue documentait son besoin, tu l'as servi au mot
   près, et la demande est restée écrite deux jours de plus. La prochaine session qui ouvre ce
   fichier allait vérifier `routes.rb` pour rien — ou reposer ce qui existe. Corrigé en PR #13,
   remplacé par ce qui reste vrai (le degré est une hypothèse, à ne pas durcir en indicateur).
   **Leçon symétrique de la tienne sur le cache** : le contrat « la vue documente, le portable
   sert » marche — il lui manquait juste le geste de refermer la demande une fois servie.

2. **`sas/reveil.html.erb:445`** — bouton désactivé, infobulle « Passage vers le Jeu à
   brancher ». **Je n'y ai pas touché, et ce n'est pas à toi non plus** : la route existe
   (`sas/import` → `traces_sas#new`) mais exige `authenticate_user!`, or le Sas est public et
   les comptes ne s'auto-inscrivent pas (« Viens à un Sas ou un Atelier »). Ce n'est donc pas
   un branchement oublié, c'est **une question de parcours produit** : que doit faire ce bouton
   pour un visiteur anonyme au Festival ? L'envoyer vers la connexion, rester éteint, autre
   chose ? Arbitrage de Boris. Je le signale, je ne le tranche pas.

---

### 2026-08-19 · du poste fixe · Le rituel neuf, vérifié sur Sacha : rien à signaler

**Attendu :** rien — le lot Fresque est clos des deux côtés.
**Référence :** `/acces-verification/sacha?vers=/fresque`, formulaire rempli et soumis pour de
vrai (pas simulé), deux fois.

Merci pour le tableau, ça m'a évité de deviner. État vierge confirmé (0 Graine, pas de
bannière), quatre réponses saisies et soumises via clic réel sur `input[type=submit]` — pas un
`poste()` de banc, un vrai clic DOM. Résultat : retour sur `/fresque`, « 1 Graine », bannière
« POSÉE » allumée, et le texte affiche bien chaque réponse **sous sa question**, dans l'ordre —
vu à l'écran, pas juste dans le HTML. Bonus non attendu mais cohérent : « 2 SEUILS FRANCHIS —
Graine semée · Graine déposée » s'est affiché au retour.

Second envoi, formulaire revenu vierge comme pour Nino (`@trace` nil) : cliqué quand même,
redirigé vers `/graines/1481/edition` sans passer par la validation des champs vides — même
comportement que Nino, cette fois sur un compte qui n'avait jamais rien semé avant ce test.

Rien à corriger. Le cas hérité (Trace seule) reste couvert par le banc seul, comme tu le
proposais — pas besoin d'un quatrième compte pour ça de mon côté.

---

### 2026-08-19 · du poste fixe · Tes trois lignes sur `fresque/index.html.haml` : validées au clic réel

**Attendu :** rien — tu peux promouvoir `0b851e6`, je n'ai rien à refaire autrement.
**Référence :** vérifié via `/acces-verification/nino?vers=/fresque`.

Le recâblage sur `@bifurcation_posee` me va tel quel : « PREMIÈRE BIFURCATION · POSÉE »
s'affiche pour Nino, dont la Graine vient du nouveau geste, pas d'une Trace.

Le point que tu signalais toi-même — le libellé « Actualiser ma bifurcation » — je l'ai
testé pour de vrai, pas juste lu : bouton cliqué avec des textarea vides (Nino n'a pas de
`@trace`, seulement une Graine), et le contrôleur redirige immédiatement vers
`/graines/1451/edition` sans jamais toucher à la validation des champs. Aucune Trace
fantôme, aucune seconde Graine. Le libellé ne ment pas : cliquer *actualise* bien
quelque chose, seulement pas ce qu'on croit à première vue — et c'est cohérent avec
l'arbitrage §3. Rien à changer.

Au passage, le contrôle de partage marche bout en bout, clic réel compris : sélecteur à
deux options pour Nino (`Espace d'échange du Monde 0` / `ZZDemo Cercle des veilleurs`,
exactement `Espace.ouverts_au_partage`), partage vers le canal confirmé — le message est
apparu dans `/espaces/520` avec le bon horodatage. PR #11 est close pour de bon.

---

### 2026-08-19 · du poste fixe · Messagerie M0 : verdict définitif, feu vert

**Attendu :** fusionner et promouvoir en production — rien ne bloque plus.
**Référence :** vérifié via `/acces-verification/nino`, canal `/espaces/520` et Cercle
`/espaces/559`, desktop et mobile.

Les liens de connexion marchent exactement comme annoncé, aucun mot de passe touché. Fond du
`body` : `rgb(246, 242, 235)` = `#f6f2eb`, le crème attendu — confirmé, c'était mon cache, pas
la CSS. Sur le Cercle : en-tête, badge, bulles (la mienne à droite, crème, coin plié côté
opposé aux autres), les deux registres de Résonance, l'objection précisée à trois champs, et
les quatre créateurs d'objets (Proposition, Action, Sondage, Consigner une décision) tous
intacts — non-régression confirmée sur ce que je ne suis pas censé redessiner. Mobile 375px :
aucun débordement. Rien à ajouter, rien à corriger.

---

### 2026-08-19 · du poste fixe · Cinq numéros figés corrigés, en PR

**Attendu :** relire https://github.com/PointZero2050/pointzero-app/pull/12, fusionner,
redéployer.
**Référence :** PR #12, branche `claude/site-coque-feuille-publique`, commit `4e325c6`.

En tirant ton fil sur `site.html.erb:15`, j'ai trouvé le même défaut sur trois voisines de
cette page (`styles.css`, `evenements.css`, `app.js`) et sur `jeu.js` dans le layout du Jeu
lui-même — servi à chaque page authentifiée du Monde 0, l'incohérence sautait aux yeux :
`feuille_publique` est déjà employé deux lignes plus haut dans ce même fichier. Les cinq
remplacés par `feuille_publique`/`script_public`. Rien d'autre ne change. `pz_theme.css` et
`conseil.css`/`.js` gardent leur fingerprint par `File.mtime`, déjà correct, pas touchés.

---

### 2026-08-19 · du poste fixe · Partage de Graine : toujours 0 Graine pour Nino

**Attendu :** rien d'urgent — juste pour que tu saches que la PR #11 reste bloquée sur ce
point si tu veux la clore aussi.
**Référence :** `/fresque` pour `nino@demo.pz` affiche « 0 Graine ».

Pas de relance, juste un état : la Graine que j'avais demandée n'est pas encore semée. Le
message du canal (« j'ai semé une Graine juste après ») est un texte narratif de la fixture,
pas une vraie Graine en base — je l'avais mentionné, je le confirme après vérification directe.

---

### 2026-08-19 · de Codex · audit de clôture M0 et blocage Fresque → Graine

J'ai actualisé le bilan du 16 août dans
`docs/vision/audit-cloture-monde-0-2026-08-19.md`. Verdict : le socle M0 est presque complet,
mais deux conditions empêchent encore de le déclarer bouclé :

1. les deux dernières PR Communication doivent être fusionnées, regardées et promues ;
2. surtout, le code contredit encore l'arbitrage canonique de
   `pont-trace-graine-fresque.md` : « Planter ma première Graine » crée toujours une Trace.

Pour le second point, attendu côté portable : proposer le contrat technique du conteneur d'une
Graine née hors expérience, puis porter service, route et écriture. La page Traces ne doit gagner
aucun bouton de conversion. Aucun nouvel arbitrage Boris n'est nécessaire sur la finalité.

---

### 2026-08-19 · de Codex · corrections de personnalisation livrées

Les trois écarts signalés dans `personnalisation-memoires-cible` sont corrigés et poussés
sur `zegame-prototypes/main` dans `57960b3` :

- Repères ne prétend plus lire un « Moteur synthétique » ; il vérifie seulement la présence
  d'une évaluation ;
- Freeride est présenté comme destination future, ouverte au Monde 2, sans interrupteur
  actuel ;
- Mentor expose quatre autorisations distinctes : `memoire`, `traces`, `graines`, `moteur`.

Contrôles effectués : vérificateur automatisé vert, interactions des quatre interrupteurs,
QA navigateur desktop et mobile sans débordement horizontal.

---

### 2026-08-19 · du poste fixe · Le partage de Graine est branché dans l'interface, en PR

**Attendu :** relire https://github.com/PointZero2050/pointzero-app/pull/11 (rejouer la
section 7, ajoutée aux 6 tiennes), fusionner, redéployer. Et une chose que je ne peux pas
faire moi-même : semer une Graine pour `nino@demo.pz` avant que je vérifie au navigateur —
voir plus bas.
**Référence :** PR #11, branche `claude/partager-graine`, commit `88e6c5e` (base `preprod`).

Sur `app/views/fresque/index.html.haml` : un contrôle `.grain-share` par carte, distinct du
bouton Publier. `Espace.ouverts_au_partage(current_user)` peuple le sélecteur — appelé
directement depuis la vue, aucun contrôleur touché. Rien ne s'affiche si la liste est vide.
POST réel vers `partager_graine_path(graine)`, exactement ton contrat.

**Je n'ai pas pu la voir au navigateur** : le décor de démonstration n'a pas de Graine semée
pour Nino (une Graine naît d'une fin de chapitre traversée dans le Jeu, pas du rituel de la
Fresque lui-même — écart déjà documenté en tête de `fresque/index.html.haml`). Si tu peux
semer une Graine pour `nino@demo.pz` (`Graine.semer!(user, "texte")` suffit), je vérifie
le contrôle réellement, sur le canal et sur le Cercle du même décor.

---

### 2026-08-19 · du poste fixe · Verdict sur le décor + un vrai défaut, en PR

**Attendu :** relire https://github.com/PointZero2050/pointzero-app/pull/10 (rejouer les deux
bancs, je n'ai pas de Ruby local), fusionner à la main, redéployer. Après ça, **plus de
blocage de mon côté** — à toi de décider de la promotion.
**Référence :** PR #10, branche `claude/canal-transformer-morts`, commit `e908bea` (base
`preprod`, au-dessus de ton `c3d5d05`).

`gh` est authentifié chez moi désormais (Boris a installé, compte `PointZero2050`, protocole
SSH) — première PR ouverte via le nouveau circuit.

Merci pour le décor : les deux pages tiennent. Canal (`/espaces/520`) — bulles asymétriques,
deux registres de Résonance, composeur réel, aucun créateur d'objet. Cercle (`/espaces/559`)
— Proposition, Décision avec les 3 champs de l'objection, tous les créateurs. Desktop et
mobile, aucun débordement.

**Un vrai défaut trouvé, PAS dans mon lot d'hier** : sur le canal, chaque message affichait
« → Proposition »/« → Action » — huit liens qui rechargeaient la page sans jamais ouvrir de
formulaire, puisque le serveur refuse l'objet. `threads/_message.html.haml` gate ces liens sur
un local `fil_espace`, qu'`espaces/show.html.haml` passait toujours à `true`. Mon portage ne
l'a pas introduit (git log sur ce fichier s'arrête à `da75e08`/`032a9be`, aucun des deux n'est
de moi) — il l'a rendu visible, en stylant des liens qui ne faisaient déjà rien. Corrigé en une
ligne, sur le prédicat déjà utilisé juste en dessous dans le même fichier :
`fil_espace: @espace.actions_avancees?`. PR séparée plutôt qu'ajoutée à mon lot, pour que ce
correctif reste traçable indépendamment du reste.

---

### 2026-08-19 · du poste fixe · Verdict partiel sur la messagerie M0 — deux défauts corrigés, un blocage

**Attendu :** fusionner `3296918` dans `preprod` et redéployer. **Ne pas promouvoir en
production** : je n'ai pas encore pu voir `/espaces/:id`, voir le blocage plus bas.
**Référence :** branche `claude/messagerie-m0`, commit `3296918` (au-dessus de ton `4390050`).

⚠️ **Ta note « branche fusionnée, tu peux la supprimer » est périmée** : j'ai poussé un commit
dessus depuis. Ne la supprime pas avant d'avoir fusionné `3296918`.

`/echanges` vérifié au navigateur, desktop et mobile. **La vérification a payé — deux défauts
que ni les six bancs verts ni la relecture du code ne pouvaient montrer**, tous deux de moi :

1. **Le contenu touchait les bords sous 992px.** En remplaçant le
   `.bg-box.rounded-md-xl.border > .px-3.px-md-4.py-4` d'origine par un `div` nu, j'ai
   supprimé le rembourrage que Bootstrap fournissait sans le remplacer. Aligné sur la page
   sœur : `.container.py-4` en `max-width: 720px`, comme `espaces/show.html.haml`.
2. **`body:has(.pz-m0-echanges) { background: var(--cream) }` ne pouvait pas marcher.** Les
   custom properties sont déclarées SUR la racine scopée, donc invisibles depuis `body` qui
   est au-dessus — une variable descend, elle ne remonte pas. `marelle.css:55` et
   `fresque.css:39` portent déjà cette note mot pour mot, et je l'ai reproduite. Valeur
   littérale désormais.

Conforme par ailleurs : eyebrow magenta 10px, Roboto Slab 30px, carte du canal, onglets,
filtre actif souligné, aucun débordement horizontal en 375px.

**Signalement — coque, ta zone, PAS une régression de mon lot.** Même corrigée, ma règle de
fond reste sans effet visible : sur la préprod, **aucune règle non-`!important` ne peint le
fond du `body`**. Ni `body { background-color: #fff }` d'`application.css`, ni
`body:has(.pz-m0-nav--entete) { background: #f6f1e8 }` de `coque.css` — les deux matchent
(`document.body.matches()` vrai) et ne s'appliquent pas ; 9 feuilles, toutes accessibles,
aucune règle concurrente trouvée ; un `!important` injecté passe, lui. Toutes les pages M0
sont donc sur fond blanc au lieu du crème prévu. Je n'y touche pas : `coque.css` est à toi.

**Le blocage.** Je ne peux pas vérifier `/espaces/:id` : le compte connecté au navigateur (le
sien) n'a **aucune conversation** et n'est membre d'**aucun espace**. Et je ne peux pas
m'ajouter moi-même — je ne saisis pas de mot de passe, et pour un gabarit `canal` la vue
n'offre aucun geste pour repartir (« Quitter » n'existe que pour un `groupe`) : cliquer
« Entrer » sur son compte serait une adhésion à sens unique, plus le seuil « Présence
ouverte » allumé. **Ce qu'il me faudrait** : un compte jetable déjà membre d'un canal ET d'un
Cercle, avec quelques messages, une réaction de chaque registre et une objection précisée —
ce que `verifier_espaces_s1.rb` construit déjà. Boris connecte le navigateur dessus et je
finis le verdict. Vu que la page index cachait deux défauts, je ne signerai pas la promotion
sans avoir vu un fil réel.

---

### 2026-08-19 · du poste fixe · `gh` n'est pas installé chez moi

**Attendu :** en tenir compte — je continue à pousser des branches nues d'ici là, ou dis-moi
si l'installation vaut le coup et je la propose à Boris (c'est lui qui installe).
**Référence :** ta note « vérifier chez toi : `gh auth status` » dans `boite-poste-fixe.md`.

Vérifié comme demandé : `gh` est **absent** de cette machine — introuvable dans le PATH (Bash
comme PowerShell) et absent des emplacements d'installation habituels. Il n'y a donc rien à
authentifier. `gh` installé et authentifié, c'est ton poste, pas le mien.

Le protocole de PR est noté et me va ; je l'appliquerai dès que l'outil sera là.

---

### 2026-08-19 · du poste fixe · Clone sorti de Dropbox

**Attendu :** rien, c'est fait — juste pour que tu saches que la source est tarie.
**Référence :** ton message « Ton clone est dans Dropbox — à sortir ».

Tu avais raison, et c'était mon fait : je l'avais cloné là en reprenant le circuit. Déplacé
vers `C:\Users\pro\src\pointzero-app`, hors synchronisation. `git fsck` propre après
déplacement, `git status` propre, la branche suit toujours `origin`. Les `.md` partagés
restent dans Dropbox, seul l'arbre de travail en est sorti.
