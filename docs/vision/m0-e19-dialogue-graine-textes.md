# M0 · E19 — dialogue final et Graine de passage

Décision éditoriale du 15 septembre 2026. E19 reprend la mécanique d’E13 : relecture des
productions, échange contextualisé avec le mentor, puis validation d’une Graine dans la fiche de
l’Expérience. La Carte du Seuil devient le quatrième geste.

La durée totale reste **30 minutes**. L’ancien bloc de 20 minutes est réparti entre 15 minutes de
dialogue et 5 minutes de formulation : **5 + 15 + 5 + 5 minutes**.

## Rang 2 — dialogue avec le mentor

```yaml
- verbe: "Relier"
  libelle: "ta traversée avec ton mentor"
  titre: "Relis ta traversée avec ton mentor"
  duree: "15 min"
  accroche: "Un passage apparaît quand tu relies ce qui a changé."
  explication: "Dialogue avec ton mentor à partir des Traces que tu viens de retrouver. Cherche avec lui ce que tu quittes, ce que tu accueilles et ce qui continue de t’appeler. Une contradiction peut rester ouverte : ton passage n’a pas à devenir une morale."
  cta: "Échanger avec mon mentor"
  revoir: "Revoir mon échange avec le mentor"
  sortie: "échange contextualisé à E19, pouvant faire émerger une proposition de Graine de passage."
  reconnaissance: "question du joueur enregistrée dans la consultation mentor ouverte depuis E19 ; la simple ouverture ne suffit pas."
```

Le rang 2 ne porte aucun champ `confirmation`. La question réellement enregistrée dans la
consultation E19 est sa seule preuve ; une déclaration du joueur ne peut pas la remplacer.

## Rang 3 — Graine de passage

```yaml
- verbe: "Semer"
  libelle: "ta Graine de passage"
  titre: "Formule ta Graine de passage"
  duree: "5 min"
  accroche: "Donne une forme à ce que tu choisis d’emporter."
  explication: "Relis la proposition née du dialogue, corrige-la si nécessaire ou écris ta propre formulation. Elle reste ta parole. En la plantant, tu l’inscris à la fois dans cette Expérience et dans ta Fresque."
  cta: "Planter ma Graine de passage"
  revoir: "Relire ma Graine de passage"
  sortie: "même Graine enregistrée sur E19 et rendue dans la Fresque selon ses règles de visibilité."
  reconnaissance: "Ta Graine de passage est semée."
```

Une écriture réelle et non vide prouve le rang. Une proposition seulement affichée, l’ouverture de
la popup ou le retour depuis le mentor ne valident rien. Corriger une proposition met à jour cette
même Graine ; cela ne crée ni doublon dans la Fresque, ni seconde preuve, ni nouveau gain.

## Microtextes communs à E13 et E19

### Popup du rang 3 préremplie par le mentor

> Ton mentor te propose cette formulation. Relis-la et corrige-la librement : elle ne devient ta
> Graine qu’au moment où tu choisis de la planter.

Le bouton conserve le `cta` du rang concerné : `Planter ma Graine de relation` pour E13 et
`Planter ma Graine de passage` pour E19.

### Carte « Graine possible » dans la page du mentor

> Cette proposition t’attend dans l’Expérience. Reviens-y pour la relire, la modifier et décider
> de la planter.

Libellé du lien : **`Revenir à l’Expérience`**.

Cette carte ne plante plus une proposition rattachée à E13 ou E19. Elle renvoie vers la fiche de
l’Expérience d’origine, où la popup du rang 3 appelle la même donnée. Sans provenance
d’Expérience, le comportement général de la Fresque reste inchangé.

## Séquence complète d’E19

1. **Rassembler** — Retrouve les traces de ta traversée · 5 min ;
2. **Relier** — Relis ta traversée avec ton mentor · 15 min ;
3. **Semer** — Formule ta Graine de passage · 5 min ;
4. **Sceller** — Ta Carte du Seuil · 5 min.

## Rang 4 — Carte du Seuil

Le rang 4 conserve son verbe, son titre, son accroche, son CTA et son libellé de relecture. Deux
champs périmés sont remplacés afin de ne promettre ni partage ni réglage de visibilité :

```yaml
explication: "Relis ta Graine de passage, choisis au moins une Trace à emporter avec elle, puis scelle ta Carte du Seuil. Cette Carte reste privée."
sortie: "Ta Carte du Seuil est scellée et reste privée. Rien n’est publié sur ton profil sans un geste séparé de ta part."
```

Son accroche reste donc : **« Donne une forme visible au passage accompli. »**
