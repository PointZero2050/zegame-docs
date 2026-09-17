# Boîte du portable

⚠️ **Vidée le 18 septembre 2026.** Traité : l'arbitrage E13 de Codex (servi, `a685ef6`) ; sa
validation du mot du rang 2 d'E19 (déjà servi, rien à faire) ; les six PR du poste fixe, #296 puis
#297 → #301, fusionnées à la main dans l'ordre, avec ma part — `@manquantes`, les clés de
`config/sas.yml`, les seuils des cartes, les cinq accroches de l'accueil public. Préprod
**`54d3cc9`**, recette ****182/182****. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#296 et #301 portent les comptes rendus) et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : une **déclaration morte au rang 3 d'E13** (« J'ai planté ma Graine de relation » est
  encore au YAML alors que le rang est prouvé — jamais rendue, jamais utile) ; et le **mot** pour
  « Reprendre cette Expérience » sur les lignes verrouillées de l'écran « Passage encore ouvert »
  (question du poste fixe ; les trois sorties qu'il propose sont servables telles quelles,
  `@manquantes` porte déjà l'état de chaque ligne).
- **Poste fixe** : le style de `.omega-receipt-rappel` (« Déjà distribué au premier
  accomplissement. ») ; le complément B des 18 verbes.
- **Boris** : retest du M0 — **et l'écran final s'affiche désormais quand il manque quelque chose**,
  en nommant quoi ; la relance des paiements Festival (7 personnes, à la main) ; #202 (A) puis
  #211 ; les trois dependabot (#226, #227, #228) ; la recette transversale et la promotion sur son
  mot.
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
  - **deux redémarrages** — et `config/sas.yml` entre désormais dans la liste des YAML mémoïsés,
    avec le parcours, les vidéos, le quiz d'E2, `coque.yml`, `monde_1.yml`, `badges.yml`.
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

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
La preuve évidente aurait rendu E19 puis E13 infranchissables à la quasi-totalité des joueurs.
**Avant d'adosser une preuve à un fait, demander qui l'écrit, et sous quels réglages.**

**Le M0 se mesure presque entièrement, et les décors des bancs doivent suivre** (18 septembre). Deux
bancs se sont cassés non parce qu'ils avaient tort, mais parce que leur DÉCOR n'existait plus : plus
aucune Expérience du Monde 0 ne porte deux gestes déclaratifs à porte d'excursion — le maximum est
un. Un décor écrit comme une liste de cas vieillit à chaque arbitrage ; un décor écrit comme une
règle (« un geste que ce banc sait accomplir », « les deux espèces présentes ») survit. Et quand un
décor se choisit par mesure, il faut qu'il exige ce que le banc teste : le premier trouvé était le
rang d'une Expérience vidéo, où la porte n'est pas exigible — le banc y mesurait le contraire de sa
propre règle.

**Quand un banc et une page se contredisent, mesurer ce que la page rend vraiment** (18 septembre,
deux fois en une heure). La régie des empreintes de `verifier_sas_vers_le_jeu` disait `[a-z-]+` et ne
voyait aucun nom de fichier portant un chiffre ; les deux scènes des scénarios étaient bel et bien
empreintées. Et le même banc portait DEUX tables des mêmes cinq adresses, dont une seule avait suivi
le portage. Dans les deux cas la page avait raison. Une recopie ne se garde pas toute seule : quand
une même vérité vit à deux endroits, ce qu'il faut livrer n'est pas la seconde copie, c'est
l'assertion qui les compare.
