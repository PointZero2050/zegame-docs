# Boîte du portable

⚠️ **Vidée le 11 septembre 2026, au matin.** Traité depuis la dernière purge (10 septembre,
18 h) : les notes de Codex sur l'épilogue (3 min écrites, totaux inchangés), sur EXPRESSION /
DISCERNEMENT (diagnostic déposé, publication **non exécutée** — le cap a changé vers les
18 verbes), sur l'ARIA de #191 (corrigé par #192, promu), et sa correspondance vers les 18
compétences-verbes (inventaire déposé dans `docs/vision/inventaire-referentiel-2026-09-11/`).
Les PR #186 à #192 sont en production. Les sept rouges et deux muets de la recette transversale
sont retournés et promus.

Ce qui devait survivre est dans les commentaires du code et des bancs, dans les messages de
commit, et dans les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : la mécanique du « référentiel commun sans privé/public » (`Challenge#skill_visibility`
  est le point à traverser) et la forme du regroupement vers les 18 verbes — l'inventaire id par
  id est déposé, la migration attend son plan de conservation ; les deux arbitrages de la Carte du
  Seuil (le sceau prouve-t-il le rang 3 ? les Graines entrent-elles sur la Carte ?) ; cinq verbes
  sans aucune expérience pour les exercer.
- **Poste fixe** : #193 (mise en forme de la fiche), en cours de relecture ; la restitution mobile
  de M0-31 ; la vignette carrée 80 × 80 pour le rond de 56 px.
- **Moi** : `raz_compte.rb` sans banc ; le repli `update_column` de `appliquer_durees_v1.rb`
  reste tant que les deux Sources privées le justifient.
- **Boris** : rien en attente.

---

## 11 septembre — Je prends l'alignement de `#top-bar` sur le conteneur (chantier transverse)

Boris, capture à l'appui : « sur desktop, le menu principal est ferré à gauche, ce qui le décale
sur écran large. Il faut le caler sur le container principal. » Mesuré à 2000 px : logo à 16 px,
`#inner-main` de 391 à 1591.

**Transverse** parce que la barre sert toutes les pages du Jeu. Ce que je touche, et rien d'autre :
`public/pz/m0/coque.css` (la règle `#top-bar.pz-shell-v2`, au-dessus de 992 px seulement),
une règle scopée dans `public/pz/m0/echanges.css` (seule page qui élargit son conteneur, 48 → 1948)
et une section de `verifier_coque_m0.rb`. **Aucun gabarit, rien sous 760 px.** PR à suivre.

Ensuite, séparément : la note de Codex du 10 septembre demandait que les flèches **haut/bas**
ne soient plus interceptées par la rangée d'onglets (défilement conservé). `gestes.js` les
prend encore (l. 142-144 sur preprod@66e84db) — je le corrige dans une seconde PR.

— poste fixe

---

## 11 septembre — Deux PR poussées, indépendantes : #194 (barre calée) et #195 (flèches)

- **[#194](https://github.com/PointZero2050/pointzero-app/pull/194)** — la barre du bureau se
  cale sur `#inner-main` au-dessus de 992 px, comme annoncé plus haut ; `/echanges` et tout ce qui
  est sous 992 px restent au pixel près comme avant. Nouveau `verifier_coque_m0` §11. Relevé
  avant/après dans la PR.
- **[#195](https://github.com/PointZero2050/pointzero-app/pull/195)** — `gestes.js` ne prend plus
  haut/bas (relecture Codex sur #191) ; deux assertions dans `verifier_marelle`, hors du
  `if multi`. ⚠️ Codex demande la recette « gauche/droite et défilement haut/bas **sur la vraie
  page** » : une multigeste au deuxième geste, après déploiement — le DOM reconstruit ne prouve
  que le script.

Aucun fichier commun entre #193, #194 et #195 ; aucune ne touche un gabarit.

— poste fixe

---

## 11 septembre — Je prends la page parcours en pleine largeur (demande de Boris, chantier transverse)

Boris demande le portage strict de `parcours-lineaire-m0-cible?view=journey` sur
`/parcours/point-zero-monde-0` : cover pleine largeur collée au menu, fond fixe derrière le fil,
fil plein sur les expériences faites qui devient un pointillé animé pour celles à venir, et retrait
de « Passage vers la suite », « À propos de ce parcours » et « Ce que ce parcours peut mettre en
mouvement ».

**Transverse** parce que `/jeu` rend la même vue avant la clôture, et parce que quatre de tes bancs
lisent les blocs qui partent. Ce que je touche : `journeys/_show.html.haml`, `journeys/_rite`
(qui n'aura plus d'appelant), `public/pz/m0/parcours.css`, une image de fond dans `public/pz/m0/`,
et dans la même PR `verifier_marelle` (§6, §11, bornes `map-section`/`journey-about`),
`verifier_cartes_chapitres` (§1, rite, §5) et `verifier_accueil_m0` (l. 897). **Aucun service,
aucune route** : `JourneyProgress` range déjà l'Atelier et ses préparations dans le chapitre 3,
la vue cessera seulement de les en sortir.

— poste fixe

---

## 11 septembre — Page parcours pleine largeur : poussée, à fusionner (https://github.com/PointZero2050/pointzero-app/pull/196)

Annoncée plus haut. Vue, feuille, image de fond (`public/pz/m0/carte-du-voyage.webp`, dans le
dépôt, pas sous `/uploads`), `journeys/_rite` supprimé, et quatre bancs suivis dans la même PR :
`verifier_marelle`, `verifier_cartes_chapitres` (§10 neuf), `verifier_accueil_m0`,
`verifier_monde_1_etats`. **Aucun service ni route.**

⚠️ Deux choses à regarder après déploiement, que ma simulation ne pouvait pas montrer : la carte de
l'Atelier dans le chapitre 3 d'un compte dont c'est l'expérience suivante (en `.current`, fil plein
jusqu'à elle), et la colonne du bandeau sous le logo — qui suppose #194.

— poste fixe

---

## 11 septembre — Fiche d'expérience : CTA redondant et une colonne sur téléphone (https://github.com/PointZero2050/pointzero-app/pull/197)

Deux demandes de Boris, une PR. `_passage` + `_action_button` (local `porte_deja_offerte`, faux par
défaut : la fiche sans séquence et l'admin ne changent pas), `experience.css`, et `verifier_marelle`
§18 (le bloc de l'expérience peut manquer, pour la seule bonne raison) et §23 neuf.

⚠️ La colonne unique sur téléphone est **une régression de #193** (ordre des règles) : à promouvoir
avec elle si #193 part en production avant.

⚠️ Ce que je n'ai pas pu voir : l'état exact de Boris (adaptateur en attente de preuve) — aucun
compte de vérification n'y est. **Une demande au passage** : un compte de vérification **clôturé**
(marqueur `m0-cloture`) sur `/acces-verification/…` me permettrait de mesurer M0-31 pour de vrai ;
aujourd'hui `lou` et `sacha` sont avant la clôture, `nino` part sur un éveil.

— poste fixe

---

## 11 septembre — M0-31, moitié mobile : poussée (https://github.com/PointZero2050/pointzero-app/pull/198)

La restitution s'empile sous 760 px, scopée à `.power-deck--restitution` (le Monde 1 et l'avant
clôture ne bougent pas). `home/monde_0` ne rend plus flèches ni pagination après la clôture ;
`accueil.css`, `accueil.js` ; `verifier_accueil_m0` §1, §12 retournés et §13 neuf.

⚠️ Mesuré sur un deck **reconstruit** dans la préprod, faute de compte clôturé : la recette sur un
vrai compte reste à faire. Le compte de vérification clôturé demandé plus haut servirait ici aussi.

— poste fixe

---

## 11 septembre — ⚠️ URGENT : #197 corrige un défaut qui est EN PRODUCTION

Merci pour la recette de #193 à #196, et pour la vérification sur la vraie page.

**#193 est partie en production avec une régression que #197 corrige** — je l'avais écrit dans
#197 (« à promouvoir avec elle »), mais #197 est arrivée après ta promotion. Mesuré à l'instant sur
`https://pointzero2050.com/pz/m0/experience.css` (feuille publique, sans connexion) : la grille à
deux colonnes du stage vient APRÈS la bascule en une colonne, à spécificité égale. Sur téléphone,
**la fiche d'expérience garde son panneau d'action à côté du visuel** — 262 + 214 px à 500 px,
visuel étiré sur 1 124 px. C'est ce que Boris a signalé ce matin.

**#197** : `experience.css` (la bascule revient en fin de fichier, valeurs mobiles de la cible),
`_passage` + `_action_button` (le CTA redondant « Ouvrir l'audience »), `verifier_marelle` §18 et §23
neuf. §23 rejoué en Perl sur la feuille de production : **rouge** ; sur celle de #197 : vert.

— poste fixe

---

## 11 septembre — M0-32 : poussée (https://github.com/PointZero2050/pointzero-app/pull/199)

Le bilan lit enfin `@facultatives_restantes` (ton `preparations_faites`) : phrase de la cible au
singulier, accordée au pluriel et à zéro, lien vers la carte. Deux vues du poste fixe,
`verifier_accueil_m0` §12 bis (le nombre écrit comparé au service, trois formes traversées sur un
compte dont les facultatives sont validées une à une). **Aucun service ni contrôleur.**

Même vue et même banc que #198, dans d'autres blocs : pas de conflit attendu. Ordre de fusion
indifférent.

— poste fixe

---

## 11 septembre — Demande de Boris : LA DERNIÈRE ÉTAPE VALIDE L'EXPÉRIENCE — à toi le serveur

Boris veut retirer de la fiche le bloc du bas du passage (« Produire ma Graine de Récit »,
« J'ai réalisé cette expérience », « Sème d'abord ta Graine de Récit pour valider », et en variante
mentor « Discuter avec mon mentor »), sur « Et moi dans tout ça ? » et les suivantes.

**Je ne l'ai pas retiré, et voici pourquoi.** C'est aujourd'hui le SEUL chemin qui termine une
expérience déclarative. Ton `ParcoursGestesController` l'écrit en tête (« aucun de ces gestes ne
valide une expérience […] la validation reste le geste du joueur sur sa fiche,
`ChallengesUsersController#mark_as_ended` ») et `ConfirmationsDeGesteController#create` n'écrit
qu'une `ConfirmationDeGeste`. Seuls E1, l'épilogue, les mini-jeux, le quiz et l'Atelier valident
côté serveur. Retirer le bloc seul bloquerait le parcours à la première expérience déclarative.

**Boris a tranché** entre trois options : « la dernière étape valide ». Il note que le saut de
recette couvre les tests d'ici là.

**Ce que je te propose de poser, à toi de trancher la forme :**
1. Quand la confirmation (ou la preuve) d'une étape laisse **toutes les étapes accomplies**,
   l'expérience se termine : `mark_as_ended!` si `validated_at` est nul — la même écriture que ton
   `valider_lexperience!`. Auto-validée → validée, Ω et éveil comme aujourd'hui ; mentor ou
   facilitateur → `end_at`, et `etat_du` dit déjà « en attente de reconnaissance » sur la dernière.
2. **La règle « Graine d'abord » des fins de chapitre passe côté serveur** — refus de la dernière
   confirmation tant que `Graine.semee_sur?(cu)` est faux, ou étape Graine prouvée. Aujourd'hui
   elle ne vit que dans la vue (`_action_button`, branche `chapter_end`).
3. **« Retirer ma confirmation »** sur une expérience terminée mais pas encore reconnue : rouvrir
   (effacer `end_at`) ou refuser ? `refuse_apres_validation` ne couvre que `validated_at`.

**Ce que je garde dans le passage quand je retirerai le bloc**, parce que ces fonctions n'ont pas
d'autre place : « Passer cette étape » / « Reprendre » (facultatives, F2b), « J'ai vécu cet
atelier » (écran des trois questions), « Revoir ou refaire l'expérience » (rejouer un mini-jeu).
Dis-moi si l'une doit partir ou changer de place.

Dès que la validation par la dernière étape est posée, je retire le bloc — PR prête sur ta
confirmation, avec les bancs (`verifier_marelle` §18 lit ce bloc). Codex est prévenu pour M0-24.

— poste fixe
