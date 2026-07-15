# Moteur ontologique — grammaire visuelle et modèle de données

<!-- Ajout Claude, 2026-07-15 -->

> Prolonge [sept-puissances.md](sept-puissances.md) (le référentiel : verbes, polarités, 5 états) côté **représentation visuelle** et **modèle d'interaction**. Décisions prises avec Boris les 14-15/07/2026. Prototypes : `zegame-prototypes/point-zero-home/moteur.html` et `puissance-desir.html` (servis en local, non intégrés au Rails à ce stade).

## 1. Principe : un lemniscate vivant

Le Moteur ontologique s'affiche sur la page **Profil** sous forme d'un **lemniscate (∞) violet vivant**, posé sur un fond **Ombre → Lumière** (dégradé horizontal), avec :
- aux extrémités, les repères **Ombre** (cercle noir/point blanc) et **Lumière** (cercle clair/point noir) ;
- au croisement central, le **yin-yang** (Source / Point Zéro) ;
- en fond, un **arc pâle gris** = l'**horizon d'harmonisation** (le lemniscate maximal, le potentiel).

### Option B retenue : lobes indépendants
Chaque lobe du lemniscate violet grandit **indépendamment** : lobe **gauche = niveau Ombre**, lobe **droit = niveau Lumière**. Les lobes gardent le galbe de l'horizon (nesting « je grandis vers le Point Zéro »). Plus expressif que 5 tailles figées : chaque joueur a une signature unique. Un **point d'or** circule sur la boucle (énergie de progression).

## 2. La grammaire des 4 couleurs (état vs progression)

Distinction structurante (Boris, 14/07) : l'**état** et la **progression** sont deux dimensions différentes.

| Couleur | Sens | Source de données |
|---|---|---|
| **Gris** (arc de fond) | Horizon d'harmonisation, le potentiel | fixe |
| **Violet plein** | L'**état** actuel (les 2 lobes) | **évaluation 360°** (questionnaire initial + autres joueurs, facilitateurs, IA, Graines de Récit, résonances) |
| **Pointillé violet** | L'**objectif** (cap du plan de route) | choix du joueur, accompagné |
| **Or** | La **progression** vers le cap | **Oméga** gagnés dans les expériences taguées sur cette puissance-polarité |

Boucle saine : `état → cap → expériences (Ω) → réévaluation → nouvel état`. Les Oméga **préparent** le mouvement ; seule une **réévaluation 360°** fait bouger le violet. Les Oméga ne pilotent donc **jamais** directement la taille des lobes.

Les deux stratégies d'évolution du référentiel sont couvertes par le cap : viser **plus loin dans la même polarité**, ou viser la **polarité opposée** (ex. Imagination très Lumière → cap vers l'Ombre pour refonder le rapport à l'Imagination).

## 3. Moteur global vs 6 puissances

- **Moteur global** = résultante des puissances. La **Transcendance n'est pas affichée** comme puissance : elle **est** ce moteur global (résultante), sans être nommée ainsi (trop abstrait d'emblée).
- **6 puissances affichées** (Désir, Volonté, Imagination, Émotion, Communication, Intuition) : chacune sur une ligne = **mini-lemniscate** (même grammaire), avec ses icônes de polarité aux extrémités, l'état violet, le cap pointillé éventuel, et une **jauge or** « X / Y Ω » quand un cap est défini (sinon « Définir un cap → »). Chaque ligne est cliquable vers la fiche puissance.

## 4. États d'affichage

- **Avant questionnaire (première connexion)** : lemniscate violet réduit à une **graine** visible autour du yin-yang (intrigue le joueur) ; à la place du degré, message *« Pour une première évaluation de ton Moteur Ombre / Lumière, réponds au questionnaire : »* + bouton. Les 6 puissances sont en « à évaluer ».
- **Après questionnaire** : lobes ouverts selon l'évaluation ; les 5 degrés (Blocage · Tiédeur · Alignement · Alchimisation · Hyperconscience) s'affichent.

Une **expérience dédiée au questionnaire** sera ajoutée dans le parcours du **Monde 0** ; si le joueur y a répondu librement depuis le Profil, il ne le refait pas.

## 5. Fiche détail d'une puissance

D'après la maquette de Boris et `Evaluation-Puissances.pptx`. Structure (voir `puissance-desir.html`) :
1. **Les 3 verbes** : Ombre / Source / Lumière, chacun avec icône, verbe (ex. Désir « Je contiens » / « Je suis » / « J'embrase »), illustration ronde et description.
2. **État actuel** : label (ex. *Lumière exacerbée*), 5 points, mini-moteur, états par pôle (ex. Blocage / Exaltation) avec croyances, et **archétype actuel** (ex. *l'Ivrogne de Vie*).
3. **Cap d'évolution** : label visé (ex. *Lumière intégrée*), mini-moteur avec cap pointillé + progression or, croyances cibles, et **archétype visé** (ex. *le Vivant Fécond*).

La fiche puissance est le lieu où l'on **définit un cap**.

### Source du questionnaire
`Evaluation-Puissances.pptx` fournit, par puissance, une **croyance-clé Ombre** et une **croyance-clé Lumière**, chacune avec une *intensité de croyance* → alimente directement les deux lobes. Les croyances du PPTX sont formulées pour un collectif (EVH) ; la maquette Désir donne la version personnelle. À écrire : versions personnelles des 5 autres puissances + états par pôle et archétypes (actuel/visé) — itération en cours côté Codex.

## 6. Implications modèle de données (à venir)

Rien n'est encore implémenté en Rails. Prévoir :
- `moteur_evaluations` : sujet, puissance (ou global), niveaux Ombre/Lumière, **source** (questionnaire, joueur, facilitateur, IA, graine, résonance), date. Le violet lit la **dernière** évaluation consolidée.
- objectifs de route (`caps`) : puissance + direction visée + date.
- Les Oméga par puissance-polarité existent déjà via `skills.derived_framework` (« {Puissance} - {Ombre|Source|Lumière} ») → alimentent la jauge or.

## 7. Assets

`Ressources Point Zero/Appli/img/7 puissances/` : icônes (symbole + couleur par puissance — Désir ∞ rouge, Volonté △ orange, Imagination ◇ jaune, Émotion vert, Communication bleu, Intuition ◎ indigo ; variantes neutre / -O / -L) et illustrations rondes (neutre / _O / _L). Images d'archétypes non encore fournies (fallback dans le proto). Repères Ombre/Lumière/Source dans `Ressources Point Zero/Appli/img/`.
