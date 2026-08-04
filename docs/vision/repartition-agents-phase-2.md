# Répartition des agents — phase 2 (post-portage)> Actée par Boris le 2026-08-04. Version de référence, partagée entre agents et postes.> Le message de cadrage transmis à l'instance du poste fixe en est la mise en forme directe.
> PHASE 2 » de `PASSATION-CLAUDE.md`.

---

Bonjour,

Le portage est terminé et la migration réelle est faite : **`pointzero-app` est désormais
l'application de référence** (31 joueurs migrés avec leur progression, 927 Ω, Cercle et fils de
conversation). `vibe.ze.game` reste debout comme plan B, mais **plus rien de ce qui s'y joue ne
compte** — et surtout, **n'y édite plus aucun contenu pédagogique** : un réimport écraserait la
progression des joueurs sur la nouvelle application.

Ta caractérisation a servi exactement comme prévu : les sept documents ont guidé le portage, et
les cinq vérifications de parité des Puissances passent sur la nouvelle pile (§8 de
`caracterisation-puissances-monde-1.md`). Merci — le point que tu avais laissé ouvert sur
`update_columns` est tranché et documenté dans le code.

## Ton rôle en phase 2 (Boris, 2026-08-04)

Tu passes de la caractérisation à la **production** : intégration de pages, correctifs
éditoriaux, prototypage HTML, et **conception de mini-jeux**.

**Tu écris librement dans** : `zegame-prototypes` et `zegame-docs`.

**Dans `pointzero-app`, uniquement les zones de contenu** :
- `content/articles/` — les articles de fond en markdown (relations éditoriales dans
  `config/articles.yml`) ;
- `app/views/site/` — les pages du site public ;
- `public/sas/` — les parcours publics.

**Tu n'écris jamais** dans les modèles, les migrations, la configuration serveur, la
billetterie ni les contrôleurs applicatifs. Les déploiements passent tous par l'instance du
portable de Boris : elle seule porte la clé SSH du serveur Hetzner, et elle vérifie en
production. Si tu n'as pas d'accès en écriture au dépôt, travaille sur une branche — elle
fusionnera après relecture.

Principe, symétrique de celui de la phase 1 : **celui qui produit ne s'auto-valide pas.**

## Contrat d'intégration des mini-jeux

Ce qui a rendu l'intégration de tes cinq parcours du Sas parfaitement mécanique, formalisé —
applique-le aux mini-jeux :

1. **Dossier autonome** en kebab-case, ouvrable par simple `index.html`.
2. **Aucune dépendance externe** : pas de CDN, pas de framework, pas d'étape de construction.
   CSS en variables personnalisées, polices embarquées localement.
3. Un **`NOTES.md`** qui documente : les états simulés, les **données réellement attendues de
   l'application** (comptes, Ω, validation, progression), les **points de branchement**
   souhaités, et ce qui est délibérément hors périmètre.
4. **Persistance locale décrite explicitement** : clé, schéma, et ce qui ne doit jamais partir
   au serveur.
5. **Aucune donnée inventée** : un contenu éditorial manquant reste visiblement manquant plutôt
   que comblé — exactement comme tu l'as fait pour les neuf manifestations sans définition.

L'instance du portable branche ensuite routes, comptes, attribution des Ω et validation
d'expérience. **Le prototype reste la référence visuelle figée** : toute évolution de contenu
se décide chez toi puis se reporte dans l'application, jamais l'inverse.

## L'état de la nouvelle application, pour te situer

- **Site public** : `/` (accueil), `/comprendre`, `/ecosysteme`, `/le-jeu`, `/moteur`,
  `/cercle`, `/omega`, `/agir`, `/ressourcerie`, `/agenda`, `/entrer`, `/association`, plus les
  trois pages canoniques du Livre II et quatre articles appliqués sous `/ressources/`.
- **Le Sas** : `/sas` et `/sas/{scenarios,croyances,paralysie,reveil}` — tes cinq prototypes,
  intégrés tels quels, liens inter-parcours câblés.
- **Le jeu** (authentifié) : `/jeu` (accueil orchestrateur), `/parcours`, `/cercles`,
  `/profils`, `/ressources`, `/evenements`, `/users/me`.
- **Gestion** : billetterie complète (événements, inscriptions, gabarits, abonnés) et espace
  pédagogique (parcours, expériences, compétences) pour les administrateurs.

## Ce qui t'attend en priorité

1. **Les trous éditoriaux du Sas**, que ton `NOTES.md` avait honnêtement signalés : les
   définitions des neuf manifestations restantes (écran 7 du parcours humanité) et les exemples
   de relations multi-cycles manquants (écran 8).
2. **Les recommandations de fin de parcours** : le manifeste de Codex les demande (§4 et §10.2-3
   de `manifeste-connexion-puissances-marelle.md`) — trois suites au maximum par parcours, une
   page canonique, une page profonde, une action. Les trois pages canoniques existent
   désormais : `/le-moteur-et-les-sept-puissances`, `/la-marelle-depolarisateur-geant`,
   `/des-puissances-aux-cadres`.
3. **Les mini-jeux**, selon ce que Boris priorisera.

Bon travail — et n'hésite pas à signaler tout écart que tu constaterais entre un prototype et
son intégration : le prototype fait foi.
