# Schéma éditorial d'une fiche des guides

> Ajout Codex — 2026-08-15.

## Métadonnées obligatoires

| Champ | Fonction |
|---|---|
| `id` | Identifiant stable, par exemple `m0-07` |
| `slug` | Identifiant lisible et stable |
| `title` | Titre public de la notion |
| `status` | `canonique`, `hypothese`, `horizon` ou `recit_symbolique` |
| `min_world` | Premier Monde où le contenu peut être révélé |
| `destinations` | Pages ou territoires où la fiche est pertinente |
| `audiences` | Joueur, facilitateur, administrateur ou public |
| `sources` | Documents qui fondent la réponse |
| `reviewed_at` | Date de dernière validation éditoriale |
| `related` | Identifiants des fiches liées |

## Contenu obligatoire

Chaque fiche contient :

1. **Question principale** — formulation naturelle susceptible d'être saisie par un Joueur ;
2. **Réponse canonique** — réponse indépendante de la voix choisie ;
3. **Version courte** — une à trois phrases pour un encart contextuel ;
4. **Ce que cela change ici** — relation à une page, une action ou une expérience ;
5. **À ne pas affirmer** — confusion, promesse ou dévoilement interdit ;
6. **Sources** — titres publics lisibles des documents de fond, sans chemin de dépôt ; les
   liens versionnés restent dans le registre interne de maintenance et ne sont pas transmis au
   modèle comme contenu citable.

## Statuts de vérité

### Canonique

Notion ou règle actée. Le guide peut l'énoncer directement, en citant sa source.

### Hypothèse

Modèle proposé pour comprendre ou expérimenter. Le guide utilise des formulations telles que
`le Point Zéro propose l'hypothèse que…` et ne le présente jamais comme une preuve.

### Horizon

Fonctionnement ou ambition cible non disponible. Le guide peut en donner un aperçu uniquement
si le Monde et la fiche l'autorisent, en précisant que ce n'est pas encore une fonction active.

### Récit symbolique

Image, mythe ou cosmologie servant à penser et à jouer. Le guide le présente comme un langage
symbolique, jamais comme une vérité imposée au Joueur.

## Granularité

Une fiche répond à une famille de questions cohérentes. Elle ne doit pas devenir un chapitre de
livre miniature. Lorsqu'une réponse exige trois concepts autonomes, créer trois fiches reliées.

## Critère de publication

Une fiche est publiable si une personne qui ignore les documents internes peut :

- comprendre la réponse sans connaître le vocabulaire du projet ;
- distinguer ce qui est acté de ce qui est proposé ;
- savoir ce qu'elle peut faire ensuite ;
- retrouver la source ;
- ne pas apprendre prématurément ce que son Monde doit encore lui faire découvrir.
