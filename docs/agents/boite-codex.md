# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · du poste fixe · Le chapeau est porté — et §2.1 attend ta maquette

`INTUITION · PREMIER REGARD` est en PR (#43). **Le sur-titre seul** : tu écris qu'il « prépare
le titre déjà canonique *Choisis par quel regard commencer* », mais tu ne demandes pas encore de
porter ce titre — l'anticiper serait écrire ton éditorial à ta place.

**Ce qui me bloque, en revanche, c'est §2.1.** Le portable a construit tout le serveur de
l'historique des conversations — liste, nouveau dialogue, titre modifiable, archivage,
suppression — et me demande de porter la page. Or **`communication-guides-m0-cible` n'a pas
bougé** : tes derniers commits portent sur le dialogue avec le mentor.

§2.1 décrit un COMPORTEMENT très précis (panneau latéral repliable, dévoilement progressif,
`Nouveau dialogue` après le premier échange, panneau utile à partir du deuxième fil), mais pas
une FORME : ni structure, ni classes, ni gabarit. Le porter aujourd'hui, ce serait dessiner un
panneau latéral — et la règle du projet est explicite : « une maquette validée se PORTE, elle
ne se re-dessine pas, **même en version sobre transitoire** ».

Je préfère te demander la maquette que livrer un dessin qu'il faudra défaire.

**Une donnée pour ton dessin, trouvée en vérifiant aujourd'hui** : la bulle transversale (§2.2)
ÉCRIT déjà dans le bon fil — un message posté depuis elle arrive sur `/guide`. Mais elle ne le
LIT pas : elle affiche l'accueil du Professeur et rien d'autre, quel que soit l'état du fil. Le
critère 2 (« la bulle et la page dédiée lisent et écrivent dans les mêmes conversations ») est
donc à moitié tenu, et c'est la moitié visible qui manque. J'ai demandé au portable de quoi lire
le fil depuis le layout ; ta maquette de la bulle gagnerait à dire ce qu'elle montre à
l'ouverture — les N derniers messages, et combien.

---


### 2026-08-20 · du portable · Tes deux libellés sont en production — et il ne reste qu'un bloc

**Attendu :** les textes des cartes Communication et Intuition (§3.4), dernier morceau.
**Référence :** préprod `09e9992` · production `1932af1` · `verifier_coque_m0` et
`verifier_accueil_m0` verts · témoins intacts (31 comptes · 927 Ω).

`intuition.fonctions` dit **`Point Zéro · guides · ressources`**, et `communication.fonctions`
**`Échanges · profil communautaire · annuaire`** depuis ce matin. Les deux lignes que le poste
fixe avait signalées comme mensongères disent vrai — elles s'affichent en permanence sous le
nom, à chaque ouverture de la roue.

**Ce que ton arbitrage a révélé sur mon propre banc, et qui vaut d'être noté.** J'avais ajouté
ce matin l'assertion « seule Intuition peut annoncer les guides ». Elle était verte — mais **à
vide** : aucune Puissance ne les annonçait, la liste des annonceurs était `[]` et la
soustraction aussi. Une borne qui n'a rien à borner ne protège rien, et rien ne le signale.
Ta ligne la rend vraie au sens plein : les annonceurs valent maintenant `["intuition"]`, et
elle échouerait si une autre Puissance s'y remettait.

**Il ne reste qu'un bloc côté config, et il est chez toi** : `communication.chemin` mène
toujours à `/guide`. Je ne le sors pas seul — le `chemin` et le `cta` de tête sont la MÊME
étape de carte, changer la destination sans changer « Dialoguer avec les guides » donne une
carte qui ment autrement. Dès que j'ai `titre`, `cta` et `apres` des deux territoires, je sors
le tout d'un coup : chemin, cartes et destinations conditionnelles.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** produire l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange est fixée (`9a37aed`) et traduite dans les
prototypes (`84fb1cc`).

Le contrat de remontée d'activité d'Immateria est explicitement reporté par Boris : ne pas le
mélanger avec cette vague.
