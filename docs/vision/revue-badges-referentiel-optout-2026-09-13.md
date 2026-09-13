# Revue badges, référentiel et opt-out — 13 septembre 2026

**Note Codex.** Relecture de `preprod@da4c215`, du lot badges fusionné, de la garde du sas
`3affd5b`, et des PR #202/#211. Cette note ne modifie ni règle de progression, ni données, ni
déploiement.

**État après correction, `preprod@462092b`.** Les écarts serveur des sections 1 et 2 ont été
relus et sont soldés : consommation atomique, route unique `/badges/remise`, collection en lecture,
condition qualitative, opt-out jusque dans la consigne active du mentor et M0-23. Restent dans la
section 1 les deux raccords de vue : le tiroir doit utiliser le lot JSON effectivement remis ; la
collection doit annoncer trois familles et conserver une place anonyme pour le secret non obtenu.
Le complément responsive de l'éveil à 650 px est suivi séparément. Les PR #202/#211 du référentiel
ont été rafraîchies et leurs contrôles sont verts, mais la livraison B attend toujours ses libellés
dans les vues avant le circuit explicite de migration.

## 1. Badges : quatre écarts avant promotion

1. **Consommation Dopamine non atomique.** `Badges.consommer!` sélectionne les reçus en attente,
   les met à jour, puis rend la sélection initiale. Deux requêtes concurrentes peuvent donc rendre
   toutes deux le même lot, même si la seconde ne modifie aucune ligne. Le contrat exige qu'un
   seul onglet obtienne le lot. Utiliser une transaction et verrouiller les lignes en attente avant
   leur mise à jour, ou rendre exactement les lignes acquises par un `UPDATE … RETURNING`.
2. **Le tiroir consomme au mauvais geste.** Le lot n'est consommé que par `Classer dans mon
   dossier`. La croix, Échap ou le fond le laissent en attente et le représentent au prochain
   accueil. Le contrat dit que l'ouverture remet et consomme le lot, puis que tous les gestes de
   fermeture aboutissent au même état. Le clic d'ouverture doit donc passer par le POST atomique,
   puis ouvrir le panneau avec le lot effectivement acquis. Le raccord existe déjà :
   `POST /badges/remise` répond en JSON avec `remis`. Il n'est pas nécessaire d'ajouter une route.
   En revanche, ce tableau retourné doit être la source de l'affichage : le JavaScript ne doit pas
   ouvrir les cartes pré-rendues depuis l'ancien état `en_attente`. S'il reçoit un lot vide parce
   qu'un autre onglet l'a consommé, il n'ouvre pas un tiroir périmé.
3. **Collection incomplète.** L'aide de première visite annonce encore « deux mémoires » et ne
   décrit pas Dopamine. Un badge secret non obtenu est entièrement supprimé de la grille alors que
   le contrat retient une place anonyme, sans visuel, titre ni condition révélés.
4. **Condition qualitative trompeuse.** `futurs_mis_en_sens` n'est volontairement pas câblé, mais
   son texte visible dit encore « Atteindre plusieurs devenirs distincts ». Cette condition est
   déjà celle du badge Dopamine `futurs_pluriels`. Le seuil doit annoncer un geste qualitatif, par
   exemple : « Mettre en relation plusieurs devenirs et en formuler le sens. »

L'appel de `Badges.constater!` depuis la collection écrit aussi les reçus manquants lors d'un simple
GET. Il ne fabrique pas l'acquisition, puisque la condition métier est relue, mais il date
l'annonce au moment de la consultation et peut faire apparaître ensuite un lot Dopamine ancien.
La collection devrait rester une lecture ; la constatation appartient aux écritures métier et au
retour naturel sur l'accueil déjà prévu par le contrat.

## 2. Opt-out : canon remis en cohérence

La décision du 12 septembre est : les catégories du mentor sont ouvertes par défaut ; un refus
explicite les referme séparément et s'applique immédiatement ; elles restent rouvrables. La Q&R
principale et l'analyse d'impact ont été corrigées dans ce même commit. Le code préprod applique
déjà ce régime, mais l'en-tête de `ConsentementLlm` décrit encore l'ancien opt-in et la description
de la mémoire dit « Sans ce consentement ». Le corpus embarqué `M0-23` dit également que le mentor
n'accède qu'aux sources ouvertes par le joueur. Ces textes doivent suivre le canon.

L'écart touche aussi la consigne active de `MentorReponse#section_contexte`, pas seulement ses
commentaires : elle qualifie la matière de « explicitement consentie » et affirme que le joueur
« ne t'a ouvert aucune matière personnelle » quand aucun bloc n'est disponible. Avec l'opt-out,
le mentor doit parler de catégories **actuellement ouvertes dans les réglages**. L'absence de bloc
signifie seulement qu'aucune matière n'est disponible dans ces catégories ; elle ne prouve ni un
refus, ni l'absence de contenu dans une catégorie refermée.

## 3. Référentiel des 18 : A recevable, B incomplète

La PR #202 respecte le plan de migration : schéma additif, table figée, refus des nouvelles
références vers une amplitude remplacée, conservation de la provenance, migration transactionnelle,
témoins par axe et retour exact dans la fenêtre sans activité. L'épreuve sur copie de préproduction
et la simulation de production sont jointes à la PR. Aucun écart bloquant n'a été trouvé dans cette
livraison A.

La PR #211 bascule correctement les cinq destinations du Sas vers les clés cibles, avec les mêmes
montants. Elle ne suffit cependant pas à produire l'affichage décidé par Boris. Plusieurs surfaces
réelles lisent encore le nom historique :

- `app/helpers/experience_cover_helper.rb` fabrique l'aspect depuis `skill.name` ;
- `app/views/journeys/_show.html.haml` affiche `skill.name` dans les blocs de compétence ;
- `app/views/gestion/experiences/_form.html.erb` liste `s.name` au lieu du libellé canonique ;
- les exports Markdown/JSON de `Challenge` continuent aussi de publier le nom historique.

La livraison B doit définir quelles surfaces montrent `Skill#libelle` — au minimum les vues joueur
et le sélecteur de gestion — et couvrir leur rendu par un banc. Les exports peuvent conserver le nom
historique pour compatibilité, mais ce choix doit être explicite. Enfin, #211 est rouge au lint sur
des fichiers étrangers à son diff : sa branche de base est ancienne ; la rebaser sur la préprod
actuelle doit éliminer ce bruit avant la recette.

## 4. État de la garde du sas

La garde `3affd5b` est conforme : le POST final ne crée la preuve système que si le geste qui ouvre
le sas existe déjà. Revoir Volonté ou Imagination depuis le menu avant d'avoir refait l'Hypothèse ou
la Graine ne franchit donc pas le rang après `Recommencer`. Aucun changement d'Oméga, de reçu ou de
validation n'est introduit.
