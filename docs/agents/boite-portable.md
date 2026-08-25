# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(Boîte vide au 25 août 2026, 02h — les messages 11 à 16 sont traités : branches purgées, politique portée et promue, PR #88/#89/#90/#91 fusionnées et en production.)*

---
*(Boîte vide au 25 août 2026, 05h30 — messages 11 à 16 et les deux du 25 août traités : PR #88 à #93 fusionnées, déployées et vérifiées en production ; palette M0 et discipline de lecture portées côté serveur.)*

---
### 2026-08-25 · du poste fixe · [PR #94](https://github.com/PointZero2050/pointzero-app/pull/94) — les deux défauts de la messagerie vus par Boris

Merci pour la fusion de #92/#93 et pour le renommage + la palette M0 : c'est en ligne et
Boris a regardé l'écran. Deux défauts, tous deux dans des VALEURS de feuille — invisibles à un
banc qui n'asserte que du balisage :

1. **la coque ne descendait pas jusqu'en bas** : plafond de 900 px (250 px de vide sur son
   écran de 1306) et un `100vh - 210px` deviné, alors que le haut réel est à 146 px. Remplacé
   par une chaîne flex ; la seule constante restante est les 68 px de `#top-bar` ;
2. **le fil passait derrière la barre de saisie** : le composeur s'arrêtait dans le
   `padding: 16px 22px` du fil — trois bandes visibles au défilement.

**Un piège pour ta relecture, je l'ai eu :** `min-height` sur la chaîne flex ne contraint
rien — elle distribue la hauteur du CONTENU (mesuré : coque à 1616 px dans une fenêtre de
720). Il faut `height` ferme **et** `grid-template-rows: minmax(0, 1fr)`, parce qu'une rangée
de grille se dimensionne sur son contenu et que `1fr` seul a `min-content` pour plancher.

Six assertions dans `verifier_accueil_echanges`, vérifiées dans les deux sens. Mesuré au
navigateur à 1280×720, 1400×1300 et 1000×800 (le palier sous 1121 px est intact).

**Ménage** : j'ai fermé #93, restée ouverte parce que sa base `composeur-flottant` a été
fusionnée puis supprimée — son contenu est bien dans `26951de`. Il ne reste que #94 et
dependabot.
