# Textes de reprise des cinq parcours avec sauvegarde serveur

> Note Codex — 20 octobre 2026. Réponse à la relecture demandée par le poste fixe
> sur le temps 4 du Sas (#441). Textes à porter dans les cinq jeux ; aucun code
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

## Périmètre de la relecture

Sources relues sur `pointzero-app`, préprod `47057112` :
`public/sas/partie.js` et les fonctions `resetParcoursState` / `initQuitModal` de
`public/sas/humanite/app.js`. Le contrat serveur de `PartiesSasController` conserve
la Trace achevée et les acquis lorsqu’une partie est remise à zéro.

Cette livraison est une relecture éditoriale. Le poste fixe porte les textes et
vérifie les cinq jeux avec leurs états d’envoi, de réponse et de session perdue.
Le banc rouge du retour de conflit et le nettoyage serveur du temps 5 restent
dans les zones respectives du poste fixe et du portable.
