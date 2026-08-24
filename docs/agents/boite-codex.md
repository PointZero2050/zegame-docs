# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

### Différé après la clôture du Monde 0 · du poste fixe · Échanges Monde 1

### 2026-08-24 · du portable · Canon reçu — il me manque **cinq mots** pour livrer la mécanique d'Ω

**Attendu :** les cinq Puissances de rattachement, et un choix technique que ton canon laisse
ouvert. Tout le reste est décidé et je peux écrire dès ta réponse.
**Référence :** `sas-site-et-sas-point-zero-canon.md` §2 · préprod, tout vert.

Ton canon ferme tout ce qui bloquait. J'ai mesuré ce qu'il implique côté mécanique, et il reste
**un seul trou** — celui que tu as toi-même laissé ouvert : *« ce mapping éditorial des cinq
Puissances doit être validé avant la première attribution réelle »*.

**Ce qui me manque, littéralement cinq mots :**

| parcours | badge | Puissance de rattachement |
|---|---|---|
| `humanite` | `decodeur-cycles` | ? |
| `scenarios` | `prospectiviste` | ? |
| `croyances` | `archeologue-des-croyances` | ? |
| `paralysie` | `changeur-d-echelle` | ? |
| `reveil` | `reactivateur-de-puissances` | ? |

Je **ne les propose pas** : ton canon dit « le code ne déduit jamais le `skill_id` du badge, du
slug ou d'un libellé », et proposer un mapping à partir des mêmes libellés reviendrait à faire
faire par moi ce que tu interdis au code. C'est éditorial, c'est à toi.

**⚠️ ET UN CHOIX TECHNIQUE QUE TON CANON NE TRANCHE PAS.** Mesuré : les Ω ne s'accrochent pas à
une Puissance mais à un **`skill_id`** — et une Puissance en compte **six** :

```
Skill : "COMMUNICATION : ÉCOUTE", "COMMUNICATION : EFFACEMENT", "COMMUNICATION : ENVOÛTEMENT", …
42 skills pour 7 Puissances
```

Déclarer « Communication » ne suffit donc pas : il faut savoir SUR LEQUEL des six. Deux voies :

1. **tu nommes le skill exact** pour chacun des cinq parcours — le plus fidèle à ton « jamais
   déduits », et je n'ai rien à décider ;
2. **tu nommes la Puissance**, et je pose une règle de résolution **explicite et documentée**
   (par exemple le premier skill de la Puissance par ordre d'id), écrite dans `config/sas.yml` à
   côté du montant pour qu'elle ne soit jamais une surprise.

Dis-moi laquelle. La seconde est plus légère à écrire pour toi, la première ne laisse aucune
latitude au code — c'est ton arbitrage, et il ne coûte rien de plus tard puisque **les Ω ne
redescendent jamais** : ce que la première attribution écrit est écrit pour toujours.

**Le reste est prêt dans ma tête et ne demande que ton feu vert :** challenge système
`parcours-de-decouverte-du-site` sans aucune inclusion dans un parcours (c'est ainsi qu'il reste
invisible — il n'existe pas de colonne de visibilité), montants dans `config/sas.yml`, import
idempotent (une seule attribution par parcours), et un banc qui asserte qu'un second import
n'ajoute pas un Ω.

**Et je tiens l'ordre que le poste fixe a rappelé** : ta mécanique d'abord, ses textes ensuite.
Il a raison de ne pas publier « 5 Omégas » avant que les Ω existent — c'est exactement l'ordre
que j'ai tenu sur Imagination, dans l'autre sens.

Le portage de `messagerie-par-mondes-cible/?stage=m1entry` et `?stage=m1circle` attend encore :

- le contenu du panneau de Monde (`DISPONIBLE MAINTENANT`, `HORIZON SUIVANT`, soutien du cadre,
  prochain seuil) ;
- les deux cartes d'apprentissage d'entrée et de Cercle ;
- l'arbitrage pages ou onglets pour `Fil · Actions · Décisions · Mémoire`.

Ce lot reste volontairement différé : Boris a demandé de finir le Monde 0 avant de reprendre les
parcours et les surfaces Monde 1.
