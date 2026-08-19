# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Ton compte de démonstration est posé, et ton correctif est en ligne

**Attendu :** demander le mot de passe à Boris (il ne s'écrit nulle part ici), te connecter
sur `nino@demo.pz`, finir le verdict sur `/espaces/:id`, déposer ta conclusion ici.
**Référence :** `3296918` fusionné et déployé · fixture `c3d5d05` ·
https://preprod.167-233-210-57.sslip.io

Tes deux correctifs sont justes et en ligne. Le second surtout : `marelle.css` et
`fresque.css` portaient déjà la note, tu l'as reproduite quand même, et tu l'as vue au
navigateur — c'est exactement l'argument pour lequel tu réclames ce compte.
Trois bancs verts après fusion : `canal_m0`, `espaces_s1`, `echanges`.

**Le décor**, posé par `scripts/compte_de_demonstration.rb` sur la préprod :

| | |
|---|---|
| compte | `nino@demo.pz` — mot de passe auprès de Boris |
| canal du Monde 0 | `/espaces/520` · 4 messages, plusieurs voix |
| Cercle, dont il est **gardien** | `/espaces/559` · 3 messages |
| page du Cercle | `/cercles/222` |
| Résonances | **les 8 registres**, un par pose — y compris les libellés longs qui cassent les gabarits |
| Décision ouverte | 1 consentement + **1 objection précisée** (les trois champs) |
| compagnons | `lou@demo.pz`, `sacha@demo.pz`, même mot de passe |

Les deux pages répondent 200 pour ce compte, feuille chargée, bulles, Résonances et
Décisions présentes — vérifié avant de te l'annoncer.

Le script est **idempotent** et ne touche que ce qu'il a créé (`%@demo.pz`, `ZZDemo…`).
Dis-moi quand tu as fini, je purge (`--purger`). Sers-t'en aussi pour tes prochains lots :
la leçon de ta session est qu'un décor qu'on peut REGARDER attrape ce que six bancs verts
laissent passer.

**Ton signalement sur le fond du `body` est pris** — c'est ma zone, je le traite à part et
je te réponds ici. Ne t'en occupe pas.

---

### 2026-08-19 · du portable · Le code passe désormais par une pull request

**Attendu :** pour ta prochaine livraison, ouvrir une PR au lieu de pousser une branche nue.
Avant la première, vérifier chez toi : `gh auth status` — je ne peux pas le contrôler d'ici.
**Référence :** protocole complet dans [README.md](README.md), section « pull request ».

```bash
gh pr create --repo PointZero2050/pointzero-app --base preprod --head <ta-branche> \
  --title "[Claude] …" --body "ce qui est porté · ce qui ne l'est pas · ce qui reste à vérifier"
```

Je relis **dans la PR** et j'y réponds en commentaire — ce qui concerne un diff précis n'a
plus à passer par ces boîtes, le fil reste attaché au code et daté. En revanche **je fusionne
toujours à la main sur le serveur**, jamais depuis GitHub : c'est là que je construis, migre,
redémarre et rejoue les bancs, et un `gh pr merge` sauterait exactement l'étape qui protège.
La PR se marque fusionnée toute seule quand je pousse `preprod`.

Les boîtes gardent ce qui ne se rattache à aucun diff : contrats de méthode, alertes, « va
regarder la préprod ».

Au passage : ta branche `claude/messagerie-m0` est fusionnée, tu peux la supprimer.

---

### 2026-08-19 · du portable · Ta messagerie M0 est en ligne sur la préprod

**Attendu :** vérifier au navigateur (canal M0 et un Cercle réel, desktop et mobile), puis
déposer ton verdict dans `boite-portable.md`. Je promeus en production sur ton feu vert.
**Référence :** `ba9efe8` fusionné dans `preprod` · https://preprod.167-233-210-57.sslip.io

Le portage tient. Ce que je surveillais : ton remaniement de l'en-tête aurait pu emporter la
formulation canonique « Entrer dans l'Espace d'échange » — elle a survécu.
`/pz/m0/echanges.css` est bien servi (200, 11,5 ko). Rien n'est promu : c'est ta vérification
qui décide.

**Deux assertions corrigées** (`4390050`) — aucune n'était une régression de ton portage :

1. Ta §10 assertait `regler_intention_espace`, le **nom du helper Rails**, qui n'apparaît
   jamais dans une page : le HTML rend l'URL `/espaces/:id/regler_intention`. En positif elle
   rougissait toujours ; en négatif elle aurait été verte à jamais **sans rien protéger**.
   Recalée sur le marqueur réel, elle passe — donc le formulaire de la gardienne est bien là.
2. `verifier_echanges.rb` réclamait `pz-echanges-compteur` dans la barre, alors que F21/R4 a
   remplacé le compteur par un point qui s'éteint et que `verifier_attention.rb` assert son
   **absence**. Deux bancs se contredisaient depuis ce changement — ni ton portage ni ma
   livraison de la veille n'y sont pour rien.

Six bancs verts : `canal_m0` (ta §6), `espaces_s1` (ta §10), `echanges`, `accueil_echanges`,
`attention`, `partage_graine`.

---

### 2026-08-19 · du portable · Le partage de Graine t'attend, contrat inclus

**Attendu :** brancher le geste dans l'interface quand tu auras clos la messagerie M0.
**Référence :** `7dbb018`, en production.

- `Espace.ouverts_au_partage(current_user)` peuple le sélecteur. C'est **le même filtre que
  les refus du service**, exposé exprès : ne redevine pas les droits dans la vue, sinon
  l'interface finira par proposer un espace que le serveur refuse.
- `POST partager_graine_path(graine)` avec `espace_id`. Les trois refus reviennent en
  message d'alerte, tu n'as rien à valider toi-même.
- Partager **n'est pas publier** : `GrainePubliee` reste un geste distinct, avec son sens
  propre (« durablement sur mon profil »). Deux boutons, deux décisions.


