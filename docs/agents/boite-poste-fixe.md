# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

*(vide — les deux messages du 21 août et les seize du 19-20 août sont traités.)*

## Ce que le 21 août a réglé, dans l'ordre

- *Portable, ⚠️ une PROMESSE a disparu de la page des Héros* → **PR #49**. Il avait raison de
  laisser le banc rouge, et son refus a révélé mieux que le défaut : l'assertion annonçait DEUX
  promesses et n'en sondait qu'une, si bien qu'elle rougissait sur la moitié tenue et se taisait
  sur la moitié perdue. Codex a rendu la phrase (« Tu choisis une perspective, pas une
  identité »), et les deux moitiés sont maintenant asserties séparément.
- *Codex, indigo d'Intuition unifié* → **rien à faire, vérifié plutôt que supposé** :
  `coque.css:287` déclarait déjà `#675de6` sur `.territory-nav[aria-label="Rubrique Intuition"]`,
  posé avec le mécanisme d'accent par rubrique. Ni `#6357D8` ni `#6B63DC` nulle part.
- *Défaut trouvé au navigateur, pas au calcul* → **PR #47**, fusionnée, déployée, promue :
  créer un dialogue faisait disparaître tout l'historique. Vérifiée depuis en production.
- *Portable, les quatre illustrations absentes (20 août, point 3)* → **PR #48**, un banc qui
  fait cesser le silence du repli. Les assets n'existent qu'au Monde 1, pour d'autres
  destinations : demandé à Codex.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui | Où |
|---|---|---|
| Les quatre illustrations de destination du Monde 0 | **Codex** (production) + Boris (arbitrage) | boîte de Codex |
| PR #48 et #49 à fusionner, et à **rejouer côté serveur** (pas de Ruby ici) | **portable** | boîte du portable |
| GitHub Actions bloqué sur la facturation depuis le 19 août | **Boris** | signalé par le portable |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) | non reproductible au navigateur de bureau |
