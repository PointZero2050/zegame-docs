# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · #56 — les trois Directions de Voyage sont rendues

**À relire et fusionner.** [PR #56](https://github.com/PointZero2050/pointzero-app/pull/56).
Vue, CSS, banc. **Le commentaire de l'écart n° 4 est tombé**, comme tu le disais — il annonçait
« le bloc apparaîtra de lui-même le jour où la donnée existera », et c'est ce jour.

**1. ⚠️ LA BRANCHE CLIQUABLE N'EST PAS ÉCRITE, ET J'AI POSÉ UN RENDEZ-VOUS PLUTÔT QUE DE LA
DEVINER.** Le contrat §2 la conditionne à un `parcours_slug` qui désigne un parcours existant
ET accessible ; les 144 sont nuls. L'écrire demanderait de résoudre un slug vers un `Parcours`
et de lire l'état du Joueur — ta zone — et surtout de deviner le CTA, le Monde minimal et la
durée que le contrat veut « lus sur le parcours réel et jamais dupliqués ». Inventer ça, c'est
exactement ce que le contrat interdit.

**Le banc attend donc ZÉRO slug résolu sur les 48 figures et rougira au premier.** Quand tu
poseras la résolution, cette ligne te dira qu'il est temps d'écrire la branche — plutôt qu'on
la découvre morte le jour où quelqu'un s'étonne qu'une carte reliée ne mène nulle part.

**2. Le titre bascule tout seul.** « Trois directions de Voyage » tant que rien n'est relié,
« Parcours associés » (le titre de la maquette) dès qu'un slug l'est. Annoncer des parcours
qui n'existent pas serait le faux CTA que le contrat écarte, en plus grand.

**3. Un écart de teinte, MESURÉ.** L'or des libellés passe de `#d7bd62` à `#e2c774` : sur
`#20171f` l'original donne 5,9:1, bon pour le 11px de la maquette, mais ces `small` sont à 10px
après le passage à Roboto Slab et la règle du lot est de ne jamais descendre sous 4,5 pour du
petit texte. 7,4:1 après.

**4. Le banc asserte l'ORDRE côté écran.** Le tien le garantit côté donnée ; la fiche numérote
01/02/03 en s'appuyant dessus, donc un ordre qui changerait nommerait la mauvaise Puissance
sous le bon titre. Les deux assertions ne font pas doublon : elles tiennent les deux bouts de
la même promesse.

⚠️ **Banc non exécuté** (pas de Ruby ici). Vérification navigateur dès le déploiement — fiche
d'Aragorn, desktop et sous 700px où les trois cartes s'empilent.

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
