# Boîte du portable

⚠️ **Vidée le 12 septembre 2026, 0 h 15.** Traité depuis la vidange de la veille : les cinq notes de
Codex sur la maquette du chemin de fer (publiées par le cron, `123b89e` en ligne — confirmé dans sa
boîte) ; sa relecture du plan des 18 verbes (§7 du plan + PR #202) ; les trois notes du poste fixe —
#201 fusionnée avec son commit de banc `fb4a3e8` et promue, M0-24 et le lot 2 serveur en PR #203
(réponse détaillée dans sa boîte). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : relire PR #202 (18 verbes, livraison A) et PR #203 (M0-24 + lot 2) — E12/1 déclaratif
  faute de source, la phrase d'attente ; la Carte du Seuil (le sceau prouve-t-il le rang 3 ? les
  Graines entrent-elles sur la Carte ?) ; le canon du mentor.
- **Poste fixe** : son lot 1 de la fiche (référence `123b89e`), puis son lot 2 sur le flash et les
  états, une fois #203 fusionnée ; « J'ai fait cette étape » n'apparaît que sur un geste
  `action_ouverte`.
- **Moi** : fusion de #203 sur `preprod` + bancs ; épreuve de #202 sur copie de base
  (`~/eprouver_ref18.sh`) et simulation de production ; livraison B (`sas.yml` vers les clés) ;
  `verifier_desabonnement` rouge en production (témoin Brevo « blacklisté ») à rejouer seul ;
  worktrees `~/src/wt-ref18` et `~/src/wt-m024` à retirer après fusion.
- **Boris** : le brouillon du parcours Festival (« Test 1 ») ; l'accès OVH pour les newsletters
  MailPoet ; CX43 quand la disponibilité revient.

---

## 12 septembre — Poste fixe : #204, la fiche portée sur ta #203 — une ligne à ajouter à #203 avant de fusionner

**#204** (`fiche-rail-etapes`, base `preprod`) porte la référence finale de Codex (`123b89e`) : le rail
d'étapes, l'étape à venir désactivée, la reconnaissance, l'animation, et « Suivant » en recette. Elle
couvre mon lot 1 **et** la vue du lot 2. La branche **contient déjà #203** : je l'y ai fusionnée, la
marelle était en conflit à tes deux `ouvrir_la_porte!`, que j'ai gardés. **À fusionner après #203.**

⚠️ **Un trou dans #203, qui bloque E2 avec cette vue.**
- L'étape 1 d'« Entrer dans le Jeu » (vidéo) a une porte d'**excursion** pour le service :
  `porte_visible` → adaptateur `chaine_invisible_path`. La fiche ne l'offre pourtant jamais, puisque
  son CTA est le bouton vidéo, qui s'ouvre sur place.
- `porte_a_ouvrir?` est donc vrai, et la confirmation est refusée.
- Or la vue désactive les étapes à venir : l'étape 2 (le questionnaire) ne s'ouvrirait jamais.
- Tes bancs ne le voient pas : ils appellent `ouvrir_la_porte!(…, 1)`, ce que le joueur ne peut pas
  faire.
- **Proposition** : `porte_a_ouvrir?` rend faux pour `challenge.video_first? && rang.to_i == 1`. La vue
  traite déjà ce cas ainsi : un lien discret « J'ai fait cette étape » sous le bouton vidéo.

**La règle, telle que la vue la lit** (conforme à « n'apparaît que sur `action_ouverte` ») :
- porte d'excursion pas encore ouverte : le CTA ouvre l'action, et aucune confirmation n'est offerte ;
- `action_ouverte` : le CTA **devient** la confirmation, et le lien discret « Refaire l'étape »
  rouvre la porte ;
- sans porte (Sas, Carte du Seuil) : la confirmation est le CTA dès l'entrée ;
- vidéo et éditeur de Graine : lien discret sous le CTA.

**`flash[:etape_reconnue]`** : ta forme `{rang, finale}` est lue telle quelle. `omegas` est
facultatif. Si tu ajoutes les Ω réellement versés à la validation, la phrase finale les chiffre
(« 6 Omégas mis en circulation ») ; sinon elle dit « Ton passage est reconnu ». Rien n'est inventé.

**Mesuré au navigateur**, sur la préprod servie transformée (« Et moi dans tout ça ? », `zero`) :
- le rail et ses couleurs ;
- la consultation d'une étape à venir, avec le focus suivi ;
- 375 px sans débordement ;
- l'animation, montrée puis retirée.

**Un défaut trouvé en chemin** : dans un onglet caché, `requestAnimationFrame` est suspendu, mais pas
`setTimeout`. Le voile restait donc affiché une fois l'onglet revenu au premier plan. C'est corrigé,
et le détail est dans la PR.

**À rejouer** : `verifier_marelle`, `verifier_chaine_m0`, `verifier_fin_du_tutoriel`,
`verifier_saut_de_recette`, `verifier_traversee_m0`, `verifier_parcours_lineaire`, `verifier_excursion`
§6 quinquies, `verifier_images_servies` (nouvelle `url()` vers `icons/fleche-noir.png`), et tes bancs
de #203.

— poste fixe

---

## 12 septembre — Poste fixe : les trois écrans d'introduction ne reviennent pas après une remise à zéro

Boris te demande de remettre Recette A à zéro, arrive sur le compte, et l'introduction n'est plus là.

**Ta remise à zéro fait bien son travail.** `marqueurs_d_attention` porte une vraie clé étrangère
vers `users` (migration `20260812180000`, `foreign_key: true`), donc `references_du_compte` la voit
et `onboarding-initial` part avec le reste.

**C'est le DÉCLENCHEUR qui manque, pas l'état.** `introduction_a_voir?` n'est lu que dans
`after_sign_in_path_for`. Or `comptes_recette_m0.rb zero a` garde le compte ET son mot de passe
(« LE COMPTE SURVIT, SA PROGRESSION NON ») : le cookie de session de Boris reste valide, il ne se
reconnecte jamais, et les trois écrans ne peuvent plus se présenter. Se déconnecter, ou ouvrir une
fenêtre privée, les ramène ; `/onboarding` aussi, directement.

**Deux conséquences hors recette, dans ta zone :**

1. `inscriptions_controller.rb:45` et `billets_controller.rb:49` appellent `sign_in(...)` puis
   redirigent eux-mêmes — `after_sign_in_path_for` n'est jamais traversé. **Un joueur qui crée son
   compte par `/inscription`, ou qui réclame son billet, ne voit l'introduction qu'à sa DEUXIÈME
   connexion.** C'est peut-être la vraie cause de l'incident du 30 août, que le commentaire de
   `application_controller.rb` impute à `stored_location_for`.
2. `acces_verification#creer` fait pareil — sans conséquence, mais c'est le même trou.

**Deux propositions, à toi de trancher :**
- les trois `sign_in` passent par `onboarding_path` quand `introduction_a_voir?` est vrai — la
  surface reste étroite, et `/jeu` n'est pas touchée (l'objection des 22 bancs tient toujours) ;
- le mode `zero` écrit en sortie : « la session ouverte survit à la remise à zéro — se déconnecter
  ou passer en fenêtre privée pour revoir l'introduction ».

**Et un défaut de MON côté, signalé pour mémoire** : le CTA « Entrer dans le Jeu » de l'écran 3
vise encore `accueil_jeu_path` au lieu de `sortie_onboarding_path` (mon lot 5, jamais livré). La
destination mémorisée d'un visiteur du Sas n'est donc pas consommée là où ton commentaire l'attend.
`verifier_sas_vers_le_jeu` interroge la route directement : il reste vert pendant que le bouton va
ailleurs. Je le corrige au feu vert de Boris — ça déplace la sortie vers la première expérience.

— poste fixe

**Suite, même jour — #205 est ouverte** (`sortie-onboarding`, base `preprod`, indépendante de #204) :
elle corrige le CTA de l'écran 3, qui visait `/jeu` au lieu de `/onboarding/sortie`, et ajoute au
banc de l'onboarding l'assertion qui manquait — sur le HTML servi, le lien suivi jusqu'à la première
expérience. Mesuré sur la préprod : `/onboarding/sortie` mène à
`/excursion/ouvrir/point-zero-monde-0/faconner-mon-jumeau/1`, puis `/immateria`. À rejouer :
`verifier_onboarding`, `verifier_sas_vers_le_jeu`.

---

## 12 septembre — Poste fixe : `lint` est rouge sur `preprod` même, et il te reste deux caractères

Dix offenses RuboCop, quatre fichiers. **Aucune PR ne peut être verte tant qu'elles sont là** :
#204, #205 et #206 héritent toutes du rouge de la base. Un rouge permanent ne signale plus rien.

- `app/helpers/composants_helper.rb` (5) et `app/helpers/navigation_helper.rb` (3) : **de moi**,
  posées le 10 septembre par la roue des Puissances et par la pastille. **Corrigées en #206**
  (`alignements-helpers`) — `git diff -w` est vide, c'est de l'indentation seule, et les deux
  heredocs `<<~` gardent leur indentation relative, donc la chaîne rendue est identique.
- `app/services/excursion.rb:48` : `Style/TrailingCommaInHashLiteral`, virgule après le dernier
  élément du hash.
- `app/controllers/challenges_users_controller.rb:46` : `Layout/EmptyLinesAroundClassBody`, ligne
  vide en fin de classe.

Ces deux-là sont dans ta zone et je n'y touche pas. Avec elles, `lint` redevient vert et la case
recommence à vouloir dire quelque chose.

**Trois PR ouvertes, dans cet ordre de fusion** : #203 (la tienne, avec la ligne pour la vidéo
d'E2), puis **#204** (la fiche), puis **#205** (le CTA de l'onboarding) et **#206** (les
alignements), indépendantes l'une de l'autre et de #204.

— poste fixe
