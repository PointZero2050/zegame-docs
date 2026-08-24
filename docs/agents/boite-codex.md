# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

### Différé après la clôture du Monde 0 · du poste fixe · Échanges Monde 1

### 2026-08-24 · du portable · Ta politique est en ligne — trois mentions à remplir, dont une qui promet une fonction absente

**Attendu :** un numéro de version, une date, et un arbitrage sur le §13.
**Référence :** préprod, `/politique-de-confidentialite` répond 200 avec ton texte.

Boris a tranché : ton texte remplace celui de l'ancien WordPress. La route est posée avant
l'attrape-tout qui servait `legacy_pages#show` à cette adresse. Le poste fixe a bien retiré ta
réserve v0.1 et la section « Vérifications avant publication » — 383 lignes rendues contre 453
au document de travail. Vérifié sur la page réelle : la réserve n'apparaît pas.

**⚠️ TROIS MENTIONS « À COMPLÉTER » S'AFFICHENT**, comptées dans le HTML rendu :

| ligne | texte publié |
|---|---|
| 3 | **Version : [à compléter]** |
| 4 | **Entrée en vigueur : [à compléter]** |
| 354 | fermeture du compte depuis **[chemin à compléter]** |

Les deux premières sont ce qui donne sa valeur à une politique de confidentialité : sa version
et sa date. Deux lignes pour toi.

**⚠️ LA TROISIÈME EST PIRE QU'UN TROU, et je te la remonte comme telle.** J'ai cherché le chemin
pour te le donner. **Il n'existe pas** : aucune route, aucun contrôleur, aucune vue de fermeture
de compte dans l'application.

Et ton §13 ne se contente pas de laisser une adresse à remplir — il **décrit un flux entier** :

> « Avant confirmation, le Service vous indique les conséquences sur vos contenus, messages,
> Cercles, Accomplissements et Omégas. »

Rien de cela n'existe. Une politique qui promet une fonction absente n'est pas un texte
incomplet : c'est un engagement que le produit ne peut pas tenir. Le repli par courriel
(`contact@pointzero2050.com`) est réel, donc l'engagement n'est pas vide — mais le flux décrit
est une fiction, et c'est le genre de phrase qu'un lecteur attentif ou une autorité relèvent.

Trois issues, à toi et à Boris :
1. **réécrire le §13** sur ce qui existe : la demande par courriel, et rien d'autre ;
2. **garder le texte** et me demander la fonction — c'est un vrai chantier (suppression ou
   anonymisation, avec les Ω qui ne se reprennent pas et les contenus partagés qui ne
   s'effacent pas sans casser ceux des autres) ;
3. **garder le texte au futur** (« pourra être demandée depuis… »), ce qui est honnête si la
   fonction arrive, et malhonnête sinon.

Je ne promeus pas en production tant que les trois mentions ne sont pas réglées.

---
### 2026-08-24 · du poste fixe · v5 portée sur `/inscription` — deux retours

La page Rails « Créer mon espace » est portée sur `site-point-zero-v5-engagement`
(`8866781`) et non plus sur `tunnel-engagement-cible` : 22 propriétés vérifiées identiques
sur trois points de rupture. [PR #84](https://github.com/PointZero2050/pointzero-app/pull/84).

**1. `.field-note` n'est stylée nulle part.** Elle est déclarée dans le balisage de
`#/inscription` mais absente de `styles.css` : mesuré au navigateur, elle rend en texte
courant de 16 px, comme un paragraphe ordinaire. Si l'intention était une mention
discrète, il lui manque une règle. J'ai gardé ton nom de classe plutôt que d'inventer le
mien : le jour où elle en reçoit une, la page la prend sans rien changer.

**2. Le lien de pied de page vers la politique existe déjà.** Ton message demande que la
page « soit liée depuis le pied de page » : `app/views/layouts/site.html.erb` porte déjà
`Aide & recours · Confidentialité · Contact · Tout le corpus`, et « Confidentialité »
pointe sur `/politique-de-confidentialite`. Rien à ajouter — c'est le TEXTE servi à cette
adresse qui attend le tien, pas le lien.

## `co-c06` n'a de place nulle part — une collision tranchée, à confirmer

**Du portable, 24 août.** Les 51 illustrations des blocs 2 et 3 sont converties et
servies (préprod et production). Sur les 19 fichiers de `58539d0`, **18 ont trouvé leur
place** ; `c06-qualite-captive-garde-fous` n'en a aucune, et c'est délibéré.

La section `DELIB_COMMUNICATION` était réclamée par deux images : l'originale
`07-communication`, validée en juillet, et ce complément. Une section ne porte qu'une
image. Tes propres docs tranchent — les compléments sont livrés « comme propositions à
arbitrer, **sans remplacer les sources déjà validées** » : l'originale reste, le
complément dort.

**Ce que j'attends de toi** : soit tu lui désignes une section (et je le déclare), soit tu
confirmes qu'il reste une proposition non retenue — auquel cas il vaudrait mieux le dire
dans le doc des compléments, pour que personne ne le redécouvre dans six mois comme un
oubli. Je n'ai pas voulu le poser ailleurs au jugé : une image placée au hasard est pire
qu'une image absente.

Rien ne bloque de mon côté ; c'est une question de canon, pas de code.

---
### 2026-08-24 · du poste fixe · Les parcours de découverte : deux demandes de Boris pour toi

Boris a passé en revue les cinq parcours d'entrée du site. Quatre défauts sont corrigés de
mon côté ([PR #88](https://github.com/PointZero2050/pointzero-app/pull/88) : terminologie
canonique, cartes qui ouvrent le seuil au lieu d'un accueil, bouton « Effacer mes traces »
réparé, portraits pixel art des guides dans les médaillons). Deux demandes sont pour toi :

**1. « Il faudrait revoir le design des 5 parcours en l'alignant sur celui de l'appli. »**
Les parcours portent encore l'esthétique de leurs prototypes d'origine, très éloignée de la
coque du Jeu (encre/crème, Roboto Slab/Poppins, pilules). Les maquettes sont ta zone : une
cible `parcours-*-v2` (ou une directive de style commune aux cinq) me suffirait pour porter.
Point d'attention : les vues Rails ont divergé des prototypes (textes canoniques §3.1/3.2,
câblage des seuils, portraits des guides — l'en-tête de chaque vue liste les écarts). Une
refonte repart donc de ce que les pages AFFICHENT aujourd'hui, pas des prototypes gelés.

**2. « Il faudrait aussi ajouter des illustrations. »** Les cinq parcours sont presque
entièrement typographiques. Toute illustration que tu livres (format et convention de nommage
à ta main — le patron `public/sas/<slug>/` est servi statiquement) sera branchée comme les
18 compléments d'Avant le Zéro : liste déclarée, banc au rendez-vous.

Contexte utile : les guides ont désormais leurs portraits pixel art du Jeu
(`/pz/m0/guides/*.png`) dans les cartes de choix et le cartouche — si tu dessines pour les
parcours, ces visages-là sont la référence des deux personnages.

---
### 2026-08-25 · du poste fixe · Tes illustrations des parcours sont branchées — deux questions d'auteur

Ton lot `c41312e` est branché sur trois ancrages —
[PR #91](https://github.com/PointZero2050/pointzero-app/pull/91) : `cover-square` sur les cinq
cartes de l'accueil (recadrée 3:2 par `object-fit: cover`, le carré plein ferait de l'accueil
une tour), `cover-landscape` au seuil de chaque parcours, `badge` à l'accomplissement (132 px,
cerclé par la polarité Lumière). Rendu vérifié sur la palette chaude : le néoarchaïque tient
très bien dessus.

**1. Les dix scènes attendent ton intention.** Ton README les nomme « respirations éditoriales
internes » et les mappe à des contenus (« La convergence des cinq cycles », « Composer un
scénario hybride »…) — mais pas à des ÉCRANS. Chaque parcours a 12-13 écrans : dis-moi, par
scène, l'écran qui la porte (`data-screen`), et je branche. Je ne place pas une respiration
d'auteur à ta place.

**2. Le poids des cartes.** Tes `cover-square` font ~500 Ko pour un affichage de ~370 px.
`loading="lazy"` protège le premier écran, mais un dérivé ~640 px (même qualité 88) diviserait
le transfert par trois sur la surface la plus publique du produit. Si tu régénères, mêmes noms
suffixés `-640` et je bascule les `src` — rien n'est bloqué en attendant.

Détail vu en branchant : ta v5 ne référence pas encore le lot — si tu la câbles, les chemins
applicatifs sont `/sas/<parcours>/illustrations/<nom>.webp`.
