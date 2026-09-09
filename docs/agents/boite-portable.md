## 10 septembre (9) — #175 : M0-22, débloqué par ta fusion de #170

https://github.com/PointZero2050/pointzero-app/pull/175 — indépendante de #173, sur `preprod`.

`_passage.html.haml` et `experience.css` étaient tenus par #170 ; ta fusion les a libérés, et
c'était le seul écart du lot 4 qui me restait.

L'index de séquence ne répète plus le panneau. Trois nuances par rapport à la référence, chacune
répondant à une phrase du remède : l'index ne montre que les étapes **déjà atteintes**, il ne se
rend qu'à partir de deux entrées, et il ne disparaît pas tout à fait — la référence rejoue par
une URL `?replay=1`, nous par ces onglets, et les supprimer aurait retiré le seul chemin de
relecture.

### ⚠️ Ce que le balayage complet a attrapé — et je l'ai fait sans `head` cette fois

- **`gestes.js` réécrivait `.step-counter` à chaque clic.** Le compteur était unique, donc il
  fallait le tenir à jour ; il vit maintenant dans chaque panneau. Le code part plutôt que de
  rester : `querySelector` rendrait `null` et la garde `if` **avalerait le fait que le contrat a
  changé**.
- **`var total` n'était compté que pour cette ligne.** J'avais écrit qu'il « restait employé plus
  haut » — c'était faux, vu en le vérifiant.
- **Quatre assertions** dans `verifier_marelle` et `verifier_chaine_m0`.

C'est la deuxième fois que `verifier_marelle` garde un contrat que je viens de changer. La
première, j'avais conclu d'une sortie coupée qu'il n'y avait rien. Cette fois je l'ai vu.

### ⓘ Et une assertion qui se dédouble au lieu de se desserrer

Le surtitre perd son « ÉTAPE n SUR m » ; le repère compact le reprend. Raccourcir l'attendu sans
vérifier ailleurs, ce serait cesser de garder le compte — et c'est au moment où une information
change de place qu'elle se perd. Le banc garde les deux, plus le fait que l'ancien compteur ne
revienne pas.

### État

    #173  dévoilement + transition   prête
    #175  M0-22                      prête

⚠️ **Sur #173, la question tient toujours** : le cas « chapitre fermé » est-il atteignable avec
un compte ordinaire ? Si tu vois comment le provoquer côté données, la branche cesserait d'être
du code non exercé.

Il ne me reste rien de débloqué sur le lot 4 : M0-23 et M0-25 sont chez Codex (il annonce sa
passe éditoriale, je ne touche pas au YAML), M0-24 attend le contrat d'autorité, M0-28 attend
tes quatre éléments.
# Boîte du portable

⚠️ **Vidée le 10 septembre 2026.** Tout ce qui précédait est traité : #168 à #172 fusionnées et
promues, M0-00 / M0-01 / M0-02 / M0-06 / M0-07 / M0-10 / M0-11 / M0-12 / M0-17 / M0-19 / M0-20 /
M0-21 / M0-26 / M0-27 livrés, la traversée réelle d'Immateria jouée, l'hypothèse du bind mount
écartée, et les deux arbitrages de Codex reçus. Ce qui devait survivre a été écrit là où ça
survit : dans les commentaires du code et des bancs, dans les commits, et dans
`zegame-docs`. L'historique reste dans git.

Ne subsiste ici que ce qui est **encore ouvert**.

- **M0-13/14** : je suis derrière ton inventaire, comme Codex le demande. Mes cinq populations
  manquantes et ma proposition sur les durées inconnues sont dans le message précédent.
- **Ma boîte est vide** : tout est traité.
## 10 septembre (4) — M0-01 : l'appel que tu attends est en production depuis `8aa96b2`

Tu écris « mesuré moi-même, comme Codex : **zéro occurrence** de `fin-tutoriel` ou de
`tutoriel_termine` dans tout `public/` ». Ce n'est plus vrai, et la chronologie l'explique :

    195b77a  03:40  la révision AUDITÉE — le constat de Codex était juste
    8aa96b2  12:12  [Claude] M0-01 côté module : la sortie signale la fin du tutoriel

**Huit heures et demie séparent les deux.** Sur `origin/main` aujourd'hui : quatre occurrences
dans `GameScene.js`. Le constat de Codex était exact quand il l'a fait ; il a été repris tel quel
sans être remesuré.

### Ce qui est en production, et qui répond à ton contrat

`async signalerFinDuTutoriel()` (ligne 1063) fait exactement ton extrait — même en-tête CSRF,
même `console.warn` sur `!res.ok`, même `catch` qui laisse sortir le joueur hors ligne, avec la
raison écrite : l'appel est idempotent, le renvoyer ne coûte rien.

### ⚠️ Et ton point sur l'`async` : vérifié, il est couvert deux fois

Tu écrivais « `gotoMonde0` devient `async` ; son appelant fait `this.gotoMonde0();` **sans**
`await` — c'est à vérifier chez toi ». Fait :

1. **Un seul appelant**, ligne 962, et il fait `await this.gotoMonde0();` — avec le commentaire
   qui dit pourquoi.
2. Et même sans lui, la séquence tiendrait : le `await this.signalerFinDuTutoriel()` est **à
   l'intérieur** de `gotoMonde0`, ligne 1079, **avant** `window.location.href`. La navigation
   attend la preuve quoi que fasse l'appelant.

C'était la bonne question — c'est le détail qui décide si la preuve part vraiment.

### ⚠️ Une hypothèse à écarter, parce qu'elle serait grave

Si tu as mesuré **sur le serveur** et non sur le dépôt, et que tu trouves encore zéro, alors ce
n'est pas une mesure périmée : ce serait le **bind mount `/home/deploy/pz` qui masque
`/rails/public/pz`** — et donc tout `public/pz/` que je livre n'atteindrait jamais les joueurs.
Les fichiers compose vivent chez toi, je ne peux pas le vérifier.

`.gitignore` exclut `puissances`, `ressources`, `epoque`, `coupable-ideal`, `fonts` et `moteur` —
**pas `immateria`**, qui est bien versionné. Si le montage couvre tout `pz/` plutôt que ces
six-là, la moitié de mon travail d'intégration est invisible en production sans que rien ne le
dise. Un `docker exec … grep -c fin-tutoriel /rails/public/pz/immateria/js/scenes/GameScene.js`
tranche en une commande.

ⓘ Si le compte y est, M0-01 est entier : ta moitié serveur + cette moitié module. Il reste à le
jouer de bout en bout — Codex demande une traversée réelle, pas un appel de route.
## 10 septembre (3) — contrat M0-13/14 de Codex : ce qu'il me faut de toi, et ma proposition

Codex a rendu le [contrat d'affichage](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-comptages-durees-contrat.md).
Il te met devant : inventaire E1–E19 + épilogue, sélections explicites, analyse d'impact. Je
porte les libellés **après**. Et il écrit « implémenter des populations explicites, pas des
constantes dispersées ni une soustraction aveugle de 1 » — donc je ne dérive rien dans la vue.

⚠️ **Je ne touche pas `journeys/_show` ni `_fiche_joueur` tant que #169 est ouverte** : Codex
demande de ne pas rouvrir ces zones en parallèle, et ce sont exactement les fichiers du contrat.

### Les cinq choses que `JourneyProgress::Etat` n'expose pas et que le contrat exige
