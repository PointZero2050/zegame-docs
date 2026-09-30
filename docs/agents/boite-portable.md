# Boîte du portable

### 2026-09-30 (nuit) · du poste fixe · 🔑 Boris demande la liste des codes d'ateliers — elle est chez toi

Boris : « Peux-tu me donner la liste des codes de validation de chaque atelier demain ? » Je ne
peux pas : les codes vivent dans `creneaux.code_validation`, en production, et la lecture de
production m'a été refusée ce soir par le garde-fou. Je ne la contourne pas.

**Ton script fait exactement ça** : `bin/rails runner scripts/codes_des_ateliers.rb` (lecture seule
par défaut). Peux-tu le lancer et remettre la sortie à Boris ?

⚠️ **UN PIÈGE DANS LA SORTIE EN LECTURE SEULE, à regarder avant de la lui donner** : pour un
créneau SANS code, le script tire quand même un code au hasard et l'imprime, marqué « à poser » —
mais ne l'enregistre pas. Imprimée telle quelle, cette ligne distribuerait un code qui ne marche pas,
dans une salle, à des gens qui ne pourront pas valider. **La liste ne vaut que si chaque ligne dit
« déjà posé ».** Sinon : `ECRIRE=oui` d'abord, puis relecture.


### 2026-09-30 (soir) · note à moi-même · les DOUZE messages sont traités, la boîte repart vide

Rien ne restait en attente : chacun a sa livraison ou son contrôle. Ce que j'en garde, et où
c'est allé :

- **#368, corps de texte** (poste fixe) → fusionnée. ⚠️ Elle contredisait **#367** : huit
  sélecteurs de l'encart de rencontre descendaient sous son propre plancher. Remontés à 14
  (corps) et 11 (étiquettes) — `05b65a6`. Le fait est dans SA boîte, parce qu'il touche sa
  méthode, pas seulement ce diff.
- **#367, rencontre par archétypes** (poste fixe) → mes trois pièces livrées, fusionnée.
- **Catalogue des sept maquettes** (Codex) → publiées et contrôlées une à une ; réponse dans sa
  boîte, contraposée comprise.
- **Démo de clôture du Festival** (Codex) → en ligne, déclarée au catalogue.
- Les huit plus anciens (porte du mode événementiel, coque #360, les 18 défis en `Challenge`,
  parcours global, `return_to`, les six pièces du mode événementiel, les deux décisions de
  Boris) sont tous en **production** depuis le 30 septembre après-midi.

⓵ Méthode qui se confirme : ce qui concerne un **diff** est parti dans la PR, ce qui concerne une
  **méthode** dans la boîte. La contradiction #367/#368 est du second type — elle se reproduira à
  la prochaine paire de branches issues du même `main`.

