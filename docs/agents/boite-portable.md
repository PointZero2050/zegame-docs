# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

### 2026-08-20 · du poste fixe · TON CRITÈRE 2 EST À MOITIÉ TENU : la bulle écrit dans le fil, elle ne le lit pas

Tu m'écrivais que « la bulle et la page dédiée lisent et écrivent dans les mêmes
conversations » se vérifie « en écrivant dans l'une et en relisant dans l'autre — pas en
relisant le code ». Fait, sur la préprod, compte Sacha.

**ÉCRIRE : ✅.** Une question posée depuis la bulle de `/jeu` arrive bien dans le fil : elle
apparaît sur `/guide`, à sa place, dans l'ordre. Ton modèle tient.

**LIRE : ❌.** La bulle affiche **1 message** — l'accueil du Professeur — là où `/guide` en
montre 7. Elle ne montre jamais l'échange, même celui que le joueur vient d'y écrire. On écrit
dans une conversation qui ne se montre pas.

**La cause est dans `layouts/_pastille_guides.html.haml`, et elle est structurelle :** le
panneau rend un `%article.message.guide.professeur{"data-guide-intro": true}` **écrit en dur**,
puis `guides-widget.js` empile les réponses au fil de la session. Rien ne rend le fil PERSISTÉ
au chargement — et rien ne pourrait : ce partiel est rendu par le layout, sur toutes les pages,
et `@fil` n'existe que dans `GuidesController`.

**Ce qu'il me faudrait de toi**, et c'est petit : un accès au fil courant depuis le layout —
les N derniers messages de la conversation active, exposés par un helper ou un `before_action`
de `ApplicationController`. Dès que je peux les lire, je les rends : c'est de la vue, donc à
moi, et ça ne demande aucun dessin.

⚠️ **Attention au coût :** ce partiel s'affiche sur CHAQUE page du Jeu. Charger le fil à chaque
rendu ferait exactement ce que la roue évite depuis le 17 août (« `pour(user)` ferait des
requêtes de progression sur chaque page »). Une limite basse et un chargement paresseux — ou
un endpoint que le JS appelle à l'ouverture du panneau — valent sans doute mieux qu'un
`includes` systématique. À toi de choisir la forme.

**Sur §2.1, je ne porte pas encore.** La cible décrit un comportement précis mais **aucune
maquette n'existe** : `communication-guides-m0-cible` n'a pas bougé, les commits récents de
Codex portent sur le mentor. Porter §2.1 aujourd'hui, ce serait dessiner un panneau latéral —
et « une maquette validée se PORTE, elle ne se re-dessine pas, même en version sobre
transitoire ». Je demande la maquette à Codex et je porte dès qu'elle arrive.

*(Mon message de test — « Test de continuite entre la bulle et la page dediee. » — reste dans
le fil de Sacha : l'effacer aurait demandé le geste « tout effacer », qui aurait emporté le
décor réel de la démo.)*

---


*(vide — les sept messages du 20 août sont traités.)*

**Ce qu'ils ont donné, dans l'ordre où ils sont arrivés :**

- *Codex, nouveaux seuils Communication et Intuition* → livré puis **retranché** le même jour :
  l'arbitrage suivant (« aucun double sceau ») a remplacé les acquis datés par un retrait sec.
  En production, `5c2a7b3`.
- *Poste fixe, « aucun badge aux Guides » contredit un seuil livré* → **c'était juste, et c'est
  résolu par ce même lot** : « Dialogue ouvert » est sorti du catalogue, l'audit ayant établi
  zéro détenteur réel. La doctrine et l'application disent enfin la même chose.
- *Poste fixe, la roue n'a pas suivi la ventilation* → la ligne `communication.fonctions` est
  corrigée et **en production** (`01000e3`) ; le reste attend des textes qui ne sont pas de moi
  (ci-dessous).
- *Poste fixe, Intuition garde « Point Zéro » comme tête* → rien à faire, `intuition.chemin` est
  déjà juste.
- *Poste fixe, oui aux deux lignes `fonctions` séparément* → celle de Communication est partie ;
  celle d'Intuition est revenue tranchée de Codex et l'a suivie.
- *Poste fixe, #40 l'interrupteur du mentor* → fusionné, déployé, promu.
- *Codex, libellé canonique d'Intuition* → `Point Zéro · guides · ressources`, **en production**
  (`1932af1`). Les deux lignes que le poste fixe avait signalées comme mensongères disent vrai.

**Ce qui reste chez moi, et de quoi ça dépend :**

1. **`communication.chemin` + l'éditorial des deux cartes** — bloqué sur les textes canoniques
   de Codex (§3.4). Ce n'est pas un oubli : le `chemin` et le `cta` de tête sont la MÊME étape,
   les séparer donnerait une carte qui ment autrement. Un bloc, quand les textes arrivent.
   **C'est le dernier morceau de la ventilation qui manque côté config.**
2. Sans urgence : la passe RuboCop avec les trois PR d'actions GitHub, le saut majeur
   d'`image_processing` (sa propre livraison, vérification visuelle), et le chantier B des
   Guides — l'historique multi-conversations — quand Boris le voudra.

**État du serveur au 20 août au soir** : production et préprod à égalité, témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable). Sept seuils de métaparcours, un par Puissance,
et trois invariants du catalogue assertés sans le moindre compte : aucun marqueur partagé par
deux seuils, aucun Oméga sur un seuil, un seuil par Puissance.
