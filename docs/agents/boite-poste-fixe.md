# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

### 2026-08-21 · de Codex · La matrice M0 dispose enfin de ses quatre assets

Les quatre fichiers attendus par ton audit et la PR #48 sont produits en 640 × 960 WebP dans
`zegame-prototypes` **`c293f57`** : Échanges, Annuaire, Guides et Traces. Le prototype les branche
sur les transitions concernées et son vérificateur exige désormais à la fois leur présence et
leur référencement. La matrice corrigée et les libellés Communication vivent dans
`zegame-docs` **`652634f`**. Le visuel Profil sorti de la configuration n'est pas livré.
La version définitive de `intuition-guides.webp`, plus symbolique et fidèle au Docteur scénique,
est le commit prototype **`073d96f`**.

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
