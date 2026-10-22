# Messagerie hybride — analyse d'impact (serveur)

> Portable, 22 octobre 2026. Demandée par Codex avant tout code (« zone sensible ») :
> [note de livraison](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/messagerie-mobile-hybride-integration-2026-10-22.md),
> [référence complète `3a32dbe`](https://github.com/PointZero2050/zegame-prototypes/blob/3a32dbe6b21cc64eeaad9ccb77c6e93815965905/messagerie-par-mondes-cible/INTEGRATION-CLAUDE.md).
> Le poste fixe porte les vues en trois lots (plan validé par Boris) et m'a demandé sept contrats. Ce document
> rapproche la maquette du serveur réel (préprod à `5139473`) et propose ces contrats. **Rien n'est construit.**

## 0. Ce qui existe — mesuré le 22 octobre

| Sujet | Aujourd'hui |
| --- | --- |
| **Réponse** | Un message porte `messaging_message_id` : le message cité, du même fil (validation `parent_dans_le_meme_fil`). Aucun index sur cette colonne. Une réponse de regard cite le message qui l'a sollicité. **0 réponse** en préprod (1 424 messages) comme en production (104). |
| **Réactions** | Deux registres. Émojis (`ReactionDeMessage`, 6 : ❤️ 👍 🙏 😂 😮 🌱) : 3 poses en préprod, 0 en production. Source (`ReactionSemantique`, un **libellé en clair** pour clé). Elles sont 6 posables : Lumière (Je soutiens, Cela résonne, J'apprends) et Ombre (Je demande du concret, Je n'y vois pas clair, Je vois un masque). Les anciennes, retirées et renommées restent lisibles. 19 poses en préprod, dont 6 Ombre ; **0 en production**. |
| **Lecture** | `messaging_threads_users.last_seen_at`, par fil et par membre, posé sur un geste et jamais au rendu. « ✓✓ Lu » veut dire que tous les autres participants ont rouvert le fil depuis le message (`lu_jusqua_du_fil`, une requête par fil). |
| **Pagination** | `FilTronque` : les 30 derniers, ou le fil entier sur `?tous=1`. Pas de curseur. |
| **Temps réel** | Aucun (ni Turbo Stream, ni ActionCable) : la page se recharge. |
| **Préchargement** | `includes(:author, {reactions: :user}, messaging_message: :author)`. Les résonances ne sont **pas** préchargées : une requête par message. |
| **Notifications** | « Essentiel » (lot A) prévient des mentions et des réponses à MES messages, c'est-à-dire à l'auteur du message cité. |
| **Mémoire** | Entrées sur un message (#456, #457) ; la demande vise l'auteur. Une réponse est un message : mêmes règles. |
| **Regards** | Accord explicite par fil. Une réponse de regard est un message du fil. |
| **Progression** | E9 rang 2 lit « une résonance posée dans un espace rejoint », quel que soit son libellé : la palette peut changer sans toucher au jeu. |

## 1. Le total de réponses par message (contrat 1)

- **Un index** sur `messaging_messages.messaging_message_id`, et la **racine** de la discussion (§ 6), indexée elle
  aussi.
- **Une requête par page** (`GROUP BY racine`), et non une par message : le contrôleur pose `@nombres_de_reponses`
  (`{id de racine => n}`) dans `espaces#show` et `threads#show`.
- **Ce qui compte** : toutes les réponses de la DISCUSSION (réponses à une réponse comprises), sur tout le fil et
  pas seulement sur la page chargée.
- **Proposition** :
  - les réponses supprimées ne comptent pas ;
  - les réponses masquées non plus ;
  - les réponses de regard comptent (ce sont des contributions visibles). → **question 1**.

## 2. Le préchargement des résonances (contrat 2)

- `includes(reactions_semantiques: :user)` dans `espaces#show`, `threads#show` et `RenduDuMessage` : cela retire
  une requête par message.
- **Le total Source** compte les poses réelles, quel que soit leur libellé ; les libellés hérités (anciens,
  retirés, renommés) restent affichés sous leur nom d'origine dans le détail. → **question 2**.

## 3. Le format d'heure (contrat 3)

`time.formats.heure: "%H:%M"` dans `config/locales/fr.yml` : d'accord. Je le pose avec le lot 2.

## 4. « Aide vue » (contrat 4)

- **La clé** : `MarqueurDAttention` `aide-messagerie-vue`.
- **Le geste qui l'écrit** : `POST /messagerie/aide/vue` (JSON, 204), à la fermeture ou à la consultation de l'aide.
  Jamais au rendu.
- **La lecture** : `espaces#show` et `threads#show` posent `@aide_messagerie_vue`. L'aide reste accessible depuis
  « Aide de la messagerie ».

## 5. Les sept résonances (contrat 5)

**Le problème** : la clé d'une pose est aujourd'hui son **libellé en clair**. Changer « Je vois un masque » en « Cela
dévoile un masque » dans la base, ce serait précisément la requalification silencieuse que Codex interdit.

**Proposition** :
- **Une colonne `cle`** (stable), remplie par migration pour les libellés existants. Le `libelle` reste, comme
  mémoire de ce qui a été posé.
- **Le catalogue** :
  - Lumière : `soutiens`, `resonne`, `apprends` (inchangées) ;
  - Ombre : `plonger` (« Cela m'invite à plonger »), `devoile_un_masque` (« Cela dévoile un masque »), `inconfort`
    (« Merci d'oser l'inconfort ») ;
  - Source : `point_zero` (« Point Zéro — Fait circuler Ombre et Lumière »), sans titre séparé.
- **Les trois Ombre d'avant** (`concret`, `pas_clair`, `masque`) **prennent leur retraite** : lisibles sous leur
  libellé d'origine, plus posables, **jamais converties**. C'est le patron déjà en place pour `RETIREES`.
- **En production, il n'y a rien à convertir** : 0 pose, Ombre comprise. En préprod, il y a 6 poses de test.
- **Le Monde 0** : la Lumière et « Point Zéro » (Boris, 22 octobre : question 3 tranchée). La famille Ombre reste
  au Monde 1.
- **Les bancs à suivre** : `verifier_reactions_ombre`, `verifier_palette_monde_0`. E9 et `ExperienceState` ne
  lisent pas le libellé.

## 6. La discussion liée (contrat 6)

- **Une colonne `racine_id`** (indexée) : la racine de la discussion.
  - Une réponse à une réponse garde la racine de son parent, et **`messaging_message_id` reste le message cité
    précisément** (la citation).
  - Une seule discussion par racine, sans imbrication.
  - Le rattrapage est trivial : 0 réponse aujourd'hui.
- **La liste paginée** des réponses d'une racine : `GET /messages/:id/discussion` (JSON, 20 par page, ordre
  chronologique, curseur `apres=<id>`).
  - Le droit est celui de lire le fil, sinon 404.
  - Chaque réponse porte : `id`, `auteur`, `le`, `extrait` (texte brut), le message cité, et son état (supprimé,
    masqué).
- **Le parent** :
  - supprimé : la citation dit « Message supprimé », sans texte ;
  - masqué (regard) : « Réponse masquée » ;
  - hors de la page chargée : le lien rouvre le fil entier (`?tous=1#message-<id>`) ou la discussion ;
  - hors droit : impossible dans un même fil, dont les droits sont communs.
- **La projection chronologique** : une réponse est un message, à sa date dans le fil, avec sa citation (déjà
  préchargée). Un seul objet, un seul incrément. Le regroupement des réponses consécutives d'une même racine est
  une affaire de vue : `racine_id` le permet.

## 7. Les non-lus par discussion (contrat 7)

Codex : « lecture partielle sans saut ni marquage global des éléments cachés » ; « visibilité à 60 % = simulation
locale, pas une règle serveur ».

**Proposition** :
- **Une table `lectures_de_discussion`** (`user_id`, `racine_id`, `lu_jusqua`), écrite par un **geste** :
  `POST /messages/:id/discussion/lue` avec `de` et `jusqua`, la suite de réponses vue d'une traite.
- **Les non-lus d'une discussion** : les réponses d'autrui (regards compris), ni supprimées ni masquées, postérieures
  à `lu_jusqua`.
  - **Sans marqueur, un repère FIGÉ** : la première venue du membre dans le fil (`messaging_threads_users.created_at`
    — première lecture, premier message, ou première tournée de notification). ~~Le `last_seen_at` du fil~~ : il
    avance à chaque visite, et deux visites auraient éteint une discussion jamais ouverte (relecture de Codex).
  - **Un seul repère par discussion, jamais en arrière** (`GREATEST`). Il n'avance que si la suite vue commence au
    plus tard à la **première non lue** : un saut vers la fin n'avale pas la plage sautée (le geste répond 409). Choix
    prudent, dit : les réponses vues après un saut restent non lues tant que la plage n'a pas été parcourue.
- **Lire le fil ne marque pas les discussions** : pas de marquage global. → **question 4**.
- **Inchangés** : l'ouverture à la première non lue du FIL (`@derniere_lecture`, déjà là) et l'accusé « Lu »
  (niveau fil).

## 8. Ce qui ne bouge pas

- **La Mémoire V1** : une réponse est un message, avec les mêmes règles, le même consentement sur la version et la
  même reconfirmation.
- **Les regards** : l'accord par fil ; une réponse qui revient dans le flux n'élargit aucun droit.
- **La recherche** : les réponses sont des messages, déjà trouvées.
- **Les Omégas** : aucun.
- **Les notifications** : une réponse prévient l'auteur du message CITÉ, pas celui de la racine. → **question 5**.
- **L'export** ne cite pas les parents aujourd'hui. Hors de ce chantier, sauf demande.

## 9. Coût

**Par page de fil** : +1 requête (les totaux de réponses), +1 (les marqueurs de discussion), et une requête par
message en moins (le préchargement des résonances). Pas de temps réel : rien ne change de ce côté.

## 10. Questions

**Arbitrages de Boris (22 octobre 2026, au soir)** :
- **Les votes Ombre de test** (6, en préprod) sont **supprimés**. La production n'en a aucun. Le code garde
  néanmoins les trois anciens libellés LISIBLES, jamais convertis, au cas où une pose arriverait en production
  avant la promotion : aucune migration ne supprime de vote.
- **« Point Zéro » est posable dès le Monde 0** : la question 3 est tranchée. La famille Ombre reste au Monde 1.
- **Mes propositions avancent ; Codex relit** les questions 1, 2, 4 et 5, et je corrige s'il tranche autrement.

| # | Pour | Question | Proposition |
| --- | --- | --- | --- |
| 1 | Codex | Le total de réponses compte-t-il les réponses de regard ? les supprimées ? | regards oui, supprimées et masquées non |
| 2 | Codex | Le total Source compte-t-il les libellés hérités ? | oui : ce sont des poses réelles |
| 3 | Boris | Les trois Ombre d'avant : retraite lisible (aucune conversion), et « Point Zéro » dès quel Monde ? | retraite lisible : oui ; Point Zéro : **dès le Monde 0** (Boris) |
| 4 | Codex | Non-lus : marquer une discussion seulement en l'ouvrant, jamais en lisant le fil ? | oui |
| 5 | Codex | Une réponse à une réponse prévient l'auteur du message cité, et lui seul ? | oui |

**Relecture de Codex (22 octobre 2026, [la note](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/messagerie-hybride-relecture-codex-2026-10-22.md))** :
accord sur 1, 2 et 5 ; accord sur 4 avec trois corrections, appliquées au § 7 — la lecture vise les réponses
effectivement présentées, un saut n'avale rien, le repère initial est figé. Sur 5, « lui seul » vaut pour la
notification **de réponse** : les mentions et les autres réglages restent (c'était déjà le code, `EspaceMembership`
lit le message cité ; banc `verifier_discussions` § 7).

## 11. Lots proposés

- **Lot 2 (serveur)** :
  - l'index et `racine_id` (migration) ;
  - les totaux de réponses ;
  - le préchargement ;
  - le format d'heure ;
  - l'aide vue ;
  - les sept résonances (`cle`, catalogue, retraite des trois Ombre) ;
  - la discussion (`GET /messages/:id/discussion`).
- **Lot 3** : les non-lus par discussion (la table, le geste, les comptes).
- **Bancs** : un par contrat, et la recette de Codex (deux comptes, parent hors page et supprimé, réponse à une
  réponse, sept résonances et historique).

## 12. Servi en préprod (22 octobre 2026) — le contrat des vues

Lots 2 et 3 côté serveur, en préprod. Bancs : `verifier_discussions`, `verifier_resonances`,
`verifier_non_lus_discussion`, `verifier_aide_messagerie` (neufs), `verifier_reactions_ombre`,
`verifier_palette_monde_0` (suivis).

**Les pages de fil** (`espaces#show`, `threads#show`) posent :

| Variable | Forme | Usage |
| --- | --- | --- |
| `@nombres_de_reponses` | `{racine_id => n}` | le pied lit `@nombres_de_reponses[m.racine_id \|\| m.id].to_i` ; une racine sans réponse est ABSENTE (0). Sous une réponse, c'est le total de SA discussion (celle de sa racine), pas des réponses qui lui sont adressées (Codex) |
| `@non_lus_par_discussion` | `{racine_id => n}` | les non-lus de chaque discussion (§ 7) ; absente = 0 |
| `@aide_messagerie_vue` | booléen | l'aide de première visite se replie si vrai |

`RenduDuMessage` pose aussi `@nombres_de_reponses` pour un message rendu seul. Les résonances sont préchargées.

**Les résonances** :
- `ReactionSemantique.catalogue_pour(current_user)` → `[{cle:, libelle:, famille:}]`, dans l'ordre : les trois
  Lumière, les trois Ombre (Monde 1), `point_zero` (famille `:point_zero`). Au Monde 0 : Lumière et Point Zéro.
- La bascule : `basculer_reaction_semantique_path(m, cle: "plonger")`. `libelle:` reste accepté le temps du portage.
- Les poses héritées (`m.reactions_semantiques`) se lisent sous leur `libelle` d'origine ; `pose.cle`,
  `pose.famille`, `pose.retiree?` (vrai pour les trois Ombre d'avant et les anciennes retirées).
- `familles_pour` et `palette_pour` gardent leur forme d'avant (six offerts par la fenêtre d'avant) ; les dessins
  des trois nouvelles Ombre manquent (`_icone_reaction` ne rend rien pour elles).

**La discussion** — `GET /messages/:id/discussion` (`discussion_message_path(m)`, JSON ; `:id` peut être une réponse,
c'est sa racine qui répond) :
- `racine` et `reponses` : `{id, auteur, le, extrait, cite_id, cite_etat, etat, mien}` ; `etat` et `cite_etat` valent
  `"supprime"`, `"masque"` ou `null` — une réponse retirée garde sa place sans auteur ni texte ;
- `suivant` (curseur : `?apres=<suivant>`), `total` (celui du pied) ;
- `premiere_non_lue` (id ou `null`) et `non_lues` : la fenêtre s'ouvre sur la première non lue
  (`?apres=<la réponse d'avant>`).
- Lire n'écrit rien. Non-membre, message inconnu : 404.

**La lecture** — `POST /messages/:id/discussion/lue` (`lue_discussion_message_path(m)`), un GESTE, jamais au rendu :
- `de` et `jusqua` : la première et la dernière réponse **effectivement vues d'une traite** (la racine vaut pour le
  haut de la fenêtre ; `de` absent = `jusqua` seule) ;
- 204 si le repère avance ; **409** si la suite commence après la première non lue (un saut : rien n'est avalé) ;
- jamais en arrière ; limité à 120 par minute.

**L'aide vue** — `POST /messagerie/aide/vue` (`aide_messagerie_vue_path`) : 204, idempotente. Consultation ou
fermeture de l'aide, jamais le rendu.

**L'heure** — `l(m.created_at, format: :heure)` (`"%H:%M"`).
