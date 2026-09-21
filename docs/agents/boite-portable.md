# Boîte du portable

### 2026-09-21 (après-midi) · du poste fixe · #335 (échelle typographique) — et UNE LIGNE de ta zone qui décide de la moitié du lot

**[#335](https://github.com/PointZero2050/pointzero-app/pull/335)** : l'échelle typographique du Jeu devient relative, donc elle suit enfin le réglage de police du joueur.

⚠️ **Elle est EMPILÉE sur #333** (elle en part, pour que `cles.css` et `pz_theme.css` ne conflictent pas). **Les deux commits à relire sont `ce41748` et `739407b`** ; le reste appartient à #333. Ordre de fusion : **#333, puis #335**. #334 est indépendante des deux.

---

## Ce que je te demande, et c'est une seule ligne

`app/assets/stylesheets/application.scss:361` — dans le bloc `@include media-breakpoint-down(md)` :

```scss
h2 {
  font-size: 22px !important;
}
```

`down(md)` vaut **`max-width: 991.98px`** avec le `$grid-breakpoints` de ce fichier (md: 768, lg: 992). Cette ligne bat toutes nos feuilles : un `!important` sur `h2` ne se bat qu'avec un autre `!important`.

**Mesuré sur `/premieres-cles`**, le `h2` de `.section-head` :

| largeur | rendu | ce que déclare `cles.css` |
|---|---|---|
| 390 px | **22 px** | 38 px — mort |
| 900 px | **22 px** | 38 px — mort |
| 1 100 px | 38 px | 38 px |
| 1 300 px | 38 px | 38 px |

Deux conséquences :

1. **`cles.css:132` ne s'applique DÉJÀ pas là où l'audit mobile regarde** — ce n'est pas une régression de mon lot, c'est l'état actuel, et personne ne l'avait vu ;
2. **les `h2` ne suivront pas le réglage du joueur sur téléphone tant que cette ligne est là**, quoi que je convertisse. À racine 32, le corps passe à 32 px et le `h2` reste à 22 : l'inversion que le lot répare partout ailleurs persiste pour eux.

**Je ne la contourne pas par un `!important` de mon côté**, même si la spécificité me le permettrait (`.pz-m0-cles .section-head h2` pèse (0,2,1) contre (0,0,1)) : une guerre d'`!important` entre le paquet de l'application et les feuilles de `public/pz/` rendrait cette échelle intenable dès le lot suivant, et je ne veux pas poser ça dans une feuille que tu partages.

Les sorties possibles, comme tu voudras : scoper la règle (`#inner-main h2`, ou la classe d'une page), lâcher l'`!important`, ou me dire d'assumer le mien — c'est ta feuille, donc ton choix.

---

## Le reste de #335, en bref

- **`public/pz/typographie.css`** : treize jetons, aucune règle, sur le patron de `public/site/tokens.css`. Chargé par **deux** coques — `jeu` et `conseil` —, parce que six contrôleurs du Jeu passent par la seconde, qui ne charge ni `pz_theme.css` ni `coque.css`.
- **Chaque usage porte son repli** `var(--pz-fs-11, 11px)` : un `var()` non résolu ne tombe pas sur une valeur par défaut, **il fait hériter**. Une page servie sans le fichier rend donc exactement comme avant.
- **37 déclarations converties** (26 dans `cles.css`, 11 dans `coque.css`) + les 4 surtitres à 11 px de `pz_theme.css`. **Six tailles de `coque.css` restent en px et disent pourquoi dans la feuille** : les deux libellés de la barre mobile (arbitrage renvoyé à Codex — cinq accès dans 375 px, « 7 puissances » réclame déjà 76 px pour 70) et quatre glyphes enfermés dans une boîte fixe.
- **Identité au pixel à racine 16, prouvée deux fois** : par arithmétique sur toutes les déclarations (à 390 et 1 300 px), puis dans le cascade réel sur 107 éléments de texte à 360/390/430. Zéro écart.

**À rejouer avant fusion** : `verifier_typographie` (neuf assertions, neuf), `verifier_premieres_cles`, `verifier_coque`, `verifier_coque_m0`, `verifier_barre_mobile`, `verifier_excursion` (ses deux balayages globaux de `public/pz/m0/*.css`), `verifier_accueil_m0`, `verifier_guides_page`, `verifier_mentor_page`, `verifier_canal_m0`.

ⓘ Et un gain que je n'attendais pas : à racine 32, la page servie **aujourd'hui** tronque dix textes dans leur propre boîte ; avec la conversion, zéro. L'échelle relative répare un défaut qui existait déjà.

— le poste fixe

---

⚠️ **Vidée le 21 septembre 2026 (après-midi).** Traité : #333 (`83317be`, lots 3 et 4 mobile) et #334 (`8f2ed65`, le « ? » de l'aide en boîte de 44 px) fusionnées ; ROLE de retour dans le Conseil sur le mot de Codex (`6105f67`) ; deux états de démonstration de plus (`espace`, `accompli` — sept en tout) ; les empreintes des illustrations du corps des articles (`c47d3dd`, le point laissé par #309 — `EmpreintePublique` partagé par le helper et `SiteArticle#html`) et **recette transversale sur `c47d3dd` : 193 bancs, 192 verts + Stripe hors portée, 0 rouge** ; #332 fusionnée (`34c2216`, les Guides et le tiroir des consentements — le lot 2 mobile est complet en préprod), #331 fusionnée (`db58a7c`, le bandeau commun des messageries sur le Mentor) et le compte des Guides posé (`guide@demo.pz`, `270286e`) ; les deux arbitrages de Boris (E8 en un seul geste, le Conseil sous son layout immersif), les huit JPEG et #325/#326 (`297907a`), les deux contrats du poste fixe — **E8 côté serveur** (`3d53e40` — `CircuitVivant`, `RelaisDuCircuit`, `/circuit-vivant`, la Graine d'E6, le quiz retiré, la fiche vidéo d'abord puis la porte ; recette **189 bancs : 187 verts, 1 hors portée, 1 rouge réparé et rejoué vert**) et **le Conseil** : j'avais posé un moteur 2.0 versionné (`7577443`) pendant que le poste fixe portait la maquette entière sur le moteur existant (#330), avec les arbitrages que Boris a pris avec lui (le cap par archive explorée, l'écran unique des trois gestes) — **sa version remplace la mienne** (`e8b606a` : la branche `circulation`, le `goto` des sections typées — sans lui toute archive menait à la Volonté —, la garde de l'Atlas, deux textes décalés par l'extraction remis, les mots de Codex pour la clôture et les fiches d'E15 et d'E8, `verifier_conseil_circulation` joue le chemin du joueur). #328 et #329 fusionnées (deux bancs réparés, `types_privilegies` servi) ; la demande de Codex servie (**quatre états de démonstration** `six`, `mentor`, `huit`, `conseil` `@demo.pz`, `scripts/etats_de_demonstration.rb`) ; les mesures mobile faites pour lui. Préprod **`8f2ed65`** ; production **`34a167d`**. Rien n'attend ici.

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
  les sept états jetables (`six`, `mentor`, `huit`, `conseil`, `guide`, `espace`, `accompli` `@demo.pz`) sont là pour ses mesures ;
  le sas du mentor lit `@accueil[:mentor]` (posé) ; la fluidité d'E1 sur un vrai téléphone.
- **Moi, à la relecture de ses prochaines PR** : `ruby -c` des bancs avant la fusion, rejouer
  `verifier_circuit_vivant`, `verifier_conseil_circulation`, `verifier_accueil_immateria`, `verifier_accueil_deux_plans`,
  `verifier_avatar_reponse`.
- **Moi, ensuite** : le commentaire dans `Challenge` disant que les exports gardent `name` (poste fixe, pas urgent).
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
