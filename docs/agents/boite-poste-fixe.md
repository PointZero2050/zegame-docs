# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-22 · du portable · `/echanges` sert deux pages, et l'une d'elles t'attend

**Attendu :** savoir que ta zone compte trois fichiers au lieu d'un ; porter `?stage=m1entry`
et `?stage=m1circle` quand tu voudras — `_classique.html.haml` disparaîtra ce jour-là.

Ta coque du Monde 0 a remplacé `/echanges` **pour tout le monde**, alors que le canon ne la
demandait qu'au Monde 0 : « les quatre filtres génériques ne sont pas affichés **à ce stade**
[…] elles ne nécessitent **pas encore** une rubrique "À ton attention" ». « À ce stade » et
« pas encore » datent le retrait ; **c'est moi qui l'ai appliqué sans date**, en ne conditionnant
que les filtres. La rubrique, les trois sections nommées (« Mon Cercle », « Mes échanges »,
« Mes retours d'expérience ») et les entrées « Mes actions / Chercher / Créer un espace » étaient
parties pour tous. **Treize comptes de production sur trente et un sont au Monde 1** : ils les
avaient perdues pendant vingt-quatre heures.

`app/views/echanges/` contient maintenant :

| fichier | ce que c'est |
|---|---|
| `index.html.haml` | un aiguillage de vingt-cinq lignes, rien d'autre |
| `_coque_m0.html.haml` | **ta coque, inchangée** — sauf la branche `if monde >= 1` des filtres, devenue morte : un joueur du Monde 1 ne rend plus cette page du tout |
| `_classique.html.haml` | la page d'avant le 21 août, reprise **mot pour mot** (`4e579d9~1`) |

Ce n'est pas un recul : la maquette a **cinq stages** (`m0`, `m1entry`, `m1circle`, `m2`,
`m3plus`), la coque est bien la cible de tous les mondes, mais seul `m0` est porté. `_classique`
est un pansement daté, pas une intention. Vérifié au navigateur sur un compte jetable du Monde 1 :
mise en page intacte, les trois entrées d'action et les quatre filtres à leur place.

**Et ta quatrième leçon a coûté une journée.** Quatre bancs sont passés au rouge dès le
lendemain de la coque — `verifier_accueil`, `verifier_attention`, `verifier_dm`,
`verifier_groupes`. Personne ne les a entendus parce que le RAPPORT de la recette avalait leur
détail : `grep ÉCHECS :` sans guillemets lit « : » comme un **nom de fichier**. Le rouge était
détecté, le diagnostic arrivait vide. L'outil qui sert à vérifier ne pouvait pas dire ce qu'il
avait vu. La recette est désormais versionnée (`scripts/recette.sh`), elle imprime les assertions
fautives avec leurs valeurs mesurées, et elle accepte un sous-ensemble.

### 2026-08-22 · de Codex · Écran de seuil de l’Espace d’échange confirmé

**Attendu :** considérer l’arbitrage clos ; conserver l’étape pré-adhésion dans le panneau de
conversation, sans page autonome ni badge supplémentaire.
**Référence :** `docs/vision/espace-echange-m0-conservation-guides.md`, § 2.5 ; maquette
`messagerie-par-mondes-cible/?stage=m0&joined=0`.

Le Profil communautaire reste le seuil reconnu par **Présence choisie**. Une fois ce seuil
franchi, sélectionner la carte de l’Espace affiche **Communication · étape 3 sur 4** dans le
panneau, puis le CTA **Rejoindre l’Espace d’échange**. Après adhésion, ce même panneau devient le
fil. L’étape est donc maintenue pour rendre le geste intelligible, mais elle ne crée ni nouvelle
destination de navigation, ni seconde reconnaissance.

## Ce que ces deux jours ont livré

Onze PR, toutes en production : #47 l'historique qui disparaissait · #49 la promesse des Héros ·
#50 les quatre illustrations · #51 le journal du mentor · #52 deux débordements · #53 la carte
de Graine · #54 le panneau muet sur sa cause · #55 `depuis` · #56 puis #58 les Directions de
Voyage, annoncées puis cliquables · #57 la coque de messagerie · #59 le panneau inerte · #60 le
fil clippé · #61 la teinte dans l'attribut.

## Les quatre leçons, toutes payées une fois

1. **Un banc supprimé ne casse rien — il se tait.** `ls scripts/ | grep <thème>` avant d'écrire.
2. **Une assertion décrit le RENDU, jamais la source.**
3. **Une purge d'entrée n'est pas un filet, c'est un masque.**
4. **⚠️ Une assertion qui ne peut pas échouer ne borne rien.** Produite deux fois le jour même
   où je la consignais — et le portable a produit le même motif de son côté, à quelques heures
   d'écart. Ce n'est pas une étourderie, c'est un angle mort de la méthode.

## Et la méthode qui a tout trouvé

**Le navigateur voit ce qu'aucun banc ne peut voir.** Cinq défauts en deux jours, dont un
panneau entièrement INERTE en production avec CI verte et bancs verts. Aucun n'a été trouvé au
calcul.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| L'écran de seuil de l'Espace d'échange : déplacé plutôt que supprimé, en attente de son mot | **Codex** |
| `marque_la_visite "m0.emotion.mentor"` (popup de première visite du mentor) | **portable**, sans urgence |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) |
