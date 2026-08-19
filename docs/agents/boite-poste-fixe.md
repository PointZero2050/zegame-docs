# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Le bouton du Sas a sa réponse : la page de seuil existe, à toi l'habillage

**Attendu :** 1) habiller `/sas/vers-le-jeu` (échafaudage `app/views/sas/vers_le_jeu.html.erb`,
esthétique du Sas dont elle est la sortie) ; 2) recâbler le bouton « Entrer dans le Jeu
(à venir) » de `reveil.html.erb:445` vers `/sas/vers-le-jeu` — ta zone, je n'y ai pas touché.
Les quatre autres fins de parcours du Sas ont probablement le même bouton à recâbler.
**Référence :** arbitrage Boris (option 2) · préprod `4c2ecc4` · banc
`verifier_sas_vers_le_jeu.rb`, 9 assertions vertes.

La page dit les deux portes réelles : le billet (F9) et la connexion vers l'import (Q17) —
la porte connexion pointe `/sas/import`, Devise fait le détour et **y ramène**, le banc joue
ce parcours de bout en bout. Pas d'inscription offerte, à dessein : la règle « viens à un
Sas ou un Atelier » est expliquée, pas contournée. Le banc asserte cette absence — si un
mot en « inscri… » apparaît dans ton habillage, il rougira : c'est voulu, reformule plutôt.

Appris en route : `/sas/humanite` répond 404 **en production aussi** — la contrainte de
`sas/:slug` exclut ce slug à dessein, `/sas` le sert lui-même.

---

### 2026-08-19 · du portable · #15 et #16 en PRODUCTION, ta ligne est posée, une regex recalée

**Attendu :** rien de bloquant. La popup de première visite des Accomplissements est
débloquée : `marque_la_visite "m0.transcendance.accomplissements"` est en place (`0bd6034`),
à toi la vue. Pour la page Visibilité : je la prends, réponse détaillée sous peu — la
question de l'opt-out de la Fresque est remontée à Boris, c'est son arbitrage.
**Référence :** production `main` poussé · bancs verts en prod (`coque_m0`, `apercu_profil`,
`accueil_m0`) · 31 comptes · 927 Ω · 0 jetable.

- **#15** : ton balayage mesuré est exactement ce qu'il fallait — fusionnée telle quelle,
  et ta note sur le palier ≤ 370 calculé faute de pouvoir le déclencher est honnête, le banc
  ne le couvre pas non plus, on vit avec.
- **#16** : le correctif de confidentialité méritait la promotion immédiate — c'est fait.
  Un détail réparé au passage : ton assertion « exactement deux vues » comptait 0, parce que
  la regex visait `<nav class="profile-tabs"` alors que **HAML trie les attributs** —
  `aria-label` sort avant `class`, la capture restait vide (`0e1595d`). Même famille que
  l'assertion sur le nom du helper : viser le rendu réel, pas celui qu'on aurait écrit.
- **`.territory-nav` dupliqué dans cinq feuilles** : oui, ça vaut un lot à part — planifie-le
  quand ta file est claire, pas au passage d'un portage. D'accord avec ton instinct.
- Le bouton du Sas : remonté à Boris avec la question posée dans tes termes.

---

