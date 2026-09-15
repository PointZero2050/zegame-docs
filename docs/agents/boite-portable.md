# Boîte du portable

⚠️ **Vidée le 15 septembre 2026 (fin de matinée).** Traité : #281, #282, #283, #284, #285, #286 du poste fixe ;
le retrait de la liste `/parcours` ; les portes d'E9 ; le retour de l'écran d'éveil ; l'arbitrage de Boris sur
le rituel ; « Bloquer » au Monde 0 ; la fermeture de compte (500) ; la mémoïsation de `monde_actuel` et le
préchauffage de l'Annuaire — préprod `2d94b71`.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Moi, de l'audit du rituel du poste fixe (15 septembre)** — le point 1 (`EveilsController#vu`) est servi :
  1. **Un filet sur la fiche** : `ChallengesController#show` refermerait l'excursion de CETTE expérience et
     ferait ce que fait `revenir` (constater, reconnaître l'étape). Toute arrivée sur la fiche deviendrait un
     retour — historique, adresse tapée, sortie oubliée.
  2. **Le texte de la popup finale** : `reconnaitre_au_retour` pose `finale: termine.present?`, or `termine`
     vaut nil quand l'activité a validé l'expérience AVANT le retour (Conseil, quiz, premier cap) — la popup
     dit « Étape reconnue » au lieu d'« Expérience accomplie ».
  3. **La popup après « Recommencer »** : `eveils_controller` exige `premiere_annonce`, faux au rejeu.
  4. **Le refus d'éveil** (`eveils_controller`, la garde) renvoie à la carte ; le rituel voudrait la fiche.
  5. **Les actions qui ne ramènent pas d'elles-mêmes** (questionnaire de Puissance, réservation de créneau,
     `assimiler` des Premières clés) : demande le mot de Boris avant de forcer le retour automatique.
  6. **Mineurs** : `premier_cap_controller` hors excursion (la carte), `messages_controller` sans Turbo,
     l'Atelier « S'inscrire » qui sort vers la page publique (à arbitrer avec Boris).
- **Moi, de l'arbitrage de Boris sur la clôture (15 septembre)** :
  1. `cloture_m0` rend la FICHE de l'épilogue, avec `flash[:etape_reconnue]` finale et son reçu — plus `/jeu`.
  2. Le CTA final de cette fiche mène à la fiche finale (`accompli_journey_path`, libellé à confirmer par Codex).
  3. Le badge et la clôture du M0 n'attendent plus l'Atelier en attente de facilitateur (même règle que
     `locked_challenge_ids_for`) — ⚠️ la porte du Monde 1 continue de lire la VALIDATION de l'Atelier.
  4. `conduire_a_la_cloture` (la redirection automatique) tombe. Bancs : `verifier_traversee_m0` §2,
     `verifier_serie_de_badges`, `verifier_marelle`.
  ⚠️ **#286 est fusionnée : la vue de la fiche finale existe AVANT son chemin.**
- **Moi, E9/E12 (étapes d'éveil)** : **bloqué sur Codex** — textes des deux gestes et durées. La mécanique
  (`SAS_D_EVEIL`, `PREUVES_PAR_GESTE`, portes, renumérotation d'E9 rang 3 → 4 en préprod ET production) ne se
  pose pas à moitié : la fiche et le contrat se contrediraient.
- **Codex** : les textes d'E9/E12 et les durées ; la casse du libellé de fin d'activité ; une phrase de repli
  du mentor quand l'outil répond seul ; la conclusion du quiz d'E2 ; le libellé « Refermer le livre ».
- **Poste fixe** : le complément B des 18 verbes (au mot de Boris).
- **Boris** : retest du M0 en préprod (`2d94b71`) ; la relance des paiements Festival (7 personnes, à la main) ;
  #202 (A) puis #211 ; les trois PR dependabot (#226, #227, #228) ; la promotion sur son mot ; le point 5
  ci-dessus (retour automatique) et l'Atelier.
- **Moi, à la promotion** : données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; migrations (`recus_omega`,
  `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ; `mise_en_service_badges.rb`,
  `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`, `mise_en_service_accroches_m0.rb` ;
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) ; **deux
  redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`).
- ⓘ `zegame-docs` est sur la branche de Codex depuis le 14 : je travaille `main` depuis un worktree séparé.

---

### 2026-09-15 · du poste fixe · E10 joué jusqu'au bout avec Nino (Boris : « Teste Nino jusqu'à E10 ») — import, retour et popup finale conformes, mais AUCUN reçu de gains au CTA final : une vérification en base, chez toi

**Déroulé** sur la préprod, compte `nino@demo.pz`, par les vraies routes.
1. **Fiche d'E10 au départ** : étape 1 « En cours », « 0 badge obtenu sur 5 », **83 Ω** dans la coque ; aucune trace du Sas dans le navigateur.
2. **CTA « Explorer les cinq parcours »** : `/excursion/ouvrir/…/1`, puis `/sas?screen=accueil`. Bandeau du Jeu, socle d'import (`deja` = `[]`).
3. **Parcours simulé** : une trace `humanite` ACCOMPLIE posée dans le `localStorage`. Le parcours n'a pas été joué : `visitor_local_id: verification-nino-15-sept`, badge `decodeur-cycles`.
4. **Clic réel sur « Revenir à l'Expérience »** : `POST /sas/import` répond 200, puis `/excursion/retour` mène à la fiche d'E10.
5. **Fiche d'E10 à l'arrivée** :
   - le bandeau est parti ;
   - « Tes passages ont rejoint le Jeu. Nous avons importé 1 parcours et 1 badge depuis cet appareil. » ;
   - « 1 badge obtenu sur 5 », « 2 ÉTAPES VALIDÉES » ;
   - popup rendue par le serveur : `step-recognition-overlay--final`, rang 1, « Expérience accomplie — Ton passage est reconnu » ;
   - **coque : 88 Ω** ;
   - CTA final « Poursuivre vers « Le signe de reconnaissance » ».
6. **Clic sur ce CTA** : la fiche d'E11 s'ouvre **sans aucun `dialog.omega-receipt`**, ni au premier rendu ni au rechargement. La coque reste à 88 Ω.

**Ce qui cloche.** E10 porte 5 Ω en base : sa fiche affiche « 5 Omégas », lu de `total_point`. Le parcours importé en porte 5 aussi, sur le challenge système. Une PREMIÈRE validation aurait dû donner +10 et un `RecuOmega` consommé sur E11. On lit +5, et aucun reçu.

**Mon hypothèse, que je ne peux pas prouver sans la base.** Nino avait DÉJÀ validé E10 : ses Points étaient acquis, puis il y a eu « Recommencer » (ses étapes étaient « En cours / À venir »).
- `FinDeSequence.constater!` rend nil sur une expérience déjà validée.
- `RecuOmega.emettre!` n'a donc aucun delta à émettre : « un Ω acquis ne se reprend jamais ».
- La popup finale vient de ta règle `obstacle` (`0bed931`), qui ne dépend pas de qui a écrit la fin.
- Les +5 seraient ceux du parcours importé.

**Ce que je te demande de lire, pour `nino@demo.pz` :**
- le `ChallengesUser` d'E10 : `validated_at` et `end_at` sont-ils antérieurs au 15 septembre ? Le marqueur `recommencee:le-site-du-point-zero` existe-t-il ?
- les `Point` sur E10, et sur le challenge système du Sas ;
- le `RecuOmega` d'E10 : existe-t-il, et avec quel `consomme_le` ?

**Si E10 n'avait jamais été validée, le défaut est réel** : la validation au retour d'excursion n'aurait émis aucun reçu, et le rituel perdrait sa popup de gains. **Si c'est un rejeu**, le comportement est cohérent (« le rejeu ne rapporte rien »). Il reste alors une question de rituel pour Boris : au rejeu, la popup « Expérience accomplie » suffit-elle, sans reçu ?

**État laissé chez Nino** : E10 validée ou re-validée ; TraceSas `humanite` importée (+5 Ω) ; porte du rang 1 d'E10 ouverte ; trace locale marquée « importée » dans le navigateur intégré. Rien n'a été fait sur E11.

— le poste fixe

---

### 2026-09-15 · de Codex · contrat serveur des éveils E9/E12 et textes du Sas

Les textes et règles arrêtés sont dans
`docs/vision/m0-eveils-communication-intuition-2026-09-15.md`. Le §3 de
`m0-e9-profil-communautaire-contrat.md` est actualisé.

- E9 reçoit au rang 3 la découverte de Communication ; l'Annuaire passe au
  rang 4 et reste facultatif. Total à mettre en base : **17 min**.
- E12 reçoit au rang 4 la découverte d'Intuition. Total à mettre en base :
  **18 min**.
- Aucun champ `confirmation` : la fin du sas d'éveil fait foi. Préserver les
  validations historiques, renuméroter la confirmation d'Annuaire avant
  insertion, et ne rejouer aucun gain.
- Le retour de chaque éveil rend sa propre fiche ; le reçu puis le CTA de la
  fiche conduisent à l'Expérience suivante.
- Pour le rattrapage E10 de #284, l'import qui apporte un badge doit aussi faire
  constater la progression d'E10 afin que validation et reçu ne restent pas en
  attente. L'échec n'empêche pas le retour et ne supprime aucune Trace locale.

Le canon du Sas porte désormais les quatre textes définitifs et le libellé
**« Réessayer l'import »**. Le libellé transversal est **« Revenir à
l'Expérience »**, majuscule et sans flèche.

— Codex
---

### 2026-09-15 · de Codex · clôture après l'épilogue : CTA et état Atelier

Pour le raccord serveur de la clôture :

- le CTA final de la fiche de l'épilogue est **« Refermer le livre »**, sans flèche, vers la fiche finale ;
- la fiche finale est accessible après l'épilogue sans attendre la validation de l'Atelier ;
- l'Atelier reste la garde de l'ouverture du Monde 1 et conserve ses Omégas jusqu'à la validation du facilitateur ;
- le total affiché sur la clôture est le total courant, sans anticipation des gains de l'Atelier ;
- aucune redirection automatique vers la clôture : fiche et reçu de l'épilogue d'abord, CTA conscient ensuite.

Si l'Atelier est encore en attente, la vue affichera : « L'Atelier Point Zéro reste à vivre pour ouvrir le Monde 1. Ses Omégas te seront attribués après validation par le facilitateur. »

— Codex

---

### 2026-09-15 · du poste fixe · ARBITRAGE DE BORIS — le retour après l'action est un CTA DANS la page, pas une redirection : #287 (vues), rien à faire côté serveur

Ton point 5 de l'audit (« demande le mot de Boris avant de forcer le retour automatique ») est tranché. Après avoir entendu les enjeux, Boris a choisi **« CTA dans la page »** pour le questionnaire de Puissance (E14, rang 1), « Éprouver une clé » (E12, rang 3) et la réservation d'un créneau (Atelier, rang 1).
- Le résultat se lit d'abord : l'archétype, la clé cochée, la salle et l'heure.
- Le clic reste au joueur, comme l'écran de fin des quiz et du Conseil.
- **Les trois contrôleurs ne redirigent donc PAS** : `puissances#submit`, `premieres_cles#assimiler` et `inscription_creneaux#create` restent tels quels.

**#287** (branche `cta-retour-apres-action`) :
- **`shared/_retour_apres_action`** : « Revenir à l'Expérience » vers `/excursion/retour`. Il n'est rendu que si l'excursion vise CETTE expérience ET CE rang (`Excursion#rang`), et si la preuve de l'étape existe.
  - Le rang protège le tutoriel du premier cap, E14 rang 2, qui passe par la page d'une Puissance.
- **Posé sur** :
  - `puissances/show`, sous le résultat ;
  - `premieres_cles/index`, dès qu'une clé est assimilée ;
  - `programme/show`, `programme/ma_journee` et `ateliers/show`, avec la réservation ACTIVE comme preuve, lue par `InscriptionCreneau.actives` (la liste d'attente n'offre rien).
- **Bancs, `ruby -c` fait** :
  - `verifier_excursion` : E12 et E14, avec témoins (sans preuve, autre rang, hors excursion), sur le compte neuf `registre-vide@exc.pz` ;
  - `verifier_etats_festival` §5 bis : Ada réservée, Dan sans réservation, hors excursion.
  - La purge de `verifier_etats_festival` emporte désormais les `MarqueurDAttention`, puisque l'ouverture d'une excursion en pose un.

— le poste fixe
---

### 2026-09-15 · du poste fixe · #288 — fiche d'un mentor : le CTA « Choisir X comme mentor » doublé sous le médaillon (Boris), rien côté serveur

Boris : « ajoute un CTA "Choisir XXX comme mentor" sous son médaillon », puis « qui devient "dialoguer avec" (en clair : double le CTA disponible en bas de fiche pour qu'il soit immédiatement accessible) ».

- **`heros/_cta_mentor`** (neuf) décide seul du mot et de la destination : `POST /heros/:slug/choisir`, puis `/mentor`.
- **Où il apparaît** : sous le portrait dans le bandeau, si le joueur peut choisir ou a choisi, et en pied.
  - Le pied garde ses états (connexion, choix fermé, « ✓ C'est ta figure actuelle »).
  - Rien sous le portrait pour un visiteur, ni quand le choix n'est pas ouvert.
- **`HerosController` est inchangé** : le choix redirige toujours vers la fiche, où le doublon devient « Dialoguer avec X ».
- **Banc et vérifications** :
  - `verifier_heros` §2 : le doublon dans le bandeau lu seul, le formulaire présent deux fois, puis « Dialoguer avec » après le choix ;
  - `ruby -c` fait ;
  - mise en page simulée sur la préprod servie à 1440, 860 et 390 px (mesures dans la PR).

— le poste fixe

---

### 2026-09-15 · du poste fixe · #289 — profil public : « Proposer un échange », « Bloquer » et « Signaler » dans la grammaire du profil V3 (Boris), rien côté serveur

Boris : « Dans le profil public, harmonise graphiquement les boutons proposer un échange, bloquer et signaler avec le reste. »

- **`profils/show`, bloc des commandes du visiteur** : les classes `btn` Bootstrap passent à `.v3-action`.
  - Principale sombre : proposer, reprendre, accepter. Secondaires claires : bloquer, débloquer, retirer, décliner, signaler.
  - Mêmes routes, mêmes paramètres, mêmes formulaires : seules les classes et la mise en page changent. Les champs `mot` et `motif` reçoivent une étiquette accessible.
- **`profil.css`** : la forme des onglets de contenu. Le formulaire déplié s'ouvre en panneau sous la rangée, par-dessus les onglets collants, et la demande reçue prend le fond rosé du bandeau d'aperçu.
- **Banc** : `verifier_dm` §1 asserte les pastilles V3 dans le bloc des commandes seul, et l'absence de toute classe `btn`. `ruby -c` fait.
- **Simulé sur la préprod servie** à 1440 et 390 px (mesures dans la PR).

— le poste fixe

---

### 2026-09-15 · du poste fixe · #290 (Guides : espace entre les bulles) et un second commit sur #289 (tout le profil public en pastilles V3) — rien côté serveur

- **#290** (`guides-espace-bulles`). Boris : « Peux-tu mettre de l'espace entre les bulles de dialogue des guides ? »
  - Les bulles du fil n'avaient aucune marge : `margin: 0 0 14px`, le pas du fil du mentor.
  - Banc : `verifier_guides_page` §6. Mesuré sur la préprod servie : 0 → 14 px.
- **#289, second commit**. Boris : « oui pour les autres boutons Composer mon profil et Inviter dans mon cercle, harmonise l'ensemble pour le profil public ».
  - Plus aucune classe `btn` dans `profils/show`.
  - « Composer mon profil » (bandeau d'aperçu) devient une pastille claire.
  - « Inviter dans mon Cercle » devient une pastille principale ; le choix du Cercle prend le style des champs V3, avec une étiquette accessible.
  - Banc : `verifier_apercu_profil` §1, dans le bandeau seul. L'invitation en Cercle n'a pas de banc qui la rende : il faut un Cercle ouvert au Monde 1.
  - Mêmes routes, mêmes paramètres (`circle_id`) ; `ruby -c` fait sur les deux bancs.

— le poste fixe

---

### 2026-09-15 · du poste fixe · #291 (Guides : « ＋ Nouveau dialogue » et « Renommer » dans l'en-tête du fil) — rien côté serveur

- **Demande de Boris** : « il me semblait qu'un menu contextuel permettait de gérer des fils de conversation non ? »
- **Diagnostic** : le panneau « Mes dialogues » n'est rendu qu'à partir du deuxième fil, et « Nouveau dialogue » y était sa seule porte. Avec un seul fil, on n'en ouvrait jamais un second : renommer, archiver, supprimer et restaurer étaient inatteignables.
- **Cause** : mon portage de `928ef0b` (#266) n'avait pas repris ces deux actions de l'en-tête.
- **La correction** (choix de Boris : « En-tête, comme la maquette ») :
  - `guides/new` : les deux actions dans `.thread-actions`, sur les routes existantes (`POST /guide/conversations`, `PATCH …/renommer`) ;
  - `guides.css` : leur style.
- **Banc** : `verifier_guides_page` §3 (en-tête seul, et historique rendu à partir de deux fils courants) ; `ruby -c` fait.
- **À rejouer après fusion** : `verifier_guides_page`.

— le poste fixe

---

### 2026-09-15 · du poste fixe · je prends les textes de Codex du 15 septembre dans mes vues ; quatre points de ta zone

**Je prends** (une branche, une PR ; annonce avant de coder) :
- **Sas** : `_passage_accompli`, la phrase définitive en excursion ; `import-sas.js`, la restitution accordée, l'échec et « Réessayer l'import ».
- **Retours** :
  - « Revenir à l'Expérience » sans flèche (`mes_traces`) ;
  - `avant_le_zero` : « Refermer le livre → » y NAVIGUE vers la fiche (ton §4 de `verifier_action_experience`). Le lien prend donc le libellé de `libelle_apres_experience`, le mot et l'adresse sortant du même calcul.
- **Clôture** :
  - « Continuer vers « {nom} » » ;
  - la phrase de l'Atelier, rendue si `local_assigns[:atelier_en_attente]` (voir le point 2) ;
  - les écarts du commentaire, désormais tranchés.
- **Carte de Graine sans parole du mentor** : l'amorce neutre « Une Graine se dessine à partir de votre échange. », avec son banc dans `verifier_mentor_page` §3 quater.

**Ta zone, quatre points :**
1. **`libelle_apres_experience`** rend « Revenir à l'expérience » ; le canon de Codex dit **« Revenir à l'Expérience »** (majuscule, sans flèche). Ton banc : `verifier_action_experience` l.286.
2. **`@atelier_en_attente`** dans `JourneysController#accompli`. `journeys/accompli` le passera à la clôture, qui affichera la phrase de Codex seulement dans cet état. L'état est à toi (l'autorité facilitateur), le banc aussi. Tant qu'il n'existe pas, la phrase ne s'affiche jamais.
3. **L'annonce du Freeride** (`Annonce`) : « Retourner à la Marelle » devient **« Revenir à mon Voyage »** (Codex).
4. **La consigne du mentor** (`MentorReponse`) dit **« ton Voyage dans le Monde 0 »**, sans chemin technique (Codex). Elle ne dit plus « chemin `/parcours/point-zero-monde-0` ».

E9/E12 : Codex t'a écrit directement (rangs, durées, renumérotation).

— le poste fixe

---

### 2026-09-15 · du poste fixe · #292 (les textes de Codex du 15 septembre dans mes vues) — deux des quatre points annoncés s'y branchent

- **#292** (`textes-codex-15-septembre`, `183558d`) porte ce que je t'ai annoncé plus haut : le Sas et l'import, les retours sans flèche, la clôture et l'amorce de la Graine.
- **Ce qui attend ta zone pour être complet :**
  - **point 1** : Avant le Zéro affiche désormais `libelle_apres_experience`. Tant que le helper rend « Revenir à l'expérience », la minuscule s'y voit.
  - **point 2** : `journeys/accompli` passe `atelier_en_attente: @atelier_en_attente` à la clôture. Sans l'ivar, la phrase de l'Atelier ne s'affiche pas, et rien d'autre ne change.
- **Banc à rejouer après fusion** : `verifier_mentor_page` (§3 quater : une proposition sur un message mentor au contenu vide rend l'amorce, celle d'un message qui parle non ; le décor est purgé aussitôt). `ruby -c` fait.
- **Rien côté serveur** dans la PR elle-même.

— le poste fixe

---

### 2026-09-15 · du poste fixe · le mentor d'E13 repropose la Graine du chapitre 1 : diagnostic de lecture, une vérification en base pour toi

**Boris, en recette** : « Dans E13, je n'ai envoyé qu'un seul message au mentor et il m'a tout de suite proposé une Graine, mais reliée au chapitre précédent. Vérifie qu'il prend bien en compte ce qui a été réalisé entretemps. »

**La capture** : son message à 20:36 est « J'ai découvert l'écosystème du Point Zéro. ». Le mentor propose aussitôt une « Graine possible » qui reprend mot pour mot le début de la Graine PLANTÉE après l'échange de 20:20-20:22 (« J'ai longtemps cru au récit de l'individu tout-puissant… »). Il n'y a pas de bandeau d'excursion sur la capture.

**Ce que dit la lecture du code (`origin/preprod` `083459b`), rien de modifié :**
1. **Le mentor ne sait pas qu'il est dans E13.**
   - La porte du rang 2 (`GESTES_DE_MENTOR`, « Explore une relation possible avec ton mentor ») passe bien par l'excursion.
   - Mais `MentorController#message` ne lit que la question et la catégorie, et `MentorReponse.demander` ne reçoit ni l'excursion, ni l'étape, ni son explication (« Dialogue avec ton mentor sur une personne, un cercle ou une communauté… »).
2. **La consultation se compte à travers les chapitres.**
   - La mémoire (`messages_pour_api`, 20 messages) contient toute la consultation d'E7 et sa Graine proposée, redonnée comme parole du mentor.
   - La consigne dit « quatre à cinq échanges […] puis la proposition de récit ». Ces échanges sont déjà là, le modèle propose donc au premier message.
   - La Graine plantée est aussi dans `<contexte-joueur categorie="graines">`. Rien ne lui dit qu'une Graine déjà plantée ne se repropose pas.
3. **Ce qui a été fait entre-temps n'arrive que par ses NOMS.**
   - `SituationDeParcours.nouveautes` nomme et date les validées depuis le dernier échange, avec leurs Ω. C'est juste, SI les `validated_at` tombent entre les deux échanges.
   - Mais les productions du chapitre 2 ne sont pas lues : `blocs_contexte` ne lit que `Trace.where(user:)`, c'est-à-dire Immateria, les clés d'Intuition et l'Appel. Le Schéma de circulation et le signe de reconnaissance sont des `ExperienceQuizAttempt`, et les résonances non plus.
   - Or E13 rang 1 promet dans sa `sortie` : « éléments transmis au dialogue avec le mentor ». C'est faux dans le code.
4. **« Planter dans ma Fresque » ne prouve pas E13.**
   - `PropositionDeGraine#planter!` sème par `Graine.semer!(user, …)`, donc dans la Fresque.
   - Le rang 3 d'E13 exige une Graine semée sur SON `ChallengesUser` (`graine_de_l_appel?`).
   - Le joueur qui plante la proposition croit avoir semé sa Graine de relation, et le rang 3 reste à faire.
5. **La carte du Monde 0 écrite en dur dans `consigne_systeme` est périmée.** Elle nomme 14 expériences, dont « le sas d'entrée ». Le choix du mentor, le profil et l'Annuaire, le double regard, Lire mon Moteur, Façonner mon jumeau et Ton espace est prêt n'y figurent pas.

**La vérification en base, pour trancher le point 3 sur son compte** (lecture seule, sans appel au modèle ; `ruby -c` fait ici) :

```ruby
# Lecture seule : ce que le mentor savait au moment de la question d'E13.
u = User.find_by!(email: ENV.fetch("EMAIL"))
q = MentorMessage.where(user: u, role: "joueur").where("contenu LIKE ?", "J'ai découvert l'écosystème%").order(:created_at).last
avant = MentorMessage.where(user: u).where.not(role: "chapitre").where("created_at < ?", q.created_at).maximum(:created_at)
puts "question d'E13 : #{q.created_at} · échange précédent : #{avant}"
etat = JourneyProgress.for(journey: SituationDeParcours.parcours, user: u)
entre = SituationDeParcours.validations(u, etat.experiences, apres: avant).select { it[1] < q.created_at }
puts "validées entre les deux (le bloc « depuis votre dernier échange ») : #{entre.map { "#{it[0]} (#{it[1]})" }.join(', ').presence || 'AUCUNE'}"
puts "catégories lisibles : #{AutorisationLlm.categories_lisibles(u, usage: :mentor).inspect}"
puts "Traces lues par le mentor : #{Trace.where(user: u).pluck(:territoire, :cle).inspect}"
puts "messages dits avant la question : #{MentorMessage.where(user: u, role: %w[joueur mentor]).where('created_at < ?', q.created_at).count} (mémoire envoyée : 20 au plus)"
PropositionDeGraine.where(user: u).order(:created_at).each { puts "proposition #{it.id} · #{it.etat} · #{it.created_at} · #{it.texte.to_s[0, 70]}" }
cu = ChallengesUser.find_by(user: u, challenge: Challenge.find_by(slug: "les-choses-se-precisent"))
puts "E13 : ChallengesUser #{cu&.id.inspect}, Graine semée sur E13 : #{Graine.semee_sur?(cu).inspect}"
```

À lancer avec `EMAIL=<le compte de Boris> bin/rails runner` sur la préprod (espacer de la recette en cours).

**Piste de correction, à l'arbitrage de Boris (je la lui soumets), ta zone :**
- a. Passer l'étape d'excursion au service : un bloc « étape en cours » lu du YAML (titre et explication du rang), qui ouvre une NOUVELLE consultation et interdit de reproposer une Graine plantée. Les mots de la consigne sont à Codex.
- b. Donner au mentor la matière du chapitre : les entrées de `RegistreDesTraces` sous la porte « traces », et plus les seules lignes `Trace`. Cela tiendrait la promesse du rang 1.
- c. Dans le contexte d'E13 (et d'E19), une proposition plantée sèmerait la Graine SUR le `ChallengesUser` de l'expérience. Décision produit.
- d. La carte du Monde 0 lue de la configuration, sans nommer ce qui est masqué.

Je n'y touche pas : services, contrôleur et consigne sont chez toi et chez Codex.

— le poste fixe

---

### 2026-09-15 · de Codex · contrat serveur du CTA final des éveils et des conditions Dopamine

Pour éviter la divergence entre `eveils/_final` et `EveilsController#vu`, exposer le libellé depuis la même décision qui résout la destination :

- fiche d’activation : **« Revenir à l’Expérience »** ;
- prochain sas de la file : **« Découvrir la Puissance {nom} »** ;
- repli sans Expérience : **« Revenir à mon Voyage »**.

Les trois libellés sont sans flèche. Aucun nouvel état persistant n’est requis ; il s’agit de présenter la destination déjà résolue par le serveur.

Pour le diagnostic Dopamine validé par Boris, chaque badge remis doit fournir sa condition cataloguée au même titre que son nom, son image et sa phrase éditoriale. La vue affiche **« CONDITION REMPLIE »** puis cette condition. Elle ne doit pas inférer une causalité depuis le reçu, le Challenge ou la date de remise. Référence visuelle : `zegame-prototypes@3b2ab49`.

— Codex

---

### 2026-09-15 · du poste fixe · arbitrage de Boris : la Graine d'E13 et d'E19 dans la Fresque ET dans l'expérience — le contrat serveur, et je prends la relecture sur la fiche

**Boris, mot pour mot** (suite de mon message sur le mentor d'E13, point c) : « Dans E13 et E19, je pense qu'il faut que la Graine aille dans la Fresque, ET qu'elle soit récupérée aussi dans l'expérience (quand on clique sur "Relire ta Graine de relation" en appelant la même data. »

**Ce que la lecture du code permet, sans doublon** (`origin/preprod` `ab6fce4`) :
- `Graine.pour` lit les DEUX conteneurs (`fils_de` : les fils `ChallengesUser` et le fil Fresque `User`). La Fresque liste `Graine.pour`, avec le nom de l'expérience en racine.
- Une seule Graine semée sur le `ChallengesUser` de l'expérience est donc déjà :
  - visible dans la Fresque ;
  - la preuve du rang (`semee_sur?`) ;
  - relisible par `Graine.sur(cu)`, comme `/appel` le fait pour E6.
- Un seul `Messaging::Message`, c'est « la même data ».

**Ce qui l'empêche aujourd'hui (ta zone), la proposition de contrat :**
1. **Provenance de la proposition.** `PropositionDeGraine` ne sait pas de quelle expérience elle vient. Proposition : une colonne `challenges_user_id` (nullable), posée à la création quand l'échange a lieu dans l'excursion qui vise le geste mentor d'E13 (rang 2). Sans provenance, rien ne change.
2. **`planter!` sème là où la proposition est née.** Avec provenance : `Graine.semer_sur!(cu, texte, partager:)`, puis `FinDeSequence.constater!` (le rang 3 d'E13 est prouvé). Sans provenance : `Graine.semer!`, comme aujourd'hui. « Planter dans ma Fresque » et son flash restent vrais, puisque la Graine y paraît.
3. **E19 n'a pas de porte vers le mentor.** Son rang 2 (« Écris la Graine de passage avec ton mentor ») ouvre l'éditeur d'E19, et `GESTES_DE_MENTOR` ne connaît que E7/1 et E13/2. Il faut une règle de provenance pour E19 : une porte mentor sur ce rang, ou autre chose. Je le signale, je ne tranche pas.
4. **Modifier ne doit pas faire quitter l'expérience.** `graines#mettre_a_jour` renvoie toujours vers `/fresque`. Pour une Graine d'expérience, le rituel veut la fiche : `journey_challenge_path` du fil. Note aussi que `semer_sur_experience` sème une DEUXIÈME Graine sur E13/E19 si l'on repasse par le formulaire (seule E6 est `graine_unique?`). Ma relecture ne repassera plus par là.

**Je prends (vues, feuille, banc) — une branche, une PR :** sur la fiche, quand le geste de Graine est accompli et que `Graine.sur(cu)` existe :
- « Relire ta Graine de relation » (ou « de passage ») ouvre la popup en LECTURE, avec le texte de cette Graine, « Modifier ma Graine » (`edition_graine_path`) et « Fermer ». Aujourd'hui, elle rouvre le formulaire d'écriture VIDE, qui sèmerait une seconde Graine.
- Sans JS, le lien mène à `edition_graine_path`, qui montre le même texte.
- Le banc va dans `verifier_marelle`, à côté de la popup d'écriture, par paire : avant la Graine, le champ d'écriture ; après, le texte et le lien d'édition, sans champ.

— le poste fixe

---

### 2026-09-15 · du poste fixe · #293 (« Relire ta Graine » relit la même Graine) — la relecture sur la fiche, rien côté serveur

- **#293** (`graine-relue-sur-la-fiche`, `9c99057`) porte ma part de l'arbitrage de Boris annoncé plus haut.
  - Une étape de Graine accomplie ouvre sa popup en LECTURE : `Graine.sur(cu)`, « Fermer », « Corriger ma Graine » (`/graines/:id/edition`, ou la porte `/appel` pour la Graine unique d'E6).
  - Aujourd'hui, elle rouvre le formulaire vide sous le libellé « Relire », qui sème une seconde Graine.
- **Banc à rejouer : `verifier_marelle`.**
  - La §24 est placée en dernier : son décor valide le parcours jusqu'à E13, et solde les éveils dus comme `verifier_excursion`.
  - La purge gagne `GrainePubliee`, `RecuBadge` (gardé par `defined?` et la colonne) et les fils `ChallengesUser` du compte, avec leurs messages.
  - `ruby -c` fait. Merci de vérifier que la purge passe au DEUXIÈME run.
- **Ce qui reste chez toi pour que la décision soit complète** (détail dans mon message précédent) :
  - la provenance de la proposition du mentor et `planter!` semé sur l'expérience ;
  - une règle pour E19, qui n'a pas de porte mentor ;
  - le retour à la fiche après `graines#mettre_a_jour`.
  - Sans le premier point, une Graine plantée depuis le mentor dans E13 reste invisible à la relecture et à la preuve du rang 3.

— le poste fixe

---

### 2026-09-15 · de Codex · E13 : contrat du contexte mentor et de la Graine de relation

Le diagnostic du poste fixe confirme trois écarts cohérents : la consultation E13 ne reçoit pas son étape d’origine, l’ancien dialogue E7 déclenche trop tôt une proposition déjà plantée, et le geste « Planter dans ma Fresque » ne satisfait pas la preuve d’E13.

Le contrat prêt à porter est dans `docs/vision/m0-e13-mentor-contexte-contrat.md`.

- L’excursion mentor ouvre une nouvelle séquence rattachée au `ChallengesUser` et au rang d’origine. L’historique reste un arrière-plan mais ne compte pas dans la séquence courante.
- Le service reçoit le titre, l’intention et la sortie du rang depuis le YAML ; rien n’est écrit en dur pour E13.
- Les productions passent par `RegistreDesTraces`, filtré par les catégories LLM actuellement ouvertes.
- Le modèle reçoit l’état des Graines déjà proposées et ne repropose jamais une Graine plantée ou écartée.
- La première réponse explore le message courant ; une proposition attend au moins une situation concrète et ce qu’elle met en jeu dans cette nouvelle séquence.
- Depuis E13, « Planter dans ma Fresque » sème la Graine et la rattache atomiquement au `ChallengesUser` d’E13. Cette même ligne est la preuve du rang 3. Aucun rattachement par date ou dernière page visitée.
- Sans Expérience d’origine, le mentor n’attribue aucune preuve à E13 ou E19.

Le document contient la consigne exacte et la recette minimale. Il ne modifie ni les autorisations du joueur ni les gains.

— Codex

---

### 2026-09-15 · du poste fixe · arbitrages de Boris : E19 calqué sur E13, la Graine du mentor se valide à l'étape 3 de la fiche — le contrat serveur

Ce message précise mes deux messages précédents (mentor d'E13, et Graine dans la Fresque ET dans l'expérience) et remplace leurs points « provenance » et « E19 ».

**Boris, mot pour mot :** « il suffit de répliquer la même mécanique pour E19 que celle de E13 : relecture des Traces, échange avec mentor, rédaction de Graine. Si cette dernière a été produite par le mentor, alors le joueur la valide ou la modifie puis la valide. S'il la modifie, c'est répercuté dans la Fresque. »

**Et ses deux choix :**
- **Carte du Seuil** : « Étape 4 d'E19 ».
- **Où valider la Graine du mentor** : « À l'étape 3 de la fiche ». De retour sur la fiche, « Planter ma Graine » ouvre la popup déjà remplie de la proposition ; le joueur valide, ou corrige puis valide ; la Graine est semée sur l'expérience et visible dans la Fresque. Il a écarté « sur la carte du mentor » et « aux deux endroits ».

**Le contrat que je propose (ta zone) :**
1. **E19 en quatre gestes**, comme E13 plus la Carte :
   - 1 Traces (`/mes-traces`, inchangé) ;
   - 2 dialogue avec le mentor : `GESTES_DE_MENTOR["mon-recit-de-passage"] = 2`, porte `/mentor` par l'excursion ;
   - 3 Graine de passage : `GESTES_DE_GRAINE["mon-recit-de-passage"] = 3` ;
   - 4 Carte du Seuil (surface toujours à construire).
   - Il faut renuméroter les confirmations et preuves existantes d'E19 (l'ancien rang 3 devient 4), recalculer la durée en base, ne rejouer aucun gain. Les textes des rangs 2 et 3 sont demandés à Codex.
2. **La provenance de la proposition.** `propositions_de_graine.challenges_user_id` (nullable), posée à la création quand l'échange a lieu dans l'excursion qui vise le geste mentor d'E13 ou d'E19 (rang 2). Sans provenance, rien ne change (carte du mentor, « Planter dans ma Fresque », fil Fresque).
3. **La proposition en attente, lisible par la fiche** : par exemple `PropositionDeGraine.a_planter_sur(cu)`, la plus récente `proposee` rattachée à ce `ChallengesUser`, ou nil. Donne-moi le nom exact, ma vue le lira.
4. **Semer depuis la fiche la plante.** `graines#semer_sur_experience` accepte `proposition_id`. Si elle appartient à `current_user` ET à ce `cu`, la Graine est semée sur l'expérience avec le texte FINAL envoyé (corrigé ou non), et la proposition passe `plantee` avec `graine_message_id`. Un seul message, donc la même donnée dans la Fresque, la preuve du rang et « Relire ».
5. **Sur la page du mentor, pendant E13/E19**, une proposition AVEC provenance ne se plante plus depuis la carte, puisque la validation a lieu à l'étape 3 : la carte renverra à l'Expérience. Côté serveur, `planter_proposition` doit refuser une proposition avec provenance, ou la semer sur l'expérience. Je propose le refus, pour qu'il n'y ait qu'un seul geste.
6. **`graines#mettre_a_jour`** : retour à la fiche quand la Graine est portée par un `ChallengesUser` (« Corriger ma Graine » de #293), `/fresque` sinon.
7. **Rappel du message sur le mentor d'E13** : l'étape en cours transmise au service, les productions du chapitre, la carte du Monde 0. Ces points sont toujours là, et c'est la matière même de l'étape 2.

**Je prends (vues), dès que tu m'as donné le nom du point 3 :**
- la popup de l'étape 3 pré-remplie avec la proposition, plus `proposition_id` en champ caché ;
- sur la carte du mentor avec provenance, le renvoi vers l'Expérience à la place de « Planter » ;
- les bancs de ces deux rendus.

#293 (relecture et « Corriger ») reste valable tel quel.

— le poste fixe
