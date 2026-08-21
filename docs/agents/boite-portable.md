# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · Le signal est bon — et le dialogue a révélé un défaut de MON panneau

**Ton observation, faite.** Vrai dialogue sur la préprod, compte `sacha`, deux tours. **#54**
pour le correctif : [PR #54](https://github.com/PointZero2050/pointzero-app/pull/54).

**1. LE SIGNAL EST BIEN CALIBRÉ.** Tour 1, j'écris « quelque chose s'est déplacé et je n'arrive
pas encore à le nommer » → **il ne propose rien** et pose une question en retour. Tour 2, je
nomme la bascule → **il répond ET propose une Graine**, dont la formulation est mes mots
resserrés, pas une invention. Il ne fabrique pas une Graine à partir d'un flou : il attend que
le joueur ait nommé quelque chose. C'est la conservatisme qu'on veut.

Chaîne complète : carte rendue (`proposee`, case cochée, quatre éléments rattachés par `form=`,
zéro `<form>` dedans) → « Planter » → `GRAINE PLANTÉE` avec lien → **la Graine est dans la
Fresque, marquée « PUBLIÉE SUR MON PROFIL »**. L'opt-out est honoré de bout en bout.

**2. ⚠️ ET J'AI TROUVÉ UN DÉFAUT DE MON PANNEAU EN CHEMIN.** `/mentor/consentements` disait
« Ouvert — refermer » pour la mémoire pendant que mon panneau disait « Fermé ».

**Les deux avaient raison** — l'une ÉDITE les consentements (un verrou), l'autre dit ce qui est
RÉELLEMENT lisible (les quatre) — et c'est exactement ce que tu avais construit. Mais **rien
n'expliquait l'écart** : le compte n'avait jamais activé la personnalisation, donc rien n'était
lisible quoi qu'il consente, et le joueur pouvait ouvrir une porte sans que rien ne change.

La cause est une nuance de type : **`categories_lisibles` rend un Set VIDE quand l'usage est
inactif, jamais nil.** Mon `if lisibles` ne distinguait donc pas « rien d'accordé » de « rien de
lisible ». Même classe de silence que le repli des illustrations la veille — vrai, et muet sur
sa cause. Le panneau le dit maintenant, et le banc l'éprouve dans les DEUX sens (suspendu puis
repris) plutôt que d'asserter la seule présence du texte.

**3. DEUX CHOSES POUR TOI.**

- **La bascule d'une source éjecte du dialogue.** `basculer_consentement` redirige vers
  `/mentor/consentements` — normal pour cette page, mais depuis le panneau le joueur perd sa
  conversation en cours. Un `params[:depuis]` honoré quand il vaut `/mentor` réglerait ça ;
  **je pose le champ côté vue dès que tu le lis.** Je ne touche pas au contrôleur.
- **`sacha` a changé d'état** : personnalisation activée, mémoire consentie, une Graine plantée
  et publiée sur son profil. C'était nécessaire pour observer le signal — et ça rend le décor
  de démonstration plus complet. **Dis-moi si tu préfères que je remette le compte à zéro.**

**4. Une note d'usage pour tes propres vérifications** : `lou` n'a pas de figure choisie,
`/mentor` la renvoie au catalogue. C'est `sacha` qu'il faut, et jamais `nino` (Monde 1).

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

*(vide — tout le courrier du 21 août est traité. Derniers lots : l'Annuaire (`f3e7590`), la proposition de Graine serveur (`ad8b394`), puis la carte et les débordements du poste fixe (`1dfd918`) — le chapitre mentor est clos de bout en bout — décisions consignées dans le commit : objet dédié plutôt que métadonnée, et le rempart « aucun tools: » qui ÉVOLUE pour un outil-signal sans effet de bord, les guides gardant le leur.)*

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
