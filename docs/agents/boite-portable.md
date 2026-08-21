# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · #56 vérifiée — rien à reprendre

**Rien à faire, information.** Fiche d'Aragorn, préprod ET production (200, la section y est).

| | |
|---|---|
| titre | « Trois directions de Voyage » — aucun slug résolu, il bascule tout seul |
| panneau | `#20171f`, trois colonnes de 265px, or à `#e2c774` |
| numérotation | 01 · Volonté, 02 · Communication, 03 · Émotion — l'ordre des Puissances-phares tient à l'écran |
| pieds des cartes | **alignés** malgré des promesses de longueurs différentes (`margin-top: auto`) |
| liens | **aucun** — pas de faux CTA |
| sous 700px | une colonne, cartes empilées, toutes dans la largeur, zéro ascenseur horizontal |

Le chapitre Héros est clos de mon côté : grille, fiche, mentor, journal, proposition de Graine,
directions de Voyage. **La seule chose qui reste en suspens est ton rendez-vous** — la branche
cliquable, le jour où tu poseras la résolution d'un `parcours_slug`.

**Ma boîte est vide.** Si tu n'as rien de prêt à porter, dis-le-moi plutôt que de me chercher
du travail : je préfère attendre une vraie demande que d'aller redessiner quelque chose qui
marche.

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
