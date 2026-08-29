# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

### Différé après la clôture du Monde 0 · du poste fixe · Échanges Monde 1

Rappel conservé sans action immédiate : reprendre ce chantier seulement après le signal de
clôture du Monde 0 par Boris.

---

## 29 août · du poste fixe — l'UX chapitre est portée, trois points te reviennent

`zegame-prototypes@6c6c884` est intégré dans `pointzero-app` (PR #116, commit `51e922e`) :
structure DOM, noms de classes et valeurs portés à la lettre, feuille
`public/pz/m0/chapitre.css` scopée sous `.pz-m0-chapitre`. Les deux seuils (900 et 620) y
sont, la coque de la maquette n'est pas reportée (l'application a la sienne, et
`.territory-nav` vit dans `coque.css` — le banc de la marelle garde qu'elle n'y soit pas
redéclarée).

**Trois éléments de ton contrat ne peuvent pas être remplis aujourd'hui**, et j'ai préféré
les laisser vides plutôt que les figer — ta consigne le dit : « brancher les données du
portable, ne pas les figer dans la vue ».

1. **Les trois Puissances dominantes avec leur verbe.** Cette donnée n'existe nulle part :
   ni sur le Challenge, ni dans `chapitres:` de `config/journeys/point-zero-monde-0.yml`,
   ni dans la structure `Chapitre`. Le bloc est écrit, commenté, et attend son champ.
   Peux-tu poser `puissances: [{id, verbe}]` par chapitre dans le canon ?

2. **La question d'entrée** (« Dans quel jeu joues-tu ? »). Le YAML ne connaît que
   `mouvement` et `fil`. `fil` occupe la même place — une ligne courte sous le titre — et
   c'est lui qui est branché faute de mieux : pour le chapitre 1 cela donne « Crises,
   récits, Moteur, futurs et Appel. », qui n'est pas une question. Un champ `question:`
   par chapitre réglerait cela.

3. **Le titre porte un suffixe que ta maquette ne montre pas.** Tu écris « Franchir le
   seuil » ; la donnée dit « Franchir le seuil — Je pressens ». Je rends la chaîne ENTIÈRE :
   la couper serait ré-éditorialiser un texte dont tu es l'auteur. Dis-moi si le geste doit
   partir du titre (et aller où ?) ou si le titre doit rester complet.

⚠️ **Et une question de forme, mesurée.** `.experience-path` est en `repeat(5, 1fr)`. Les
trois chapitres du Monde 0 portent **cinq, quatre et cinq** expériences : au chapitre 2, la
cinquième colonne restera vide et la ligne de liaison, calculée en pourcentages, dépassera
le dernier médaillon. J'ai porté ta valeur telle quelle — c'est à toi de dire si un chapitre
plus court garde cinq colonnes ou en compte autant qu'il a.

---

## 29 août · du poste fixe — menu Actions M1 porté : trois entrées sur cinq

`zegame-prototypes@5390b18` est intégré ([PR #118](https://github.com/PointZero2050/pointzero-app/pull/118)) :
en-tête, deux groupes, lignes à glyphe/titre/sous-titre/chevron, popover puis panneau bas
sous 720 px. M0 ne change pas.

**Ta règle appliquée à la lettre** — « une entrée sans route, service, droits négatifs et banc
reste absente, jamais grisée ». Audit des cinq gestes :

| geste | route | service | banc | verdict |
|---|---|---|---|---|
| sondage, rencontre, ressource | ✓ | ✓ | ✓ | présents |
| **élément de Récit** | ✗ | ✓ | ✓ | *absent* |
| **Mouvement** | ✗ | ✗ | ✗ | *absent* |

⚠️ **Tu écris « le partage de Récit peut appeler la couche déjà livrée ».** Elle l'est
vraiment — `PartagesDeRecit` porte `apercu` (l'aperçu des futurs lecteurs que tu demandes) ET
`partager!`, avec son banc. Mais **aucune route ne les appelle**. Le geste est à une route
d'exister ; c'est demandé au portable. Dès qu'elle est là, l'entrée s'ajoute sans toucher à la
forme.

⚠️ **Un écart de texte, que je te rends plutôt que de le trancher seul.** Ton sous-titre de la
ressource dit « Joindre un fichier **ou préparer l'aperçu d'un lien** ». Chez nous l'aperçu
d'un lien n'est pas un geste : il se fabrique tout seul quand un lien part dans le texte
(`ApercuDeLienJob`). J'ai gardé ton titre et raccourci le sous-titre à « Joindre un fichier au
fil » — promettre la seconde moitié aurait été un libellé qui ment. Dis-moi si tu préfères une
autre formule.
