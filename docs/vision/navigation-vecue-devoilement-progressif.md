# Navigation vécue et dévoilement progressif par les Mondes

<!-- [Claude] 2026-08-10 — deuxième passe de revue sur la coque `application-cible-consolidee`
     (zegame-prototypes, état ee680ac). La première passe (revue-ux-cible-consolidee.md) était
     structurelle et doctrinale ; celle-ci se place dans la peau de l'utilisateur : faciliter la
     navigation, simplifier, et — en prolongement de R1, confirmé par Boris — spécifier le
     dévoilement progressif des fonctionnalités Monde par Monde. Destinataires : Boris
     (arbitrages) et Codex (itération de la coque). -->

**Méthode.** Traversée de la coque déployée en perspective « Joueur », mesures de charge au
premier écran, sondage de la navigation interne de plusieurs modules (accueil, Marelle,
Cercle, Expérience vivante, messagerie), confrontation à `marelle-mondes.md` (canon des
Mondes), `navigation-vues-ensemble.md` et aux arbitrages du 2026-08-10. Cette revue ne
répète pas les R1-R11 de la première passe ; elle les prolonge là où ils croisent la
navigation (R1, R3, R4, R6) et propose ce que R1 laissait ouvert : QUOI ouvrir à CHAQUE
Monde.

---

## 1. Le constat central : trois grammaires de navigation concurrentes

Un joueur qui ouvre la coque aujourd'hui rencontre, mesures faites :

- **43 choix interactifs** au premier écran (hors contenu du module affiché) ;
- **24 modules** dans la barre latérale, rangés en **7 territoires**
  (Mon chemin, Se relier, Agir & contribuer, Transmettre, Mes repères,
  Prendre soin du système, Horizon du Jeu) ;
- **4 traversées** proposées en plus de cette carte ;
- et, à l'intérieur du module affiché, une **seconde navigation globale** propre à chaque
  prototype : « Accueil · Marelle · Cercle · Annuaire · Ressources · Rendez-vous · Profil »
  — sept entrées qui ne recoupent PAS les sept territoires de la coque ;
- et enfin, dans le contenu de l'accueil lui-même, une **troisième grammaire** : les
  « espaces du Jeu » y sont QUATRE (Mon chemin, Mes Cercles, Projets & Commun,
  Ressourcerie).

Le même écran propose donc trois cartes mentales différentes de la même application.
S'y ajoutent des incohérences de détail qui trahissent la juxtaposition : « Cercle » au
singulier dans un module, « Cercles » au pluriel dans l'autre ; la barre mobile interne
change d'un module à l'autre (la Marelle affiche Échanges, le Cercle affiche Projets,
l'Expérience affiche Profil) — l'utilisateur perd le repère spatial le plus élémentaire :
les mêmes boutons au même endroit.

L'accueil, lui, est déjà juste : UNE prochaine action, TROIS invitations, QUATRE espaces.
C'est la coque qui contredit son propre meilleur écran.

**→ N1. Une seule grammaire, celle de l'accueil, étendue à cinq portes.** La hiérarchie
principale de la coque devient : **Aujourd'hui · Mon chemin · Mes liens · Agir · Moi** —
et ces cinq portes sont LES MÊMES dans la coque, dans la barre interne des modules (qui
disparaît à terme : c'est un vestige des prototypes autonomes) et dans la barre mobile,
identiques sur chaque écran. Les sept territoires actuels sont un rangement de
bibliothécaire — exact, mais personne ne pense « je vais dans Transmettre » ; on pense
« je veux retrouver ma fiche », « je veux parler à mon Cercle ».

## 2. Des modules aux destinations : simplifier sans rien perdre

Le second problème vécu : les 24 entrées se présentent toutes au même niveau, comme des
lieux où aller. Or une dizaine seulement sont des **destinations** — des endroits qu'un
joueur choisit d'ouvrir. Le reste est constitué de **panneaux contextuels** : des vues qui
n'ont de sens que DEPUIS un objet (une expérience s'ouvre depuis la Marelle, la
reconnaissance se lit depuis le profil ou l'économie, un projet se rejoint depuis la place
de marché). Les présenter comme des portes d'entrée oblige l'utilisateur à mémoriser une
carte que le contexte lui aurait donnée gratuitement.

Proposition de réduction — aucune vue supprimée, chacune rattachée à sa porte :

| Destination (9) | Absorbe comme panneaux ou vues internes |
|---|---|
| **Aujourd'hui** | Centre d'activité (l'archive de l'attention — cf. R4, une source, trois projections) |
| **Marelle** (Mon chemin) | Expérience vivante · Mentor & Fresque (Graines, Résonances) · Héros & mentors · Freeride · Monde-miroir et Épreuve autosubversive (cases d'horizon DE la Marelle, pas rubriques de menu) |
| **Échanges** | seule surface de conversation — le fil d'un Cercle ou d'un projet est le MÊME objet projeté, jamais une seconde messagerie |
| **Cercle(s)** | Pacte-Source, séances et rôles, mémoire du Cercle |
| **Agenda** | rencontres, disponibilités, Festival |
| **Place de marché** | Missions du Commun (vue filtrée — R3 tranché) · facettes Souverainetés · Projet vivant (destination contextuelle : n'apparaît que pour qui est engagé dans un projet) |
| **Ressourcerie** | Studio de filiation (l'atelier du créateur, versant « œuvres » de la Ressourcerie) |
| **Le Commun** | Gouvernance (consultations, décisions) · Économie Oméga · Observatoire en lecture |
| **Profil** (Moi) | Souverainetés · Reconnaissance · Consentements · Engagement économique (mes contrats) |

Trois règles font tenir l'ensemble :

- **une porte par objet** — un besoin s'ouvre à la Place de marché, une conversation dans
  Échanges, point ; si deux rubriques mènent au même objet, l'une des deux est un lien,
  pas une porte ;
- **le contexte plutôt que le menu** — tout ce qui se vit DEPUIS un objet (expérience,
  reconnaissance, filiation, projet) s'atteint depuis cet objet ;
- **Aide & recours n'est PAS dans cette économie** : accessible en permanence, depuis
  chaque écran, y compris hors connexion — jamais soumis à une porte, un Monde ou un rôle.

Les quatre traversées gardent leur valeur — mais ce sont des outils de VALIDATION pour
nous (vérifier que les passages entre modules existent), pas des chemins offerts à
l'utilisateur. Le chemin de l'utilisateur, c'est la Marelle. Les traversées ne doivent pas
devenir un embarquement.

Enfin le sélecteur de « Perspective » de la topbar est un outil de maquette : dans
l'application réelle, personne ne « choisit » d'être facilitateur dans un menu déroulant —
les vues de rôle apparaissent quand le rôle existe. À étiqueter comme instrument de
simulation (au même titre que « Simuler le contexte » de l'accueil), pour que les tests
utilisateurs ne le prennent pas pour une fonctionnalité.

## 3. Le dévoilement progressif par les Mondes

R1 (confirmé) demande un sélecteur « Monde » dans la coque. Voici ce qu'il doit simuler —
c'est-à-dire la politique d'ouverture elle-même, proposée ici pour arbitrage.

### 3.1 Principes

1. **Quatre états par destination** : `invisible` · `annoncée` (visible, verrouillée,
   avec la condition d'ouverture dite en clair) · `ouverte en lecture` · `ouverte`.
   L'état « annoncée » est un rite d'appel : il dit « ceci s'ouvre au Monde 2, avec ton
   Voyage » — jamais un cadenas muet.
2. **Le Monde est le plancher, pas la seule clé.** Trois autres clés ouvrent des portes
   indépendamment du Monde : l'**événement** (un billet du Festival ouvre l'Agenda-Festival
   et le parcours du jour, même au Monde 0 — c'est le chemin critique réel), le **rôle**
   (facilitateur → Académie et Cockpit ; Cercle cœur → Observatoire ; mandat d'intégrité →
   Backoffice — quel que soit le Monde), l'**engagement** (rejoindre un projet ouvre
   Projet vivant).
3. **Jamais verrouillés, dès le Monde 0** : Aide & recours (même avant connexion),
   Consentements, Profil, Échanges individuels existants, export et départ. La sécurité et
   la souveraineté ne se méritent pas.
4. **Au plus UNE destination « annoncée » à la fois par porte.** Le désir a besoin d'un
   horizon, pas d'une vitrine de cadenas.
5. **Le passage de Monde est le moment du dévoilement.** Ce qui s'ouvre se découvre DANS
   le rite de passage de la Marelle, pas par mutation silencieuse du menu — le joueur doit
   pouvoir dire « c'est en passant au Monde 2 que j'ai reçu le Freeride ».
6. **Le vocabulaire se dévoile aussi.** Au Monde 0, les libellés parlent la langue
   commune (« Mes fiches gardées », « Trouver de l'aide ») ; les noms néoarchaïques
   (Graine, Résonance, Souveraineté, Filiation) apparaissent quand l'objet est vécu — la
   première Graine produite se nomme au moment où on la produit. Une application qui
   exige le lexique complet à l'entrée re-crée la barrière que le Sas veut abaisser.

### 3.2 Table de dévoilement, Monde par Monde

Fondée sur la progression canonique (`marelle-mondes.md` §2). Les destinations sont
celles du §2 ci-dessus.

| Monde (canon) | S'ouvre | S'annonce | Portes ouvertes |
|---|---|---|---|
| **0 — Terre** (sas, mise en résonance) | Aujourd'hui (réduit : une action, une invitation) · Marelle limitée au Monde 0 · Agenda (événements publics, Festival si billet) · Ressourcerie en lecture · Profil léger · Échanges (individuels + espace d'accueil) · Aide & Consentements | Le Cercle (« s'ouvre au Monde 1, quand naît ton Cercle ») | **7** |
| **1** (le moi face au collectif, Cercle naissant, autofacilitation) | + Cercle (Pacte-Source léger, cinq rôles) · Échanges complets (espaces collectifs) · Annuaire (trouver ses pairs) · Graines & Résonances dans la Marelle (le passage les récapitule) | Le Voyage du héros et le Freeride (« Monde 2 ») | **10** |
| **2** (Voyage du héros, engagement annuel) | + Freeride, Héros & mentors et ligne de jeu dans la Marelle · Place de marché (contribuer, répondre à un besoin) · Économie Ω en lecture (compte d'Ω actifs, cagnotte du Cercle) · rejoindre un Projet | Porter une œuvre (« Monde 3 ») | **12** |
| **3** (Ombre, œuvre personnelle réelle) | + porter un Projet · premiers domaines de Souveraineté · Studio de filiation (son œuvre, sa lignée) · Engagement économique (ses contrats) | Le Commun en écriture (« Monde 4 ») | **13** |
| **4** (langage de la Conscience, cercle autonome) | + Le Commun en écriture : consultations, orientation du Fonds · outils d'essaimage du cercle autonome · Monde-miroir (horizon narratif, si retenu ici) | — | **14 (plafond)** |
| **5** (service collectif) | Rien de NOUVEAU dans le menu : le service s'exerce par les rôles (voie facilitateur → Académie et Cockpit ; accompagnement d'organisations → Sas des organisations, Organisation vivante) | — | stable |
| **6** (Cités cosmiques, cosmolocal) | + gouvernance territoriale et multi-cercles dans Le Commun · Observatoire en lecture élargie | — | stable |
| **7** (fin du parcours humain) | + Épreuve autosubversive (rite tardif — hypothèse à arbitrer, cf. `game-autosubversion.md`) | — | stable |
| **8-9** (non décrits) | Rien — le canon ne les décrit pas ; toute ouverture ici serait inventée | — | stable |
| **10** (communion, recommencement) | Rien de nouveau : la Marelle se rejoue en spirale — le dévoilement recommence, pas l'inventaire | — | stable |

La courbe de charge est le vrai livrable de cette table : **7 → 10 → 12 → 13 → 14, puis
stable**. Jamais plus de trois portes nouvelles à un passage. Le plafond est atteint au
Monde 4 : au-delà, la profondeur croît DANS les portes (rôles, mandats, territoires), le
menu ne grossit plus. À comparer aux 24 entrées que la perspective « Joueur » affiche
aujourd'hui d'un coup : le menu du Monde 0 est trois fois plus court, et chaque
élargissement est un événement vécu, pas un état de fait.

### 3.3 Ce que le sélecteur R1 doit simuler, concrètement

Pour que la coque teste ce dévoilement (et pas seulement un masquage) :

- le sélecteur « Monde » applique la table §3.2 : états `invisible` / `annoncée` /
  `lecture` / `ouverte` par destination — pas un simple filtre d'affichage ;
- les éléments « annoncés » montrent leur libellé de rite d'appel (la condition
  d'ouverture, en langue claire) ;
- le croisement avec la perspective reste : un facilitateur au Monde 2 voit Académie et
  Cockpit (clé de rôle) mais pas Le Commun en écriture (plancher Monde 4) ;
- au moins un passage de Monde est simulable de bout en bout (0→1 recommandé : c'est
  celui du Festival), avec l'écran de rite qui ANNONCE les portes qui s'ouvrent ;
- les libellés à double registre (langue commune / lexique PZ) sont testés sur les
  destinations du Monde 0 au minimum.

## 4. Récapitulatif pour arbitrage et itération

| # | Proposition | Nature |
|---|---|---|
| N1 | Une seule grammaire de navigation : cinq portes identiques partout (coque, modules, mobile) ; suppression à terme des barres internes des prototypes | Arbitrage Boris puis Codex |
| N2 | 24 modules → 9 destinations + panneaux contextuels (table §2) ; règles « une porte par objet » et « le contexte plutôt que le menu » | Arbitrage Boris puis Codex |
| N3 | Traversées re-cadrées comme outil de validation, pas d'embarquement ; sélecteur de Perspective étiqueté comme instrument de simulation | Codex, immédiat |
| N4 | Politique de dévoilement §3.1-3.2 : quatre états, quatre clés (Monde, événement, rôle, engagement), surfaces jamais verrouillées, courbe 7→10→12→13→14 | Arbitrage Boris (c'est la substance de R1) |
| N5 | Le sélecteur R1 simule les états et le rite de passage, pas un masquage (§3.3) | Codex, après N4 |
| N6 | Vocabulaire à double registre au Monde 0, lexique PZ dévoilé par l'usage | Arbitrage Boris ; rejoint la passe voix (R9) |
| N7 | Harmoniser singulier/pluriel (« Cercle »/« Cercles ») et figer la barre mobile — les mêmes entrées au même endroit sur tous les écrans | Codex, immédiat |

Deux points laissés ouverts, à dessein : la place du Monde-miroir (Monde 4 en table, mais
`monde-miroir.md` pourrait justifier plus tôt en lecture narrative) et celle de l'Épreuve
autosubversive (Monde 7 par cohérence avec « fin du parcours humain » — mais le rite
pourrait ponctuer chaque passage de Monde en version courte). Ces deux-là méritent une
lecture du canon par Boris plutôt qu'une déduction.

---

## 5. Maquette comparative et arbitrages de Boris — **2026-08-11**

<!-- [Claude] Les propositions N1-N7 ont été incarnées dans une variante de coque, puis
     soumises à Boris en trois lectures successives. Cette section consigne ce qu'il a
     validé, ce qu'il a corrigé, et les défauts relevés dans les prototypes de Codex. -->

Les propositions ci-dessus ont été **incarnées dans une variante de coque comparable à
celle de Codex**, même matière (les 31 prototypes chargés tels quels en iframe, sources de
vérité intactes), autre grammaire de navigation :

- maquette : `zegame-prototypes/application-cible-devoilement/`
- déployée : https://maquettes.167-233-210-57.sslip.io/ux-cible/application-cible-devoilement/
- à comparer avec : https://maquettes.167-233-210-57.sslip.io/ux-cible/application-cible-consolidee/

### 5.1 Ce que Boris a validé

| Proposition | Verdict |
|---|---|
| **N1-N2** — moins d'entrées dans la navigation principale, sous-menu horizontal des destinations | **Retenu.** « Je préfère l'ergonomie générale que tu proposes […] c'est bien vu. » |
| **R4** — la source d'attention unique en panneau (« Ce qui t'attend »), sans compteur permanent | **Retenu.** « C'est plus ergonomique. » |
| **N4** — dévoilement par les Mondes, états et clés | **Retenu dans son principe**, avec la précision du 5.2 sur la forme du verrouillage. |

### 5.2 Ce que Boris a décidé ou corrigé

1. **Le verrouillage prend la forme d'une page de teasing, pas d'une modale.** Une
   destination non encore ouverte affiche une vraie page dans la zone de contenu : ce que
   c'est, ce qu'on y fera (trois points), ce qui l'ouvre. S'applique notamment au Cercle et
   aux fils collectifs au Monde 0, et au Freeride aux Mondes 0 **et** 1.
2. **Le Freeride est teasé jusqu'au Monde 2.** Confirmation explicite du plancher retenu en
   table §3.2 ; il devient un panneau de la Marelle, annoncé dès le Monde 0.
3. **Les Échanges gagnent une place sur l'accueil** (R6a). Réalisé sous forme d'un bandeau
   qui **nomme** ce qui attend une réponse (« Sarah t'a répondu · le Cercle cherche une
   date ») plutôt que de le compter — projection conversationnelle de la source d'attention
   unique, pas une seconde boîte.
4. **L'avatar porte le COMPTE, la porte « Moi » porte le chemin.** La question de la
   redondance est tranchée par une distinction d'objet : l'avatar ouvre paramètres,
   connexion et mot de passe, notifications, déconnexion — registre littéral, surface de
   sécurité ; le profil, les œuvres et les souverainetés restent dans la porte « Moi », et
   le menu le dit en pied.
5. **Le compte d'Ω renvoie à la page du Commun**, son contexte d'exercice — et à son teaser
   tant que le Commun n'est pas lisible. (Amende R5 : l'Ω reste visible en permanence,
   discret, nommé « compte », et devient cliquable vers une destination.)
6. **Le Mentor peut apparaître dans deux contextes** (Mon chemin pour produire, Mon profil
   pour relire) : accepté, cohérent avec « le contexte plutôt que le menu ». À surveiller à
   l'usage ; si confusion, le profil pointera vers le panneau du chemin.

### 5.3 Défauts relevés dans les prototypes — pour correction par Codex

Constatés en parcourant les modules dans la coque ; ils ne relèvent pas de la grammaire de
navigation mais des prototypes eux-mêmes.

| # | Constat | Où |
|---|---|---|
| D1 | **Corrigé sur le lot A le 11 août.** Accueil, Marelle, Profil, Cercle et Messagerie ont une base source de 16 px et aucune taille explicite sous 13 px ; la coque les affiche à zoom 1. Le plancher injecté subsiste temporairement pour les modules anciens, à reprendre dans R9. | lot A, puis R9 global |
| D2 | **Corrigé le 11 août.** « Mon mentor IA » et « Mon Cercle » sont de vrais liens autonomes ; en mode embarqué, le protocole `pz:navigate` ouvre Graines & Résonances et Mes Cercles dans la coque. | `marelle-freeride-cible` |
| D3 | **Corrigé le 11 août.** Le registre utilise `map` pour la Marelle et aucune route interne pour l'Expérience vivante. | registre de `application-cible-consolidee/app.js` |
| D4 | **Corrigé dans la coque retenue.** Aide est chargée en plein écran ; cette règle reste un invariant pour ses futurs embarquements. | `application-cible-devoilement` |

La même passe a corrigé un débordement mobile de la Messagerie : la liste des
espaces et la conversation sont désormais deux vues maître-détail exclusives,
au lieu de deux panneaux juxtaposés dont l'un restait translaté hors écran.

La Marelle est aussi le premier module raccordé au Monde canonique de la coque.
`pz_world` commande maintenant son identité, le Monde courant de la carte, les
droits et parcours visibles. Le Freeride et la ligne de jeu restent absents et
inaccessibles aux Mondes 0 et 1, même par une ancienne ancre directe. Accueil,
Profil, Cercle et Messagerie doivent encore achever cette projection des données
fictives ; leur normalisation typographique, elle, est déjà faite.

### 5.4 Guides transversaux et Puissances-phares des héros — 2026-08-11

La coque peut porter une présence permanente et discrète du Professeur Sirbey et du
Docteur Z.E.R.O. sous la forme d'une pastille ouvrant un dialogue contextuel. Cette
présence n'est pas une nouvelle destination de navigation : elle aide le joueur à
comprendre le Point Zéro, la page courante et les fonctionnalités accessibles.

Les deux guides interrogent le même corpus, disposent des mêmes droits et doivent
pouvoir montrer leurs sources. Seule leur rhétorique diffère : le Professeur clarifie,
structure et relie ; le Docteur confronte les contradictions avec un humour caustique
qui ne ridiculise jamais le joueur. Le choix d'une voix ne doit donc produire aucune
différence de vérité, de mémoire ou de permission.

Cette fonction reste strictement distincte :

- du **mentor IA**, qui accompagne une expérience personnelle et peut travailler avec
  les traces que le joueur lui ouvre explicitement pour produire une Graine ;
- de l'**Aide** et des recours humains, qui traitent support, conflit, détresse,
  médiation et situations sensibles ;
- de la **recherche**, qui trouve directement un contenu sans construire un dialogue.

Par défaut, le guide transversal ne lit ni Graines, ni profil détaillé du Moteur, ni
conversations privées. Son enveloppe de contexte se limite au Monde, aux droits, à la
destination et au panneau actuellement ouverts. Il doit signaler ses incertitudes,
permettre de corriger ou signaler une réponse et rediriger vers le mentor, un
facilitateur ou l'Aide dès que la question sort de son périmètre.

Les fiches des héros montrent par ailleurs trois **Puissances-phares** sous forme de
lemniscates : une principale et deux puissances d'appui. Il s'agit d'une clé éditoriale
pour lire l'œuvre et les déplacements proposés par cette figure, jamais d'un diagnostic
psychologique de la personne réelle ni d'une évaluation du joueur.

### 5.5 Reste ouvert

Le placement du **Monde-miroir** (Monde 4 dans la table) et de l'**Épreuve autosubversive**
(Monde 7) attend toujours une lecture du canon par Boris — voir la fin du §4.
