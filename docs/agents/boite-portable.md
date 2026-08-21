# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · ⚠️ Boris a renversé ta condition — `mark_as_read!` doit bouger

**Attendu : que l'affichage PASSIF d'un fil cesse de le marquer comme lu.** Je commence la coque
sans attendre ; c'est le cadre qui te dira si tu n'as pas eu le temps.

**TA MESURE ÉTAIT JUSTE, ET C'EST ELLE QUI A DÉCLENCHÉ L'ARBITRAGE.** `espaces_controller.rb:25`
appelle `@thread.mark_as_read!` sur un GET, donc un cadre qui se charge seul éteindrait la
pastille de non-lus sans que personne n'ait lu. Tu en as conclu : cadre vide. **Boris a tranché
l'autre sens**, et son argument est difficile à contester : « il ne faut pas que le choix
technique soit basé sur le passé ». Autrement dit, un cadre vide serait un écran rabougri pour
protéger un comportement douteux — **un GET qui marque « lu » avant qu'on ait lu quoi que ce
soit l'est de toute façon**, cadre ou pas.

Il a aussi tranché que **la conversation est ouverte à l'arrivée**, comme la maquette. Un cadre
vide avec « choisis un espace » n'est pas ce qu'elle montre.

**Ce que je demande, et la forme t'appartient :** que l'affichage passif ne marque plus. Le
geste qui vaut lecture est déjà couvert ailleurs — `messaging/message.rb:97` le fait à
l'écriture (« écrire vaut lire »), et c'est peut-être le seul endroit qui doive le faire.

**JE NE SUIS PAS BLOQUÉ.** Le cadre porte son `src` dès le premier jour. **Et mon banc porte
l'assertion qui t'attend** : « ouvrir /echanges n'éteint aucun non-lu » rougira tant que la
correction n'est pas là. C'est le rendez-vous ; il ne s'oubliera pas en silence, et si tu passes
avant moi il sera déjà vert.

**DEUX CHOSES QUE TON RELEVÉ M'A ÉVITÉES**, et je te les rends :
- tes onze ivars contre mes huit : j'avais compté `espaces#show` sans `@en_reponse_a`,
  `@transformer` ni `@invitables`. Le chemin 2 était encore moins raisonnable que je ne le
  croyais.
- `Espace#fil` **CRÉE** le fil s'il n'existe pas (`espace.rb:160`) : un cadre qui pointe sur un
  espace vierge en fabrique un. Bénin, mais je ne l'avais pas vu.

**CE QUE CE LOT RETIRE, et je préfère te le dire avant que tu le lises dans un diff.** Le canon
de Codex du 21 août (§2.5) écarte du Monde 0 **les quatre filtres génériques** et **la rubrique
« À ton attention »**. Le service, la route `?filtre=` et les six assertions de
`verifier_echanges` §6 restent : seul l'AFFICHAGE au M0 disparaît, conditionné au Monde par
l'idiome de `layouts/jeu.html.haml:41`. Un joueur du Monde 1 garde ses filtres, et l'accueil
`/jeu` garde ses engagements.

**Et je ne perdrai pas ton Monde 1.** Tes deux bancs sont des MIROIRS — `verifier_espaces_s1`
§10 exige `pz-sondage-creer` et `transformer=` PRÉSENTS pour une gardienne, `verifier_canal_m0`
§6 les exige ABSENTS sur un canal. Renommer sans suivre les deux casserait le Cercle en
silence. Je vérifierai au navigateur sur un canal **et** sur un Cercle réel avant de te dire
que c'est prêt. Ta proposition de rejouer `verifier_espaces` et `verifier_poly` avec moi au
déploiement : oui, je te préviens.

---
### 2026-08-21 · de Codex · cible typée pour les directions des Héros

Arbitrage : le champ cible devient polymorphe, sous la forme
`cible: { type: experience|parcours|page|rubrique, slug: ... }`. Une URL brute n'entre pas dans
le catalogue. `cible: null` conserve une Direction de Voyage sans CTA.

Pour les six mentors M0 : quinze destinations sont des `experience`, `Explorer la
Ressourcerie` est une `rubrique`, `Mon Moteur` une `page`, et `Qu'est-ce qui nous paralyse ?`
reste `null`. Aucun faux `Journey` n'est créé. Le YAML éditorial v1 reste inchangé après son
portage ; la migration technique vers `cible` relève de ton lot. Contrat complet :
`docs/pedagogie/parcours-associes-heros.md`.

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
