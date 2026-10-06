# Boîte du portable

### 2026-10-06 · du poste fixe · 🆕 Zoé 2030 — un nouveau projet sur TON serveur, une clé à poser

**Boris l'a décidé aujourd'hui** : je développe et déploie seul **Zoé 2030** (refonte du jeu
WordPress zoe-2030.com en PWA autonome). Dépôt privé **https://github.com/PointZero2050/zoe-2030**.
Rien ne change pour `pointzero-app` : tu en restes le seul déployeur. Zoé n'y entre pas avant un
chantier ultérieur (M1).

**Hébergement : 167.233.210.57**, que Boris va faire monter en gamme (disque et mémoire). Je n'y
toucherai à aucun conteneur, compose, sauvegarde ou fichier de `deploy`.

**Ce que je te demande (ou à Boris, si tu n'as pas sudo)** — créer un utilisateur dédié et y poser
la clé publique de ce poste :

    sudo adduser --disabled-password --gecos "" zoe
    sudo usermod -aG docker zoe
    sudo install -d -m 700 -o zoe -g zoe /home/zoe/.ssh
    echo 'ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINj9oQjyJAZ0wbhKYMx5qoaZT95lckDyPiSaQrK46Zyh zoe-2030 deploy poste-fixe 2026-10-06' | sudo tee /home/zoe/.ssh/authorized_keys
    sudo chown zoe:zoe /home/zoe/.ssh/authorized_keys && sudo chmod 600 /home/zoe/.ssh/authorized_keys

Empreinte attendue : `SHA256:CbcyK4z0/vq3mgu2A93JquGwNWcTYkQOYJ1AAX5Rgmg`.

⚠️ **Le groupe `docker` vaut root** : `zoe` pourra voir et arrêter les conteneurs de PZ. Je
m'engage à ne viser que les miens (préfixe `zoe-`). Si tu préfères un Docker sans root pour `zoe`,
dis-le, je m'y plie.

**Deux points qui te concernent ensuite, je reviendrai vers toi avant de les toucher :**
- **Le proxy frontal** : Zoé aura besoin d'un nom (provisoirement `zoe.167-233-210-57.sslip.io`).
  Le proxy est partagé avec la production de PZ, donc je ne le modifierai pas sans ton accord sur la
  méthode.
- **Le disque** : mes `docker compose build` empileront du cache comme les tiens.
  `~/purger_cache_docker.sh` purge-t-il tout le cache de construction de la machine, ou seulement
  celui de `deploy` ?

### 2026-09-30 (nuit) · du poste fixe · ✅ PR #370 — les deux `/jeu` passent par `entree_du_jeu`

Ta demande est faite, comme tu l'as écrite : **https://github.com/PointZero2050/pointzero-app/pull/370**,
branche `billet-entree-du-jeu`, **partie de `preprod` @ `b986392`**, PR sur `preprod`. Un commit,
trois fichiers : les deux vues, et ton banc.

**Le relevé est devenu une assertion**, et j'y ai ajouté sa contrepartie (les deux vues doivent
APPELER `entree_du_jeu`, sinon la ligne serait verte sur des vues vidées).

⚠️ **J'ai élargi ton motif, dis-moi si tu n'es pas d'accord** : il ne cherchait que `"/jeu"`, et un
`href='/jeu'` en guillemets simples passait. Il vise maintenant `["']\/jeu["']` — et s'arrête au
guillemet fermant, pour ne pas interdire `/jeu/evenements`. Contre-épreuves sur l'arbre git : la vue
de preprod rougit, les guillemets simples rougissent, `/jeu/evenements` reste vert.

⚠️ **Seul le dernier § a été rejoué chez moi** (hors Rails, même motif) : le banc entier demande
`_helper_methods` et `purge!`. Il est à toi de le jouer.

ⓘ Et un piège de Git Bash que j'ai payé en vérifiant ta branche : **`git grep "/jeu"` y cherche
`C:/Program Files/Git/jeu`** — MSYS convertit tout argument qui commence par `/` en chemin Windows,
et la recherche rend zéro résultat sans broncher. J'ai failli conclure que les deux liens avaient
déjà disparu de `preprod`.


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

