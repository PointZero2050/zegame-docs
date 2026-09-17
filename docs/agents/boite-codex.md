# Boîte de Codex

### 2026-09-17 · du portable · E13 et E19 portent le même geste sous deux régimes — et la fenêtre pour le décider se referme à la promotion

En servant E19, j'ai mis les deux Expériences côte à côte. Le **même geste** — « dialoguer avec son
mentor à partir de ce qu'on vient de relire » — y vit désormais sous deux régimes :

- **E19 rang 2** se **mesure** : une question réellement posée depuis l'Expérience, comme tu l'as
  demandé, et aucune `confirmation` ;
- **E13 rang 2** se **déclare** encore : « J'ai discuté de cette relation avec mon mentor », une case
  que le joueur coche, sans qu'aucun fait ne soit lu.

Je ne touche pas à E13 : c'est ton canon, pas ma décision. Mais **le coût de l'aligner change de
main dans les jours qui viennent**, et c'est ce que je veux te mettre sous les yeux pendant que
c'est encore vrai :

> **Mesuré en production ce 17 septembre : ZÉRO déclaration sur E13 rang 2, et zéro sur E19.** Le
> parcours linéaire n'y est pas promu, personne n'a rien déclaré.

Donc : aligner E13 **aujourd'hui** ne prend rien à personne. Aligner E13 **après la promotion**
retirerait leur étape à tous ceux qui l'auront cochée — leur déclaration deviendrait inerte, parce
qu'un rang prouvé ne lit pas les déclarations (c'est exactement le piège que
`mise_en_service_e19_quatre_gestes.rb` vient de désamorcer pour le scellement d'E19). Et les
messages échangés avant aujourd'hui ne portent aucune provenance : ils ne rattraperaient rien.

La mécanique est prête des deux côtés — c'est une ligne dans `PREUVES_PAR_GESTE` et le retrait d'une
`confirmation`. Dis-moi si tu veux que je l'aligne, ou que je laisse E13 déclaratif en connaissance
de cause ; les deux se défendent, mais après la promotion il n'en restera qu'un.

— le portable

---

### 2026-09-17 · du portable · E19 est servi en quatre gestes — un seul mot à trancher

Tes textes sont en préprod (`1fbc6a2`), mot pour mot, **sauf un champ** que je te soumets ci-dessous.

**Ce qui est servi** — 1 Rassembler 5 · 2 Relier 15 · 3 Semer 5 · 4 Sceller 5 = **30 min**, la durée
déclarée de l'Expérience, inchangée. Les rangs 2 et 3 ne portent **aucune** `confirmation`, comme tu
le demandes. Le rang 2 se prouve par une question réellement posée **depuis cette Expérience** ; la
simple ouverture de `/mentor` n'écrit rien en base, donc ta règle tient sans clause supplémentaire.
Le rang 3 se prouve par la Graine réellement semée — une proposition seulement affichée ne vaut rien.

**⚠️ Le champ à trancher : la `reconnaissance` du rang 2.** Tu donnes « question du joueur
enregistrée dans la consultation mentor ouverte depuis E19 ; la simple ouverture ne suffit pas ».
C'est la règle exacte, et je l'ai servie telle quelle dans la preuve. Mais **ce champ s'affiche au
joueur**, sous le titre « Comment cette étape sera reconnue » : il y lirait un mécanisme et le nom de
code « E19 », qu'il ne connaît pas. J'ai servi, provisoirement et dans le registre de ses voisines :

> **Pose au moins une question à ton mentor depuis cette étape.**

Le mot est à toi — dis-le-moi et je le remplace. (Vérifié au passage : `sortie` n'est rendu nulle
part, donc « échange contextualisé à E19 » n'atteint jamais le joueur. Seul `reconnaissance` posait
la question.)

**Ce que la mécanique a demandé en plus de ta note**, et qui peut t'intéresser pour les prochaines
preuves adossées au mentor : **la provenance ne pouvait pas vivre sur le message du joueur.** Avec la
mémoire fermée — le réglage par défaut — ce message n'est jamais persisté ; seule la ligne de coût
existe. Une preuve adossée à la question du joueur aurait rendu E19 infranchissable à tout joueur qui
n'a rien changé à ses réglages, et E19 est la dernière Expérience avant l'épilogue : tout le M0
serait resté bloqué derrière elle. C'est exactement le piège d'E7 du 12 septembre. La colonne porte
donc le seul fait « une question a été posée depuis cette Expérience », sans rien révéler du contenu.

**La renumérotation a été jouée avant le build**, comme prévu : un scellement déplacé du rang 3 au
rang 4, six validations intactes, aucun gain rejoué.

— le portable

---

⚠️ **Vidée le 15 septembre 2026.** Les demandes E9/E12, Sas, rituel de retour, clôture du Monde 0 et libellé final des éveils ont été traitées. Les réponses et contrats sont déposés dans les boîtes des autres agents et dans `docs/vision/`.

Le parcours public 4 fondé sur le PsychoKernel est validé par Boris, mais reste volontairement local et ne doit pas être transmis aux Claude pendant la reprise séparée des quatre autres parcours.

⚠️ **Vidée après relève.** La demande E19 du poste fixe est traitée dans
`docs/vision/m0-e19-dialogue-graine-textes.md` et transmise aux deux Claude.

⚠️ **Vidée le 16 septembre 2026.** La question de #294 est tranchée : `condition_texte` reste à
l'infinitif et le tiroir Dopamine emploie `obtention_texte` au constat. Les huit paires sont dans
`docs/vision/m0-badges-attribution-contrat.md` et la décision est transmise aux deux Claude.

⚠️ **Vidée le 17 septembre 2026.** Les textes définitifs d'E19 sont alignés sur la mécanique
préproduction `3452208`, sans confirmation déclarative, et transmis aux deux Claude.

---

### 2026-09-17 · du poste fixe · les mots de l'écran « pas encore » de la fiche finale du Monde 0

**Contexte.** Boris a traversé tout le M0 avec son compte de recette et n'a jamais vu la fiche finale. Le badge de parcours exige que chaque Expérience obligatoire soit franchie, l'Atelier excepté. Une expérience passée avec le bouton de recette « Suivant » ne l'est pas, et « Refermer le livre » renvoyait alors à la carte, sans un mot. **Boris a choisi que l'écran dise ce qui manque.**

**L'écran** : `/parcours/point-zero-monde-0/accompli`, dans la grammaire de la clôture (fond sombre, surtitre or, titre Slab), quand le badge manque. Il liste les Expériences obligatoires non franchies, chacune avec son état de carte (« Passée pour l'instant », « Commencée », « Attend d'être reconnue »…) et un lien vers sa fiche.

**Mes textes provisoires, à remplacer par les tiens** :
- surtitre : « Parcours presque accompli » ;
- titre : « Le livre attend encore une page » (une manquante) / « Le livre attend encore N pages » (plusieurs) ;
- phrase : « Le badge de ce parcours se reçoit quand chaque Expérience obligatoire est franchie. L'Atelier Point Zéro, qui attend son facilitateur, n'en fait pas partie. » ;
- lien de chaque ligne : « Reprendre » ;
- sortie : « Revenir à la carte du voyage ».

Ton ton et tes mots, dans le registre de la clôture. Sans jamais laisser croire que le joueur a échoué : il a seulement une page à écrire.

— le poste fixe

---

### 2026-09-17 · du poste fixe · Boris veut les cinq parcours du site en ligne pour le Festival (1er octobre) — ton calendrier de livraison, et la Carte du Seuil du M0

**Boris, aujourd'hui** : les parcours du site que vous retravaillez ensemble doivent être **en ligne pour le Festival du 1er octobre**. Il reste quatorze jours, et la promotion en production doit précéder le Festival.

**1. Les cinq parcours — ce qu'il me faut pour les porter à temps**
- **Une date de livraison, et si possible une livraison PROGRESSIVE** : le PsychoKernel, déjà validé par Boris, d'abord, puis les autres à mesure. Je porte parcours par parcours dès réception, dans `public/sas/` et `app/views/sas/` (ma zone), sans mobiliser le portable. Je sais que tu voulais garder le PsychoKernel jusqu'à la fin de la reprise ; l'échéance de Boris change la donne, à toi de dire si c'est possible.
- **Le contrat qui rend le portage sûr**. Ces parcours prouvent E10 et sont liés au M0 depuis #284 :
  - les **slugs** (`humanite`, `scenarios`, `croyances`, `paralysie`, `reveil`) ;
  - la trace locale **`pz_parcours_<slug>_v1`** et son **`completed_at`** (c'est lui que l'import lit) ;
  - les **clés de réponse importées** (`config/sas.yml`, `cles:`) ;
  - les **identifiants de badge** (`badge:`) ;
  - les deux accroches de fin d'écran que le Jeu remplace en excursion (`_passage_accompli`, `_sortie_vers_le_jeu`) et le bandeau.
  - Ce qui change dans ce contrat doit être DIT, parcours par parcours : un slug, une clé importée ou un badge modifiés passent par le portable (`config/sas.yml`, `TraceSas`) et par ses bancs.
- **Le lieu de livraison** : un dossier par parcours dans `zegame-prototypes`, comme pour les autres maquettes, ou le lieu que tu préfères, pourvu que je puisse le lire.

**2. La Carte du Seuil (E19, rang 4) — deux questions avant tout code**
Aujourd'hui, le joueur coche « J'ai scellé ma Carte du Seuil » sans qu'aucune Carte n'existe. Le contrat de stockage est prêt (`docs/vision/m0-e19-carte-du-seuil-contrat.md`) ; il manque :
- **la maquette cible du M0**. `carte-seuil-m1-cible` vise le Monde 1 (états Invitation, Active…), et `carte-du-seuil-role-appel` est un ancien prototype sur le Profil. Laquelle porter pour E19, ou faut-il une cible propre ?
- **le modèle éditorial**, que le contrat renvoie à toi et à Boris (§5) : la Carte porte-t-elle la Graine de passage en socle plus une sélection de productions, ou une sélection seule ?

Avec l'échéance, une Carte minimale (la Graine de passage, les éléments choisis, le sceau) serait tenable. Dis ce que tu veux voir.

**3. Rappel** : les mots de l'écran « pas encore » de la fiche finale (#296), dans mon message précédent.

— le poste fixe

---

### 2026-09-17 · du poste fixe · Carte du Seuil du M0 : Boris a tranché — Graine + sélection, puis sceller ; il faut une maquette minimale

**Boris, mot pour mot** : « Oui, Graine + sélection puis sceller. » C'est la réponse au §5 du contrat (`m0-e19-carte-du-seuil-contrat.md`), avec une version minimale pour le Festival.

**Il n'y a pas de maquette à porter.** `carte-seuil-m1-cible` est un autre objet (le triangle des futurs du Monde 1), et `carte-du-seuil-role-appel` un ancien prototype sur le Profil. Il faut une cible pour E19 rang 4, **minimale, idéalement d'ici le 21 septembre** : la Carte est la dernière pièce qui ferme le M0, et elle doit passer la recette avant la promotion.

**Un squelette pour aller vite — à toi de le dessiner, de le corriger ou de le refuser :**
1. **La Graine de passage, en socle.** Celle du rang 3 d'E19, relue et non modifiable ici (un lien pour la corriger, comme « Relire »). Sans Graine, la Carte renvoie à l'étape 3.
2. **Les productions à choisir.** Les entrées du registre des Traces, groupées par famille, chacune avec son titre et un court extrait, cochables.
3. **L'aperçu de la Carte** : la Graine et les éléments cochés, tels qu'ils seront scellés. La Carte reste privée.
4. **« Sceller ma Carte du Seuil »**, refusé si rien n'est choisi ; puis l'état scellé (la date, la Carte relue) et le retour à l'Expérience.

**Les mots** : le titre, l'accroche, la phrase de privauté, le libellé du sceau, l'état scellé, l'état vide (aucune production à choisir) et le refus quand rien n'est coché.

Le portable prépare le stockage en parallèle. Je porte l'écran dès ta maquette.

— le poste fixe

---

### 2026-09-18 · du poste fixe · parcours 1 porté (#297) — un libellé à trancher, et les questions des parcours 2 à 5 pour te laisser le temps

**Le parcours 1 est porté** (pointzero-app#297, en attente de fusion) : tes sept écrans, tes classes, tes textes et tes images. Seuls ajouts : la coque du site (bandeau, galerie des cinq questions, fenêtre « Quitter », traces locales) et les accroches du Jeu à l'accomplissement.

**Un libellé à trancher.** Ta maquette dit « Explorer les futurs possibles » ; le parcours servi dit « Continuer avec « Quels sont les scénarios du futur ? » → ». J'ai gardé le second, pour deux raisons :
- le canon du Sas §3.2 veut une poursuite qui nomme sa destination ;
- `verifier_sortie_sas` §3 compare ce libellé au titre de la page visée : c'est lui qui a attrapé, le 5 septembre, un libellé copié d'un autre parcours.

Si tu préfères ton libellé, dis-le : je le porterai en déplaçant la garde du banc. Pas avant.

**Deux autres écarts, pour information :**
- **Les boutons de fin sont quatre, et non deux.** « Entrer dans le Jeu » (ou « Revenir à l'Expérience » en excursion) et « Revenir aux cinq questions » rejoignent les tiens ; la rangée passe à la ligne.
- **La phrase de passage accompli** (canon §3.2) est posée sous la note du guide, en clair sur le cadre sombre.

**Pour les parcours 2 à 5, les points que j'aurai besoin de toi** (je les détaillerai dans chaque PR, avec l'écran) :
- **Parcours 2, scénarios** : d'où viennent les options de signes (`signOptions`) ? Sont-elles éditoriales et figées, ou tirées de l'Atlas des 25 ?
- **Parcours 3, croyances** :
  - le titre de c01 énonce la thèse au lieu de poser la question : est-ce voulu ?
  - l'option « ne pas répondre » a disparu : est-ce un choix ?
- **Parcours 4, paralysie** : les récits de la ville fictive sont-ils validés tels quels (textes définitifs) ?
- **Parcours 5, réveil.** Ta note le disait déjà : les règles de `evaluate()` sont écrites en dur dans la maquette. Il me faut, pour ne rien inventer dans la vue :
  - les poids et les seuils des jauges ;
  - d'où viennent les 82 % et les 3 % affichés ;
  - le mot final selon le taux ;
  - ce qui doit être conservé dans la trace locale et importé.

— le poste fixe

---

### 2026-09-18 · du poste fixe · parcours 2 porté (#298) — le même libellé de poursuite, et l'icône de lecture devenue bouton

**Le parcours 2 est porté** (pointzero-app#298, en attente de fusion), fidèle à ta maquette. Trois points pour toi :

1. **La poursuite.** Ta maquette dit « Explorer les cycles du Point Zéro », ce qui ramènerait au parcours 1. Le parcours servi mène aux croyances : « Continuer avec « Quelles forces ont façonné nos croyances ? » → ». J'ai gardé le second, pour la même raison qu'au parcours 1 (canon §3.2, garde de `verifier_sortie_sas`). **Ta décision vaut pour les deux** : si tu veux tes libellés, dis-le, et dis aussi vers où chacun doit mener.
2. **L'icône de lecture de chaque carte ouvre le film.** Les vingt-cinq films existaient dans le parcours servi, et ta NOTE dit que l'icône « signale la vidéo associée ». Si tu voulais une icône purement indicative, dis-le.
3. **Deux propositions de signes sont génériques** (« Un débat public reprend les hypothèses de « X » », « Des pratiques locales expérimentent déjà une réponse proche »). Elles sont portées telles quelles, et c'est la question déjà posée hier.

**Hors maquette** : une seule colonne de leviers sous 420 px, parce que les deux colonnes débordaient de 8 px à 375 px (« comportement » ne se coupe pas). S'y ajoute un garde-fou : sans les trois sommets du triangle, s05 → s07 renvoient à s04 au lieu de remplir un triangle d'exemple.

— le poste fixe
