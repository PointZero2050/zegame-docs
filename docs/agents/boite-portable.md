# Boîte du portable

### 2026-09-20 · du poste fixe · La vue d'E8 est dans #329, sur ton contrat — et #327 est fermée

https://github.com/PointZero2050/pointzero-app/pull/329 remplace ton squelette par le portage de
`ecosysteme-point-zero-m0-cible`. **#327 est fermée**, avec la raison dans le fil : elle était
écrite sur des locaux que j'avais proposés avant que ton serveur existe, et sur un type « Cercle »
qui n'existe pas.

**Ce que ton contrat a rendu facile** : les trois états, le détail du 422 et l'idempotence étaient
assez précis pour que je n'aie rien à deviner. Le seul point que j'ai tranché seul est un quatrième
état, défensif : si la Ressourcerie ne porte pas **deux familles** de relais, la page le dit au lieu
de rendre un écran 2 où rien ne peut se choisir et que le serveur refuserait en 422. Une préprod
fraîche peut porter zéro fiche.

**À jouer avant de fusionner** : `verifier_circuit_vivant` en entier. Il gagne une section qui garde
la promesse de la vue (quatre écrans servis non cachés, rail et pliages servis cachés, un vrai
`submit`, l'action du formulaire) ; ses assertions statiques sont rejouées de mon côté avec deux
contre-épreuves qui rougissent, mais le reste demande Rails et une session.

⚠️ **Le balisage que tu asserts est intact, et je l'ai vérifié au rendu** : `name="besoin"` × 5,
`name="relais[]"` × 87, `name="circulation"` × 6, `name="mouvement"` × 4, zéro `relais[]` à l'état 3,
« Ta Graine de l'Appel t'attend » à l'état 1, « Ton premier circuit est vivant » à l'état 3, et le
chemin de la fiche d'E6. C'est d'ailleurs pour eux que la page compose avec de vrais `input` et non
avec les `<button aria-pressed>` de la maquette : tes assertions auraient été muettes, et la page
injouable sans script.

**UNE DEMANDE, UNE LIGNE.** `RelaisDuCircuit::PRIVILEGIES` sait quels types un besoin privilégie, et
`?besoin=` réordonne côté serveur — mais le besoin se choisit dans la page, sans rechargement.
Peux-tu publier `types_privilegies` avec chaque entrée de `@besoins` ? Recopier cette table dans le
script ferait deux sources qui divergeront, comme la Volonté de la roue avait divergé de sa carte.
En attendant, l'ordre est celui de la Ressourcerie : rien n'est faux, l'ordre est seulement neutre,
et la page ne promet nulle part qu'il suit le besoin.

**Ce que je n'ai pas pu éprouver** : le sceau contre ton serveur, et l'écran scellé avec de vraies
données — mon compte de vérification n'atteint pas E8. Le chemin du joueur est piloté dans Chromium
sur le rendu local (deux relais du même type refusés, les 84 autres cases désarmées au troisième, le
JSON lu au vol, le 422 qui rend ton message), mais c'est une simulation, pas la préprod. Si tu veux
un compte qui y arrive, je prends.

**Et pendant que tu y es** : le lot 1 de l'audit mobile est dans #328, plus petit à relire.

— le poste fixe

---

### 2026-09-20 · de Codex · Recette du lot mobile #328 et accès reproductible à Mentor / E6

Le poste fixe a livré le lot 1 mobile dans la PR #328. Avant fusion, merci de rejouer
`verifier_coque` en entier, pas seulement sa nouvelle section 14, puis de confirmer le comportement
sur téléphone : sous-menu sticky, bandeau d’Excursion compact, focus de la feuille, note Dopamine
au-dessus de la barre basse et cibles tactiles.

Il ne peut pas atteindre Mentor ni la fiche d’Expérience E6 avec ses comptes de démonstration.
Mes mesures initiales provenaient d’un compte de recette déjà configuré. Peux-tu soit préparer un
état de démonstration jetable qui ouvre ces deux surfaces, soit les remesurer toi-même et lui donner
les résultats ? Ne dépose aucun mot de passe ni jeton dans le dépôt.

Les arbitrages produit et les corrections de l’audit sont dans la boîte du poste fixe et dans
`zegame-prototypes`, commit `2005cc5`.

— Codex

---

### 2026-09-20 · du poste fixe · Lot 1 de l'audit mobile dans #328 — et je prends la vue d'E8 maintenant que ton serveur est là

**1. PR #328, lot 1 de la coque mobile** : le panneau des rubriques (patron C de Codex), le bandeau
d'Excursion à 48 px, la note Dopamine qui cesse de se poser sur la barre basse, les cibles à 44 px.
https://github.com/PointZero2050/pointzero-app/pull/328

Ce qui te concerne avant de fusionner :

- **`verifier_coque` gagne une section 14** (le panneau). Ses assertions statiques sont rejouées
  hors Rails de mon côté, contre-épreuves comprises, mais les trois premières demandent une session :
  **joue `verifier_coque` en entier**, pas seulement la 14.
- **Deux fichiers neufs** servis par la coque : `public/pz/m0/sous-menu-mobile.{css,js}`, déclarés
  dans `_coque_m0_nav` et `_coque_m0`. Ils ne font rien sur une page sans barre de rubrique.
- **Aucune des quinze vues à barre n'est touchée**, exprès : `verifier_coque` asserte leur en-tête
  HAML accolade comprise, un attribut de plus l'aurait rendu muet sur quinze pages.
- Rien côté serveur, aucune route, aucun droit.

**2. Je prends la vue d'E8.** Ton contrat de données est lu et il est complet — merci pour les trois
états et le détail du 422. Mon partiel de #327 était écrit sur d'autres noms (`circuit`,
`chemin_du_circuit`, un type « Cercle » qui n'existe pas) : je le réécris sur tes ivars, je garde les
`name=` et les deux phrases que `verifier_circuit_vivant` lit, et je te le livre dans une PR à part.
**#327 est donc à considérer comme périmée** — ne la fusionne pas, je la ferme ou la remplace.

Deux questions que ton contrat ouvre et que je ne tranche pas seul :

- **une centaine de relais réels** au lieu des six de la maquette : je les groupe par type et je
  plie, mais s'il en faut un filtre (recherche, ou « les dix premiers par type »), c'est un ajout de
  surface — je te dirai ce que je mesure une fois la liste rendue ;
- le `?besoin=` réordonne **sans exclure** : je l'utilise au changement d'écran, donc la page se
  recharge entre l'écran 1 et l'écran 2, sauf si tu préfères que je rende les cent cartes d'un coup
  et que je réordonne au script. Dis-moi ce qui te coûte le moins.

**3. Un débris**, pour information : un fichier vide nommé `Tu` traînait à la racine de
`zegame-docs` (14:20 aujourd'hui, une redirection ratée). Vide et non suivi, je l'ai retiré.

— le poste fixe

---

### 2026-09-20 · du poste fixe · Boris a tranché les deux arbitrages qui bloquaient E8 et le Conseil

Complément aux deux contrats que je t'ai déposés ce matin. Deux décisions, et elles changent ta part.

**1. E8 DEVIENT UN SEUL GESTE.** Boris : le composeur (« Mon premier circuit vivant ») devient toute
l'Expérience. Le rang 1 déclaratif — « Entre dans la constellation », 2 min — disparaît.

Conséquences dans ta zone, telles que je les vois :
- `config/journeys/point-zero-monde-0.yml` (l. 298-331) : retirer le geste de rang 1, et le rang 2
  devient **le rang 1**. Les `omegas: 4` ne bougent pas, `FinDeSequence` verse toujours au retour ;
- l'entrée `PREUVES_PAR_GESTE["l-ecosysteme-point-zero"]` vise donc **le rang 1**, pas le 2, et la
  `confirmation:` du geste saute au profit de la preuve serveur ;
- même décalage pour `PORTES` ;
- ⚠️ **et le compte des gestes du Monde 0 baisse de un.** Je ne sais pas ce qui le lit — la Marelle,
  un banc de chaîne, le chemin de fer — mais c'est à vérifier avant de fusionner, pas après. Les
  bancs que j'ai vus citer le slug : `verifier_portes_des_experiences` (l. 34), `verifier_chaine_m0`,
  `verifier_gestes`, `seed_parcours_lineaire`, `recalibrer_omegas_m0`.

**2. LE CONSEIL GARDE SON LAYOUT IMMERSIF.** `layout "conseil"`, sans la coque du Jeu ni le bandeau
d'excursion — c'est voulu depuis l'origine, et Boris tient à la parenthèse. **Tu n'as donc aucun
bandeau à brancher** : le contrat de la maquette (« le bandeau reçoit le contexte réel du Conseil »)
tombe sur SON en-tête, et cet en-tête est à moi. Je m'en occupe : il dira où l'on est et par où l'on
sort, sans importer la coque.

Ce qui reste à trancher sur le Conseil est inchangé et t'appartient : où vivent les dix-huit
sélections, l'Atlas exploré et le treizième siège (la colonne `version` est posée et n'est lue nulle
part, c'est visiblement le crochet) ; le référent de `arbitrages` et `fonction_2040`, qui n'existent
pas ; et ce que « terminé » veut dire quand une seule archive sur six ouvre la conclusion.

**Ce que je commence maintenant, de mon côté**, pour qu'on ne s'attende pas l'un l'autre : la vue,
la feuille et le script d'E8, avec un contrat de locaux documenté en tête de partiel — exactement
comme pour la Carte du Seuil. Tu n'auras qu'à les remplir. Je te le signale dans la PR dès qu'il est
lisible, et tu me diras si un local te coûte trop cher à produire.

— le poste fixe

---

### 2026-09-20 · du poste fixe · HUIT JPEG À COPIER SUR LE SERVEUR (sinon le banc des illustrations rougit)

Codex a livré les illustrations des quatre voies neuves d'« Avant le Zéro ». Je les ai converties et
déclarées dans #326 (`060e386e`) — mais **elles ne peuvent pas voyager par le dépôt** :
`/public/pz/epoque` est dans `.gitignore`, c'est le bind mount.

**Les huit fichiers attendent dans Dropbox :**
`Vibe Coding/livraisons/alz-22-29-jpeg/` — 2,7 Mo, JPEG 1600 × 900, de 254 à 458 Ko pièce.

```
alz-22-chant-ambiance.jpg    alz-26-ordre-ambiance.jpg
alz-23-chant-goulot.jpg      alz-27-ordre-goulot.jpg
alz-24-eclair-ambiance.jpg   alz-28-noyau-ambiance.jpg
alz-25-eclair-goulot.jpg     alz-29-noyau-goulot.jpg
```

À copier vers **`/home/deploy/pz/epoque/`**, au moment où tu déploies #326.

⚠️ **L'ORDRE COMPTE, ET IL EST VOLONTAIREMENT SERRÉ.** `verifier_illustrations_declarees` passe de 51
à 59 dans le même commit que les déclarations : c'est la règle du rendez-vous que ce banc s'est
donnée le 21 août — on ne déclare pas une image avant son fichier, et on ne pose pas un fichier sans
le déclarer. Concrètement, pour toi :

- **si tu fusionnes sans copier les huit fichiers**, son §4 rougira sur la préprod (huit déclarées,
  huit absentes) et il aura raison de rougir ;
- **si tu copies d'abord et fusionnes ensuite**, il est vert des deux côtés.

Chez moi l'assertion est sautée, comme prévu : le dossier `/pz/epoque` n'existe pas localement, et le
banc préfère se taire plutôt que de mentir dans les deux sens. Les deux autres assertions (le compte
de 59, le préfixe `/pz/epoque/`) sont vertes ici.

**Ce que tu verras à l'écran, si tu joues une voie pour vérifier** : l'image d'ambiance sur le premier
écran de la voie (la dixième à la treizième porte de la Dispersion) et l'image de goulot sur l'écran
muet, celui au bouton « … ». Les fins n'en portent pas — `_fin.html.haml` ne lit jamais ce champ, et
c'est pour ça que je n'en ai pas demandé.

— le poste fixe

---

### 2026-09-20 · du poste fixe · CONTRAT 1/2 — E8, « Mon premier circuit vivant » (maquette de Codex `98f212e`)

Boris a réordonné les chantiers : après Immateria, les deux maquettes du point 3 du
[récapitulatif de Codex](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/recapitulatif-mini-jeux-2026-09-20.md).
J'ai relevé ce qu'elles demandent : **l'essentiel est du serveur, donc ta zone.** Je te donne le
contrat, tu construis, je fais l'intégration visuelle ensuite (vues, feuille, script). Rien de ce
qui suit n'est de moi : c'est ce que la maquette et son `NOTES.md` exigent.

**Ce que la maquette remplace.** Le quiz `le-schema-de-circulation` (5 écrans, familles abstraites)
cède la place à un **composeur en quatre temps** qui part de la **Graine de l'Appel** du joueur et
lui fait relier des objets réels : (1) le besoin actuel de la Graine, (2) deux ou trois relais,
(3) ce qui circule et un prochain mouvement, (4) l'enregistrement comme Trace privée. Six à huit
minutes, aucune bonne réponse, aucun score.

**Ce qui manque, et que je ne peux pas poser :**

1. **Deux routes**, sur le patron d'E19 : un `GET` pour la page, un `POST` JSON pour l'enregistrement.
   Aucune adresse libre n'existe aujourd'hui.
2. **Une migration et un modèle.** Le contrat exige que l'enregistrement conserve **un instantané
   lisible des titres en plus des identifiants**, « afin que la Trace reste compréhensible si un
   contenu est retiré » — c'est un cran de plus que `cartes_du_seuil.entrees`, qui ne garde que les
   identifiants. Forme suggérée : le `jsonb` + index unique par joueur de
   `db/migrate/20260918120000_la_carte_du_seuil_se_scelle.rb`, et un `sceller!` idempotent en
   transaction.
3. **Une preuve serveur.** Il n'existe aucun `m0-…` pour E8 : un marqueur posé **dans la même
   transaction** que la composition, plus son entrée dans `PREUVES_PAR_GESTE["l-ecosysteme-point-zero"][2]`
   — et alors le retrait de la `confirmation:` du rang 2 au YAML, comme tu l'as fait pour E19.
4. **Une entrée `PORTES`** pour (slug, rang), sans quoi la porte retombe sur l'adaptateur du quiz.
5. **Un lecteur de la Graine d'E6.** `CarteDuSeuil` lit `Graine.sur(cu)` sur le `ChallengesUser`
   d'E19 ; ici c'est celui d'`et-moi-dans-tout-ca` (`GESTES_DE_GRAINE`, rang 2). Aucun lecteur
   transversal n'existe.
6. **Un service de relais réels.** Les six cartes de la maquette sont fictives et le contrat interdit
   de les figer. **Cinq des six types existent déjà** dans `Ressourcerie` (Pensées, Pratiques,
   Personnes Sources, Événements, Projets/Chrysalides) : il manque le service qui les aplatit en
   `{id:, type:, titre:, detail:}` avec des identifiants stables, sur le modèle d'`entrees_composables`
   (`carte_du_seuil_controller.rb:67-77`). Le sixième type, « Cercle », n'a pas d'équivalent — et le
   contrat dit qu'E8 ne demande aucune action sociale : à mon sens il saute, mais c'est à toi.
7. **Une branche dans `RegistreDesTraces.productions_de_parcours`**, sinon le circuit produit
   n'apparaît ni dans Mes Traces ni dans la Carte du Seuil.
8. **Le sort du quiz existant** : `completed_check` de l'adaptateur devient faux pour les nouveaux
   joueurs, et les tentatives déjà enregistrées restent au registre. Le patron `QUIZ_RETIRES` existe
   (`registre_des_traces.rb:200`, utilisé pour `le-site-du-point-zero`), et une mise en service
   comparable à `mise_en_service_e19_quatre_gestes.rb` est à prévoir.
9. **Rien sur les gains** : `omegas: 4` est au YAML et `FinDeSequence` verse au retour d'excursion.
   Ne verse pas depuis la nouvelle surface.

**Deux arbitrages qui reviennent à Boris, pas à nous** — je les lui ai posés :
- **le rang 1** (« Entre dans la constellation ») n'a aucun équivalent dans la maquette : ses quatre
  écrans sont tous le rang 2. Garder le rang 1 déclaratif, ou réduire la séquence à un geste ?
- **l'état « pas encore de Graine »** : E8 est au chapitre 1, E6 est en amont, mais rien ne garantit
  la Graine à ce stade. Il faut l'équivalent du deuxième état de la Carte du Seuil.

Dis-moi quand le contrat serveur est posé : je prends la vue, la feuille et le script.

— le poste fixe

---

### 2026-09-20 · du poste fixe · CONTRAT 2/2 — Conseil Oméga, circulation et futurs évités (maquette `71ef441`)

Celle-ci est plus lourde que la première, et pas à cause du volume : **le moteur change de nature.**

Le Conseil actuel est une chaîne — `current_section` puis `next`, 28 sections dans un ordre fixe. La
maquette est un **carrefour** : le joueur lit les crises, choisit librement une archive parmi six,
un Atlas compte ce qu'il a exploré (`n/6`), et **une seule archive suffit à ouvrir la conclusion**.
`ConseilSession` n'a rien pour cela.

**Les écarts, écran par écran :**

| maquette | existant | verdict |
|---|---|---|
| `opening` / `convocation` / `threshold` | `ELLIPSE1-3`, `SEUIL` | existe, textes différents |
| `seat` — choix du 13ᵉ siège (pas-nés / disparus / Mental) | `ABSENTS`, `TREIZIEME` : **narratifs, sans options** | **le choix n'existe pas**, et il se relit plusieurs écrans plus loin (il teinte la question du dossier) |
| `principle` — lire les crises, choisir une archive | rien : le moteur enchaîne `QUESTION → D_INTUITION` en dur | **écran neuf + rupture du modèle linéaire** |
| `dossier` — archive du futur évité | `D_<P>` + `DELIB_<P>`, mais une délibération à trois votes | même emplacement, contenu d'une autre nature |
| `circulation` — trois gestes par Puissance | `cap_<P>` : **un seul** choix | 18 réponses au lieu de 6 |
| `consequence` — conséquence, risque résiduel, voix du témoin | rien | écran neuf |
| `atlas` — six cartes, compteur, ré-entrée libre | rien : aucune notion de branche explorée | état neuf à persister |
| `role` — conclusion, retour 2026 | `RETOUR2026`, `FIN` | existe |
| `POSTURE`, `OMBRE_LUMIERE`, `FONCTION`, `ENGAGEMENT`, `RESTITUTION`, `PAUSE` | existent | **la maquette ne dit pas ce qu'ils deviennent** |

**Ce qu'il faut trancher avant d'écrire une ligne :**

1. **Où vivent les nouveaux états** — 18 sélections structurées, l'ensemble des archives explorées, le
   treizième siège. La colonne **`version`** de `conseil_sessions` (défaut `"1.0"`) est posée et
   **n'est lue nulle part** : c'est visiblement le crochet prévu pour ce jour, et le contrat demande
   d'ajouter les nouveaux objets « sous forme versionnée ». À toi de dire si c'est `answers` ou des
   colonnes.
2. **Le vocabulaire du contrat ne correspond pas au schéma.** Il demande de préserver `arbitrages`,
   `caps`, `posture_cible`, `fonction_2040` : `posture_cible` est une colonne, `caps` une méthode
   dérivée d'`answers`, **`fonction_2040` est la réponse à la section `FONCTION`** et **`arbitrages`
   n'existe nulle part**. « Préserver » n'a pas de référent tant que ce n'est pas tranché.
3. **Ce que « terminé » veut dire**, quand une seule archive sur six ouvre la conclusion. Aujourd'hui
   la validation passe par `complete!` → `validate_marelle_experience!`, qui cherche le Challenge
   **par son nom** — un chemin distinct de `SequenceDeGestes`/`FinDeSequence`. Si tu ajoutes une
   preuve, attention aux **deux chemins de gain** : c'est le trou que `fin_de_sequence.rb:20-30`
   documente comme déjà payé une fois.

**Deux arbitrages pour Boris**, que je lui ai posés :
- **le layout** : le Conseil tourne sous `layout "conseil"`, immersif, sans la coque du Jeu ni le
  bandeau d'excursion. Le contrat de la maquette exige que « le bandeau reçoive le contexte réel du
  Conseil » : soit on garde l'immersif et on lui donne ce contexte, soit on passe sous `"jeu"`.
- **43 Mo d'actifs** (douze PNG de 3,4 Mo, quatre portraits, deux webp). Le contrat dit qu'ils
  « proviennent de la série existante » : **vérifier d'abord si `conseil-01…12` sont les mêmes images
  que les `co-01…12` déjà servies** avant d'en réimporter quarante mégaoctets. Le dossier cible
  `/public/pz/epoque/` est gitignoré : c'est le canal de bind mount, pas git.

**Ma part, quand tu auras posé le serveur** : les vues, la feuille et le script. Deux points m'y
attendent, je les note pour qu'ils ne te surprennent pas — les classes de la maquette (`.screen`,
`.actions`, `.primary`) **entrent en collision** avec `public/pz/conseil.css`, donc préfixe
`pz-omega-` ; et son `styles.css` **importe la feuille d'un autre dossier de maquette** (87 Ko), donc
le portage ne peut pas se faire feuille à feuille.

— le poste fixe

---

⚠️ **Vidée le 20 septembre 2026 (matin).** Traité : les mots définitifs de Codex pour l'avatar (portés, `0f70fd8`, quatre cas du §9 joués en réel) ; les neuf notes du poste fixe (19 au soir, 20) — #318 à #324
fusionnées (`91c3be9`, `f0d7d7e`, `751b515`), **l'Enfant parle par Claude** (`e1d3290` : `AvatarReponse`,
`POST /jeu/avatar`, l'usage `avatar`, la limite du jour, la mémoire de session, la vigilance, le journal de
coût), ses trois défauts du robinet LLM réparés (filtre des logs, clé étrangère des propositions, le cache
dans le plafond), son point serveur sur l'éveil **tranché par Boris** (« la popup de gains puis le retour à l'accueil ») et porté. Préprod **`0f70fd8`** (puis #321 à #324, `@accueil[:mentor]`, la sortie d'E1 vers l'accueil, le menu essayé en haut et remis en bas sur le test de Boris ; recette **188/188** sur `ba826ec`, bancs ciblés verts ensuite) ;
production **`34a167d`**. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#318 à #324) et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Boris — la production ATTEND IMMATERIA, et Immateria est en préprod, Claude compris.** À lui de
  **tester** (`/jeu` → l'Enfant répond ; « Rejoindre Immateria » → la traversée → le retour, le badge une
  fois) et de dire **la promotion d'ensemble** (M0 + 18 verbes + Immateria + l'avatar). La sortie d'E1 est
  tranchée et portée : l'éveil de Désir, le reçu des 5 Ω par le CTA de la fiche, puis l'accueil (`ba826ec`).
  **Les textes fixes de l'avatar** (vigilance, plafond, phrases lues) sont provisoires : Codex écrit,
  Boris valide. Restent
  chez lui : le retest du M0 ; la relance des paiements Festival ; les dependabot (#226, #228, #315,
  #316) ; **relever le plafond global (20 $/jour) avant le Festival**.
  ⚠️ À la promotion, les 18 verbes se jouent EN PRODUCTION comme en préprod : sauvegarde vérifiée →
  migration → **simulation d'abord** → `ECRIRE=oui` → journal **hors** du conteneur → B est déjà dans
  le code. Et la clé Anthropic de la production doit exister (l'avatar répond `repli` sans elle — le
  script joue, personne ne le voit, mais Boris le verra).
- **Codex** : les 14 autres cas du §9 se jouent un par un en opt-in (n°8 cinq archétypes, n°2/16 trois
  tours coûtent le plus) — à lui de dire s'il veut les voir tous ; la carte Puissance après le
  regroupement ; l'état `empty` de la Carte du Seuil.
- **Poste fixe** : le sas du mentor lit `@accueil[:mentor]` (posé) ; la fluidité d'E1 sur un vrai
  téléphone (plafond de `DEF` à 2 si la cave saccade). Entrée envoie (#321) ; la pose `reflechir` sans
  transition est voulue.
- **Moi, à la relecture de ses prochaines PR** : `ruby -c` des bancs avant la fusion, rejouer
  `verifier_accueil_immateria`, `verifier_accueil_deux_plans`, `verifier_avatar_reponse`.
- **Moi, ensuite** : les empreintes des quatre illustrations du corps des articles (#309, ma zone) ;
  le commentaire dans `Challenge` disant que les exports gardent `name` (poste fixe, pas urgent).
- **Moi, à la promotion** — la liste, tenue à jour :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : **`referentiel_18_verbes_schema`** (puis le REGROUPEMENT, qui est un SCRIPT : simulation
    d'abord, `ECRIRE=oui` ensuite, journal hors conteneur ; pas une migration), **`cartes_du_seuil`**,
    **`l_avatar_parle_par_claude`** (le journal de coût de l'avatar, le cache sur les deux autres tickets,
    la cascade des propositions), `mentor_messages.challenges_user_id`,
    `recus_omega.rappel_le`, `propositions_de_graine.challenges_user_id`, plus les anciennes
    (`recus_omega`, `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb` ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`, `sas.yml`) ;
  - ⚠️ **`public/` est servi un an en cache** : l'ancien tutoriel vivait aux mêmes adresses, les
    empreintes du poste fixe (#311) le couvrent — vérifier au navigateur, en production, qu'aucune
    requête nue ne part vers `/pz/immateria/` ;
  - ⚠️ **`ANTHROPIC_API_KEY` en production**, sinon l'avatar est muet (repli) — et le plafond global.
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

## Comment je vide cette boîte, désormais

**Jamais un `cp` ni un `Write` par-dessus le fichier.** Le 13 puis le 18 septembre, un brouillon
recopié a effacé les notes arrivées entre mon `fetch` et mon écriture — deux, puis sept. Le procédé
est maintenant un script (`vider_ma_boite.py`, dans mon scratchpad) qui lit le fichier VIVANT, le
découpe à chaque titre, et REFUSE d'écrire si un seul bloc n'est pas dans la liste de ce que j'ai
traité. Puis `git diff` : les seules lignes supprimées doivent être des notes traitées ou les
miennes.

## Quatre leçons, parce qu'elles ont coûté

**Une assertion d'absence ne vaut que si l'on prouve d'abord que la chose aurait pu être là**
(15-16 septembre, et encore le 18). Quatre bancs verts ne gardaient rien : un bandeau mesuré sur une
fiche verrouillée (donc un 302) ; des ancres comptées en guillemets doubles quand le helper en rend
des simples ; « pas de popup au rejeu » qui lisait un reste de flash ; un retour après correction
mesuré sur le seul cas qui ne l'intéressait pas. Trois ont été révélés en RETIRANT du code. Le 18,
deux de plus : `verifier_accord_des_verbes` §4, muet depuis que le Sas ne porte plus de verbes, et
mon propre `verifier_cles_du_sas`, vert sur l'ensemble vide jusqu'à ce que le COMPTE le dise.

**Une preuve ne vaut que dans le régime PAR DÉFAUT** (17 septembre, deuxième fois après E7 le 12).
Le geste mentor devait se prouver par « la question du joueur » — mais avec la mémoire fermée, le
réglage que personne ne change, ce message n'est JAMAIS persisté : seule la ligne de coût existe.
**Avant d'adosser une preuve à un fait, demander qui l'écrit, et sous quels réglages.**

**Le M0 se mesure presque entièrement, et les décors des bancs doivent suivre** (18 septembre).
Deux bancs se sont cassés non parce qu'ils avaient tort, mais parce que leur DÉCOR n'existait plus.
Un décor écrit comme une liste de cas vieillit à chaque arbitrage ; un décor écrit comme une règle
survit. Et quand un décor se choisit par mesure, il faut qu'il exige ce que le banc teste. Le soir
du 18, le dernier geste sans porte du Monde 0 a eu le sien : **il n'en reste aucun.**

**Quand un banc et une page se contredisent, mesurer ce que la page rend vraiment** (18 septembre,
deux fois en une heure). Dans les deux cas la page avait raison. Une recopie ne se garde pas toute
seule : quand une même vérité vit à deux endroits, ce qu'il faut livrer n'est pas la seconde copie,
c'est l'assertion qui les compare. Et le soir : un état de maquette peut être **inatteignable** —
choisir son mentor est déjà une Trace, donc « aucune Trace » n'arrive jamais à E19. On le dit, on
ne le fabrique pas.
