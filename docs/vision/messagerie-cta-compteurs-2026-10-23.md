# Échanges : conserver les actions dans les compteurs

> Note Codex — 23 octobre 2026. Validé par Boris puis transmission demandée
> explicitement : « Pousse à Claude ». Complément ciblé à la livraison du 22 octobre.

## Référence livrée

- Dépôt : `PointZero2050/zegame-prototypes`.
- Branche : `codex/messagerie-m1-popup-unique-20261018`.
- [Commit 25593c9](https://github.com/PointZero2050/zegame-prototypes/commit/25593c9).
- [Rendu partagé](https://github.com/PointZero2050/zegame-prototypes/blob/25593c9/messagerie-par-mondes-cible/compact.js).
- Maquette principale : `messagerie-par-mondes-cible/?stage=m1circle` ;
  comparaison : `messagerie-par-mondes-cible/compact.html?case=mixed&width=390&status=read`.

## Consigne d’intégration

Dans le pied de chaque message et réponse, conserver le verbe quand le compteur
est positif : **Réagir (X)** et **Répondre (X)**, au lieu du nombre seul.
À zéro, conserver les pastilles **Réagir** et **Répondre** sans « (0) ».
Les smileys, icônes Source et réponse, état sélectionné, menus, droits et fenêtres
restent ceux déjà intégrés. Les boutons conservent leurs actions respectives.

Les grands nombres gardent l’abréviation de la maquette (ex. « Répondre (2,8k) »),
avec le total exact dans le libellé accessible ou l’infobulle. Garder les compteurs
à gauche avec espacement et l’heure/état à droite. Si la largeur est insuffisante,
autoriser le retour à la ligne du pied pour préserver les textes et l’heure,
sans rogner ou réduire davantage les caractères.

## Impact et vérification

Changement de présentation uniquement : aucun changement de comptage, stockage,
validation, routes, droits ou logique de bascule. Porter le libellé dans les vues
serveur qui rendent les pieds (messages et réponses), sans recopier le JS de
simulation comme logique métier. Maintenir le rafraîchissement réel de #471.

Maquette contrôlée au navigateur à 390 et 320 px : pieds sans débordement,
états à zéro, positifs et grands nombres inclus. Syntaxe JS et diff propres.
Une fois porté, vérifier aussi l’actualisation après réaction, ajout/retrait,
réponse et changement de nombre. Aucun code applicatif ni déploiement effectué
par Codex pour cette livraison.
