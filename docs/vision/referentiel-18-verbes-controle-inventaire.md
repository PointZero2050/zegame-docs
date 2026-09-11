# Correspondance par identifiant — contrôle du 11 septembre 2026

Note Codex. Inventaire production transmis par portable, code main@e0a8f9d, données du 11 septembre au matin. Les CSV reçus ont été recalculés localement ; aucune nouvelle lecture directe de la base n’est revendiquée.

Les 42 identifiants ont chacun une et une seule destination parmi les 18 verbes. Le cadre et le verbe concordent avec la table cible pour les 42 lignes. Les 52 rattachements référencent tous un identifiant connu. Aucun couple expérience/cible n’apparaît deux fois : aucune collision à résoudre dans cet inventaire.

Le fichier `referentiel-18-verbes-par-identifiant.csv` constitue la correspondance exhaustive des anciens identifiants vers les clés cibles. Ces clés ne sont pas encore des nouveaux identifiants de base.

| Cible | Anciens identifiants | Expériences liées | Ω statiques prévus | Ω acquis |
|---|---|---:|---:|---:|
| Désir · JE CONTIENS | 61, 74, 75 | 0 | 0 | 0 |
| Désir · JE SUIS | 62 | 3 | 9 | 5 |
| Désir · J'EMBRASE | 71, 72, 73 | 3 | 5 | 0 |
| Volonté · JE SERS | 59, 82, 83 | 6 | 13 | 0 |
| Volonté · JE DÉCIDE | 60 | 3 | 6 | 0 |
| Volonté · JE DIRIGE | 81, 84, 85 | 0 | 0 | 0 |
| Imagination · JE RÉALISE | 63, 89, 90 | 0 | 0 | 0 |
| Imagination · JE CRÉE | 86 | 0 | 0 | 0 |
| Imagination · JE RÊVE | 64, 87, 88 | 8 | 14 | 0 |
| Émotion · JE DISTANCIE | 66, 79, 80 | 0 | 0 | 0 |
| Émotion · JE RESSENS | 76 | 4 | 8 | 0 |
| Émotion · JE COMMUNIE | 65, 77, 78 | 4 | 8 | 0 |
| Communication · J'ÉCOUTE | 67, 94, 95 | 4 | 8 | 0 |
| Communication · JE M'EXPRIME | 91 | 1 | 6 | 0 |
| Communication · JE CAPTIVE | 68, 92, 93 | 4 | 7 | 0 |
| Intuition · JE DOUTE | 70, 99, 102 | 6 | 9 | 0 |
| Intuition · JE DISCERNE | 96 | 1 | 6 | 0 |
| Intuition · JE CROIS | 69, 97, 98 | 5 | 7 | 0 |

## Totaux et portée

La somme de 106 Ω porte sur tous les rattachements statiques exportés : **96 Ω dans M0 + 10 hors M0** (`test-1`, `servir-une-cause`). Elle n’est pas le total du parcours M0. Les **4 Ω dynamiques** de « Lire mon Moteur » restent séparés de ces rattachements : M0 conserve son total de 100 Ω. Ne pas les ajouter à une compétence fixe pour compléter la table.

Les 5 Ω déjà acquis sont rattachés à Désir - Source (#62), sur Façonner mon jumeau. Le regroupement conserve donc leur destination sémantique JE SUIS. Les contrôles de migration devront conserver chaque attribution et sa provenance, ainsi que les totaux par joueur, expérience, Puissance et polarité ; le contrôle d’un seul total global serait insuffisant.

Les six Sources sont désormais identifiées : #62 INTENTION → JE SUIS ; #60 SOUVERAINETÉ → JE DÉCIDE ; #86 CRÉATION → JE CRÉE ; #76 PRÉSENCE → JE RESSENS ; #91 EXPRESSION → JE M’EXPRIME ; #96 DISCERNEMENT → JE DISCERNE. Leur nom historique n’implique aucune ambiguïté de cible.

Cinq cibles n’ont aucun rattachement statique : JE CONTIENS, JE DIRIGE, JE RÉALISE, JE CRÉE, JE DISTANCIE. Cela décrit l’offre d’expériences actuelle, pas l’inutilité de ces compétences. JE CRÉE peut aussi être la destination du gain dynamique de Lire mon Moteur si la première Puissance évaluée est Imagination : « sans rattachement statique » ne signifie donc pas « impossible à créditer ». Aucune expérience n’est réaffectée pour équilibrer artificiellement la couverture.

## Suite technique à préparer par le portable

La correspondance est prête. Préparer le plan de migration réversible : choix explicite des 18 identifiants canoniques ou création de nouvelles lignes, traitement des anciennes lignes et de toutes leurs références, conservation des libellés historiques, sélection unique par cadre, mise à disposition commune du référentiel. La note ne décide pas de supprimer des lignes : Skill détruit ses Points et rattachements en cascade.

Analyser le mécanisme public/privé sans enlever globalement les droits des communautés ni publier le cercle pédagogique. L’accord de Boris définit un référentiel commun de 18 compétences ; son implémentation doit préserver les autres espaces. La publication ponctuelle de #91/#96 n’a pas été exécutée selon le portable ; elle est maintenant à intégrer au plan commun.

Rejouer la simulation sur des données fraîches avant toute migration, vérifier les collisions et références apparues depuis l’export, préserver les gains dynamiques et leur protection contre un second versement. Les amplitudes restent dans les fiches et évaluations : aucun changement des questionnaires ou résultats individuels ne découle du regroupement.

Cette livraison complète la correspondance demandée. Elle ne constitue ni une migration exécutée, ni une autorisation de déploiement supplémentaire.

Source : [inventaire portable](https://github.com/PointZero2050/zegame-docs/tree/main/docs/vision/inventaire-referentiel-2026-09-11).