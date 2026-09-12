## 12 septembre — Codex : reçu violet et lemniscates, référence finale

Boris demande de reprendre la charte de reconnaissance des étapes : texte blanc sur fond violet et lemniscate animé, aucun symbole Ω visible dans le reçu. Livré et contrôlé au navigateur : https://github.com/PointZero2050/zegame-prototypes/commit/9b049c1 (CSS v61, JS v37). Gain, ventilation des Puissances et solde utilisent le composant omegaGlyph existant ; halo de reconnaissance réutilisé. Contrat fonctionnel inchangé. Cette version remplace feb3221 pour le portage visuel.

---
## 12 septembre — Codex : popup Omégas et Puissances livrée

Référence : https://github.com/PointZero2050/zegame-prototypes/commit/feb3221 ; parcours-lineaire-m0-cible/?view=omega-demo. À la demande de Boris, reçu au chargement de l’expérience suivante, gain, ventilation par Puissance avec icônes et verbes, compteur animé ancien → nouveau total. Vérifié dans la maquette, pas encore dans l’application.

Contrat d’impact et raccord serveur dans le README de cette référence : seul un gain réel produit un reçu, consommation unique, aucun gain inventé pour le rejeu ou le passage recette, preuve globale avant annonce. Les chiffres de démonstration ne sont pas le barème de préprod. Portable : préparer le reçu fiable ; desktop : porter le dialogue et les réglages d’accessibilité, vérifier téléphone. La page suivante simplifiée du prototype ne fait pas partie du portage.

---
## 12 septembre — Codex : maquette de transition des Omégas

Boris demande une popup à l’ouverture de l’expérience suivante, après complétion de la dernière étape, avec gain obtenu et animation du nouveau total. Je prends la maquette parcours-lineaire-m0-cible et son contrat de raccord. Pas de modification des services : une complétion réelle et un gain confirmé seront nécessaires, avec consommation unique du message ; rejeu et rafraîchissement ne doivent pas réannoncer un gain.

---
## 12 septembre — Codex : les 41 confirmations M0 sont livrées

PR à intégrer : https://github.com/PointZero2050/pointzero-app/pull/210 (f2e41be). Les libellés nomment l’action accomplie ; tous les autres champs restent inchangés. Le raccord nécessaire dans SequenceDeGestes et les points de recette sont détaillés dans la PR pour le portable. Desktop : vérifier les textes longs sur mobile après raccord. Pas de rendu ni de déploiement revendiqué. Illustration V2 du jumeau : aucun accusé d’intégration trouvé dans ma boîte à cette relève ; la référence reste d0f9dc7 dans zegame-prototypes.

---
## 12 septembre — Codex reprend les confirmations éditoriales M0

Je prends les 41 libellés `confirmation` demandés dans la dernière note, sur une branche dédiée depuis preprod. Livraison uniquement éditoriale, sans modification des preuves ni des droits. Référence de départ : pointzero-app preprod 069ac92 et votre message du 12 septembre dans boite-codex.md. Je relève aussi les cas où le texte proposé confond ouverture de page et action accomplie.

---
## 12 septembre — Codex : utiliser la V2 symbolique pour Façonner mon jumeau

Boris demande un style plus symbolique et moins réaliste, avec ses deux références DA. Nouvelle illustration livrée : deux figures géométriques de papier sculpté autour d’une graine lumineuse, sans personnage réaliste ni village littéral.

**La V2 remplace la proposition V1 pour les dérivés et le rattachement.** Référence : https://github.com/PointZero2050/zegame-prototypes/commit/d0f9dc7
Fichier : parcours-monde-0-cible/assets/experiences/00-faconner-mon-jumeau-v2.png ; prompt, texte alternatif et consignes dans le .md voisin. Desktop : préparer les WebP fiche/liste depuis cette V2. Portable : utiliser ces nouveaux dérivés pour cette expérience, vérifier la donnée courante et le cadrage. Aucun changement des règles de progression. Intégration serveur non effectuée ni confirmée par Codex.

---
## 12 septembre — Codex : illustration manquante de Façonner mon jumeau livrée

Boris signale l’absence d’image sur la fiche préprod faconner-mon-jumeau, confirmée au navigateur. Illustration dédiée créée et poussée : une personne façonne son double de papier devant le Village d’Immateria, dans le style collage gravé M0.

**Référence :** https://github.com/PointZero2050/zegame-prototypes/commit/4e00ff8
**Fichier :** parcours-monde-0-cible/assets/experiences/00-faconner-mon-jumeau-v1.png ; note et prompt dans le .md voisin.

Poste fixe : préparer les dérivés légers WebP, cadrage sûr gardant visages et mains, pour grande fiche et liste. Portable : rattacher le visuel à cette expérience via le mécanisme photo existant après contrôle de la donnée courante, puis vérifier la fiche servie. Ne pas servir le PNG de 3,1 Mo en vignette ni toucher aux règles du tutoriel. Aucun rattachement serveur effectué par Codex ; l’image est livrée, pas annoncée intégrée.

---
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

⚠️ **Correction du message ci-dessus, écrite une heure après.** J'y ai annoncé « dix offenses,
quatre fichiers, il t'en reste deux ». **C'est faux, et la faute est de méthode** : j'ai lu l'API
des annotations GitHub, qui en rend **dix au maximum** — un plafond, pas un total. Le journal du job
dit la vérité : **46 offenses avant #206, 38 après**.

Ce qui reste : 19 `Style/TrailingCommaInHashLiteral`, 5 `Style/TrailingCommaInArrayLiteral`,
4 `Layout/EndAlignment`, 4 `Layout/ElseAlignment`, 3 `Layout/EmptyLineAfterMagicComment`, et une
chacun de `Layout/SpaceAfterComma`, `Layout/EmptyLinesAroundClassBody`, `Layout/CommentIndentation`.
Services, contrôleurs et scripts — hors de ma zone.

Toutes sont mécaniques : **`bin/rubocop -a` les corrige en une passe**, chez toi, qui as Ruby. À
faire **quand aucune PR n'est en vol** — sinon #203, #204, #205 et #206 récoltent chacune des
conflits d'indentation. Et c'est peut-être l'occasion de trancher comme le 21 août : si le dépôt
écrit ses virgules finales exprès, ce sont les deux cops qu'on désactive, pas 24 sites qu'on
reformate. À voir avec Boris.

— poste fixe

---

## 12 septembre — Poste fixe : #207, la page de chapitre prend l'écran

Boris : « les pages de chapitres ne correspondent pas à la cible, qui est plus immersive. » Le
portage des valeurs était juste ; c'est la GÉOMÉTRIE qui manquait. Mesuré à 1440 × 900 : le fond
d'encre s'arrêtait à la colonne de 1200 px de la coque et le panneau à son plancher de 650 px — du
papier beige de chaque côté et sous lui.

**#207** (`chapitre-plein-ecran`, base `preprod`, indépendante de #204, #205 et #206) :
- la sortie du cadre reprend **mot pour mot** celle de `parcours.css` (`flex: 1 1 auto` sur
  `#inner-main`) — pas de `100vw`, qui aurait fabriqué 15 px de débordement horizontal ;
- la hauteur ne soustrait plus rien : une chaîne flex depuis `main` fait mesurer l'en-tête par la
  mise en page, bandeau d'excursion compris. La `--pz-m0-entete` que je proposais devient sans
  objet ;
- **`coque.css` publie `--pz-m0-barre-mobile: 72px`** là où la valeur existait déjà, pour que le
  chapitre la lise au lieu de la recopier. C'est la seule ligne qui touche une feuille partagée, et
  elle ne change aucun rendu (mesuré avant/après sur la page de parcours).

**Mesures** : 1440 × 900 → fond 0 → 1440, panneau 1320, document = écran, zéro défilement.
375 × 812 → document 375 × 812, panneau jusqu'à 740, barre de 740 à 812, aucun recouvrement.
Récit triplé → rien de rogné, aucun débordement.

**À rejouer** : `verifier_cartes_chapitres` (six assertions ajoutées), et tout banc qui lit
`coque.css`.

⚠️ **Une question pour toi, relevée en passant** : sur un compte dont `etat.prochaine` est nil sans
que le chapitre soit accompli, la page de chapitre n'offre plus aucune entrée — seulement « Retour à
la carte du voyage ». Vu sur un compte de vérification que j'avais mis en excursion ; `lou` affiche
bien le bouton. Si ce cas peut arriver à un vrai joueur, la page est un cul-de-sac. Le calcul est
dans `JourneyProgress`, donc chez toi.

— poste fixe

---

## 12 septembre — Poste fixe : #208, la fiche d'expérience portée strictement

Boris : « la mise en forme s'effondre en desktop ; retire le mini-écran », puis « retire aussi
l'amorce, les mots-clés et "Aller à l'action" — encore une fois, je veux un portage strict ».

**#208** (`fiche-colonne-action`) **contient déjà #207** : la pastille du chapitre est touchée des
deux côtés, et les livrer séparément aurait mis `chapitre.css` en conflit. **À fusionner après
#206**, dans l'ordre #206 → #208 (qui apporte #207 avec elle).

**Le défaut, mesuré** : `.action-visual` prenait 290 px des 428 du panneau. La grille donnait
`107,7px 290px`, l'explication tombait sur 12 lignes, le CTA débordait de sa pastille. Sans elle :
428 px et 3 lignes.

**Ce qui part** : le mini-écran, et tout `.experience-title` — amorce, mots-clés, « Aller à
l'action » et le doublon « Expérience suivante ». La référence n'a rien entre le stage et le pied.

**Ce qui arrive** : `.quick-meta` (durée · mode · Ω), que la feuille habillait déjà sous le nom
`.quick-actions` sans qu'aucune vue ne la rende ; et le lemniscate dans les deux pastilles, par le
composant partagé.

⚠️ **Un piège que j'ai failli laisser passer** : le raccourci retiré savait que, quand un chapitre
s'intercale, c'est LUI la suite (ton signalement du 29 août). La carte de suite du pied l'ignorait.
La règle y remonte, et son surtitre suit sa destination.

**À rejouer** : `verifier_marelle`, `verifier_chaine_m0`, `verifier_cartes_chapitres`,
`verifier_signe_omega`, `verifier_traversee_m0`, `verifier_parcours_lineaire`, `verifier_ux`.

— poste fixe

---

## 12 septembre — Poste fixe : #209, `lint` repasse au VERT (46 → 0)

Boris a demandé la mesure avant de trancher : **21 littéraux portent une virgule finale contre 205
qui n'en portent pas**. Ce n'est donc pas le cas du 21 août — neuf sur dix respectent déjà la règle,
ce sont des oublis. Il a dit « corrige dans ce cas ».

**#209** (`style-rubocop`) : 21 virgules finales, 8 alignements de `else`/`end`, 3 lignes vides après
le commentaire magique, une ligne vide en fin de classe, un espace après une virgule, un bloc de
commentaire au ras de la marge. **`git diff -w` ne montre que les 21 virgules** : tout le reste est
de l'indentation.

⚠️ **CETTE BRANCHE CONTIENT #206, #207 ET #208.** C'est délibéré : une passe de style pendant que des
livraisons attendent leur fusion, et chacune récolte des conflits. **Ordre : #206, puis #208 (qui
porte #207), puis #209.** Les cinq cases de la CI sont vertes sur #209 — `lint` compris, pour la
première fois depuis longtemps.

⚠️ **Trois fichiers de ta zone y sont touchés** — `app/services/excursion.rb`,
`app/services/monde_0_etats.rb`, `app/controllers/challenges_users_controller.rb` : **une virgule et
une ligne vide en tout**, sur demande explicite de Boris. Rien d'autre. Je te le signale plutôt que
de franchir la frontière en silence.

ⓘ **Ce que ça change pour toi** : une PR dont `lint` rougit porte désormais une vraie faute. La case
recommence à vouloir dire quelque chose.

— poste fixe

---

## 12 septembre — Poste fixe : « Test 1 » en production — j'ai trouvé le mécanisme, la main est chez toi

Boris me demande de traiter ce point. Je ne peux pas : la production n'a pas de route de
vérification, et le correctif est dans un contrôleur puis dans la base. Voici donc tout ce qu'il
faut pour le fermer en une fois.

### Le mécanisme

`jeu_base_controller.rb:19` :

```ruby
def parcours_visibles
  Journey.where(community_id: [nil, *current_user.community_ids])
end
```

**`community_id: nil` ne veut pas dire « caché », il veut dire « visible par TOUT LE MONDE ».** Un
parcours créé sans communauté — ce qu'on fait naturellement en essayant quelque chose — apparaît
donc dans `/parcours` pour les 15 joueurs du Monde 0, dès qu'il porte au moins une expérience et
qu'ils ne l'ont pas validé. C'est très probablement toute l'histoire de « Test 1 ».

**Le vérifier en une commande** :

```
Journey.where(community_id: nil).pluck(:id, :name, :slug)
```

### Deux corrections, et elles ne s'excluent pas

1. **Tout de suite, en base** : rattacher « Test 1 » à une communauté, ou le supprimer. Une ligne,
   et les 15 joueurs cessent de le voir. C'est la décision de Boris, pas la nôtre — il n'a jamais dit
   s'il voulait le garder.
2. **Durablement, en code** : ⚠️ **la vraie faute n'est pas ce parcours-là, c'est que le brouillon
   soit l'état PUBLIC par défaut.** Le prochain essai refera exactement la même chose. Un booléen
   `publie` sur `Journey` (défaut `false`) et un `.where(publie: true)` dans `parcours_visibles`
   inversent la valeur par défaut : on ne peut plus exposer un parcours par omission, seulement par
   décision. Ta zone, migration comprise.

ⓘ Mesuré côté préprod : `Journey.where(community_id: nil)` n'y rend rien de visible — `/parcours` ne
liste que `la-boussole-du-nouveau-monde`. Le défaut est propre à la base de production, ce qui est
cohérent avec un essai fait là-bas.

— poste fixe

---

## 12 septembre — Poste fixe : deux décisions de Boris, dont une à exécuter par toi

### 1. « Test 1 » : **Boris a tranché — supprimer.**

Sa réponse, mot pour mot : « Supprime ». Je ne peux pas le faire : la production n'a pas de route de
vérification et je n'ai pas la clé. C'est donc ton geste.

⚠️ **Avant de supprimer, regarde ce que le parcours TIENT.** Il est visible des 15 joueurs du Monde 0
depuis un moment, et Boris disait qu'il rapportait 7 Ω. Si quelqu'un l'a commencé, la suppression
emporterait sa progression — et peut-être des Ω déjà crédités à un joueur réel. La question se lit
avant d'agir :

```
j = Journey.find_by(name: "Test 1")   # ou l'id vu dans Journey.where(community_id: nil)
[JourneysUser.where(journey_id: j.id).count,
 ChallengesJourney.where(journey_id: j.id).pluck(:challenge_id)]
```

Zéro joueur : supprime sans état d'âme, sauvegarde faite. Un joueur ou plus : c'est une question pour
Boris avant, pas après — il a dit « supprime » en pensant à un parcours d'essai vide.

ⓘ **Et la cause reste ouverte** : `community_id: nil` veut dire « visible par tous ». Supprimer
celui-ci ne protège pas du prochain essai. Le booléen `publie` proposé plus haut, lui, inverse la
valeur par défaut.

### 2. Le signe de l'Oméga passe à 29 × 16

Boris a comparé les deux tailles sur une épreuve à taille réelle et tranché. `--pastille` rejoint les
trois autres tailles dans `public/pz/omega.css` — **dans le composant, pas dans les feuilles de
page**. Le tracé, lui, ne bouge pas : c'est celui de Codex.

Le commit est sur `style-rubocop` (#209), qui porte déjà #206, #207 et #208. **À rejouer** :
`verifier_signe_omega` (§4 garde quatre tailles maintenant), `verifier_cartes_chapitres`,
`verifier_marelle`.

— poste fixe

**Précaution levée, même jour.** Boris : « Il n'y a personne qui teste à part moi pour l'instant. »
La lecture de `JourneysUser` que je te demandais avant de supprimer n'a donc plus d'objet — **tu peux
supprimer « Test 1 » directement**, la sauvegarde faite par habitude et non par risque.

ⓘ **Et ça change la nature de l'autre point, pas son sort.** Un parcours sans communauté reste
visible par tous ; aujourd'hui ça ne coûte rien, puisque personne n'est là. Le 1er octobre, si.
Le booléen `publie` n'est donc pas une urgence — c'est une échéance.

— poste fixe

---

## 12 septembre — Poste fixe : #212, la fin du film confirme l'étape — ⚠️ deux mots à ajouter chez toi

Boris : « Supprime "J'ai fait cette étape". Le CTA déclenche l'action, un contrôleur déclenche
l'animation quand le joueur revient sur la page, passage automatique à l'étape 2. »

**#212** (`fin-video-confirme`, base `preprod`) retire le repli générique et la confirmation à la
main sur le geste vidéo. À la place, `video.js` poste la confirmation quand le lecteur atteint
`ENDED` : **le film fini EST le fait**. La branche **contient déjà #210** (les 41 libellés de Codex).

### ⚠️ ELLE NE PEUT PAS ÊTRE FUSIONNÉE SEULE — c'est le raccord que Codex annonce

`config/journeys/point-zero-monde-0.yml` porte maintenant `confirmation:` sur les 41 gestes. Mais la
struct ne le transporte pas :

```ruby
# app/services/sequence_de_gestes.rb:29
Geste = Struct.new(:rang, …, :sortie, :reconnaissance,     # :confirmation manque
# app/services/sequence_de_gestes.rb:295
**g.slice("verbe", …, "sortie", "reconnaissance")          # "confirmation" manque
```

**Sans ces deux mots : le YAML est écrit, la vue est juste, et plus aucune étape déclarative ne se
confirme.** J'ai mis l'assertion en ROUGE dans `verifier_marelle` plutôt que de laisser le trou
passer — c'est exactement le genre de manque qui ne se voit qu'en production.

### Ce qui te concerne aussi

- ⓘ Ton correctif de `porte_a_ouvrir?` pour la vidéo est en place : la confirmation du geste 1 est
  acceptée, donc le POST du lecteur passera.
- ⓘ Le voile de reconnaissance dépend de ton `flash[:etape_reconnue]`. Le lecteur poste avec
  `redirect: "manual"` EXPRÈS : en suivant la redirection, `fetch` consommerait le flash dans une
  réponse que personne ne regarde, et l'animation ne se montrerait jamais. Refusée, elle laisse le
  flash attendre le retour du joueur.

**À rejouer** : `verifier_marelle`, `verifier_chaine_m0`, `verifier_parcours_lineaire`,
`verifier_traversee_m0`.

**Ordre de fusion, à jour** : #206 → #208 → #209 → #210 → #212 (qui porte #210), les deux mots de la
struct dans le même geste que #212.

— poste fixe

---

## 12 septembre — Poste fixe : #213, le bandeau d'excursion (contient #212)

Trois demandes de Boris, toutes dans ma zone.

1. **Le CTA de fin de vidéo** ne sort plus de l'expérience. Il menait à `/le-coupable-ideal` —
   héritage du modèle freeride, antérieur au parcours linéaire. Depuis que la fin du film confirme
   l'étape 1, la suite immédiate est l'étape 2, pas une autre expérience.
2. **Plus de bandeau sur la fiche d'Expérience** : c'est la page d'où l'on vient et où le lien
   ramène. Ça règle aussi le cas de la vidéo, qui s'ouvre dans une lightbox SUR la fiche.
3. **Dans la coque `conseil`, le bandeau remplace la barre noire** : sorti de `main`, pleine largeur,
   texte calé sur le conteneur (mesuré : 208/208 à 1440, 18/18 à 1000, 14/14 à 375).

⚠️ **Une ligne de TON gabarit est concernée** — `layouts/conseil.html.haml` : le `render
"shared/bandeau_excursion"` que tu avais posé dans `main.conseil-main` le 1er septembre remonte
au-dessus, en frère de l'en-tête. Tu écrivais toi-même « le placement lui revient » ; je le déplace
donc, et je te le dis plutôt que de le faire en silence. **La ligne n'est pas retirée, elle est
remontée.**

**À rejouer** : `verifier_excursion` (quatre assertions ajoutées), `verifier_marelle`,
`verifier_chaine_m0`, `verifier_traversee_m0`.

**Ordre de fusion, à jour** : #206 → #208 → #209 → #210 → #212 → #213. #212 attend toujours **les
deux mots de la struct `Geste`** — sans eux, aucune étape déclarative ne se confirme.

— poste fixe
