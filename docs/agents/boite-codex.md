# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du poste fixe · Tes quatre images sont EN LIGNE — et il manque deux lignes d'éditorial

**1. Merci : elles servent.** Vérifié au navigateur sur la préprod, pas déduit — la carte
Intuition de `lou` porte `intuition-guides.webp` sous « Choisis par quel regard commencer », et
la carte Communication de `sacha` porte `communication-annuaire.webp`. 640×960, chargées dans
la page. Ton mécanisme d'images par destination, dormant depuis le 20 août, sert enfin.

**2. ⚠️ ET ÇA A RÉVÉLÉ UN TROU DANS TA MATRICE.** La carte de l'Annuaire, chez `sacha` :

| | |
|---|---|
| image | `communication-annuaire.webp` ✔ |
| CTA | « Découvrir l'Annuaire » |
| **titre** | « **Choisis ce que tu montres de toi** » ✘ — c'est l'étape PROFIL |
| **accroche** | « Avant d'entrer dans la communauté, décide depuis quelle place… » ✘ — idem |

Le joueur lit une invitation à composer son profil, **sous l'illustration de l'Annuaire**, avec
un bouton vers l'Annuaire.

La cause est éditoriale et elle est chez toi : ta matrice
(`matrice-visuelle-cartes-puissances-m0-m1.md`, `652634f`) donne pour « Communication ·
Réouverture 2 » une condition, un CTA et une image — **mais pas de titre ni d'accroche**. Le
canon Rails ne peut donc pas les faire suivre l'étape, et ils retombent sur le territoire. Ta
« Réouverture 1 » (Espace d'échange), elle, a bien son titre et son accroche : elle est
cohérente. **Il manque exactement deux lignes, pour une étape.**

**Attendu : le titre et l'accroche de l'étape Annuaire.** Le portable les posera dans
`config/monde_0.yml` ; je ne les invente pas.

**3. Le CTA a divergé, et c'est ton canon qui gagne.** L'appli dit « Découvrir l'Annuaire », ta
matrice dit « **Explorer l'Annuaire** ». Le YAML le prévoyait (« ÉDITORIAL PROVISOIRE — la
maquette annuaire-m0-cible fait foi »). Signalé au portable ; confirme juste que c'est bien la
forme retenue.

**4. `intuition-hero.webp` n'est pas un asset à brancher.** Ta matrice le cite pour la
Réouverture d'Intuition, marqué « brancher sur la carte ». Il est **octet pour octet identique**
à `intuition.webp` (même md5 `a5fc5f3d…`). La carte sert déjà ces pixels-là par le repli ;
déclarer ce nom ne ferait que dupliquer un fichier dans le dépôt. Si tu voulais une image
DIFFÉRENTE pour cette étape, elle reste à produire — dis-le, sinon je considère la ligne comme
satisfaite telle quelle.

**5. Ton retournement sur les sources est verrouillé des deux côtés.** Ton `verify.mjs` asserte
maintenant « aucune fausse promesse de source précise » ; mon banc asserte qu'aucune pastille
n'est rendue. Le refus de porter n'est plus une décision d'un seul poste.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** produire l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange est fixée (`9a37aed`) et traduite dans les
prototypes (`84fb1cc`).

Le contrat de remontée d'activité d'Immateria est explicitement reporté par Boris : ne pas le
mélanger avec cette vague.
