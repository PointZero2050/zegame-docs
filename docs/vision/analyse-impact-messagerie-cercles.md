# Analyse d'impact — Profil communautaire et messagerie des Cercles (P0)

> Ajout Claude - 2026-07-31. Répond à l'analyse d'impact obligatoire exigée par
> [Profil communautaire et messagerie des Cercles — V1](profil-communautaire-messagerie-cercles-v1.md)
> § 12, avant tout code. Méthode : audit en lecture seule du code et de la base de production de
> `vibe.ze.game` (aucune écriture, aucun envoi de mail réel). Les faits cités — code source exact,
> colonnes, volumétries — ont été vérifiés sur le serveur et sur la révision réellement chargée des
> deux gems (`mathieu_core` `c193dd17`, `mathieu_core_messaging` `7bda7513`), pas déduits de leur
> documentation.

## 0. Constat prioritaire — faille d'accès déjà en production

**Indépendamment de tout ce qui suit, `Messaging::Thread` n'a aucune restriction de lecture ou
d'écriture liée à la participation.** `app/models/ability.rb:266-272` :

```ruby
model Messaging::Thread do
  all(:show, :index)          # <- inconditionnel : accordé à TOUT utilisateur connecté
  all(:sse) do |user, thread| can? :nested, thread.container end
end
```

La seule protection réelle vient aujourd'hui du droit `:nested` sur le conteneur
(`ChallengesUser`/`JourneysUser`), vérifié dans les routes imbriquées. Or ce droit est bien plus
large qu'il n'y paraît (`app/models/ability.rb:106-109`) :

```ruby
roles(:nested) do |user, cu|
  (user.community_ids & cu.user.community_ids).any? or
  (user.community_ids & cu.challenge.journeys.joins(:community).pluck("communities.id")).any?
end
```

Tout joueur appartient de fait aux deux communautés `default: true` (Monde 0 #15, Monde 1 #26,
`join_default_communities` — voir analyse Cercles § C1). **`user.community_ids & cu.user.community_ids`
n'est donc quasiment jamais vide entre deux joueurs quelconques.** Concrètement : n'importe quel
joueur connecté qui construit ou devine l'URL `/journeys/:jid/challenges/:cid/challenges_users/:id/threads`
d'un AUTRE joueur accède à son fil — y compris son thread de Graine de fin de chapitre — et peut y
écrire, `Messaging::Message` n'exigeant que `can? :show, message.thread` (donc la même absence de
garde). Vérifié : `messaging_threads_users` (150 lignes) n'enregistre que des marqueurs de lecture
(`mark_as_read!`), jamais une liste de participants autorisés — il n'existe **aucune** notion de
participation explicite dans le modèle actuel, alors que c'est précisément ce que suppose déjà
`receive_message_extra` pour la validation par facilitateur.

Cette faille est **antérieure à tout travail Cercles** et touche le système de Graines/feedback
déjà en production (67 fils, 86 messages). Elle n'est pas provoquée par la nouvelle spec — la
spec l'a fait apparaître en exigeant explicitement l'audit du § 8.2. Je ne l'ai pas corrigée : une
règle `:nested` aussi large a peut-être une raison d'être (accès DFF/support) que je ne connais pas,
et la resserrer sans le bon niveau de garantie pourrait casser un usage légitime. **Correctif
recommandé pour P0** : remplacer `all(:show, :index)` par une vérification de participation
explicite (§ 5 ci-dessous), qui est de toute façon un prérequis non négociable pour les fils de
Cercle (dossier de rencontre, coordonnées).

## 1. Modèles Cercles récemment implémentés et leurs statuts

Rappel de C2 (`Circle`, `CircleCycle`, `CircleMembership`, `PactSourceVersion`, `CircleSession`,
aucune macro `mathieu_core`). `CircleMembership.status` : `demande` / `actif` / `refuse` / `parti`
— c'est le statut le plus proche du `Membership / JoinRequest / Invitation` que la spec (§ 9)
demande de faire converger vers UN cycle d'états. État actuel en production : 1 demande en
attente, aucun fil de messagerie qui y soit encore rattaché — **aucune donnée à migrer sur ce
point**, ce qui simplifie beaucoup le choix du § 3.

## 2. `Messaging::Thread` / `Message` / `ThreadsUser` / `Mention` — schéma exact

| Table | Colonnes vérifiées |
|---|---|
| `messaging_threads` | `id, name, container_type, container_id, created_at, updated_at, photo, kind:enum` |
| `messaging_messages` | `id, message:text, messaging_thread_id, messaging_message_id, author_type, author_id, created_at, updated_at` |
| `messaging_threads_users` | `id, messaging_thread_id, user_id, last_seen_at, last_notified_at, created_at, updated_at` |
| `messaging_mentions` | `id, mentionnable_id, mentionnable_type, context_type, context_id, hardcoded, created_at, updated_at` |

Volumétrie : 67 threads (5 `JourneysUser`, 62 `ChallengesUser` — aucun autre type), 86 messages,
150 `threads_users`, **0 mention** (jamais utilisées), **0 `last_notified_at` renseigné** (voir § 4).

`container` est polymorphe et **`optional: true`** sur `Thread` — un fil sans conteneur est
possible côté schéma. `Thread` expose un contrat d'extension que le conteneur peut implémenter
(`try`/`respond_to?`, donc jamais obligatoire) :

```text
receive_message_extra(message, extra)      # déjà utilisé par ChallengesUser/JourneysUser
notify_of_new_message(message)             # non implémenté nulle part dans l'app
thread_search_includes(users)              # non implémenté
thread_has_mentions?(thread)                # non implémenté (défaut GlobalSettings: true)
mentionnable_users(thread)                  # non implémenté (défaut: thread.users)
allowed_hardcoded_mentions                  # non implémenté (défaut: [{text:"all", slug:"__all"}])
to_message_partial_path                     # non implémenté (défaut: "messaging/messages/box")
```

Aucun conteneur actuel ne personnalise le rendu des messages ni les mentions : la vue générique
`messaging/messages/_box` (fournie par la gem, jamais surchargée par l'app) suffit déjà pour tous
les cas. **Aucun travail requis sur ce point pour les Cercles.**

## 3. Conteneur unique du fil — décision proposée

La spec (§ 9) demande de choisir le conteneur unique. Constat : `Thread#resource` côté
`ThreadsController` (§ 6) fait `parent.thread || parent.build_thread(...)` — un **`has_one`**, donc
un conteneur = au plus un fil. C'est exactement la forme d'un `CircleMembership` : une ligne par
(joueur, cycle), qui porte déjà `status`. C'est cette ligne qui doit devenir le conteneur du fil de
mise en relation — pas un nouvel objet `JoinRequest` séparé, pour éviter la double-source-de-vérité
que la spec § 8 interdit explicitement (« ne pas transformer un `CircleMembership` accepté en objet
temporaire de candidature sans préserver son historique »).

**Recommandation** : ajouter `has_one :thread, as: :container, dependent: :destroy` à
`CircleMembership`, et `receive_message_extra` minimal (même motif que `ChallengesUser`) pour, à
terme, permettre les actions métier `Accepter`/`Refuser` déclenchées depuis le fil sans dupliquer
un second canal d'action (bouton API + bouton dans le fil). Le statut reste porté par
`CircleMembership#status`, jamais déduit du contenu d'un message — conforme à la spec § 4.2 et au
critère d'acceptation n°8.

## 4. Notifications e-mail — n'existent pas aujourd'hui, à construire entièrement

`Thread#send_mail_notif` planifie un job Solid Queue déduplifié (`GenericJob`, fenêtre de 10 min)
qui appelle in fine `GlobalSettings.try(:send_mail_notif_for_thread, self, user, kind)`.
**`GlobalSettings.send_mail_notif_for_thread` n'est défini nulle part** : ni dans la classe de base
(`mathieu_core/lib/.../global_settings.rb`, qui ne définit que `default_has_mentions?`,
`default_hardcoded_mentions`, `notify_new_mention`, `searched_models`), ni par une surcharge dans
l'app hôte (recherche exhaustive : zéro occurrence de `GlobalSettings` dans `app/`, `config/`,
`lib/`). Le `.try` avale l'appel silencieusement. Confirmé par la donnée :
**`messaging_threads_users.last_notified_at` n'a jamais été renseigné sur les 150 lignes
existantes.**

Conséquence directe : **aucun mail de notification n'a jamais été envoyé pour un fil, Graine ou
validation, en production.** Ce n'est pas une régression à craindre — c'est une fonctionnalité à
bâtir de zéro pour satisfaire les § 5/§ 6 de la spec (critère d'acceptation n°5). Périmètre : une
classe `GlobalSettings` hôte (ou un monkey-patch documenté) définissant `send_mail_notif_for_thread`,
un mailer sobre (identité d'expéditeur, type de demande, nom du Cercle, lien profond — jamais le
contenu), et le job Solid Queue existant suffit déjà comme mécanisme de déduplication.

## 5. Vues d'index/show — hard-codées Challenge/Journey, exactement comme prévenu par la spec § 8.1

`ThreadsController` (app hôte, `app/controllers/threads_controller.rb`) :

- `#collection` : la clause `if parent.is_a? User ... elsif parent.is_a? Community ... else raise
  RoutingError` ne connaît que deux origines de fils, `JourneysUser` et `ChallengesUser`, combinées
  par des `.or()` explicites. Un commentaire du code original (« *A clarifier avec Hervé parce que
  c'est n'imp* ») signale que l'auteur lui-même considérait cette méthode fragile.
- `before_action only: :show { @__hotwire_title_show = (@challenge || @journey).name }` — plante
  (`NoMethodError` sur `nil.name`) si le fil affiché n'a ni `@challenge` ni `@journey`.
- `app/views/messaging/threads/index.html.haml` : `real_container.is_a?(ChallengesUser) ?
  real_container.challenge : Journey...find(real_container.journey_id)` — même hypothèse binaire.

**Aucun de ces trois points n'expose de risque immédiat pour un fil de `CircleMembership`** : comme
`#collection` ne référence que `JourneysUser`/`ChallengesUser`, un fil de Cercle ne remontera
simplement jamais dans l'index actuel plutôt que de le faire planter. Mais cela signifie aussi que
**la Boîte d'échanges unifiée que demande la spec (§ 10) n'existe pas tant que ces trois points ne
sont pas rendus polymorphes** — c'est un vrai chantier, pas une extension mineure. Recommandation :
introduire une petite interface de conteneur (`titre_fil`, `url_fil`, `libelle_contexte`) que
`ChallengesUser`, `JourneysUser` et `CircleMembership` implémentent chacun, et faire porter
`#collection` et la vue sur cette interface plutôt que sur des `is_a?` en cascade — sans toucher au
comportement existant pour les deux types déjà en production (nécessite un test de non-régression
explicite avant/après, § 8).

## 6. Routes

Aujourd'hui : `/users/:id/threads` (index), `/communities/:id/threads` (index),
`/journeys/:jid/journeys_users/:id/threads` (show, singulier), `/journeys/:jid/challenges/:cid/
challenges_users/:id/threads` (show, singulier). Aucune route générique `/threads/:id`. Pour les
Cercles : nouvelle route imbriquée sous `cercles`, par exemple `resource :threads, as:
'messaging_thread', only: [:show]` sous `circle_memberships` (ou directement sous l'action
`demander`/`decider` déjà existante dans `CerclesController`) — cohérent avec le motif déjà en
place, pas une nouvelle convention.

## 7. `Ability` — droits sur conteneurs, participants, profils, communautés

Voir § 0 pour `Messaging::Thread`/`Message`. Il n'existe **aucune règle `Ability` pour `Circle`,
`CircleCycle`, `CircleMembership`, `PactSourceVersion` ou `CircleSession`** — `CerclesController`
ne fait pas `authorize_resource` (contrôleur plat, comme `RessourcesController`) et vérifie les
droits à la main (`ouvreur?`, `membre_actif?`). C'est cohérent avec le choix déjà pris de ne pas
faire hériter ces modèles de la grammaire `mathieu_core` — mais cela signifie que le futur droit
d'accès au fil (§ 8.2 de la spec) devra être vérifié dans `CerclesController`/un futur
`ThreadsController` dédié aux Cercles, pas dans `app/models/ability.rb`, pour rester cohérent avec
le reste du modèle Cercle.

## 8. `User`, Profil, Oméga, Puissances, badges, Contributions, Graines, Résonances

Confirmé par introspection : **`Badge`, `Contribution` et `Resonance` n'existent pas** (`Object.
const_defined?` négatif pour les trois). La section « Ce que je contribue » du profil communautaire
(§ 3.2) suppose des objets qui n'existent pas encore — ce n'est pas un périmètre P0, c'est tout le
Lot P1. Une Graine reste aujourd'hui un simple message dans un thread de fin de chapitre (voir
analyse Cercles/Intercycle § 5) : aucune notion de visibilité par cercle ni de sélection volontaire
pour un profil, exactement ce que la spec signale déjà comme non couvert.

## 9. Cascades de suppression

`ChallengesUser`/`JourneysUser` ont `has_one :thread, ..., dependent: :destroy` ; `Messaging::
Thread` a `has_many :messages, dependent: :destroy` et `has_many :threads_users, dependent:
:destroy`. La chaîne est propre dans les deux sens : détruire un `ChallengesUser` détruit son fil et
ses messages ; rien côté `Thread` ne détruit son conteneur. Pour `CircleMembership`, ajouter le même
`has_one :thread, dependent: :destroy` reproduit ce motif sans surprise. Point de vigilance
explicite de la spec (critère n°10, § 8) : la fermeture d'un fil ne doit jamais entraîner la
suppression silencieuse d'une adhésion — respecté tant que la relation reste `CircleMembership →
Thread` (détruire le fil ne détruit pas l'adhésion) et non l'inverse.

## 10. Historique déjà créé

1 `CircleMembership` en statut `demande` (Julien, compte de test) en production au moment de cet
audit, sans fil associé. Aucune migration de données nécessaire pour ce point précis.

## 11. Journalisation, blocage, signalement, export, suppression

**Rien n'existe** (`Block`, `Report`, `Signalement` : aucun défini). Le § 6 de la spec range
volontairement ces sujets en P3 (« Reporté ») à l'exception d'un strict minimum P0 : « signalement
minimal vers l'administration si le mécanisme existe déjà, sinon journalisation et contact support
clairement indiqué ». Comme rien n'existe, le P0 se limite à afficher un contact support explicite
dans le fil — pas de nouvel objet métier.

## 12. Stratégie de migration et retour arrière

- Tables neuves uniquement pour tout ce qui précède (pas de colonne ajoutée à `messaging_threads`
  côté app). Retour arrière = drop des tables ajoutées.
- Le correctif `Ability` du § 0, s'il est validé, doit être accompagné de tests négatifs explicites
  (un joueur A ne peut ni afficher ni écrire dans le fil d'un `ChallengesUser` de B, même partageant
  une communauté par défaut) rejoués sur les 67 fils existants pour vérifier l'absence de
  régression sur les usages légitimes (DFF, admin, auteur).
- Aucun envoi de mail réel ni migration de données de production sans autorisation explicite de
  Boris — conforme à la clause finale de la spec § 12.

## 13. Ce que cette analyse ne tranche pas

- Le périmètre exact du correctif `Ability` (qui, au juste, doit légitimement voir le fil d'un
  autre : DFF de la même communauté ? Admin seul ?) — nécessite un arbitrage produit, pas une
  déduction technique.
- La forme exacte de l'interface de conteneur polymorphe (§ 5) — plusieurs découpages raisonnables
  existent, à trancher au moment du code plutôt que figés ici.
- Tout ce qui relève de P1 (profil communautaire) et au-delà : hors périmètre de ce P0.
