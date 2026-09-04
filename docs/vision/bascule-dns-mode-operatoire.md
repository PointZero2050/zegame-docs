# Bascule DNS et extinction de WordPress — mode opératoire

> Rédigé par Claude (portable de Boris) le 2026-08-04, à sa demande. Établi après **relevé réel
> des enregistrements DNS** et lecture de la configuration du serveur. À exécuter tel quel : les
> valeurs ci-dessous sont celles constatées, pas des exemples.

## 0. État constaté

| Élément | Valeur actuelle |
|---|---|
| Registrar / DNS | OVH (`ns20.ovh.net`, `dns20.ovh.net`) |
| `pointzero2050.com` A | `164.132.235.17` (OVH mutualisé — WordPress) · **TTL 3600 s** |
| `www` A | `164.132.235.17` (enregistrement A, pas un CNAME) |
| `new` A | `167.233.210.57` (Hetzner — la nouvelle pile) |
| ⚠️ `pointzero2050.com` **AAAA** | `2001:41d0:301::23` (OVH) — **`new` n'en a aucun** |
| ⚠️ `www` **AAAA** | `2001:41d0:301::23` (OVH) |
| IPv6 du serveur Hetzner | `2a01:4f8:c015:16f3::1` — Caddy y répond (vérifié le 4 septembre) |
| MX | `mx1/mx2/mx3.mail.ovh.net` — **le courrier ne bouge pas** |
| SPF | `v=spf1 include:mx.ovh.com include:spf.brevo.com -all` — déjà correct |
| DMARC | `p=none; rua=mailto:rua@dmarc.brevo.com` |
| DKIM | `mailpoet1` et `mailpoet2` → `sendingservice.net` (MailPoet, à retirer après extinction) |
| Autres | `mail`, `ftp`, `autoconfig`, `autodiscover` — liés au courrier OVH, **ne pas toucher** |
| Caddy | ne sert que `new.pointzero2050.com` |
| `APP_HOST` | `new.pointzero2050.com` (utilisé pour les liens des courriels) |

**Règle d'or : seuls trois enregistrements changent — l'apex `A`, le `www`, et rien d'autre.**
Toucher au MX couperait le courrier de tout le domaine.

## 1. Préalables (à cocher avant de fixer une date)

- [ ] La vente de billets est ouverte et stable depuis **au moins 48 heures** — ne jamais
      superposer une bascule DNS et une ouverture de vente : deux sources d'incident simultanées
      rendent tout diagnostic impossible.
- [ ] Le Festival est publié et un achat réel a été vérifié (fait le 2026-08-04).
- [ ] Sauvegarde fraîche de la base (`/home/deploy/sauvegardes/`).
- [ ] Boris est disponible dans les deux heures qui suivent la bascule.
- [ ] **Ne pas basculer un vendredi ni la veille d'une absence.**

## 2. J-2 : abaisser le TTL

Chez OVH, zone DNS de `pointzero2050.com` : passer le **TTL de l'enregistrement A de l'apex et
du `www` à 300 secondes**, sans changer leur valeur.

Raison : le TTL actuel est de 3600 s. Sans cet abaissement préalable, un retour en arrière
mettrait **une heure** à se propager au lieu de cinq minutes. C'est la seule étape qui doit être
faite à l'avance, et elle est sans risque.

Vérification (à faire depuis le serveur, où `dig` est disponible) :

```bash
ssh -i ~/.ssh/id_ed25519_pointzero deploy@167.233.210.57 'dig pointzero2050.com A +noall +answer'
```

Le TTL affiché doit descendre à 300 dans l'heure qui suit.

## 3. J-0, étape 1 : préparer Caddy (avant de toucher au DNS)

Caddy doit **déjà accepter les nouveaux noms** au moment où le DNS bascule, sinon le certificat
ne peut pas être délivré et le site tombe. Nouveau `caddy/Caddyfile` :

```
pointzero2050.com, www.pointzero2050.com {
	encode zstd gzip
	reverse_proxy web:3000
}

new.pointzero2050.com {
	encode zstd gzip
	reverse_proxy web:3000
}
```

`new.pointzero2050.com` est **conservé délibérément** : c'est la porte de secours si l'apex pose
problème, et l'URL déclarée au webhook Stripe continue de fonctionner.

Puis `docker compose up -d caddy`. Caddy tentera d'obtenir les certificats et **échouera tant
que le DNS n'a pas basculé** — c'est normal et attendu, il réessaie automatiquement.

## 4. J-0, étape 2 : basculer le DNS

Chez OVH, zone DNS :

| Enregistrement | Ancienne valeur | Nouvelle valeur |
|---|---|---|
| `pointzero2050.com` A | `164.132.235.17` | **`167.233.210.57`** |
| `www` A | `164.132.235.17` | **`167.233.210.57`** |
| `pointzero2050.com` **AAAA** | `2001:41d0:301::23` | **`2a01:4f8:c015:16f3::1`** |
| `www` **AAAA** | `2001:41d0:301::23` | **`2a01:4f8:c015:16f3::1`** |

⚠️ **REPOINTER, PAS SUPPRIMER.** Le 4 septembre, les AAAA ont d'abord été supprimés : les
résolveurs gardent alors l'ancienne valeur jusqu'à l'expiration de son TTL (une heure), et **tout
client qui préfère l'IPv6 continue d'atteindre l'ancienne machine** pendant ce temps — le site
paraît « pas encore basculé » alors qu'il l'est. En les repointant vers notre IPv6, les résolveurs
déjà rafraîchis (Cloudflare, Google : quelques minutes) envoient l'IPv6 chez nous immédiatement.
Vérifié le jour même : apex et `www`, en IPv4 **et** en IPv6, `200` avec certificat valide.

⚠️ **LES AAAA MANQUAIENT À CE DOCUMENT, ET ÇA A COÛTÉ LA BASCULE DU 4 SEPTEMBRE.** Cette procédure
ne relevait que les enregistrements A. Résultat mesuré ce jour-là : l'apex basculé en IPv4, mais
**tout visiteur en IPv6 continuait de voir WordPress** — et surtout, Let's Encrypt valide **en
priorité par IPv6** quand un AAAA existe. Le défi partait donc vers l'ancienne machine, aucun
certificat ne pouvait être délivré, et le site est resté injoignable en HTTPS le temps qu'on
comprenne. Un relevé DNS qui ne regarde qu'une famille d'adresses n'est pas un relevé.

Rien d'autre. Ne pas toucher aux MX, aux DKIM, à `mail`, `ftp`, `autoconfig`, `autodiscover`.

Piège déjà rencontré : le champ « sous-domaine » d'OVH **ajoute la zone automatiquement**.
Pour l'apex, laisser le champ vide ; pour le `www`, écrire `www` seul — jamais
`www.pointzero2050.com`, qui produirait `www.pointzero2050.com.pointzero2050.com`.

## 5. J-0, étape 3 : dans les minutes qui suivent

```bash
# la propagation
dig +short pointzero2050.com A        # doit renvoyer 167.233.210.57
dig +short www.pointzero2050.com A

# le certificat (Caddy l'obtient en quelques secondes une fois le DNS à jour)
curl -sI https://pointzero2050.com | head -3
curl -sI https://www.pointzero2050.com | head -3
```

Puis **pointer l'application sur son nouveau nom** — sinon les liens des courriels
(confirmation d'inscription, réinitialisation de mot de passe) continueraient de renvoyer vers
`new.` :

```bash
# dans /home/deploy/deploy/.env
APP_HOST=pointzero2050.com
```
puis `docker compose up -d web`.

## 6. J-0, étape 4 : vérifications fonctionnelles

- [ ] `https://pointzero2050.com` affiche le nouvel accueil (et non WordPress)
- [ ] `https://www.pointzero2050.com` répond aussi
- [ ] Une page du corpus historique : `/le-pouvoir-des-recits`
- [ ] Le Sas : `/sas` et un parcours
- [ ] Connexion au jeu, puis `/jeu`
- [ ] La page du Festival et son formulaire d'achat
- [ ] **Un achat réel de contrôle** sur un événement d'essai à 1 €, remboursé — c'est le seul
      moyen de prouver que Stripe et le webhook fonctionnent sous le nouveau nom
- [ ] Une réinitialisation de mot de passe : le lien reçu doit pointer `pointzero2050.com`

## 7. Le plan de redirections — plus léger qu'attendu

Constat mesuré : **les 138 pages du corpus sont servies à leur URL d'origine**, et **aucun slug
du nouveau site n'entre en collision** avec elles. La majorité du référencement est donc
préservée sans aucune redirection.

Restent les URL propres à WordPress, qui n'existent plus :

| Motif | Traitement |
|---|---|
| `/wp-content/uploads/*` | déjà réécrit vers `/media/*` à l'import ; ajouter une 301 pour les liens externes |
| `/wp-admin`, `/wp-login.php`, `/xmlrpc.php` | 410 ou redirection vers l'accueil |
| `/feed`, `/*/feed` | 301 vers l'accueil (ou un flux natif plus tard) |
| `/category/*`, `/tag/*`, `/author/*` | 301 vers `/corpus` |
| `?p=123`, `?page_id=123` | non résolvables sans table de correspondance — laisser en 404 |
| `/panier`, `/mon-compte` | **présents dans le corpus importé** : ils s'afficheront tels quels alors qu'ils n'ont plus d'objet — à rediriger vers `/agenda` |

**Méthode recommandée plutôt qu'un plan exhaustif à l'aveugle** : après la bascule, journaliser
les 404 pendant une semaine et ajouter les redirections que le trafic réel réclame. C'est plus
sûr que de deviner, et cela évite d'écrire des règles pour des URL que personne ne visite.

## 7 bis. ⚠️ Le piège du compte ACME de staging

Vécu le 4 septembre, après la correction des AAAA : les certificats échouaient encore, avec
« *The key authorization file from the server did not match this challenge* » — la bonne étiquette,
mais **signée d'une autre clé de compte**.

Cause : `preprod.pointzero2050.com` était déclaré dans le Caddyfile **sans exister au DNS**, et
Caddy tentait son certificat depuis vingt-cinq jours (122 essais). Après tant d'échecs il se rabat
sur l'endpoint de **staging** de Let's Encrypt pour ne pas brûler les quotas de production — et se
retrouve avec **deux comptes ACME** dans son magasin. Les deux répondent au même défi, chacun avec
sa clé : la validation échoue toujours, et les certificats de staging ne sont reconnus par aucun
navigateur.

Deux gestes, dans cet ordre :

1. **retirer du Caddyfile tout nom qui n'existe pas au DNS** — un nom mort dans un bloc TLS n'est
   pas inoffensif, il entraîne le client ACME avec lui ;
2. **supprimer le compte de staging** du magasin, après avoir vérifié qu'aucun certificat n'en
   dépend :

```bash
docker compose -f ~/deploy/compose.yml exec -T caddy sh -c \
  'ls /data/caddy/certificates/ ; rm -rf /data/caddy/acme/acme-staging-v02.api.letsencrypt.org-directory'
docker compose -f ~/deploy/compose.yml restart caddy
```

Les certificats sont alors obtenus en moins d'une minute.

## 8. Retour en arrière

Si quoi que ce soit d'important ne fonctionne pas :

1. remettre l'apex et le `www` à `164.132.235.17` chez OVH ;
2. avec le TTL à 300 s, le retour est effectif en **cinq minutes** ;
3. WordPress est toujours debout et resservira le site.

C'est la raison pour laquelle **WordPress ne s'éteint pas le jour de la bascule** : on le laisse
en veille au moins une semaine.

## 9. Extinction de WordPress (J+7 au plus tôt)

Une fois la bascule stable :

- [ ] **Supprimer le webhook WooCommerce chez Stripe** — `https://pointzero2050.com/?wc-api=wc_stripe`,
      toujours actif et abonné aux mêmes événements que le nôtre. Une fois WordPress éteint, il
      accumulerait des échecs de livraison.
- [ ] Retirer les DKIM `mailpoet1` et `mailpoet2` de la zone DNS (MailPoet ne sert plus).
- [ ] Révoquer les clés et jetons WordPress restants.
- [ ] Sauvegarde finale de WordPress (base + `wp-content`), archivée hors OVH.
- [ ] Désactiver l'hébergement mutualisé — **sans toucher au domaine ni au courrier**, qui
      restent chez OVH.
- [ ] Faire tourner la clé Stripe restreinte si ce n'est pas déjà fait.

## 10. Durées

| Étape | Durée |
|---|---|
| J-2 : abaisser le TTL | 5 min |
| Préparer Caddy | 10 min |
| Basculer le DNS | 5 min |
| Propagation et certificats | 5 à 30 min |
| Vérifications fonctionnelles | 30 min |
| **Total le jour J** | **environ 1 h 30**, dont beaucoup d'attente |

L'extinction de WordPress, une semaine plus tard, demande une heure de plus.
