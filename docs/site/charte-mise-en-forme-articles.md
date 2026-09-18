# Charte de mise en forme des articles

> Note Codex — 18 septembre 2026. Cette charte fixe le contrat éditorial et
> typographique des articles publiés sur le site Point Zéro. Elle complète la
> [voix Point Zéro](../vision/voix-point-zero.md) sans modifier la voix propre
> de chaque auteur.

## 1. Principe

Un article Point Zéro se lit comme un texte, pas comme une suite de blocs
d’interface. La mise en forme rend le raisonnement visible, donne de l’air aux
phrases et garde une sortie claire. Elle ne transforme pas chaque idée en carte,
encadré ou effet graphique.

Le site sert trois familles :

- les **pages canoniques**, qui posent la grammaire du Point Zéro ;
- les **articles appliqués**, qui lisent cette grammaire depuis un public ou une
  situation ;
- les **chroniques**, qui racontent le chantier depuis l’intérieur, avec ses
  essais, ses contradictions et ses détours.

## 2. Structure du fichier

Le contenu vit dans `content/articles/<slug>.md`.

1. Un seul titre de niveau 1, sur la première ligne : `# Titre`.
2. Un chapeau de un à trois paragraphes avant le premier titre de niveau 2.
3. Des sections `##` chaque fois que l’argument change. Pour un article long,
   trois à sept paragraphes par section donnent un bon rythme.
4. Des sous-sections `###` seulement lorsqu’une section porte plusieurs idées
   distinctes. Ne jamais sauter un niveau de titre.
5. Une conclusion qui ferme le mouvement du texte avant l’appel à l’action.
   Le CTA principal est déclaré dans `config/articles.yml`, pas répété dans le
   corps.

Les titres restent en casse phrase. Ils peuvent porter la voix de l’auteur,
mais doivent annoncer le mouvement de la section.

## 3. Paragraphes et rythme

- Un paragraphe porte une idée ou un mouvement narratif.
- Les paragraphes courts créent du rythme ; leur accumulation ne doit pas
  transformer le texte en fil de réseau social.
- Aucun `<br>` ne sert à fabriquer de l’espace. Les espacements appartiennent à
  la feuille de style.
- Un paragraphe composé uniquement de texte gras devient une **phrase pivot**.
  Deux à quatre pivots suffisent dans un article long.
- Une liste sert des éléments réellement parallèles. Une succession de phrases
  qui forme un raisonnement reste en prose.

## 4. Emphase et citations

- L’italique signale un titre d’œuvre, un terme étranger ou une inflexion de
  voix brève.
- Le gras nomme un concept ou une phrase pivot. Il ne sert pas à surligner une
  phrase sur deux.
- Le bloc de citation (`>`) est réservé à une parole effectivement citée. La
  source est indiquée lorsqu’elle est publique.
- Les guillemets français `« … »` sont utilisés dans le texte courant.

## 5. Liens, sources et images

- Le libellé d’un lien annonce sa destination. Éviter « cliquez ici ».
- Une affirmation factuelle centrale renvoie, lorsque c’est utile, vers une
  source primaire ou institutionnelle.
- Les liens de contexte restent dans le corps ; l’action principale reste le
  CTA unique de la configuration.
- Une image doit ajouter une information, une scène ou une respiration
  nécessaire. Elle porte un texte alternatif et, si besoin, une légende et un
  crédit. Une image purement décorative n’est pas ajoutée pour remplir un vide.

## 6. Typographie française

- apostrophe typographique `’` dans les textes visibles ;
- accents sur les capitales : `É`, `À`, `Ç` ;
- ligature `œ` dans `cœur`, `œuvre`, `vœu` ;
- espaces insécables avant `:`, `;`, `?`, `!` au rendu ;
- tiret cadratin pour une incise forte, avec mesure ;
- nombres, dates et unités écrits de manière cohérente dans tout l’article.

## 7. Déclaration éditoriale

Chaque article possède une entrée dans `config/articles.yml` :

```yaml
mon-slug:
  nature: chronique # canonique, article ou chronique
  rubrique: Chronique du Point Zéro
  canonique_amont: le-moteur-et-les-sept-puissances
  cta:
    libelle: "Découvrir le rendez-vous"
    url: /agenda
```

Le slug est également autorisé par la route `ressources/:slug`. Une page
canonique dispose de sa propre route racine. Un texte juridique utilise la
nature `legal` et reste hors du sommaire éditorial.

## 8. Rendu commun

La vue extrait le titre du Markdown pour le placer dans le héros. Elle affiche
ensuite la rubrique et un temps de lecture calculé. Le chapeau a un corps plus
grand ; les titres de section, phrases pivots, citations, listes, liens et
images suivent les styles communs de `.article-fond`.

La largeur de lecture reste limitée. La mise en forme doit fonctionner sans
JavaScript et sur mobile. Les composants spéciaux sont introduits seulement
quand le contenu les exige et rejoignent alors cette charte.

## 9. Revue avant publication

- Le titre n’apparaît qu’une fois dans la page rendue.
- Le chapeau permet de comprendre la promesse de lecture.
- La hiérarchie `h2` / `h3` est continue et descriptive.
- Les phrases pivots restent rares.
- Les liens sont explicites, valides et accessibles au clavier.
- Les faits sensibles ont une source et les formulations datées ont été
  revérifiées.
- La ponctuation, les apostrophes, les noms propres, les nombres et les dates
  ont été relus.
- Le CTA de configuration est unique et correspond à la suite réelle.
- La page figure dans `/articles`, répond sans compte et reste lisible sur
  grand et petit écran.
- Un banc de publication garde la route, le titre, les sections, le CTA et
  l’absence de doublon du `h1`.

