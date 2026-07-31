# Refonte pointzero2050.com — révision éditoriale Livre I → Livre II

> Rédigé par Claude le 2026-07-31. Complément de
> https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/refonte-site-pointzero2050.md
> Décisions Boris actées : option A (migration complète avant l'ouverture des ventes fin août) ;
> le contenu du site, écrit sur la base du Livre I, doit être révisé à partir du Livre II
> (qui porte tout ce qui est aujourd'hui implémenté dans l'appli) AVANT la migration.

## 1. Sources

- **Livre II** : `Vibe Coding/Ressources Point Zero/Livres/PRT-Le Point Zéro - Livre II.docx`
  (version du 2026-07-07, ~1,25 M caractères, 533 sections en 5 parties). Le Livre III est en
  chantier (version du 2026-07-16) — non utilisé comme source pour cette révision.
- Structure du Livre II : Introduction (le Jeu cosmique, les deux récits) · I. L'Empire et la
  Cité cosmique (morphologies de civilisation, Chrysalides, les dix vagues) · II. Ombre et
  Lumière (pouvoir des récits, la marelle, avatars/Assemblée intérieure, les trois Jeux,
  Dr Z.E.R.O.) · III. La Transcendance (la Source, les sept Puissances JE SUIS → JE DONNE, la
  famille sacrée et le Moteur, le Point Oméga) · IV. La Marelle Oméga (les 10 mondes, les sept
  gardiens, le néoarchaïsme, les cadres capacitants, l'harmonie des besoins, le Pacte-Source) ·
  V. Révolution vibratoire (la redécision, les communautés Oméga, la roue civilisationnelle,
  les 5 transitions, la monnaie Oméga, le festival de 7 ans).
- **Appli PZ** (sandbox vibe.ze.game) : Monde 0 (13 expériences), Moteur, 6 fiches Puissances +
  162 archétypes, Conseil Oméga 2040, mini-jeu « Le coupable idéal », Cercles de croissance
  (spécifiés), Rôles d'appel (spécifiés), Oméga (comptabilité V1).

## 2. Constat : l'écart est structurel, pas cosmétique

Scan de présence des concepts Livre II / appli sur les 18 pages du cœur éditorial (accueil,
Comprendre ×6, Écosystème ×8, Formats, Cycle) :

- **0 page** ne mentionne : les (sept) Puissances, le Moteur, la marelle, les Mondes,
  l'Oméga, l'Empire / la Cité cosmique, le Jeu Cosmique comme récit-cadre.
- Le vocabulaire présent est celui du Livre I : « individuation alchimique » (6 pages),
  « cadres capacitants » (13 pages), « PsychoKernel » (1 page), processus en 5 phases,
  16 domaines civilisationnels.
- Une seule page (`/ecosysteme-commun/`) mentionne une « application ».
- Le site présente le PZ comme un **écosystème-méthodologie** (piliers, phases, domaines) ;
  le Livre II et l'appli le présentent comme un **Jeu** : un récit-cadre (Jeu cosmique,
  Empire/Cité cosmique), une école (la Marelle, les Mondes), des instruments (Moteur,
  Puissances, cadres), une économie (Oméga) et des collectifs (Cercles).
- Le « tunnel » narratif du site s'arrête à l'inscription à un événement ; il n'amène pas
  vers l'entrée dans le Jeu (Monde 0), qui est pourtant la porte d'entrée réelle du parcours.

Conclusion : réécrire page par page en gardant la structure actuelle serait un contresens.
La révision éditoriale et la refonte UX sont le même chantier : **le nouveau site raconte le
Jeu et y conduit**.

## 3. Inventaire typé des 105 pages + 33 articles

| Catégorie | Volume | Sort proposé |
|---|---|---|
| Cœur éditorial du menu (accueil, Comprendre ×6, Écosystème ×8, Ressourcerie ~15, Formats ×7, Cycle) | ~38 | **Réécriture** sur base Livre II (voir §4) |
| Articles de fond (série « Semaine n/52 » ×6 + articles thématiques ×27) | 33 | **Conserver** (blog/ressourcerie), toilettage léger de vocabulaire, assainissement iframes |
| Pages « Jeu Cosmique — Challenge 01-09 + Défi + index » (fév. 2026) | 11 | **Remplacées par l'appli** (c'est le prototype WP de ce que fait l'appli) — rediriger vers vibe.ze.game / l'appli festival |
| Formulaires WPForms (newsletter, préinscription NCF, concepts PZ, sprint pédagogique, livre 2, formats entreprise, amélioration site, suite webinaire) | ~8 | Refaire en natif Rails ; fusionner ce qui peut l'être |
| Pages contact (contact, champions, services, master classes, organiser un événement) | 5 | Fusionner en 1 page contact + motifs |
| Pages événements (ateliers présentiels/en ligne, sas, webinaire) | 4 | Remplacées par les pages événements de l'appli |
| Pages système WooCommerce/registration (panier, commander, mon compte, produit, transactions, thank you, registration checkout/cancelled, waiter, lab-rh, parcours, rejoindre) | ~12 | Remplacées par le tunnel Stripe Checkout de l'appli |
| Ateliers « questions » ×5 (mars 2025) | 5 | À fusionner dans les pages Comprendre réécrites ou supprimer |
| Orphelines 2024 (traumas collectifs, stratèges, pratico-inerte, scénarios ×2, cultures et civilisations, le point zéro, stratégies d'action) | ~8 | Trier : intégrer à la ressourcerie ou supprimer (redirections) |
| Tests (test, test-1, test-2, test-658), templates témoignages/CTA ×4, Homepage English | ~9 | Supprimer (les templates deviennent des partials) |

Les 5 scénarios du futur et les 4 cartographies (Pensées, Pratiques, Chrysalides, index) sont
comptés dans la Ressourcerie : contenus à **conserver et réécrire légèrement** — ils
correspondent aux 25 scénarios et à la Ressourcerie déjà intégrées dans l'appli
(`config/ressources/*.yml`), qui doivent devenir la source unique.

## 4. Architecture éditoriale cible (proposition à valider)

Principe : le site public devient la **couche d'appel du Jeu** — courte, incarnée, dans le
registre du Livre II et de la direction artistique de l'appli (collages néoarchaïques, atlas,
Moteur lumineux). Cinq ensembles au lieu de 5 rubriques × 40 entrées :

1. **Le Récit** (remplace « Comprendre ») — 3-4 pages incarnées : le point de bascule
   civilisationnel (les dix vagues, l'intercycle) ; l'Empire et la Cité cosmique (les deux
   morphologies) ; la Marelle et le Jeu cosmique (pourquoi un Jeu) ; s'appuyer sur les fiches
   pédagogiques existantes (73 collages produits par Codex) plutôt que sur de longs textes.
2. **Le Jeu** (nouveau, remplace « Écosystème » côté individus) — le parcours réel : Monde 0
   (entrer dans le Jeu), le Moteur et les 7 Puissances, les Mondes, les Cercles de croissance,
   l'Oméga. C'est la vitrine directe de l'appli, avec les visuels de l'atlas.
3. **Les Chemins** (remplace « Formats » + parcours Explorateur/Chrysalide/Vaisseau) —
   individus (Sas → Atelier → Monde 0), projets/Chrysalides, organisations/Vaisseaux ;
   événements et inscriptions intégrés (données de l'appli).
4. **La Ressourcerie** — conservée : articles (33), scénarios, cartographies, bibliographie,
   vidéos — servie depuis les mêmes sources que la Ressourcerie de l'appli (une seule source
   de vérité), avec la fiche « Gouvernance des communs » et le lot Pensées V2 de Codex.
5. **L'Alliance** (remplace « Écosystème » côté structure) — l'association, le commun,
   l'Incubateur, le Pacte-Source, le festival (NCF) et sa billetterie.

Le tunnel type : arriver par le Récit → vivre un avant-goût (extrait du mini-jeu « Le coupable
idéal » ou fiche interactive) → s'inscrire à un Sas/Atelier → créer son compte → Monde 0.

## 5. Méthode de travail proposée

1. **Pas de réécriture dans WordPress** : le travail éditorial produit directement le contenu
   du nouveau site (fichiers versionnés, probablement Markdown/YAML dans le dépôt de l'appli
   festival), WP restant en l'état jusqu'à la bascule (hors traitement de la compromission).
2. Rédaction par lots (un ensemble du §4 à la fois) : Claude propose, Boris relit et tranche.
   Sources : Livre II (extrait en texte intégral), fiches pédagogiques, corpus zegame-docs.
3. Chaque lot précise : pages remplacées, redirections 301, visuels (existants Codex ou à
   générer), CTA vers l'appli.
4. Les 33 articles : passe de toilettage (vocabulaire Livre II là où c'est naturel, liens vers
   le nouveau site) — pas de réécriture de fond.

## 6. Questions à trancher (Boris)

1. Valides-tu l'architecture cible en 5 ensembles (§4) et le principe « le site est la couche
   d'appel du Jeu » ?
2. Les 11 pages « Jeu Cosmique Challenge » WP : à archiver purement (redirection vers l'appli),
   ou certains contenus sont-ils à récupérer dans le Monde 0 ?
3. La page d'accueil doit-elle ouvrir sur le Récit (bascule civilisationnelle) ou sur le Jeu
   (l'expérience) ?
4. Le site cible est-il servi par l'appli festival elle-même (mêmes vues Rails) ou reste-t-il
   un front séparé ? (Recommandation : même appli — une seule pile, contenu versionné.)
5. Bilinguisme : l'anglais (page « Homepage-FR — English », titre du site) est-il un objectif
   pour cette refonte ou reporté ?
