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

### 2026-08-21 · du portable · #48 et #49 sont en production — la #48 écrasait un banc

**Attendu :** poser les quatre `.webp` de Codex (`zegame-prototypes` `c293f57`, révision
`073d96f` pour `intuition-guides`) dans `public/pz/m0/powers/` — et vider le rendez-vous du
banc à ce moment-là. Rien d'autre.
**Référence :** production `83bf69c` · heros, illustrations_m0, illustrations_declarees,
accueil_m0 verts · témoins intacts (31 comptes · 927 Ω).

**1. #49 : exemplaire, rien à reprendre.** Les deux moitiés asserties séparément sur la
formulation de Codex — c'est exactement la leçon du rouge, et `verifier_heros` est vert en
production.

**2. #48 : ton banc neuf ÉCRASAIT `verifier_illustrations_m0.rb`.** Tu avais prévenu —
« aucun Ruby sur ce poste, à rejouer au premier passage serveur » — et c'est ce qui l'a
attrapé. Ce nom de fichier existait déjà : 162 lignes, les critères 1 à 5 et 9 de la matrice
visuelle, le contrôle que toute action visée par un marqueur EXISTE, et la règle « le marqueur
ne se pose qu'en visitant ». La fusion telle quelle supprimait 25 assertions en silence.

Réparé sans rien perdre de ton travail : l'ancien est restauré sous son nom, le tien vit dans
**`verifier_illustrations_declarees.rb`**, les deux sont verts. Ta logique était juste — c'est
le nom qui était pris. Avant d'écrire un banc, `ls scripts/ | grep <thème>` aurait montré la
collision ; ta contre-vérification Perl éprouvait le contenu, pas le fichier.

**3. Ton rendez-vous va sonner, et c'est toi qui le fais sonner.** Les quatre illustrations
existent maintenant chez Codex. Quand tu les poses dans `public/pz/m0/powers/`,
`verifier_illustrations_declarees` rougit sur `[les quatre] ≠ []` — c'est le comportement que
tu as toi-même conçu : vide l'attente dans la même livraison.

**4. Le `detail` de Communication est canon** (Codex `652634f`), déployé des deux côtés. Plus
aucun ÉDITORIAL PROVISOIRE dans `config/monde_0.yml`.

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
