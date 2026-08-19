# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Arbitrage Boris : la Fresque passe en OPT-OUT

**Attendu :** rien pour l'instant — je construis la page Visibilité sur cette base et je te
préviens quand la route existe. Ton banc qui asserte l'absence de l'onglet rougira à ce
moment-là, comme prévu.
**Référence :** décision de Boris, 19 août — la maquette `profil-communautaire-m0-cible`
avait raison, le réel avait tort.

Le sens retenu : une Graine de Fresque est **partagée par défaut**, le joueur peut la
retirer. Mon plan d'implémentation, pour que tu saches où ça va : l'opt-out se fera **à la
semaison** — `semer!` depuis la Fresque créera la `GrainePubliee` d'office, la page
d'édition permettant de dépublier aussitôt. Le modèle de lecture ne change pas
(`GrainePubliee` reste la vérité), et surtout **rien n'est rétroactif** : les Graines déjà
semées sous le régime opt-in gardent leur état — les exposer d'office trahirait ce que
leurs auteurs croyaient au moment d'écrire.

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

### 2026-08-19 · du portable · La carte Communication progresse — à regarder sur la préprod

**Attendu :** vérifier le rendu de la carte aux trois étapes, puis verdict ici. Je promeus
sur ton feu vert.
**Référence :** préprod `57c56b5` · banc `verifier_accueil_m0.rb` vert (dont 7 assertions
neuves sur cette progression).

Constat de Boris : après un dialogue avec un guide, la carte de l'accueil restait sur
« Rencontre les deux guides ». Elle progresse désormais : guides → profil communautaire →
Espace d'échange. Même mécanique que la carte Imagination (destinations incrémentales).

Le parcours de vérification, avec les comptes du décor :

1. `/acces-verification/sacha?vers=/jeu` — Sacha n'a jamais dialogué : carte de base,
   « Dialoguer avec les guides » ;
2. pose une question à un guide avec lui, reviens sur `/jeu` : la carte doit inviter
   « Créer ton profil communautaire » (surbrillance, image de repli = celle de la Puissance,
   les webp dédiées n'existent pas encore) ;
3. visite `/profils/apercu`, écris une présentation, reviens : « Entrer dans l'Espace
   d'échange » ;
4. visite `/echanges` : la carte s'apaise, et reste une porte vers l'Espace d'échange —
   c'est la règle de la matrice (l'image du dernier territoire révélé reste), pas un oubli.

Nino et Lou ont déjà dialogué et un profil selon l'état du décor — Sacha est le seul
propre pour l'étape 1. Rien n'a changé dans tes vues : la carte est rendue par le même
partial, seules la config et deux `marque_la_visite` (profils#apercu, echanges#index) ont
bougé côté serveur.

---
