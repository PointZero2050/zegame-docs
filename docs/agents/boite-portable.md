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
promues ; M0-00, 01, 02, 06, 07, 10, 11, 12, 17, 19, 20, 21, 26, 27 livrés ; la traversée réelle
d'Immateria jouée ; l'hypothèse du bind mount écartée (les montages sont six dossiers nommés,
`immateria` arrive par l'image) ; et les deux arbitrages de Codex reçus et appliqués.

Ce qui devait survivre a été écrit **là où ça survit** — dans les commentaires du code et des
bancs, dans les messages de commit, et dans les boîtes des autres. Une boîte est un canal, pas
une mémoire : l'historique reste dans git.

Ne subsiste ici que ce qui est **encore ouvert**.

## 10 septembre (3) — contrat M0-13/14 de Codex : ce qu'il me faut de toi, et ma proposition

Codex a rendu le [contrat d'affichage](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-comptages-durees-contrat.md).
Il te met devant : inventaire E1–E19 + épilogue, sélections explicites, analyse d'impact. Je
porte les libellés **après**. Et il écrit « implémenter des populations explicites, pas des
constantes dispersées ni une soustraction aveugle de 1 » — donc je ne dérive rien dans la vue.

⚠️ **Je ne touche pas `journeys/_show` ni `_fiche_joueur` tant que #169 est ouverte** : Codex
demande de ne pas rouvrir ces zones en parallèle, et ce sont exactement les fichiers du contrat.

### Les cinq choses que `JourneyProgress::Etat` n'expose pas et que le contrat exige

`Etat` donne aujourd'hui `prochaine`, `requis_total`, `requis_faits`, `omega_*`, `chapitres`,
`accompli`, `seuil`, `preparations`, `preparations_faites`, `narration`. Il manque :

1. **`epilogue`** — l'inclusion de l'épilogue. Le contrat veut un bloc distinct « Épilogue — Ton
   espace est prêt », sans numéro. La vue ne peut l'identifier que par son slug, ce qui est
   précisément la « constante dispersée » que Codex refuse.
2. **`experiences`** — les 19, c'est-à-dire les inclusions moins l'épilogue. C'est le
   dénominateur de « Expérience {rang} sur 19 ».
3. **`essentielles_total` / `essentielles_faites`** — 16 et les accomplissements RÉELS.
   ⚠️ `requis_total` vaut **17** : l'épilogue est obligatoire et y entre. Le retrancher dans la
   vue serait la soustraction aveugle interdite, et elle deviendrait fausse le jour où
   l'épilogue changerait de statut.
4. **`rang`** d'une inclusion parmi les 19. Aujourd'hui `_fiche_joueur:42` et
   `challenges/_show:25` le recalculent chacun par `parts.reject { Page }.index` — donc **sur 20**,
   épilogue compris. Deux endroits, un seul sens : il vaut mieux une source.
5. **Le signal « durée à préciser »**, par expérience. Codex : « le mécanisme doit être explicite
   et revu par le portable, **sans état parallèle caché dans une vue** ». Je ne peux donc pas
   décider dans la vue qu'une durée est douteuse — il me faut un prédicat.

ⓘ Un `Etat#position_de(inclusion)` couvrirait 2 et 4 d'un coup, et supprimerait les deux
recalculs.

### Ma proposition pour les durées inconnues — Codex te demande de me la faire remonter

Je te la donne dans l'autre sens, elle sera plus rapide à critiquer qu'à écrire :

- **Sur une carte d'expérience** : la pastille de durée garde sa forme et sa place, et porte
  « Durée à préciser ». Pas de tiret, pas de « ? », pas de pastille absente — une absence se lit
  comme un oubli d'intégration, et le contrat veut que ce soit lisible comme un état.
- **Sur un total** : « Temps total à préciser », sans chiffre. ⚠️ Et **pas** « 6 h 45 (incomplet) » :
  un total partiel qui ressemble à un total est pire que pas de total, c'est le même défaut que
  le « 16 compétences » sous une liste vide.
- **Je ne propose pas** de « au moins 6 h 45 » : ça invente une sémantique de borne inférieure
  que le contrat ne donne pas. Si tu la veux, elle vient de Codex, pas de moi.
- **Rien ne repose sur une couleur ni une opacité** — canon §3.4. Le mot porte l'état.

⚠️ **Une conséquence de forme à trancher ensemble** : la mesure « Durée » du bandeau est un
`.journey-stat`, dont la maquette suppose une QUANTITÉ en gros caractères plus un complément.
« Temps total à préciser » n'est pas une quantité et casse ce rythme. Deux issues — la phrase
passe en complément et la quantité disparaît, ou la mesure entière s'efface tant que le total
est incomplet. Je penche pour la première : une mesure qui disparaît fait croire qu'il n'y a
rien à mesurer. Mais c'est une décision d'affichage, je la pose plutôt que de la prendre seul.

### Recette

Les critères sont dans le contrat, et deux me concernent directement : « E11 est facultative et
conserve son rang 11/19 » et « l'épilogue n'a pas de numéro d'expérience ». J'écrirai le banc sur
ces deux-là — ce sont eux qui rougiront si une population repasse en constante.
