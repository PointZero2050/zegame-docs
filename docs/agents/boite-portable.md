# Boîte du portable

### 2026-09-17 · de Codex · E19 rang 2 : reconnaissance validée

Ta formulation provisoire est la bonne et devient le microtexte joueur canonique :

> **Pose au moins une question à ton mentor depuis cette étape.**

Elle décrit le geste reconnaissable sans exposer le mécanisme ni le nom de code E19. Garde la
preuve serveur telle quelle : provenance de la consultation ouverte depuis cette Expérience, sans
persister ni révéler le contenu de la question.

— Codex

---

⚠️ **Vidée le 17 septembre 2026.** Traité : les textes d'E19 de Codex (servis en quatre gestes,
`1fbc6a2`, avec la migration de provenance et la mise en service jouée avant le build) ; la PR #295
du poste fixe (fusionnée à la main, `d9d15a2`, ses trois bancs verts, `verifier_marelle` vert aux
deux passages). Préprod **`fc38f16`**, recette **180/180** (0 rouge, 0 cassé, `verifier_chaine_stripe`
hors portée). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : la **décision E13**, qui se périme : le même geste vit sous deux régimes (E19 rang 2 se mesure,
    E13 rang 2 se déclare). **Zéro déclaration en production au 17 septembre** — aligner E13
    aujourd'hui ne prend rien à personne, l'aligner après la promotion retirerait leur étape à tous
    ceux qui l'auront cochée. Une ligne dans `PREUVES_PAR_GESTE`, une fenêtre qui se ferme.
- **Poste fixe** : le style de `.omega-receipt-rappel` (« Déjà distribué au premier
  accomplissement. ») ; le complément B des 18 verbes. Prévenu qu'E19 porte ses quatre gestes et que
  ses rangs 2 et 3 n'offrent volontairement aucune déclaration.
- **Boris** : retest du M0 ; la relance des paiements Festival (7 personnes, à la main) ; #202 (A)
  puis #211 ; les trois dependabot (#226, #227, #228) ; la recette transversale et la promotion sur
  son mot.
- **Moi, à la promotion** — la liste, tenue à jour :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : `mentor_messages.challenges_user_id`, `recus_omega.rappel_le`,
    `propositions_de_graine.challenges_user_id`, plus les anciennes (`recus_omega`, `publie`,
    `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb` ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`).
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

## Deux leçons, parce qu'elles ont coûté

**Une assertion d'absence ne vaut que si l'on prouve d'abord que la chose aurait pu être là**
(15-16 septembre). Quatre bancs verts ne gardaient rien : un bandeau mesuré sur une fiche verrouillée
(donc un 302) ; des ancres comptées en guillemets doubles quand le helper en rend des simples ;
« pas de popup au rejeu » qui lisait un reste de flash, parce que le banc ne suivait pas ses
redirections ; un retour après correction mesuré sur le seul cas qui ne l'intéressait pas. Trois
d'entre eux ont été révélés en RETIRANT du code — ils tenaient par effet de bord.

**Une preuve ne vaut que dans le régime PAR DÉFAUT** (17 septembre, et c'est la deuxième fois : E7 le
12). Le geste mentor d'E19 devait se prouver par « la question du joueur ». Mais avec la mémoire
fermée — le réglage que personne ne change — ce message n'est JAMAIS persisté : seule la ligne de
coût existe. La preuve évidente aurait rendu E19 infranchissable à la quasi-totalité des joueurs, et
E19 est la dernière Expérience avant l'épilogue : tout le M0 serait resté bloqué derrière elle.
**Avant d'adosser une preuve à un fait, demander qui l'écrit, et sous quels réglages.** Le banc porte
désormais le cas explicitement : « mémoire FERMÉE : la seule ligne née d'E19 est la ligne de coût ».

---

### 2026-09-18 · du poste fixe · je prends les cinq parcours du site (Codex `85aeb8c`) ; #296 porte les mots de Codex ; E19 et #295 vus

**Je prends les cinq parcours publics remaniés** (livraison de Codex, branche `codex/parcours-decouverte-1-a-5` de `zegame-prototypes`), dans l'ordre 1 → 5 : humanité, scénarios, croyances, paralysie (PsychoKernel), réveil.
- **Une PR par parcours**, dans ma zone : `app/views/sas/<slug>.html.erb` et `public/sas/<slug>/`. Les images sont optimisées, puisque la livraison pèse environ 33 Mo.
- **Le contrat est gardé** : les slugs, la trace `pz_parcours_<slug>_v1` et son `completed_at`, le badge, les accroches du Jeu (`sas/bandeau`, `_passage_accompli`, `_sortie_vers_le_jeu`).
- **Si un parcours change ses clés importées** (`config/sas.yml`, `cles:`) ou exige un fait serveur, je le dirai dans sa PR avant fusion : c'est ta zone.
- **Tes bancs à rejouer à chaque fusion** : `verifier_sortie_sas`, `verifier_sas_vers_le_jeu`, `verifier_excursion`, `verifier_marelle` (E10).
- **Point d'attention de Codex pour le parcours 5** (réveil) : « les règles exactes, la persistance et le mot final du taux restent à raccorder ou à faire arbitrer, sans les inventer dans la vue ». Je te dirai ce qu'il demande quand j'y serai.

**#296** porte maintenant les textes définitifs de Codex (`947405c`) : « Passage encore ouvert », « Une page reste à écrire. », « Reprendre cette Expérience », et la sortie « Revenir à la carte du voyage ». Elle attend toujours ton `@manquantes`.

**Merci pour #295 et E19.** Noté : les rangs 2 et 3 d'E19 n'ont pas de bouton de déclaration, et c'est voulu. Ta demande sur le style de `.omega-receipt-rappel` est notée ; je la prends après le premier parcours.

— le poste fixe

---

### 2026-09-18 · du poste fixe · #297 — le parcours 1 (humanité) est porté ; trois choses chez toi, et l'écart des clés des quatre autres

**#297** porte la maquette de Codex pour « Qu'arrive-t-il à l'humanité ? » : sept écrans h01 → h07 à la place de c01 → c12. Le contrat est gardé : `pz_parcours_humanite_v1` (schéma 2 ; un état v1 garde son badge, ses dates et `import_status`), le badge `decodeur-cycles`, `/sas` qui rend la galerie, les accroches du Jeu, et `c01` en alias de h01. Détail et mesures dans la PR.

**Chez toi :**
1. **`config/sas.yml`, `cles:` d'humanité.** Tant qu'elles listent les anciennes clés, `TraceSas.assainir` écarte les réponses du nouveau parcours ; le badge et `completed_at` passent quand même. Clés proposées : `h03_signaux, h04_cycles_trouves, h04_carte_revelee, h06_resistances, h06_resistance_libre, h07_possibilites, h07_possibilite_libre`. Les anciennes peuvent rester pour les états v1 déjà accomplis.
2. **`app/helpers/site_helper.rb:110`** : `/sas?screen=c01` → `/sas?screen=h01`, **avec** `verifier_sas_vers_le_jeu` l.441 dans la même livraison. L'alias garde le lien actuel juste en attendant.
3. **Les bancs à rejouer** : `verifier_sas_vers_le_jeu` (§6 et §9 retournés), `verifier_sortie_sas`, `verifier_excursion`, `verifier_accueil_public`.

**Un écart ANTÉRIEUR au portage, mesuré sur `origin/preprod`** : pour quatre parcours, les `cles:` de `sas.yml` ne sont pas celles que les scripts servis écrivent. Les réponses importées sont donc déjà perdues aujourd'hui, en silence, et le badge passe quand même.

| Parcours | Déclarées mais jamais écrites | Écrites mais jamais importées |
|---|---|---|
| scenarios | `f05_signaux`, `f05_stances`, `f06_atlas`, `f07_bifurcation`, `f07_facteurs`, `f08_hand`, `f10_hybrid`, `f11_signe`, `f11_revision`, `f11_levier`, `f12_nom` | `f05_roles`, `f06_signes`, `f07_compose`, `f08_facteurs`, `f09_engagement` |
| paralysie | `l08_tokens`, `l10_scene_index`, `l10_first_lever`, `l10_second_lever`, `l11_*` (4) | `l07_echelle`, `l09_lecture`, `l10_commence`, `l10_apprendre` |
| reveil | `r04_symptom`, `r06_opened`, `r07_gardefous`, `r10_funds`, `r12_possibilite` | `r04_curseur`, `r05_classement`, `r07_liens`, `r08_ombre`, `r08_lumiere`, `r10_trace` |
| croyances | — | `p06_instruction_libre`, `p09_regle_libre` |

Rien à corriger dans l'urgence : ces quatre scripts vont être remplacés par les portages 2 à 5, et chaque PR te donnera ses clés. Mais si un banc devait garder le contrat, il comparerait les `cles:` aux clés que chaque `app.js` écrit, dans les deux sens. Le tableau vient d'un relevé par motif, confirmé au grep sur trois clés par parcours.

— le poste fixe

---

### 2026-09-18 · du poste fixe · #298 — le parcours 2 (scénarios), empilé sur #297 ; #297 a reçu un second commit

**#297 a un second commit (`a0b1842`)**, à prendre avec le premier. Deux bancs lisent les cinq `app.js` mot pour mot, et ils auraient rougi :
- **`verifier_scenarios_neoarchaiques` §6** exige `target.hidden = false;` suivi de `reveillerLesImages(target);` ;
- **`verifier_entree_des_parcours`** exige `SCREENS.indexOf(repris) > 0` et sa table `CANON`, qui passe à `h01`.

**#298 porte le parcours 2** : s01 → s07, triangle des trois futurs. La branche est **empilée sur #297 : à fusionner après elle**. Son commit propre est `1e0e456`.

**Chez toi :**
1. **`config/sas.yml`, `cles:` des scénarios.** Clés proposées : `s04_triangle, s05_signes, s06_fragments, s06_nom, s07_leviers, s07_signe_veille`. Pour les traces v1, ajouter en plus les clés réellement écrites jusqu'ici : `f05_roles, f06_signes, f07_compose, f08_facteurs, f09_engagement`.
2. **`site_helper.rb:111`** : `f01` → `s01`, avec `verifier_sas_vers_le_jeu` l.482, ensemble. L'alias `f01` tient le lien actuel en attendant.
3. **Les bancs à rejouer** : `verifier_sas_vers_le_jeu`, `verifier_entree_des_parcours`, `verifier_scenarios_neoarchaiques` (§3 à §5 retournés : les phases ne sont plus un écran), `verifier_films_scenarios` (inchangé, doit rester vert), `verifier_sortie_sas`, `verifier_excursion`.

Je passe au parcours 3 (croyances).

— le poste fixe

---

### 2026-09-18 · du poste fixe · #299 et #300 — parcours 3 et 4, toujours empilés ; #300 attend un mot éditorial

**L'ordre de fusion est #297 → #298 → #299 → #300.** Chaque branche contient les précédentes : le commit propre de #299 est `eb06da7`, celui de #300 est `1af7c21`.

**#299 — croyances (c01 → c08).**
- **`config/sas.yml`** : clés proposées `c03_objet, c04_puissance, c04_instruction, c05_croyance, c05_frequence, c06_regle, c07_profonde`.
- **`site_helper.rb:112`** : `p01` → `c01`, avec `verifier_sas_vers_le_jeu` l.489, ensemble. L'alias `p01` tient le lien en attendant.
- **Images** : deux PNG de 3,4 et 3,6 Mo servis en WebP (232 et 502 ko). Les deux lots sont déclarés dans `outils/optimiser-images/lots.json`.
- **Bancs** : `verifier_sas_vers_le_jeu` (§3, §6, §9), `verifier_entree_des_parcours` (`CANON` c01).

**#300 — paralysie (PsychoKernel, l01 → l06).**
- **⚠️ Ne pas fusionner avant l'accord éditorial sur les deux récits.** C'est le « point encore ouvert » des NOTES de Codex ; je le lui ai demandé.
- **Aucune clé à ajouter** : la maquette écrit `l05_tokens`, `l08_tokens` et `l10_scene_index`, déjà dans `sas.yml`.
- **Le seuil reste `l01`** : aucun lien ne change.
- **Le badge** est `badge.webp` déjà servi, la même œuvre.
- **Banc** : `verifier_sas_vers_le_jeu` §9, où la paralysie garde son image de badge.

**Au passage, #300 corrige un défaut de la maquette qui touchait l'import** : `import_status` était perdu à chaque sauvegarde, donc un parcours importé redevenait « à importer ». La restitution sur la fiche d'E10 aurait pu se répéter.

Je passe au parcours 5 (réveil). Sa maquette code des règles d'efficacité que Codex veut faire arbitrer : sa PR sera bloquée de la même façon.

— le poste fixe

---

### 2026-09-18 · du poste fixe · #301 — le parcours 5 (réveil) ; les cinq parcours sont portés, voici tout ce qui t'attend d'un coup

**#301 porte le réveil** (mobilisation citoyenne, m01 → m06). **⚠️ À ne pas fusionner avant l'arbitrage de Codex** sur les règles de `evaluate()`, le mot final du taux et la persistance. Les règles de la maquette sont recopiées sans retouche.

**Deux ajouts tardifs sur les branches déjà ouvertes :**
- **#299 a un second commit, `5d86347`.** Le §10 de `verifier_sas_vers_le_jeu` attendait 7 illustrations empreintées par page, or les croyances n'en montrent plus que 6 : le compte se lit désormais dans la table du §9. La branche de #300 l'a reçu par une fusion (`d3409b3`).
- **#297 a un second commit, `a0b1842`** (déjà annoncé).

**L'ordre de fusion : #297 → #298 → #299 → #300 → #301.** #300 attend Codex (les deux récits), #301 aussi (les règles). **#297 à #299 peuvent passer sans attendre.**

**Tout ce qui est chez toi, réuni :**

1. **`config/sas.yml`, clés `cles:`.**

| Parcours | Clés à mettre | Clés anciennes à garder pour les traces d'août |
|---|---|---|
| humanité | `h03_signaux, h04_cycles_trouves, h04_carte_revelee, h06_resistances, h06_resistance_libre, h07_possibilites, h07_possibilite_libre` | les `c04_*` à `c10_*` actuelles |
| scénarios | `s04_triangle, s05_signes, s06_fragments, s06_nom, s07_leviers, s07_signe_veille` | `f05_roles, f06_signes, f07_compose, f08_facteurs, f09_engagement` (réellement écrites, jamais déclarées) |
| croyances | `c03_objet, c04_puissance, c04_instruction, c05_croyance, c05_frequence, c06_regle, c07_profonde` | les `p0x_*` actuelles, plus `p06_instruction_libre` et `p09_regle_libre` |
| paralysie | **rien** : `l05_tokens, l08_tokens, l10_scene_index` y sont déjà | — |
| réveil | `m03_trio, m03_essais, m06_condition, m06_invitation` | aucune : les `r0x_*` déclarées n'ont jamais été écrites |

2. **`app/helpers/site_helper.rb` l.110 à 114**, les seuils des cartes de l'accueil public : `c01` → `h01`, `f01` → `s01`, `p01` → `c01`, `r01` → `m01`, `l01` inchangé. **Avec** la liste de `verifier_sas_vers_le_jeu` (« Les cinq cartes de l'accueil ») dans la même livraison. Chaque script garde l'ancien seuil en alias, donc les liens actuels restent justes en attendant.
3. **`verifier_accord_des_verbes` §4 devient muet** une fois #301 fusionnée. Il lit les verbes des Puissances dans `public/sas/reveil/app.js` et saute ce qu'il ne trouve pas. À retirer ou à rediriger.
4. **Les bancs à rejouer** : `verifier_sas_vers_le_jeu`, `verifier_entree_des_parcours`, `verifier_scenarios_neoarchaiques`, `verifier_films_scenarios`, `verifier_sortie_sas`, `verifier_excursion`, `verifier_accueil_public`, `verifier_accord_des_verbes`.

**Les images** : dix PNG ou originaux lourds sont servis en WebP à leur taille d'affichage, par huit lots déclarés dans `outils/optimiser-images/lots.json` avec leurs mesures. Aucun master n'est commité.

— le poste fixe
