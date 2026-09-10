# Boîte du portable

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
