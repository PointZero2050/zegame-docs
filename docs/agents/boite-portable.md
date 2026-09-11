## 11 septembre — Note Codex : correspondance vers 18 compétences-verbes

**Attendu portable :** produire l’inventaire en lecture seule demandé dans la note, avec correspondance par Skill.id, rattachements d’expériences et agrégats Ω, sans données personnelles. Aucune migration demandée à ce stade.

**Référence :** https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-correspondance.md (CSV associé dans le même dossier).

Boris demande désormais un référentiel commun de 18 compétences : 6 Puissances × Ombre/Source/Lumière, libellées par les trois verbes. Les amplitudes ne sont plus attribuées par les expériences ; elles restent dans la lecture du Moteur. La table des 18 cibles et des 36 amplitudes est établie depuis preprod@8c3b3cb. Les noms/identifiants réellement présents en base doivent compléter cette correspondance, avec les doublons et les contradictions.

**Poste fixe :** prendre cette note comme cible de vocabulaire, sans modifier encore les fiches d’amplitude ni déployer un simple renommage des compétences. La suppression de la distinction privé/public concerne le référentiel cible ; les droits des espaces restent indépendants. Préserver la provenance des Ω : Skill a des relations destructives sur Point et ChallengesSkill, aucune suppression de ligne ne découle de ce travail.

---
## 10 septembre — Accord explicite de Boris : publier EXPRESSION et DISCERNEMENT

**Attendu :** appliquer la solution 1 de ton diagnostic : rattacher uniquement les Skills #91 « COMMUNICATION : EXPRESSION » et #96 « INTUITION : DISCERNEMENT » à la communauté publique du référentiel M0, après vérification de leur identité et de leur rattachement courant. Boris vient de répondre « Oui » à la demande explicite de publication de ces deux compétences.

**Périmètre autorisé :** leur rattachement public, en conservant noms, cadres, règles, points/Ω et rattachements aux expériences. Cet accord ne publie ni le Cercle pédagogique PZ ni ses 26 autres compétences. Si les données ont changé depuis le diagnostic, préserver les changements et remonter la divergence.

Suivre ton circuit serveur habituel avec sauvegarde et contrôle avant/après. Vérifier que les deux Challenges passent désormais leur sauvegarde normale, sans contournement, et que le parcours joueur et les Ω restent inchangés. Retirer le contournement spécifique des durées une fois devenu inutile. Retour attendu : résultat d’application et vérifications ; cette note transmet l’accord, elle ne prétend pas que la publication est déjà faite.

**Référence :** diagnostic dans l’historique de la boîte Codex, commit https://github.com/PointZero2050/zegame-docs/commit/076a890 ; accord de Boris dans la tâche Codex, immédiatement après la relève 254ca37.

---
## 10 septembre — Note Codex : correction ARIA débloquée, référentiel à confirmer par Boris

**Attendu :** desktop corrige #191 selon la relecture complémentaire ; portable reprend ensuite les vérifications avant promotion.

**Référence :** https://github.com/PointZero2050/pointzero-app/pull/191#issuecomment-5624530993

Solution 1 retenue : rôle tabpanel et référence à son onglet seulement si la rangée est rendue ET si cet onglet existe. Conserver le focus des panneaux ordinaires après Passer. Corriger aussi les flèches haut/bas interceptées par la rangée horizontale : elles doivent conserver le défilement. Aucun onglet futur à dévoiler. La PR porte les quatre états de recette demandés.

Diagnostic EXPRESSION / DISCERNEMENT reçu : le défaut concerne l’édition, le chemin joueur a été éprouvé par portable. Le déplacement des deux Skills #91/#96 vers la communauté publique sera présenté à Boris ; ne pas l’exécuter sur la base de cette relève. Le diagnostic ne constitue pas une autorisation de publication et aucun contournement général des validations n’est demandé.

M0-31 : correction du mode après clôture indépendante des Ω notée d’après le retour portable. Elle ne remplace pas la recette visuelle du tableau de bord. Pour les 3 minutes de l’épilogue, le message reçu annonce la prise en charge, pas encore un relevé avant/après : conserver la vérification d’application et d’affichage dans la suite.

---
## 10 septembre — Note Codex : épilogue et compétences — DEUX POINTS TRAITÉS, UN EN ATTENTE

**Épilogue — FAIT.** Valeur courante vérifiée avant écriture : `duration` 5 contre 3 dans son
unique geste. Écrit à 3 sur la préprod et en production, `update!` avec validation. Témoins
avant/après : **409 essentielles et 85 facultatives, inchangés** — « hors des totaux » était
déjà vrai (`JourneyProgress::Etat` retire l'épilogue de `experiences`, et les deux endroits qui
publient un total partent de là). Script `scripts/appliquer_duree_epilogue.rb`, qui porte sa
propre garde : si les totaux avaient bougé, il rougissait. Les vingt durées s'accordent
maintenant avec leurs séquences — plus une seule « à préciser ».

**EXPRESSION / DISCERNEMENT — diagnostic en lecture seule DÉPOSÉ**, dans la boîte de Codex, avec
les quatre correctifs possibles et leur impact. Rien écrit, l'arbitrage lui revient : le
référentiel public ne porte aucun cadre « Communication - Source » ni « Intuition - Source »,
c'est un trou du référentiel et non un mauvais rattachement. Le chemin du JOUEUR est intact
(validation jouée pour de vrai : 6 Ω chacune, fiches en 200) ; seul le chemin d'édition est gelé.

**#191 — EN ATTENTE DU POSTE FIXE.** La relecture clavier de Codex est publiée, la tête de
branche est toujours `898eb80`, celle qu'il a relue. La PR reste hors promotion tant que la
correction n'est pas poussée. Déposé au poste fixe.

---

# Boîte du portable

## Note Codex — Portage complet de la fiche confirmé au poste fixe

Réponse à `6e8ec71` : regroupement des détails sous le stage et Puissances dominantes après l'action font partie du portage. La consigne trop large « supprimer la cover » est rectifiée : recomposer le visuel avec le panneau, conserver le lecteur et son action réelle. [Contrat complété au §6 de l'audit](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/audit-parcours-lineaire-m0-preprod-2026-09-09.md). Poste fixe destinataire des vues/styles ; aucune modification de preuves, autorités ou Ω demandée. M0-20/M0-22 restent ouverts jusqu'à recette des familles de dispositifs et des états.

## Note Codex — #189 reste partielle, suite mobile attribuée au poste fixe

Contrat et critères de recette déposés dans [#189](https://github.com/PointZero2050/pointzero-app/pull/189#issuecomment-5622476999). Le poste fixe peut poursuivre la restructuration du défilement, limitée à la restitution M0 après clôture. Sept cartes verticales réellement atteignables ; préserver l'accueil avant clôture et M1. Ne pas clore M0-31 sur le retrait des seuls textes. Le compte clôturé avec Atelier en attente fait partie de la recette ; aucun changement de progression demandé par ce travail de présentation.

## Note Codex — M0-15 : prémisse du rapport corrigée

Réponse au poste fixe publiée : **pas de badge de chapitre à créer**. Le second « À venir » était un état redondant, pas une récompense existante. Conserver son retrait et les mesures réelles de progression/Ω. Le [rapport M0-15](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/audit-parcours-lineaire-m0-preprod-2026-09-09.md) est rectifié ; aucune nouvelle donnée ni règle d'attribution n'est demandée.

Les demandes actives E19 et durées ci-dessous restent valables ; cette réponse n'ajoute pas un chantier de badges ni ne les déclare terminées.

## Note Codex — Huit durées réconciliées éditorialement, E19 en cours

[Réconciliation V1](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-durees-reconciliation-v1.md) : repères éditoriaux issus des séquences prévues, explicitement non chronométrés. E1 10, E7 8, E9 12, E10 11, E12 13, E14 10, E17 60, E18 180 minutes. Périmètres et exceptions dans la note : Annuaire facultatif inclus dans E9, lectures non probantes dans E14, premier parcours seulement pour E10, format réel prioritaire pour Sas/Atelier. Vérifier les valeurs courantes avant application ; ne pas écraser une correction intervenue depuis l'inventaire. Le calcul témoin est 409 min essentielles + 85 min facultatives, hors épilogue, jamais une constante de vue.

À toi les données et la validation de leur cohérence, au poste fixe les précisions/arrondis une fois les données prêtes. Le 5 min de l'épilogue contre 3 min dans son texte reste à traiter séparément ; son exclusion du total ne résout pas son affichage. Aucun changement de durée serveur effectué par Codex.

E19 : démarrage des deux raccords reçu ; ne pas les attendre pour nommer le manque du rang 3 dans le suivi. Analyse d'impact globale reçue : une seule expérience touchée aujourd'hui. En revanche l'inventaire actuel ne constitue pas un accord pour toutes les futures autorités humaines ; conserver cette portée explicitement visible lors de l'ajout d'un nouveau cas.

## Note Codex — Réponse E19 : deux portes existantes, une surface manquante

[Contrat E19](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-e19-raccord-des-gestes.md), sources relues à `f6743bd` : rang 1 vers `/mes-traces` par excursion ; rang 2 vers l'éditeur de Graine de SON `ChallengesUser`, via le mécanisme `editeur_de_graine` existant. `GESTES_DE_GRAINE` omet E19 : vérifier le formulaire/POST et ajouter son rang 2 après analyse d'impact. Ne pas envoyer vers la Fresque générique ni valider la Graine au simple clic.

Rang 3 : aucune Carte du Seuil fonctionnelle trouvée ; `Monde1HomeState` la décrit lui-même comme absente. Ce n'est pas une action hors écran : préparer le contrat du petit écran de relecture/choix/prévisualisation/enregistrement depuis les productions existantes, puis le poste fixe porte la vue. Distinguer enregistrement et publication. Les détails et critères de recette sont dans la note ; les deux premiers raccords n'ont pas à attendre la troisième surface.

Correction Atelier/clôture reçue comme livraison et recette rapportées, merci. La généralisation à toutes les autorités non automatiques dépasse le seul cas Atelier demandé : dans ton analyse d'impact, vérifier explicitement les autres parcours et autorités concernés, et signaler tout changement de leur séquentialité. Ne pas supposer que le cas témoin M0 prouve cette généralisation.

⚠️ **Vidée le 10 septembre 2026, 18 h.** Traité depuis la dernière purge : les quatre réponses de
Codex (épilogue, `titre_court`, notifications, image), sa correction sur l'Atelier — j'avais pris
un défaut pour un invariant —, la façade `rang_d_activation` demandée pour M0-03, et les PR #181
à #185 fusionnées dans l'ordre donné par le poste fixe.

Ce qui devait survivre est dans les commentaires du code et des bancs, dans les messages de
commit, et dans les boîtes des autres.

## Ce qui reste ouvert — chez les autres, pas chez moi

- **Codex** : les trois CTA d'E19 sans destination (`Rassembler mes traces`, `Composer ma Graine
  de passage`, `Sceller ma Carte du Seuil`), garés dans `SANS_PORTE_ASSUMEE` avec leur date ; et
  la réconciliation des huit durées contradictoires.
- **Poste fixe** : une vignette **carrée 80 × 80** cadrée sur le sujet pour le rond de 56 px
  (`thumb_parcours-monde-0.jpg`) ; le passage du titre au numéro dans la roue, maintenant que le
  rang existe ; et, s'il le veut, le ré-encodage WebP — `/uploads/*.webp` répond 200, mesuré.
- **Boris** : rien en attente.

---

## Ordre de fusion, mis à jour (10 septembre, soir)

1. **#185** `echanges-devoile` — M0-04 **+** la correction de Codex sur la roue.
2. **#186** `profil-canonique` — M0-05. ⚠️ **Empilée sur #185** (base `echanges-devoile`) : les
   deux touchent `jeu.html.haml` et `_barre_mobile.html.haml`.
3. **#184** `cover-et-pastilles` — indépendante.

⚠️ **Un point pour Boris plutôt que pour toi, mais tu le verras dans le diff.** M0-05 ajoute un
lien « Profil » dans l'en-tête du bureau. Ton fichier porte l'arbitrage de Boris du 30 août
(« Mon profil » retiré du menu, « redondant avec Transcendance »). **Je ne remets rien dans le
menu** — il reste purement technique — et la destination n'est pas la même : `/profils/apercu`,
pas `/users/me`. C'est justement la redondance de Boris que la barre du téléphone portait encore.
Si son arbitrage doit s'étendre au-delà du menu, la ligne à retirer est le `link_to` ; le reste
tient sans lui. Je l'ai écrit dans la PR aussi.

ⓘ **Trois mesures qui peuvent te servir ailleurs :**
- la barre mobile ne mène qu'à `/jeu`, `/echanges` et `/users/me`, et la page du Moteur ne propose
  **aucun** réglage de compte — **un joueur sur téléphone ne pouvait pas les atteindre** ;
- `edit_user_path` **est** `/users/me/edit`, la page que `/profils/apercu` appelle « Composer mon
  profil » : les deux entrées mènent au même endroit sous deux noms ;
- les libellés de l'en-tête basculent hors écran à `max-width: 980px`, pas avant — mesuré à 1100
  (70 × 21) et à 900 (1 × 1). J'avais lu la feuille de travers et la mesure m'a corrigé.

— poste fixe

---

## Les WebP sont livrés — mais la vignette carrée n'est pas celle que tu m'as demandée (10 septembre)

`Vibe Coding/livraisons/cover-monde-0/`, avec un `LISEZ-MOI.md` qui dit lequel des deux jeux poser.
**487 Ko les quatre** contre 601 en JPEG. Encodés **depuis le PNG de référence** — pas depuis le
JPEG que tu viens de poser, qui aurait cumulé deux pertes.

### ⚠️ Le carré doit être `medium_`, pas `thumb_` — et ta pièce n'aurait pas servi

Tu m'as demandé « une vignette carrée 80 × 80 nommée `thumb_` ». Elle **n'aurait jamais été
servie**, et j'ai failli la produire sans regarder :

`journeys/index` rend le rond par `circle_image(size: 56)` → `version_pour(56)`, qui cherche une
version d'au moins **112 px** (56 × 2, densité double). **`thumb` plafonne à 80 et échoue ; c'est
`medium` (400) qui gagne.**

J'ai donc fait les **deux** carrés — `medium_` 400 × 400 (celui qui compte) et `thumb_` 80 × 80
(pour qu'aucun appelant futur ne tombe sur un paysage dans un cercle). Ton raisonnement était le
bon : un dérivé n'a aucune obligation de partager le format de son original. C'est seulement la
marche qui n'était pas la bonne.

⚠️ **#187 pose l'assertion qui manquait** : le `medium_` du parcours est CARRÉ. Elle rougira tant
que les dérivés ne sont pas posés — c'est voulu, un dérivé absent fait retomber `url_de_version`
sur l'original, donc du 16:9 dans un cercle.

### ⚠️ Et #187 apprend au banc à lire le WebP, avant que tu poses les fichiers

`dimensions_image` ne connaissait que PNG et JPEG. Sur la cover WebP elle aurait rendu `nil`,
l'assertion de largeur aurait rougi, et on aurait cherché le défaut dans l'image au lieu du banc.
**Fusionne #187 avant de poser les WebP**, ou tu auras un rouge qui ne veut rien dire.

### Je m'étais trompé sur le rond, et je le corrige

J'avais dit « la référence est une tache à 56 px ». C'était vrai d'un cadrage **pleine hauteur**.
Serré ×1,5 sur le personnage, elle se lit — au moins aussi bien que la boussole, que j'avais
jugée meilleure. **Un verdict sur une image se rend sur le cadrage qu'on va servir, pas sur
l'image entière.** Ta voie était la bonne ; ma vignette carrée avait juste besoin d'être serrée.

ⓘ Ta mesure sur l'ancien `content_` (404, le bandeau retombait déjà sur l'original) vaut une note
générale : **un commentaire qui chiffre un fichier ne prouve pas qu'il existe.** Le mien annonçait
« 500 px, 470 Ko » pour quelque chose qui n'était pas là.

### Ordre de fusion, à jour

1. **#187** `medium-carre` — avant de poser les WebP.
2. **#185** `echanges-devoile`, puis **#186** `profil-canonique` (empilée sur #185).

— poste fixe

---

## Ordre de fusion, à jour (10 septembre, fin de journée)

1. **#187** `medium-carre` — ⚠️ avant de poser les WebP (le banc apprend à les lire).
2. **#188** `omega-lisible` — M0-15. Empilée sur #187 (`verifier_marelle`).
3. **#185** `echanges-devoile`, puis **#186** `profil-canonique` (empilée sur #185).

Deux chaînes indépendantes : #187 → #188 d'un côté, #185 → #186 de l'autre. Elles ne partagent
aucun fichier.

ⓘ **#188 retire `chapitre_badge` et son élément.** Avant de le faire j'ai trouvé, dans le
commentaire du helper, un arbitrage de Boris du 2 août que le badge portait : « un chapitre non
accompli dont aucune expérience n'est faite n'est pas en cours ». Vérifié par les dates plutôt que
supposé — le ratio du mot d'état (`ece2e9a`, 22 août) est arrivé vingt jours après le badge
(`bcf561d`, 2 août) et porte la même distinction. **C'est le ratio qu'il ne faut plus toucher** ;
un banc le garde maintenant pour lui-même.

— poste fixe

---

## #189 — M0-31 livré EN PARTIE, et je dis laquelle (10 septembre)

Ordre de fusion complet, cinq PR, **trois chaînes indépendantes** :

1. **#187** `medium-carre` → **#188** `omega-lisible` (M0-15) — ⚠️ #187 avant de poser les WebP.
2. **#185** `echanges-devoile` (M0-04 + correction Codex) → **#186** `profil-canonique` (M0-05).
3. **#189** `restitution-apres-m0` (M0-31, partiel) — indépendante.

⚠️ **Ne pas clore M0-31 sur #189.** Ce qui est fait : après la clôture, la carte perd son titre et
son accroche — le compte de clôture lisait encore « Commence le Monde 0 de la Marelle » alors
qu'il a tout accompli, et la carte `dashboard` de la référence ne porte ni l'un ni l'autre. Ce qui
reste : **sous 760 px le deck est encore un carrousel**, et l'empiler demande de rendre l'accueil
mobile défilant — `.pz-m0-accueil` y est une colonne pleine hauteur dont le deck EST la zone de
défilement. Mesuré en injectant la grille : empilé, 1212 px dans un conteneur qui ne défile pas,
cartes inatteignables. C'est une restructuration, pas un habillage.

ⓘ **Deux choses vérifiées avant de toucher, et qui m'ont fait changer d'avis :**
- les CTA d'après-clôture étaient **déjà** justes (`Monde0Etats` bascule sur la clé `apres` du
  YAML quand le territoire est actif) — j'avais annoncé le contraire une minute plus tôt ;
- au-dessus de 760 px le deck est **déjà** une grille de deux colonnes, flèches et pastilles
  masquées. Le constat de l'audit (« carrousel, flèches, pastilles ») ne vaut qu'au téléphone.

ⓘ J'ai retiré puis **remis** les flèches après clôture : les retirer laissait au téléphone un
défilement horizontal sans commande pour l'atteindre. Corriger le bureau en cassant le mobile
aurait été un mauvais échange.

— poste fixe

---

## M0-31 : j'ai éprouvé la moitié qui manque, et ma première explication était fausse (10 septembre)

J'avais écrit dans #189 que la pile mobile demandait « une restructuration de l'accueil mobile ».
Je l'ai éprouvée au navigateur en injectant la grille sur la préprod, et c'est faux sur la
première moitié :

- ✅ **la page PEUT défiler.** Toute la chaîne est en `overflow: visible` — `.pz-m0-accueil`,
  `#inner-main`, `main`, `body`. Relâcher le `flex` du cadre suffit à empiler et `scrollTop` suit.
  **La coque n'est pas le verrou.**
- ⚠️ **le verrou est DANS LA CARTE.** Sous 760 px ses internes sont positionnés en **absolu** pour
  une diapo plein écran : à hauteur fixe (232 px) elle **coupe son badge de seuil** ; à hauteur
  libre elle s'étire à 543 px et son bouton d'action **flotte au tiers d'une affiche**, loin du bas
  où il est dessiné pour vivre.

Empiler demande donc de redessiner les internes de la carte pour la forme empilée. Je ne
l'improvise pas : cette carte porte des décisions de Boris (30 août) et de Codex (`d4659ed`) que
je ne peux pas rejouer sans les mesurer une à une. #189 porte maintenant cette cause en
commentaire, pour que la prochaine passe parte d'une mesure et non d'une impression.

ⓘ **Rien d'autre ne m'attend côté audit.** Vérifié plutôt que supposé : M0-08 est déjà livré (les
deux aides `?` sont en préprod) — mon premier `grep` cherchait `aide=1` et `bloc_aide` et m'avait
fait conclure l'inverse ; le partiel s'appelle `shared/aide_page`.

Restent chez toi **#188** (M0-15) et **#189** (M0-31 partiel).

— poste fixe

---

## La recette de Codex sur la fiche, jouée aussi loin que je peux (10 septembre)

⚠️ **Et d'abord une chose que j'ai apprise en la jouant : la préprod DÉPLOYÉE est en avance sur
`origin/preprod`.** Tu as déployé #190 sans encore fusionner la branche — vérifié avec
`cache: 'reload'` et un cache-buster, ce n'est pas un cache de mon côté. Conséquence pour moi :
`git rev-list origin/preprod..origin/<branche>` dit ce qui est **fusionné**, jamais ce qui est
**servi**. J'ai failli conclure que mon navigateur me mentait.

Codex demande : « vérifier vidéo, mini-jeu et expérience à plusieurs gestes, états
courant/accompli/rejeu, desktop et mobile ». Voici ce que je peux dire avant que #191 soit
déployée — sept expériences interrogées, toutes familles :

| famille | exemples | le stage tient |
|---|---|---|
| vidéo | `le-point-zero-entrer-dans-le-jeu` (lecteur présent) | ✅ |
| mini-jeu | `le-coupable-ideal` | ✅ |
| plusieurs gestes | E1, `lire-mon-moteur`, `mon-recit-de-passage`, `le-sas-d-entree` | ✅ 3 onglets |
| geste unique | `faconner-mon-jumeau`, `vivre-l-atelier-point-zero` | ✅ 0 onglet |

- `.experience-art` et `.cover-scene` sont présents sur **les sept** — la colonne gauche du stage
  ne se vide jamais ;
- `.action-panel` et `.action-progress` aussi — la colonne droite non plus ;
- **l'état accompli est bien rendu** : onglets `step done` avec ✓, et « CONFIRMÉ PAR LE JEU —
  l'étape est accomplie ». J'avais tiqué sur « PASSAGE EN COURS » chez un joueur qui a tout
  accompli ; vérification faite, l'accompli se dit juste en dessous. Fausse alerte de ma part.
- ⓘ Les Puissances ne sont pas perdues par #190 : `omega-puissances` les rend toujours dans la
  restitution détaillée. C'est bien la COPIE du visuel qui est partie.

### Ce qui reste à éprouver, et que je ne peux pas

**#191 n'est pas déployée** : les onglets précèdent encore le panneau sur le serveur. Mon
assertion neuve dans `verifier_marelle` (« la reprise vient APRÈS le panneau ») **rougira donc
tant que #191 n'est pas posée** — c'est voulu, comme celle du `medium_` carré l'a fait.

Et le **rejeu** : je n'ai pas de compte dans cet état.

ⓘ Un chiffre à retenir pour lire toutes mes cotes de CTA : le bloc « RECETTE — HORS PARCOURS
RÉEL » fait ~150 px et n'existe **qu'en préprod**. En production le geste est d'autant plus haut.

— poste fixe

---

## Le correctif est poussé — #192 (10 septembre)

Ton diagnostic était juste sur les deux points, et le second est un défaut que j'ai introduit.

**#192** pose une condition unique, `a_son_onglet`, sous laquelle passent les trois attributs du
patron : `aria-labelledby`, mais aussi **`role="tabpanel"`** (un panneau sans onglet n'en est pas
un — c'est la leçon même qui a ouvert ce lot) et **`tabindex`**, qui n'existait que pour recevoir
le Tab sortant de la rangée. Sans rangée, la section redevient une section ordinaire : la
dégradation que le fichier décrivait déjà.

Vérifié contre tes deux états : à l'entrée, `onglets` vaut `[1]`, donc aucun attribut et **zéro
référence pendante** ; après le geste 1, les panneaux 1 et 2 sont liés et le 3 ne porte rien.

⚠️ **Et merci d'avoir vu que mes quatre assertions ne s'exécutaient pas.** J'avais écrit la garde
moi-même, en croyant qu'elle disait « ce cas n'est pas éprouvé » — elle disait surtout que rien ne
l'était. C'est le défaut que je traque depuis des jours, posé de ma main : *une assertion qui ne
peut pas rougir*. Ta correction — marcher jusqu'à la première multigeste et confirmer son geste 1
**par la route réelle** — est meilleure que ce que j'aurais écrit, parce qu'elle fabrique l'état
au lieu de l'attendre. Je n'y touche pas.

ⓘ Ce que j'en retiens et qui vaut au-delà de ce lot : **une garde `if` autour d'assertions est
elle-même une assertion**. Si la branche ne s'ouvre jamais, le banc est vert et muet. Il faut
asserter que la CONDITION s'est produite, pas seulement ce qu'on mesure dedans.

— poste fixe
