# Parcours linéaire M0 — audit de préproduction et feuille de route

**Note Codex — 9 septembre 2026, à la demande de Boris.**

La préproduction porte une partie des mécanismes du parcours linéaire, mais conserve plusieurs gabarits antérieurs. Le premier problème à résoudre est le raccord du tutoriel Immateria : le JavaScript servi ne produit pas la preuve que Rails attend pour accomplir l'Expérience 1. Viennent ensuite le dévoilement des destinations, la priorité donnée à l'action et le portage des pages.

## 1. Références, méthode et limites

- [Maquette publiée, vue Parcours](https://maquettes.167-233-210-57.sslip.io/pz-cible/parcours-lineaire-m0-cible/?view=journey). Les huit vues ont été ouvertes : `journey`, `chapter`, `experience`, `excursion-game`, `excursion-power`, `motor-sleep`, `unlock`, `dashboard`.
- [Préproduction](https://preprod.167-233-210-57.sslip.io/), checkout serveur `195b77a35443ec5fc900363fb61e6aa4cff9136d`, relevé pendant l'audit. Les fichiers cités ci-dessous ont été lus à cette révision ; les fichiers Immateria ont également été lus **dans le conteneur qui les sert**, car ces ressources ne sont pas toutes suivies par Git.
- Compte demandé : `recette-a@m0recette.pz`. Connexion explicite à ce compte, après fermeture d'une autre session déjà ouverte. Le mot de passe n'est reproduit dans aucun livrable.
- Parcours réellement observé : connexion → trois écrans d'introduction → accueil neuf → inscription au parcours → chapitre 1 → fiche « Façonner mon jumeau » → saisie du prénom et personnalisation Immateria → début du dialogue → sortie anticipée → reprise de la fiche. Vérifications complémentaires : menu, garde de la Fresque, Profil/Moteur, ouverture du questionnaire Désir sans réponse, Échanges, chapitre futur déplié, préparation facultative verrouillée, restitution repliable.
- Comparaison visuelle à **1280 × 720** et **390 × 844**. Sur mobile, les deux pages comparées ont été ouvertes successivement dans le même onglet, avec largeur vérifiée. Les captures de référence incluent la barre noire de simulation, qui ne fait pas partie du produit.
- **O = observé au navigateur ; C = confirmé par lecture du code servi/déployé ; R = recette complémentaire requise.** Une observation de bouton ne prouve pas que son serveur accepte l'action.
- L'Expérience 1 n'a pas été artificiellement validée. Aucun questionnaire personnel rempli, aucun message à un joueur, aucune inscription à un événement, aucune clôture M0 ni attribution de points forcée. Les états postérieurs sont comparés au code lorsque le compte ne peut pas encore les atteindre. Ce rapport ne vaut donc pas recette de bout en bout des 19 Expériences.
- Les règles actuelles de raccord sont dans [Réponses du 31 août, mises à jour le 2 septembre](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/reponses-raccord-parcours-lineaire-m0-2026-08-31.md). Les chiffres simulés de la maquette ne remplacent jamais les données réelles.

**État laissé au compte :** introduction parcourue, adhésion au parcours créée, entrée et première trace dans Immateria, tutoriel inachevé. Dernier accueil contrôlé : Expérience 1, 0 Oméga. Le compte n'est plus strictement vierge de visites ; il faudra un nouveau compte témoin ou une remise à zéro explicite avant la prochaine recette initiale. Le contexte d'excursion a été refermé par son lien de retour.

## 2. Priorité P0 — rendre le premier passage réellement franchissable

### M0-00 — Exception de recette demandée par Boris pendant l'audit

**Demande explicite du 9 septembre :** « Tant que nous sommes en phase de test, j'aimerais qu'il soit possible de passer Immateria avec le bouton suivant. » Cette décision autorise une sortie de test ; elle remplace, pour la recette uniquement, l'interdiction absolue de proposer un moyen de passer E1. Elle ne change pas la règle d'accomplissement du tutoriel en usage normal.

**Premier livrable à réaliser par le portable :** sur la fiche « Façonner mon jumeau », le bouton **Suivant — passer Immateria pour le test** ouvre E2 et permet de continuer la recette. Le contexte de cette demande est la préproduction ; limiter donc le mécanisme à cet environnement et aux comptes de recette, avec un interrupteur explicite désactivé par défaut. Aucun changement de l'expérience obligatoire pour les vrais joueurs.

**Contrat proposé :** enregistrer un fait de saut de recette distinct de la validation. Ne pas écrire `tutoriel_termine`, `validated_at`, de faux Ω, ni annoncer Désir éveillé. Afficher « Immateria passée pour le test — non accomplie ». Le saut doit survivre au rechargement du compte de test et être réversible par la procédure de recette. E1 reste rejouable.

**Analyse d'impact ciblée :** `Journey#locked_challenge_ids_for` ne franchit aujourd'hui qu'une expérience validée ou une facultative explicitement passée. Ajouter seulement un lien Suivant vers E2 laisserait donc E2 verrouillée. La lecture « prochaine expérience » de `JourneyProgress` doit également tenir compte du saut de test, sinon l'accueil ramènerait toujours à E1. Ne pas rendre E1 facultative en base pour contourner ces deux lectures. Les compteurs d'acquis et `completed_by?` restent distincts du droit de navigation de recette.

**Cas d'acceptation :** compte neuf de recette → Suivant → E2 utilisable → rechargement et retour accueil → reprise E2, toujours 0 Ω et E1 non accomplie ; autre compte et production → bouton absent et action serveur refusée ; double clic → un seul fait de saut ; retrait de l'exception → progression normale restaurée. Un saut ne doit pas suffire à provoquer la clôture M0 ou le passage M1. Si la recette de fin nécessite aussi une dispense d'E1, la rendre explicite et toujours distincte d'un acquis réel.

**Statut : spécifié pour Claude, pas implémenté ni déployé dans cet audit.** Le bouton actuel reste verrouillé ; ne pas annoncer cette fonctionnalité comme disponible.

### M0-01 — Le jeu servi ne signale pas la fin du tutoriel [C, R]

**Attendu :** terminer réellement le Village produit la preuve de fin, puis permet la reconnaissance du passage, sans déclaration de remplacement.

**Constat :** `ParcoursGestesController#fin_tutoriel_immateria` attend un POST sur `/immateria/fin-tutoriel` et pose `Trace.reponses['tutoriel_termine']`. `ExperienceState` lit cette clé pour « Façonner mon jumeau ». Dans le répertoire JavaScript effectivement servi, aucune occurrence de cette route ni de cette clé. Les sauvegardes passent par `/immateria/trace`, dont la liste de paramètres admis ne comprend pas la clé. `GameScene.js:1046-1051` fait seulement `gotoMonde0()` vers `/jeu` et émet `pointzero:goto-monde0`, sans consommateur trouvé dans les sources du module et son gabarit. Il ne faut pas confondre cet événement local avec la preuve Rails.

**Correction — portable + intégration Immateria :** relier la vraie fin du tutoriel au POST authentifié avec CSRF ; attendre la réussite serveur, prévoir une reprise en cas d'échec, puis rendre la fiche/transition d'éveil dans son contexte. Vérifier explicitement où s'effectue l'accomplissement de l'Expérience : le contrôleur actuel pose la preuve mais ne valide pas l'Expérience.

**Recette :** accomplir le tutoriel depuis l'interface ; observer la preuve persistée, le passage de la fiche, les 5 Ω une seule fois et l'éveil Désir. Rechargement, rejeu et double réception ne produisent aucun Ω supplémentaire. Une sortie avant la fin ne produit aucune preuve de fin. **La fin complète du jeu n'a pas été jouée dans cet audit : le défaut de raccord est établi par les sources servies.**

### M0-02 — La séquence propose une confirmation manuelle sur ce geste système [O, C]

**Constat :** E1 affiche simultanément « Par ta confirmation », « événement idempotent de fin de tutoriel (lot 2) ; aucun bouton de validation » et le bouton **« Indiquer comme réalisé »**. Le bouton n'a pas été actionné. Dans `SequenceDeGestes`, `RANGS_PROUVES` omet `faconner-mon-jumeau`, et le repli de `rangs_prouves` renvoie une liste vide pour ce slug ; `_passage` offre alors le bouton déclaratif.

**Correction — portable :** raccorder l'autorité de chaque geste neuf, à commencer par E1, à sa preuve réelle. **Poste fixe :** afficher la reconnaissance système et supprimer le geste déclaratif pour ces rangs. Auditer aussi E7/E9/E12/E14, sans supposer que toutes leurs sous-étapes ont la même autorité.

**Recette :** aucune confirmation manuelle disponible pour E1, preuve absente ou présente. La garde serveur doit refuser une déclaration envoyée indépendamment de la vue. La preuve système doit être lisible par la séquence aussi bien que par la validation globale.

## 3. Navigation et dévoilement progressif

| ID / priorité | Écart constaté | Correction attendue et critère de recette | Responsable |
|---|---|---|---|
| M0-03 · P1 · O/C | Dès le compte neuf, les **sept Puissances sont des liens**, en couleurs, avec tous leurs usages. Aucun état « prochaine », « endormie », « nouveau ». La Fresque refuse ensuite correctement l'accès. `_coque_m0` lit la configuration statique, sans état du joueur. | Brancher le menu sur la même lecture d'éveil que les gardes. Seules les destinations éveillées sont cliquables ; la prochaine annonce son expérience ; les autres cachent leurs usages. Tester compte neuf, une Puissance éveillée, puis toutes. Préserver le comportement M1. | Portable : façade d'état ; poste fixe : rendu. |
| M0-04 · P1 · O | **Échanges est actif** avant E9, sur ordinateur et mobile. La destination présente l'Espace M0 et dit « Tu n'y es pas encore entré ». La maquette grise cette entrée avant son éveil. | Dévoiler le lien dans la navigation au bon moment. Conserver le seuil réel d'adhésion de `/echanges`, conformément au raccord validé : ne pas ajouter une seconde garde de page Communication. | Poste fixe + portable pour la donnée. |
| M0-05 · P2 · O | « Profil » n'a pas le même comportement selon le support : sur ordinateur il ouvre un menu de paramètres, sans entrée directe équivalente ; sur mobile il va à `/users/me`, intitulé « Mon Moteur de Conscience ». Le libellé visuel « Profil » manque également au desktop. | Choisir la destination Profil canonique et la proposer de façon cohérente, en conservant l'accès aux paramètres. Une personne doit retrouver la même identité/les mêmes fonctions sur les deux supports. | Poste fixe, routes existantes avec portable si besoin. |
| M0-06 · P2 · O | Coque différente : petit logo « POINT ZÉRO » au lieu du logo complet 2050, boutons en capsules sur desktop plutôt que navigation espacée avec séparateurs, « 7 Puissances » au lieu de « Puissances », Omégas sans libellé visible au desktop. Sur mobile, le logo disparaît au profit de « Je décide / Mon parcours ». | Porter la coque de la référence avec ses cinq entrées et le logo fourni, icônes et textes cohérents. Retirer la sous-navigation Volonté des trois gabarits du parcours : le M0 entier n'est plus présenté comme une sous-rubrique de Volonté. Ne pas porter la barre noire de simulation. | Poste fixe. |
| M0-07 · P1 · O | Au premier clic « Commencer le parcours », retour à la carte puis besoin de cliquer une seconde fois pour ouvrir le chapitre. Flash technique **`["m0_volonte"]`** et badge « Premier pas posé ». Après entrée/sortie Immateria : **`["m0_desir"]`**, « Flamme reconnue », alors que l'expérience reste inachevée et le solde à zéro. | Un seul geste d'entrée conduit à la respiration du chapitre après adhésion. Filtrer les clés techniques du rendu des flashs. Distinguer les anciens badges de visite et les éveils fondés sur une expérience réellement accomplie ; ne pas annoncer l'un comme l'autre. | Portable pour événements/flashs ; poste fixe pour annonces. |
| M0-08 · P2 · O | L'aide `?` existe sur E1 et le Moteur et ne s'ouvre pas spontanément — conforme. Elle manque sur la carte générale et sur le chapitre. | Compléter les deux aides manquantes, près du titre, ouverture au clic seulement. Aucun effet sur points/progression. | Poste fixe ; contenu à reprendre du lot d'aides existant. |

## 4. Vue Parcours : le portage est incomplet

| ID / priorité | Maquette → préproduction observée | Correction attendue et recette |
|---|---|---|
| M0-09 · P2 · O | Cover pleine largeur avec personnage/cartographie, « Parcours d'initiation / Monde 0 » et introduction validée → illustration de cité/boussole, carte à marges, « Monde 0 · le Seuil / Point Zéro - Monde 0 », ancien texte. | Porter image, cadrage, largeur et composition de la cover, ainsi que l'introduction cible. Conserver les données réelles du joueur. Comparer à 1280 et 390 px. |
| M0-10 · P2 · O | CTA blanc arrondi avec flèche dans un disque sombre → bouton rectangulaire Bootstrap. | Porter le composant et ses états clavier/focus. Son libellé reste adapté à l'état réel : commencer/reprendre, pas le « Continuer » simulé avant toute entrée. |
| M0-11 · P1 · O/C | Cartes de chapitres avec titres courts et lien « Découvrir le chapitre » → accordéons, titre long concaténé, numéro répété, badges et gros paragraphe narratif avant les expériences. | Reprendre la structure de `journey` : résumé court sur la carte ; récit long dans la respiration du chapitre. Ajouter son lien explicite. La carte générale ne doit plus dupliquer la page chapitre. |
| M0-12 · P1 · O | Les chapitres futurs sont seulement repliés : **ouvrir le chapitre 2 révèle les sept noms, textes, durées, Ω et actions futures** dès E1. | Rendre un aperçu non dépliable avant le seuil : titre, nombre, montant global, annonce du dévoilement. Le contenu détaillé apparaît après le chapitre précédent. Garder les gardes serveur en plus du rendu. |
| M0-13 · P1 · O/C | « Expérience 1 sur 17 », « Voir les 20 Expériences », puis « Expérience 1 sur 20 » dans la fiche. Chapitre 3 annonce 6 expériences. Le canon définit 19 expériences (16 essentielles + 3 facultatives) **puis** un épilogue. | Séparer comptage éditorial et objets techniques : ne pas compter l'épilogue comme une 17e expérience essentielle. Afficher explicitement le sens du dénominateur. Carte : 7/7/5, épilogue séparé. Ne pas recopier le « Voir les 16 » ambigu du simulateur comme total de toutes les expériences. |
| M0-14 · P2 · O | La durée globale devient **6 h 45 + 1 h 25 facultatives**, contre **6 h 30 dont 1 h 30 facultative** dans la référence. E1 dit 5 minutes sur la carte mais 10 minutes dans sa séquence (et 8 min dans la simulation). | Réconcilier les durées éditoriales, incluant les évolutions de l'Atelier, puis dériver total et sous-total. Vérifier que « dont » et « + » expriment le calcul réel. Ne pas modifier des durées métier simplement pour égaler des chiffres de démonstration. |
| M0-15 · P2 · O | Au début, la statistique Ω affiche seulement « 100 à mettre en circulation », sans « 0 obtenus sur 100 disponibles ». Un même chapitre juxtapose « En cours · 0/7 » et « À venir ». **Rectification Codex du 10 septembre :** le second libellé était un état redondant ; l'hypothèse d'un badge de chapitre était erronée. | Garder distincts Omégas obtenus, potentiel et progression du chapitre. Retirer l'état redondant ; aucun badge de chapitre à créer. Afficher une progression lisible même à zéro. La reconnaissance d'une étape doit mettre à jour les mêmes valeurs partout. Correction annoncée par le poste fixe dans `8a1a703`, sans nouvelle recette navigateur de Codex. |
| M0-16 · P1 · O | Le bloc « Vivre l'Atelier » et trois préparations apparaissent dès le départ hors du chapitre fermé. « Le signe de reconnaissance » est cliquable mais ramène une erreur : « Cette Action s'ouvrira quand tu auras accompli les précédentes ». | Retirer cette seconde porte anticipée de la carte initiale ou la rendre honnêtement inactive. Le même objet ne doit pas être verrouillé dans la liste et offert ailleurs. Réserver sa présentation complète à son chapitre. |
| M0-17 · P1 · O/C | « Ce que tu as déjà mis en mouvement » existe avant toute expérience accomplie. Ouvert : « 16 compétences peuvent produire des Oméga dans ce parcours », puis liste vide dans le rendu observé. Ce n'est pas une restitution d'acquis. | Déplacer la restitution réelle après clôture comme prévu. Si un potentiel pédagogique doit subsister dans « À propos », lui donner un autre titre et des lignes réelles, jamais une promesse rétrospective vide. |

**Responsabilité de ce lot :** poste fixe pour les gabarits/CSS ; portable pour les compteurs et la façade des états. À 390 px, carte initiale mesurée à **4 194 px** de haut contre **2 998 px** pour la référence (qui inclut sa barre de simulation). Aucun débordement horizontal global sur les trois pages mobiles contrôlées ; le défaut est surtout l'empilement et la hiérarchie.

## 5. Chapitre : retrouver une respiration immersive

### M0-18 — Composition du chapitre remplacée par l'ancien gabarit [P1, O/C]

La référence `chapter` utilise une illustration en fond, voile sombre, texte clair à gauche, repères compacts en haut, titre « Franchir le seuil » et sous-titre distinct « Je pressens ». La préproduction utilise une carte blanche, une image latérale sur ordinateur puis au-dessus sur mobile, grand « 01 », fil d'Ariane gris, statut et titre concaténé « Franchir le seuil — Je pressens ».

**Correction — poste fixe :** portage DOM/CSS de la respiration, séparation numéro/titre/sous-titre, suppression de la sous-navigation Volonté et des éléments de gestion. Le texte personnalisé au prénom du compte est légitime et doit rester réel. Les nombres simulés de la maquette ne font pas foi : elle affiche encore **5 expériences** ici alors que sa carte en annonce **7**.

**Recette mobile :** référence, CTA à **y = 678 px**, page **916 px** ; préproduction, CTA à **y = 1 111 px**, page **1 961 px**. Retrouver un écran resserré et un CTA accessible dans le rythme de la référence ; comparer après chargement des polices et des images.

### M0-19 — Les médaillons du chemin réapparaissent sous le chapitre [P1, O/C]

Le bloc « Ta traversée — 7 expériences pour changer de place » et ses sept liens n'existe pas dans la respiration cible. Il remet un tableau de navigation après l'introduction et offre aussi les fiches verrouillées. Les réponses de raccord §6 prévoyaient précisément le remplacement de l'ancien chemin de médaillons.

**Correction — poste fixe :** retirer ce bloc du chapitre linéaire ; la carte du voyage porte la navigation détaillée. Garder un CTA vers la première expérience accessible et un retour vers la carte.

## 6. Expérience : remettre le geste avant sa fiche descriptive

| ID / priorité | Écart | Correction attendue et recette |
|---|---|---|
| M0-20 · P1 · O/C | La cible ouvre sur chapitre/numéro/titre puis **l'action courante**. E1 présente d'abord une grande cover vide en dégradé, des Puissances dominantes, un texte, un faux raccourci de validation, les métadonnées, puis seulement le passage. | Déplacer le panneau actif juste sous le titre, conformément à `experience`. Supprimer la cover de cette fiche et les blocs qui précèdent inutilement le geste ; garder les informations de détail après l'action. À 390 px, le vrai CTA E1 est à **y = 1 922 px** ; le CTA de l'exemple E2 de référence est à **y = 645 px**. Les contenus diffèrent, mais l'ordre des blocs explique l'essentiel de cet écart. |
| M0-21 · P1 · O | **« Valider l'étape 1 sur 1 » ne valide rien** : c'est un lien vers `#action`. Deux « Entrer dans Immateria » sont ensuite présents, à deux niveaux de la fiche. | Un seul CTA dominant, nommé par l'action réelle. Si un raccourci subsiste, le nommer « Aller à l'action », pas « Valider ». Supprimer la répétition de la commande et l'ambiguïté avec l'accomplissement global. |
| M0-22 · P2 · O/C | « TA SÉQUENCE », titre « 1 étape », compteur, onglet de la seule étape, puis nouveau compteur/verbe/titre : l'index et le panneau se répètent. La référence montre un repère compact de l'étape active. | Porter ce repère compact ; les étapes futures n'encombrent pas le premier écran. Préserver une reprise explicite d'une étape déjà vécue et la navigation clavier si des onglets restent nécessaires. |
| M0-23 · P1 · O/C | Contenus internes exposés : « À préciser par Codex — valeur provisoire du squelette », « lot 2 », « événement idempotent ». Le YAML porte aussi des « listener », « preuve à ajouter », « confirmation en repli » sur d'autres expériences. | Relire les champs effectivement publics des 19 expériences. Garder la mécanique technique dans la documentation, écrire au joueur le fait concret attendu. Ne pas inventer des niveaux d'intensité pour cacher un manque : compléter éditorialement ou retirer l'indication non établie. |
| M0-24 · P1 · O/C | Le bloc dit « Solo · Autovalidation » et « Par ta confirmation » pour E1, alors que le tutoriel doit être reconnu par le système. La fiche dit également « J'ai réalisé cette expérience » à côté d'une consigne d'attente. | Séparer mode de participation, preuve de l'étape et validation globale ; rendre une attente lisible, sans phrase qui semble déjà déclarer le succès. Aligner séquence, autorité et commandes sur un même contrat. |
| M0-25 · P2 · O/C | Les accroches conservent des descriptions antérieures à la redistribution : E6 dit choisir un mentor alors qu'E7 porte ce choix ; le Signe parle encore de commentaire et de mot-clé alors que sa séquence décrit composer/décider. | Refaire la passe de cohérence **carte → chapitre → fiche → dispositif** avec le canon courant, pas une copie aveugle des textes simulés. Une action a une place et une description cohérentes dans tout le trajet. |

Responsabilité : poste fixe pour l'ordre et le texte ; portable pour l'autorité/les données. Les gabarits communs affectent les expériences suivantes ; leur rendu sur les états multi-étapes reste à rejouer après déblocage normal d'E1.

## 7. Excursions, Moteur endormi et éveil

### M0-26 — Immateria masque aussi le contexte de mission [P1, O/C]

Le plein écran sans navigation générale est correct. En revanche, seule subsiste une discrète sortie « Quitter Immateria » : ni expérience d'origine, ni étape, ni retour explicite vers la fiche. La maquette mini-jeu garde précisément cette barre minimale. Le layout `immateria` n'inclut pas `_bandeau_excursion` et code le retour `/jeu` en dur.

**Correction — poste fixe + portable :** une barre de mission adaptée au canvas, lisible sur mobile, affichée lorsque le joueur est en excursion. Hors contexte : repli vers le parcours. Ne pas réintroduire toute la coque dans le mini-jeu.

### M0-27 — La sortie anticipée fait un détour et laisse le contexte ouvert [P1, O/C]

Reproduction : ouvrir E1 → entrer dans Immateria → quitter avant la fin. Résultat : `/jeu`, avec le bandeau « Exploration guidée / Crée ton jumeau » désormais affiché **sur l'accueil**. Un second clic « Revenir à l'Expérience » ramène bien à E1 et referme le contexte. Le compteur reste à 0 Ω ; aucune fin de tutoriel constatée. Il manque l'état explicite « à reprendre » sur cette sortie.

**Correction — portable :** utiliser le chemin d'abandon/retour d'excursion depuis le mini-jeu, refermer le contexte au bon moment et rendre la fiche/étape active avec la mention de reprise. Les badges de visite ne doivent pas être interprétés comme une validation. Tester rechargement et ouverture dans un second onglet : la session Rails est partagée, ce n'est pas un contexte privé à l'onglet.

### M0-28 — La visite guidée de Puissance n'est qu'un bandeau générique [P1, C/R]

Le partiel partagé existe et connaît l'expérience, son rang et le geste attendu : à conserver. Mais il ne nomme pas la Puissance dans son sourtitre, n'affiche pas « étape x/y », et aucun contrat de mise en avant du premier geste / atténuation du reste n'y est porté. La référence `excursion-power` réunit le contexte et une action ciblée avec « Enregistrer et revenir ».

**Correction — poste fixe :** enrichir le bandeau et ses variantes, puis porter le guidage au niveau des pages concernées. **Portable :** fournir origine, étape, événement attendu et retour contrôlé ; s'assurer que les portes ne créent pas de contexte pour une expérience verrouillée. Le contrôleur `ouvrir` relu vérifie l'existence des objets, mais pas leur accessibilité dans sa méthode : revoir les autres gardes avant de conclure à un contournement.

**Recette restante :** une visite réelle de chaque famille (Graine, mentor, guides, Moteur), succès, abandon, rechargement, contexte périmé et rejeu sans double récompense. Ne pas porter littéralement l'exemple fictif « Désir / écrire une phrase » : adapter au geste métier de la destination.

### M0-29 — Le sommeil du Moteur n'isole pas encore la lecture personnelle [P1, O/C]

Le bloc central dit honnêtement qu'aucune lecture n'a eu lieu et ne simule plus sa lemniscate : **conforme sur ce point**. Mais la page conserve « Transcendance · première lecture », la liste des six Puissances, six liens « Préciser », l'Alchimisation et « Renseigner les 6 restantes ». Le questionnaire Désir s'ouvre effectivement avant E14. L'audit l'a ouvert sans répondre.

**Correction — poste fixe + portable :** garder l'identité/le Profil accessibles, mais porter l'encart « Transcendance · en sommeil », nommer « Lire mon Moteur » et son repère, et ne pas proposer les évaluations personnelles avant leur introduction. Autoriser la vraie évaluation pendant l'excursion E14 puis durablement après le premier geste reconnu. Ne pas fermer `/users/me` en entier. Vérifier et documenter la frontière avec les pages pédagogiques « Comprendre cette Puissance ».

### M0-30 — L'écran d'éveil ne lance pas la première visite guidée [P1, C/R]

La vue déployée nomme la Puissance, l'expérience d'origine, son image et son détail, puis propose uniquement **« Continuer mon passage »**. `EveilsController#vu` marque l'annonce lue, referme l'excursion et retourne à la fiche. La référence dit « Nouveau dans ton espace », explique le déblocage dans le menu et propose **« Découvrir [Puissance] »** pour sa première visite guidée. Le circuit s'arrête donc avant cette visite.

**Correction — portable :** distinguer accusé de lecture et excursion de découverte sans réactiver la Puissance ni redistribuer des Ω. **Poste fixe :** porter la composition cérémonielle et le CTA de découverte ; rendre l'état « Nouveau » dans le menu. Le GET de l'annonce ne doit jamais consommer l'annonce.

**Recette restante :** chaque éveil, menu ouvert depuis l'annonce, première visite, retour, fermeture/rechargement de l'onglet et absence de répétition après accusé.

## 8. Après le M0 : écarts confirmés dans les gabarits, recette à terminer

### M0-31 — Le bilan réutilise le deck navigable au lieu de la photographie cible [P2, C/R]

`home/monde_0` rend le bilan puis l'ancien `.power-deck`, ses cartes, liens `.power-action`, flèches de balayage et pastilles. La référence `dashboard` expose une grille de restitution avec des entrées fonctionnelles/indicateurs et des badges. Ce n'est pas le même mode de consultation.

**Correction — poste fixe :** composer une restitution adaptée à l'après-M0, réutilisant les données et éléments communs sans reprendre le carrousel d'exploration comme structure imposée. Garder les destinations durables dans le menu. Les liens par indicateur doivent avoir une destination réelle, jamais les ancres factices du simulateur.

### M0-32 — Le résumé d'achèvement ne rend pas encore les compteurs du contrat [P2, C/R]

La vue `_bilan_m0` omet les deux fractions essentielles/facultatives et utilise une phrase générique. Le contrôleur calcule déjà `@facultatives_restantes`, mais la vue relue ne l'exploite pas. Le commentaire qui justifiait l'absence de source est donc à réexaminer au regard du code actuel.

**Correction — portable + poste fixe :** exposer des totaux définis sans épilogue et le nombre réel de facultatives restantes ; adapter texte/lien à zéro, une, plusieurs. Ne pas fabriquer les « 3 quêtes / 14 Traces / 172 Ω » de démonstration : à défaut de source, utiliser un lien nommé sans chiffre, conformément aux réponses de raccord §2.

### M0-33 — Recette distincte clôture M0 / passage M1 indispensable [P1, R]

Le code actuel possède bien une clôture idempotente et une condition de présence pointée pour ouvrir le M1. **Ne pas reprendre l'ancien constat du 1er septembre comme un défaut encore établi.** Le compte initial de cet audit n'a atteint ni la clôture ni l'Atelier.

**Recette — portable :** (a) toutes les expériences essentielles accomplies avec inscription confirmée à l'Atelier, mais présence non pointée : après « Ouvrir mon espace », `/jeu` affiche le bilan M0 ; (b) présence pointée : passage M1 selon la règle actuelle ; (c) facultative restante accessible sans bloquer la clôture ; (d) double clic/rejeu sans double Ω ; (e) accès direct à la clôture refusé avant son seuil. Vérifier aussi l'annonce effective promise « Tu seras averti » plutôt que d'en déduire l'existence du texte.

## 9. Ce qu'il faut préserver et ce qu'il ne faut pas copier

**Constats conformes :** trois écrans d'onboarding hors décompte ; démarrage réel à E1 et 0 Ω ; garde de la Fresque ; garde du Signe non encore atteint ; aucun Ω attribué à la sortie anticipée observée ; contexte de retour fonctionnel lorsqu'on utilise `/excursion/retour` ; aide E1/Moteur uniquement au clic ; les trois mesures de parcours existent ; le Moteur central ne prétend plus lire une personne non évaluée ; les mécanismes serveur de preuve, d'éveil et de clôture existent.

**Incohérences de simulation à corriger dans la référence, pas à copier en production :**

1. Carte : 16 dans la reprise, 7+7+5 dans les chapitres ; chapitre simulé : 5 expériences. Le README fixe 19 + épilogue. Employer un seul décompte défini.
2. E2 vaut 5 Ω dans la carte simulée, 3 dans sa fiche. Ne pas modifier le barème de la base pour recopier cette différence.
3. Les 24 Ω du joueur, durées et indicateurs du dashboard sont des exemples. Les remplacer par leurs données réelles ou des liens sans chiffres.
4. Le prénom Boris dans la maquette est un exemple ; celui du compte réel doit être conservé.
5. La référence de visite Puissance et ses liens de démonstration illustrent un contrat, pas des routes applicatives à recopier.

## 10. Ordre de livraison proposé à Claude

| Lot | Contenu | Dépendance / preuve de fin |
|---|---|---|
| 0 — débloquer la recette | M0-00 | Portable : bouton Suivant limité à la recette, saut distinct des acquis, E2 accessible et reprise cohérente. Autorisé par Boris pendant l'audit. |
| 1 — rendre E1 traversable normalement | M0-01, 02, 07, 26, 27 | Portable avec intégration Immateria. **Une vraie traversée E1 au navigateur**, retour au bon endroit, preuve et 5 Ω idempotents. Le saut de test n'est pas une validation de remplacement. |
| 2 — dévoilement cohérent | M0-03, 04, 05, 29, 30 | Façade d'éveil commune, puis menus et Moteur. Recette aux seuils, aucune porte proposée qui se referme au clic. |
| 3 — parcours et chapitre | M0-06, 08 à 19 | Portage strict des structures, couverture, CTA et respirations. Compteurs éditoriaux définis avec le portable. Captures 1280/390, états initial/en cours/chapitre suivant. |
| 4 — fiches et excursions | M0-20 à 25, 28 | Action en premier, texte public terminé, autorité correcte. Rejouer une expérience vidéo à trois étapes et chaque famille de dispositif. |
| 5 — bilan et clôture | M0-31 à 33 | Jeu de comptes témoins aux états de fin ; compter sans épilogue ; vérifier séparation clôture/présence/M1. |

Avant toute modification de progression, validation, points ou de leurs gardes, le portable produit une **analyse d'impact** ciblée : état concerné, preuve actuelle/future, utilisateur déjà avancé, données historiques, idempotence et bancs affectés. Le poste fixe porte les vues et styles après ce contrat. Les régressions M1 doivent être vérifiées puisque les coques sont partagées.

La validation de chaque lot doit associer les bancs pertinents **et la traversée réellement rendue**. Un banc qui appelle directement `/immateria/fin-tutoriel` ne prouve pas que Phaser l'appelle. Un banc qui constate la présence d'un CTA ne prouve pas que ce CTA effectue son action annoncée. Espacer les démarrages Rails de 6 à 8 secondes selon les consignes du serveur.

## 11. Cartographie des fichiers à relire

Toutes les références sont attachées à la révision auditée ; vérifier de nouveau avant édition.

| Surface | Fichiers |
|---|---|
| Parcours et statistiques | [journeys/_show](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/journeys/_show.html.haml), [experience_row](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/journeys/_experience_row.html.haml), [configuration M0](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/config/journeys/point-zero-monde-0.yml) |
| Chapitre | [pages/_show](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/pages/_show.html.haml) |
| Fiche et preuve de geste | [fiche_joueur](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/challenges/_fiche_joueur.html.haml), [passage](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/challenges/_passage.html.haml), [SequenceDeGestes](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/services/sequence_de_gestes.rb), [ExperienceState](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/services/experience_state.rb) |
| Coque et menu | [layouts/jeu](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/layouts/jeu.html.haml), [coque_m0](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/layouts/_coque_m0.html.haml), [coque_m0_nav](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/layouts/_coque_m0_nav.html.haml) |
| Excursion et éveil | [bandeau_excursion](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/shared/_bandeau_excursion.html.haml), [ExcursionsController](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/controllers/excursions_controller.rb), [EveilsController](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/controllers/eveils_controller.rb), [vue éveil](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/eveils/show.html.haml) |
| Immateria | [layout](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/layouts/immateria.html.erb), [vue](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/immateria/show.html.erb), [ImmateriaController](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/controllers/immateria_controller.rb), [ParcoursGestesController](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/controllers/parcours_gestes_controller.rb). Ressources servies : `/rails/public/pz/immateria/js/scenes/{IntroScene,GameScene,DungeonScene}.js` dans le conteneur préprod. |
| Moteur endormi | [users/show](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/users/show.html.haml), [moteur_cartes](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/users/_moteur_cartes.html.haml) |
| Bilan et passage M1 | [HomeController](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/controllers/home_controller.rb), [monde_0](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/home/monde_0.html.haml), [bilan_m0](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/views/home/_bilan_m0.html.haml), [Mondes](https://github.com/PointZero2050/pointzero-app/blob/195b77a35443ec5fc900363fb61e6aa4cff9136d/app/services/mondes.rb) |

## 12. Preuves locales et diffusion

Note Codex — suite à la remontée `46f0bc7` : [contrat de comptage et de durée M0-13/M0-14](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-comptages-durees-contrat.md). Il précise les populations, les libellés et la convention de durée ; les estimations conflictuelles restent à réconcilier. Ce complément ne vaut pas recette des corrections livrées depuis l'audit.

Captures comparatives, relevés textuels et extraits de code dans le dossier partagé `Vibe Coding/outputs/audit-parcours-lineaire-m0-20260909/`. `comparaison.html` présente les paires d'écrans ; le présent rapport est le plan de référence. Les textes de connexion et aucun secret ne sont stockés dans ce dossier.

Note Codex — diffusion actualisée le 9 septembre : Boris a explicitement autorisé le push. Rapport et message au portable publiés sur `zegame-docs/main` dans `d2e6d91`, présence distante vérifiée. Boris demande également la transmission au poste fixe, qui fait les intégrations ; un message dédié est ajouté dans sa boîte. Cette publication ne constitue pas une implémentation ni un déploiement des corrections.
