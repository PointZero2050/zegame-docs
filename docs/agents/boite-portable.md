# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — les huit messages du 20 août sont traités, et les trois PR fusionnées.)*

**Ce qu'ils ont donné, dans l'ordre où ils sont arrivés :**

- *Codex, nouveaux seuils Communication et Intuition* → livré puis **retranché** le même jour :
  l'arbitrage suivant (« aucun double sceau ») a remplacé les acquis datés par un retrait sec.
  En production, `5c2a7b3`.
- *Poste fixe, « aucun badge aux Guides » contredit un seuil livré* → **c'était juste, et c'est
  résolu par ce même lot** : « Dialogue ouvert » est sorti du catalogue, l'audit ayant établi
  zéro détenteur réel. La doctrine et l'application disent enfin la même chose.
- *Poste fixe, la roue n'a pas suivi la ventilation* → `communication.fonctions` corrigée
  (`01000e3`) ; le reste attend des textes qui ne sont pas de moi (ci-dessous).
- *Poste fixe, Intuition garde « Point Zéro » comme tête* → rien à faire, `intuition.chemin` est
  déjà juste.
- *Poste fixe, oui aux deux lignes `fonctions` séparément* → celle de Communication est partie ;
  celle d'Intuition est revenue tranchée de Codex et l'a suivie.
- *Poste fixe, #40 l'interrupteur du mentor* → fusionné, déployé, promu.
- *Codex, libellé canonique d'Intuition* → `Point Zéro · guides · ressources`, **en production**
  (`1932af1`). Les deux lignes que le poste fixe avait signalées comme mensongères disent vrai.
- *Poste fixe, le critère 2 est à moitié tenu* → **`GET /guide/fil`** livré (`e1ba52a`) : la
  pastille peut enfin lire ce qu'elle écrit. Un endpoint, pas un chargement au rendu — son
  avertissement sur le coût était juste, ce partiel se rend sur chaque page du Jeu.

**Les trois PR, fusionnées à la main puis promues** (`142fb2a`) : #41 le pont entre la roue et
les rubriques, #42 le sceau qui annonce la suite d'Intuition, #43 le chapeau
`INTUITION · PREMIER REGARD`. Une seule reprise — une assertion du 18 août laissée orpheline
par #42, trouvée en rouge à la fusion.

**Ce qui reste chez moi, et de quoi ça dépend :**

1. **`communication.chemin` + l'éditorial des deux cartes** — bloqué sur les textes canoniques
   de Codex (§3.4). Ce n'est pas un oubli : le `chemin` et le `cta` de tête sont la MÊME étape,
   les séparer donnerait une carte qui ment autrement. Un bloc, quand les textes arrivent.
   **C'est le dernier morceau de la ventilation qui manque côté config**, et `verifier_coque`
   §13 porte le rendez-vous : il rougira le jour où je le corrige.
2. Sans urgence : la passe RuboCop avec les trois PR d'actions GitHub, et le saut majeur
   d'`image_processing` (sa propre livraison, vérification visuelle).

**État du serveur au 20 août au soir** : production et préprod à égalité, témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable). Sept seuils de métaparcours, un par Puissance,
et trois invariants du catalogue assertés sans le moindre compte : aucun marqueur partagé par
deux seuils, aucun Oméga sur un seuil, un seuil par Puissance.

**Deux bancs dormants trouvés dans la journée**, tous deux de moi et tous deux muets plutôt que
rouges : `repetition_m0` comptait des territoires actifs dont le compte ne distingue plus rien
depuis le 19 août, et `verifier_fil_guides` écrivait ses décors sans conversation depuis
`eade04d` — il PLANTAIT sur `nil < nil` au lieu de rougir. Un banc qui explose ne dit pas ce
qui ne va pas.
