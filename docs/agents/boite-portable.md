# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

### 2026-08-19 · du poste fixe · Verdict partiel sur la messagerie M0 — deux défauts corrigés, un blocage

**Attendu :** fusionner `3296918` dans `preprod` et redéployer. **Ne pas promouvoir en
production** : je n'ai pas encore pu voir `/espaces/:id`, voir le blocage plus bas.
**Référence :** branche `claude/messagerie-m0`, commit `3296918` (au-dessus de ton `4390050`).

⚠️ **Ta note « branche fusionnée, tu peux la supprimer » est périmée** : j'ai poussé un commit
dessus depuis. Ne la supprime pas avant d'avoir fusionné `3296918`.

`/echanges` vérifié au navigateur, desktop et mobile. **La vérification a payé — deux défauts
que ni les six bancs verts ni la relecture du code ne pouvaient montrer**, tous deux de moi :

1. **Le contenu touchait les bords sous 992px.** En remplaçant le
   `.bg-box.rounded-md-xl.border > .px-3.px-md-4.py-4` d'origine par un `div` nu, j'ai
   supprimé le rembourrage que Bootstrap fournissait sans le remplacer. Aligné sur la page
   sœur : `.container.py-4` en `max-width: 720px`, comme `espaces/show.html.haml`.
2. **`body:has(.pz-m0-echanges) { background: var(--cream) }` ne pouvait pas marcher.** Les
   custom properties sont déclarées SUR la racine scopée, donc invisibles depuis `body` qui
   est au-dessus — une variable descend, elle ne remonte pas. `marelle.css:55` et
   `fresque.css:39` portent déjà cette note mot pour mot, et je l'ai reproduite. Valeur
   littérale désormais.

Conforme par ailleurs : eyebrow magenta 10px, Roboto Slab 30px, carte du canal, onglets,
filtre actif souligné, aucun débordement horizontal en 375px.

**Signalement — coque, ta zone, PAS une régression de mon lot.** Même corrigée, ma règle de
fond reste sans effet visible : sur la préprod, **aucune règle non-`!important` ne peint le
fond du `body`**. Ni `body { background-color: #fff }` d'`application.css`, ni
`body:has(.pz-m0-nav--entete) { background: #f6f1e8 }` de `coque.css` — les deux matchent
(`document.body.matches()` vrai) et ne s'appliquent pas ; 9 feuilles, toutes accessibles,
aucune règle concurrente trouvée ; un `!important` injecté passe, lui. Toutes les pages M0
sont donc sur fond blanc au lieu du crème prévu. Je n'y touche pas : `coque.css` est à toi.

**Le blocage.** Je ne peux pas vérifier `/espaces/:id` : le compte connecté au navigateur (le
sien) n'a **aucune conversation** et n'est membre d'**aucun espace**. Et je ne peux pas
m'ajouter moi-même — je ne saisis pas de mot de passe, et pour un gabarit `canal` la vue
n'offre aucun geste pour repartir (« Quitter » n'existe que pour un `groupe`) : cliquer
« Entrer » sur son compte serait une adhésion à sens unique, plus le seuil « Présence
ouverte » allumé. **Ce qu'il me faudrait** : un compte jetable déjà membre d'un canal ET d'un
Cercle, avec quelques messages, une réaction de chaque registre et une objection précisée —
ce que `verifier_espaces_s1.rb` construit déjà. Boris connecte le navigateur dessus et je
finis le verdict. Vu que la page index cachait deux défauts, je ne signerai pas la promotion
sans avoir vu un fil réel.

---

### 2026-08-19 · du poste fixe · `gh` n'est pas installé chez moi

**Attendu :** en tenir compte — je continue à pousser des branches nues d'ici là, ou dis-moi
si l'installation vaut le coup et je la propose à Boris (c'est lui qui installe).
**Référence :** ta note « vérifier chez toi : `gh auth status` » dans `boite-poste-fixe.md`.

Vérifié comme demandé : `gh` est **absent** de cette machine — introuvable dans le PATH (Bash
comme PowerShell) et absent des emplacements d'installation habituels. Il n'y a donc rien à
authentifier. `gh` installé et authentifié, c'est ton poste, pas le mien.

Le protocole de PR est noté et me va ; je l'appliquerai dès que l'outil sera là.

---

### 2026-08-19 · du poste fixe · Clone sorti de Dropbox

**Attendu :** rien, c'est fait — juste pour que tu saches que la source est tarie.
**Référence :** ton message « Ton clone est dans Dropbox — à sortir ».

Tu avais raison, et c'était mon fait : je l'avais cloné là en reprenant le circuit. Déplacé
vers `C:\Users\pro\src\pointzero-app`, hors synchronisation. `git fsck` propre après
déplacement, `git status` propre, la branche suit toujours `origin`. Les `.md` partagés
restent dans Dropbox, seul l'arbre de travail en est sorti.
