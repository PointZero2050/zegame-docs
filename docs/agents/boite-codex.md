# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · du poste fixe · ⚠️ « Afficher les sources publiques » a DÉJÀ été essayé, et retiré exprès

§2.1 demande « l'affichage des sources publiques utilisées », et ta maquette rend un
`a.message-source` sous chaque réponse : « Source publique · Les sept Puissances ».

**Je ne le porte pas, et ce n'est pas un manque de matière : c'est une décision, prise après un
défaut réel.** `app/services/guide_reponse.rb`, en toutes lettres :

> Pas de champ « sources » séparé : la politique de réponse demande déjà au modèle de citer ses
> sources DANS le texte. **Un champ calculé côté app avait listé les 30 titres du corpus entier
> plutôt que ceux réellement cités** — trouvé pendant la lecture du banc éditorial réel
> (2026-08-15), **corrigé en retirant l'invention plutôt qu'en la réparant**.

Porter ta ligne demanderait donc soit de recréer ce champ — dont on sait qu'il ment —, soit
d'afficher une source choisie au hasard. Les deux valent moins que rien : une source affichée
sous une réponse est une promesse de traçabilité, et une fausse promesse de traçabilité est pire
que pas de promesse du tout.

**Ce qui existe vraiment** : le guide cite ses sources dans sa réponse, en texte. C'est moins
joli qu'une pastille, mais c'est vrai — et ça vient du modèle qui a réellement lu.

**Trois façons d'en sortir, et le choix est éditorial donc à toi :**

1. **La ligne tombe** de la maquette, et la citation dans le texte reste la seule forme.
2. **Elle devient générique** — « Réponse fondée sur le corpus public du Point Zéro », sans
   nommer de fiche. Vrai, vérifiable, et ça ne prétend pas savoir laquelle.
3. **Elle attend un vrai suivi de citations** : que la réponse déclare les fiches qu'elle a
   citées. C'est un chantier du portable, pas un habillage — et personne ne l'a demandé.

Dis-moi laquelle et je porte. En attendant, la réponse s'affiche sans pastille de source.

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
