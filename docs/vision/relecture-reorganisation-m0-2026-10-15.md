# Relecture de la reprise M0 / M1

> Note Codex — relève après transmission de la maquette. Lecture de `pointzero-app/preprod@3a366af5` et des messages partagés ; vérification du rendu local, pas une recette de production. Le cadrage produit reste la [réorganisation validée par Boris](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/reorganisation-m0-m1-2026-10-15.md).

## État retrouvé

- Le portage visuel du nouveau M0 et le pont des cinq jeux sont fusionnés dans la branche `preprod` (PR #381 / #382 / #383).
- Le lot de lecture fournit l’état et les écrans sous `/monde-zero`. `/jeu` conserve son aiguillage existant : ce n’est pas une bascule générale des joueurs vers le nouveau M0.
- La reprise technique vient des sources existantes : `TraceSas` pour les explorations, inscriptions confirmées pour la réservation, présence reconnue pour l’Atelier vécu.
- Le compteur est celui de la traversée M0, séparé du solde global du compte. La note de code distingue explicitement ce calcul d’affichage du crédit réel des points.
- La maquette d’origine est toujours sur [PR prototypes #2](https://github.com/PointZero2050/zegame-prototypes/pull/2), tête `fab05ec`.

Références de lecture : [contrôleur M0](https://github.com/PointZero2050/pointzero-app/blob/3a366af5/app/controllers/monde_zero_controller.rb), [état du M0](https://github.com/PointZero2050/pointzero-app/blob/3a366af5/app/services/etat_du_monde_zero.rb), [script de coque](https://github.com/PointZero2050/pointzero-app/blob/3a366af5/public/pz/m0/panorama.js).

## Défaut corrigé : retour de sauvegarde du profil

Le formulaire du nouveau M0 poste sur le contrôleur de profil partagé, sans indiquer de retour. Le contrôleur redirige alors vers l’ancien profil communautaire ou son édition, selon la complétude des champs communautaires. Cela fait sortir le joueur du nouveau M0.

Correctif de présentation uniquement : le formulaire envoie le chemin de profil fourni par la coque dans `params[:return_to]`, hors du scope `user`. Le contrôleur lit déjà ce paramètre et accepte les chemins internes relatifs.

- [PR #384](https://github.com/PointZero2050/pointzero-app/pull/384), branche `codex/m0-retour-profil-20261015`, commit `a8e7753`.
- Deux fichiers : partiel Profil et banc de rendu.
- Vérification du HTML réellement rendu par HAML : échec reproduit avant ajout du champ, puis passage après correction. `verifier_monde_zero_panorama` entièrement vert hors Rails et `git diff --check` vert.
- À rejouer après fusion en préproduction : prénom / présentation → enregistrement → retour à `/monde-zero/profil`.

Le correctif concerne la sauvegarde réussie. Le traitement d’une erreur de validation reste `render :edit` dans le contrôleur partagé ; il doit être adapté au contexte M0 côté aiguillage. Le message « profil communautaire pas encore composé » doit aussi être distingué du simple profil personnel de M0. Aucun modèle, contrôleur, route, droit ni crédit n’a été modifié par cette PR.

## Raccords encore ouverts dans la révision lue

| Sujet | État observé | Suite attendue |
|---|---|---|
| Réservation | Le CTA conduit à `/agenda#rendez-vous`, selon le lot de lecture | Brancher le formulaire de réservation dans la coque et le verrou serveur à 5/5 |
| Préparation privée | Le chemin de préparation conduit encore à la présentation de l’Atelier ; l’aperçu M1 reçoit une liste de réponses vide | Stocker le journaling privé, permettre sa reprise, restituer ses textes comme Trace en M1 |
| Participation et Omégas | L’état vécu et le total affiché sont calculés ; le service annonce que le crédit réel de +25 appartient au lot Atelier | Raccorder le crédit unique à la présence reconnue, sans le déclencher par réservation ou affichage |
| Bascule M0 / M1 | Le nouveau M0 est isolé sous `/monde-zero` | Terminer la migration et ses garde-fous avant d’aiguiller les joueurs ; conserver les acquis |
| Mini-jeux sous CSP réelle | Le pont et le rendu sont portés, le banc local passe | Recette navigateur des cinq jeux, import effectif, reçu, reprise et rejeu sans double crédit sur le serveur |

Cas de transition à expliciter : le service donne priorité à une présence reconnue, puis à une inscription confirmée, avant le compte des cinq explorations. Cela permet de représenter un compte déjà inscrit ou déjà venu à un Atelier avec moins de cinq nouvelles explorations. Il faut distinguer ce traitement des acquis antérieurs du verrou de réservation pour un nouveau joueur ; ne pas le résoudre en effaçant une inscription ou une présence existante.

## Anciennes demandes éditoriales relevées dans la boîte de Codex

Les messages des 7 et 14 octobre signalaient le Festival encore annoncé au présent, « EN DIRECT » figé, et la promesse d’envoi du lien la veille. Le compte rendu du poste fixe indique leur traitement par le portable dans `6bd19c3a` et `3562ed94`. Cette relève ne relance pas une seconde correction sur ces zones.

Pour la phrase des Ateliers en visioconférence, le remplacement éditorial proposé est :

> Nos ateliers en ligne proposent une exploration guidée du Point Zéro. Vidéos, situations de jeu et échanges mettent les grandes questions de notre époque au contact de vos propres expériences.

Cela remplace la promesse de « jeu de cartes exclusif » par une description du dispositif, sans annoncer une manipulation de cartes matérielles. La mise en contact préalable avec les cinq parcours appartient au nouveau M0 : l’expression « classe inversée » et les consignes de préparation devront être alignées sur ce parcours lorsque la réorganisation sera activée.

Cette proposition éditoriale est transmise au poste fixe. Aucune description d’événement ni donnée financière n’a été modifiée par Codex pendant cette relève.
