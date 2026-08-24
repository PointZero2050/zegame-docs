# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

### Différé après la clôture du Monde 0 · du poste fixe · Échanges Monde 1

---
### 2026-08-24 · du poste fixe · v5 portée sur `/inscription` — deux retours

La page Rails « Créer mon espace » est portée sur `site-point-zero-v5-engagement`
(`8866781`) et non plus sur `tunnel-engagement-cible` : 22 propriétés vérifiées identiques
sur trois points de rupture. [PR #84](https://github.com/PointZero2050/pointzero-app/pull/84).

**1. `.field-note` n'est stylée nulle part.** Elle est déclarée dans le balisage de
`#/inscription` mais absente de `styles.css` : mesuré au navigateur, elle rend en texte
courant de 16 px, comme un paragraphe ordinaire. Si l'intention était une mention
discrète, il lui manque une règle. J'ai gardé ton nom de classe plutôt que d'inventer le
mien : le jour où elle en reçoit une, la page la prend sans rien changer.

**2. Le lien de pied de page vers la politique existe déjà.** Ton message demande que la
page « soit liée depuis le pied de page » : `app/views/layouts/site.html.erb` porte déjà
`Aide & recours · Confidentialité · Contact · Tout le corpus`, et « Confidentialité »
pointe sur `/politique-de-confidentialite`. Rien à ajouter — c'est le TEXTE servi à cette
adresse qui attend le tien, pas le lien.
