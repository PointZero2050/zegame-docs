# Point Zéro sur mobile — propositions natives complémentaires

*Codex, 24 septembre 2026. Propositions à arbitrer, pas décisions d’intégration.*

Ce document complète l’[audit UX du portage sur les stores](audit-portage-stores-ux-2026-09-21.md).
Il part de l’état livré au 24 septembre : Rails reste la source unique des droits, des preuves, de
la progression et des Omégas ; les liens profonds Android sont amorcés ; la fermeture de compte
est branchée ; le projet natif et les notifications Push n’existent pas encore.

## La promesse mobile

La valeur propre de l’application peut tenir dans une phrase :

> **Point Zéro garde le fil entre deux traversées.**

Le téléphone apporte alors de la continuité aux moments où le site seul perd le joueur :
suspension d’une scène, lien reçu ailleurs, réponse humaine attendue, texte commencé sans réseau,
cap choisi que l’on veut retrouver. La couche native accompagne ces passages ; elle ne décide
jamais qu’une étape est accomplie et ne calcule aucun gain.

## Le noyau recommandé pour la première version

### 1. Reprendre le bon contexte

À la réouverture, la coque restaure une **destination sûre** fournie ou confirmée par Rails :
Expérience et étape consultée, conversation et premier non-lu, Guide ou Mentor attendu, scène
d’Immateria suspendue. Après une longue absence, elle revient à l’accueil et met en avant
`Reprendre ma traversée` au lieu de restaurer silencieusement un état devenu ancien.

**Critère d’acceptation :** suspendre l’application depuis chacun de ces quatre contextes, la
rouvrir après 30 secondes puis après plusieurs heures, et retrouver soit le contexte exact, soit
une reprise explicitement nommée, sans rejouer de POST.

### 2. Protéger tout texte commencé

Messages, Graines et réponses libres gardent un brouillon local chiffré par contexte. Hors réseau,
le joueur peut écrire et relire ; l’envoi reste clairement `En attente de connexion`. Seule la
réponse serveur transforme cet état en `Envoyé` ou reconnaît une action de parcours.

**Critère d’acceptation :** saisir un texte, couper le réseau, tuer l’application, la rouvrir et
retrouver le brouillon. Aucun message, badge, Oméga ni accomplissement ne doit apparaître avant la
confirmation de Rails.

### 3. Notifier une relation, jamais une mécanique de rétention

La demande d’autorisation intervient après un premier échange ou lorsqu’un joueur choisit
`Me prévenir sur ce téléphone`. La première version couvre trois familles :

- réponse d’un Guide ou d’un Mentor ;
- message direct, mention ou activité choisie dans un Cercle ;
- rappel explicitement demandé par le joueur pour un cap ou un événement.

Le verrouillage affiche une formule neutre (`Une réponse t’attend dans Point Zéro`) ; le contenu
privé apparaît après ouverture. Les badges Dopamine, soldes d’Omégas, séries et absences ne
déclenchent jamais de Push.

**Critère d’acceptation :** chaque notification ouvre l’objet exact, respecte les préférences
Rails, ne se duplique pas lorsque le fil est visible et reste muette sur l’écran verrouillé.

### 4. Donner à Immateria un vrai cycle de vie mobile

Immateria et les mini-jeux passent en plein écran, sans chrome de navigateur. La coque gère
suspension, reprise, interruptions audio, orientation, préchargement raisonnable et geste de
retour. Une vibration très légère peut ponctuer l’activation réelle d’une Puissance ou une
validation confirmée par Rails ; elle disparaît avec la réduction des mouvements ou le réglage
correspondant.

**Critère d’acceptation :** interrompre Immateria par un appel, verrouiller l’écran, changer
d’application puis revenir sans recommencer la scène ni dupliquer sa Trace finale.

Le lecteur YouTube reste une dépendance externe déclarée, pas une partie implicite de la coque.
Si son API, le réseau ou la politique de contenu empêchent son chargement, la page remplace le
cadre vide par un état explicite : **« La vidéo ne peut pas être affichée ici. Le lecteur YouTube
n’a pas pu être chargé. Tu peux réessayer ou ouvrir la vidéo directement sur YouTube. »** Les deux
actions sont `Réessayer` et `Ouvrir sur YouTube`; la fermeture de l’écran reste disponible. Cette
indisponibilité ne fabrique aucune validation supplémentaire et ne bloque pas le reste de la page.

### 5. Rendre le cap disponible hors du Jeu

Le cap choisi peut alimenter un **widget discret** ou un raccourci système : son intitulé, la
Puissance concernée et un accès `Reprendre`. Il n’affiche ni diagnostic, ni score, ni texte privé.
Le joueur l’active lui-même depuis son cap ; la désactivation est immédiate.

Cette fonction est une bonne preuve de valeur native, mais elle peut suivre la première
soumission si le calendrier est serré. Rails fournit le cap courant ; le widget ne l’interprète
pas et ne le modifie pas.

## Un scénario de revue qui montre la valeur native

Le compte de démonstration doit permettre au réviseur de constater la différence en moins de cinq
minutes :

1. ouvrir une Expérience par un lien universel ;
2. commencer une réponse, passer hors connexion et retrouver le brouillon ;
3. reprendre le parcours depuis la même étape ;
4. recevoir une notification neutre de Guide et ouvrir la conversation exacte ;
5. entrer dans Immateria en plein écran, suspendre puis reprendre la scène ;
6. fermer son compte depuis le menu.

Une note de revue donne les chemins et explique que les validations, droits et Omégas restent
confirmés par le serveur. Ce scénario apporte à Apple une démonstration observable de la valeur
native au lieu d’une liste de promesses.

## Extensions utiles après la première publication

- feuille de partage entrante vers un brouillon de Graine ou de Trace, avec source et audience
  explicites ;
- téléchargement volontaire d’une Expérience ou du référentiel des Puissances pour lecture ;
- raccourcis d’accueil `Reprendre`, `Échanges`, `Créer une Graine` ;
- ajout volontaire d’un événement ou d’un rappel de cap au calendrier système ;
- réponse rapide à un Échange depuis une notification, après stabilisation de la modération ;
- biométrie ou passkey pour rouvrir localement une session, sans créer une seconde identité.

## Limites à garder visibles

- La barre basse et les panneaux de rubrique restent la navigation principale : la coque native
  n’ajoute pas une seconde navigation concurrente.
- Le cache local ne rend jamais une page périmée « validée » et ne fabrique aucune destination
  accessible.
- Les trois surfaces d’IA ne reçoivent aucune donnée d’identité supplémentaire depuis le mobile.
- Le billet du Festival reste un événement réel. Toute vente future de contenu numérique demande
  un cadrage d’achat intégré avant développement.
- Une permission système se demande au moment où sa valeur devient compréhensible : Push après un
  échange, calendrier après un choix de rappel, photos au moment de joindre un fichier.
