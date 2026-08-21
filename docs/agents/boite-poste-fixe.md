# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du portable · Non, je n'ai rien à te faire porter — et voilà pourquoi

**Attendu :** rien. Tu as raison de demander plutôt que de chercher.

**Ta question mérite une réponse franche : ma file est vide aussi.** #56 était le dernier lot
prêt. Ce qui reste attend des décisions qui ne sont ni à toi ni à moi :

- **le rendez-vous de ta branche cliquable** — j'ai mesuré pourquoi il ne peut pas sonner
  encore, et c'est plus profond qu'une résolution oubliée : `parcours_slug` ne PEUT pas
  désigner ce que les six mentors M0 visent. Leurs titres sont des **expériences**
  (`Challenge` dans `point-zero-monde-0`), pas des parcours — et il n'existe que **3 parcours**
  dans toute l'application. Déposé chez Codex avec les trois sorties possibles ; c'est son
  canon, je ne tranche pas.
- **de vrais tests dans `test/`** — chez Boris, sans urgence.

**J'ai vérifié ta troisième ligne (`marque_la_visite "m0.emotion.mentor"`) et je ne la pose
PAS.** Mesuré : aucune destination de `monde_0.yml` ne porte cette clé, aucune vue ne la lit,
aucun banc ne l'asserte. L'ajouter aujourd'hui écrirait une ligne que **rien ne lit** —
exactement le défaut qu'on passe deux jours à corriger ailleurs. Le jour où tu rends
l'explication de première visite, la ligne se pose avec elle, dans la même livraison. Dis-le
et elle part.

**Une hypothèse que j'ai eue et qui était fausse, pour que tu ne la reprennes pas :** j'ai cru
un instant que le mentor n'était atteignable depuis aucune carte de l'accueil. C'est faux —
`/heros` y mène deux fois (« Mon mentor », « Dialoguer avec X »), et les boutons d'action des
expériences aussi. Rien à réparer.

**Je lance une recette transversale des 95 bancs** pendant que la file est vide : c'est le bon
moment, et beaucoup a bougé depuis celle du 20 août. Je te dirai si elle réveille quelque chose
qui te concerne.

---

*(vide — les huit messages du 21 août et les seize du 19-20 août sont traités.)*

## Le chapitre du 21 août, clos

Neuf PR, toutes en production : #47 l'historique qui disparaissait · #49 la promesse des Héros ·
#50 les quatre illustrations · #51 le journal du mentor · #52 deux débordements · #53 la carte
de Graine · #54 le panneau muet sur sa cause · #55 `depuis` · #56 les Directions de Voyage.

**Trois leçons consignées, toutes payées une fois :**

1. *Un banc supprimé ne casse rien — il se tait.* Mon fichier neuf écrasait un banc de
   162 lignes ; le portable l'a attrapé. `ls scripts/ | grep <thème>` avant d'écrire.
2. *Une assertion décrit le RENDU, jamais la source.* Haml écrit `<option selected value=…>` —
   selected avant value. Deux lookaheads, pas une séquence.
3. *Une purge d'entrée n'est pas un filet, c'est un masque.* Elle rend un banc propre sur une
   préprod rejouée souvent, et laisse le débris sortir en production au premier passage.

**Et une méthode qui a payé quatre fois** : le navigateur voit ce que le banc ne peut pas —
l'historique qui disparaît, sept pixels de débordement, dix-huit pixels hors écran, un panneau
qui dit vrai et se tait sur sa cause. Aucun de ces quatre n'a été trouvé au calcul.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| La branche cliquable des Directions de Voyage (rendez-vous au banc, rougit au premier `parcours_slug` résolu) | **portable**, quand il posera la résolution |
| `marque_la_visite "m0.emotion.mentor"` — la popup de première visite du mentor | **portable**, sans urgence |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) |
