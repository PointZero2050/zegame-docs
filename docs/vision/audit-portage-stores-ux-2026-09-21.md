# Audit UX du portage de Point Zéro sur les stores

<!-- Ajout Codex, 2026-09-21 -->

## Décision proposée

Publier Point Zéro comme une **application hybride à couche native mince**, en conservant Rails
comme source unique du contenu, des droits, des preuves de progression et des Omégas.

Le portage ne doit pas être une simple WebView. Sa valeur mobile doit être visible dans cinq
continuités :

1. reprendre exactement là où le Joueur s'est arrêté ;
2. ouvrir directement la bonne conversation ou la bonne Expérience ;
3. prévenir sobrement lorsqu'un échange humain ou une réponse attendue est disponible ;
4. ne pas perdre un texte en cours ni devenir opaque lorsque le réseau disparaît ;
5. répondre aux gestes et conventions du téléphone : retour, partage, clavier, zones sûres,
   suspension et reprise.

Cette cible apporte une vraie amélioration d'usage et donne à la version iOS une valeur qui
dépasse le site reconditionné, point explicitement examiné par Apple.

## Périmètre vérifié

Audit réalisé le 21 septembre 2026 sur :

- la préproduction authentifiée réellement servie ;
- `pointzero-app`, branche `preprod`, commit observé `651b38e` ;
- l'audit mobile du 20 septembre et ses quatre lots d'intégration ;
- l'accueil, une fiche d'Expérience, les Échanges et un fil de 500 messages ;
- le manifeste PWA, le service worker, la coque mobile, les préférences de notification,
  les routes du compte et les mécanismes de modération.

Il ne s'agit pas d'un audit juridique complet ni d'une validation sur appareils physiques.

## Ce qui est déjà au niveau d'une application mobile

Les derniers lots ont résolu une grande partie des défauts de la version web initiale :

- barre principale basse à cinq accès, stable et accessible au pouce ;
- panneau vertical commun pour les sous-rubriques ;
- bandeau d'Excursion compact ;
- cibles tactiles principales de 44 px ;
- conversations bornées par la hauteur dynamique du téléphone, avec fil seul défilant et
  composeur séparé ;
- prise en compte de `safe-area-inset-bottom` dans la coque, les composeurs et les reçus ;
- version installable en PWA avec manifeste, icônes et démarrage sur `/jeu` ;
- signalement et blocage disponibles pour les contenus produits par les Joueurs ;
- notification par courriel débouncée pour les fils et digest quotidien par espace ;
- politique de confidentialité versionnée et déjà adaptée au site comme à l'application.

Il faut conserver ces composants plutôt que recréer une seconde interface dans les projets
Android et iOS.

## Écarts actuels

### 1. Il n'existe pas encore de projet natif

Le dépôt ne contient ni projet Android/iOS, ni configuration Capacitor/Cordova, ni fichiers
`AndroidManifest.xml` ou `Info.plist`. La PWA est installable depuis le navigateur, mais elle
n'est pas un binaire distribuable sur les stores.

### 2. Le hors-ligne est volontairement absent

Le service worker transmet chaque requête au réseau sans cache. Une coupure produit donc une page
en échec. Il n'existe pas non plus d'état commun `hors connexion`, de conservation des brouillons
ou de reprise d'un envoi échoué.

### 3. Les notifications restent limitées au courriel

Le réglage actuel est essentiellement `Me prévenir par courriel quand on m'écrit`, complété par
les préférences immédiat/digest des espaces. Il n'existe pas de jeton push, de canaux système ou
de préférence par famille d'événement.

### 4. Les liens web n'ouvrent pas encore l'application

Aucun fichier `apple-app-site-association`, `assetlinks.json` ou gestionnaire de lien profond
n'est présent. Un lien vers un fil ou une Expérience s'ouvre donc dans le navigateur, même si
l'application est installée.

### 5. La suppression du compte est absente

Le menu propose connexion, notifications, personnalisation, aide, CGU et déconnexion. Il ne
propose ni demande de suppression du compte, ni route publique dédiée. Apple exige que la
suppression puisse être initiée dans l'application ; Google exige en plus une ressource web où
la demander.

### 6. Les zones sûres ne sont pas encore complètes

La coque lit correctement l'encoche basse, mais les layouts déclarent
`width=device-width, initial-scale=1` sans `viewport-fit=cover`. Il manque aussi une recette
native des encoches hautes, de la barre d'état, du clavier virtuel et du mode bord à bord
d'Android 16.

### 7. La reprise est fonctionnelle, mais pas systémique

L'accueil sait proposer la reprise du parcours. En revanche, la coque native ne peut pas encore
mémoriser et restaurer :

- la dernière destination sûre ;
- le fil et le premier message non lu ;
- la position dans un contenu long ;
- un brouillon de message ou de Graine ;
- une réponse de Guide ou de Mentor arrivée pendant la suspension.

### 8. Les CGU visibles sont encore un squelette

La politique de confidentialité est complète, mais `/cgu` contient encore plusieurs mentions
`[à compléter]`. Ce n'est pas une amélioration native, mais c'est un obstacle à traiter avant
soumission et avant de présenter la page comme cadre contractuel final.

## Améliorations UX recommandées

### A. Reprise exacte et retour système

À l'ouverture, restaurer le dernier contexte utile lorsque celui-ci est encore autorisé :

- Expérience et étape sélectionnée ;
- fil et séparation des non-lus ;
- conversation avec Amaé, un Guide ou un Mentor ;
- écran d'Immateria avant suspension.

Le retour Android et le geste de bord iOS doivent suivre l'historique interne, fermer d'abord une
feuille ou la roue des Puissances, puis revenir à l'écran précédent. Ils ne doivent jamais fermer
l'application depuis un sous-écran ni réexécuter un POST Turbo.

Après plusieurs heures, l'application peut revenir à l'accueil avec une carte claire
`Reprendre ma traversée`, plutôt que restaurer un état périmé.

### B. Liens profonds vérifiés

Associer `https://pointzero2050.com` aux deux applications :

- Universal Links sur iOS ;
- Android App Links vérifiés ;
- conservation du chemin, de l'ancre et des paramètres utiles ;
- authentification, puis retour automatique vers la destination demandée ;
- repli web identique lorsque l'application n'est pas installée.

Priorités de liens : fil/message, Expérience/étape, invitation de Cercle, profil, événement et
réponse d'un Guide ou Mentor.

### C. Notifications qui respectent l'économie de l'attention

Ne pas demander l'autorisation au premier lancement. La proposer après le premier échange ou
lorsque le Joueur active explicitement `Me prévenir sur ce téléphone`.

Canaux proposés :

1. **Échanges directs et mentions** — activables séparément ;
2. **Guides et Mentor** — seulement lorsqu'une réponse attendue est prête ;
3. **Cercles et événements** — immédiat, digest ou silencieux selon l'espace ;
4. **Rappels choisis par le Joueur** — uniquement si une date ou un cap a été demandé.

Principes :

- aucun contenu sensible dans l'écran verrouillé ;
- une notification ouvre l'objet exact ;
- pas de notification pour un badge Dopamine, un solde d'Omégas, une absence ou une série à
  maintenir ;
- aucun doublon si le Joueur regarde déjà le fil ;
- regroupement des messages d'un même espace ;
- réglage commun `Dans l'app / Push / Courriel / Digest`, sans deux systèmes de préférences.

### D. Réseau dégradé plutôt que faux hors-ligne

Pour la première version, ne pas promettre que tout le Jeu fonctionne hors ligne. Prévoir trois
niveaux lisibles :

1. **consultable** : accueil déjà chargé, fiche de l'Expérience en cours, référentiel des
   Puissances, derniers messages et contenus éditoriaux récemment ouverts ;
2. **conservable localement** : brouillon de message, Graine ou réponse libre ;
3. **connexion requise** : validation d'étape, attribution d'Omégas, IA, paiement, partage et
   envoi de message.

Une action métier différée porte l'état `À envoyer` et une clé d'idempotence serveur. La vue ne
simule jamais une validation, un badge ou un gain avant la confirmation du serveur.

Le premier livrable peut se limiter à : écran hors connexion cohérent, brouillons locaux et
bouton `Réessayer`. Le cache éditorial enrichi peut suivre après publication.

### E. Messageries véritablement mobiles

Le squelette visuel est déjà bon. La couche native permet d'ajouter :

- brouillon conservé par fil ;
- reprise au premier non-lu depuis une notification ;
- état `envoi / envoyé / échec — réessayer` au niveau du message ;
- insertion douce d'un nouveau message sans arracher la lecture ;
- partage système d'une ressource vers le composeur ;
- sélection photo/document via les sélecteurs système ;
- réponse rapide depuis la notification dans une version ultérieure.

Sur les fils très longs, garder le chargement progressif et ajouter une recherche ou un saut par
repères. La préproduction observée montre déjà un espace avec 499 messages antérieurs : charger
ou remonter toute l'histoire ne doit pas devenir le coût normal d'ouverture.

### F. Immateria et les mini-jeux

Pour ces surfaces, le portage peut produire un gain immédiat :

- passage plein écran sans chrome du navigateur ;
- suspension/reprise sans recommencer la scène ;
- état audio cohérent avec le mode silencieux et les interruptions du téléphone ;
- préchargement de la prochaine scène sur Wi-Fi ;
- retour et rotation maîtrisés ;
- vibration très légère sur une validation, désactivée avec la réduction des mouvements ou dans
  les réglages.

La vibration reste une ponctuation rare : activation d'une Puissance ou accomplissement réel,
jamais chaque clic ni chaque Oméga.

### G. Graines et Traces depuis la feuille de partage

La meilleure fonction native différenciante pour une version suivante serait : sélectionner un
texte, une image ou un lien dans une autre application, choisir `Point Zéro`, puis ouvrir un
brouillon de Graine ou de Trace avec la source jointe.

Ce geste relie directement l'usage quotidien au Récit sans fabriquer une nouvelle mécanique. Il
demande toutefois une extension de partage iOS/Android, une règle de provenance et un écran de
consentement ; il ne doit pas retarder la première soumission.

### H. Partage sortant et continuité web

Ajouter la feuille de partage système pour :

- une ressource publique ;
- une invitation à un événement ou un Cercle ;
- une carte d'Accomplissement explicitement rendue partageable ;
- un lien vers une Expérience publique.

Les Graines, Traces, diagnostics et conversations restent exclus par défaut. Le partage doit
indiquer l'audience et ne jamais exporter une donnée personnelle par simple appui accidentel.

### I. Connexion et sécurité perçue

Conserver le compte Rails et le gestionnaire de mot de passe du système. Ajouter ensuite, sans
bloquer la V1 :

- remplissage automatique correctement balisé ;
- stockage du cookie/session dans le coffre de la coque native ;
- déconnexion de toutes les sessions déjà disponible ;
- biométrie ou passkey comme réouverture locale, jamais comme seconde identité métier.

Point Zéro n'utilise pas de connexion Google/Facebook : `Sign in with Apple` n'est donc pas
nécessaire au titre de la règle d'équivalence des fournisseurs sociaux.

### J. Paiement et sorties du Jeu

L'inscription à un événement physique passe aujourd'hui par Stripe. Dans l'application :

- annoncer clairement la sortie vers le paiement sécurisé ;
- ouvrir Stripe dans le navigateur système ou une session web sécurisée ;
- revenir par lien profond sur l'état réel de l'inscription ;
- ne jamais afficher `Payé` avant confirmation du webhook.

Si Point Zéro vend ultérieurement dans l'application un accès numérique, un abonnement ou des
contenus consommés dans l'application, le mode de paiement devra faire l'objet d'un cadrage Store
spécifique avant de réutiliser Stripe.

## Architecture de portage recommandée

### Couche web conservée

- Rails, Turbo et les vues actuelles ;
- même domaine canonique ;
- mêmes sessions, droits et contrôleurs ;
- mêmes composants responsive ;
- même registre de progression et de preuves.

### Couche native mince

- conteneur WebView maintenu, par exemple Capacitor ou équivalent ;
- pont limité à notifications, liens profonds, réseau, partage, haptique, cycle de vie et
  sélection de fichiers ;
- aucune règle de validation ni calcul d'Oméga dans le binaire ;
- version du pont négociée avec Rails pour afficher une mise à jour obligatoire uniquement en cas
  d'incompatibilité réelle.

### Une seule navigation visible

La barre basse web actuelle reste la navigation principale. La coque native ne doit pas lui
ajouter une seconde barre d'onglets. Elle gère les gestes système, les zones sûres et les écrans
techniques natifs invisibles dans le parcours.

## Ordre de réalisation

### Lot Store 0 — Bloquants de soumission

1. créer les projets iOS et Android et figer les identifiants d'application ;
2. ajouter la suppression de compte dans l'application et une page web publique de demande ;
3. finaliser les CGU visibles ;
4. ajouter `viewport-fit=cover`, statut réseau, clavier et recette des zones sûres ;
5. construire avec Xcode 26 / SDK iOS 26 et Android API 36 ;
6. fournir le compte de revue durable et un scénario de revue M0 ;
7. compléter les déclarations confidentialité, sécurité des données, IA et contenus générés par
   les utilisateurs.

### Lot Store 1 — Valeur native de la première publication

1. liens profonds vérifiés ;
2. restauration sûre du dernier contexte ;
3. notifications Push pour Échanges, Guides/Mentor et événements, avec préférences ;
4. brouillons locaux et écran réseau dégradé ;
5. retour Android, geste iOS, clavier, ouverture externe de Stripe ;
6. partage système des contenus explicitement publics ;
7. haptique rare et réglable sur les accomplissements réels.

Ce lot doit accompagner la première soumission iOS : il constitue la réponse concrète au risque
de rejet pour application réduite à un site emballé.

### Lot Store 2 — Après publication

1. partage entrant vers une Graine ou une Trace ;
2. cache éditorial et téléchargement volontaire d'une Expérience ;
3. réponse rapide aux Échanges depuis la notification ;
4. raccourcis d'accueil `Reprendre`, `Échanges`, `Créer une Graine` ;
5. widget discret `Mon cap` ou `Prochaine étape` ;
6. passkeys/biométrie et continuité multiappareil ;
7. App Clip ou expérience instantanée pour un parcours public ou un événement, si l'usage le
   justifie.

## Matrice de priorité

| Amélioration | Impact Joueur | Risque Store | Effort | Cible |
|---|---|---|---|---|
| Suppression de compte | confiance | bloquant | moyen | Store 0 |
| Zones sûres, clavier, retour système | quotidien | élevé | moyen | Store 0/1 |
| Liens profonds | très fort | valeur native | moyen | Store 1 |
| Reprise exacte | très fort | valeur native | moyen | Store 1 |
| Push sobre et réglable | fort | valeur native | fort | Store 1 |
| Brouillons + état réseau | fort | qualité | moyen | Store 1 |
| Partage sortant | moyen | valeur native | faible à moyen | Store 1 |
| Immateria plein écran + cycle de vie | fort | qualité | moyen | Store 1 |
| Partage entrant vers Graine/Trace | très fort | faible | fort | Store 2 |
| Hors-ligne enrichi | fort | faible | fort | Store 2 |
| Widget / raccourcis | moyen | faible | moyen | Store 2 |

## Recette sur appareils obligatoire

Tester au minimum :

- iPhone avec encoche et iPhone sans bouton d'accueil ;
- petit Android, Pixel récent en navigation gestuelle, Samsung ;
- iPad et tablette Android, sans exiger encore une interface à deux colonnes ;
- clavier ouvert dans Espaces, Guides, Mentor, Amaé et formulaires ;
- rotation pendant Immateria et un mini-jeu ;
- perte/récupération réseau pendant une saisie, une réponse IA et une validation ;
- suspension de 30 secondes, 10 minutes et plusieurs heures ;
- arrivée par notification ou lien profond avec session ouverte, expirée et absente ;
- taille de texte à 200 %, VoiceOver/TalkBack et réduction des mouvements ;
- paiement annulé, réussi et webhook retardé ;
- suppression de compte avec contenus, conversations, billet et données conservées légalement.

## Points de conformité directement liés à l'UX

- Apple demande une application qui dépasse un site reconditionné et possède une utilité durable.
- Apple demande une suppression de compte initiable dans l'application lorsque le compte peut y
  être créé ; Google demande aussi une ressource web de suppression.
- Les contenus produits par les utilisateurs exigent filtrage, signalement, blocage et contact
  publié. Point Zéro possède déjà signalement et blocage ; il faut vérifier le filtrage et le
  délai opérationnel de traitement avant soumission.
- Les nouvelles soumissions Google Play doivent cibler Android 16 / API 36 depuis le 31 août
  2026.
- Les envois App Store doivent utiliser Xcode 26 et le SDK iOS 26 depuis le 28 avril 2026.
- Les notifications demandent un consentement contextualisé et ne doivent pas exposer de contenu
  privé sur l'écran verrouillé.

## Sources officielles consultées

- [Apple — App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- [Apple — Offering account deletion in your app](https://developer.apple.com/support/offering-account-deletion-in-your-app)
- [Apple — Upcoming requirements](https://developer.apple.com/news/upcoming-requirements/)
- [Apple — Universal Links](https://developer.apple.com/documentation/Xcode/allowing-apps-and-websites-to-link-to-your-content)
- [Apple — Notifications](https://developer.apple.com/design/human-interface-guidelines/notifications/)
- [Google Play — Account deletion requirements](https://support.google.com/googleplay/android-developer/answer/13327111)
- [Google Play — Target API level requirements](https://support.google.com/googleplay/android-developer/answer/11926878)
- [Android — Core app quality](https://developer.android.com/develop/adaptive-apps/quality-guidelines/core-app-quality)
- [Android — App Links](https://developer.android.com/training/app-links/about)

