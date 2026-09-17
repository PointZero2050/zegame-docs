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
