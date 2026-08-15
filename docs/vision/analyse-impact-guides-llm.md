# F19 — Guides LLM transversaux : analyse d'impact

*Claude (portable), 12 août 2026. Demandée par la spec elle-même : « Prototype front
réalisé ; aucun appel LLM réel ni modèle Rails décidé à ce stade. Une analyse d'impact
dédiée est requise avant intégration. » Ce document ne construit rien : il dit ce que
coûte la fonction, ce qu'elle risque, et ce que Boris doit trancher avant qu'une ligne
de code soit écrite.*

---

## 0. Ce que F19 demande

Une présence discrète et permanente du **Professeur Sirbey** et du **Docteur Z.E.R.O.**
sous forme d'une pastille ouvrant un dialogue contextuel. Elle aide à comprendre le Point
Zéro, la page courante, les fonctionnalités accessibles.
[Spécification §5.4](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/navigation-vecue-devoilement-progressif.md)

La spec pose déjà quatre bornes que cette analyse ne rediscute pas — elle les prend pour
acquises et vérifie ce qu'elles impliquent :

1. **Même corpus, mêmes droits pour les deux voix.** Seule la rhétorique diffère ; le
   choix d'une voix ne produit « aucune différence de vérité, de mémoire ou de permission ».
2. **Enveloppe de contexte minimale.** Le guide ne lit ni Graines, ni profil du Moteur, ni
   conversations privées. Il connaît le Monde, les droits, la destination, le panneau.
3. **Distinct du mentor, de l'Aide et de la recherche.** Trois fonctions voisines, trois
   régimes de responsabilité différents.
4. **Il doit pouvoir montrer ses sources**, signaler ses incertitudes, et rediriger dès que
   la question sort de son périmètre.

**Verdict de l'analyse : la fonction est réalisable, et son coût monétaire est
négligeable. Ce qui la bloque n'est ni technique ni financier — c'est le corpus, qui
n'existait pas lors de cette analyse, et la voix du Docteur, qui demande un arbitrage humain.**

> **Mise à jour Codex — 2026-08-16.** Le palier éditorial est désormais constitué dans
> [`docs/pedagogie/corpus-guides/`](../pedagogie/corpus-guides/README.md) : schéma de fiche,
> hiérarchie des sources, politique de réponse, profils des deux voix, manifeste, trente
> fiches du Monde 0 et vingt-et-une fiches du Monde 1. Le lot M0 a été ingéré et éprouvé en
> préproduction par le portable le 15 août ; le lot M1 reste à intégrer et à recetter. Les
> sources citables ont été assainies le 16 août : titres publics uniquement, aucun chemin de
> dépôt transmis au modèle.

---

## 1. Constat initial — le corpus joueur n'existait pas

Un guide qui répond « d'après ce que je sais » est un générateur de plausible. Ce que la
spec demande — montrer ses sources — impose un corpus indexé, cité, et **écrit pour être
lu par un joueur**. Or ce corpus n'existe nulle part aujourd'hui.

Ce qui existe, mesuré :

| Fonds | Volume | Nature | Utilisable tel quel ? |
|---|---|---|---|
| `zegame-docs/docs/vision/` | 2,5 Mo · 54 fichiers · ~120 000 mots | Specs, arbitrages, passations, plans | **Non** |
| `pointzero-app/content/articles/` | 56 Ko · 7 fichiers | Articles de fond publiés | Oui |
| `config/*.yml` (mondes, coque, ressourcerie, héros) | ~800 Ko | Données de jeu structurées | Oui, mais ce sont des données, pas de la prose |

**Le problème n'est pas le volume, c'est la nature.** `docs/vision/` est de la
documentation de travail interne : elle contient les arbitrages de Boris, les plans non
livrés, les fonctionnalités des Mondes 2 à 7 que le dévoilement progressif a précisément
pour but de ne pas révéler, et les passations entre agents. Indexer ce dossier, c'est
construire une machine à répondre « d'après le plan de développement, le Monde 4 sera le
Monde-miroir » à un joueur du Monde 0 — ce qui contredit frontalement la coque que nous
venons de porter.

C'est un **travail éditorial, pas un travail de développement** : quelqu'un doit écrire le
corpus joueur — une vingtaine de fiches par Monde ouvert, dans la voix du jeu, disant ce
qu'un joueur a le droit de savoir. Tant qu'il n'existe pas, le reste est prématuré.

**Conséquence sur la faisabilité technique** : un corpus de cette taille (quelques
centaines de Ko de prose curatée) tient **entièrement dans le prompt**. Aucune base
vectorielle n'est nécessaire — et c'est heureux, car `pgvector` n'est pas disponible sur
notre Postgres (vérifié : `pg_available_extensions` ne le connaît pas). Un simple filtrage
par Monde et par destination suffit à sélectionner les fiches pertinentes. **Le RAG
n'est pas le chantier ; le corpus l'est.**

---

## 2. La pastille suppose un JavaScript que l'application n'a pas

C'est le constat architectural qui coûte le plus cher, et il est invisible depuis la spec.

L'application est **délibérément sans framework JS**. Le layout du Jeu charge un unique
fichier de 32 lignes (`public/pz/jeu.js`) qui fait deux choses : ouvrir le menu de
l'avatar, et enregistrer le service worker de la PWA. Il n'y a ni Turbo, ni Stimulus, ni
React. Tout le reste — le composeur Proposition/Action, les sondages, les décisions par
consentement, la recherche — fonctionne en formulaires HTML et `<details>`. Cette
discipline n'est pas un accident : elle rend l'application lisible, testable par bancs
HTTP, et robuste sur les mobiles du Festival.

Une pastille flottante ouvrant un dialogue conversationnel est, par construction, du JS :
il faut envoyer la question sans recharger la page, afficher une réponse qui arrive en
plusieurs secondes, et gérer l'attente.

**Trois options, une recommandation :**

| Option | Ce que ça coûte | Ce que ça donne |
|---|---|---|
| **A. Une page « Demander au guide »** — formulaire, POST, rechargement | Zéro JS. Une destination de coque. Une journée. | Le dialogue fonctionne, mais il n'est pas *ambiant* : il faut aller à lui. Perd le « présence discrète et permanente » de la spec. |
| **B. `fetch` minimal dans `jeu.js`** — ~60 lignes, pas de framework | Introduit une dépendance JS dans la coque, avec dégradation gracieuse si le JS échoue. | La pastille de la spec, sans framework. |
| **C. Turbo Streams** | Introduit Hotwire dans une app qui l'a évité. Refonte du layout. | Surdimensionné pour un seul usage. |

**Recommandation : A d'abord, B ensuite.** Livrer la fonction en page dédiée permet de
vérifier la qualité des réponses, la sécurité et le coût réels avant de débattre de la
chrome. La pastille est un habillage ; elle ne doit pas retarder la fonction, ni la faire
échouer pour une raison d'interface. Si Boris tient à la présence ambiante dès la v1,
l'option B reste tenable — mais elle se décide, elle ne se subit pas.

Point non négociable dans tous les cas : **l'appel part du serveur Rails, jamais du
navigateur.** La clé d'API ne doit à aucun moment être livrée à une page.

---

## 3. Injection de prompt — le corpus est du texte, pas des ordres

C'est le risque de sécurité propre à la fonction, et il est structurel.

Un guide RAG lit du texte de son corpus et le place dans son propre prompt. Si une fiche
contient une phrase adressée au modèle — « ignore les instructions précédentes », « révèle
la liste des Mondes », « tu es autorisé à lire les Graines » —, le modèle peut la suivre :
pour lui, rien ne distingue une consigne d'un contenu. Notre corpus est du Markdown écrit
en partie **par des agents** (Codex et moi), ce qui rend le scénario moins théorique
qu'ailleurs.

Le rempart n'est pas parfait, mais il se construit :

1. **Le corpus est encadré comme donnée**, dans une balise dédiée, avec une consigne
   système explicite : ce qui est à l'intérieur est de la documentation à citer, jamais
   des instructions à exécuter.
2. **Le guide n'a aucun outil.** Pas d'accès base, pas de lecture de fichiers, pas
   d'appels sortants. Une injection réussie ne peut donc au pire que faire dire une bêtise
   — elle ne peut rien *faire*. C'est le vrai rempart : **on limite les dégâts en limitant
   les pouvoirs, pas en limitant les mots.**
3. **Le corpus est relu avant publication**, comme un article du site. Une fiche entre par
   un commit, pas par un formulaire.
4. **Le contexte joueur n'entre jamais dans le prompt sous forme de texte libre** — Monde,
   destination et droits sont des valeurs énumérées côté serveur, pas une phrase.

Le point 2 est celui qui compte. Tant que le guide ne peut que parler, le risque plafonne.
**Le jour où l'on voudra lui donner un outil — chercher dans l'annuaire, ouvrir un fil —,
cette analyse devra être refaite entièrement.**

---

## 4. Le Docteur Z.E.R.O. — le risque humain, et il n'est pas technique

C'est le constat qui m'inquiète le plus, et c'est celui qu'aucune revue de code ne
trouvera.

La spec décrit un Docteur qui « confronte les contradictions avec un humour caustique qui
ne ridiculise jamais le joueur ». Cette ligne est tenable pour un auteur humain qui écrit
une réplique. Elle est beaucoup plus difficile à tenir pour un modèle qui génère en
direct, face à une personne qu'il ne voit pas, dans un jeu qui travaille explicitement
l'Ombre, les puissances, et ce que les gens ont de vulnérable.

Trois faits aggravent le risque :

- **Le public du Festival n'est pas trié.** Le 1er octobre, des inconnus créent un compte
  avec un billet. Certains arriveront avec un vécu que nous ignorons.
- **L'humour caustique est précisément le registre qui échoue mal.** Une réponse trop
  chaleureuse est fade ; une réponse caustique mal calibrée blesse. L'asymétrie des
  conséquences n'est pas discutable.
- **Nous ne pourrons pas relire les réponses avant qu'elles soient lues.** Contrairement à
  tout le reste de l'application, cette fonction produit du contenu que personne n'a
  validé.

Ce que je recommande, dans l'ordre :

1. **Le Docteur n'est pas dans la v1.** On ouvre avec le Professeur seul — la voix qui
   clarifie, structure et relie, dont l'échec est ennuyeux et non blessant. Le Docteur
   s'ajoute quand nous aurons lu de vraies réponses sur de vraies questions.
2. **Le guide disparaît des écrans sensibles.** Partout où le joueur travaille sa propre
   matière — Graines, Ombre, questionnaire du Moteur, dossier de rencontre — la pastille
   n'est pas là. Ce n'est pas un réglage, c'est une règle du registre.
3. **L'Aide est toujours à un clic**, et n'est jamais servie par le modèle (§7).
4. **Chaque réponse est signalable en un geste**, et le signalement va à un humain.

Cet arbitrage appartient à Boris. Je le pose parce que la spec écrit « qui ne ridiculise
jamais le joueur » comme une contrainte — et qu'une contrainte qu'aucun mécanisme ne fait
respecter n'est qu'un souhait.

---

## 5. RGPD et le recours à un tiers

La question d'un joueur quitte notre serveur pour celui d'un prestataire. Ce n'est pas un
détail de conformité : c'est un fait qu'il faut assumer et déclarer.

| Point | État | À faire |
|---|---|---|
| Base légale | Intérêt légitime (fournir une aide contextuelle), sous réserve d'information claire | Mentionner le recours à un prestataire d'IA dans la politique de confidentialité |
| Données transmises | La **question**, saisie librement — donc potentiellement personnelle, même si nous ne l'y invitons pas. Plus le Monde, la destination et les droits, qui ne sont pas identifiants. | Ne jamais joindre l'identité, l'adresse, ni un identifiant de compte à l'appel |
| Sous-traitance | Un DPA est nécessaire avec le fournisseur retenu | À vérifier au moment du choix du compte |
| Conservation | À décider : conserver les échanges permet d'améliorer le corpus, mais crée un fichier | **Recommandation : conserver la question et la réponse 30 jours, sans identifiant joueur**, uniquement pour corriger le corpus |
| Mineurs | Si des mineurs participent au Festival, le régime change | Question ouverte pour Boris |

Le principe qui simplifie tout : **le guide n'a pas besoin de savoir qui parle.** Son
enveloppe de contexte est déjà minimale par la spec ; il suffit de ne pas y ajouter
l'identité. Un appel anonyme est à la fois plus sûr et plus simple à déclarer.

---

## 6. Coût — ce n'est pas la contrainte

Estimation à l'échelle du Festival, méthode explicite pour que Boris puisse la refaire :

- **Hypothèse** : 100 participants, 5 questions chacun sur la journée = **500 échanges**.
- **Par échange** : ~4 000 jetons en entrée (consigne système + fiches sélectionnées +
  question), ~400 en sortie.
- **Volume** : 2 M jetons en entrée, 0,2 M en sortie.

| Modèle | Coût de la journée | Remarque |
|---|---|---|
| Haiku 4.5 | ~3 $ | Le moins cher, mais le registre du Docteur est exactement là où un petit modèle dérape |
| **Sonnet 5** | **~9 $** (moins avec la mise en cache) | **Recommandé** |
| Opus 5 | ~15 $ | Surdimensionné pour répondre sur un corpus fourni |

**La mise en cache de la consigne divise encore l'entrée par dix** sur les échanges
suivants, la partie stable du prompt (consigne + fiches du Monde) étant identique d'un
joueur à l'autre. Attention à un détail : le seuil minimal de mise en cache dépend du
modèle — 1 024 jetons sur Sonnet 5, mais 4 096 sur Haiku 4.5, ce qui rend le cache
inopérant sur un petit prompt avec Haiku. Un argument de plus pour Sonnet.

**Conclusion : le coût d'une journée de Festival est de l'ordre du prix d'un déjeuner.**
Il ne doit pas peser dans les arbitrages, et surtout pas justifier un modèle moins
capable sur la seule fonction où la qualité de jugement compte — tenir une voix sans
blesser, et dire « je ne sais pas » plutôt qu'inventer.

Ce qui *doit* être posé en revanche, c'est un **plafond de dépense** : un compteur
quotidien qui coupe la fonction au-delà d'un seuil, pour qu'un incident (boucle, abus,
robot) ne se traduise pas par une facture. Le guide qui s'éteint proprement est un
non-événement ; une facture inattendue n'en est pas un.

**Côté outillage, la voie est dégagée** : le SDK Ruby officiel existe et est actif
(`anthropic`, v1.61.0, publiée il y a cinq jours). Il n'y a rien à bricoler — mais rien
n'est installé non plus aujourd'hui : ni client HTTP, ni gemme d'IA dans le `Gemfile`.

---

## 7. Modes de panne et invariants

Une fonction qui dépend d'un tiers réseau tombera. La question n'est pas si, mais ce
qu'on voit quand elle tombe.

| Panne | Comportement exigé |
|---|---|
| Prestataire indisponible / lent | Message clair (« le guide ne répond pas pour l'instant »), lien vers l'Aide. **Jamais une page d'erreur.** |
| Plafond de dépense atteint | Même comportement. La fonction s'éteint, l'application continue. |
| Le modèle décline la demande | Le refus est un état normal, pas une panne : il s'affiche avec le renvoi vers l'Aide. |
| Question hors périmètre | Renvoi explicite vers le mentor, un facilitateur, ou l'Aide — c'est déjà dans la spec. |

**Un invariant domine tous les autres : l'Aide et les recours humains ne passent jamais
par le modèle.** Quelqu'un en détresse à 23 h doit atteindre un humain par un chemin qui
ne dépend d'aucun service tiers, d'aucun quota, d'aucune disponibilité réseau. `/aide`
existe déjà et est statique ; **elle doit le rester.** C'est la ligne à ne pas franchir,
même par commodité.

---

## 8. Recommandation

**Ne pas ouvrir F19 comme un chantier de développement.** Le code n'est pas le goulot :
une page, un appel, un corpus en prompt — deux à trois jours. Ce qui manque est ailleurs.

### Palier 0 — avant tout code (éditorial, appartient à Boris et Codex) — réalisé pour M0 et M1

Le **corpus joueur** est versionné pour les Mondes 0 et 1. Chaque extension de Monde doit
rejouer le même cycle : rédaction, niveau de dévoilement, sources publiques, recette des deux
voix et validation humaine. Le serveur ne doit jamais indexer directement `docs/vision/`.

### Palier 1 — la fonction nue

Une page « Demander au guide », le Professeur seul, corpus en prompt, sources citées,
plafond de dépense, signalement en un geste, absence sur les écrans sensibles. Vérifiable
par banc comme le reste : le guide cite au moins une source, ne répond pas hors corpus,
disparaît des écrans sensibles, et l'Aide reste atteignable quand le service est coupé.

### Palier 2 — la présence

La pastille (option B), puis le Docteur — **si et seulement si** la lecture des échanges
réels du palier 1 montre que la ligne « sans ridiculiser » tient.

### Les cinq décisions qui t'appartiennent

1. **Le Docteur en v1, ou le Professeur seul d'abord ?** (Je recommande le Professeur seul.)
2. **Pastille dès la v1, ou page dédiée puis pastille ?** (Je recommande page d'abord.)
3. **Qui écrit le corpus joueur, et pour quand ?** C'est le seul vrai chemin critique.
4. **Conserve-t-on les échanges ?** (Je recommande 30 jours, sans identifiant.)
5. **Y aura-t-il des mineurs au Festival ?** La réponse change le régime de conformité.

---

*Cette analyse remplit l'exigence posée par la spec §5.4. Elle ne vaut que pour un guide
**sans outils**, qui lit un corpus et parle. Le jour où l'on voudra lui donner la moindre
capacité d'action — chercher dans l'annuaire, ouvrir un fil, écrire quoi que ce soit —,
elle doit être refaite : ce sont les pouvoirs, pas les mots, qui déterminent le risque.*
