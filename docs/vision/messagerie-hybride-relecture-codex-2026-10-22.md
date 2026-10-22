# Messagerie hybride — relecture Codex des contrats et du lot 1

> Note Codex — 22 octobre 2026. Suite au « r&c » de Boris : relecture de
> l’analyse du portable et du diff de la PR #464 à `c015f38`.
> Relecture documentaire et statique ; ni banc Rails exécuté, ni recette préprod.
> Complète la livraison `zegame-prototypes@3a32dbe`, sans modifier le code serveur.

Références : [analyse d’impact](../architecture/messagerie-hybride-analyse-impact.md),
[livraison et notes complètes](messagerie-mobile-hybride-integration-2026-10-22.md),
[PR #464](https://github.com/PointZero2050/pointzero-app/pull/464).
Les remarques sur le diff sont également déposées dans cette PR.

## 1. Les décisions récentes de Boris

Le portable rapporte et a inscrit dans son analyse : Point Zéro accessible dès
le Monde 0 ; Ombre accessible au Monde 1 ; retrait des six votes Ombre de test de
préprod avec conservation du code de lecture des anciens libellés. Pris en
compte comme décisions de Boris, pas comme nouvelles décisions de Codex.

Conserver les anciens types lisibles sans conversion automatique ni suppression
générale dans une migration. Le constat « aucune pose en production » est celui
du portable au relevé du 22 octobre ; ce n’est pas une garantie d’absence à la
date du déploiement. La future colonne stable ne doit pas dépendre du libellé.

L’analyse contient encore deux formulations antérieures (« M0 Lumière seule »
au §5 et « oui et oui » à la question 3) : les aligner sur ces décisions récentes.

## 2. Réponses aux quatre règles soumises à relecture

### Total des réponses : accord

Compter les réponses visibles de la discussion entière, réponses à une réponse
comprises, humaines ou regards IA. Exclure supprimées et masquées ; ne compter
ni la racine ni sa projection une seconde fois. Utiliser l’ensemble autorisé,
pas la page chargée. Un regard reste identifiable comme tel : son inclusion ne
doit pas suggérer une contribution humaine.

Pour le pied d’une réponse, expliciter que l’ouverture retrouve la même
discussion ; ne pas présenter le total racine comme le nombre de réponses
directement adressées à cette personne. Si le contrat ne fournit un total que
pour la racine, ne pas fabriquer un zéro sur la réponse : conserver l’invitation
jusqu’au raccordement explicite du pied à sa racine.

### Total Source : accord, toutes les poses lisibles

Inclure les poses héritées dans le total Source. Les montrer sous leur libellé
d’origine dans le détail, en lecture seule si le type n’est plus posable. Ne pas
ramener le compteur à zéro ni afficher « tu n’as pas encore réagi » pour un joueur
dont la seule pose est héritée. Le retrait d’un ancien choix suit les droits et
le contrat existants, sans permettre de le poser à nouveau s’il est retiré.

Une seule source de vérité pour le total et les sous-totaux. Éviter à terme les
anciennes rangées expansives sous le message : elles annulent le gain mobile.
Le découpage en lots peut conserver temporairement une lecture héritée, mais
ne doit pas la faire disparaître des comptes réels.

### Non-lus : accord pour un geste explicite, avec corrections indispensables

Lire le fil principal ne marque pas en masse les discussions comme lues.
L’ouverture explicite entre dans la discussion et affiche la première non lue ;
elle **ne vaut pas lecture de toutes les réponses**.

1. Le POST de lecture doit viser les réponses effectivement présentées au lecteur,
   pas le dernier ID de la discussion ni le dernier ID chargé. Une ouverture à
   100 réponses dont 20 chargées n’en lit pas 100. Même dans ces 20, les cartes
   hors écran ne sont pas toutes vues. Le seuil démo de 60 % n’est pas imposé.
2. Le marqueur de lecture doit avancer sans régresser, dans l’ordre autorisé et
   réellement parcouru. Un saut vers la dernière réponse ne doit pas avaler une
   plage intermédiaire non lue ; documenter comment le stockage choisi traite
   ce cas avant de considérer le simple maximum d’ID comme suffisant.
3. **Pas de repli mobile sur le `last_seen_at` courant du fil à chaque rendu.**
   Sinon, ouvrir le fil fait avancer cette date et peut effacer les non-lus
   d’une discussion jamais ouverte : cela contredit la règle de séparation.
   La référence initiale doit être figée au démarrage de ce suivi (ou au premier
   rattachement de la discussion au suivi), puis évoluer seulement par les gestes
   de lecture de discussion. Portable choisit et documente le mécanisme sûr.
4. La première non lue reste un repère stable pendant la session ; nouvelles
   réponses signalées sans saut du défilement. Comptes hors messages du lecteur,
   supprimés et masqués ; accès contrôlé sur chaque lecture/écriture.

Le terme « Lu » du message envoyé reste actuellement un accusé au niveau du fil
selon le contrat décrit par le portable. Ce n’est pas une preuve de lecture de
chaque réponse : les deux mécanismes doivent être nommés et testés séparément.

### Notification : accord pour le destinataire de la réponse, sans perte des autres règles

Une réponse à une réponse prévient l’auteur du message précisément cité,
pas automatiquement l’auteur de la racine. Pas de notification à soi-même,
à un compte non autorisé ou à un regard comme s’il était un destinataire humain.
Respecter silence/préférences et dédoublonner avec les autres motifs.

« À lui seul » concerne la notification **de réponse** : ne pas supprimer les
notifications de mentions explicites ou les autres abonnements déjà autorisés.
La même réponse visible dans deux projections ne produit pas deux notifications.

## 3. Les sept écarts du poste fixe

| Écart | Avis de relecture |
| --- | --- |
| Auteur et menu hors de la bulle | Acceptable : même rattachement visuel au message, une seule heure dans le pied. Préserver le libellé « modifié ». |
| Pièces jointes sous la bulle | À corriger pour le message composé : le pied doit venir après tout son contenu, pas entre texte et pièce/carte. L’affichage d’un pied seul après un média sans texte peut servir de raccord local, sans répéter les commandes. |
| Six libellés jusqu’au lot 2 | Acceptable transitoirement : aucun faux septième choix. Le titre **Tes résonances** peut être porté dès le lot 1, sans dépendre du catalogue. |
| Pas de fiche de statut | Acceptable : ne pas inventer de chronologie. En revanche distribué/lu doivent être distinguables visuellement, pas uniquement dans `title` ou `aria-label`. |
| Total Source limité aux posables | À aligner sur la règle ci-dessus : toutes les poses lisibles, détail hérité conservé. Le zéro doit rester un vrai zéro. |
| Aide limitée aux fonctions réelles ; pas encore de marqueur | Acceptable transitoirement. L’aide permanente reste accessible ; dès que le marqueur est disponible, consultation/fermeture l’écrit, jamais le rendu seul. |
| Douze prénoms + N autres | Acceptable comme aperçu borné de lot 1 ; annoncer qu’il s’agit d’un aperçu. Prévoir l’accès paginé au détail complet plutôt que rendre des milliers de nœuds cachés. Ne pas confondre nombre de poses et personnes distinctes. |

Les pièces, le total Source et l’état visuel ne sont donc pas validés tels quels.
Le découpage en trois lots est cohérent ; ne pas annoncer le fil hybride ou les
non-lus par discussion comme servis par ce seul lot 1.

## 4. Point vérifiable dans le diff #464

Le pied émet `dessin["delivered"]` pour les deux états. Sur les bulles du joueur,
le CSS impose du blanc au texte/état et à `.message-stamp.read svg`. Conséquence :
même double coche blanche pour Distribué et Lu ; le retrait des anciens mots
visibles efface la distinction. Demander deux formes discernables (par exemple
une puis deux coches si cela correspond au contrat actuel), ou un libellé court
visible. Une différence de couleur seule ne suffit pas à la recette accessible.

Le branchement du pied pour un message textuel précède les pièces et cartes,
alors que le cas sans texte le rend après. Tester texte seul, fichier seul,
lien/Récit seul, texte + pièce et texte + carte ; un seul pied tout en bas du
message et un seul menu lié au bon objet.

Recette serveur du lot 1 à faire par le portable : les bancs Rails sont annoncés
non exécutés par le poste fixe. La relecture présente ne les remplace pas.

## 5. Autres demandes reçues

### Immateria « non » et statut Mentor

Conserver le sens technique établi de `SituationDeParcours.statut` : inscription
à ce parcours = commencé. Ne pas modifier globalement les statuts pour réparer
la seule orientation du Mentor. Si aucune expérience n’est encore entamée,
l’orientation d’entrée doit rester proposée à partir de ce fait spécifique,
même avec une inscription automatique de passage. Distinguer « parcours inscrit »
et « première expérience réellement entamée » dans les faits fournis au Mentor,
sans prétendre qu’un joueur a déjà exploré ce qui ne l’est pas.

La séparation données `<faits>` / consigne est correcte. La consigne existante
peut rester ; veiller à ne pas attribuer au joueur une émotion ou une raison
non exprimée, ni à répéter la question après chaque retour. « Sans forcer »
reste une instruction du personnage, pas une donnée sur la personne.

### Avis de civilité

Le texte proposé est clair et compatible avec les trois choix :
« Choisis une civilité : Madame, Monsieur ou Non précisé. » Aucun changement
éditorial demandé, aucune modification du caractère obligatoire décidé par Boris.

### Canon des verbes

Le message récent rapporte un arbitrage explicite de Boris : **J’exprime** et
**Je connais** remplacent les anciennes variantes dans les usages actifs.
Les archives figées de livraison ne doivent pas être silencieusement réécrites.
Pour les maquettes qu’on reprend, relire le référentiel actuel avant de changer
un contenu ; ne pas déduire une décision sur « Je veux / Je décide » du seul
arbitrage de ces deux verbes.
