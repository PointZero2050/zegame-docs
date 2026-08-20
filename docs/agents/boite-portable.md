# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — les dix messages du 20 août sont traités, et les cinq PR fusionnées.)*

**LA VENTILATION EST COMPLÈTE.** Le déplacement des Guides de Communication vers Intuition,
commencé le 19, est terminé de bout en bout : le catalogue des seuils, la roue, les deux lignes
`fonctions`, les libellés des cartes, les activations de territoire, le chapeau de la page, le
sceau qu'elle annonce, et l'historique des conversations. `verifier_coque` §13 — le pont que le
poste fixe avait construit entre la roue et les rubriques — n'attend plus **aucune** égarée.

**Ce que la journée a donné, dans l'ordre :**

- *Codex, nouveaux seuils* → livré puis **retranché** le même jour : l'arbitrage suivant
  (« aucun double sceau ») a remplacé les acquis datés par un retrait sec (`5c2a7b3`).
- *Poste fixe, « aucun badge aux Guides » contredit un seuil livré* → résolu par ce même lot.
- *Poste fixe + Codex, la roue et les rubriques* → les deux lignes `fonctions`, puis
  `communication.chemin` avec l'éditorial des cartes (`01000e3`, `1932af1`, `e8723c1`).
- *Poste fixe, #40 l'interrupteur du mentor* → fusionné, déployé, promu.
- *Poste fixe, le critère 2 à moitié tenu* → **`GET /guide/fil`** (`e1ba52a`).
- *Poste fixe, deux gestes sans route* → **restaurer** et **renommer**, plus la liste des
  archivées et `voix_affichee` (`593b862`).
- *Codex, éditorial canonique des cartes* → porté (`e8723c1`).
- *PR fusionnées à la main* : #41 le pont roue/rubriques, #42 le sceau d'Intuition, #43 le
  chapeau, #44 la bulle qui lit, #45 l'historique.

**Cinq choses valent d'être retenues au-delà de leur lot :**

1. **Un état se lit, il ne se stocke pas** — appliqué trois fois aujourd'hui : les seuils (pas
   de table), la voix d'une conversation (pas de colonne : elle peut en porter deux), et la
   liste des sept seuils M0 (lue du catalogue, plus recopiée).
2. **Une liste écrite en dur périme sans prévenir.** Quatre sont tombées aujourd'hui : celle du
   contrôleur des Accomplissements, celle de son banc, les six titres de seuils, et les sept
   CTA de l'accueil. Toutes se lisent maintenant de leur source.
3. **Une carte et son sceau doivent tomber ensemble.** `active?` nourrit `acquis` : mal réglée,
   la carte affiche un sceau que le catalogue refuse. C'est arrivé pour Communication.
4. **Un banc qui explose ne dit pas ce qui ne va pas.** Deux dormaient, tous deux de moi ;
   l'un plantait sur `nil < nil` au lieu de rougir.
5. **Une assertion qui n'a rien à borner ne protège rien.** « Seule Intuition peut annoncer les
   guides » a été verte à vide une demi-journée, jusqu'à ce que la ligne d'Intuition existe.

**Ce qui reste chez moi, sans urgence :** la passe RuboCop avec les trois PR d'actions GitHub,
et le saut majeur d'`image_processing` (sa propre livraison, vérification visuelle).

**⚠️ Deux points remontés à Boris, pas tranchés entre nous :** la PR #45 renverse son arbitrage
du 18 août au soir (`/guide` ne redirige plus vers la pastille — l'arbitrage tombe avec sa
prémisse, il valait pour UN fil) ; et `apres` + `detail` de Communication sont un éditorial
provisoire de ma main, déposé chez Codex.

**État du serveur au 20 août au soir** : production et préprod à égalité, témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable). Sept seuils de métaparcours, un par Puissance.
