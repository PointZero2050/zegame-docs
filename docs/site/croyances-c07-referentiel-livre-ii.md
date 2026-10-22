# « Quelles forces ont façonné nos croyances ? » — écran 7 au référentiel du Livre II

> Proposition du poste fixe, 22 octobre 2026, à la demande de Boris : « mettre à jour les libellés des
> 7 puissances, qui sont le référentiel du Livre II (qui a un peu évolué par rapport au L I). Établis une table de
> correspondance et propose un éditorial et des rattachements à jour. » **Validée telle quelle par Boris le
> 22 octobre 2026**, sans relecture de Codex (sa décision) : lecture B des rattachements, formule de la
> Transcendance retenue. Intégrée par https://github.com/PointZero2050/pointzero-app/pull/461. Les verbes (§ 1) restent à
> trancher : cette page ne les affiche pas.

## Ce que la page affiche aujourd'hui

Écran 7 du Sas « Croyances » (`/monde-zero/exploration/croyances`, `public/sas/croyances/app.js`,
`DEEP_BELIEFS` et `RENFORTS`) : sept boutons de puissance, chacun ouvre une croyance limitante, une phrase sur
la manière dont le pratico-inerte l'entretient, et allume les inventions qui « peuvent la renforcer ». Les noms,
les croyances et les flèches viennent du **Livre I** et de sa carte `Ressources Point Zero/Modèles/Pratico-inerte-2.jpg`.

## 1. Table de correspondance — par chakra, pas par nom

Le Livre II garde trois noms du Livre I **à une autre place** : rattacher par le nom serait une erreur. La
correspondance se fait par le chakra, que confirment l'ordre du Livre II (Désir à la Racine, Émotion au
cœur — « Anahata, le quatrième chakra » —, la Couronne qui « donne ») et les couleurs de l'application
(`config/puissances/*.yml` : rouge, orange, jaune, vert, bleu, indigo).

| Chakra | Livre I (page actuelle) | **Livre II** | Verbe (application) |
|---|---|---|---|
| Racine | Ancrage | **Désir** | JE SUIS |
| Sacré | Désir | **Volonté** | JE DÉCIDE |
| Plexus solaire | Volonté | **Imagination** | JE CRÉE |
| Cœur | Sensibilité | **Émotion** | JE RESSENS |
| Gorge | Communication | **Communication** | JE M'EXPRIME |
| Troisième œil | Intelligence | **Intuition** | JE DISCERNE |
| Couronne | Transcendance | **Transcendance** | JE DONNE |

ⓘ Les verbes ne s'affichent pas sur cet écran. À noter pourtant : le manuscrit d'impression du Livre II écrit
*Volonté : JE VEUX*, *Communication : J'EXPRIME*, *Intuition : JE CONNAIS* ; l'application, *JE DÉCIDE*,
*JE M'EXPRIME*, *JE DISCERNE*. Lequel fait foi ?

## 2. Éditorial proposé — les croyances des sept gardiens

Les croyances sont celles des **gardiens du Livre II** (chapitre « les puissances blessées »), dans **leur
ordre de descente** : le livre insiste qu'« il serait naïf de vouloir commencer directement par la Racine », et
les Mondes 0-1 travaillent le premier gardien (« JE DISCERNE »). La page ouvrirait donc sur l'Intuition — au
lieu de la Transcendance aujourd'hui.

La troisième colonne (la lecture du pratico-inerte) est **réécrite par moi** pour chaque nouvelle croyance, sur
le modèle des phrases actuelles (« Les … peuvent … ») : à relire par Codex.

| # | Puissance | Croyance (Livre II) | Lecture proposée |
|---|---|---|---|
| 1 | Intuition | « Je dois comprendre avant d'agir » | Les instruments de preuve peuvent faire de la compréhension un préalable sans fin, et disqualifier ce qui se perçoit avant de se démontrer. |
| 2 | Communication | « M'exprimer pleinement est impossible » | Les codes et médiations peuvent autant faciliter la parole que la rendre conforme, jusqu'à faire croire qu'aucun langage ne peut porter ce qui a été vécu. |
| 3 | Émotion | « Si j'ouvre mon cœur, je vais souffrir » | Les dispositifs qui endurcissent ou anesthésient peuvent apprendre à protéger le cœur plutôt qu'à écouter ce qu'il signale. |
| 4 | Imagination | « Je peux créer des mondes, mais pas transformer celui-ci » | Les industries de l'image et de la technique peuvent capter l'imaginaire dans des mondes à consommer, et le détourner du réel à transformer. |
| 5 | Volonté | « Mériter demande un effort » | Les systèmes de mérite et de rétribution peuvent faire croire que rien ne se reçoit sans avoir été arraché. |
| 6 | Désir | « M'aimer serait de l'égoïsme » | Les normes peuvent faire de l'amour de soi une faute, et le marché proposer de combler par la consommation ce qui ne naît que de l'intérieur. |
| 7 | Transcendance | « Ce que je suis doit être conservé » ⚠️ | Les dispositifs d'accumulation et de mémoire peuvent faire d'une existence une possession à garder plutôt qu'une offrande à renouveler. |

⚠️ **Le septième gardien n'a pas de croyance entre guillemets dans le Livre II.** Le livre décrit une tentation —
transformer le « JE SUIS » en « je suis pour toujours », en « nouvelle forteresse » — à laquelle la Couronne
répond « JE DONNE CE QUE JE SUIS ». La formule proposée en est tirée ; à valider ou à remplacer par Boris.
(Le Livre I disait « L'univers est vide de sens ».)

## 3. Rattachements proposés — les inventions qui « peuvent renforcer »

Les vingt inventions de la carte ne changent pas. Deux lectures possibles des flèches :

- **A. Fidèle à la carte** : on garde chaque flèche sur son chakra et l'on renomme seulement la puissance. Rien
  n'est inventé, mais trois rattachements deviennent faibles avec les croyances du Livre II (marqués ✗).
- **B. Relu au Livre II (proposé)** : chaque croyance du gardien reçoit les inventions qui l'entretiennent le plus
  directement. C'est une lecture éditoriale, plus une transcription de la carte : la note de source de l'écran
  (« relevé flèche par flèche sur la carte-source ») devrait le dire.

| Puissance | A. Carte du Livre I, par chakra | B. Proposé (Livre II) |
|---|---|---|
| Intuition | Droit, Écriture, Science | Droit, Écriture, Science *(inchangé)* |
| Communication | Religion, Politique, Démocratie | Religion, Politique, Démocratie *(inchangé)* |
| Émotion | Travail salarié, Éducation publique | Guerre codifiée, Médecine industrielle |
| Imagination | Technique, Mode et marques, Guerre codifiée ✗ | Technique, Mode et marques |
| Volonté | Alimentation industrielle ✗, Sexualité de consommation ✗ | Travail salarié, Éducation publique, Argent |
| Désir | Territoire ✗, Propriété ✗, Médecine industrielle ✗ | Alimentation industrielle, Sexualité de consommation |
| Transcendance | Rituels funéraires, Mesure du temps, Argent | Rituels funéraires, Mesure du temps, Propriété, Territoire |

La **Sédentarité** reste sans flèche dans les deux lectures, comme sur la carte.

## 4. Ce que la mise à jour toucherait

`public/sas/croyances/app.js` (`DEEP_BELIEFS`, `RENFORTS`, et le commentaire de source), une partie
enregistrée dont l'index `c07_profonde` change de sens (l'ordre change : réinitialiser ce seul choix), et le banc
qui lit cet écran. Aucune donnée serveur. Pas d'autre page du Sas : les puissances n'y apparaissent qu'ici.
