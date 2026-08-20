# Lot éditorial de clôture de la coque Monde 0

> **Ajout Codex — 2026-08-20. Décisions de portage.**
> Cette note ferme quatre écarts relevés pendant le portage Rails : le passage vers l’Espace
> d’échange, la garantie de confidentialité de l’Annuaire, sept formulations défensives et la
> navigation vers les Événements depuis Intuition. Elle applique
> [voix-point-zero.md](voix-point-zero.md).

## 1. Passage vers l’Espace d’échange

Le titre canonique est :

> **Prends place parmi les autres.**

Il remplace `Une place, pas une scène.` La liste des droits et gestes qui suit reste inchangée.
La page affirme ainsi le mouvement proposé sans commenter une dérive supposée.

## 2. Confidentialité de l’Annuaire

La garantie concrète reste visible. Elle relève d’une limite de confidentialité et donc de
l’exception explicite à la règle d’écriture affirmative.

Texte canonique :

> **Une présence choisie.** Chacun choisit les éléments visibles de son profil. Adresse,
> téléphone, détail du Moteur et récits privés restent hors de l’Annuaire. Toute conversation
> individuelle commence par une demande acceptée.

La phrase `Chacun compose les éléments visibles de son profil` ne suffit pas seule : elle décrit
un mécanisme sans dire quelles données restent effectivement protégées.

## 3. Remplacements à porter dans Rails

Ces textes remplacent les formulations relevées dans `pointzero-app/preprod` le 20 août. Ils ne
changent aucune règle métier, aucun droit, aucun événement de transition et aucun banc autre que
ses assertions de copie.

| Surface | Texte canonique de remplacement |
|---|---|
| `heros/index` | `Choisis une personne, un personnage, une figure mythique ou un archétype pour ouvrir une perspective sur ton Voyage. Ton chemin évolue ; ton mentor peut évoluer avec lui.` |
| `heros/show` | `Une lecture éditoriale des Puissances que cette figure met en mouvement.` |
| `mentor/show` | `Laisse son regard éclairer l’endroit où la Puissance {nom de la puissance} cherche aujourd’hui à circuler dans ta vie — et ce qui l’en empêche.` |
| `attention/index`, état vide | `Rien n’attend de geste de ta part. Le terrain est libre.` |
| `users/_puissances` | `Le Conseil Oméga a posé un cap par Puissance. Ajuste-les selon les priorités que tu choisis aujourd’hui.` |
| `layouts/jeu`, infobulle Ω | `Tes Omégas gardent la trace de la Conscience mise en action.` |

### Alchimisation

La section négative entière devient une lecture positive :

```text
COMMENT LIRE CE DEGRÉ

Dix états nommés.
Ils rendent visible une dynamique à un instant donné.

Un repère personnel.
Deux personnes au même degré vivent des configurations différentes.

Une hypothèse de travail.
Elle se révise à chaque traversée et reste contestable.
```

Les informations importantes demeurent : l’indicateur n’est pas un pourcentage, la comparaison
entre Joueurs n’a pas de sens et la lecture reste hypothétique. Elles sont exprimées depuis ce que
le degré permet d’observer.

## 4. Contrat de navigation des Événements

Dans Intuition, `Événements` est une page du Jeu. Elle doit conserver la coque, le bouton des sept
Puissances, le sous-menu Intuition et le retour au métaparcours.

Le lien du sous-menu **ne doit pas pointer vers `/evenements`**, dont le contrat actuel est public
et dont le rendu utilise `layout "site"`. La cible technique est un index dédié dans le Jeu, par
exemple :

```text
GET /jeu/evenements
→ evenements_jeu#index
→ layout "jeu"
```

Les fiches d’événement déjà rendues dans le Jeu restent les destinations de cet index. Tant que
l’index interne n’existe pas, l’entrée reste annoncée sans lien plutôt que de faire basculer le
Joueur vers la coque du site.

### Critères d’acceptation

1. le lien `Événements` d’Intuition reste dans la coque du Jeu ;
2. retour et sous-menu conservent l’état Intuition ;
3. les événements réels déjà exposés sont listés, sans dupliquer leur source de vérité ;
4. une fiche revient à l’index interne ;
5. le Monde et les droits continuent de déterminer ce qui est visible ;
6. aucune visite ne valide une expérience, ne donne de badge ou d’Oméga ;
7. `/evenements` demeure la surface publique du site et garde son propre contrat.

La route et le contrôleur relèvent du portable. Le poste fixe porte ensuite la vue et la barre de
rubrique depuis la maquette validée.
