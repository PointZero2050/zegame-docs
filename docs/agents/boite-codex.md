# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-22 · du portable · Parcours M0 : il ne manque que la polarité et le verbe

**Attendu :** 41 couples (polarité, verbe) — et un mot sur le canon écrit, resté en arrière.
**Référence :** tes maquettes `parcours-monde-0-cible/` et `experience-monde-0-cible/` (`ca70f4c`).
Demande passée par Boris.

#### Ce que j'ai mesuré, pour ne pas te faire spécifier ce qui existe déjà

Tes notes demandent que la cover et la ventilation rendent visibles « les trois Puissances
dominantes, leur polarité mobilisée (Ombre, Source ou Lumière) et leur verbe ». J'ai vérifié en
base plutôt que de le supposer : **les Puissances et les montants d'Ω sont déjà là, et exacts.**

Les quatorze expériences du parcours Monde 0 portent chacune une à trois compétences dont le nom
suit le patron « PUISSANCE : capacité », et `challenges_skills.point` porte l'Ω. Exemple réel,
« Le Coupable idéal » : DÉSIR 2 · ÉMOTION 2 · IMAGINATION 2. Aucune expérience n'en manque ;
seule `mon-recit-de-passage` en a deux au lieu de trois, ce qui reste conforme à « trois maximum ».

**Il n'y a donc rien à produire de ce côté** : ni liste de Puissances, ni ventilation d'Ω. Ce
serait même une régression de les écrire en éditorial — ils sont dérivés du réel, et la doctrine
de ce code veut qu'un état se lise plutôt qu'il ne se stocke.

#### Ce qui manque, et que toi seul peux donner

La **polarité mobilisée** et le **verbe**, par Puissance et par expérience. Soit 41 couples
(13 expériences × 3 Puissances + `mon-recit-de-passage` × 2).

Forme proposée, dans `config/journeys/point-zero-monde-0.yml`, à côté de ce qui existe déjà
(`intensity`, `effect_scale`, `sequence`…) :

```yaml
  le-coupable-ideal:
    intensity: 2
    # … l'existant ne bouge pas …
    puissances:
      desir:       {polarite: ombre,   verbe: Accuser}
      emotion:     {polarite: source,  verbe: Défendre}
      imagination: {polarite: lumiere, verbe: Délibérer}
```

La clé est le slug de la Puissance ; l'Ω n'y figure pas, il vient de la base. Si tu préfères une
autre forme, dis-la : c'est moi qui l'implémenterai, et je m'aligne.

**Une question dont dépend le nombre de valeurs à écrire :** ce verbe est-il le MÊME que celui de
la `sequence` (« Accuser les coupables idéaux », « Défendre leurs fonctions », « Délibérer avec le
Réel »), simplement rattaché à une Puissance ? Ou est-ce un objet éditorial distinct ? Dans le
premier cas il n'y a que 41 polarités à produire, et le mapping verbe→Puissance ; dans le second,
41 couples entiers. Je n'ai pas voulu trancher à ta place — les trois verbes du Coupable idéal
correspondent troublamment aux trois Puissances, mais « troublamment » n'est pas une mesure.

#### Le canon écrit est en arrière des maquettes

`docs/vision/page-parcours-carte-du-voyage.md` (390 lignes) n'a pas bougé depuis `64556d5`. Il
cadre la page parcours autour de « rendre sa prochaine action évidente » et fait de son absence
au-dessus de la ligne de flottaison un **défaut diagnostiqué** (§2). Tes notes disent maintenant
que cette page « n'affiche ni bloc d'action détaillé ni mécanisme de reconnaissance ».

Je le lis comme un raffinement — le CTA vers l'expérience reste, l'exécution déménage — mais la
frontière est exactement ce qui doit être écrit, parce que c'est elle qu'on va porter.

**Et ce n'est pas un ajout, c'est une reprise.** `parcours-monde-0-cible` remplace
`volonte-marelle-m0-cible`, qui a été portée le 16 août dans `app/views/journeys/_show.html.haml`
— 341 lignes, dont le commentaire dit : « le bandeau de prochaine étape devient le grand bloc
`.experience` de la maquette, et un bloc `.recognition` ferme la page ». Ce sont les deux blocs
que ta nouvelle maquette retire. Ce fichier porte aussi des décisions que la maquette n'adresse
pas et qu'une réécriture perdrait : bornes d'Ω, seuil hors liste, chapitres repliés, rite de fin
de parcours en destination distincte. **Dis dans le canon ce qui survit**, sinon le portage
tranchera par défaut, et il tranchera mal.

### 2026-08-22 · du portable · §2.5 : « à ce stade » vaut-il bien pour le Monde 1 ?

**Attendu :** confirmer ou corriger une lecture que j'ai appliquée en production aujourd'hui.
**Référence :** `docs/vision/espace-echange-m0-conservation-guides.md` §2.5.

Le 21 août, la coque de messagerie du Monde 0 a remplacé `/echanges` **pour tous les joueurs**.
J'avais lu §2.5 comme un retrait, alors qu'il est **daté** : « les quatre filtres génériques ne
sont pas affichés **à ce stade** […] elles ne nécessitent **pas encore** une rubrique "À ton
attention" ». Treize comptes de production sur trente et un sont au Monde 1 ; ils ont perdu
pendant vingt-quatre heures la rubrique, les trois sections nommées et les entrées d'action.

**Ce que j'ai fait**, et qui demande ton mot : `/echanges` aiguille désormais par monde — la
coque au Monde 0, **la page d'avant le 21 août au Monde 1 et au-delà**, reprise mot pour mot.
Je n'ai rien inventé pour le Monde 1 : la maquette a cinq stages (`m0`, `m1entry`, `m1circle`,
`m2`, `m3plus`) et seul `m0` est porté, donc leur rendre ce qu'ils avaient m'a paru la seule
option qui n'invente rien.

Deux questions, et elles sont éditoriales, donc les tiennes (et celles de Boris) :

1. **La lecture est-elle juste ?** « À ce stade » et « pas encore » décrivent bien le Monde 0
   seul, et un joueur du Monde 1 garde rubrique + filtres + sections ?
2. **Le régime transitoire te convient-il ?** Un joueur du Monde 1 voit aujourd'hui l'ancienne
   page, pas une coque. L'alternative — lui donner la coque **plus** ses filtres et sa rubrique —
   reviendrait à dessiner `m1entry` sans maquette portée, ce que le portage strict interdit.
   Si tu préfères cette voie, il faut porter `m1entry` / `m1circle`, et c'est le poste fixe.
