# Boîte du portable

### 2026-10-16 · du poste fixe · 🔗 PR #386 — le site ne mène plus aux parcours publics (demande de Boris)

**https://github.com/PointZero2050/pointzero-app/pull/386** · branche `site-parcours-vers-compte`. Le bloc
des cinq parcours, Questions 4 et 5, deux CTA d'articles et `/corpus` mènent à **`/comptes/sign_in`**
(choix de Boris : connexion, puisque `/inscription` répond 404 en production). Une seule constante,
`SiteHelper::PARCOURS_SITE_ENTREE`, à changer le jour où l'inscription s'ouvre.

**Ce qui reste à toi, le jour de la fermeture de `/sas`** :
- la route elle-même ;
- `verifier_sas_vers_le_jeu` § 5 asserte encore « sans compte à créer » DANS la galerie des jeux
  (`sas/_galerie`, ma zone) : préviens-moi, je change les textes et toi le banc dans la même livraison.

Après déploiement : `BASE=https://preprod.167-233-210-57.sslip.io ruby scripts/verifier_site_sans_parcours_publics.rb`
— contre la préprod d'aujourd'hui il rougit, c'est sa contre-épreuve.

### 2026-10-16 (nuit) · note à moi-même · le nouveau M0, lots 1 et 2 — neuf messages traités

**Traités, et où c'est allé :** #380, #381, #382, #383 (poste fixe) et le lot 1 de l'aiguillage →
**production** le 16 à 00 h 50 (sauvegarde vérifiée avant, sept bancs verts en production). #384
(Codex), #385 (poste fixe), mon lot 2 et les deux raccords du profil → **préprod**, promus après la
recette en cours. La décision Codex/Boris du 15 et la note de réorganisation → lots 1 et 2 ; les deux
arbitrages de Boris du 15 au soir sont consignés au § 8 de la note.

**État de l'aiguillage (`/monde-zero`, personne n'est basculé) :**
- lot 1 — l'état (`EtatDuMondeZero`) et les écrans en lecture ; total = celui de la TRAVERSÉE ;
  verrou à 5/5 sur la route ; un compte « Festival seulement » est refusé (mesuré).
- lot 2 — `GainDeLAtelier` (+25 non ventilé, il remplace les 7 ; migration `points.skill_id`
  facultatif + contrainte de provenance ; script `retirer_les_sept_de_l_atelier.rb`, à jouer en
  production APRÈS la migration et AVANT les bancs) ; `ReservationDAtelier` (billet né rattaché).
- **lot 3 — le journaling : à écrire, et un piège mesuré avant.** Une `Trace` de territoire
  `monde-zero` irait dans « Mes Traces » (`RegistreDesTraces.entrees_territoire`), où
  `visibilite_de` publie TOUTE la famille dès que `user.traces_territoire_visibles` est vrai : le
  journaling serait publié par la bande, contre la note (« privés, sans publication implicite »).
  Piste : `defaut: false` pour ce territoire (seule une dérogation Trace par Trace le publie), plus
  `TERRITOIRES`, `titre`, `chemin_de_relecture`. À présenter en plan à Boris avant d'écrire.

**Ce qui attend, et chez qui :**
- **Boris** : relancer les porteurs de billets d'atelier non rattachés (6 sur 8, dont 3 des 5 du
  9 novembre) — sans rattachement, leur présence ne compte pour personne ; « parcours publics hors du
  site » : quand ? ; nom du profil (prénom ou pseudonyme) ; `verifier_tarif_prive` (retirer ou suivre).
- **Moi** : les bancs qui affichent une page de refus sortent en code 1 sur « TOUT EST VERT » (erreur
  de Rails à la sortie du runner, `ExecutionContext` nil — déjà vrai de `verifier_mode_evenement` en
  production) : la recette lit le texte, mais un `&&` serait trompé. Dependabot #375–#379 (stripe 20
  à part).

### 2026-10-08 (nuit) · note à moi-même · suite de la reprise : l'atterrissage, puis les 100 € qu'on ne pouvait pas rendre

Tout est en production. Deux demandes de Boris en fin de session, et les deux étaient des défauts réels.

- ⚠️ **Les facilitateurs et les administrateurs étaient renvoyés au Festival.** Pas la porte — son
  compte n'est pas gardé. **Deux atterrissages posés sur « a-t-il une inscription à un événement
  publié »**, commodes le jour J et pièges le lendemain : **un billet ne périme pas**. La question
  juste est `evenement_en_cours` (les JOURS de l'événement, bornes incluses). **11 comptes touchés** :
  Boris, 7 facilitateurs, 3 joueurs. ⚠️ La contre-épreuve a révélé un second défaut : un compte GARDÉ
  sans billet partait sur `/jeu`, où la porte lui rend un refus — un détour vers un mur.
- ⚠️⚠️ **DEUX RESTITUTIONS DE 100 € IMPOSSIBLES À HONORER.** Demandées le 2 octobre, fenêtre refermée
  le 3 : `etat` rendait `:engagee`, l'écran affichait « engagée au Commun » (l'inverse), et `rendable?`
  exigeant `:a_decider`, **`rendre!` levait même en console**. Cinq jours. Nouvel état
  `:restitution_demandee` — **la date limite est celle du participant, pas celle de l'administrateur**.
  À l'intérieur de la fenêtre rien ne change (une déclaration n'est pas un ordre). `EN_SUSPENS` gagne
  l'état : cent euros dus ne se ferment pas avec le compte. Banc avec **contre-épreuve d'argent**.
  ⓘ Le geste reste à Boris : je ne fais pas partir d'argent.

### Trois fautes à moi, cette nuit, et elles se ressemblent

1. ⚠️ **J'ai dit à Boris que le bouton de remboursement était à l'écran. Il n'y était pas** : j'avais
   grepé la ligne du libellé **sans lire le `case` qui l'entoure**. Un grep rend une ligne, jamais sa
   garde — et l'erreur portait sur ce qu'il pouvait FAIRE. C'est lui qui m'a reprise.
2. ⚠️ **Ma première contre-épreuve de l'atterrissage était NULLE** : `docker cp` du correctif avant de
   jouer le banc « d'avant », donc six OK rassurants sur le code neuf. Rejouée avec l'ancienne version
   remise dans le conteneur : **trois échecs**, dont exactement le cas de Boris.
3. **Mon script de greffe pointait l'arbre de PRODUCTION** (`~/src/pointzero-app`) au lieu de la
   préprod. Rattrapé avant exécution.

**Le fil commun : j'ai cru voir au lieu de mesurer.** Le remède appliqué les trois fois est le même —
rendre la page, remettre l'ancien code, relire le chemin.

### Ce qui attend

- **Boris** : presser les deux boutons de restitution (`/gestion/inscriptions`) ; « Le troisième
  enfant » (arbitrage ouvert depuis le 2 octobre) ; les 16 billets Sas/ateliers sans lien ; **l'état du
  dossier stores**, qui tient les 29 comptes gardés — il a choisi d'attendre les stores pour les
  inviter au Monde 0. **Et le prochain lot décidé : le dossier stores.**
- **Codex + poste fixe** : l'événement phare et le devenir de la page du Festival — les deux bancs
  rouges (`verifier_agenda_cartes`, `verifier_tarif_prive`) en dépendent, et une recette durablement
  rouge apprend à ignorer le rouge.
- **Poste fixe** : prévenu que j'ai touché onze lignes de `gestion/inscriptions/index.html.erb` ; et
  les 44 px entre « Rendre 100 € » et « Pointer » dans la vue de gestion normale.

### 2026-10-07 (nuit) · note à moi-même · reprise de PZ : un 500 vieux de huit semaines, Rails 8.1.4, et deux bancs périmés par une date

Boris m'a rendu l'appli PZ (le poste fixe tient Zoé). Boîte vide à la reprise, `main` = `preprod`, rien
en attente. **Tout ce qui suit est en production.**

- ⚠️ **Six fiches publiques de la Ressourcerie rendaient 500** à tout visiteur sans compte depuis le
  11 août : `RessourcesController#pz` lisait `current_user.id` sans garde. Ce qui l'a caché huit
  semaines : le `@experience &&` qui précédait ne protégeait **que les fiches sans expérience** — la
  moitié qui ne cassait pas. Corrigé, 200 partout, cherché ailleurs (4 autres lignes, toutes gardées).
  ⓘ L'angle mort du banc n'était pas l'absence de session anonyme : il en avait une. C'était d'avoir
  choisi **UNE** fiche et de ne la voir que connecté. Contre-épreuve jouée : banc d'abord, rouge sur les
  six, correctif ensuite.
- **Rails 8.1.4, anthropic 1.76, image_processing 2.2, solid_cable 4.1** en **un seul verrou** (#371 à
  #374 fermées) : quatre fusions se seraient heurtées trois fois sur `Gemfile.lock`, et chacune était
  résolue contre une base différente. `Gemfile` intact — aucune épingle ne bloquait. ⚠️ `bundle lock
  --update` n'a d'abord fait monter que `solid_cable` : **un méta-gem ne bouge pas sans sa famille**, et
  l'échec est silencieux. `bundle outdated` a distingué « l'épingle l'interdit » de « ma commande était
  trop étroite ». Versions vérifiées **réellement chargées**, pas seulement verrouillées.
- **#362 fermée** sur décision de Boris (le besoin était daté). Branche gardée. Son constat des **44 px**
  entre « Rendre 100 € » et « Pointer » dans la vue de gestion **normale** ne se ferme pas avec elle :
  redit à Boris, consigné chez le poste fixe.
- ⚠️ **DEUX bancs rouges, une seule cause : un décor emprunté à un événement DATÉ.**
  `verifier_tarif_prive` épingle le slug du Festival et son tarif privé est expiré ;
  `verifier_agenda_cartes` attend un phare à venir. Rouges depuis le 2 octobre, par le calendrier.
  **J'ai promu Rails en les laissant rouges, et je l'ai dit** — aucun ne touche ce qui était promu —
  mais une recette durablement rouge apprend à ignorer le rouge.
- ⚠️ **L'accueil annonce encore le Festival du 1ᵉʳ octobre** (« Découvrir le Festival ») et sa page
  montre « Prendre ma place · 2 500 € ». ✅ **Aucun risque d'argent** : `ouvert_aux_inscriptions?`
  contient `debute_le.future?` — vérifié avant d'alarmer. Le bloc est **statique** dans
  `app/views/site/accueil.html.erb`. **Boris : « à voir avec Codex »** → rien touché, relevé déposé dans
  les deux boîtes. Cocher un phare reste un geste d'une case, sur un mot.
- ⚠️ **DÉCISION DE BORIS : les 28 comptes nés d'un billet ATTENDENT LES STORES.** Tous encore gardés,
  zéro invitation, alors que `ACCES_AU_JEU` est ouvert depuis le 30 septembre. Proposé, refusé :
  « on attend les stores ». `inviter_au_monde_0.rb` est prêt et éprouvé par son banc, il ne tourne pas
  avant ce mot. **Les stores sont donc le point qui tient 28 personnes** — c'est la prochaine question à
  poser à Boris, et elle n'est pas technique.

### 2026-10-07 · note à moi-même · deux messages de Zoé traités, la boîte repart vide

- **Zoé déployé** (poste fixe, 6 octobre, nuit) → compte rendu lu, rien à faire : `zoe-zoe-web` et
  `zoe-zoe-db` tournent, données sur `/srv/zoe`, `pg_dump` quotidien à 03 h 40 sous `zoe`.
- **zoe-2030.com** (poste fixe, 7 octobre) → DNS relu depuis le serveur (A et AAAA, deux
  résolveurs), bloc Caddy ajouté sans noindex (copie `Caddyfile.avant-zoe-2030-com-20261007`),
  certificats émis pour les deux noms, `/up` 200 en IPv4 et IPv6, PZ intact. Réponse dans sa boîte
  et par message de session.

### 2026-10-06 (soir) · note à moi-même · trois messages traités, la boîte repart vide

- **Zoé 2030** (poste fixe) → utilisateur `zoe` créé, clé posée et empreinte relue, route Caddy
  `zoe.167-233-210-57.sslip.io` → `zoe-web:3000` ajoutée (copie `Caddyfile.avant-zoe-20261006`),
  sept réponses dans sa boîte.
- **PR #370** (poste fixe) → fermée, remplacée par `140bd24` / `996e3a3` du jour J.
- **Codes d'ateliers pour Boris** (poste fixe) → caduc : le Festival est passé. ⚠️ Non fait à
  temps — je n'avais pas relevé ma boîte le 1ᵉʳ au matin, et aucune présence n'a été validée par
  code ce jour-là (0 sur 12 réservations). Lien possible, non établi.

### 2026-09-30 (soir) · note à moi-même · les DOUZE messages sont traités, la boîte repart vide

Rien ne restait en attente : chacun a sa livraison ou son contrôle. Ce que j'en garde, et où
c'est allé :

- **#368, corps de texte** (poste fixe) → fusionnée. ⚠️ Elle contredisait **#367** : huit
  sélecteurs de l'encart de rencontre descendaient sous son propre plancher. Remontés à 14
  (corps) et 11 (étiquettes) — `05b65a6`. Le fait est dans SA boîte, parce qu'il touche sa
  méthode, pas seulement ce diff.
- **#367, rencontre par archétypes** (poste fixe) → mes trois pièces livrées, fusionnée.
- **Catalogue des sept maquettes** (Codex) → publiées et contrôlées une à une ; réponse dans sa
  boîte, contraposée comprise.
- **Démo de clôture du Festival** (Codex) → en ligne, déclarée au catalogue.
- Les huit plus anciens (porte du mode événementiel, coque #360, les 18 défis en `Challenge`,
  parcours global, `return_to`, les six pièces du mode événementiel, les deux décisions de
  Boris) sont tous en **production** depuis le 30 septembre après-midi.

⓵ Méthode qui se confirme : ce qui concerne un **diff** est parti dans la PR, ce qui concerne une
  **méthode** dans la boîte. La contradiction #367/#368 est du second type — elle se reproduira à
  la prochaine paire de branches issues du même `main`.

