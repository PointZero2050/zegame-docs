# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

### 2026-08-24 · du poste fixe · Les 51 illustrations sont déclarées — et `co-c06` n'a pas de place

**Attendu :** dire où va le complément `c06-qualite-captive-garde-fous`, ou acter qu'il ne se
branche pas. **Référence :** https://github.com/PointZero2050/pointzero-app/pull/82

Boris a demandé de tout brancher. Les **51** illustrations des blocs 2 et 3 sont désormais
déclarées dans le champ `image:` des sections — les deux jeux n'en portaient **aucune**, alors
que tes 33 originales attendaient depuis le 17 juillet.

Tes listes de branchement se lisent directement dans les clés du YAML. Trois de tes intitulés
n'ont pas de code d'écran : je les ai résolus par le titre de section (« La Bulle —
l'aménagement » = `B1`, « Barrière » = `F4`, « Josef » = `V4`), et « Fil3 » s'appelle `FI3`.

**⚠️ UNE COLLISION, ET JE L'AI TRANCHÉE AVEC TES PROPRES MOTS.** `DELIB_COMMUNICATION` était
réclamée par deux images : l'originale `07-communication`, validée en juillet, et le complément
`c06-qualite-captive-garde-fous`, proposé ce matin. Une section ne porte qu'une image. Tes docs
disent que les compléments sont livrés « comme propositions à arbitrer, **sans remplacer les
sources déjà validées** » : l'originale reste.

**Conséquence assumée : `co-c06` n'est déclaré nulle part.** Je ne l'ai pas posé ailleurs au jugé
— c'était le seul des 19 qui ne se lisait pas dans un titre de section, et le déplacer aurait été
une décision éditoriale déguisée en intégration. Dis-moi s'il remplace l'originale, s'il va sur
un autre écran, ou s'il reste une proposition non retenue.

---

### Différé après la clôture du Monde 0 · du poste fixe · Échanges Monde 1

### 2026-08-24 · du portable · ⚠️ Boris demande UNE étape là où ta §6.6 en garde trois — et son motif ne se vérifie pas

**Attendu :** trancher, puis écrire le contenu « étape unique » des six expériences concernées.
Sans lui je ne porte rien : inventer l'éditorial serait exactement ce que j'ai refusé de faire
pour les Puissances. **Référence :** ta §6.6 · mesures de production ci-dessous.

**Boris a listé neuf expériences à réduire.** Deux sont faites (`les-choses-se-precisent` et
`le-sas-d-entree`, dont le lien fautif vers les cinq parcours est retiré). **Six attendent ton
éditorial** — tu n'as écrit l'étape unique que pour Le Coupable idéal.

**⚠️ ET TROIS DE SES DEMANDES CONTREDISENT TA §6.6 :**

| expérience | ta §6.6 | demande de Boris |
|---|---|---|
| `une-drole-d-epoque` | **3 gestes**, bornés par `jour_1_e2`, `jour_1_e4`, miroir atteint | **1 étape** |
| `avant-le-zero` | **3 gestes**, bornés par `D`, goulot `R*`, fin atteinte | **1 étape** |
| `le-conseil-omega` | **3 gestes**, bornés par `TREIZIEME`, `cap_desir`, Rôle d'appel | **1 étape** |

Ta §6.6 n'est pas un choix esthétique : tu as **dérivé** ces bornes d'états réellement persistés,
et c'est solide. Boris, lui, veut une étape. **Je ne tranche pas** — mais je te donne le fait qui
manque au débat, parce qu'il défait le motif invoqué.

**Son motif était : « une étape validée par contrôleur, SINON LES POINTS NE SONT PAS DISTRIBUÉS ».
Mesuré en production, c'est faux :**

| | lignes | validées | Ω distribués |
|---|---|---|---|
| `une-drole-d-epoque` | 14 | **13** | **39** |
| `avant-le-zero` | 14 | **14** | **84** |
| `le-conseil-omega` | 7 | **7** | **21** |

Les trois sont en validation **automatique** et leurs Ω circulent. Le découpage en trois étapes
n'empêche rien : il est décoratif, jamais bloquant. Je l'ai dit à Boris.

**Reste donc un arbitrage d'ergonomie pure**, et il t'appartient autant qu'à lui : trois étapes
qui nomment trois moments réellement observables, ou une étape qui dit « traverse » et laisse le
mini-jeu faire son travail — comme tu l'as tranché pour le procès, avec l'argument des « deux
reprises mensongères ». Cet argument vaut-il pour ces trois-là ? Toi seul peux le dire : c'est
toi qui as établi que leurs interruptions sont réelles.

**Les trois autres réductions ne te contredisent pas** et n'attendent que ton texte :

| | demande |
|---|---|
| `l-ecosysteme-point-zero` | **2 étapes** — Boris : « Conserver mon schéma ne correspond à rien » (et de fait, cette porte mène à la même URL que l'étape 2, je te l'avais signalé) |
| `le-signe-de-reconnaissance` | **1 étape** |
| `vivre-l-atelier-point-zero` | **1 étape** : s'inscrire à un atelier, vérifié par contrôleur — `InscriptionCreneau` existe, la preuve est à portée |

**Et une restructuration complète, la plus lourde : `le-site-du-point-zero`.** Boris :

> « Elle consiste à présent à réaliser les 5 parcours du site. Étape 1 : renvoi vers les 5
> parcours. Faire au moins un parcours (suivi par contrôleur) ouvre l'étape 2 qui indique
> "X parcours réalisés sur 5" et propose un CTA vers l'expérience suivante. Un lien vers les
> 5 parcours reste constamment disponible. »

**Côté serveur, tout est prêt** : le compteur existe (`TraceSas.pour(joueur)`), et les Ω des cinq
parcours sont livrés depuis une heure — 5 par parcours, sur les skills exacts que tu as validés.
La preuve serveur de l'étape 1 sera « au moins une `TraceSas` importée ». Il ne manque que ton
éditorial des deux étapes.
