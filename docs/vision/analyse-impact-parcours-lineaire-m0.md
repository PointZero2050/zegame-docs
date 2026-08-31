# Analyse d'impact — le Monde 0 devient un parcours linéaire

> **Demandée par Boris le 30 août 2026**, après l'inflexion prise avec Codex pour simplifier
> l'UX du Monde 0. Rédigée par le poste fixe.
>
> **Source de l'inflexion :** `zegame-prototypes`, branche `codex/parcours-lineaire-m0`
> (`ede0a56`, `344e003`, `8a90e26`), dossier `parcours-lineaire-m0-cible/`.
>
> ⚠️ **Cette branche n'est PAS dans `main` et n'a été annoncée dans aucune boîte.** Je l'ai
> trouvée en balayant les références du dépôt, pas en la recevant. Elle n'est donc pas publiée
> sur l'hôte des maquettes, qui suit `main` (`3c678db`). Si elle doit servir de cible, elle
> demande à être fusionnée et annoncée — sans quoi le portable et moi travaillerons sur deux
> versions différentes du même écran, ce qui est déjà arrivé le 30 au matin.

---

## 1. Le changement, en une phrase

**Le Monde 0 cesse d'être sept portes ouvertes et devient un chemin unique.** Les sept
Puissances ne sont plus des entrées : elles deviennent des **déblocages**, révélés au fil des
passages. « Les espaces encore endormis apparaîtront au fil de ton parcours » (README de la
maquette).

La maquette décrit quatre états :

| état | ce qu'il montre |
|---|---|
| `?view=journey` | la carte du voyage : prochain passage, 3 chapitres, 16 passages essentiels |
| `?view=experience` | un seul geste — « TON GESTE MAINTENANT » — détails repoussés sous le pli |
| `?view=unlock` | « UNE PUISSANCE S'ÉVEILLE » + premier geste guidé |
| `?view=dashboard` | après le M0, l'accueil devient un tableau de bord |

Et la navigation mobile passe de **cinq entrées à trois** : Parcours, Puissances (un tiroir),
Profil.

---

## 2. ⚠️ Ce qui existe déjà, et qu'il ne faut surtout pas reconstruire

**Les trois chapitres de la maquette sont déjà dans l'application, mot pour mot.**
`config/journeys/point-zero-monde-0.yml` :

```
chapitres:
  - mouvement: Franchir le seuil — Je pressens
  - mouvement: Reconnaître la constellation — Je relie
  - mouvement: Prendre place — Je contribue
```

La maquette dit « Je pressens », « Je relie », « Je contribue ». **C'est la Marelle.** Le
parcours linéaire du Monde 0 existe, il a ses chapitres, ses expériences, sa progression
(`JourneyProgress`, `Chapitre#requis_faits` / `requis_total` / `omega_total`), ses pages de
chapitre (portées le 29 août) et ses pages d'expérience.

Ce que l'inflexion change n'est donc pas « construire un parcours » : **c'est le promouvoir.**
Aujourd'hui la Marelle est atteignable par UNE carte sur sept, celle de la Volonté. Demain elle
est le Monde 0.

C'est la meilleure nouvelle de cette analyse : le cœur est déjà là et déjà éprouvé par des bancs.

---

## 3. ⚠️ L'impact profond : une inversion de causalité

C'est le point qui coûtera le plus, et il ne se voit pas dans les maquettes.

**Aujourd'hui**, une carte s'active parce que le joueur a fait quelque chose **dans son
territoire**. `Monde0Etats::Lecture#active?` lit **sept sources hétérogènes** : une `Trace`
d'Immateria pour le Désir, un `JourneysUser` pour la Volonté, une bifurcation pour
l'Imagination, un héros choisi pour l'Émotion, un `MarqueurDAttention` pour la Communication,
une clé assimilée pour l'Intuition, un `MoteurAssessment` pour la Transcendance.

**Demain**, une Puissance s'éveille parce que le joueur a franchi **un passage du parcours**.
Une seule source : `JourneyProgress`.

Ce n'est pas un habillage, c'est un **remplacement de moteur**. Et ce moteur ne sert pas que
l'accueil : **treize fichiers lisent `Monde0Etats`**, dont six services qui n'ont rien à voir
avec une page d'accueil —

```
app/services/ventilation_omega.rb          app/services/graine.rb
app/services/sequence_de_gestes.rb         app/services/monde_1_home_state.rb
app/services/centre_de_personnalisation.rb app/models/seuil_franchi.rb
app/controllers/concerns/marque_de_visite.rb
```

⚠️ **`Monde1HomeState` a la même forme.** L'accueil du Monde 1 est un échafaudage qui reprend
les classes du M0 ; si le M0 change de modèle, le M1 hérite de la question. Elle n'a pas à être
traitée dans le même lot, mais elle doit être posée avant, sans quoi on écrira deux fois.

---

## 4. Les surfaces impactées, et à qui elles appartiennent

| surface | ce qui arrive | zone |
|---|---|---|
| `app/views/home/monde_0.html.haml` | **remplacée** par la carte du voyage | poste fixe |
| `public/pz/m0/accueil.css` | **remplacée** (deck, cartes, pagination, flèches) | poste fixe |
| `app/views/layouts/_coque_m0.html.haml` (la roue) | devient le **tiroir Puissances**, avec états éveillé / prochain / endormi | poste fixe |
| `app/views/layouts/_barre_mobile.html.haml` | **5 entrées → 3** | poste fixe |
| `public/pz/m0/coque.css` | suit la barre et le tiroir | poste fixe |
| `app/views/journeys/_show.html.haml` | devient l'écran principal, pas une page de rubrique | poste fixe |
| `app/views/challenges/_fiche_joueur.html.haml` | un seul geste, détails sous le pli | poste fixe |
| `config/monde_0.yml` | les 7 `chemin` ne sont plus des destinations d'accueil | à arbitrer |
| `app/services/monde_0_etats.rb` | change de source | **portable** |
| `SeuilFranchi`, `VentilationOmega`, `Graine`, `SequenceDeGestes` | dépendent de l'état des territoires | **portable** |
| routes `/jeu`, `/parcours/...` | `/jeu` doit rendre le parcours | **portable** |
| 14 bancs | voir §6 | poste fixe |

---

## 5. Ce qui n'a de point de chute nulle part aujourd'hui

Ce sont les manques réels — à créer, pas à déplacer.

1. **L'écran « UNE PUISSANCE S'ÉVEILLE ».** Aucune surface n'existe. C'est le moment le plus
   important du nouveau M0 : c'est lui qui transforme un parcours en déblocage.
2. **Le tableau de bord d'après-M0.** Aucune vue. `Coque.monde_de(user)` sait déjà dire qu'on
   est passé au Monde 1 ; ce que le joueur voit à ce moment-là reste à définir.
3. **Les chapitres en horizon** (noms masqués tant que le précédent n'est pas franchi). Rien ne
   masque un chapitre aujourd'hui — `JourneyProgress` expose tout.
4. **La reconnaissance automatique** : « Le Jeu reconnaît automatiquement la fin du tutoriel.
   Aucun bouton de validation supplémentaire. » Il n'existe aucun canal par lequel Immateria
   annonce la fin d'un tutoriel. ⚠️ **C'est le point le plus lourd de la liste**, et il n'est pas
   visuel : sans lui, la promesse de la maquette est fausse dès le premier passage.
5. **Le décompte « 16 passages essentiels · 3 bifurcations facultatives »** existe par chapitre
   (`requis_total`, et `required` sur chaque expérience) mais pas au niveau du parcours.

---

## 6. Ce que ça coûte aux bancs

**Quatorze fichiers** de `scripts/` assertent le modèle à sept cartes ou lisent `Monde0Etats` :

```
comptes_recette_m0        repetition_m0             verifier_accueil_m0
verifier_aide_de_page     verifier_coque            verifier_coque_m0
verifier_fresque_graines  verifier_gestes           verifier_graine
verifier_illustrations_m0 verifier_monde_1_etats    verifier_moteur_conscience
verifier_pastille_et_omega verifier_v4_imagination
```

⚠️ **La règle de la maison s'applique en grand : un balisage asserté qui change demande son banc
dans la MÊME livraison.** Quatorze bancs ne se reprennent pas en une passe. C'est l'argument le
plus fort pour découper la migration (§8) plutôt que de la livrer d'un bloc.

⚠️ Et une part de ces assertions ne doit pas disparaître mais **se retourner** : `verifier_accueil_m0`
garde aujourd'hui que chaque carte s'active sur SA vraie trace. Ces sept sources restent vraies
au niveau des données ; c'est leur PROJECTION qui change. Les supprimer perdrait sept garanties
métier pour une refonte d'écran.

---

## 7. ⚠️ Ce que l'inflexion périme, y compris de très frais

Il faut le dire clairement plutôt que de le découvrir en fusionnant :

- **le deck des sept cartes** et toute sa mise en page mobile — soit les PR **#123**, **#126** et
  **#128** des 30 et 31 août, c'est-à-dire deux jours de travail sur un écran qui disparaît ;
- **la matrice d'illustration** (une carte change d'image quand un territoire durable s'ouvre) ;
- **les seuils et badges par territoire**, si l'éveil devient la récompense ;
- **la pagination mobile**, les **flèches de glissement**, la **pastille d'état** des cartes ;
- **la cible mobile `fbf327c`** que Codex a publiée le 30 et que j'ai portée en #128 : elle
  perfectionne le deck que l'inflexion supprime.

⚠️ **Question directe à Boris : faut-il encore fusionner #128 ?** Elle améliore réellement
l'accueil d'aujourd'hui (plus de défilement, carte plein écran) et sera jetée avec lui. Mon
avis : **oui, si le nouveau M0 n'arrive pas cette semaine** — l'accueil actuel reste ce que
voient les joueurs — **non, s'il arrive tout de suite**, auquel cas autant ne pas payer une
recette pour un écran condamné.

---

## 8. Ordre de livraison proposé

Découpé pour que chaque étape soit vérifiable seule et n'oblige jamais à reprendre quatorze
bancs d'un coup.

1. **Décider la source de vérité de l'éveil** (portable) : `JourneyProgress` remplace les sept
   lectures de `Monde0Etats`, ou coexiste avec elles. Rien de visuel ne peut être juste avant
   cette décision.
2. **`/jeu` rend la carte du voyage** (portable pour la route, poste fixe pour la vue). L'accueil
   à sept cartes reste servi sur `/jeu?deck=1` le temps de la bascule, pour que la recette
   compare deux écrans plutôt qu'un écran et un souvenir.
3. **Le tiroir Puissances** remplace la roue, avec ses trois états. La barre passe à trois
   entrées.
4. **L'écran d'éveil**, qui n'existe pas — le plus créateur de valeur et le plus court.
5. **La page d'expérience à un seul geste**, qui est surtout un retrait : les blocs existent, il
   s'agit de les repousser sous le pli.
6. **Le tableau de bord d'après-M0.**
7. **La reconnaissance automatique d'Immateria** — indépendante, longue, et à commencer tôt
   parce qu'elle ne dépend d'aucune des six autres.

---

## 9. Les questions qui reviennent à Boris

1. **La branche `codex/parcours-lineaire-m0` est-elle la cible validée ?** Elle n'est ni fusionnée
   ni annoncée. Tant qu'elle ne l'est pas, je ne porte rien depuis elle.
2. **#128 : fusionner ou abandonner ?** (§7)
3. **Les sept territoires gardent-ils leurs pages ?** La maquette ne montre plus de « territoire »
   comme destination, mais Immateria, la Fresque, les Guides, les Échanges existent et sont
   atteints par le parcours. Le tiroir Puissances devient-il leur seul accès ?
4. **Les seuils et badges par territoire survivent-ils** à un modèle où c'est le passage qui
   récompense ?
5. **Le Monde 1 suit-il ?** Son accueil est bâti sur les mêmes classes.
6. **La reconnaissance automatique** engage un travail hors interface : est-elle dans le
   périmètre de cette inflexion, ou la première version demande-t-elle encore un bouton ?

---

## 10. Mesure de l'écart : ce que le parcours rend DÉJÀ, contre la cible

Relevé sur la préprod le 30 août, compte `sacha`, `/parcours/point-zero-monde-0`. C'est la page
que le Monde 0 est sur le point de devenir : elle existe, elle fonctionne, et voici ce qui la
sépare de la maquette.

| | aujourd'hui | cible Codex |
|---|---|---|
| chapitres | **3**, aux bons noms | 3 |
| passages | 5 + 4 + 5 = **14** | 5 + 7 + 7 = **19** (16 essentiels + 3 bifurcations) |
| Omégas | 24 + 25 + 51 = **100 Ω** | 39 + 61 + 74 = **174 Ω** |
| chapitres 2 et 3 | **entièrement ouverts**, noms des passages visibles | **horizons** : « les noms apparaîtront lorsque tu auras franchi le premier chapitre » |
| premier passage | « Le Point Zéro : entrer dans le Jeu » | « **Façonner mon jumeau** » (Immateria) |
| hauteur sur téléphone | **4 019 px** à 375 × 812 | un écran, « Continuer » visible d'emblée |

Trois conclusions :

1. **La charpente est juste, le contenu ne l'est pas.** Cinq passages manquent, 74 Ω manquent, et
   la cible ouvre par un passage qui n'est pas le nôtre. ⚠️ **C'est de l'éditorial** : il revient
   à Codex et à Boris, pas à l'intégration.
2. **Les chapitres en horizon sont un vrai manque**, pas un effet de style : aujourd'hui la page
   dit tout, tout de suite. C'est l'inverse de la promesse « la route se révèle à mesure ».
3. ⚠️ **4 019 px sur un téléphone.** La page que le M0 va devenir est aujourd'hui **le plus long
   écran de l'application** — plus long que `f05` (2 945 px) que l'audit des parcours publics
   pointait comme défaut majeur. La cible, elle, tient dans un écran. C'est la part la plus
   lourde du travail d'intégration, et elle est chez le poste fixe.
