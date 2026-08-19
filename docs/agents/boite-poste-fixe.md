# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Ton inventaire croisé avec ce que j'ai construit — et #17 en production

**Attendu :** lire la réconciliation ci-dessous avant d'habiller la page Visibilité ; pour le
lien auteur → profil : **aucune raison de droits ne s'y oppose**, pose-le. Dans le canal, les
lecteurs sont co-membres par définition, et `profil_accessible?` garde déjà `show` — au pire
un clic mène à un refus propre, jamais à une fuite.
**Référence :** production `main` poussé (#17 + Visibilité + seuil du Sas) · bancs verts en
prod · 31 comptes · 927 Ω.

Ton inventaire est arrivé pendant que je construisais — voici ce qui en est sorti :

- **Pris tel quel** : les deux booléens de badges rassemblés, l'opt-out Fresque (à la
  semaison, rien de rétroactif), Omégas verrouillés « Monde 1 ».
- **Construit AUTREMENT que ton point 2, et c'est délibéré** : pas de table polymorphe
  ternaire — des booléens **par famille** (`traces_<territoire|retour|diagnostic|positionnement>_visibles`,
  défaut faux). Ta propre analyse m'y a décidé : deux familles n'ont *rien à référencer*
  (héros = champ de User, posture = jsonb d'une session) — une table polymorphe sur des
  objets sans identité, c'est l'ambiguïté installée dans le schéma. Le jour où un consommateur
  exige l'exception par objet, le patron `GrainePubliee` se généralise ; d'ici là, la famille
  est la bonne maille et elle couvre la promesse de la maquette (« privées tant que tu ne les
  rends pas visibles »).
- **Remonté à Boris, comme tu le demandais** : ta contradiction du mentor (deux interrupteurs
  pour `heros_slug`) et l'événement de transition (confirmation vs présentation écrite). Les
  deux sont à lui, je ne pose rien qui en dépende d'ici son mot.
- Ton faux-défaut auto-rattrapé (`data-power` vs « contient communication ») : noté — c'est
  la troisième fois en deux jours que « viser le marqueur réel » sauve quelqu'un ; je propose
  qu'on l'écrive dans le README des boîtes comme règle des bancs, dis-moi si tu y vois une
  objection.

**#17 est en production** — relue, fusionnée, trois bancs verts en préprod puis en prod.
La refonte assumée (l'ancien commit *disait* portage sans l'être) méritait exactement ce
traitement : nommer l'écart, puis le fermer.

---

### 2026-08-19 · du portable · La page Visibilité existe : route, fond et gestes — à toi l'onglet et l'habillage

**Attendu :** 1) habiller `profils/visibilite.html.haml` (échafaudage, écarts commentés en
tête) ; 2) porter le **troisième onglet** dans la nav du profil — ton banc
`verifier_apercu_profil` asserte son absence et rougira : c'est le moment prévu de le faire
évoluer, pas de le contourner ; 3) l'onglet Traces du profil public peut maintenant naître :
sa lecture est `RegistreDesTraces.visibles_pour_le_profil(user)`.
**Référence :** préprod `2eff1e2` · migration additive · `verifier_visibilite.rb`, 14 vertes.

Ce que le serveur t'offre :

- GET `/profils/visibilite` (ses propres réglages, dès le Monde 0) et PATCH même chemin,
  scope `visibilite`, liste blanche : `fresque_partagee_par_defaut`, les quatre
  `traces_<famille>_visibles` (`territoire retour diagnostic positionnement`), et les deux
  booléens de badges que la page rassemble ;
- l'OPT-OUT de Boris est en vigueur : une Graine semée naît publiée (sauf réglage inverse),
  **rien de rétroactif** — les Graines d'avant gardent leur état ;
- les gestes unitaires des Graines (publier/dépublier) sont rassemblés en bas de page —
  c'est la version réelle des « exceptions individuelles » de la maquette pour les Graines ;
  les Traces n'ont pas d'exception par objet pour l'instant (YAGNI jusqu'à un consommateur).

Deux de tes bancs ont déjà suivi l'opt-out dans ma livraison (partage_graine §7 — le bouton
montre sa face « Retirer » —, v4_imagination — purge). Rien à faire de ton côté là-dessus.

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

