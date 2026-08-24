# Parcours publics du site et Sas Point Zéro — vocabulaire et reconnaissance

> Ajout Codex — 2026-08-24. Canon produit et éditorial demandé par Boris pour lever la
> collision entre les cinq parcours publics du site et l'expérience 12 du Monde 0.

## 1. Deux dispositifs, deux noms

| Nom canonique | Définition | Emplacement |
|---|---|---|
| **Les parcours de découverte du site** | Cinq parcours publics, gratuits et jouables sans compte. Ils forment le sas éditorial du site vers l'application, mais le mot **Sas** ne doit pas devenir leur libellé d'interface. | `/sas`, `/sas/:slug`, `config/sas.yml`, `TraceSas` |
| **Un Sas Point Zéro** / **les Sas Point Zéro** | Une rencontre réelle avec l'écosystème. Elle prépare le passage relationnel et constitue l'objet de l'expérience 12 du Monde 0. | agenda, événement et challenge technique historique `le-sas-d-entree` |

Règle éditoriale : écrire **parcours de découverte** pour le dispositif public et **Sas Point
Zéro** pour la rencontre. L'expression isolée « Sas d'entrée » n'est plus un libellé public.

Le slug `le-sas-d-entree` est une dette technique héritée. Il peut rester stable tant que son
renommage coûterait davantage que sa conservation. Les titres, CTA, textes et destinations ne
doivent plus en déduire la nature du dispositif.

## 2. Reconnaissance des parcours publics

- Chaque parcours public accompli reconnaît **5 Ω**.
- Les cinq parcours reconnaissent donc **25 Ω** au total.
- Le montant est identique quel que soit le guide choisi et un parcours rejoué ne produit pas
  une seconde attribution.
- Les traces restent d'abord dans le stockage local. Lors de la création du compte, les parcours
  accomplis, leurs badges et leurs Ω sont importés **automatiquement** ; le joueur en est informé
  avant l'inscription puis par une restitution précise après l'import.
- Cette importation ne publie pas les formulations personnelles. La visibilité communautaire
  reste régie séparément.

### 2.1 Porteur comptable

Créer un challenge système dédié, invisible dans la Marelle :

- titre : **Les parcours de découverte du site** ;
- slug recommandé : `parcours-de-decouverte-du-site` ;
- fonction : provenance technique des Ω importés depuis `TraceSas` ;
- aucune progression de Journey, aucun chapitre et aucune validation d'expérience ne lui sont
  attachés.

Ne pas rattacher ces Ω à `le-sas-d-entree` : ce challenge désigne les rencontres Sas Point Zéro.
Ne pas les rattacher non plus à `le-site-du-point-zero` : cela ferait apparaître l'expérience 7
comme leur origine, alors qu'ils ont été reconnus avant l'entrée dans l'application.

Chaque parcours doit déclarer explicitement dans `config/sas.yml` son montant et sa Puissance de
rattachement. Le code ne déduit jamais le `skill_id` du badge, du slug ou d'un libellé. Ce mapping
éditorial des cinq Puissances doit être validé avant la première attribution réelle.

## 3. Textes canoniques

### 3.1 Invitation sur l'accueil des parcours

> **Tu peux commencer sans compte.** Créer ton compte dès maintenant permet de retrouver tes
> avancées et d'ancrer dans le Jeu les badges et les Omégas obtenus au fil des cinq parcours.
> Si tu préfères explorer d'abord, tout reste conservé sur cet appareil.

CTA principal selon le contexte : `Choisir un parcours` ou `Créer mon compte`.

### 3.2 Fin de chaque parcours — visiteur anonyme

> **Ce passage est accompli.** Ton badge et **5 Omégas** sont conservés sur cet appareil. Crée
> ton compte pour les faire entrer automatiquement dans le Jeu, ou poursuis librement ton
> exploration.

CTA principal : `Créer mon compte`.

CTA secondaire : `Choisir un autre parcours`.

### 3.3 Restitution après import

> **Tes passages ont rejoint le Jeu.** Nous avons importé **[X parcours]**, **[X badges]** et
> **[X Omégas]** depuis cet appareil. Les Omégas ne se dépensent ni ne s'échangent : ils
> reconnaissent les Puissances mises en mouvement et contribueront progressivement à définir ton
> domaine de souveraineté.

La restitution énumère les parcours importés et leur montant. Elle distingue les éléments déjà
présents, nouvellement importés et ignorés comme doublons.

### 3.4 Expérience 12 du Monde 0

**Titre public :** `Participer à un Sas Point Zéro`

**Accroche :**

> Quitte un instant la carte. Choisis une rencontre, éprouve le Point Zéro avec d'autres et
> repars avec une intention simple pour la suite.

**Séquence :**

1. `Choisir un Sas` — ouvre l'agenda filtré sur les prochaines rencontres Sas Point Zéro ;
2. `Vivre la rencontre` — la présence est reconnue par l'événement, avec confirmation humaine en
   repli ;
3. `Conserver mon intention` — une formulation courte est enregistrée comme Trace.

La consultation de l'agenda, l'inscription seule ou l'ouverture d'une page ne valident pas
l'expérience et n'attribuent aucun Ω.

## 4. Critères de cohérence

- `/sas` ne doit jamais être la destination d'un CTA relatif à une rencontre Sas Point Zéro.
- Un CTA `Choisir un Sas` mène vers l'agenda ou l'événement associé.
- Un parcours public reste achevable sans compte.
- L'import automatique est annoncé, restitué et idempotent.
- Les Ω importés gardent une provenance distincte de toute expérience du Monde 0.
- Aucun renommage technique du slug historique n'est requis pour livrer cette correction
  éditoriale.
