# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · du poste fixe · ⚠️ Le canon « aucun badge aux Guides » contredit un seuil LIVRÉ

Consigne de Codex restée dans ma boîte : « **ne pas afficher un badge à la rencontre des
Guides** » (`guides-intuition-metaparcours-badges.md` §3.4). « Le premier échange complet active
cette bulle mais ne donne aucun badge. `Présence ouverte` reste attaché à l'entrée dans l'Espace
d'échange et `Première grammaire acquise` aux dix clés. »

**Or le seuil existe, il est livré, et il est délibéré :**

- `config/seuils.yml:167` — `m0_communication`, titre **« Dialogue ouvert »**, description
  « Une première question posée aux guides du Jeu », sceau `pluriel`, annonce `bandeau` ;
- `guides_controller.rb:44` pose `m0-dialogue-guides` dès qu'une question est posée, avec un
  commentaire qui nomme explicitement le badge : « le badge "Dialogue ouvert" lit cette clé » ;
- `monde_0_etats.rb:134` et `:178` lisent la même clé pour la carte Communication.

**Je n'y touche pas, et pour trois raisons.** `config/seuils.yml` est le fichier du portable ;
retirer un seuil est un arbitrage produit ; et des joueurs le détiennent peut-être déjà — un
badge qui disparaît d'un profil n'est pas un détail d'affichage.

**Ce qu'il faut trancher**, dans cet ordre : Codex parle-t-il de la cible d'Intuition (où les
Guides changent de fonction) ou de l'état d'aujourd'hui ? Si c'est d'aujourd'hui, que devient le
seuil déjà accordé — retiré, conservé pour ceux qui l'ont, ou renommé ?

Tant que ce n'est pas tranché, l'écart reste : la doctrine dit une chose, l'application en fait
une autre, et les deux sont écrites noir sur blanc.

---


### 2026-08-20 · du poste fixe · Éditorial `/guide` à réaligner sur Intuition

**Attendu :** remplacer l'ancien chapeau « COMMUNICATION · PREMIER CONTACT » maintenant que les
Guides appartiennent à Intuition.
**Référence :** lot de ventilation porté par la PR #33 ; arbitrage de libellé « Échanges » déjà
porté côté Rails.

Le reste du message du poste fixe — ventilation, lot éditorial et agenda M0 — est traité.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** produire l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange est fixée (`9a37aed`) et traduite dans les
prototypes (`84fb1cc`).

Le contrat de remontée d'activité d'Immateria est explicitement reporté par Boris : ne pas le
mélanger avec cette vague.
