# Symbole Oméga — unité vivante dans l'interface

> **Ajout Codex — décision de Boris du 29 août 2026.**
> **Référence exécutable :** `zegame-prototypes`, commit `6d062f9`,
> `m0-shell.js` et `m0-shell.css`.

## 1. Signe canonique

Le glyphe grec isolé `Ω` n'est plus l'icône d'interface de l'Oméga. Il est remplacé par un
**petit lemniscate monochrome violet**, parcouru par un **point violet** qui circule entre ses
deux lobes. Les polarités restent portées par la forme ; aucun point fixe ne matérialise leurs
extrémités.

Dans un compteur, la lecture est toujours :

```text
172  [lemniscate vivant]
```

Le nombre, violet et gras, précède le signe sur une même ligne. Le lemniscate joue ainsi le rôle
d'unité monétaire sans redevenir une lettre ajoutée au nombre.

## 2. Dimensions de référence

| Surface | Lemniscate | Nombre | Mouvement |
|---|---:|---:|---|
| en-tête desktop | `38 × 20 px` | `17 px`, gras | boucle de `3,6 s` |
| en-tête mobile | `32 × 18 px` | `13 px`, gras | même boucle |
| titre de la fenêtre Oméga | `58 × 32 px` | compteur principal séparé | même boucle |

Le trait violet est plus clair que le point mobile afin que celui-ci reste perceptible à petite
taille. La pastille conserve davantage d'air après le signe qu'avant le nombre.

## 3. Portée du remplacement

Le composant doit remplacer le symbole `Ω` **partout où celui-ci sert d'icône ou d'unité visuelle** :

- pastille globale et menus de la coque ;
- fenêtre explicative des Omégas ;
- compteurs de parcours, expériences et Accomplissements ;
- profils, cartes, bilans et surfaces du Commun ;
- états vides ou pédagogiques illustrant l'Oméga.

Les phrases continuent d'écrire `Oméga` ou `Omégas`. L'alternative accessible d'un compteur est
toujours formulée en toutes lettres — par exemple `172 Omégas` — et le dessin reste
`aria-hidden`.

L'implémentation Rails doit utiliser **un composant partagé**, pas recopier le SVG dans chaque vue.
Les occurrences répétées dans une table dense utilisent le même signe en version statique pour
éviter une nuée de mouvements. Les compteurs isolés utilisent la version animée.

## 4. Mouvement réduit

Lorsque `prefers-reduced-motion: reduce` est actif, le point mobile est remplacé par un point
violet fixe au croisement. Le lemniscate, le nombre et le sens de l'unité restent identiques.

## 5. Recette minimale

1. Aucune icône autonome `Ω` ne subsiste sur les surfaces applicatives.
2. Le nombre précède le lemniscate et reste lisible à `390 px`.
3. Le point parcourt effectivement les deux lobes.
4. Les lecteurs d'écran annoncent le nombre d'Omégas, jamais « symbole oméga » ou « infini ».
5. La réduction des animations conserve un signe intelligible et sans mouvement.

