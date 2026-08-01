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

## 2 bis. CORRECTION DE CADRAGE — les trois Livres sont trois niveaux, pas trois versions

> Ajout Claude, 2026-07-31, après retour de Boris. **Cette section corrige le §2 ci-dessus**,
> qui concluait trop vite que le contenu Livre I était périmé. Il ne l'est pas : il est la
> rampe d'accès sans laquelle le Livre II est inaudible.

L'œuvre se déploie sur trois niveaux complémentaires :

- **Livre I — le diagnostic.** Histoire humaine, causes profondes des crises, impuissance de
  l'humanité malgré son pouvoir technique. Vision **neutre**, qui accueille tous les
  imaginaires possibles via les 25 scénarios. C'est la face « universitaire » de l'œuvre :
  elle donne les clés de décodage et fait passer d'une conscience superficielle à une
  conscience systémique.
- **Livre II — la grammaire de la Conscience.** Accessible seulement aux lecteurs du Livre I.
  Pensée métaphysique qui **prend parti** pour un scénario de transcendance : matrice
  cosmogonique, multivers, plan archétypal, niveaux de réalité, et la Marelle Oméga — base de
  la fractale de résorption de l'Empire dans la Cité Cosmique. C'est lui qui comble la faille
  d'action reprochée au Livre I, en traitant le fond du problème (la polarisation) et en
  l'opérationnalisant par des parcours.
- **Livre III — le plan d'action** (en chantier) : les 7 ans à venir puis 2050, avec les
  transitions épistémologique, anthropologique, organisationnelle et économique.

### Le modèle des 5 niveaux de conscience systémique

Référence : `Ressources Point Zero/Modèles/Niveaux-conscience-systemiques.png`. Cinq lectures
des crises, chacune avec sa perception, ses solutions et ses acteurs :

| Niveau | Perception | Solutions typiques | Acteurs |
|---|---|---|---|
| 1. Superficiel | Manque de sensibilisation | Campagnes, information, médias | Organisations, pouvoirs publics, médias |
| 2. Introspectif | Enjeux internes, biais cognitifs | Coaching, thérapie, développement personnel, fresques | Entreprises progressistes, thérapeutes |
| 3. Systémique | Cadres invisibles qui déterminent les comportements | Culture organisationnelle, sociocratie, cadres capacitants | Consultants, facilitateurs |
| 4. Holistique | Conditionnement anthropologique, traumas collectifs | Raison d'être civilisationnelle, guérison collective, nouvelles croyances | Chercheurs interdisciplinaires, prospectivistes |
| 5. Hyperconscience | Enfermement dans une histoire prise pour le réel | Cosmogénèse générative, pratiques transcendantales, ingénierie civilisationnelle | Praticiens, communautés hyperconscientes |

Ce modèle est le pont manquant entre les Livres : il explique **pourquoi** les solutions
courantes sont réelles mais insuffisantes, sans les disqualifier. Il est aussi la meilleure
réponse au reproche « le Point Zéro manque d'action » : ce n'est pas l'action qui manque
ailleurs, c'est le niveau auquel elle s'applique.

### Conséquence pour le site

Le site ne remplace pas la couche Livre I par la couche Livre II : il **superpose** les deux
et laisse le visiteur entrer par où il en est.

- Pour celles et ceux qui sont déjà prêts et veulent agir vite : un tunnel d'engagement court
  vers le Jeu et les formats.
- Pour les autres : de la matière Livre I en quantité, pour entrer dans le sujet et monter en
  conscience systémique.

Le §2 reste valable sur un point : le site actuel ne dit **rien** du Jeu, du Moteur, des
Puissances ni des Mondes, et son tunnel s'arrête à l'inscription. Il manque la couche haute,
pas la couche basse.

## 2 ter. Décisions Boris — 2026-07-31 (2e série)

1. **Trois portes + une introduction générale.** L'accueil pose d'abord l'intention de
   l'écosystème (support pressenti : la **vidéo teaser Écosystème PZ**, script dans
   `Ressources Point Zero/Vidéos/Vidéo teaser Ecosystème PZ.docx`, versions longue et courte),
   puis oriente vers trois portes : agir / comprendre / porter un projet ou une organisation.
2. **Les 5 niveaux deviennent un dispositif public** : un petit jeu d'auto-positionnement qui
   oriente vers le contenu adapté du site ou directement vers l'appli. Aujourd'hui absent
   partout. Articulation avec les trois portes : voir §4 bis.
3. **Dispositifs sans cosmogonie.** Marelle, Moteur, Puissances et Cercles sont présentés comme
   des dispositifs opérationnels. La Source, le multivers et le plan archétypal restent dans
   les Livres et dans le Jeu.
4. **La promesse d'action s'appuie sur le Jeu ET le plan**, à condition de filtrer les aspects
   métaphysiques trop marqués. **Les dix vagues technospirituelles ont toute leur place** :
   c'est une interprétation historique défendable, qui inclut toutes les approches et
   traditions spirituelles sans en imposer une.
5. **Tutoiement confirmé de fait** : le script du teaser tutoie déjà (« toi qui regardes cette
   vidéo », « est-ce que tu es prêt à prendre ta place »).

## 3 bis. Ancrage dans la vision-cible de l'application

Lecture faite de l'index [README.md](README.md) et des documents structurants. Ce que la
vision-cible impose au site :

- **Le site est l'amont de l'« accueil orchestrateur »** décrit dans
  [accueil-point-zero.md](accueil-point-zero.md) : l'accueil de l'appli répond à « Où suis-je ?
  Que se passe-t-il ? Quel est mon prochain pas ? » pour un joueur connecté. Le site public
  répond aux mêmes trois questions pour le visiteur *pas encore joueur* — son unique issue
  naturelle est « Entrer dans le Monde 0 » (état « Nouveau Joueur » de l'accueil). Le site et
  l'accueil forment un seul tunnel, pas deux univers.
- **Mode événement / Festival** : accueil-point-zero.md prévoit l'entrée événementielle
  « très courte, via invitation, lien ou QR code ». La page Festival du site (et sa
  billetterie) est exactement cette porte latérale — elle doit déboucher sur le flux
  d'inscription de l'appli, pas sur un tunnel WooCommerce parallèle. Cohérent avec l'option A.
- **Charte de voix** ([voix-point-zero.md](voix-point-zero.md)) : lucide, provocatrice,
  décalée, complice sans complaisance ; sortie de la voix « Enfant Adapté » ; test rapide :
  « si le texte pourrait être publié par une plateforme de bien-être, il n'est pas encore
  Point Zéro ». Le contenu actuel du site échoue à ce test sur la quasi-totalité des pages
  (registre encyclopédique-inspirationnel). La réécriture Livre II doit appliquer cette charte,
  avec le dosage par surface prévu (pages narratives : torsion forte ; inscription/paiement :
  clarté littérale, jamais d'humour qui masque une conséquence).
- **Direction artistique** ([direction-artistique-point-zero.md](direction-artistique-point-zero.md)) :
  coque produit stable (violet PZ, composants) + grammaire néoarchaïque (collages, matière,
  vides actifs, glyphes) + grain de sabotage discret. Le site doit adopter la même coque que
  l'appli — c'est l'argument décisif pour qu'il soit servi par la même pile (question 4 du §6).
  Les assets existent déjà : 73 fiches pédagogiques, 162 médaillons d'atlas, covers Ressourcerie,
  emblèmes des Rôles d'appel.
- **Navigation cible de l'appli** (accueil-point-zero.md : Accueil · Marelle · Cercle ·
  Ressources · Profil) : la Ressourcerie du site et celle de l'appli doivent être la même vue
  avec deux niveaux d'accès (public / joueur), pas deux copies.
- **Réserve** : le README de la vision rappelle qu'hors application-festival-2026.md (décision
  opérationnelle) ces documents sont un horizon, pas une spécification. Le site ne doit
  vitrine-iser que ce qui existera au festival (Monde 0, Moteur, Puissances, Cercles V1,
  événements) — pas le monde-miroir ni la marketplace.

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

## 4 bis. Trois portes et auto-positionnement : deux axes, pas deux choix

Question de Boris : le jeu d'auto-positionnement contredit-il les trois portes ? **Non — à
condition qu'ils ne se disputent pas le même moment du parcours.** Ils opèrent sur deux axes
orthogonaux :

- **Les trois portes = l'axe de l'intention.** « Qu'est-ce que je veux faire maintenant ? »
  C'est un choix, fait par le visiteur, instantané et sans engagement.
- **Les cinq niveaux = l'axe de la lecture.** « Comment est-ce que je lis le problème
  aujourd'hui ? » Ce n'est pas un choix mais un **miroir** : un dispositif le renvoie, en deux
  minutes, avec une sortie qui est un aiguillage de contenu.

Les deux axes sont indépendants : on peut lire les crises au niveau 2 et vouloir agir tout de
suite, comme on peut être au niveau 4 et vouloir d'abord comprendre. La contradiction
n'apparaîtrait que si les deux étaient placés au même endroit — deux portiques « situe-toi »
à l'entrée, ce qui ferait fuir tout le monde.

**Règle de conception retenue :** un seul choix à l'entrée (les trois portes), le jeu
d'auto-positionnement comme dispositif *à l'intérieur*.

- Il est le **moteur de la porte « Je veux comprendre »** — exactement le public qui a besoin
  d'un miroir avant d'avoir besoin d'un catalogue.
- Il reste accessible depuis n'importe où par une entrée secondaire permanente.
- Sa sortie peut **renvoyer vers n'importe laquelle des trois portes**, y compris « agir ».
  C'est donc lui qui convertit un visiteur « comprendre » en visiteur « agir » quand il est
  prêt, au lieu de le laisser lire indéfiniment.

Formulation : *les portes sont la carte, le jeu est la boussole.*

### Garde-fous d'écriture du jeu d'auto-positionnement

- On ne classe **jamais une personne**, on caractérise **une lecture** : « voici la lecture qui
  te parle le plus aujourd'hui », pas « tu es niveau 1 ».
- Chaque niveau est présenté comme **réel et partiel** : ce qu'il explique bien, ce qu'il ne
  voit pas encore. Les acteurs cités au niveau 1 et 2 ne sont pas des naïfs : ce sont
  souvent les visiteurs eux-mêmes, et parfois les partenaires du Point Zéro.
- Pas de score, pas de rang, pas de progression affichée : une lecture, ses angles morts, et
  une porte de sortie.
- Le dispositif doit passer le test de la charte de voix : s'il ressemble à un quiz de magazine
  ou à un diagnostic de cabinet de conseil, il est raté.

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
