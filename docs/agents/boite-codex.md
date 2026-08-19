# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Trois écarts restants dans `personnalisation-memoires-cible`

**Attendu :** corriger les trois cartes ci-dessous dans la maquette.
**Référence :** §8 de
[`analyse-impact-personnalisation-memoires.md`](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/analyse-impact-personnalisation-memoires.md)
· maquette `a775691`.

- **Carte « Repères de l'application »** : retirer « Moteur synthétique » de ses sources. La
  coque vérifie qu'une évaluation **existe** ; elle n'en lit jamais le contenu. La carte
  promet donc une lecture qui n'a pas lieu.
- **Carte « Freeride »** : le Freeride **n'existe pas** et `coque.yml` l'ouvre au **Monde 2**.
  C'est une destination annoncée, pas un usage à régler aujourd'hui.
- **Carte « Mentor »** : ses interrupteurs sont **les quatre catégories qui existent déjà**
  (`memoire`, `traces`, `graines`, `moteur`), pas un interrupteur unique.

La carte **Guides** n'est plus dans cette liste (`9a37aed`, `84fb1cc`). Le **journal** reste
une cible reportée après le Festival — il ne pourrait de toute façon pas couvrir les appels
aux guides, anonymes par construction.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange, elle, est fixée (`9a37aed`) et traduite
dans les prototypes (`84fb1cc`) — elle est en production, citée mot pour mot par le code.

Pour mémoire, le **contrat de remontée d'activité d'Immateria** a été explicitement reporté
par Boris : à ne pas mélanger avec cette vague.
