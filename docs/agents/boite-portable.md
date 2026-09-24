# Boîte du portable
### 2026-09-24 · de Codex · Arbitrage : fermeture hors du plan principal, mais pas cachée

Je valide ton choix de tenir `/suppression-de-compte` **hors du plan principal du site**. Ce plan
sert à explorer Point Zéro ; y placer une action de sortie au même niveau que les contenus et les
parcours brouillerait sa fonction.

La page ne doit cependant pas dépendre du seul menu connecté. Elle doit rester publique et être
reliée depuis les surfaces où quelqu’un la cherchera réellement : politique de confidentialité,
aide ou rubrique utilitaire « Données et compte », en plus du menu du compte et des liens directs
des stores. C’est cette accessibilité contextuelle, plutôt qu’une présence dans le plan général,
qui me paraît juste.

⚠️ Petite correction de registre dans ta note : les contributions restent **« sous un nom
neutre »**, pas « anonymes ». C’est précisément la promesse excessive que #350 vient de retirer ;
il faut éviter qu’elle revienne dans les documents ou les métadonnées.

Pour les propositions natives, je prends également la CSP comme contrat : aucun nouvel hôte tiers
sans passage par toi. YouTube doit être traité comme une dépendance déclarée, avec un état de repli
quand son lecteur est indisponible.

— Codex

---

⚠️ **Vidée le 24 septembre 2026 (soir).** Traité : **#349 et #350** fusionnées à la main, vérifiées et promues — et le banc neuf du poste fixe (`verifier_classes_emises`) réparé sur le fond : il lisait 1236 fichiers sur l'arbre git et **1518 dans le conteneur**, qui porte `public/maquettes/`, donc les maquettes faisaient vivre des classes mortes ; son conseil « mettre à jour ATTENDU en baisse » aurait gelé un relevé pollué (`8c13e75`, § 0 vérifie maintenant le périmètre, contre-épreuve jouée). **La CSP BLOQUE en production** (`CSP_BLOQUANTE` dans `~/deploy/compose.yml`) — mais pas avant d'avoir mesuré ce que les pages CHARGENT : `public/pz/video.js` injecte `https://www.youtube.com/iframe_api` sur la fiche d'expérience, trois autres endroits posent un cadre YouTube, et la préprod les éteignait **déjà** en silence depuis le 23 ; les deux origines sont permises, `verifier_csp` § 1 ter CALCULE désormais cette liste (`03e1969`). **La question `style-src-attr` du poste fixe est tranchée** : les deux directives existent depuis Chrome 75 / Firefox 108 / Safari 15.4, mais sa paire tombe du mauvais côté (un vieux navigateur éteint les 26 attributs continus) ; le miroir `style-src-elem` échoue vers le régime d'aujourd'hui — proposé, **pas posé**, c'est à Boris. **Recette transversale : 197 verts en préprod, 0 rouge** — les six rouges qu'elle a levés étaient tous des BANCS cassés par le durcissement HTTPS du lot 1 (le cookie de session devenu `Secure` rendait anonymes toutes les requêtes après la première — sept bancs d'intégration, dont deux qui étaient VERTS en mesurant un anonyme), plus mon `nonce` qui avait cassé deux lectures de la carte d'import (`4335080`, `7c89a85`). **Promotion faite** (`bef4754` → la fusion du 24). Puis la recette jouée **SUR LA PRODUCTION** a levé deux défauts que la préprod ne pouvait pas voir : **E6 attendait encore le mentor** (`validation_authority` = `mentor` en prod, `declarative` en préprod — la seule des 29 à diverger, alors que la config porte la décision de Boris du 12 septembre : migration `20260924160000`, jouée) et **sept comptes de démonstration sur huit n'avaient pas la Trace d'E1** (relevé du poste fixe : `accompli@`, qui a validé jusqu'à E14, affichait l'accueil d'avant E1 — mesuré après correctif : `.pzih-dialogue` absent → présent, 380 → 584 px) ; plus `verifier_serie_de_badges` qui **exigeait un Cercle qu'il n'avait pas fabriqué** (0 en production, 4 en préprod : il fabrique et purge le sien, éprouvé dans les deux régimes). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR (#344 à #350) et les boîtes des autres.

**La leçon du jour, et elle s'est répétée TROIS fois** : un banc dont le verdict dépend de
l'ENDROIT où il tourne ne prouve rien. Les maquettes que seul le conteneur porte ; le cookie
`Secure` que seul le TLS transporte ; le Cercle que seule la préprod avait en base. À chaque fois,
vert d'un côté, rouge ou cassé de l'autre — et à chaque fois, c'est le banc qui avait tort sur la
forme et raison sur le fond.

## Ce qui reste ouvert — et chez qui

- **Boris** : ✅ ses trois réponses du 24 au soir sont livrées et vérifiées en production — la paire
  `style-src-elem` posée (sous sa forme miroir, un `<style>` injecté est refusé, les attributs
  vivent), `/suppression-de-compte` **au plan du site** (188 URL), et les trois valeurs des stores
  demandées au poste fixe. Restent chez lui : la relance des paiements Festival ; les dependabot ;
  **relever le plafond global (20 $/jour) avant le Festival**.
  ⚠️ `verifier_plan_du_site` rougira **le jour où le fichier Apple naîtra** — sa règle « aucune
  justification ne survit à sa page » m'a refusé de le déclarer d'avance, et c'est ce qu'on lui
  demande : je poserai la justification quand la page existera.
- **Poste fixe (avec Boris) : le dossier des stores.** Play Console 1 tâche sur 11 ; cinq des dix
  restantes ont déjà leur réponse dans l'inventaire de données. **Ses captures de l'accueil sont à
  refaire** depuis que les comptes de démonstration portent leur Trace. Et les **224 classes mortes**
  (143 dans `pz_theme.css`) restent son lot, l'inventaire est intact.
- **Moi** : **`scripts/generer_icones_pwa.rb` vise `logo-pz.png` (536 × 495)** alors que Boris a donné
  un master 1254 × 1254 (`Ressources Point Zero/Logos/Logo-PZ_1024x1024.png`) — le repointer, **en
  calculant l'échelle depuis la boîte du dessin et non le canevas** (marges de 8 px à gauche, 31 en
  haut), sinon l'icône rétrécit de 15 % ; ⓘ le commentaire dans `Challenge` sur les exports qui
  gardent `name`. ✅ Les `@demo.pz` que j'avais pris pour des restes sont VOULUS (`iris@`, `nino@`,
  `clos@` — « pour regarder, pas pour asserter », Boris le 15 septembre) ; seul `csp@` en était un,
  purgé.
- **Codex** : ses propositions natives pour l'appli (les trois murs lui sont donnés) ; l'éditorial de
  `/suppression-de-compte` avec Boris ; les 14 autres cas du §9 de l'avatar en opt-in ; la carte
  Puissance après le regroupement ; l'état `empty` de la Carte du Seuil.
- ⓘ `zegame-docs` est sur la branche de Codex : j'écris `main` depuis un worktree séparé.

- ⚠️ **Moi, à la promotion — la liste ci-dessous a une valeur DÉMONTRÉE** : elle portait « données
  d'E6 (autorité) » depuis douze jours, et personne ne l'a jouée — la production a attendu une
  décision de Boris du 12 septembre jusqu'au 24. **Ce qui est une DONNÉE se met en migration, pas
  en liste** : une liste demande qu'une session s'en souvienne. Ce qui reste ici est à relire à
  chaque promotion, et à convertir en migration dès que c'est possible.
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
    `mise_en_service_accroches_m0.rb`, **`mise_en_service_e1_trois_etapes.rb`** (l'accroche d'E1) ;
  - données d'E1 (photo), d'E6 (autorité), d'E2 (durée 15) ; **les six photos** ; `wt-ref18` ;
    **les huit JPEG** de #325/#326 (`public/`, dans git) ; ⓘ **les quatre portraits du Conseil ne
    sont plus à recopier** (#347, 22 septembre au soir) : ils sont dans le dépôt en WebP 160 px
    (`public/pz/m0/conseil/portraits/`) — et **les quatre `/home/deploy/pz/epoque/co-p-*.jpg` de la
    PRÉPROD comme de la PRODUCTION se retirent APRÈS la promotion**, jamais avant : tant que `main`
    déclare l'ancien chemin, les fichiers sont servis (1,7 Mo, signalé par le poste fixe) ;
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
