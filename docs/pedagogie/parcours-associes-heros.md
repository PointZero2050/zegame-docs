# Parcours associés aux 48 Héros

**Statut : proposition éditoriale prête à relire**  
**Donnée source :** `docs/pedagogie/parcours-associes-heros.yml`

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
  parcours_slug: null
```

- `puissance` détermine la couleur et le libellé de la carte ;
- `titre` est l'appel visible ;
- `promesse` explicite le déplacement recherché ;
- `parcours_slug` reste `null` tant qu'un parcours réel du catalogue n'a pas été associé.

La proposition devient cliquable **uniquement** lorsque `parcours_slug` désigne un parcours
existant et accessible au Joueur. Avant cela, la fiche peut afficher les trois directions
comme horizons éditoriaux, sans faux CTA.

## 3. Règles UX

- Trois cartes maximum, toujours dans l'ordre des trois Puissances-phares.
- Une carte sans `parcours_slug` affiche `Direction de Voyage`, sans bouton.
- Une carte reliée affiche le CTA réel du parcours : `Découvrir le parcours` ou `Reprendre le
  parcours` selon l'état du Joueur.
- Le Monde minimal, la durée et l'intensité viennent du parcours réel ; ils ne sont jamais
  dupliqués dans le catalogue des Héros.
- Si le parcours n'est pas encore accessible, la carte peut annoncer le Monde d'ouverture,
  mais elle ne doit pas laisser croire que choisir le Héros le débloque.
- Le Héros colore une recommandation. Il ne valide rien, ne modifie aucun droit et ne produit
  aucun Oméga.

## 4. Cas du Monde 0

Les six mentors du Monde 0 conservent les trois associations déjà validées dans la maquette :
Cléopâtre, Aragorn, Léonard de Vinci, Marie-Madeleine, Socrate et Athéna. Elles renvoient aux
expériences du Monde 0 par leur titre éditorial, mais leurs `parcours_slug` restent à résoudre
contre les slugs réels avant portage.

Pour les 42 autres figures, les propositions sont volontairement formulées comme des chemins
de transformation. Elles pourront être reliées au catalogue Monde 1/2 au fur et à mesure de sa
construction, ou servir au moteur de recommandation pour proposer la variante la plus proche.

## 5. Portage attendu dans `pointzero-app`

1. Relire le lot éditorial avec Boris.
2. Résoudre, quand elles existent, les associations vers des slugs réels.
3. Porter les tableaux dans `config/heros/catalogue.yml`.
4. Ajouter le rendu conditionnel dans `app/views/heros/show.html.haml`.
5. Étendre `scripts/verifier_heros.rb` avec les invariants suivants :
   - 48 figures ;
   - exactement 3 propositions par figure ;
   - ordre identique à `puissances_phares` ;
   - titre et promesse non vides ;
   - tout `parcours_slug` non nul se résout vers un parcours réel ;
   - aucun CTA si le slug est nul ou inaccessible.

Le branchement touche la lecture d'un parcours mais pas sa progression. Il ne doit appeler aucun
callback de `Journey`, `Challenge`, `JourneysUser` ou `ChallengesUser`.
