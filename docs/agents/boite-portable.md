# Boîte du portable

### 2026-09-30 (nuit) · du poste fixe · 📣 PR #369 — les pages du lien magique n'avaient AUCUNE mise en forme

Boris, après que tu as ouvert l'accès : « les pages de magiclink n'ont pas de mise en forme ». Il a
raison, et c'était pire que ça : `reclamer` (la page du jeton, celle que le courriel ouvre) n'avait
**aucune classe**, et `confirme` en portait cinq depuis août que **rien ne dessinait** —
`billet-confirme`, `billet-recap`, `billet-suite`, `primary-button`, `secondary-button`.

**https://github.com/PointZero2050/pointzero-app/pull/369** · branche
`billet-sous-la-coque-festival`, partie de `main`, un commit, sept fichiers : cinq vues,
`public/site/billet.css` et un banc. **Indépendante de #367 et #368.**

## ⚠️ CE QUI TE CONCERNE : je n'ai PAS changé la coque, et c'est délibéré

Ces pages restent sous **`layout "site"`**. J'ai été tenté de les basculer sous `layout "evenement"`
pour la continuité visuelle — c'est un piège : la coque de l'appli porte quatre onglets vers
`/festival/*`, qui exigent tous une session, et la personne qui ouvre un lien magique **n'a par
définition pas encore de compte**. Un rail dont chaque destination refuse l'entrée est pire qu'une
page sobre. Le § 5 du banc garde ce choix — si quelqu'un bascule la coque un jour, il rougira.

Le dessin vient donc d'une feuille dédiée qui **porte** les valeurs de `festival.css` et
`evenement.css` sans les charger. ⚠️ Charger `evenement.css` ici décalerait l'en-tête et le pied du
SITE : elle redéfinit `:root`, et les couleurs du site vivent dans `tokens.css`.

## Un détail qui vaut pour toi aussi

Les tailles de cette feuille neuve suivent **déjà le plancher de #368** (corps 15/16, étiquettes
jamais sous 11). Recopier les 9 et 10 px de la maquette aurait recréé, sur une page neuve, le défaut
qu'on venait de corriger sur toutes les autres. Et le champ de saisie est à **16 px** : en dessous,
un navigateur mobile zoome à la mise au point — la page saute au moment où l'on tape son mot de
passe.

## ⚠️ Non éprouvé chez moi

Rien n'a été rendu par Rails. Les six gabarits compilent, le banc passe `ruby -c`, et seule la
branche « créer ton compte » a été rendue hors Rails. **Les quatre autres branches de `reclamer`
— billet déjà rattaché, rattaché à un autre compte, compte existant, déjà connecté — se regardent à
ton déploiement.** C'est la page la plus branchue du lot.


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

