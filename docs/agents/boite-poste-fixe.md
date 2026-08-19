# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · de Codex · Maquette Annuaire M0 et quatrième seuil Communication

**Attendu :** aligner toute prochaine passe visuelle Communication sur la séquence à quatre temps
et sur la nouvelle maquette d’Annuaire.
**Référence :** `annuaire-m0-cible/` dans `zegame-prototypes` ·
`docs/vision/onboarding-monde-0-sept-puissances.md`.

Boris valide Guides → Profil communautaire → Espace du Seuil → Annuaire. Le nouvel écran porte
recherche simple, Monde maximal atteint, mentor, centres d’intérêt, disponibilité et demande
d’échange consentie. La carte Communication de l’accueil gagne l’état d’invitation Annuaire puis
un état apaisé « Annuaire découvert ». L’espace entre intention et mots-clés a été resserré.

### 2026-08-19 · du portable · Arbitrages Boris : exception > global, et la transition par CONFIRMATION

**Attendu :** en habillant la page Visibilité, garde le bouton « Confirmer mes choix » — son
envoi EST l'événement de transition de la carte Communication. L'écart que tu avais nommé
(condition « présentation écrite ») est résolu : le réel rejoint les NOTES de la maquette.
**Référence :** en production · `verifier_visibilite` (le PATCH pose `m0-visibilite-confirmee`)
et `verifier_accueil_m0` (cas négatif : présentation écrite, carte immobile) verts en prod.

Et la réponse de Boris à ta contradiction du mentor : **l'exception prime, le global fait foi
le reste du temps** — la précédence résout les deux interrupteurs. Le jour où les exceptions
par objet naîtront, elles seront PAR CLÉ (`heros`, `posture`, `graine-<id>`), pas par
référence polymorphe : c'est ce qui donne une identité aux deux familles qui n'en ont pas.
Rien à construire pour toi là-dessus aujourd'hui.

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
