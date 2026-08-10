# Revue critique de l'UX-cible consolidée

<!-- [Claude] 2026-08-10 — revue de `zegame-prototypes` (coque `application-cible-consolidee`
     + 31 modules, commit a6e4007) confrontée au corpus de docs/vision/. Destinataires :
     Boris (arbitrages) et Codex (réponses / itération des maquettes). -->

**Méthode.** Lecture intégrale des NOTES.md des 31 modules de la coque (leur couche
d'intention et d'invariants), navigation dans la coque déployée
(https://maquettes.167-233-210-57.sslip.io/ux-cible/application-cible-consolidee/), sondage
du code de plusieurs modules (messagerie, accueil, économie, gouvernance), confrontation
aux documents d'ancrage : `application-festival-2026.md` (seule décision opérationnelle),
`ecosysteme-point-zero-questions-reponses-cercle-coeur.md`,
`cercles-croissance-profils-flow-omega.md` (canon du 31/07),
`messagerie-point-zero-vision-cible.md`, `cosmo-coin-omega.md`,
`navigation-vues-ensemble.md`, `impacts-fonctionnels.md`, `voix-point-zero.md`,
`direction-artistique-point-zero.md`. Les modules sont homogènes en profondeur
(12-40 ko de HTML/JS chacun) : des esquisses interactives de fidélité moyenne, pas des
écrans de production — c'est le bon niveau pour ce qu'elles veulent tester.

---

## 1. Ce qui est fort — à préserver tel quel

1. **Les invariants anti-score sont partout et globalement fidèles.** Chaque module répète,
   dans son vocabulaire, la doctrine : pas de classement de personnes, pas de score de
   conscience, l'Oméga non fongible qui ne paie rien, le refus sans pénalité. C'est la
   colonne vertébrale du corpus (cosmo-coin, Q&R §IX-X, messagerie §16/§22.7) et elle tient.
2. **Les surfaces sensibles sont les plus mûres.** `aide-situations-sensibles` (numéros
   d'urgence avant connexion, récusation du facilitateur impliqué, humour absent),
   `consentement-securite` (retrait d'accès honnête sur ce qui a déjà été lu),
   `backoffice-integrite` (pas de super-admin implicite, accès exceptionnel à double
   contrôle) sont d'une maturité rare à ce stade — et convergent avec ce qui est DÉJÀ
   construit en préprod/prod (mandat de modération orthogonal, A0).
3. **La séparation des circuits financiers** (cagnotte de Cercle / Fonds du Commun /
   financement de projet ; Ω jamais dépensé, capacité d'orientation affichée séparément)
   est conforme au canon, et les hypothèses chiffrées (decay 10 %, retours 20 %, indice
   100 €/Ω) sont honnêtement étiquetées « expérimentales ».
4. **La coque préserve la source de vérité** : chaque prototype reste autonome (« Ouvrir
   sans la coque »), pas de recopie. Et son principe « la perspective réduit la navigation
   mais ne modifie aucun droit réel — les autorisations restent côté serveur » est
   exactement la doctrine `ContexteDeFil` de l'application réelle.
5. **Le module messagerie documente « ce qui existe déjà en préproduction »** avant de
   projeter — c'est le seul à le faire, et c'est le bon patron (voir recommandation R7).

---

## 2. Écarts et contradictions à traiter

### 2.1 La dimension « Monde » est absente de la coque — l'écart le plus structurant

La coque offre cinq perspectives de RÔLE (Joueur, Facilitateur, Cercle cœur, admin, atlas),
mais aucune simulation de PROGRESSION : la perspective « Joueur » montre ~24 modules d'un
coup, alors que tout le corpus (marelle-mondes, Q&R §V, canon 31/07 §6 : héros et Freeride
**à partir du Monde 2**) prescrit une application qui **s'ouvre par seuils**. Un joueur
réel du Monde 0 verra six ou sept vues, pas vingt-quatre. Conséquences :

- les tests utilisateurs des traversées seront faussés (charge de navigation irréaliste) ;
- la coque suggère une application-cathédrale là où la doc prescrit une divulgation
  progressive (messagerie §15.2) ;
- des modules rangés dans « Mon chemin » (Héros & mentors, Freeride) sont en réalité
  verrouillés jusqu'au Monde 2 sans que rien ne le montre.

**→ R1 : ajouter un sélecteur « Monde » (0 / 1 / 2+) à la coque**, croisé avec la
perspective, qui masque/verrouille ce que chaque Monde n'ouvre pas encore — avec l'état
« verrouillé mais visible » comme rite d'appel là où la Marelle le veut.

### 2.2 Aucune traversée ne couvre le seul périmètre daté : le Festival

Les quatre traversées (grandir, projet, transmettre, Commun) sont des chemins d'horizon.
Or la seule décision opérationnelle du corpus (`application-festival-2026.md`) définit UN
chemin critique : **billet → rattachement → accueil Festival → Monde 0 → réservation
d'ateliers → validation par présence → après-Festival**. Ce chemin existe en production —
il n'existe pas dans la coque.

**→ R2 : ajouter la traversée « Vivre le Festival »**, construite sur l'état réel, pour
que la maquette serve aussi à tester ce qui sera vécu le 1er octobre — et pour montrer aux
testeurs le POINT D'ENTRÉE réel de l'écosystème, pas seulement son état de croisière.

### 2.3 Trois surfaces revendiquent les « besoins » — qui est la porte canonique ?

`missions-commun-cible` (« Place des besoins »), `place-marche-cible` (« porte commune
pour les besoins, accompagnements… ») et `observatoire-ecosysteme-cible/#needs` (« place
de marché des besoins du système ») se recouvrent. La coque les range côte à côte sans
hiérarchie. Le doublon missions/place-de-marché est le plus net : les deux affichent des
besoins avec correspondances explicables.

**→ R3 : trancher la porte unique.** Proposition : la Place de marché est LA porte
(besoins, offres, œuvres) ; les Missions du Commun en sont un SOUS-ENSEMBLE filtré (porté
par le Fonds) ; l'Observatoire ne fait que LIRE (il pointe, il n'héberge pas).

### 2.4 Trois boîtes d'attention concurrentes

L'accueil (« trois invitations maximum »), le Centre d'activité (« demandes typées,
échéancier ») et l'accueil des Échanges (« À ton attention », engagements — construit en
préprod, S1-A4) forment trois inboxes. Le Centre d'activité dit bien « ne pas dupliquer
l'action métier », mais rien ne dit comment les trois se PARTAGENT l'attention — et la
topbar de la coque ajoute un badge numérique « ◌ 3 » qui recrée la boîte-à-vider que
l'accueil bannit explicitement.

**→ R4 : une seule source d'attention, trois projections.** Spécifier l'objet transversal
(l'`ActivityItem` que centre-activite propose) comme SOURCE unique, dont l'accueil montre
une sélection (≤3), le Centre l'archive complète, et les Échanges la part conversationnelle
(les engagements S1-A4 en sont déjà une projection réelle). Supprimer le badge numérique
permanent de la topbar, ou le remplacer par un indicateur binaire.

### 2.5 L'Oméga affiché en permanence dans la topbar

La coque et l'accueil épinglent « 172 Ω » dans la barre — une affordance de
solde/portefeuille. Or : cosmo-coin distingue soigneusement Ω actifs et cumul historique
(lequel affiche-t-on ?) ; l'économie de l'attention (messagerie §16) bannit les compteurs
permanents ; et l'accueil lui-même promet « aucun résumé ne classe la personne ». Pire, la
NOTES de l'annuaire écrit « l'Oméga peut être visible comme **score unique** » — le mot
« score » est précisément celui que tout le corpus proscrit.

**→ R5 : sortir l'Ω de la topbar** (le loger dans Profil et Économie, ses deux contextes
d'exercice), et **bannir le mot « score »** des NOTES de l'annuaire au profit de « total
visible, jamais un critère ni un tri ».

### 2.6 Navigation mobile : les Échanges n'ont pas de porte

Les cinq portes mobiles fixes de l'accueil sont Accueil, Marelle, Cercles, Ressources,
Profil. La messagerie — l'usage quotidien n° 1 visé (« quitter WhatsApp », critère
d'acceptation §22.1) — n'y figure pas. Une messagerie qu'on n'atteint pas en un geste sur
téléphone ne remplacera pas WhatsApp.

**→ R6 : arbitrer la cinquième porte mobile.** Proposition : Accueil · Marelle · Échanges ·
Cercles · Profil — la Ressourcerie est contextuelle par nature (ses propres NOTES disent
« au moment où un contexte lui donne un usage »).

### 2.7 L'écart réel/projeté n'est piloté que par un module sur trente et un

Seule la messagerie documente « ce qui existe déjà ». Pour les autres, rien ne distingue ce
qui projette l'existant (profil, marelle, cercles — largement construits) de ce qui invente
(monde-miroir, place de marché). Sans ce marquage, la maquette devient une promesse
uniforme — et les décisions de périmètre se prendront sur une carte qui ne dit pas où sont
les routes déjà pavées.

**→ R7 : généraliser le chapitre « État réel / état projeté »** dans chaque NOTES, sur le
patron du module messagerie. Je peux fournir l'état réel par module (c'est l'inventaire de
ce qui tourne en prod).

### 2.8 Les nouveaux objets métier n'ont pas de ligne d'impact

La règle du registre `impacts-fonctionnels.md` : « aucune implémentation sans ligne
d'analyse ». Les maquettes introduisent une quinzaine d'objets nouveaux — Meeting/Rencontre
d'agenda, ActivityItem, Mission, Besoin, Habilitation, Domaine de souveraineté,
Œuvre/Version/Filiation, Consultation, Mandat, Espace sensible, Contribution reconnue,
Enveloppe de reconnaissance… Aucun n'a de ligne F.

**→ R8 : étendre le registre (F19+) avant tout portage Rails**, en commençant par les
objets des lots proches (messagerie étape B : Proposition/Décision/Action — leur spec est
le prochain chantier convenu ; l'agenda `Meeting` dont la V1 simple existe déjà sous forme
de `PropositionDeRencontre`).

### 2.9 Convergences déjà construites — à acter pour ne pas re-spécifier

Trois éléments de la maquette messagerie existent déjà en production, dans une forme
proche mais non identique ; il faut acter la convergence pour éviter une double vérité :

- **l'objection en trois temps** (ce que je protège / le risque / la condition de levée)
  est construite (S1-B1) comme réaction sémantique précisable ; la maquette la veut geste
  autonome attaché à une Proposition/Décision. Compatible — mais à écrire : quand l'objet
  Décision naîtra, l'objection B1 migrera vers lui, elle ne coexistera pas ;
- **les cartes structurées** (S1-B2) implémentent le contrat §8.1 (type, statut, porteur,
  action selon habilitation, lien selon droits, indisponible honnête) — la maquette doit
  les réutiliser comme grammaire, pas en inventer une seconde ;
- **intentions de conversation** : la doc (§6) les met au niveau espace/sous-fil, la
  maquette dans le composeur (par message). À trancher — par fil est plus sobre et plus
  conforme (« l'intention ne change jamais automatiquement les droits »).

### 2.10 Direction artistique et voix

La coque utilise des glyphes système (◇ ○ ⌘ ✦ ◌ ▤ ∞) comme iconographie et une esthétique
neutre, sans la grammaire néoarchaïque prescrite par `direction-artistique-point-zero.md`,
ni les codes visuels réels de l'application (violet #82246f, fontello vendorisé,
lemniscates du Moteur). La voix est sobre partout — la charte `voix-point-zero.md` prescrit
un ton adulte, décalé, à doser par surface (et son absence est CORRECTE sur les écrans
sensibles — la maquette aide/sécurité le fait bien).

**→ R9 : une passe DA + voix sur la coque et les modules de la traversée Festival** (les
premiers vus par de vrais joueurs), au moment où les libellés seront figés — pas avant.

### 2.11 États vides, chargement, erreur, accessibilité

Codex le recommande lui-même (« matrice des droits et états vides/chargement/erreur ») ;
aucune maquette ne les montre. S'y ajoute l'accessibilité : navigation clavier des panneaux
latéraux, glyphes non lus par lecteurs d'écran, contrastes non vérifiés — le critère §22.12
(« utilisables sur mobile et accessibles ») n'a pas encore sa preuve.

**→ R10 : un gabarit par module** — matrice droits × états (vide / chargement / erreur /
verrouillé-par-Monde) + une passe d'accessibilité, en commençant par les six modules de la
traversée Festival, pas par les trente et un.

---

## 3. Récapitulatif des recommandations, par priorité

*(État au 2026-08-10 après les arbitrages de Boris — voir §4.)*

| # | Recommandation | État | Porteur |
|---|---|---|---|
| R1 | Sélecteur « Monde 0/1/2+ » dans la coque | **Confirmée et renforcée** (la coque est la cible réelle) | Codex |
| R2 | Traversée « Vivre le Festival » | À faire | Codex (état réel fourni par le portable) |
| R7 | Chapitre « état réel / projeté » par module | À faire | Portable (inventaire) → Codex/poste fixe |
| R3 | Porte unique des besoins | **Tranchée : la Place de marché absorbe les Missions** | Codex |
| R4 | Une source d'attention, trois projections | À faire ; le badge numérique de la topbar reste à retirer | Codex, puis portable (`ActivityItem`) |
| R5 | Vocabulaire de l'Ω | **Amendée : l'Ω reste visible en permanence, discret, nommé « compte » — « score » banni** | Codex (NOTES annuaire) |
| R6a | Échanges visibles sur l'accueil du Jeu **réel** | **Décidée, actionnable tout de suite** | Portable |
| R6b | Configurations de barre mobile à tester | En attente des tests de Boris | Codex |
| R8 | Lignes F19+ pour les nouveaux objets | À faire, préalable à tout portage | Portable + Codex |
| R9 | Passe DA + voix | Confirmée (cible réelle) ; après gel des libellés | Poste fixe |
| R10 | Matrice droits × états + accessibilité | À faire, modules Festival d'abord | Codex + relecture portable |
| R11 | Variante « intention par fil » à comparer | **Nouvelle** (demande de Boris) | Codex |

Deux convergences à acter sans attendre (§2.9) : l'objection B1 migrera vers l'objet
Décision ; les cartes B2 sont LA grammaire des cartes de la maquette.

---

## 4. Questions ouvertes — **arbitrées par Boris le 2026-08-10**

### Q1. La coque est-elle la navigation réelle, ou un outil de test ?

**→ C'est la cible RÉELLE**, mais au terme d'un processus en trois temps :
**revue Claude → corrections par Boris → consolidation finale avec Codex.**

Conséquences : R1 (dimension Monde) et R9 (DA + voix) cessent d'être des améliorations de
confort — ce sont des investissements sur la future navigation de production. Et le cycle
lui-même devient une règle de gouvernance : aucune maquette ne devient cible sans avoir
traversé les trois temps. La présente revue est le premier temps.

### Q2. Intention de conversation : par fil ou par message ?

**→ Non tranché : Boris veut d'abord voir une variante « par fil »** pour la comparer à
la proposition « par message » de la maquette.

**→ R11 (nouveau, pour Codex) : produire la variante « intention par fil »** dans
`messagerie-point-zero-cible` — l'intention déclarée au niveau de l'espace ou du sous-fil
(conforme à la cible §6), affichée en en-tête et adaptant les cartes proposées, avec le
composeur rendu à sa sobriété. Les deux variantes doivent être comparables côte à côte
avant l'arbitrage. Cette décision conditionne la spec Proposition/Décision/Action.

### Q3. Porte des besoins : la Place de marché absorbe-t-elle les Missions du Commun ?

**→ Oui, pour simplifier.** R3 est donc tranchée : **la Place de marché est la porte
unique**. Les Missions du Commun deviennent un sous-ensemble filtré (celles portées par le
Fonds), et l'Observatoire `#needs` ne fait que lire et pointer — il n'héberge rien.
`missions-commun-cible` doit être fusionné dans `place-marche-cible` (ou explicitement
présenté comme une vue filtrée de celle-ci), et la coque ne doit plus proposer deux entrées
concurrentes.

### Q4. Cinquième porte mobile : Échanges ou Ressources ?

**→ Non tranché : Boris veut tester plusieurs configurations de menu.** Mais une décision
ferme accompagne l'attente : **dans tous les cas, les Échanges gagnent en visibilité sur la
page d'accueil elle-même.**

Cette seconde partie est **immédiatement actionnable, et vaut aussi pour l'application
réelle** : l'accueil du Jeu en production ne mentionne aujourd'hui les Échanges nulle part
— ils ne sont atteignables que par l'icône de la barre supérieure. R6 devient donc :

- **R6a (app réelle, portable)** : faire remonter les Échanges sur l'accueil du Jeu — les
  engagements « À ton attention » (déjà construits, S1-A4) y ont leur place naturelle, et
  ce sont eux qui portent l'information utile, pas un compteur.
- **R6b (maquette, Codex)** : décliner deux ou trois configurations de barre mobile à
  tester, l'accueil donnant dans chacune une place visible aux Échanges.

### Q5. L'Ω doit-il rester visible en permanence ?

**→ Oui, en permanence et discrètement — mais on l'appelle un COMPTE, jamais un score**
(c'est une monnaie de Conscience).

R5 est donc **amendée** : la moitié « sortir l'Ω de la topbar » est écartée par
l'arbitrage ; la moitié « bannir le mot *score* » est confirmée et renforcée. À appliquer :

- vocabulaire : « compte d'Omégas », « total », « Ω actifs » — jamais « score », jamais
  « solde » (qui suggérerait une dépense possible, contraire à la doctrine) ;
- traitement visuel : discret, sans badge d'alerte ni variation animée — un compte qui se
  consulte, pas une jauge qui sollicite ;
- corriger la NOTES de `annuaire-vivant-cible`, qui écrit encore « visible comme score
  unique » ;
- **sous-question restant ouverte** : le compte permanent affiche-t-il les **Ω actifs**
  (ce qui vit, soumis au decay, et ouvre la capacité d'orientation) ou le **cumul
  historique** ? Le corpus distingue soigneusement les deux. Recommandation : afficher les
  **actifs**, le cumul restant une lecture du Profil.
