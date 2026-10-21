# Échanges — microtextes du bandeau et arrivée des regards

> Note Codex — livraison éditoriale du 21 octobre 2026. Réponse aux demandes du poste
> fixe sur #449 et du portable sur l'annonce d'arrivée. À porter selon les
> fonctionnalités réellement disponibles ; aucun comportement serveur n'est livré ici.

## Notifications et recherche — textes confirmés

| Réglage cible | Complément |
| --- | --- |
| Essentiel | Mentions et réponses qui te concernent |
| Tous les messages | Chaque nouvelle publication |
| En pause | Aucune notification pour cet espace |

Dans la fenêtre de réglage, tant que le canal réellement géré est le courriel :

> Choisis les courriels que cet espace peut t'envoyer.

Ne pas présenter ces trois choix avant leur contrat serveur. Le remplacement
du résumé quotidien est l'arbitrage de Boris transmis au portable ; « Essentiel »
ne désigne pas un résumé quotidien. Ces textes ne promettent pas de notifications
natives. Les alertes indispensables au compte ne sont pas des notifications de cet espace.

**Recherche — champ** : Mot, personne ou contenu…

**Recherche — explication** :

> La recherche reste limitée à ce fil et à ce que tu as le droit de lire.

Conserver les exclusions réelles (contenus masqués ou inaccessibles, données
privées, etc.) dans la requête et les extraits, pas seulement dans le lien final.

### États de la recherche — ajout Codex, 21 octobre, nuit

Textes relus sur [#455](https://github.com/PointZero2050/pointzero-app/pull/455),
révision `b5e2b9930108cd98c4e7638ad28d95cdcdaa56e2`. Conserver les formulations
du poste fixe, avec une précision pour le champ trop court :

| État | Texte retenu |
| --- | --- |
| Saisie non vide, moins de deux caractères | Saisis au moins deux caractères. |
| Aucun résultat | Aucun message ne correspond à « [recherche] » dans ce fil. |
| Un résultat | 1 message trouvé. |
| Deux à vingt-neuf résultats | [N] messages trouvés. |
| Plafond de trente résultats atteint | Les 30 messages les plus récents qui correspondent. |
| Trop de requêtes (429) | Trop de recherches d'affilée : réessaie dans une minute. |
| Autre échec | La recherche n'a pas abouti. Réessaie dans un instant. |

Champ vide : pas d'erreur ni de résultats précédents présentés comme actuels.
À trente résultats, ne pas afficher « 30 messages au total » ni prétendre qu'il
en reste forcément d'autres : le serveur retourne au plus trente messages.
La phrase de temporisation correspond au contrat actuel de soixante requêtes
par minute ; si ce contrat change, adapter le délai affiché. Un refus d'accès
ne doit jamais être transformé en résultats issus d'un cache antérieur.

## Ajout de membres — nommer le comportement réel

Le poste fixe précise que le serveur **ajoute directement** les personnes, sans
demande d'acceptation. Pour éviter d'annoncer une invitation qui serait en attente,
adapter les mots, sans créer un nouveau processus :

- **Entrée du menu** : Ajouter un membre.
- **Titre de la fenêtre** : Ajouter des membres.
- **Explication** : Les personnes choisies seront ajoutées à « [nom] ». Elles
  pourront lire les messages auxquels le groupe leur donne accès et y écrire.
- **CTA** : Ajouter au groupe.
- **Annulation** : Annuler.

Conserver les droits actuels : l'entrée et le POST ne sont accessibles qu'aux
personnes habilitées. Ne pas promettre un accès à tout l'historique si le serveur
le limite. S'il existe plusieurs personnes ajoutées, reprendre le nombre réel
dans l'avis de succès, sans avis d'« invitation envoyée ».

Ce choix de libellé corrige uniquement l'écart signalé sur #449. Une invitation
avec acceptation serait un autre comportement, à concevoir séparément.

## Arrivée d'un regard — texte retenu

> [Nom] rejoint le fil à l'invitation de [Prénom], pour [mission]. C'est un regard
> IA. Il ne pourra lire que les messages des membres qui l'ont autorisé ici,
> écrits après leur accord et après son arrivée. Chacun garde la main sur son choix.

**Choix : « à l'invitation de »**, sans accord de genre à déduire du nom du regard.
Conserver le reste de l'annonce. Ce correctif ne modifie ni le bloc versionné
de l'accord `2026-10-20`, ni les permissions, ni la mission, ni la règle de
nouvel accord lors d'une nouvelle invitation ou mission.

## Mémoire

Règles et microtextes dédiés :
[Mémoire du groupe — V1](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/memoire-du-groupe-v1-2026-10-21.md).
Le filtre n'apparaît qu'une fois sa vue fonctionnelle ; aucune conservation
simulée dans l'application.
