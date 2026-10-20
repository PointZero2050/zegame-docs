# Textes de reprise des cinq parcours avec sauvegarde serveur

> Note Codex — 20 octobre 2026. Réponse à la relecture demandée par le poste fixe
> sur le temps 4 du Sas (#441). Textes des cinq jeux et complément d’inscription ; aucun code
> applicatif modifié par cette livraison.

## Chapeau commun

> Chaque question ouvre une expérience courte, avec un badge à la clé. Ta progression
> s’enregistre dans ton compte : tu peux reprendre plus tard, sur l’appareil de ton choix.

Cette formulation remplace la promesse absolue de pouvoir fermer immédiatement
l’onglet sans perte. La reprise porte sur le dernier état confirmé par le serveur,
pas sur un changement encore en cours d’envoi.

## Fenêtre de sortie

Conserver le choix principal : **Quitter et reprendre plus tard**.

Remplacer **Quitter sans conserver** par **Effacer cette partie**.

Précision à afficher avec le second choix :

> La progression et les réponses de cette partie seront remises à zéro.
> Les badges et Omégas déjà obtenus restent acquis.

Le second choix ne signifie pas « ignorer seulement les derniers changements ».
Dans `humanite/app.js`, `data-quit="effacer"` appelle `resetParcoursState()`, qui
repart de `defaultState()` et enregistre cet état avant de revenir à l’accueil.
Conserver cette distinction dans les autres jeux ; le libellé ne demande aucune
modification de ce comportement.

## Fin de parcours

Garder : **Ton badge est enregistré dans ton compte.**

Ce texte affirme un enregistrement achevé. L’afficher après confirmation du
serveur ; pendant l’envoi, employer **Enregistrement de ton passage…**.
Si la confirmation n’a pas été reçue, ne pas annoncer le badge comme enregistré.
Le reçu M0 attend déjà la réponse du serveur : conserver le même principe pour
cette phrase de fin. Si la vue ne distingue pas encore ces états, signaler le
raccord nécessaire avant de porter une confirmation inconditionnelle.

## Bandeau de reprise

> Ta partie t’attend. Reprends « [titre du parcours] » au dernier point enregistré.

Le titre provient du parcours concerné. Ne pas ajouter de point à l’intérieur des
guillemets si le titre ne le contient pas ; conserver son point d’interrogation.

## Avis de session expirée

> Ta session a expiré. Tes nouveaux choix ne sont plus enregistrés.
> Reconnecte-toi avant de continuer.

La partie peut encore réagir à l’écran après une réponse 401, mais le client ne
confirme plus sa sauvegarde. Ce texte ne promet pas de récupérer les choix non
enregistrés après une reconnexion ou un rechargement.

## Inscription après le retrait du flux d’import

Complément Codex du 20 octobre, en réponse aux trois formulations du poste fixe
sur `inscriptions/new`. À porter avec le temps 5 du nettoyage serveur.

**Bouton :** garder la proposition **Créer mon compte →**.

**Chapeau :** remplacer « Ton compte stabilise tes avancées. » et la phrase
annonçant une restitution d’import par :

> Crée ton compte pour explorer les cinq questions et retrouver ta progression.

**Première entrée de l’encart « Ce qui change » :**

- titre : **Tes parcours et tes badges** ;
- précision : **à retrouver sur l’appareil de ton choix**.

La seconde entrée, « Tes formulations personnelles » / « restent privées par
défaut », reste inchangée. Aucun passage antérieur ni transfert n’est annoncé à
la création du compte. Le champ de bilan local et ses commentaires d’import
obsolètes doivent disparaître avec le flux correspondant, sans modifier les
champs nécessaires à la création du compte ou à l’acceptation des CGU.

Le libellé du bouton décrit l’action réelle du formulaire : créer le compte.
L’intégration se coordonne avec le portable pour le retour au Jeu ; cette
relecture ne change aucune route ni règle d’authentification.

## Périmètre de la relecture

Sources relues sur `pointzero-app`, préprod `47057112` :
`public/sas/partie.js` et les fonctions `resetParcoursState` / `initQuitModal` de
`public/sas/humanite/app.js`. Le contrat serveur de `PartiesSasController` conserve
la Trace achevée et les acquis lorsqu’une partie est remise à zéro.

Cette livraison est une relecture éditoriale. Le poste fixe porte les textes et
vérifie les cinq jeux avec leurs états d’envoi, de réponse et de session perdue.
Le banc rouge du retour de conflit et le nettoyage serveur du temps 5 restent
dans les zones respectives du poste fixe et du portable.
