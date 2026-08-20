# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — les neuf messages du 20 août sont traités, et les cinq PR fusionnées.)*

**Ce que la journée a donné, dans l'ordre :**

- *Codex, nouveaux seuils Communication et Intuition* → livré puis **retranché** le même jour :
  l'arbitrage suivant (« aucun double sceau ») a remplacé les acquis datés par un retrait sec.
  En production, `5c2a7b3`.
- *Poste fixe, « aucun badge aux Guides » contredit un seuil livré* → **c'était juste**, et le
  retrait sec l'a résolu : l'audit a établi zéro détenteur réel.
- *Poste fixe, la roue n'a pas suivi la ventilation* → les deux lignes `fonctions` disent vrai
  (`01000e3`, `1932af1`) ; `communication.chemin` reste en attente des textes de Codex.
- *Poste fixe, #40 l'interrupteur du mentor* → fusionné, déployé, promu.
- *Poste fixe, le critère 2 est à moitié tenu* → **`GET /guide/fil`** (`e1ba52a`) : la pastille
  peut lire ce qu'elle écrit.
- *Poste fixe, deux gestes de la maquette n'ont pas de route* → **restaurer** et **renommer**
  livrés, plus la liste des archivées et `voix_affichee` (`593b862`).
- *PR fusionnées à la main* : #41 le pont roue/rubriques, #42 le sceau d'Intuition, #43 le
  chapeau, #44 la bulle qui lit, #45 l'historique.

**Trois choses valent d'être retenues au-delà de leur lot :**

1. **Pas de colonne `voix` sur les conversations.** Une conversation peut porter les DEUX voix
   — une bascule ne coupe pas le fil. Une colonne mentirait dès la première bascule ;
   `voix_affichee` se lit du fil. Même doctrine que les seuils : un état se lit, il ne se stocke
   pas.
2. **`desarchiver!` existait et n'était appelé nulle part.** Sans route, archiver était une
   disparition définitive : « archiver ≠ supprimer » n'était vrai que d'un côté. Une méthode de
   modèle sans chemin qui y mène n'est pas une fonctionnalité.
3. **Deux bancs dormants, tous deux de moi, tous deux muets plutôt que rouges.**
   `repetition_m0` comptait des territoires dont le compte ne distingue plus rien depuis le
   19 août ; `verifier_fil_guides` écrivait ses décors sans conversation depuis `eade04d` et
   PLANTAIT sur `nil < nil` au lieu de rougir. Un banc qui explose ne dit pas ce qui ne va pas.

**Ce qui reste chez moi, et de quoi ça dépend :**

1. **`communication.chemin` + l'éditorial des deux cartes** — bloqué sur les textes canoniques
   de Codex (§3.4). Le `chemin` et le `cta` de tête sont la MÊME étape : les séparer donnerait
   une carte qui ment autrement. **Dernier morceau de la ventilation côté config**, et
   `verifier_coque` §13 porte le rendez-vous — il rougira le jour où je le corrige.
2. Sans urgence : la passe RuboCop avec les trois PR d'actions GitHub, et le saut majeur
   d'`image_processing` (sa propre livraison, vérification visuelle).

**⚠️ À dire à Boris, pas à trancher entre nous** : la PR #45 renverse son arbitrage du 18 août
au soir (« une page complète ET une pastille disent la même chose deux fois »). `/guide` ne
redirige plus vers la pastille, elle rend le dialogue. L'arbitrage tombe avec sa prémisse — il
valait quand il n'y avait qu'UN fil — et la maquette que Boris vient de valider décrit `/guide`
comme une page à panneau latéral. `verifier_guides_page` §3b a été RETOURNÉE, pas supprimée :
elle dit maintenant l'inverse, avec la trace du pourquoi.

**État du serveur au 20 août au soir** : production et préprod à égalité, témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable). Sept seuils de métaparcours, un par Puissance.
