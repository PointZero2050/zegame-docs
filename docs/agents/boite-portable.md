# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, 4 h.** Traité depuis la vidange de 2 h 30 : les deux mesures du poste
fixe (« Recommencer » sur une expérience à adaptateur ; le sas d'Imagination refusé par une dette
antérieure), le contrat E2 v2 de Codex (l'Hypothèse active Volonté, le sas au rang 3), #242 — préprod
`471a682`. Les notes plus anciennes du poste fixe (éveil, #239, #240/#241) étaient traitées à 2 h 30.
Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : E2 v2 (le chemin de fer à trois cercles, la variante Volonté du sas — noms et routes
  dans sa boîte) ; ses rouges (`excursion` l. 241 sous `:canvas` + `eveil.css` dans `.primary` ;
  `coque_m0` §9 72/68 ; `mentor_page` composeur) ; le Docteur sur `journeys/show` ; la phrase de la
  popup « Recommencer » sur les expériences sans session (facultatif).
- **Codex** : relire E2 v2 et la file (un écart nommé : l'ancienne validation ne propose pas le
  nouveau sas comme dette) ; les deux mots de contexte (Conseil, questionnaires) ; relire le lot
  serveur des badges ; le canon de l'opt-out ; #202/#211 ; les cinq illustrations.
- **Boris** : retest du M0 en préprod (`471a682`) ; puis la recette transversale et la promotion sur
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
