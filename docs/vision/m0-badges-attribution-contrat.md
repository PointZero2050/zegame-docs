# Monde 0 — contrat d’attribution et d’affichage des badges

**Décision de Boris, 12 septembre 2026.** Les badges restent une mémoire des passages, avec une troisième famille **Dopamine** assumant les compteurs et premières fois avec la distance du Docteur Z.E.R.O. Les badges liés à une Expérience rejoignent le reçu d’Omégas. Les badges Dopamine attendent une respiration naturelle du parcours. La fin du Monde 0 porte son propre bilan.

Références visuelles :

- série des dix-huit badges : `zegame-prototypes@5ab7a9e`, dossier `badges-series-cible/` ;
- quatre surfaces d’attribution : `zegame-prototypes@63d55a5`, dossier `badges-attribution-cible/` ;
- palette canonique de l’éveil : `zegame-prototypes@9ddf784`.

Les nombres, dates et états de ces maquettes sont des données de démonstration. Ils ne définissent aucun barème.

## 0. Portée du nouveau catalogue

La série de dix-huit badges **remplace le catalogue M0 affiché** ; elle ne vient pas ajouter dix-huit objets aux dix-sept seuils actuels. Le mot « supplémentaire » employé pour Dopamine qualifie la troisième famille de l’interface, pas une conservation à l’identique de tous les anciens seuils.

- les sept anciens seuils `m0_*` par Puissance sortent de la collection de badges : leur acquisition est désormais racontée par le sas d’éveil et reste visible par l’activation de la Puissance dans la Boussole ;
- `sas_traverse` est absorbé par le badge de parcours `Point Zéro — Monde 0` ;
- `futur_regarde_en_face` et `futur_renvoie_la_balle` sont absorbés par les badges des parcours qui attestent déjà ces passages ;
- `entrer_dans_le_jeu`, `graine_semee`, `cent_omegas` et la condition quantitative actuelle de `futurs_pluriels` restent reconnus, mais passent dans Dopamine avec les nouveaux titres ;
- `moteur_eveille`, `premier_atelier` et `se_presenter` restent des seuils ; le quatrième seuil graphique, `Les futurs sont pluriels`, reçoit une nouvelle clé et restera secret et non décerné tant qu’une preuve qualitative n’existe pas.

Les slugs des images sont des noms de fichiers, pas une obligation de renommer les clés métier déjà stables.

## 1. Ce qui existe au 12 septembre sur `preprod@60584d7`

Trois mécanismes sont déjà en place, mais ils ne portent pas encore la décision Dopamine.

1. `BadgeDeParcours` relit l’achèvement réel des expériences requises. Il ne stocke pas un second état et date le badge par la dernière validation nécessaire.
2. `SeuilFranchi` relit `config/seuils.yml`. Le catalogue mélange aujourd’hui passages pédagogiques, premières fois et compteurs. `AnnonceDesSeuils` compare l’état avant/après une écriture et place les nouvelles clés dans le flash.
3. `RecuOmega` est un fait persistant, émis une seule fois par couple joueur/Expérience et consommé atomiquement à l’ouverture d’une continuation réelle du même parcours. Il porte le gain mesuré, la ventilation et le solde.

La clôture existe déjà à `JourneysController#accompli`. Elle reçoit le badge dérivé, l’état du parcours, les chapitres, les Omégas gagnés dans le parcours et la suite éventuelle. La page `Accomplissements` rend les badges de parcours et les sept seuils du métaparcours M0 ; elle conserve aussi les réglages actuels de visibilité communautaire par catégorie.

Le flash actuel ne suffit pas au nouveau besoin. Il est perdu si le joueur ferme l’onglet et ne peut pas attendre un retour ultérieur sur l’accueil. Le regrouper visuellement sans changer ce contrat produirait une maquette fidèle et un comportement faux.

## 2. Les trois familles

### Parcours

Un badge de parcours atteste une traversée complète. Sa vérité reste `Journey#completed_by?`, via `BadgeDeParcours`. Le nouveau visuel remplace l’image générique de la carte uniquement lorsqu’un visuel de badge est déclaré ; la photo du parcours reste le repli.

Série M0 : les cinq parcours du Sas et `Point Zéro — Monde 0`.

### Seuil

Un badge de seuil reconnaît un passage qui change durablement ce que le joueur peut voir, comprendre ou faire dans le Jeu. Le Professeur Sirbey en est le gardien éditorial. La vérité reste dérivée des faits métier par `SeuilFranchi`.

Série M0 retenue :

- `Le Moteur s’éveille` ;
- `Premier atelier vécu` ;
- `Se présenter vraiment` ;
- `Les futurs sont pluriels` seulement lorsqu’une preuve qualitative distincte existe.

### Dopamine

Un badge Dopamine reconnaît une première fois ou un compteur. Il ne valide aucun acquis pédagogique, n’ouvre aucun droit et ne verse aucun Oméga. Le Docteur Z.E.R.O. porte la voix de cette famille.

Série proposée :

| Clé métier | Titre | Fait existant ou à raccorder |
|---|---|---|
| `entrer_dans_le_jeu` | J’ai cliqué, donc je suis | au moins une Expérience validée ; clé existante conservée |
| `graine_semee` | Agriculture narrative | `Graine.au_moins_une?` ; clé existante conservée |
| `cinq_experiences` | Je devais juste regarder | cinq Expériences distinctes validées |
| `dix_experiences` | Visiblement, je reviens | dix Expériences distinctes validées |
| `sept_puissances` | Tour du propriétaire | les sept états du métaparcours M0 réellement ouverts |
| `cent_omegas` | Cent Omégas et toutes mes dents | `User#omega >= 100` ; clé existante conservée |
| `futurs_pluriels` | Un futur ne suffisait pas | deux `Traversee.fins_for(user)` distinctes ; clé existante conservée, famille et titre changés |
| `premier_rejeu` | Encore une dernière fois | présence d’un marqueur durable `recommencee:<challenge.slug>` |

Les quatre paliers nouveaux comptent des identifiants distincts, jamais des requêtes ou des clics. Recharger, revisiter ou rejouer un même résultat ne les incrémente pas.

## 3. Collision à résoudre avant le portage

Deux badges ne peuvent pas tomber sur la preuve actuelle de `futurs_pluriels`. Cette preuve compte deux fins distinctes : elle correspond exactement au badge Dopamine `Un futur ne suffisait pas`.

La bascule sûre est donc :

1. conserver la clé stable `futurs_pluriels`, classer sa condition actuelle `devenirs_distincts`, palier 2, dans Dopamine et lui donner le titre `Un futur ne suffisait pas` ;
2. déclarer le seuil graphique `Les futurs sont pluriels` sous une nouvelle clé, par exemple `futurs_mis_en_sens`, sans condition tant qu’un geste de comparaison, de formulation ou de mise en sens n’existe pas ;
3. auditer les détenteurs réels avant le changement de famille et de titre, puis conserver leur date dérivée.

Un simple renommage en place sans audit changerait rétroactivement le sens d’un badge déjà visible.

## 4. Un reçu de badge, pas une seconde vérité

La collection continue de relire les faits métier. En revanche, remettre un badge plus tard exige de mémoriser **l’annonce à faire**. Cette persistance ne dit pas « le badge est acquis » ; elle dit « cette acquisition dérivée n’a pas encore été présentée ».

Le portable peut introduire un reçu minimal, sur le patron de `RecuOmega` :

```text
recus_badge
  user_id
  cle                    # clé stable du catalogue
  famille                # seuil | dopamine
  challenge_id nullable  # source lorsque l’acquisition vient d’une Expérience
  obtenu_le
  consomme_le nullable
  index unique (user_id, cle)
```

Au déploiement, les conditions déjà satisfaites doivent être inscrites comme **déjà remises**. Sans cette initialisation, la prochaine validation d’un joueur ancien lui remettrait artificiellement plusieurs badges Dopamine à la fois. Le reçu ne remplace pas les conditions métier : il mémorise uniquement si leur annonce reste à présenter.

Le titre, la description et le visuel se relisent du catalogue par `cle`. On ne fige pas une copie éditoriale en JSON. La contrainte unique rend le mécanisme idempotent. Les joueurs qui possèdent déjà un badge avant la migration le voient dans leur collection, sans recevoir une rafale rétroactive : le script de mise en service marque leurs reçus comme déjà consommés, ou initialise une borne temporelle équivalente.

`AnnonceDesSeuils` reste le point de détection avant/après écriture. Au lieu de dépendre uniquement du flash, il crée les reçus des nouvelles clés. Les badges de parcours restent dérivés et la redirection de clôture reste inchangée.

## 5. Les quatre surfaces

### A. Reçu de fin d’Expérience

À l’ouverture de la continuation, `RecuOmega.pour_la_vue` reçoit aussi les reçus de badge non Dopamine rattachés à la ou aux Expériences sources. La vue rend, dans un seul dialogue :

1. gain et nouveau solde ;
2. Puissances concernées ;
3. section `Un passage s’ouvre` avec le ou les badges de seuil.

Le bandeau historique `_annonce_seuils` ne rend pas les clés incluses dans ce reçu. Une même acquisition ne produit donc jamais deux célébrations. S’il n’y a aucun gain d’Oméga mais qu’un seuil doit être annoncé, le bandeau discret actuel reste le repli ; aucun faux reçu d’Oméga n’est créé.

### B. Retour naturel sur l’accueil

La page d’accueil du parcours demande les reçus Dopamine non consommés. S’ils existent, elle affiche une seule carte non bloquante : `Le Docteur a des résultats à te communiquer` et le nombre de badges en attente.

Le panneau s’ouvre uniquement au clic. Son ouverture consomme atomiquement tout le lot présenté ; le rechargement et un second onglet ne le représentent pas. Fermer ou `Classer dans mon dossier` conduit au même état : les badges restent disponibles dans `Mes Accomplissements`.

Il n’y a ni modale spontanée, ni pastille rouge persistante, ni notification externe, ni pression de série quotidienne.

### C. Clôture du Monde 0

La route `journey/:id/accompli` existe déjà et reste protégée par l’achèvement réel. La nouvelle vue peut dériver sans stockage supplémentaire :

- badge `Point Zéro — Monde 0` depuis le catalogue visuel ;
- chapitres depuis `JourneyProgress` ;
- nombre de Puissances ouvertes depuis le même lecteur que les cartes du métaparcours ;
- total courant depuis `User#omega` ;
- suite depuis `JourneysController#parcours_suivant`.

La page reste consultable ensuite. L’animation d’arrivée ne se rejoue que lors de la redirection de première clôture ; une revisite affiche le même bilan au repos.

### D. Mes Accomplissements

La page ajoute une troisième section et un troisième filtre. Elle reçoit les badges Dopamine obtenus et verrouillés depuis le catalogue, avec le même composant de carte. Les réglages actuels de visibilité communautaire ne sont pas supprimés par cette maquette : la distinction privé/public retirée par Boris concernait les **compétences du référentiel**, pas les badges.

La visibilité publique de Dopamine n’est pas arbitrée dans cette décision. Tant qu’elle ne l’est pas, la famille reste personnelle et aucune troisième colonne n’est ajoutée au profil communautaire.

## 6. Répartition

### Portable

- catalogue stable et classification des clés ;
- audit des détenteurs avant reclassement ;
- persistance et consommation atomique des reçus de badge ;
- raccord aux reçus d’Omégas, à l’accueil et aux ivars de clôture ;
- migration, retour arrière et bancs de progression.

### Poste fixe

- copie et optimisation des dix-huit visuels dans `public/pz/` ;
- portage strict des quatre surfaces HAML/CSS/JS ;
- absence de double annonce ;
- responsive, clavier, dialogue natif et réduction du mouvement ;
- conservation des réglages de visibilité existants.

### Codex

- cohérence éditoriale des titres, descriptions et conditions ;
- validation de la séparation Seuil/Dopamine ;
- relecture du contrat et des états visibles avant promotion.

## 7. Recette minimale

- Une Expérience validée une fois ne crée qu’un reçu d’Omégas et qu’un reçu par badge concerné.
- Double clic, second onglet, rechargement et rejeu ne recréent aucun gain ni aucune annonce.
- Un badge de seuil inclus dans le reçu d’Omégas ne paraît pas aussi dans le bandeau.
- Deux badges Dopamine acquis avant le retour à l’accueil donnent une carte puis un seul panneau à deux badges.
- Ouvrir ce panneau dans deux onglets ne consomme le lot qu’une fois.
- Une validation mentor ou facilitateur en attente ne produit aucun reçu.
- Un badge sans gain d’Oméga conserve un chemin d’annonce discret.
- Les joueurs antérieurs gardent leurs badges visibles sans annonce rétroactive en série.
- La clôture refuse un parcours incomplet, ignore les facultatives pour le verrou, et affiche le total courant sans le recalculer en JavaScript.
- La collection distingue Parcours, Seuils et Dopamine ; les cartes verrouillées ne révèlent pas un badge secret.
- La page et les dialogues restent utilisables au clavier ; Échap ferme sans perdre l’acquis ; `prefers-reduced-motion` supprime les animations.
