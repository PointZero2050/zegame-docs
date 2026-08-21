# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · ⚠️ ARBITRAGE DEMANDÉ par Boris — la coque de la messagerie M0

**Attendu : ton arbitrage AVANT que j'écrive une ligne.** Boris a regardé
`/echanges` contre `messagerie-par-mondes-cible/?stage=m0` et tranche : « ça ne correspond pas
du tout ». Il m'a demandé de te soumettre le choix d'architecture d'abord, et de vérifier les
specs auprès de Codex en parallèle. Je ne construis rien tant que vous n'avez pas répondu.

**CE QUE J'AI MESURÉ, pour que tu arbitres sur des faits :**

| | maquette | réel |
|---|---|---|
| largeur | messagerie pleine largeur, coque `280px + 743px` | **racine à 720px, décalée à 280px** — le `.container` Bootstrap du gabarit la serre |
| structure | `.messaging-shell` : liste à gauche, conversation à droite | une seule colonne, aucune conversation |
| vocabulaire | `spaces-panel`, `space-row`, `space-icon`, `unread`, `conversation-panel`, `conversation-head`, `workspace`, `message-avatar`, `reaction`, `is-mine` | `pz-echange-*`, entièrement le mien |

**Autrement dit, ce n'était pas un portage strict mais un habillage « dans l'esprit ».** C'est
ma décision du 19 août, et je l'assume : j'avais écarté la reconstruction de la coque comme
« un chantier d'architecture frontend hors de mon rôle ». Boris voit l'écart, donc la décision
est à reprendre. **Le carcan à 720px, lui, est un défaut dans tous les cas** — aucune autre
page du lot M0 n'est dans un `.container`.

**LES TROIS CHEMINS, ET CE QUI LES SÉPARE VRAIMENT :**

1. **Coque complète par CADRE TURBO.** `/echanges` rend la liste, et un `turbo_frame` à droite
   charge `/espaces/:id` tel quel. **Aucun contrôleur touché** : je n'ajoute qu'un
   `turbo_frame_tag` dans la vue du fil, qui est ma zone. ⚠️ **Ce serait la PREMIÈRE
   utilisation de Turbo frames du dépôt** (`turbo-rails` est là, `importmap` le sert, aucune
   vue ne s'en sert) — un patron nouveau, et c'est exactement le genre de chose que tu dois
   arbitrer plutôt que moi.
2. **Coque complète, en te demandant le serveur.** Tu exposes le fil d'un espace depuis
   `echanges#index`. Sans patron nouveau, mais `espaces#show` prépare **huit** ivars
   (`@contexte`, `@thread`, `@messages`, `@sondages`, `@propositions`, `@actions_de_fil`,
   `@decisions`, `@objets_derives`) : ou tu les dupliques, ou tu les extrais. Et je suis bloqué
   jusque-là.
3. **La colonne des espaces seule**, au vocabulaire exact, pleine largeur. Livrable tout de
   suite, sans dépendance — mais Boris verra toujours une liste là où la maquette montre une
   messagerie. Je ne le recommande pas après ce qu'il vient de dire.

**Boris a par ailleurs tranché que la page du fil est dans le MÊME lot** : si la coque montre
le fil, l'habiller à moitié se verrait immédiatement. Je vérifierai sur un canal M0 **et** sur
un Cercle réel — les objets, sondages et décisions du Monde 1 passent par cette vue, et je ne
redessine pas ces blocs.

**UN FAIT QUI CHANGE UNE DE MES DÉCISIONS.** J'avais refusé le `threshold-banner` de la
maquette le 20 août au motif qu'« aucun marqueur réel n'existe derrière ». **C'est faux
aujourd'hui** : `echanges#index` appelle `marque_la_visite "m0.communication.echanges"`, donc
`@premiere_visite` est disponible, et trois vues le consomment déjà. Le bandeau de première
visite redevient portable — je le porterai, sauf objection.

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
