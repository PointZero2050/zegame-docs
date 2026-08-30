# Audit UX et DA des cinq parcours publics — 30 août 2026

> **Ajout Codex — décision et demande de Boris du 30 août 2026.**
> **Périmètre audité :** les 58 écrans déclarés des cinq parcours servis sur
> `https://new.pointzero2050.com`, leurs entrées depuis l'accueil public et la galerie
> `screen=accueil`.

## 1. Diagnostic principal

L'accueil public et `screen=accueil` présentent deux fois les mêmes cinq parcours. Les cartes
de l'accueil public omettent le premier écran : chacune des cinq routes nues redirige donc vers
la galerie au lieu d'ouvrir l'expérience choisie.

| Parcours | Destination directe canonique |
|---|---|
| Qu'arrive-t-il à l'humanité ? | `/sas?screen=c01` |
| Quels sont les scénarios du futur ? | `/sas/scenarios?screen=f01` |
| Quelles forces ont façonné nos croyances ? | `/sas/croyances?screen=p01` |
| Qu'est-ce qui nous paralyse ? | `/sas/paralysie?screen=l01` |
| Comment nous réveiller ? | `/sas/reveil?screen=r01` |

La galerie `screen=accueil` reste utile comme page secondaire : accès `Voir les cinq parcours`,
reprise locale et sortie `Explorer un autre parcours`. Elle ne doit plus être une étape imposée
après un choix déjà fait.

## 2. Carte unique des parcours

Créer un composant éditorial unique, rendu en variante compacte sur l'accueil et en variante
large dans la galerie : illustration, question, promesse, durée, badge, état local et CTA.

- `Nouveau` → `Commencer` ;
- `En cours · X %` → `Reprendre` ;
- `Terminé` → `Revoir`.

Les cinq couvertures néoarchaïques de `screen=accueil` existent déjà et sont cohérentes. Elles
doivent apparaître dès l'accueil public et partout où les cinq parcours sont proposés. Une seule
source de contenu et d'état évite que les deux galeries divergent.

## 3. Coque commune avec le site

La coque actuelle coupe les parcours de la navigation principale : le logo revient à la galerie,
la navigation du site disparaît et la croix ne nomme pas sa destination.

Contrat proposé :

- logo Point Zéro → accueil général du site ;
- `Les 5 parcours` → galerie commune ;
- titre du parcours, badge et progression `Écran X sur Y` dans une barre persistante ;
- action explicite `Quitter et revenir au site` ;
- navigation principale accessible en version compacte, sans interrompre l'immersion ;
- en mobile : logo, progression, menu et sortie, sans reproduire toute la barre bureau.

Les sorties distinguent trois gestes : `Explorer un autre parcours`, `Retourner sur le site`,
`Entrer dans le Jeu`.

## 4. Direction artistique arbitrée

La nouvelle direction est **hybride** :

- coque, champs, interactions et textes : registre analytique, clair et fonctionnel ;
- couvertures, transitions, restitutions, badges et images archétypales : registre
  néoarchaïque symbolique ;
- trame triangulaire, papier, lignes fines et polarités avec parcimonie ;
- une couleur dominante par parcours dans une palette commune.

Cette décision précise l'ancien §9 de `parcours-publics-sas.md`, qui réservait les parcours au
seul registre analytique. Elle ne commande pas de transformer les objets documentaires en
fantasy : dans Croyances, les objets réels restent photographiques, mais sont cadrés dans une
composition Point Zéro cohérente.

## 5. Recommandations par parcours

### Humanité

- `c05` atteint environ 2 650 px sur un viewport mobile de 375 px.
- Montrer d'abord les cinq cycles centraux dans une composition de cinq horloges convergentes.
- Placer les cycles complémentaires derrière `Explorer les autres temporalités`.
- Ajouter une illustration de convergence néoarchaïque aux écrans aujourd'hui uniquement
  textuels, sans enfermer le texte dans l'image.

### Scénarios

- `f04` : régénérer les cinq phases comme une série néoarchaïque cohérente. À 1 280 px, la
  cinquième carte est partiellement coupée ; passer à une grille adaptative ou à un carrousel
  dont les commandes et la position sont explicites.
- `f05` : 25 images de styles disparates et environ 3 084 px sur mobile. Afficher une famille à
  la fois par onglets ou accordéons, avec un plateau persistant `Peur · Désir · Probable`.
- Produire les 25 vignettes dans une grammaire commune : matière papier, trame légère, cadrage
  stable et couleur propre à chaque famille de futurs.

### Croyances

- Conserver la présence documentaire des objets.
- `p11` dépasse 2 200 px sur mobile : transformer les vingt fragments en constellation,
  carrousel ou révélation progressive.
- Réserver le néoarchaïsme au cadre, aux lignes de causalité et à la restitution de l'arbre.

### Paralysie

- `l07` et `l08` portent plus de 320 mots chacun ; `l07` approche 2 000 px sur mobile.
- Remplacer une partie du texte par un schéma vivant des trois échelles : soi, organisation,
  société.
- Révéler les explications par étapes et conserver une action principale visible.

### Réveil

- `r05` et `r06` dépassent chacun 2 100 px sur mobile.
- Matérialiser les cinq Cadres et les Puissances par des circuits illustrés et progressifs.
- Conserver les couleurs et icônes canoniques des Puissances sans transformer la scène en score.

## 6. Présence des guides

Les portraits existent déjà sur les écrans de choix et doivent être réutilisés partout où le
guide intervient, notamment dans les restitutions `Ton guide te propose de poursuivre` qui ne
montrent aujourd'hui aucun visage.

- médaillon de 56 à 72 px, nom et voix choisie ;
- Professeur Sirbey : cadre clair, stable, annotations précises ;
- Docteur Z.E.R.O. : contraste violet, légère anomalie graphique, lunettes violettes et cheveux
  blancs ;
- même acquisition, même badge et mêmes choix pour les deux voix.

Assets déjà servis : `/pz/m0/guides/professeur-sirbey.png` et
`/pz/m0/guides/docteur-zero.png`.

## 7. Règles UX transversales

- Un écran long doit révéler progressivement, pas devenir une page encyclopédique.
- Une seule action dominante par écran ; sur mobile, le prochain geste reste visible ou
  facilement retrouvable.
- Les exercices longs gardent un résumé flottant des choix déjà posés.
- Les gros cadres noirs de focus autour des titres deviennent un focus visible Point Zéro,
  violet et intégré — jamais supprimé sans remplacement accessible.
- L'accueil affiche la progression locale ; la reprise ouvre l'écran réellement atteint.
- Les cinq parcours conservent la même charpente : appel, guide, situation, exploration,
  retournement, Trace, restitution, passage.

## 8. Ordre de livraison recommandé

1. Corriger les cinq destinations et brancher la carte unique.
2. Porter la coque commune et les trois sorties explicites.
3. Ajouter le portrait du guide choisi dans toutes ses interventions.
4. Recomposer les écrans longs et leur comportement mobile.
5. Produire le lot néoarchaïque `f04`, puis les 25 vignettes `f05`, puis les diagrammes des
   autres parcours.

