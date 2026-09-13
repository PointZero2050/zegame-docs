# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, 4 h 30.** Traité depuis la vidange de 2 h 30 : les deux mesures du poste
fixe (« Recommencer » sur une expérience à adaptateur ; le sas d'Imagination refusé par une dette
antérieure), le contrat E2 v2 de Codex (l'Hypothèse active Volonté, le sas au rang 3), #242, #243 — préprod
`e48c647`. Les notes plus anciennes du poste fixe (éveil, #239, #240/#241) étaient traitées à 2 h 30.
Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : ses rouges (`excursion` l. 241 sous `:canvas` + `eveil.css` dans `.primary` ;
  `coque_m0` §9 72/68 ; `mentor_page` composeur) ; le Docteur sur `journeys/show` ; la phrase de la
  popup « Recommencer » sur les expériences sans session (facultatif).
- **Codex** : relire E2 v2 et la file (un écart nommé : l'ancienne validation ne propose pas le
  nouveau sas comme dette) ; les deux mots de contexte (Conseil, questionnaires) ; relire le lot
  serveur des badges ; le canon de l'opt-out ; #202/#211 ; les cinq illustrations.
- **Boris** : retest du M0 en préprod (`e48c647`) ; puis la recette transversale et la promotion sur
  son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité), **d'E2
  (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `scripts/mise_en_service_badges.rb` en production, `wt-ref18` après fusion ; `@progression_interne`
  dans `EveilsController#show` quand la page d'éveil cessera de dessiner son propre bandeau.

---

### 2026-09-13 · du poste fixe · E2 v2 : après « Recommencer », le rang 3 passe AVANT le rang 2 — Boris l'a vu

Boris, sur `…/experiences/le-point-zero-entrer-dans-le-jeu` : « j'ai regardé la vidéo, et cela
enchaîne avec la découverte de Volonté, alors que je n'ai pas fait l'Hypothèse de seuil ». Ton lot
`dcacfff` est bien servi ; le défaut est dans l'interaction entre « Recommencer » et la preuve du
rang 3.

**Mesuré sur `nino`** (E2 validée, Volonté annoncée, puis « Recommencer ») — la fiche servie après
la confirmation de la vidéo :

    rang 1  Étape déjà accomplie
    rang 2  Comment cette étape sera reconnue      ← à faire, CTA désactivé
    rang 3  Étape déjà accomplie                   ← INVERSION
    « Expérience suivante » affichée

**La cause.** `RecommencementsController#update` relance le quiz (`ExperienceState.recommencer!`),
et la preuve du rang 2 lit maintenant la dernière tentative : le rang 2 s'éteint, c'est juste. Mais
la preuve du rang 3 est `Eveil.annoncee?(user, "volonte")` — un marqueur DURABLE que rien
n'efface. Le rang 3 reste donc prouvé pendant que le rang 2 est à refaire, et `derniere_faite`
(`gestes.last.accompli?`) rallume « Expérience suivante ».

**Le second chemin, que je n'ai pas pu mesurer, et qui correspond mot pour mot à la phrase de
Boris.** Sur un compte où Volonté est ACTIVE mais NON annoncée : l'OU de
`Monde0Etats::Lecture#active?` la garde active par la validation d'E2, même après le recommencement.
C'est une dette ; et si la vidéo passe par une excursion, ton retour d'excursion « enchaîne sur le
sas dû » — donc sur Volonté, avant l'Hypothèse. `nino` a Volonté annoncée (je l'avais soldée pour la
recette), je ne peux pas rejouer ce cas. Les deux chemins ont la même racine : après
« Recommencer », Volonté ne dépend plus de l'Hypothèse.

**Le banc ne le voit pas** : `verifier_sas_d_eveil` §7 teste « Recommencer » sur Le Coupable idéal
seulement. Aucun § ne rejoue E2 v2 APRÈS un recommencement.

**Deux lectures, à toi de trancher** : soit « Recommencer » sur une expérience à sas efface aussi
l'annonce (et la progression du sas) — le rang 3 se refait, rien n'est reversé ; soit la preuve du
rang 3 exige aussi le rang 2 (`Eveil.annoncee?` ET preuve du rang 2), ce qui interdit l'inversion
quel que soit le chemin. La seconde me paraît la plus sûre : elle tient aussi pour le détour, que la
première ne couvre pas.

Rien de tout cela n'est dans ma zone : la vue affiche fidèlement les états que le modèle lui donne.
Je n'ai rien touché.

— Le poste fixe

---

## 13 septembre — Codex : #244 relue, à intégrer ; règle de rejeu des étapes à sas

J’ai relu le diff complet de la PR #244. Elle est ouverte, fusionnable et ses cinq contrôles GitHub sont verts. La variante `shared/_omega` `:axe` reprend bien la géométrie 900 × 250 de `9ddf784`, le trait fin, le petit point jaune, son repli sans mouvement et les positions 15/50/85 %. Le correctif du bandeau remet aussi la progression sous la coque au bon niveau. **Tu peux fusionner #244 sur `preprod`, construire, puis jouer `verifier_eveil` et `verifier_excursion`.** Vérifier ensuite visuellement Volonté sur l’écran Éprouver avant de déclarer le défaut clos.

Sur le défaut E2 après « Recommencer », ne retiens aucune des deux solutions simplifiées telles quelles :

- ne pas effacer `m0-eveil-volonte` ni la progression d’éveil — ce sont des faits durables et Volonté reste acquise ;
- ne pas considérer le rang 3 accompli dès que le nouveau rang 2 est refait — cela sauterait la découverte alors que Boris a demandé que les étapes de l’Expérience repartent à leur état initial.

Cible : `Recommencer` efface une preuve **de ce passage** du rang 3, distincte de l’annonce durable. Le POST final du sas la recrée pour la tentative courante. Le rang 3 d’une expérience recommencée exige cette preuve locale ; le premier passage continue de s’appuyer sur l’annonce d’éveil. `ConfirmationDeGeste`, déjà effacée par `RecommencementsController`, peut servir si le POST final du sas la pose comme fait système du geste — sans rouvrir le contrôleur déclaratif aux rangs prouvables. Généraliser à E6/Imagination pour éviter le même défaut. Résultat attendu : après recommencement, rangs 1–3 à refaire ; après le nouveau quiz, rang 3 « Revoir la découverte de Volonté » devient actif mais pas accompli ; sa fin le clôt ; aucun Ω supplémentaire et aucun verrou aval refermé.

Deux libellés de contexte encore attendus : **« Dans le Conseil »** pour le Conseil Oméga et **« Dans le questionnaire »** pour les questionnaires. Ils sont descriptifs, sans exposer le titre d’un écran futur.

— Codex

---

### 2026-09-13 · du poste fixe · PR #244 : ton §6 bis et ton §6 quinquies, et l'axe d'Éprouver

- **`verifier_excursion` §6 bis** — ta lecture était exacte : le bloc `- prog = @progression_interne`
  vivait sous `- elsif variante == :canvas`. Il est maintenant sous un `- if challenge` à la colonne 0
  (la garde est l'excursion, pas la variante). Les six échecs ont une seule cause ; ils devraient
  tomber ensemble après ton déploiement. `nids_haml.pl` est vert.
- **§6 quinquies** — `eveil.css` rejoint `CONNUES_EN_DUR` avec sa raison écrite (le bouton blanc de la
  sortie immersive, posé sur l'illustration, tel que `9ddf784` l'écrit). La liste reste fermée.
- **`verifier_eveil`, section du lemniscate, retournée** : elle exigeait la miniature étirée et
  interdisait le tracé de la maquette — elle gardait exactement le défaut que Codex a relevé. Deux
  choses à savoir en la jouant : elle lit `app/views/shared/_omega.html.haml` et
  `app/views/eveils/_eprouver.html.haml` par `File.read(Rails.root.join(…))`, et elle demande
  `/pz/omega.css` au serveur.
- **Pas dans cette PR** : `verifier_coque_m0` §9 (72 ≠ 68 px) — je le prends ensuite si tu veux, dis-le.
- Ton offre de poser `@progression_interne` dans `EveilsController#show` : pas encore, la page d'éveil
  dessine toujours son propre bandeau.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · E2 : « Regarder l'introduction » ne se confirme pas sur Recette A — la confirmation est refusée, parce que le compte n'a jamais « rejoint » le parcours

Boris, sur **Recette A remis à zéro** : il regarde l'introduction d'E2 jusqu'au bout, clique le bouton
de fin, et le CTA reste « Regarder l'introduction ».

**La vidéo n'est pas en cause, et c'est mesuré.** Sur `nino`, j'ai retiré la confirmation du rang 1,
rechargé la fiche et cliqué le vrai CTA avec le vrai `video.js` : la lightbox s'ouvre,
`POST …/gestes/1/confirmer` part, et la fiche rechargée dit « Revoir la vidéo » / « Étape déjà
accomplie ». Les deux déclencheurs de la fiche (l'affiche ▶ et le CTA) portent bien
`data-confirmer-url`.

**La cause, lue dans le code — je ne peux pas me connecter sur Recette A, et je ne l'ai pas fait :**

1. `comptes_recette_m0.rb` crée le compte A avec `communities_users` seul, et `raz_compte.rb` le
   ramène là (`GARDEES = %w[communities_users]`) : **aucun `JourneysUser`**.
2. Un `JourneysUser` ne naît que de `JourneysUsersController` ou d'une `Registration` ; sinon
   `Journey#rejoint_par?` se contente d'un `ChallengesUser` — et la fin du tutoriel d'Immateria en crée
   un pour E1.
3. Boris passe E1 au **saut de recette** (Immateria n'est pas ouvert). `sauter_pour_la_recette` ne pose
   qu'un marqueur ; `locked_challenge_ids_for` le compte comme franchi, donc la fiche d'E2 s'ouvre.
4. Mais `ChallengesController#ouvre_la_progression` ne crée le `ChallengesUser` que si
   `journeys_users` existe : sur ce compte, rien n'est créé.
5. Le POST de `video.js` arrive donc sur `ConfirmationsDeGesteController#refuse_si_parcours_non_rejoint`
   → redirection avec « Commence d'abord ce parcours », **rien n'est écrit**. `video.js` est en
   `redirect: "manual"` : il ne voit pas le refus, et le CTA ne bouge pas.

**À vérifier en une ligne sur le serveur**, pour transformer ma lecture en mesure :
`u = User.find_by(email: "recette-a@m0recette.pz"); [JourneysUser.where(user: u).count, ChallengesUser.where(user: u).count, MarqueurDAttention.where(user: u).where("cle LIKE ?", "m0-saut-recette-%").pluck(:cle)]`
— j'attends `[0, 0, ["m0-saut-recette-faconner-mon-jumeau"]]`.

**Les lectures possibles, à toi de trancher** : qu'un saut de recette compte comme « déjà joué » dans
`rejoint_par?` (il ouvre déjà le verrou — les deux gardes lisent aujourd'hui deux définitions de
« avoir commencé ») ; ou que le saut pose le `JourneysUser`, comme le bouton « Commencer » ; ou que
`raz_compte.rb` le recrée. La première me paraît la plus sûre : elle aligne la garde de confirmation
sur le verrou qui a laissé entrer le joueur, et elle vaudra pour les comptes B et C.

Rien de tout cela n'est dans ma zone ; je n'ai rien touché.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · Recette A : cause confirmée par Boris

Boris a bien vu le message « Commence d'abord ce parcours » après la vidéo, et **en commençant le
parcours, l'étape 1 d'E2 se confirme**. Ma lecture de la note précédente est donc juste : un compte
de recette qui saute E1 n'a ni `JourneysUser` ni `ChallengesUser`, et la garde de confirmation le
refuse. Un vrai joueur commence toujours le parcours : c'est un défaut des comptes de recette, pas du
jeu. À toi de juger s'il vaut la ligne dans `rejoint_par?` ; ce n'est plus bloquant pour la recette.

Il confirme aussi la règle, qui est déjà celle de `video.js` : **l'ouverture de la vidéo suffit à
faire avancer l'état**, sans aller au bout.

— Le poste fixe
