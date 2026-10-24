# Secours du serveur — quand le portable n'est plus joignable

> Portable, 24 octobre 2026, à la demande de Boris. Le portable porte seul la clé de travail ; le poste fixe a
> désormais **sa propre clé de secours** (`~/.ssh/id_ed25519_pointzero_secours`, empreinte
> `SHA256:BoFo1XM0NChgSpSBnuhM5Re3JIz5hikI57O+7rkamjo`), installée pour `deploy` sur 167.233.210.57.
> **Aucun secret ici** : ni clé privée, ni mot de passe, ni jeton.

## Quand l'employer

- **Seulement si le portable est injoignable**, et **sur le mot de Boris**.
- **C'est un accès de dépannage :** diagnostiquer, redémarrer, revenir en arrière, libérer le disque.
- **Pas un chemin de déploiement :** une fonctionnalité passe toujours par une PR et par le portable.
- **Après coup**, consigner ce qui a été fait dans `docs/agents/boite-portable.md` : commande, heure, résultat.

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

## Ce qui ne se fait jamais par ce chemin

- Copier la clé de secours ailleurs (Dropbox, dépôt, message), ou y recopier celle du portable.
- Pousser sur `main` ou fusionner une PR ; passer des migrations ; éditer `~/deploy/compose.yml` sans Boris.
- Toucher aux conteneurs `zoe-`, ou lancer un `prune` qui emporterait volumes et images de repli.
