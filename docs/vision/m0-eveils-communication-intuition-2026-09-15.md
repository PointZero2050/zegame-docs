# M0 — étapes de découverte de Communication et d'Intuition

> **Note Codex — 15 septembre 2026.** Textes demandés par le poste fixe après
> l'arbitrage de Boris : chaque découverte de Puissance devient une étape de
> l'Expérience qui l'éveille et ramène ensuite à cette fiche.

## Règle commune

La fin du mini-jeu d'éveil constitue la preuve. Aucun champ `confirmation` ne
doit être ajouté. Le retour rend la fiche de l'Expérience, qui affiche la
reconnaissance du geste puis son CTA final ; il ne saute jamais directement à
l'Expérience suivante.

Cet enchaînement applique l'arbitrage transversal de Boris : toute action
lancée depuis une étape revient à la fiche afin que le joueur rende sa
progression consciente par ses propres clics. Une destination interceptée avant
un éveil n'est donc pas reprise automatiquement. Seule la file d'éveils peut
enchaîner le sas suivant lorsqu'une dette antérieure doit être traitée.

Les libellés suivent les verbes canoniques déjà portés dans
`config/puissances/*.yml`. Les fonctionnalités annoncées existent déjà dans les
écrans d'éveil ; d'autres usages s'ouvriront au fil des Mondes.

## E9 — rang 3 · Communication

```yaml
- verbe: "Découvrir"
  libelle: "Découvre la Puissance Communication"
  titre: "Découvre la Puissance Communication"
  duree: "5 min"
  accroche: "Ta première réaction a ouvert un espace entre toi et les autres."
  explication: "Tu viens de faire agir Communication : tu as rejoint un espace commun, reçu la parole d’un autre et choisi une réponse visible. Découvre comment cette Puissance circule entre J’ÉCOUTE, JE M’EXPRIME et JE CAPTIVE, et comment elle relie les Échanges, ton Profil et l’Annuaire au fil des Mondes."
  cta: "Découvrir Communication"
  revoir: "Revoir la découverte de Communication"
  sortie: "éveil de Communication achevé ; Communication présentée comme accès durable dans le menu Puissances."
  reconnaissance: "Tu as découvert la Puissance Communication."
```

L'Annuaire devient le rang 4, reste facultatif et prend l'accroche :
**« Une porte facultative vers les autres Joueurs. »** La durée totale d'E9
passe de 12 à **17 minutes** : 5 + 5 + 5 + 2.

## E12 — rang 4 · Intuition

```yaml
- verbe: "Découvrir"
  libelle: "Découvre la Puissance Intuition"
  titre: "Découvre la Puissance Intuition"
  duree: "5 min"
  accroche: "La clé que tu viens d’éprouver ouvre une autre manière de lire le Jeu."
  explication: "Tu viens de faire agir Intuition : tu as mis une proposition à l’épreuve au lieu de la prendre pour un verdict. Découvre comment cette Puissance circule entre JE DOUTE, JE DISCERNE et JE CROIS, et comment elle relie les Guides, les clés et la Ressourcerie au fil des Mondes."
  cta: "Découvrir Intuition"
  revoir: "Revoir la découverte d’Intuition"
  sortie: "éveil d’Intuition achevé ; Intuition présentée comme accès durable dans le menu Puissances."
  reconnaissance: "Tu as découvert la Puissance Intuition."
```

La durée totale d'E12 passe de 13 à **18 minutes** : 3 + 5 + 5 + 5.

## Libellés transversaux arrêtés dans la même relève

- Le retour canonique depuis une activité est **« Revenir à l'Expérience »**,
  avec une majuscule à `Expérience` et sans flèche. `Refermer le livre` ne reste
  valable que pour une action locale qui ferme le livre sans naviguer ; si le
  bouton rend directement la fiche, il prend le libellé canonique.
- Quand `proposer_graine` rend une carte sans texte du mentor, ne pas fabriquer
  une bulle ni une citation. La carte porte l'amorce neutre : **« Une Graine se
  dessine à partir de votre échange. »**
- La page `/parcours` ayant disparu, la consigne du mentor dit **« ton Voyage
  dans le Monde 0 »**, sans chemin technique. Le CTA Freeride qui mène à `/jeu`
  devient **« Revenir à mon Voyage »**.

## Raccords et recette

- Mettre à jour la durée en base dans la même mise en service que les nouveaux
  gestes ; la somme des gestes et la durée déclarée doivent rester identiques.
- Renuméroter l'ancienne confirmation d'Annuaire avant d'insérer le rang 3 d'E9.
- Préserver les expériences déjà validées et ne rejouer aucun gain.
- Vérifier pour E9 et E12 : geste déclencheur reconnu, rang d'éveil affiché,
  accès prématuré refusé, fin d'éveil prouvée une fois, retour à la même fiche,
  reçu puis CTA vers l'Expérience suivante, rejeu et autre onglet sans double
  validation.
