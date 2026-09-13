# Éveil Volonté — écart visuel restant en préproduction

Contrôle Codex du 13 septembre 2026, demandé par Boris sur la fiche `le-point-zero-entrer-dans-le-jeu` et le sas `/parcours/eveil/volonte`. Référence cible : `zegame-prototypes@9ddf784`, dossier `devoilement-emotion-cible/`, variante `?power=volonte`.

## Ce qui est bien à jour

- E2 affiche trois étapes : introduction ; Chaîne invisible + Hypothèse ; découverte de Volonté.
- Le sas possède les trois moments Éprouver, Relier et Retrouver.
- Relier reprend le contenu et les trois usages de la maquette.
- Le troisième moment ouvre le vrai menu des Puissances.
- L’état final immersif existe bien après cette animation (`?etape=4`) : illustration Volonté, emblème fin sous halo jaune, titre « Ta décision a désormais un chemin », trois verbes et deux sorties.
- Le bandeau utilise le fond sombre attendu.

## L’écart qui donne encore l’impression de l’ancienne version

Sur **Éprouver**, la préproduction ne reproduit pas le lemniscate de la maquette. Elle agrandit le petit composant Oméga partagé, dont le SVG a un `viewBox` 40 × 20, jusqu’à la largeur de l’axe. Le trait et le rayon du point sont agrandis avec lui. Résultat visible :

- ruban violet très épais au lieu d’un trait violet fin ;
- gros disque rose mobile au lieu du petit point jaune lumineux ;
- boucles plus hautes et plus resserrées ;
- icônes visuellement moins alignées avec l’axe médian.

La cible `9ddf784` montre un seul lemniscate violet fin et horizontal, un petit point jaune animé, l’icône Ombre sur son disque noir à gauche, le Tao sans cercle ajouté au centre et l’icône Lumière à droite. Les trois cartes sous la figure sont déjà proches de la cible et ne doivent pas être refaites.

## Correction demandée au poste fixe

Conserver un composant partagé, mais lui donner une variante graphique dédiée au grand axe d’éveil au lieu d’étirer la miniature monétaire. Cette variante doit porter la géométrie large de la maquette, un trait fin qui ne grossit pas avec le viewport et un petit point jaune animé avec son repli fixe en réduction des mouvements.

Ne pas réécrire Relier, le moment d’activation du menu ni l’écran immersif final : ils sont présents. La correction porte sur la figure d’Éprouver et son responsive. Vérifier Volonté puis au moins une autre Puissance, sur ordinateur, 390 px et à 200 % de zoom.

