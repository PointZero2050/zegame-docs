# Messagerie : relecture du correctif des réactions simultanées (#471)

> Note Codex — 23 octobre 2026. Relevé « r&c ». Relecture et épreuve locale,
> aucune modification de compte, du code applicatif ou du serveur par Codex.

## Résultat

[PR #471](https://github.com/PointZero2050/pointzero-app/pull/471), révision
`a6608eefb06cf6fbf75cccc420a8ce1b5a9e2744` : **12/12 OK** au navigateur.
Le script exact de #470 (`6c6e5748998ca13f2ded54fda393c9700b08b493`) rate
**T11 et T12 seulement** sur les mêmes cas. Les dix autres passent.
[Sortie exacte](messagerie-pr471-resultats-2026-10-23.txt).

[Relecture déposée dans la PR](https://github.com/PointZero2050/pointzero-app/pull/471#issuecomment-6362298035).
Aucun point bloquant trouvé dans ce diff.

## Ce qui est vérifié

Le numéro suit maintenant l’ouverture d’un autre contenu ou une réouverture,
pas chaque repeint. Chaque formulaire garde son ouverture dans une WeakMap.
Un événement d’une autre ouverture est traité comme étranger : il peut actualiser
la fenêtre mais ne remplace pas un brouillon commencé.

- T11 : deux réactions distinctes en vol ; retour A puis B, fenêtre v2 puis v3.
- T12 : réaction puis aller-retour par Modifier sans brouillon ; le retour de
  l’ouverture précédente actualise tout de même le contenu.
- T1 à T10 conservés : actualisation, brouillon protégé, fermeture, réponses
  réseau croisées, refus tardif, pages et position conservées, lecture masquée
  exclue, longue réponse reconnue après parcours.

`node --check` propre sur messagerie.js et cas.js. Les changements de la garde
Ruby ont été relus ; aucun banc Rails exécuté par Codex.

## Méthode et limites

Scripts et gabarits lus à la révision exacte via GitHub. Serveur temporaire
limité à 127.0.0.1:8794, fetch simulé par l’épreuve de Claude. Seules adaptations :
chemins statiques et bouton visible affichant le résultat de `__cas()`.
La contre-épreuve utilise une URL de script distincte afin d’éviter le cache des
fixtures précédentes. Une première exécution ambiguë sur l’ancienne URL a été
écartée ; elle ne fonde pas le résultat ci-dessus.

Cette épreuve vérifie le gestionnaire face aux événements simulés, pas
l’ordonnancement des réponses du serveur réel ni un usage multiutilisateur.
Les tests ne constituent pas une nouvelle recette visuelle ou en écriture
sur la préprod. Fichiers locaux : `.codex-tmp/review-messagerie-471/`.

## Livraison rapportée

La PR est fusionnée. Le portable indique `de9465d` servi et quatre bancs verts :
messagerie_suivis, messagerie_carte, reactions_ombre, a2. C’est un compte rendu
du portable, distinct de la vérification locale de Codex. Le défaut T11 signalé
dans la relecture #470 est corrigé dans le périmètre testé.
