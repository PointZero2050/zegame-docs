# Bloc 1 « Une drôle d'époque » — illustrations à générer

> Ajout Claude - 2026-07-17, pour l'itération de production d'images (Boris + Codex). Source : [bloc-1-une-drole-depoque.md](bloc-1-une-drole-depoque.md) (script complet) et la [note design](conseil-du-seuil-design.md) §5-6 (grammaire néoarchaïque, prompt matrice). Les emplacements existent déjà dans le flow en ligne (`/une-drole-depoque`) : je branche les fichiers dès qu'ils sont déposés.

## Contraintes de série (rappel + spécifiques au bloc 1)

- **Prompt matrice Codex** (base commune) : illustration éditoriale néoarchaïque, archéologie civique du futur, matières minérales et papier découpé, formes primitives abstraites + cartographie contemporaine précise, obsidienne / craie / turquoise oxydé / jaune solaire / accent corail, composition lisible sur mobile, aucun texte, aucun logo, aucun costume tribal identifiable, aucune esthétique fantasy, aucune interface.
- **Ambiance commune du bloc 1 : été caniculaire** — lumière blanche et dure, ombres portées franches, stores baissés, brumisateurs, pelouses jaunies, la vie décalée vers le soir. Le décalage Point Zéro passe par un détail prosaïque par image (charte de voix §8) : ventilateur, gilet sur une chaise, thermos, pendule arrêtée.
- **Formats** : 16:9 (desktop) + 4:3 (mobile), zone sûre centrale (le texte de l'écran passe à côté/en dessous, jamais incrusté).
- **Continuité** : même territoire (ville moyenne, salle Simone-Veil à moquette orange, friche derrière la gare), personnages récurrents non héroïsés et divers (Nadia ~45 ans, Étienne ~60 ans en polaire, Léna 19 ans, Sonia, Imane) — silhouettes reconnaissables d'image en image sans être des portraits.
- **Ratio des plans** : 70-75 % humain explicite, 25-30 % archétypal implicite (un symbole discret par image maximum : lemniscate en ombre portée, cercle réparé, graine du mauvais côté du plan).

## Les 10 images

| # | Écran | Scène | Éléments obligatoires | Détail pince-sans-rire |
|---|---|---|---|---|
| 1 | Prologue É0.1 (+ visuel de couverture) | La fresque du climat, dimanche soir, salle Simone-Veil | Douze personnes autour de cartes étalées, moquette orange, Nadia debout carnet en main, lumière de fin de journée chaude par les fenêtres | Le vidéoprojecteur éteint, débranché, presque boudeur |
| 2 | Lundi É2 | La cuisine du bureau, 8h40 | Machine à café, Sonia en larmes téléphone en main, le joueur (silhouette neutre, dos ou trois-quarts), tableau des congés au mur | La bouche de clim qui souffle juste au-dessus de la scène |
| 3 | Mardi É1/É2 | La salle de réunion climatisée à 19° | Table de réunion, écran avec slides (planète entre deux mains, illisible), Imane en bout de table, fenêtre éblouissante de chaleur | Un gilet sur le dossier d'une chaise, en plein été |
| 4 | Mercredi É1/É2 | Salle Simone-Veil, 21h, Vision contre Louviers | Deux groupes de part et d'autre, croquis d'arbres-canyons d'un côté, plan technique d'ombrières de l'autre, nuit chaude aux fenêtres | Le vidéoprojecteur allumé — et les deux camps qui le regardent avec méfiance |
| 5 | Jeudi É1/É2 | La décision impossible, 22h40 | Deux plans posés face à face sur la table (dossier mairie / croquis d'action), visages fatigués, Léna debout, Étienne assis bras croisés | La pendule murale arrêtée sur 10h07 |
| 6 | Vendredi É1/É2 | Le salon d'Étienne, réunion « la suite » | Plan de la ville au mur, chaises dépareillées mais alignées au cordeau, fenêtres ouvertes sur la nuit chaude, le joueur qui hésite à parler | L'unique ventilateur qui balaie l'assemblée |
| 7 | Samedi É1/É2 | La terrasse, la bataille des graphiques | Trois études papier étalées, téléphone posé avec un graphique, verres embués, parasol | Le thermomètre de pharmacie affichant 38° en arrière-plan, clignotant et indifférent |
| 8 | (transverse V/S) | La friche derrière la gare, 22h | Terrain vague, herbes jaunies, talus, grillage, lumière de crépuscule étrangement fraîche/bleutée par contraste avec la ville surchauffée derrière | Le chien d'Étienne assis, catégorique, refusant de partir |
| 9 | Dimanche É2 | Le pad, 19h34 | Un téléphone posé sur une table, le pad ouvert (carte aux 47 points, illisible), la nuit qui tombe enfin, une main qui hésite | La notification du collectif voisin qui flotte, un peu trop enthousiaste |
| 10 | Dimanche É4 (clôture) | Le parking de la salle Simone-Veil | Nadia rangeant son carnet, le joueur téléphone en main, ciel de fin de canicule où la chaleur « hésite », la salle éclairée derrière | Au loin, un premier nuage — accueilli comme une célébrité |

## Prompts prêts à l'emploi

Chaque prompt = **matrice + ligne de scène**. Exemple complet pour l'image 1 :

```text
Illustration éditoriale néoarchaïque pour Le Conseil du Seuil, archéologie civique du futur,
assemblée humaine diverse dans un territoire en transition, matières minérales et papier découpé,
formes primitives abstraites mêlées à une cartographie contemporaine précise, obsidienne, craie,
turquoise oxydé, jaune solaire et accent corail, lumière claire, composition lisible sur mobile,
profondeur modérée, aucun texte, aucun logo, aucun costume tribal identifiable, aucune esthétique
fantasy médiévale, aucune interface.
SCÈNE : soir de canicule dans une salle des fêtes municipale à moquette orange, douze personnes
diverses autour de grandes cartes illustrées étalées sur des tables, une animatrice d'environ 45 ans
debout avec un carnet, lumière chaude de fin de journée par les fenêtres, un vidéoprojecteur éteint
et débranché dans un coin, ambiance grave et concentrée mais pas désespérée.
```

Lignes de scène des images 2 à 10 : reprendre la colonne « Éléments obligatoires » + « Détail » du tableau, précédées de « SCÈNE : matin/soir de canicule… ». Garder les mêmes personnages d'une image à l'autre (l'animatrice au carnet = Nadia ; l'homme âgé en polaire malgré la chaleur = Étienne, c'est son détail à lui ; la jeune femme à l'énergie tendue = Léna).

## Branchement technique (pour mémoire)

Dépôt des fichiers : `public/pz/epoque/` sur vibe.ze.game, nommage `01-prologue.jpg` … `10-cloture.jpg` (+ suffixe `-43` pour la variante 4:3). Dès qu'ils existent, j'active leur affichage sur les écrans É1/É2 (les emplacements sont prévus). Me le signaler, ou les mettre dans `Ressources Point Zero/Appli/img/epoque/` et je m'occupe du transfert.
