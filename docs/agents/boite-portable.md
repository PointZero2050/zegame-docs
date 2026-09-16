# Boîte du portable

⚠️ **Vidée le 16 septembre 2026.** Traité : les PR #287 → #294 du poste fixe ; le repère du mentor et le
diagnostic d'E13 (lu en base) ; la provenance de la Graine ; le libellé du CTA final des éveils ;
E9/E12 ; `obtention_texte` — préprod `eb7356a`, recette **179/179**. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : les textes des rangs 2 et 3 d'**E19** (le rang 2 actuel porte deux gestes en un, le
  dialogue et la Graine ; il faut les défaire). Boris a accordé la porte mentor, la mécanique est
  prête — je sers dès sa réponse. Deux contraintes déjà transmises : pas de `confirmation` sur le
  rang 2 si son dialogue doit se prouver seul, et la durée totale égale à la somme des gestes.
- **Poste fixe** : les vues de la provenance (`PropositionDeGraine.a_planter_sur(cu)` est servi,
  `semer_sur_experience` accepte `proposition_id`) ; le style de `.omega-receipt-rappel` (la mention
  « Déjà distribué au premier accomplissement. ») ; le complément B des 18 verbes.
- **Boris** : retest du M0 sur `eb7356a` (Recette A remise à zéro le 15 au soir) ; la relance des
  paiements Festival (7 personnes, à la main) ; #202 (A) puis #211 ; les trois dependabot
  (#226, #227, #228) ; la recette transversale et la promotion sur son mot.
- **Moi, à la promotion** — la liste s'allonge de deux lignes :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build** (il refuse de tourner après, et c'est
    voulu : les confirmations sont rangées par numéro) ;
  - migrations : `recus_omega.rappel_le`, `propositions_de_graine.challenges_user_id`, plus les
    anciennes (`recus_omega`, `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb` ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`).
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

## La leçon du 15-16 septembre, parce qu'elle s'est répétée quatre fois

**Une assertion d'absence ne vaut que si l'on prouve d'abord que la chose aurait pu être là.** Quatre
bancs verts ne gardaient rien : un bandeau mesuré sur une fiche verrouillée (donc un 302) ; des ancres
comptées en guillemets doubles quand le helper en rend des simples ; « pas de popup au rejeu » qui
lisait un reste de flash, parce que le banc ne suivait pas ses redirections ; un retour après
correction mesuré sur le seul cas qui ne l'intéressait pas. Trois d'entre eux ont été révélés en
RETIRANT du code — ce qui veut dire qu'ils tenaient par effet de bord.
