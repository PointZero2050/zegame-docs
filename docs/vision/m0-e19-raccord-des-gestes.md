# E19 — Raccord des trois gestes

Note Codex, 10 septembre 2026. Réponse à la remontée `2c051a4`, après lecture de `preprod@f6743bd`. Les CTA de cette expérience désignent des actions dans l'application ; leur absence de destination n'en fait pas des actions déclaratives hors écran.

## Deux raccords sur des surfaces existantes

**Geste 1 — Rassembler mes Traces : `/mes-traces`.** Réutiliser le chemin d'excursion et son retour vers E19, comme pour E6/E13. Le geste est une relecture : aucune sélection persistante ni preuve automatique de lecture n'est requise. La consigne invite à repérer les éléments du récit ; elle ne doit pas promettre un panier de sélection qui n'existe pas.

**Geste 2 — Composer ma Graine de passage : éditeur de la Graine de cette expérience.** Réutiliser `SequenceDeGestes.editeur_de_graine` et le helper `journey_challenge_challenges_user_messaging_thread_path` avec le `ChallengesUser` d'E19 du joueur courant. La table `GESTES_DE_GRAINE` couvre actuellement E6/E13 mais pas E19 ; le rang à raccorder est 2. Le service `Graine` accepte déjà le conteneur `ChallengesUser` et `GrainesController#semer_sur_experience` conserve le contexte parcours/expérience. Vérifier le rendu de l'éditeur et son POST avant d'affirmer que l'ajout de table suffit.

Ne pas renvoyer au rituel générique de la Fresque : il perdrait l'origine E19. Ne pas utiliser le fil d'E6 ni celui d'E13. Une ouverture sans Graine ne vaut pas écriture. La Graine reste sous le contrôle du joueur ; publier ou partager demeure un geste explicite. L'accompagnement du mentor peut rester disponible, sans transformer l'envoi d'une question en preuve d'une Graine écrite.

## Carte du Seuil : surface manquante à construire

La recherche dans `app/` et `config/` trouve les textes, mais aucun contrôleur/vue de Carte du Seuil. `Monde1HomeState` indique lui-même que cet objet n'existe pas. Une page de profil ou une liste de Traces ne remplace pas « Sceller ma Carte du Seuil ».

**Lot minimal à préparer :** un écran de relecture de la Graine de passage d'E19, permettant de choisir les éléments à montrer, de prévisualiser la Carte puis de confirmer explicitement. Prévoir la reprise de la Carte enregistrée. Son contenu provient des productions réellement conservées ; aucun futur, cap ou récit n'est inventé pour remplir une case. L'absence de contenu invite à retourner à sa source.

Le portable vérifie d'abord si les mécanismes existants de publication de Graine et de visibilité couvrent ce besoin. Il expose ce qui manque avant d'ajouter un stockage. Le poste fixe porte l'écran après ce contrat. Distinguer enregistrer une Carte et la publier : pas de publication implicite au clic « Sceller ». La Carte peut être gardée privée. Aucun accès M1, aucun point ni validation d'Atelier n'est déclenché par son enregistrement.

Tant que cette surface n'est pas livrée, E19 reste explicitement incomplète dans le suivi d'audit ; ne pas fermer le point parce que le banc tolère l'absence de porte. Ne pas annoncer au joueur une Carte générée. Ne pas remplacer cette lacune par une confirmation déclarative prétendant qu'une Carte existe. Le lot ne modifie pas silencieusement les conditions globales actuelles d'E19 ou de clôture.

## Attribution et vérification

**Portable :** analyse d'impact, raccord des deux premières portes, contrôle du contexte et des droits, puis contrat du stockage/rendu de la Carte. **Poste fixe :** vérifier les destinations rendues, les retours et préparer la surface manquante après ce contrat. Aucun travail concurrent de Codex sur leurs fichiers.

Recette des raccords : compte réellement arrivé à E19 avec Atelier en attente ; ouverture de Mes Traces puis retour à E19 ; ouverture de l'éditeur E19 puis enregistrement d'une Graine ; rechargement et reprise ; absence de création au GET et absence d'écriture dans les expériences ou le compte d'un autre joueur. Une Graine E6 ne satisfait pas le geste d'écriture E19. Le futur test de Carte couvre prévisualisation sans écriture, enregistrement explicite, confidentialité, reprise et absence de récompense supplémentaire.

Références : [rapport M0](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/audit-parcours-lineaire-m0-preprod-2026-09-09.md), [clôture distincte du M1](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/reponses-raccord-parcours-lineaire-m0-2026-08-31.md). Cette note précise le raccord ; elle ne revendique aucun déploiement ni test navigateur nouveau.
