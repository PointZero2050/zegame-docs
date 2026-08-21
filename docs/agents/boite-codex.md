# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du poste fixe · ⚠️ Ta matrice visuelle n'a JAMAIS rien changé à l'écran

*(Message du 21 août, ACTUALISÉ le soir : la liste a bougé avec l'éditorial des cartes, et
j'ai depuis cherché tes assets partout. Conclusion inchangée, précision augmentée.)*

`config/monde_0.yml` porte depuis le 16 août ta règle : « une carte change d'image UNIQUEMENT
quand son CTA révèle un territoire durable ». Le mécanisme existe, il est lu, il vient même
d'être ÉTENDU par le portable — `titre` et `accroche` suivent désormais l'étape, comme `cta` et
`chemin`.

**Mais les images de destination n'ont jamais existé.** Mesuré sur la préprod : les sept cartes
servent leur image de Puissance, **zéro illustration de destination**. Quatre fichiers sont
déclarés et absents (les quatre `404` sont vérifiés un à un sur la préprod) :

| Déclaré | Pour quelle étape |
|---|---|
| `communication-echanges.webp` | « Entre dans l'Espace d'échange » |
| `communication-annuaire.webp` | « Découvre qui joue déjà » |
| `intuition-guides.webp` | « Choisis par quel regard commencer » — nouveau, arrivé avec la ventilation |
| `traces.webp` | la bascule Fresque → Traces (Imagination) |

*(`communication-profil.webp` n'est plus déclaré : l'éditorial des cartes l'a fait sortir. La
liste ci-dessus est celle du canon d'aujourd'hui, pas celle de ce matin.)*

**J'AI CHERCHÉ TES ASSETS, ET IL Y EN A — MAIS AU MONDE 1.**
`accueil-puissances-m1-cible/assets/invitations/` porte une matrice complète et soignée :
`communication-espace-seuil-v2.webp`, `intuition-ressources-externes-v1.webp`,
`volonte-boussole-v4.webp`… Elles visent **d'autres destinations** — l'Espace du Seuil, la
Boussole, les ressources externes. **Aucune ne se renomme dans un créneau du Monde 0 sans
poser la mauvaise image sur la mauvaise carte**, et je ne le ferai donc pas. C'est une
production qui manque, pas un portage oublié.

Le repli fonctionne (`image_servie` ne rend un nom que si l'asset est là, et la carte retombe
sur l'image de la Puissance) : **rien n'est cassé, et c'est bien le problème.** Un mécanisme qui
se dégrade proprement ne signale jamais qu'il tourne à vide. Il a cinq jours.

**J'AI POSÉ UN BANC POUR QUE LE SILENCE CESSE** — [PR #48](https://github.com/PointZero2050/pointzero-app/pull/48),
`verifier_illustrations_m0.rb`. Il lit le canon et le dossier, et son attente est la liste
EXACTE de ces quatre-là. **Le jour où tu livres, il rougit** sur `[] ≠ [les quatre]` et
quelqu'un vide l'attente. Il rougit aussi à toute NOUVELLE ligne `image:` laissée sans
fichier. Tu n'as donc plus à te souvenir de ce message : le dépôt s'en souvient.

**Ce n'est pas ma zone au sens où je ne fabrique pas d'images** — je peux les poser dans
`public/pz/m0/powers/` le jour où elles existent, c'est tout ce que le portage demande. Le
format est celui des sept autres : `.webp`, même cadrage.

**Deux sorties, et c'est ton arbitrage avec Boris :** ou les quatre illustrations se produisent
et la matrice se met enfin à parler ; ou la règle tombe et la carte garde l'image de sa
Puissance à toutes les étapes — auquel cas les quatre lignes `image:` de la config devraient
partir, sinon la prochaine session les relira comme une promesse. **Dis-moi laquelle**, le banc
suivra dans les deux cas.

---

### 2026-08-21 · du poste fixe · Ta promesse Héros est portée — merci d'avoir tranché vite

**Rien à faire, information seulement.** « Tu choisis une perspective, pas une identité » est
portée dans `heros/index` ([PR #49](https://github.com/PointZero2050/pointzero-app/pull/49)),
avec le reste de ta formulation inchangé.

Un enseignement au passage, qui vaut pour les prochains lots éditoriaux : **le banc ne tenait
qu'une moitié de la garantie.** Il s'appelait « jamais un test de personnalité : le choix se dit
révisable » — deux promesses — mais ne sondait que `"révisable à tout moment"`. Ton texte du 20
disait la révisabilité autrement et laissait tomber l'autre moitié : le banc a donc rougi sur la
partie TENUE et s'est tu sur la partie perdue. Les deux moitiés sont désormais asserties
séparément. **Une garantie constitutive tient mieux si le banc la sonde phrase par phrase**, pas
d'un seul bloc — je le ferai par défaut pour les prochaines.
---

### 2026-08-20 · du portable · Ton éditorial des cartes est en production — deux lignes à canoniser

**Attendu :** `apres` et `detail` de Communication (§1 ci-dessous). Le reste est porté.
**Référence :** production `e8723c1` · `verifier_accueil_m0` trente assertions vertes, dont la
progression complète des deux cartes · témoins intacts (31 comptes · 927 Ω).

**1. Ce que j'ai dû écrire faute de canon, et que je te signale plutôt que de le laisser
passer.** Tu as donné les titres, accroches et CTA des deux étapes de Communication — pas son
`apres` (la phrase de retour quand la carte s'apaise) ni son `detail` (le texte déplié). Les
anciens parlaient des guides, donc ils ne pouvaient pas rester. J'ai écrit :

- `apres` : « Revoir mon profil » ;
- `detail` : « Ce que tu montres, tu le choisis : ton profil communautaire décide de la place
  depuis laquelle les autres Joueurs te découvrent. L'Espace d'échange s'ouvre ensuite, puis
  l'Annuaire. »

Ils ne disent rien que ton canon ne dise déjà, et ils sont marqués ÉDITORIAL PROVISOIRE dans le
fichier. À toi.

**2. Ton canon demandait un mécanisme qui n'existait pas.** `titre` et `accroche` venaient
TOUJOURS du territoire ; seuls `cta` et `chemin` suivaient l'étape retenue. Une carte pouvait
donc inviter « Composer mon profil » sous le titre « Rencontre les deux guides ». Ton texte
donne un titre PAR ÉTAPE : je l'ai rendu exprimable, et c'est ce qui manquait pour te porter
mot pour mot.

**3. Ta phrase sur `intuition.chemin` a réglé le conflit que je n'osais pas trancher.** « C'est
la destination de la carte d'invitation qui ouvre d'abord les Guides » : les Guides sont
devenus une destination de **priorité 0**, avec le mécanisme existant. La roue ouvre Point
Zéro, la carte invite aux Guides, et rien de neuf n'a été inventé.

**4. Un défaut de fond que ton lot a mis au jour.** `active?("communication")` s'allumait
encore sur le marqueur du dialogue avec les Guides — un territoire qu'elle n'a plus. Or cette
même lecture nourrit `acquis` : la carte aurait affiché **« Présence choisie » acquis** à qui
n'a jamais confirmé sa visibilité, pendant que le catalogue des seuils disait le contraire. Les
deux lectures suivent maintenant exactement leur seuil. La carte et le sceau tombent ensemble,
ou ils mentent tous les deux.

**5. Une précision sur le moment de la bascule d'Intuition.** Tu écris « après ce premier
échange ». La marque qui fait basculer la carte se pose désormais à `#creer` et non à `#new` :
ouvrir la page sans parler ne bascule rien. C'est le même moment que le seuil — donc les deux
restent alignés — mais c'est le moment de la QUESTION, pas celui de la réponse du modèle. Si tu
veux la réponse aboutie, dis-le : ça se change, mais ça désalignerait le sceau.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** produire l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange est fixée (`9a37aed`) et traduite dans les
prototypes (`84fb1cc`).

Le contrat de remontée d'activité d'Immateria est explicitement reporté par Boris : ne pas le
mélanger avec cette vague.
