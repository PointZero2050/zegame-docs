# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du poste fixe · ⚠️ Ta matrice visuelle n'a JAMAIS rien changé à l'écran

`config/monde_0.yml` porte depuis le 16 août ta règle : « une carte change d'image UNIQUEMENT
quand son CTA révèle un territoire durable ». Le mécanisme existe, il est lu, il vient même
d'être ÉTENDU par le portable — `titre` et `accroche` suivent désormais l'étape, comme `cta` et
`chemin`.

**Mais les images de destination n'ont jamais existé.** Mesuré sur la préprod, accueil du
Monde 0 : les sept cartes servent leur image de Puissance, **zéro illustration de destination**.

Quatre fichiers sont déclarés dans la config et absents partout — pas dans le dépôt, pas dans
`zegame-prototypes/accueil-puissances-m0-cible/assets/powers/`, pas dans le dossier de travail :

| Déclaré | Pour quelle étape |
|---|---|
| `communication-profil.webp` | « Choisis ce que tu montres de toi » |
| `communication-echanges.webp` | « Entre dans l'Espace d'échange » |
| `communication-annuaire.webp` | « Découvre qui joue déjà » |
| `traces.webp` | la bascule Fresque → Traces (Imagination) |

Le repli fonctionne (`image_servie` ne rend un nom que si l'asset est là, et la carte retombe
sur l'image de la Puissance) : **rien n'est cassé, et c'est bien le problème.** Un mécanisme qui
se dégrade proprement ne signale jamais qu'il tourne à vide. Il a cinq jours.

**Ce n'est pas ma zone au sens où je ne fabrique pas d'images** — je peux les poser dans
`public/pz/m0/powers/` le jour où elles existent, c'est tout ce que le portage demande. Le
format est celui des sept autres : `.webp`, même cadrage.

**Deux sorties, et c'est ton arbitrage avec Boris :** ou les quatre illustrations se produisent
et la matrice se met enfin à parler ; ou la règle tombe et la carte garde l'image de sa
Puissance à toutes les étapes — auquel cas les quatre lignes `image:` de la config devraient
partir, sinon la prochaine session les relira comme une promesse.

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
