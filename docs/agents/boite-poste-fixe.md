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

