# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, tard dans la nuit.** Traité depuis la vidange de la nuit : #254 (Codex, « Confiance » → lecture provisoire) et #255 (le miroir de la drôle d'époque) — préprod `f398eaa`. Avant : la revue de Codex sur
`462092b` (partie serveur soldée), #252 (l'éveil entier à 650 px, le vrai bandeau d'excursion partout,
le troisième écran, l'emblème, la popup « Recommencer ») et #253 (le tiroir Dopamine sur le lot JSON,
la place anonyme des secrets). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le complément B des 18 verbes (après A, au mot de Boris) ; rien d'autre en attente.
- **Codex** : rien en attente.
- **Boris** : retest du M0 en préprod (`f398eaa`) — Recette A remise à zéro à 13 h 15 après le
  correctif `3fcfc5a` (l'Hypothèse ne valide plus E2 : la fin du sas valide et verse) ; la fusion de #202
  (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR
  dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` ET `scripts/mise_en_service_preuve_du_sas.rb` en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo`.

## 13 septembre (soir) — Poste fixe : la sortie des découvertes d'E2 et d'E6 retombe sur la carte du parcours — chez toi

Boris, en recette : « à la fin de la troisième étape de découverte de la Volonté, on aboutit sur `/parcours/point-zero-monde-0` et non sur l'expérience suivante ». Même chose pour Imagination depuis E6.

**Diagnostic (lecture du code, sans compte de recette) :**

1. `SequenceDeGestes::PORTES` donne aux rangs 3 `/parcours/eveil/volonte` (E2) et `/parcours/eveil/imagination` (E6). Leurs commentaires disent « par l'excursion ».
2. Mais `porte_visible` rend telle quelle toute porte qui commence par `/parcours/` (`return reelle if journey.nil? || reelle.start_with?("/parcours/")`). **Aucune excursion ne s'ouvre** donc pour ces deux sas.
3. `EveilsController#vu` fait alors `return redirect_to retour_excursion_path if Excursion.en_cours(session)`, qui est faux ici, puis `FinDeSequence.constater_pour_progression!`, puis **`redirect_to Excursion::REPLI`**, c'est-à-dire la carte du parcours.

**Ce que Boris attend : l'expérience suivante.** Depuis `3fcfc5a`, c'est justement la fin du sas qui valide E2 et E6, donc la suivante est ouverte au moment du POST. Deux pistes, à toi de trancher :

- **(a)** Dans `vu`, quand l'expérience d'activation vient d'être close, rediriger vers sa suite, avec le même calcul que `suite_apres_experience` (la fiche courante si la suivante reste fermée) plutôt que vers `REPLI`.
- **(b)** Ou envelopper ces portes dans l'excursion. Mais le retour ramènerait alors à la **fiche** d'E2 ou d'E6, pas à la suivante : un clic de plus que ce que Boris demande.

⚠️ **Le libellé suit la destination.** Le bouton final de l'éveil dit « Revenir à l'Expérience → » (arbitrage de Boris via Codex, v22). S'il mène à l'expérience suivante, ce mot devient faux. Je le signale à Codex. Dis-moi quelle destination tu retiens, je porterai le libellé qui va avec.

Côté poste fixe, dans la même recette : #256 retire « Refaire l'étape » et affiche « Recommencer cette Expérience » sur chaque panneau dès qu'une étape est faite.

— poste fixe

## 13 septembre (soir) — Poste fixe : E7 rang 2 est resté au raccord d'avant le v2 — « Découvrir Émotion » ouvre `/puissances/emotion`, pas le sas

Boris, sur `/parcours/point-zero-monde-0/experiences/choisir-qui-marchera-a-mes-cotes` :
- « "Découvrir Emotion" renvoie à `/puissances/emotion` et non au mini-jeu de découverte de l'Émotion » ;
- « il ne devrait pas y avoir de CTA "J'ai découvert la Puissance Emotion" mais "Revoir la découverte d'Emotion" avec "Expérience suivante" et "Recommencer cette Expérience", comme dans les Expériences précédentes ».

**Diagnostic (lecture de `f398eaa`).** E2 et E6 ont reçu leur sas v2, E7 non :

| | E2 rang 3 (Volonté) | E6 rang 3 (Imagination) | **E7 rang 2 (Émotion)** |
|---|---|---|---|
| `PORTES` | `/parcours/eveil/volonte` | `/parcours/eveil/imagination` | **`/puissances/emotion`** |
| `PREUVES_PAR_GESTE` | `sas_franchi?` | `sas_franchi?` | **absent** (seul le rang 1, mentor + question) |
| `SAS_D_EVEIL` | rang 3, `volonte` | rang 3, `imagination` | **absent** |
| YAML `confirmation` | aucune | aucune | **« J'ai découvert la Puissance Émotion »** |

Le rang 2 est donc **déclaratif** : porte d'excursion vers la page de la Puissance, puis confirmation à la main. Même le « Revoir la découverte d'Émotion » d'un compte achevé (`nino`) passe par `/excursion/ouvrir/…/2`, qui mène à la page de la Puissance, pas au sas.

**À reproduire pour E7, sur le patron d'E2/E6 :**
1. `PORTES["choisir-qui-marchera-a-mes-cotes"][2]` → `/parcours/eveil/emotion`.
2. `SAS_D_EVEIL["choisir-qui-marchera-a-mes-cotes"]` → `rang: 2, territoire: "emotion"`, avec pour `activation` la preuve du rang 1 (mentor choisi ET question enregistrée).
3. `PREUVES_PAR_GESTE[…][2]` → `sas_franchi?("choisir-qui-marchera-a-mes-cotes", user)`.
4. Validation et versement à la fin du sas, comme `3fcfc5a` pour E2/E6 (« une expérience dont le sas est un geste se ferme à la fin du sas »). Vérifie aussi que `Eveil.ouvrable?(user, "emotion")` s'ouvre dès le rang 1 fait.
5. YAML : retirer `confirmation` du rang 2 (le sas fait foi). Son `explication` décrit encore la page de la Puissance ; je demande le texte à Codex.

**Rien à faire côté vue.** Une fois le rang prouvé, `_passage` rend déjà « Revoir la découverte d'Émotion », « Expérience suivante » et, avec #256, « Recommencer cette Expérience » sur chaque panneau.

⚠️ **La même question de sortie qu'E2/E6** (mon message de tout à l'heure) : `/parcours/eveil/emotion` n'ouvre pas d'excursion (`porte_visible` laisse passer `/parcours/`). Sans correctif, la fin du sas d'Émotion retombera elle aussi sur la carte du parcours. Autant régler les trois ensemble.

— poste fixe

---

### 2026-09-13 (soir) · du poste fixe · branche `bandeau-trois-lignes-et-traces` poussée — PR sur `preprod`, à fusionner

Boris sur `/mes-traces` : « toujours l'ancienne version du bandeau » puis « 3 lignes à gauche », et « la même illustration générique pour certaines Traces ».

1. **`public/pz/m0/excursion.css` — feuille PARTAGÉE.** L'identité du bandeau passe en grille sur trois lignes à TOUTES les largeurs (8/15/8 px ; l'ancien palier 900 devient la règle de base). L'éveil, les excursions et le Conseil changent avec elle. Calage 536, pastille, rail et palier 600 intacts. Mesuré sur la préprod servie avec la feuille locale : 1440, 899 et 390 px, aucun débordement.
2. **`mes_traces/_carte`** : une source sans `challenge` retrouve son expérience :
   - `Trace` par `Monde0Etats::Lecture::ACTIVATIONS[territoire]` ;
   - les quatre sessions (procès, traversée, Conseil, Moteur) par une table nom → slug ;
   - `PuissanceAssessment` → `/pz/m0/powers/<puissance>.webp`.
   ⚠️ C'est un `Challenge.find_by(slug:)` par carte concernée. Si tu préfères une table chargée une fois dans `MesTracesController`, dis-le : le partiel n'a qu'une ligne à changer.
3. **Bancs à rejouer à la fusion** (pas de Ruby ici) : `verifier_excursion` (identité en grille à la base) et `verifier_traces_parcours` §5bis. Ce dernier pose un diagnostic d'Émotion, lit les cartes rendues et compare l'illustration de la roue à `url_de_version(cover || photo, :medium)` du procès.

— poste fixe
