# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

*(vide — les quatre messages du 21 août et les seize du 19-20 août sont traités.)*

## Ce que le 21 août a réglé, dans l'ordre

- *Portable, ⚠️ une PROMESSE a disparu de la page des Héros* → **#49, en production**. Son
  refus de rendre le banc vert a révélé mieux que le défaut : l'assertion annonçait DEUX
  promesses et n'en sondait qu'une, si bien qu'elle rougissait sur la moitié tenue et se
  taisait sur la moitié perdue. Codex a rendu la phrase, les deux moitiés sont asserties
  séparément.
- *Défaut trouvé au navigateur, pas au calcul* → **#47, en production** : créer un dialogue
  faisait disparaître tout l'historique. Vérifiée depuis sur les deux serveurs.
- *Portable, ⚠️ mon banc neuf ÉCRASAIT `verifier_illustrations_m0.rb`* → attrapé par lui à la
  relecture, 25 assertions sauvées. **#48 fermée, remplacée par #50** branchée après sa
  correction. Leçon consignée : `ls scripts/ | grep <thème>` avant d'écrire — un banc supprimé
  ne casse rien, il se tait.
- *Codex, les quatre assets M0* → **#50** : posés dans `public/pz/m0/powers/`, 640×960 lossy
  comme les sept autres, et le rendez-vous du banc repart VIDE. 11 déclarées, 11 présentes.
- *Codex, indigo d'Intuition* → rien à faire, `coque.css:287` le déclarait déjà.
- *Boris, budget Actions à 0 $* → relevé ; **la CI est verte pour la première fois**, les cinq
  travaux compris. Le blocage de facturation masquait un `db:test:prepare` qui réclamait un
  `db/schema.rb` que le projet a décidé de ne pas avoir ; le portable a porté le correctif.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui | Où |
|---|---|---|
| #50 à fusionner, déployer — **build PUIS restart** (asset mémoïsé) | **portable** | boîte du portable |
| Vérification navigateur qu'une carte montre enfin sa destination | **moi**, dès le déploiement | — |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) | non reproductible au navigateur de bureau |
