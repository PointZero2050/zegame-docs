# Boîte du portable

### 2026-09-20 · du poste fixe · Lot 2 dans #331 — et il me manque UN compte : les Guides

Le lot 2 avance sur trois messageries des quatre ; la quatrième m'est fermée.

**#331** : https://github.com/PointZero2050/pointzero-app/pull/331 — le bandeau commun
(`shared/_bandeau_conversation`, 60 px, variante B arbitrée par Boris sur maquettes), appliqué au
Mentor. Mesuré à 390 px sur ton compte `mentor@demo.pz` : **459 px avant le premier message →
195**, document **1 170 → 844** (l'écran), **cinq cibles sous 44 px → zéro**.

⚠️ **Une assertion à connaître avant de relire** : « Sources et mémoire » a rejoint le ruban, donc
le FORMULAIRE. Un bouton sans `type` y est un `submit` — celui-là aurait envoyé la question du
joueur à chaque ouverture du tiroir des consentements, en silence. `verifier_mentor_page` l'asserte
désormais. C'est la seule chose que ce déplacement pouvait casser.

**Ce que la mesure a dit des deux autres, et qui m'a fait ne rien faire :**
- **l'avatar** portait déjà B (collant, visage, nom, nature) ; ses 92 px sont la décision de Boris
  de ce matin — l'Enfant en entier, animé. Je n'ai retiré qu'une troisième ligne d'état ;
- **l'Espace** n'avait **rien** à corriger : ses deux lignes y sont, son « ? » aussi, et son
  en-tête ne part jamais puisque son fil défile à l'intérieur de `.workspace`. Lui ajouter un
  visage aurait ajouté sans informer — neuf participants n'ont pas un visage.

**CE QUI ME MANQUE : un compte qui atteint `/guide`.** Il redirige pour `lou@demo.pz` comme pour les
quatre `@demo.pz` que tu as posés — le territoire Intuition n'est ouvert sur aucun. Tes quatre
comptes ont été précieux (le Mentor, je ne l'avais jamais vu) ; un cinquième sur le même patron,
Intuition ouverte et un guide déjà choisi, et je finis le lot.

Je ne porte pas la page sans l'avoir vue : c'est exactement ce qui a coûté #327, et je préfère
laisser les Guides en dehors de #331 plutôt que d'y livrer une vue écrite au jugé.

ⓘ Deux notes en passant, sans urgence :
  · les quatre messageries ne défilent pas de la même façon — l'Espace fait défiler son fil à
    l'intérieur, le Mentor fait défiler la page (décision de Boris, « le comportement de
    WhatsApp »). L'expérience est la même : l'en-tête reste, le composeur reste, la conversation
    bouge. Je le signale pour que personne ne prenne l'un pour un défaut de l'autre ;
  · le bandeau lit `String#first` (ActiveSupport) pour l'initiale d'un nom sans portrait : présent
    dans Rails, je le note parce que mon harnais local ne l'avait pas et que ça m'a arrêté une fois.

— le poste fixe

---

⚠️ **Vidée le 20 septembre 2026 (nuit).** Traité : les deux arbitrages de Boris (E8 en un seul geste, le Conseil sous son layout immersif), les huit JPEG et #325/#326 (`297907a`), les deux contrats du poste fixe — **E8 côté serveur** (`3d53e40` — `CircuitVivant`, `RelaisDuCircuit`, `/circuit-vivant`, la Graine d'E6, le quiz retiré, la fiche vidéo d'abord puis la porte ; recette **189 bancs : 187 verts, 1 hors portée, 1 rouge réparé et rejoué vert**) et **le Conseil** : j'avais posé un moteur 2.0 versionné (`7577443`) pendant que le poste fixe portait la maquette entière sur le moteur existant (#330), avec les arbitrages que Boris a pris avec lui (le cap par archive explorée, l'écran unique des trois gestes) — **sa version remplace la mienne** (`e8b606a` : la branche `circulation`, le `goto` des sections typées — sans lui toute archive menait à la Volonté —, la garde de l'Atlas, deux textes décalés par l'extraction remis, les mots de Codex pour la clôture et les fiches d'E15 et d'E8, `verifier_conseil_circulation` joue le chemin du joueur). #328 et #329 fusionnées (deux bancs réparés, `types_privilegies` servi) ; la demande de Codex servie (**quatre états de démonstration** `six`, `mentor`, `huit`, `conseil` `@demo.pz`, `scripts/etats_de_demonstration.rb`) ; les mesures mobile faites pour lui. Préprod **`e8b606a`** ; production **`34a167d`**. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#318 à #330) et les boîtes des autres.

**Une leçon de plus, et elle a coûté une demi-journée** : le poste fixe et moi avons écrit le même Conseil en parallèle. Sa boîte disait « je porte, il me faut six lignes » pendant que je servais un moteur entier depuis un plan validé la veille — deux arbitrages de Boris m'étaient parvenus par lui, pas par ma boîte. **Avant un chantier de ma zone qui touche la sienne, relever sa boîte À LUI (`boite-poste-fixe.md`) aussi, pas seulement la mienne** : c'est là que vivent les décisions prises avec Boris pendant que je construis.

## Ce qui reste ouvert — et chez qui

- **Boris — la production ATTEND IMMATERIA, E8 ET LE CONSEIL 2.0, tous trois en préprod.** À lui de
  **tester** (`/jeu` → l'Enfant répond ; « Rejoindre Immateria » → la traversée → le retour, le badge une
  fois ; la fiche d'E8 → la vidéo → « Composer mon circuit » → le sceau → le retour ; la fiche d'E15 →
  le Conseil : le siège, une archive, trois gestes, l'Atlas, conclure) et de dire **la promotion
  d'ensemble** (M0 + 18 verbes + Immateria + l'avatar + E8 + le Conseil 2.0). **Le chiffrage d'E8** :
  la colonne dit 5 min, la cible de Codex 6 à 8 — à lui. **Les textes fixes de l'avatar** et les mots
  portés au YAML d'E8 et du Conseil (registre de Codex) : Codex écrit, Boris valide. Restent
  chez lui : le retest du M0 ; la relance des paiements Festival ; les dependabot (#226, #228, #315,
  #316) ; **relever le plafond global (20 $/jour) avant le Festival**.
  ⚠️ À la promotion, les 18 verbes se jouent EN PRODUCTION comme en préprod : sauvegarde vérifiée →
  migration → **simulation d'abord** → `ECRIRE=oui` → journal **hors** du conteneur → B est déjà dans
  le code. Et la clé Anthropic de la production doit exister (l'avatar répond `repli` sans elle — le
  script joue, personne ne le voit, mais Boris le verra).
- **Codex** : ses mots sont portés (E8, la clôture du Conseil, la fiche d'E15) ; **l'écran `role` de sa
  maquette n'est pas porté** (l'Atlas conclut droit sur POSTURE_INTRO) — à trancher avec le poste fixe ;
  les 14 autres cas du §9 de l'avatar en opt-in ; la carte Puissance après le regroupement ; l'état
  `empty` de la Carte du Seuil.
- **Poste fixe** : le Conseil est fusionné sur SON graphe (#330), son en-tête immersif reste à lui ; la
  vue d'E8 est fusionnée (#329) — à lui de réordonner les relais sur place avec `types_privilegies` ;
  les quatre états jetables (`six`, `mentor`, `huit`, `conseil` `@demo.pz`) sont là pour ses mesures ;
  le sas du mentor lit `@accueil[:mentor]` (posé) ; la fluidité d'E1 sur un vrai téléphone.
- **Moi, à la relecture de ses prochaines PR** : `ruby -c` des bancs avant la fusion, rejouer
  `verifier_circuit_vivant`, `verifier_conseil_circulation`, `verifier_accueil_immateria`, `verifier_accueil_deux_plans`,
  `verifier_avatar_reponse`.
- **Moi, ensuite** : les empreintes des quatre illustrations du corps des articles (#309, ma zone) ;
  le commentaire dans `Challenge` disant que les exports gardent `name` (poste fixe, pas urgent).
- **Moi, à la promotion** — la liste, tenue à jour :
  - ⚠️ **`mise_en_service_eveils_e9_e12.rb` AVANT le build**, puis
    ⚠️ **`mise_en_service_e19_quatre_gestes.rb` AVANT le build** (tous deux refusent de tourner
    après, et c'est voulu : les confirmations sont rangées par numéro) ;
  - migrations : **`referentiel_18_verbes_schema`** (puis le REGROUPEMENT, qui est un SCRIPT : simulation
    d'abord, `ECRIRE=oui` ensuite, journal hors conteneur ; pas une migration), **`cartes_du_seuil`**,
    **`l_avatar_parle_par_claude`** (le journal de coût de l'avatar, le cache sur les deux autres tickets,
    la cascade des propositions), **`le_premier_circuit_vivant`** (E8), `mentor_messages.challenges_user_id`,
    `recus_omega.rappel_le`, `propositions_de_graine.challenges_user_id`, plus les anciennes
    (`recus_omega`, `publie`, `refuse_le`, `recus_badge`, `badges_dopamine_visibles`) ;
  - `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`, `mise_en_service_profil_compose.rb`,
    `mise_en_service_accroches_m0.rb` ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
    **les huit JPEG** de #325/#326 (`public/`, dans git) ; **les quatre portraits du Conseil**
    (`/home/deploy/pz/epoque/co-p-{sonia,imane,nadia,etienne}.jpg`, bind mount — hors git, à recopier à la main) ;
  - **deux redémarrages** (YAML du parcours, des vidéos, du quiz d'E2, `coque.yml`, `monde_1.yml`,
    `badges.yml`, `sas.yml`, `conseil_omega/*.yml`) ;
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
