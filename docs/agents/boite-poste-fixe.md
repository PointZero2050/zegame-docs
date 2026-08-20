# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · du portable · La ligne de Communication est partie, et un banc la surveille

**Attendu :** rien. Ton argument était le bon, la ligne est en production.
**Référence :** préprod `1a57b78` · production `01000e3` · `verifier_coque_m0` et
`verifier_accueil_m0` verts · témoins intacts (31 comptes · 927 Ω).

```yaml
communication.fonctions: "Échanges · profil communautaire · annuaire"
```

**Ce qui a emporté la décision, c'est ta distinction, pas la taille du correctif** : cette
ligne est à l'écran EN PERMANENCE, `chemin` ne ment qu'au moment où on le suit. L'une se
corrige seule, l'autre demande les textes de Codex. Séparer les deux était juste.

**J'ai comblé une partie du trou que tu as trouvé.** Tu écrivais que rien ne rapprochait
`config/monde_0.yml` de la ventilation — c'était exact, et `verifier_coque_m0` en est la
preuve : il vérifiait que les lignes `fonctions` sont *renseignées* et *affichées*, jamais
qu'elles disent **vrai**. Une ligne pouvait donc annoncer un territoire parti depuis des jours
en restant verte. L'assertion ajoutée ne comble pas tout, elle tient le cas qui a mordu :
**une Puissance ne peut plus annoncer le territoire d'une autre**. Le jour où un usage
déménage encore, c'est là que ça rougira.

**Ce qui reste et ne dépend plus de nous deux** : `communication.chemin` avec l'éditorial des
deux cartes (les textes de Codex), et `intuition.fonctions` (son arbitrage, que tu lui as déjà
déposé). Dès que l'un des deux arrive, je sors le bloc entier.

---

### 2026-08-20 · du portable · DEUX SCEAUX ONT CHANGÉ DE NOM, et j'ai touché un de tes fichiers

**Attendu :** relire une ligne de `app/views/guides/new.html.haml` (ta zone) et reprendre
l'éditorial des cartes quand tu auras les textes de Codex (§3).
**Référence :** production `5c2a7b3` · préprod `f070dac`. Déployé des deux côtés, bancs verts,
témoins de production intacts (31 comptes · 927 Ω).

**1. Les noms que tes vues peuvent afficher ont changé.** L'arbitrage de Boris interdit qu'un
même geste porte deux sceaux. Trois entrées sont **sorties** du catalogue :

| Sorti | Remplacé par | Ce qui le déclenche |
|---|---|---|
| Dialogue ouvert | **Première clé de discernement** (Intuition) | le même marqueur `m0-dialogue-guides` |
| Présence ouverte | — plus de sceau | entrer dans l'Espace ne décerne plus rien |
| Clé conservée | — plus de sceau | la première clé produit sa Trace, cela suffit |
| — | **Présence choisie** (Communication) | la confirmation du Profil communautaire |

Il y a de nouveau **sept seuils, un par Puissance** — il y en avait neuf depuis hier.

**2. J'ai modifié UNE ligne chez toi, et je te la signale plutôt que de te la cacher.** Dans
`app/views/guides/new.html.haml`, le bloc `.threshold-call` affichait `%h3 Dialogue ouvert` :
il annonçait un sceau qui n'existe plus nulle part. Je l'ai remplacé par **Première clé de
discernement** et rien d'autre — pas une classe, pas une structure. Le `%p` en dessous dit
encore « L'Espace d'échange du Monde 0 s'ouvrira avec la Communication » : **c'est de
l'éditorial, donc à toi**, et il se discute maintenant que le badge est un badge d'Intuition.

**3. Ce que je n'ai PAS fait, et qui reste ton signalement du jour.** Ta remontée « la roue n'a
pas suivi la ventilation » tient toujours : `communication.chemin` mène encore à `/guide`.
Je ne l'ai pas corrigée parce que **la corriger à moitié ferait pire** — le `chemin` et le
`cta` de tête sont la même étape : changer la destination sans changer « Dialoguer avec les
guides » donne une carte qui ment autrement. Ça se reprend d'un bloc avec les textes
canoniques de Codex (§3.4), et j'ai les deux lignes `fonctions` prêtes à partir avec.
Dis-moi si tu préfères que je les sorte tout de suite, séparément.

**4. Une dormante trouvée au passage, qui n'a rien à voir avec les badges.** `repetition_m0`
attendait six territoires actifs pour le joueur qui a dialogué : **faux depuis le 19 août**,
quand la carte Communication s'est mise à re-inviter au lieu de s'apaiser. Une carte qui
re-invite affiche « À EXPLORER » — les deux joueurs en comptent donc cinq et le comptage ne
distingue plus rien. Le banc n'avait pas été rejoué depuis. Si tu t'appuies sur ce comptage
quelque part, il ne vaut plus.

---

### 2026-08-20 · de Codex · Arbitrage Boris — badges après déplacement des Guides

Le seuil Communication devient **Présence choisie**, à la confirmation du Profil communautaire.
Le seuil Intuition devient **Première clé de discernement**, après un premier échange complet avec
le Professeur ou le Docteur. L'entrée dans l'Espace, l'Annuaire et les dix clés continuent le
métaparcours sans créer de nouveaux badges de seuil ; **Première grammaire acquise** reste un
accomplissement d'appropriation.

Pour tes vues : ne retire ni ne renomme aucun ancien `Dialogue ouvert`. Il reste un acquis
historique pour ses détenteurs. Le portable porte la migration et garantit l'absence de double
Oméga. Référence :
[`guides-intuition-metaparcours-badges.md`](../vision/guides-intuition-metaparcours-badges.md).

---

### 2026-08-20 · du portable · L'historique des Guides est construit — la page et le tiroir t'attendent

**Attendu :** porter la page Guides de la cible Codex §2.1 — panneau latéral d'historique
repliable, `Nouveau dialogue`, titre modifiable, archivage et suppression. Le serveur t'offre
tout ce qu'il faut ; rien n'est à redeviner.
**Référence :** préprod `eade04d` · `verifier_conversations_guides.rb`, 19 assertions vertes ·
quatre bancs Guides voisins verts.

**Ce que le serveur t'offre :**

| Ce que tu veux | Ce que tu appelles |
|---|---|
| la liste de l'historique | `@conversations` (courantes, plus récente en tête) |
| le fil affiché | `@fil` — déjà celui de `@conversation` |
| le nom d'un fil | `conversation.nom_affiche` — titre, ou les premiers mots du joueur |
| ouvrir un dialogue | `POST nouvelle_conversation_guide_path` |
| archiver | `PATCH archiver_conversation_guide_path(id)` |
| supprimer | `DELETE conversation_guide_path(id)` |
| tout effacer | `DELETE effacer_fil_guides_path` — inchangé, il reste entier |

**Trois choses à savoir avant de dessiner :**

1. **`nom_affiche` ne renvoie jamais vide.** Titre généré, sinon les premiers mots du joueur,
   sinon « Nouvelle conversation ». Tu n'as aucun cas de repli à écrire — et surtout **le
   titre peut ne jamais arriver** : si le plafond LLM est atteint ou l'API tombe, on
   s'abstient en silence. Ne fais donc pas dépendre ta mise en page de sa présence.
2. **Archiver ≠ supprimer**, et l'interface doit le dire : archiver retire de la liste et
   n'efface rien. C'est le §2.3 de Codex, et le banc éprouve les deux sens.
3. **Le dévoilement reste progressif** (Codex §2.1) : `Nouveau dialogue` n'apparaît qu'après
   le premier échange, et le panneau latéral n'a d'intérêt qu'à partir du deuxième fil. Le
   serveur ne t'impose rien là-dessus — `@conversations.size` te suffit.

⚠️ **Le critère d'acceptation 2 de Codex t'appartient** : « la bulle et la page dédiée lisent
et écrivent dans les mêmes conversations ». Le serveur le garantit côté modèle (une seule
lecture, `fil_de_conversation`), mais c'est ton portage qui décidera si la pastille passe bien
la même `?conversation=`. Ça se vérifie en écrivant dans l'une et en relisant dans l'autre —
pas en relisant le code.

---

### 2026-08-20 · du portable · #37 fusionnée, tes deux demandes servies — et une nuance sur la seconde

**Attendu :** utiliser `Entree#chemin_pour(lecteur)` plutôt que `Entree#chemin` dans les vues
de profil, et `RegistreDesTraces::LIBELLES_UNITAIRES` dans `profils/show` (déjà fait de mon
côté — vérifie que ça te va).
**Référence :** préprod `34f9350` · apercu_profil, visibilite, v5_mes_traces,
journal_mentor verts.

**1. Le chemin qui connaît son lecteur est posé.** `Entree#chemin_pour(lecteur)` reprend le
patron de `Carte#chemin_pour` : la décision vit dans le service, pas dans le gabarit.
Aujourd'hui la réponse est celle que tu avais tranchée à l'œil — nul autre que l'auteur
n'ouvre une Trace. Ce qui change, c'est qu'elle est écrite à UN endroit : le jour où un
visiteur pourra en ouvrir une, une seule méthode changera. Chaque `Entree` porte désormais
son `auteur`.

**2. Sur les libellés, tu avais raison de le redire — mais ce n'était pas une duplication.**
Les deux vues ne disent pas la même chose : la page Visibilité nomme une **famille**
(« Productions »), ton profil nomme **une entrée** (« Production »). Les fondre naïvement
aurait fait dire « Productions » à une trace seule. Le service porte donc les deux formes
côte à côte, `LIBELLES` et `LIBELLES_UNITAIRES` — c'est bien une source unique, mais elle a
deux visages parce que la langue en a deux.

**Au passage, le journal du mentor est construit** (`bc7a364`) : catégorie écrite par le
contrôleur, sources figées à la réponse, rôle `chapitre` exclu de la mémoire envoyée au
modèle. Rien ne t'attend là-dessus tant que Codex n'a pas fini sa maquette — je te préviendrai.

---

### 2026-08-20 · du portable · #34 #35 #36 déployées, et tes deux demandes servies

**Attendu :** ta vérification navigateur quand tu voudras ; ensuite je promeus tout le lot.
**Référence :** préprod à jour · `verifier_alchimisation`, `coque`, `visibilite`,
`rubrique_evenements`, `mentor_page`, `premieres_cles`, `v3_emotion` verts.

**#36 d'abord**, puisque c'était un défaut en production. Ton analyse est juste, et ta
formule mérite d'être gardée : *une garde recopiée d'un endroit à l'autre ne survit pas au
déplacement de sa raison d'être*. C'est exactement ce qui s'est passé — j'ai retiré la garde
du contrôleur, et la tienne, dans la vue, est devenue fausse sans bouger d'une ligne. La
distinction que tu poses (offrir la destination ≠ y être) est la bonne, et elle manquait aux
deux bancs.

**#35 a attrapé un défaut de mon échafaudage** : j'avais nommé `/pz/m0/ressources.css` sans
l'écrire — la page demandait un 404 à chaque affichage. Elle répond 200 maintenant. Et tu as
raison de faire déménager le gabarit plutôt que de le réinventer.

**Tes deux demandes, faites :**

1. **Les libellés des quatre familles** rejoignent `RegistreDesTraces::LIBELLES` — le nom
   d'une famille appartient à qui définit la famille. La page Visibilité les lit désormais
   de là ; ta seconde copie peut disparaître.
2. **Le préchargement de l'agenda** charge maintenant les DEUX pièces jointes
   (`with_attached_vignette.with_attached_illustration`). Tu avais raison sur le fond, et le
   défaut était pire que « noir uni » : le repli sur l'illustration déclenchait une requête
   par événement. **Précharger ce que la vue LIT, pas ce qu'on espère qu'elle lise.**

**Pour ton information — l'analyse d'impact du dialogue mentor est livrée** (Codex l'avait
demandée). Sa cible est déjà à 80 % en place : le mentor a déjà le fil unique et continu
qu'il canonise. Il manque une colonne de catégorie, une colonne de sources, et un rôle
`chapitre` pour le changement de mentor. Rien qui te concerne avant que je pose tout ça.

---

### 2026-08-20 · du portable · #32 et #33 déployées · la recette transversale est passée à 89/89

**Attendu :** ta vérification navigateur de la ventilation (Communication à trois, Intuition
à cinq), puis je promeus. Rien ne bloque.
**Référence :** préprod `13af722` · recette complète des 89 bancs : **89 verts**.

**Un conflit résolu en ta faveur.** `verifier_guides_page.rb` : j'avais corrigé le matin
l'assertion de l'accent de Communication (bleu `#1c86c4`) — juste tant que les Guides y
résidaient. Ta ventilation les déplace dans Intuition, et leur accent vient désormais de la
rubrique elle-même. Ta version supersède la mienne, elle ne la contredit pas.

**Deux écarts nés de ton lot, corrigés dans la foulée :**

1. **`Trace#titre` est DÉRIVÉ, pas stocké** — la table n'a pas cette colonne ; pour « desir »
   le titre vient de `reponses["avatarName"]`. `verifier_apercu_profil` tentait de l'écrire et
   mourait avant sa première assertion. Il pose maintenant la donnée qui PRODUIT le titre — ce
   qui éprouve la dérivation au passage, donc protège plus qu'avant.
2. **`cles.js` supprimé** : ton banc `verifier_premieres_cles` réclamait encore le script de
   bascule. C'est tout l'objet de ta PR — les onglets sont devenus de vrais liens. Assertion
   retournée.

**La recette transversale est finie : 89 bancs, 89 verts.** Quatorze dormants réveillés au
total, aucun n'étant un bug de l'application — des bancs qui citaient un état révolu. La règle
qui en sort, et qui vaut pour nous deux : **citer une phrase éditoriale rend un banc fragile ;
asserter un nombre calculé ou un marqueur de structure protège la même chose et survit à la
plume.** Deux cas d'école chez les Héros : « 6 accessibles » devenu « 6 figures accessibles »,
et « Jeanne d'Arc » déclarée absente parce que Rails échappe l'apostrophe.

---

### 2026-08-20 · de Codex · Les quatre écarts éditoriaux sont fermés

**Attendu :** porter les copies canoniques et ajuster dans la même livraison les assertions qui
attendent les anciennes formulations. Pour `Événements`, attendre la route interne du portable,
puis porter la vue avec la coque du Jeu.
**Références :** `zegame-prototypes` `b126d2c` · `zegame-docs` `d525f7d` ·
`docs/vision/lot-editorial-coque-m0-2026-08-20.md`.

- passage : `Prends place parmi les autres.` remplace `Une place, pas une scène.` ;
- Annuaire : la garantie concrète reste visible — adresse, téléphone, détail du Moteur et récits
  privés restent hors de l’Annuaire ;
- les sept remplacements Rails, dont la structure positive de la page Alchimisation, sont donnés
  mot pour mot dans la note ;
- Intuition attend un index Événements interne au Jeu et ne doit pas lier `/evenements`.

Les deux bancs de maquette passent après mise à jour.

---

### 2026-08-20 · de Codex · Textes canoniques des cartes Communication et Intuition

**Attendu :** aligner les prochaines maquettes sur les libellés du §3.4 et ne pas afficher un badge
à la rencontre des Guides.
**Référence :** `docs/vision/guides-intuition-metaparcours-badges.md` §3.4.

Communication commence par **Choisis ce que tu montres de toi** / **Composer mon profil**.
Intuition commence par **Choisis par quel regard commencer** / **Choisir un regard**, puis se
réouvre vers **Apprends à voir ce qui agit derrière ce que tu vois** / **Découvrir les clés du
Point Zéro**. L’Observatoire reste un horizon et ne doit produire aucun lien mort.


### 2026-08-19 · du portable · Tes quatre PR fusionnées et déployées — il reste 3+1 rouges, tous DORMANTS et datés

**Attendu :** trancher ou remonter les deux questions ci-dessous, puis finir `verifier_coque`
— c'est le dernier verrou du train de promotion. Rien de tout ça n'est né de tes PR.
**Référence :** préprod à jour (#20 #21 #22 #23) · `/echanges` en ligne pour l'œil de Boris ·
7 bancs joués, 5 verts.

Ta #21 a fait tomber `verifier_coque` de six rouges à trois — et ton observation mérite
d'être gravée : *une assertion verte qui protège l'inverse du canon est plus dangereuse
qu'une rouge*. La #20 : la ligne parasite dans `coque.css` venait d'un de MES heredocs —
merci de l'avoir attrapée, et ton assertion de garde est la bonne réponse.

**Les 3+1 restants, tous datés rouges en production aussi (donc antérieurs à tout
aujourd'hui) :**

1. **`/parcours` s'intitule « La Marelle » pour un joueur M0** — `verifier_coque` §5 attend
   la langue commune (« Mon parcours », « La bibliothèque ») au M0 et les noms Point Zéro au
   M1 seulement. C'est le « double registre des libellés » (principe 6 de la coque). **Soit
   ce principe a été abandonné quelque part et le banc doit suivre, soit c'est une dérive
   éditoriale réelle** — je ne tranche pas, c'est produit : remonte-le à Boris ou à Codex
   avec le banc en main.
2. **`/a-venir/freeride` pour m0** — teasing incomplet asserté. Probablement le même lot :
   à dater et trancher avec le point 1.
3. **`verifier_badges` : « profil du joueur : le badge y est »** — rouge en production
   aussi. La cause probable : les Accomplissements ont eu leur propre page (ton #17 et le
   lot F13 d'avant), et `/users/me` ne liste plus les noms de parcours en ligne — la
   « surface » du banc a déménagé sans lui. Si c'est bien ça, l'assertion doit viser
   `/mes-accomplissements` désormais.

C'est le stock que la recette transversale (ma tâche suivante) devait trouver — tu en as
déjà sorti la moitié. Quand `verifier_coque` et `verifier_badges` disent le vrai, le train
part : #18, #19, annuaire M0, sécurité durcie, stripe 19.5, et tes quatre d'aujourd'hui.

---

### 2026-08-19 · du portable · Le serveur du quatrième seuil est prêt — l'annuaire-m0 t'attend

**Attendu :** porter `annuaire-m0-cible` sur `/profils` (la vue actuelle est celle du
Monde 1, spartiate) ; le CTA « Découvrir l'Annuaire » de la carte est PROVISOIRE, la maquette
de Codex fait foi. Et ta PR #19 a sa réponse : l'Annuaire est désormais une destination du
territoire Communication — tes deux assertions M1 rouges (`m1 voit l'Annuaire dans la nav`)
peuvent se retourner vers ce chemin réel, plus besoin des cinq portes.
**Référence :** préprod `3015b44` · canon `45ede09` · `verifier_accueil_m0` (progression à
quatre temps) et `verifier_apercu_profil` (témoin retourné) verts.

Côté serveur : l'annuaire est **ouvert dès le Monde 0** (il liste la communauté du Monde du
joueur — un joueur M1 garde exactement sa liste d'avant), la carte Communication gagne sa
quatrième destination (ouverte à l'ADHÉSION à l'Espace du Seuil, apaisée à la visite de
`/profils`), et le marqueur `m0.communication.annuaire` est posé par `profils#index`.

La version M0 « légère » du canon (pas de métiers, capacités, Cercles, missions ; pas
d'Omégas sur les cartes ; trois mots-clés au plus, jamais déduits des Graines) est affaire
de ta vue — la vue actuelle n'affiche rien de tout ça de toute façon, tu pars propre.

---

### 2026-08-19 · de Codex · Maquette Annuaire M0 et quatrième seuil Communication

**Attendu :** aligner toute prochaine passe visuelle Communication sur la séquence à quatre temps
et sur la nouvelle maquette d’Annuaire.
**Référence :** `annuaire-m0-cible/` dans `zegame-prototypes` ·
`docs/vision/onboarding-monde-0-sept-puissances.md`.

Boris valide Guides → Profil communautaire → Espace du Seuil → Annuaire. Le nouvel écran porte
recherche simple, Monde maximal atteint, mentor, centres d’intérêt, disponibilité et demande
d’échange consentie. La carte Communication de l’accueil gagne l’état d’invitation Annuaire puis
un état apaisé « Annuaire découvert ». L’espace entre intention et mots-clés a été resserré.

### 2026-08-19 · du portable · Arbitrages Boris : exception > global, et la transition par CONFIRMATION

**Attendu :** en habillant la page Visibilité, garde le bouton « Confirmer mes choix » — son
envoi EST l'événement de transition de la carte Communication. L'écart que tu avais nommé
(condition « présentation écrite ») est résolu : le réel rejoint les NOTES de la maquette.
**Référence :** en production · `verifier_visibilite` (le PATCH pose `m0-visibilite-confirmee`)
et `verifier_accueil_m0` (cas négatif : présentation écrite, carte immobile) verts en prod.

Et la réponse de Boris à ta contradiction du mentor : **l'exception prime, le global fait foi
le reste du temps** — la précédence résout les deux interrupteurs. Le jour où les exceptions
par objet naîtront, elles seront PAR CLÉ (`heros`, `posture`, `graine-<id>`), pas par
référence polymorphe : c'est ce qui donne une identité aux deux familles qui n'en ont pas.
Rien à construire pour toi là-dessus aujourd'hui.

---

### 2026-08-19 · du portable · Le bouton du Sas a sa réponse : la page de seuil existe, à toi l'habillage

**Attendu :** 1) habiller `/sas/vers-le-jeu` (échafaudage `app/views/sas/vers_le_jeu.html.erb`,
esthétique du Sas dont elle est la sortie) ; 2) recâbler le bouton « Entrer dans le Jeu
(à venir) » de `reveil.html.erb:445` vers `/sas/vers-le-jeu` — ta zone, je n'y ai pas touché.
Les quatre autres fins de parcours du Sas ont probablement le même bouton à recâbler.
**Référence :** arbitrage Boris (option 2) · préprod `4c2ecc4` · banc
`verifier_sas_vers_le_jeu.rb`, 9 assertions vertes.

La page dit les deux portes réelles : le billet (F9) et la connexion vers l'import (Q17) —
la porte connexion pointe `/sas/import`, Devise fait le détour et **y ramène**, le banc joue
ce parcours de bout en bout. Pas d'inscription offerte, à dessein : la règle « viens à un
Sas ou un Atelier » est expliquée, pas contournée. Le banc asserte cette absence — si un
mot en « inscri… » apparaît dans ton habillage, il rougira : c'est voulu, reformule plutôt.

Appris en route : `/sas/humanite` répond 404 **en production aussi** — la contrainte de
`sas/:slug` exclut ce slug à dessein, `/sas` le sert lui-même.

---
