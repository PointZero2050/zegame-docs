# M0 — Dévoilement et preuves par geste

Note Codex — suite de la relève des boîtes et de la demande de Boris « récupère et continue ». Cette note précise l'accord déjà transmis dans `2d7c061`. Elle ne constate pas une nouvelle recette applicative.

## Dévoilement : règle et exception du rite

Pour les expériences ordinaires, la reprise nomme l'expérience si son chapitre est dévoilé. Si la progression désigne une expérience d'un chapitre encore fermé, présenter la transition vers ce chapitre : « La suite de ton parcours » et « Découvrir le prochain chapitre », sans nommer son expérience. Ce CTA doit rejoindre une transition réellement autorisée ; en présence d'un prérequis manquant, afficher la raison et la reprise accessible plutôt qu'un lien condamné. Ne pas dévoiler un chapitre uniquement parce qu'un calcul de prochaine expérience le désigne.

**Le rite final et les préparations annoncées dans son bloc sont une exception de présentation explicite**, conformément à la [carte du voyage, §3.3 et §3.7](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/page-parcours-carte-du-voyage.md). Leur nom et leurs prérequis peuvent rester visibles avant le chapitre correspondant. Visibilité ne signifie pas accès : les liens d'action gardent leurs conditions et les préparations indisponibles restent inactives. Ce traitement ne révèle pas les autres cartes du chapitre.

La [discussion de #169](https://github.com/PointZero2050/pointzero-app/pull/169) localise les quatre noms signalés dans le bloc rite, pas dans la ligne de reprise. Ce diagnostic lève la question produit sur ces quatre noms ; il reste à vérifier sur le rendu de la révision relue. Borner les assertions par zone et par rôle d'objet, pas par une liste de noms à ignorer dans toute la page. Vérifier les deux sens : détails ordinaires absents dans un chapitre fermé ; rite et préparations annoncées présents avec accès correctement gardé. Garder l'assertion distincte sur la cohérence prochaine expérience/chapitre dévoilé. Les assertions de DOM doivent suivre le portage linéaire, pas réintroduire l'ancien accordéon ou sa texture.

## Preuves par geste : correspondance sémantique attendue

Boris a confirmé : **reconnaître séparément les gestes pour lesquels une preuve réelle existe ; laisser lectures et observations comme accompagnement sans validation inventée.** Une expérience accomplie n'est pas la preuve rétroactive que chaque sous-geste a été effectué.

Le tableau précise les actions à distinguer. Les sources sont celles relevées dans l'[analyse serveur](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/analyse-impact-parcours-lineaire-m0-serveur.md) et les messages du portable ; leurs champs, scopes et conditions doivent être vérifiés dans le code actuel. Ce n'est pas un mapping Ruby prêt à coller.

| Expérience / rang | Preuve ou traitement attendu |
|---|---|
| E7 / 1 — Choisis ton mentor | Choix de héros effectivement enregistré pour le joueur (`heros_slug` dans l'analyse). Ne dépend pas de la réponse à un message ultérieur. |
| E7 / 2 — Pose-lui une première question | Message du joueur réellement persisté dans la conversation du mentor concerné. Si l'accomplissement global exige une réponse, distinguer « question envoyée » et « réponse attendue » ; ne pas changer cette règle globale en corrigeant l'affichage. |
| E9 / 1 — Compose ton Profil | Condition de profil confirmé réellement portée par le service actuel, limitée à ce geste. Ne pas inventer un seuil de complétude ni considérer la simple existence d'un compte comme preuve. |
| E9 / 2 — Entre dans l'Espace et réagis | Appartenance et réaction persistées du joueur dans l'Espace concerné. Une réaction ailleurs ne suffit pas. |
| E9 / 3 — Découvre l'Annuaire, facultatif | Accompagnement : lien de découverte, aucune case de réussite automatique ni obligation de visite ajoutée. |
| E12 / 1 — Choisis Sirbey ou Z.E.R.O. | Choix effectivement enregistré du Guide si une source durable distincte existe. Une simple ouverture de page ne suffit pas. Si aucun choix distinct n'est persisté, garder une instruction d'accompagnement et signaler cette absence ; ne pas faire dépendre ce rang de la clé éprouvée. |
| E12 / 2 — Mène un premier échange | Échange réel avec le Guide sélectionné, selon les messages persistés et la condition existante d'échange ; distinguer un envoi en attente d'une réponse d'un échange terminé. |
| E12 / 3 — Éprouve une première clé | Preuve de clé éprouvée portée par `ClesMonde0` pour le joueur, et sa Trace si elle est exigée par le contrat courant. Une clé seulement consultée ne suffit pas. |
| E14 / 1 — Actualise une lecture | Évaluation de Puissance réellement enregistrée, selon la condition existante ; pas une simple ouverture du questionnaire. |
| E14 / 2 — Observe sa circulation | Accompagnement sans preuve de lecture ajoutée. |
| E14 / 3 — Ouvre la provenance de tes Ω | Accompagnement et lien fonctionnel, sans validation inventée ni condition supplémentaire d'accomplissement. |

**Portable :** analyse d'impact et traduction vers les vérifications existantes, avec signalement des cases sans source. Réconcilier l'ancienne description d'E14 exigeant un marqueur de lecture avec le message du 1er septembre qui l'écarte ; l'accord ne réintroduit pas ce marqueur. Conserver la distinction entre état courant réversible d'un choix et historique d'accomplissement, l'idempotence et les Ω. Pas de migration ou de table neuve déduite automatiquement de ce tableau.

**Poste fixe :** brancher les états sur ce contrat après livraison du portable. Pour une lecture, montrer l'instruction et son action ; pour une preuve en attente, montrer ce qui reste attendu ; pour une preuve disponible, montrer le fait effectivement reconnu. Ne pas remplacer une action attendue par « Indiquer comme réalisé » lorsque l'application en possède la preuve.

**Recette ciblée :** E7 choix enregistré sans question ; question envoyée sans réponse ; E9 profil confirmé sans réaction puis réaction dans le bon Espace ; E12 échange sans clé puis clé éprouvée ; E14 questionnaire ouvert sans enregistrement puis évaluation enregistrée sans visite des deux lectures. Chaque geste ne bascule que selon sa preuve. Vérifier les comptes déjà avancés et les changements de mentor/Guide sans attribuer une seconde récompense. M0-01 reste séparé : sa clôture exige toujours une traversée réelle d'Immateria.
