# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · #53 — la carte de Graine est portée, et elle a un piège structurel

**À relire et fusionner.** [PR #53](https://github.com/PointZero2050/pointzero-app/pull/53).
Vue, partiel, CSS, banc. **#52 est toujours en attente** (les deux débordements) — les deux
touchent `heros.css` mais sur des blocs disjoints, aucun conflit attendu.

**1. ⚠️ LE POINT QUI MÉRITE TA RELECTURE, parce qu'il est invisible.** Le fil vit DÉJÀ dans le
formulaire du journal — il le doit, sinon le menu de thématique n'enverrait rien — **et un
formulaire ne s'imbrique pas**. Les champs de la carte sont donc rattachés par l'attribut HTML
`form=` à un formulaire rendu HORS de l'espace de travail, et « Écarter » vise l'autre route
par `formaction`.

Ce n'est pas un bricolage : c'est le cas que cet attribut existe pour couvrir. Mais **si
quelqu'un « simplifie » un jour en enveloppant la carte dans un `form_with`, le HTML devient
invalide, le navigateur ignore le formulaire intérieur, et les boutons ne postent plus rien
SANS erreur visible.** Le banc asserte donc le RATTACHEMENT (`form="graine-N"` sur trois
champs, et zéro `<form>` dans la carte), pas la seule présence des champs.

**2. Tes quatre points sont tenus.** Case cochée par défaut, champ vidé non bloqué côté client,
bouton non désactivé (ton verrou suffit, je n'ajoute pas de JS par peur). Le quatrième — la
qualité du signal en conditions réelles — je ne peux pas le juger sans dépenser un appel LLM.
**Je le regarderai au premier vrai dialogue et je te dirai ce que j'observe.**

**3. UNE CLAUSE QUE TON CONTRAT N'AVAIT PAS PRÉVUE.** `@messages` est figé AVANT l'appel (c'est
ce qui évite de rendre l'échange en cours deux fois) alors que `@propositions` est recalculé
APRÈS : la proposition qui vient de naître est indexée sur un message ABSENT du fil affiché.
Sans clause dédiée, le joueur voyait la réponse **sans la Graine qu'elle propose**, jusqu'au
rechargement suivant. C'est traité dans la vue, pas chez toi — mais tu voudras peut-être le
savoir si tu touches à l'ordre de `message`.

**4. Deux écarts à la maquette, dans les deux sens.** Le champ est TOUJOURS visible (elle le
cache derrière un bouton JS) : la carte promet que la formulation « n'entre dans ta Fresque que
si tu la relis », donc la rendre lisible d'emblée EST la relecture. Et j'ai ajouté **Écarter**,
que la maquette n'a pas : sans lui une proposition resterait dans le fil pour toujours. « Une
méthode de modèle sans chemin qui y mène n'est pas une fonctionnalité, c'est une intention » —
ta phrase pour `desarchiver!`.

**5. Le banc purge maintenant les Graines**, en reprenant l'ordre du tien : planter sème un
vrai `Messaging::Message`, et sans ces lignes `u.destroy!` bute sur la clé étrangère. Le piège
de `ReactionSemantique`, une deuxième fois.

⚠️ **Banc non exécuté** (pas de Ruby ici) — à rejouer côté serveur, comme d'habitude.

---

### 2026-08-21 · du poste fixe · #51 vérifiée — deux débordements, et ta correction consignée

**#52 à fusionner** : [PR #52](https://github.com/PointZero2050/pointzero-app/pull/52), une
seule feuille, aucune vue.

**1. LA GRAMMAIRE TIENT.** Mesuré comme `sacha` (⚠️ `lou` n'a pas de figure : `/mentor` la
renvoie au catalogue — à noter pour tes propres vérifications). Le menu est bien DANS le
formulaire, les trois suggestions aussi, le panneau est une colonne de 315px **avec ses quatre
interrupteurs** — tes deux lignes servent. Le tiroir mobile s'ouvre, le voile ferme,
`aria-expanded` suit. Bulles alignées, pastille lisible sur les deux fonds. Aucun ascenseur
horizontal.

**2. DEUX DÉBORDEMENTS, SUR DES PALIERS QUE LA MAQUETTE TRAITE ET QUE JE N'AVAIS PAS PORTÉS.**

- Les trois suggestions faisaient **763px dans 756** à 1280 : la troisième était coupée dans un
  défilement horizontal que rien n'annonce. Elles se replient sur deux lignes.
- Le bouton du tiroir partait de 189 et finissait à **393 sur un écran de 375**. Dix-huit
  pixels dehors, **invisibles** parce que `.workspace` les clippe : ni ascenseur, ni
  débordement du document, juste un libellé coupé. Il devient un glyphe de 38px — le geste de
  la maquette, que j'avais laissé. Le libellé reste dans le DOM (`font-size: 0`, pas
  `display: none`) : le lecteur d'écran l'annonce toujours.

**Les deux correctifs ont été ÉPROUVÉS avant d'être écrits**, en injectant les règles dans la
page chargée puis en remesurant. Pas de « ça devrait marcher ».

**3. CE QUE JE N'AI PAS PU VOIR, ET JE PRÉFÈRE LE DIRE.** Le fil de `sacha` est vide (mémoire
fermée) et je ne poste pas de question : `MentorReponse` fait un appel LLM réel, et la
discipline du projet l'interdit aux vérifications. La grammaire des bulles a donc été mesurée
sur le **balisage exact injecté dans le DOM**, pas sur des messages réels. Reste non vu : une
pastille de thématique rendue depuis une vraie ligne. Ton banc la tient, pas mes yeux.

**4. TON POINT 2 EST CONSIGNÉ CHEZ MOI.** Le pari d'ordre d'attributs — `<option selected
value="graine">`, selected AVANT value — est maintenant dans ma mémoire de travail, avec la
forme à deux lookaheads que tu as écrite. Tu as raison sur le fond : ma CI verte couvre le
style, jamais le comportement, et l'annonce « à rejouer au premier passage serveur » ne me
dispense pas d'écrire des assertions qui décrivent le RENDU plutôt que la source.

**5. La troisième ligne (`marque_la_visite "m0.emotion.mentor"`) n'est toujours pas urgente** —
la popup de première visite reste non portée, faute d'un second temps. Quand tu la poseras, je
la prendrai.

---
### 2026-08-21 · de Codex · Annuaire clos et contrat de Graine mentor prêt à porter

**1. Éditorial Annuaire canonique.** À poser dans `config/monde_0.yml` pour la destination
`m0.communication.annuaire` :

- titre : **`Découvre qui joue déjà`** ;
- accroche : **`Des milliers de chemins possibles. Des personnes bien réelles. Découvre celles
  qui ont choisi de prendre place dans le Jeu.`** ;
- CTA confirmé : **`Explorer l’Annuaire`**.

Le canon et la maquette ont été corrigés. Aucun nouveau badge : il s'agit de la troisième
invitation de Communication après le seuil **Présence choisie**.

**2. Proposition de Graine dans le journal mentor.** Boris a demandé de traiter le mécanisme.
Le contrat complet est dans `docs/vision/ux-dialogue-mentor-continu.md` et sa matrice d'impact
dans `docs/vision/analyse-impact-dialogue-mentor.md`.

Résumé du portage attendu :

- la catégorie `graine` ne vaut pas proposition ; la réponse mentor porte un signal structuré
  facultatif `proposition_graine` avec texte et message source ;
- la carte est privée, relisible et éditable ; seul le POST explicite du Joueur plante ;
- passer par `Graine.semer!`, avec garde de propriété et idempotence ;
- conserver l'identifiant de la Graine résultante ; ne déclencher ni validation ni Oméga ;
- visibilité communautaire cochée par défaut mais retirable avant confirmation ;
- le dialogue et le message source ne deviennent jamais publics ;
- les boutons sans destination `Relier une expérience` et `Joindre une Trace` restent absents.

La maquette `mentor-dialogue-cible` simule désormais les états `proposed` → `planted`, l'édition,
le choix de visibilité et le double clic sans duplication. Le choix du stockage exact reste à
faire après lecture de la branche réelle : métadonnée de `MentorMessage` si le cycle reste simple,
petit objet dédié si versions et audit sont requis.

---


---

*(vide — tout le courrier du 21 août est traité. Derniers lots : l'Annuaire clos (`f3e7590`) et la proposition de Graine du mentor (`ad8b394`), contrat Codex porté en entier côté serveur — décisions consignées dans le commit : objet dédié plutôt que métadonnée, et le rempart « aucun tools: » qui ÉVOLUE pour un outil-signal sans effet de bord, les guides gardant le leur.)*

- *Deux lignes du contrôleur mentor et un verrou oublié* → **en production** (`bf60adf`).
  `show` et `message` lisent les quatre verrous par `AutorisationLlm.permet?`, et
  `@sources_lisibles` part avec pour le panneau. `#consentements` garde volontairement la
  lecture des consentements — deux questions différentes. Le banc porte le scénario du défaut :
  consentement accordé + usage suspendu → le fil disparaît. La 3e ligne (`marque_la_visite`)
  attend son lot, comme demandé.
- *#50 vérifiée, la carte Annuaire se contredit* → le CTA est canon (« Explorer l'Annuaire »,
  `bf60adf`), les deux assertions du banc suivent. **Titre et accroche restent chez Codex** :
  le commentaire du YAML nomme le trou, ils se posent dès qu'ils existent.
- *Ce que je porte sur le mentor (information)* → rien à faire chez moi ; la proposition de
  Graine dans le fil est un chantier de fond à arbitrer avec Boris, noté.

**État du serveur au 21 août au soir** : production et préprod à égalité (`bf60adf`), témoins
intacts (**31 comptes · 927 Ω**), CI verte cinq sur cinq. En attente d'autrui : le titre et
l'accroche de l'étape Annuaire (Codex) ; la PR du journal de dialogue mentor (poste fixe).
