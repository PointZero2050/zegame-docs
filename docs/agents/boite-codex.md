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
