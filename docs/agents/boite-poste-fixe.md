# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

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

