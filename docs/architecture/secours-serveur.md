# Secours du serveur — quand le portable n'est plus joignable

> Portable, 24 octobre 2026, à la demande de Boris. Le portable porte seul la clé de travail ; le poste fixe a
> désormais **sa propre clé de secours** (`~/.ssh/id_ed25519_pointzero_secours`, empreinte
> `SHA256:BoFo1XM0NChgSpSBnuhM5Re3JIz5hikI57O+7rkamjo`), installée pour `deploy` sur 167.233.210.57.
> **Aucun secret ici** : ni clé privée, ni mot de passe, ni jeton.

## Quand l'employer

- **Seulement si le portable est injoignable**, et **sur le mot de Boris**.
- ⚠️ **ÉLARGI LE SOIR MÊME PAR BORIS** (« j'ai besoin que tu puisses prendre la main en cas d'indisponibilité ») :
  le poste fixe **reprend alors la fonction entière du portable**, et plus seulement le dépannage :
  - dépanner : diagnostiquer, redémarrer, revenir en arrière, libérer le disque (§ 1 à 8) ;
  - relire les PR et **fusionner à la main sur le serveur** (jamais `gh pr merge`), déployer la préprod, rejouer les
    bancs, purger les comptes jetables — avec les MÊMES procédures que le portable (`CLAUDE.md`, « Déployer »,
    « Promotion en production ») ;
  - coder dans la zone du portable (modèles, migrations, contrôleurs, routes), toujours par PR ;
  - **promouvoir en production : sur le mot EXPLICITE de Boris**, sauvegarde vérifiée d'abord (§ 5).
- **Après coup**, consigner chaque geste dans `docs/agents/boite-portable.md` : commande, heure, résultat. À son
  retour, le portable relit ce qu'il n'a pas vu (une fusion faite en son absence n'est pas « validée » tant qu'il ne
  l'a pas relue) et reprend la main.
- 📝 **À compléter par le portable** : la séquence exacte d'une fusion et d'une promotion depuis le serveur (où se fait
  la fusion, ce qui se pousse vers GitHub, les bancs à rejouer), pour que la reprise ne s'improvise pas.

## Se connecter

```bash
ssh -i ~/.ssh/id_ed25519_pointzero_secours deploy@167.233.210.57
```

## Repères

| | Production | Préprod |
| --- | --- | --- |
| Adresse | https://pointzero2050.com | https://preprod.167-233-210-57.sslip.io |
| Code | `~/src/pointzero-app` (branche `main`) | `~/src/pointzero-preprod` (branche `preprod`) |
| Compose | `~/deploy/compose.yml` | `~/preprod/compose.yml` |
| Conteneurs | `pointzero-web-1`, `pointzero-db-1` | `pointzero-preprod-preprod-web-1`, `…-db-1` |

- **Le proxy frontal** est `pointzero-caddy-1`. Il est partagé avec Zoé, qui sert aussi zoe-2030.com.
- ⚠️ **Les conteneurs `zoe-…` ne se touchent jamais d'ici** : ils ont leur propre utilisateur et leur propre clé.

## 1. Diagnostiquer, sans rien changer

```bash
curl -s -o /dev/null -w "%{http_code}\n" https://pointzero2050.com/up
```

```bash
docker ps --format '{{.Names}} {{.Status}}'
```

```bash
docker logs --since 15m pointzero-web-1 2>&1 | tail -80
```

```bash
df -h / && docker system df
```

**Ce qu'il faut regarder :**
- `/up` à 200 : l'application répond.
- Un conteneur `Restarting` : il ne démarre pas, et son journal dit pourquoi.
- Un disque au-delà de 90 % : PostgreSQL s'arrête quand le disque est plein, et la billetterie avec lui.

## 2. Redémarrer l'application

```bash
cd ~/deploy && docker compose -f compose.yml restart web
```

Puis attendre que `/up` réponde 200, en une à deux minutes.

## 3. Libérer le disque

```bash
sh ~/purger_cache_docker.sh
```

- Ce script garde une semaine de cache de construction et purge le reste.
- ⚠️ Jamais `docker system prune -a`, ni `docker volume prune` : ils emportent les images de repli, voire les données.

## 4. Revenir à l'image précédente (le code d'avant, la base inchangée)

Les images de repli sont gardées sous un nom (`avant-…`) à chaque promotion :

```bash
docker images pointzero-web --format '{{.Tag}} {{.ID}} {{.CreatedSince}}'
```

Remplacer `avant-stores` par le nom choisi :

```bash
docker tag pointzero-web:avant-stores pointzero-web:latest && cd ~/deploy && docker compose -f compose.yml up -d --force-recreate web
```

- **Ce retour ne reconstruit rien.** `main` n'est pas touché : le portable remettra les choses d'aplomb à son retour.
- ⚠️ **Il ne suffit pas si une migration a changé la base depuis.** L'ancien code peut alors ne plus la lire : en ce
  cas, ne pas aller plus loin sans Boris.

## 5. Prendre une sauvegarde (toujours avant toute écriture)

```bash
F=~/sauvegardes/prod-$(date +%Y%m%d-%H%M)-secours.sql.gz; docker exec pointzero-db-1 sh -c 'pg_dump -U $POSTGRES_USER $POSTGRES_DB' | gzip > $F && sh ~/verifier_sauvegarde.sh $F pointzero-db-1
```

`verifier_sauvegarde.sh` compare cinq tables entre l'archive et la base vivante. Les deux colonnes doivent être
égales : une archive vide ne se voit qu'en l'ouvrant.

## 6. Restaurer une sauvegarde — dernier recours, avec Boris

⚠️ **Procédure NON répétée sur la production.** La répétition se fait sur une base jetable avec
`scripts/repeter_restauration.sh`.

En vrai, **après une sauvegarde de l'état présent (§ 5)** :
1. Arrêter l'application : `cd ~/deploy && docker compose -f compose.yml stop web`.
2. Mettre la base actuelle de côté, en la renommant plutôt qu'en l'effaçant, puis en créer une neuve et y charger
   l'archive choisie (`F=…`) :

```bash
docker exec pointzero-db-1 sh -c 'psql -U $POSTGRES_USER -d postgres -c "ALTER DATABASE \"$POSTGRES_DB\" RENAME TO \"${POSTGRES_DB}_avant_restauration\""' && docker exec pointzero-db-1 sh -c 'createdb -U $POSTGRES_USER "$POSTGRES_DB"' && gunzip -c "$F" | docker exec -i pointzero-db-1 sh -c 'psql -U $POSTGRES_USER -d "$POSTGRES_DB" -v ON_ERROR_STOP=1 -q'
```

3. Relancer : `cd ~/deploy && docker compose -f compose.yml up -d web`. Vérifier `/up`, puis comparer les comptages
   avec `verifier_sauvegarde.sh`.

## 7. Si SSH lui-même ne répond plus

- La **console de secours Hetzner**, depuis le compte Hetzner de Boris : accès à l'écran du serveur, redémarrage.
- Un redémarrage complet relance Docker. Les conteneurs reviennent seuls (`restart` dans les compose), et `/up` le
  confirme.

## 8. Les sauvegardes Hetzner (actives)

- Une **image du disque système chaque jour**, vers 08 h 47, et **sept gardées**. La base de production y est,
  puisqu'elle vit sur ce disque. Elles se voient dans la console : serveur → Backups.
- **Restaurer une de ces images remet TOUT le serveur à cette date** : la production, la préprod, Zoé, les
  certificats. Tout ce qui a été écrit depuis est perdu. C'est le recours ultime, **décidé par Boris**, quand rien
  d'autre ne marche.
- ⚠️ **Elles ne prennent pas les volumes.** Les données de Zoé sur `zoe-donnees` (`/srv/zoe`) n'y sont pas.
- Pour ne revenir que sur la base de production, les archives `~/sauvegardes/prod-*.sql.gz` (§ 5 et § 6) sont plus
  fines. Elles sont prises à chaque promotion.

## 9. Fusionner une PR en préprod — la séquence du portable

> Écrit par le portable le 24 octobre 2026, à la demande du poste fixe, d'après les fusions de #474 à #486.
> Chaque commande se lance par `ssh -i ~/.ssh/id_ed25519_pointzero_secours deploy@167.233.210.57 '…'`.
> Les messages de commit s'écrivent dans un FICHIER (les apostrophes cassent `-m` à travers ssh), puis
> `git commit -F` ou `git merge -F`. Ils sont préfixés `[Claude]` et finissent par la ligne `Co-Authored-By`.

1. **L'arbre est propre et à jour.**
   - `cd ~/src/pointzero-preprod && git status --porcelain` ne doit rien montrer d'inconnu ; seul
     `scripts/inscrits_depuis.rb`, non suivi, est connu.
   - Puis `git fetch -q origin`, et vérifier que `HEAD` est égal à `origin/preprod`.
2. **Relire la PR** (`gh pr view`, `gh pr diff`). La branche doit être entière : relire au dernier commit, car une
   PR ouverte bouge encore.
3. **Fusionner à la main**, jamais `gh pr merge` : `git merge -q --no-ff origin/<branche> -F /tmp/msg.txt`. Ensuite,
   `git diff --stat origin/<branche> HEAD` ne doit rien montrer, sauf ce que la branche n'avait pas.
4. **Contrôles AVANT la construction** :
   - Copier les vues et le code fusionnés dans le conteneur : `docker cp <fichier>
     pointzero-preprod-preprod-web-1:/rails/<fichier>`.
   - Compiler les vues : `docker exec pointzero-preprod-preprod-web-1 bin/rails runner scripts/verifier_vues_haml.rb`.
     Une erreur Haml n'apparaît qu'au rendu.
   - Vérifier chaque fichier Ruby : `docker exec -i pointzero-preprod-preprod-web-1 ruby -c < <fichier>`. Le `-i` est
     obligatoire, sinon tout passe.
   - JavaScript : `node --check` sur le poste fixe (le serveur n'a pas `node`).
5. **Pousser, construire, redémarrer** :
   - `git push -q origin HEAD:preprod`.
   - Puis `cd ~/preprod && docker compose -f compose.yml build preprod-web && docker compose -f compose.yml run --rm
     preprod-web bin/rails db:migrate && docker compose -f compose.yml up -d --force-recreate preprod-web`.
   - Jamais `;` entre la migration et le `up` : une migration cassée ferait boucler la préprod.
   - Un second `docker restart` si un `.yml` mémoïsé a changé.
6. **Les bancs touchés** :
   - Attendre que `https://preprod.167-233-210-57.sslip.io/` réponde 200.
   - Vérifier qu'aucune recette ne tourne, avec `pgrep -fa "^/bin/bash ./scripts/recette"` lancé SEUL.
   - Puis, dans un second appel : `cd ~/src/pointzero-preprod && (setsid nohup ./scripts/recette.sh <banc1> <banc2>
     > /tmp/recette-x.log 2>&1 &)`.
   - Lire `/tmp/recette-x.log` jusqu'à `VERTS`. Un banc qui affirme une balise changée change dans la même livraison.
7. **Commenter la PR** avec l'identifiant RELU après le commit (`git log --oneline -1`), puis écrire dans les boîtes.

## 10. Promouvoir en production — sur le mot EXPLICITE de Boris

1. **Recette transversale complète en préprod**, verte : `./scripts/recette.sh` sans argument, environ 90 minutes
   pour 267 bancs. Le banc Stripe est hors de portée en préprod.
2. **Relever ce que la promotion emporte** :
   - les migrations : `git diff --name-only main origin/preprod -- db/migrate/` ;
   - les `.yml` mémoïsés ;
   - les gestes de DONNÉES à rejouer en production (scripts `ECRIRE=oui`, relevés dans la passation). La promotion ne
     transporte que le code.
3. **Sauvegarde vérifiée (§ 5)**, puis l'image de repli : `docker tag pointzero-web:latest pointzero-web:avant-<nom>`.
4. **Fusionner** : `cd ~/src/pointzero-app && git status --porcelain && git fetch -q origin && git merge -q
   --no-edit origin/preprod`. Puis **`git diff --stat origin/preprod HEAD` doit être VIDE**. Deux scripts non suivis
   (`importer_inscrits_wordpress.rb`, `supprimer_essai.rb`) sont à laisser.
5. **Construire sans couper** : `cd ~/deploy && docker compose -f compose.yml build web`. L'ancien conteneur sert
   pendant la construction.
6. **Sur l'image neuve, en conteneurs ponctuels** :
   - `docker compose -f compose.yml run --rm web bin/rails runner scripts/verifier_vues_haml.rb` ;
   - puis, s'il y a des migrations, `… run --rm web bin/rails db:migrate` ;
   - puis les gestes de données : simulation d'abord, et arrêt au moindre écart.
7. **Basculer** :
   - `docker compose -f compose.yml up -d --force-recreate web` ;
   - un second `docker restart pointzero-web-1` si un `.yml` mémoïsé a changé ;
   - attendre que `/up` réponde 200, et lire les journaux.
8. **Pousser** : `cd ~/src/pointzero-app && git push -q origin main`.
9. **Les bancs en production** :
   - `cd ~/src/pointzero-app && CONTENEUR=pointzero-web-1 ./scripts/recette.sh <liste>`, avec Stripe, les bancs du
     lot et `verifier_limites_de_tentatives` ;
   - puis compter les comptes jetables (`email LIKE '%.pz' OR email LIKE '%banc%'`) : il doit en rester 0 ;
   - vérifier que `acces-verification` répond 404.
10. **Après** : `sh ~/purger_cache_docker.sh`, puis les boîtes et la passation.

## Ce qui ne se fait jamais par ce chemin

- Copier la clé de secours ailleurs (Dropbox, dépôt, message), ou y recopier celle du portable.
- Promouvoir en production sans le mot EXPLICITE de Boris, ou sans sauvegarde vérifiée ; éditer
  `~/deploy/compose.yml` sans lui.
- `gh pr merge` : une fusion se fait à la main sur le serveur, bancs compris.
- Toucher aux conteneurs `zoe-`, ou lancer un `prune` qui emporterait volumes et images de repli.
