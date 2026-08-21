# Parcours associés aux 48 Héros

**Statut : contrat porté en production (`894fa36`)**
**Donnée source :** `docs/pedagogie/parcours-associes-heros.yml`

> Le YAML de ce dépôt reste le lot éditorial v1, avec `parcours_slug: null`. L'application a
> migré son catalogue vers la forme typée `cible` décrite ci-dessous. Les 144 directions
> éditoriales, leur ordre et leurs Puissances ne changent pas.

## 1. Finalité

La fiche d'un Héros ne doit pas s'arrêter à l'inspiration. Elle ouvre trois directions
d'expérience : une par Puissance-phare de la figure, dans l'ordre **Puissance principale →
deux Puissances d'appui**.

Ces propositions répondent à trois fonctions :

1. traduire une figure en mouvement possible pour le Joueur ;
2. montrer qu'une même figure ne se réduit pas à sa Puissance principale ;
3. préparer la recommandation de parcours à partir du Monde 2, sans faire du Héros un modèle
   à imiter.

Le titre et la promesse décrivent une **direction pédagogique**, pas encore une destination
technique. Le fichier ne crée donc ni route, ni progression, ni validation, ni Oméga.

## 2. Contrat de donnée proposé

Chaque item porte :

```yaml
- puissance: intuition
  titre: "Voir ce que tous regardent"
  promesse: "Ralentir assez pour distinguer le détail décisif..."
  cible: null
```

- `puissance` détermine la couleur et le libellé de la carte ;
- `titre` est l'appel visible ;
- `promesse` explicite le déplacement recherché ;
- `cible` reste `null` tant qu'une destination réelle de l'application n'a pas été associée.

La proposition devient cliquable **uniquement** lorsque `cible` désigne un objet existant et
accessible au Joueur. Avant cela, la fiche peut afficher les trois directions comme horizons
éditoriaux, sans faux CTA.

Forme canonique :

```yaml
cible:
  type: experience # experience | parcours | page | rubrique
  slug: le-conseil-omega
```

`type` évite de faire passer une expérience, une page ou une rubrique pour un parcours. `slug`
est un identifiant métier stable ; une URL brute n'est jamais stockée dans le catalogue. Une
`page` ou une `rubrique` se résout également par un registre explicite de destinations.

Deux règles complètent cette forme :

- une cible `experience` se résout dans le parcours réel qui contient l'expérience. Si aucun
  parcours ne la contient, ou si plusieurs parcours la contiennent, la résolution renvoie `nil`
  plutôt que d'inventer un contexte ;
- une cible `page` ou `rubrique` doit rester dans la coque du Jeu. Une route homonyme du site
  public n'est jamais un repli acceptable.

## 3. Règles UX

- Trois cartes maximum, toujours dans l'ordre des trois Puissances-phares.
- Une carte sans `cible` affiche `Direction de Voyage`, sans bouton.
- Une carte reliée affiche le CTA réel de sa destination : `Découvrir l'expérience`,
  `Découvrir le parcours`, `Ouvrir la page` ou `Explorer la rubrique`.
- Le Monde minimal, la durée et l'intensité viennent de la destination réelle ; ils ne sont jamais
  dupliqués dans le catalogue des Héros.
- Si le parcours n'est pas encore accessible, la carte peut annoncer le Monde d'ouverture,
  mais elle ne doit pas laisser croire que choisir le Héros le débloque.
- Le Héros colore une recommandation. Il ne valide rien, ne modifie aucun droit et ne produit
  aucun Oméga.

## 4. Cas du Monde 0

Les six mentors du Monde 0 conservent les trois associations déjà validées dans la maquette :
Cléopâtre, Aragorn, Léonard de Vinci, Marie-Madeleine, Socrate et Athéna. Quinze directions
renvoient à des expériences réelles du Monde 0. Deux renvoient à des surfaces existantes :
`Explorer la Ressourcerie` est une rubrique et `Mon Moteur` une page. `Qu'est-ce qui nous
paralyse ?` reste une Direction de Voyage sans CTA tant qu'aucune destination réelle n'existe.

Le portage utilise donc `cible.type` : `experience` pour les quinze expériences, `rubrique`
pour la Ressourcerie, `page` pour le Moteur et `null` pour la direction d'Athéna. Il ne crée
jamais un faux `Journey` pour rendre ces cartes cliquables.

Les deux surfaces non pédagogiques se résolvent vers les têtes de territoire internes :

- `Explorer la Ressourcerie` → `/premieres-cles` ;
- `Mon Moteur` → `/users/me`.

Les routes publiques `/ressourcerie` et `/moteur` sont explicitement exclues : elles feraient
sortir le Joueur de la coque.

Pour les 42 autres figures, les propositions sont volontairement formulées comme des chemins
de transformation. Elles pourront être reliées au catalogue Monde 1/2 au fur et à mesure de sa
construction, ou servir au moteur de recommandation pour proposer la variante la plus proche.

## 5. Contrat de portage dans `pointzero-app`

Ce contrat est porté en production depuis `894fa36`. La liste suivante reste le banc de
non-régression du dispositif.

1. Conserver les tableaux dans `config/heros/catalogue.yml`.
2. Résoudre uniquement les associations vers des cibles réelles typées et internes au Jeu.
3. Maintenir le rendu conditionnel dans `app/views/heros/show.html.haml`.
4. Maintenir dans `scripts/verifier_heros.rb` les invariants suivants :
   - 48 figures ;
   - exactement 3 propositions par figure ;
   - ordre identique à `puissances_phares` ;
   - titre et promesse non vides ;
   - toute `cible` non nulle se résout vers un objet réel du type annoncé ;
   - aucun CTA si la cible est nulle ou inaccessible.

Le branchement touche la lecture d'un parcours mais pas sa progression. Il ne doit appeler aucun
callback de `Journey`, `Challenge`, `JourneysUser` ou `ChallengesUser`.
