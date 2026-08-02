# Caractérisation — authentification, rôles et autorisations

> Rédigé par Claude (instance bac à sable), 2026-08-02, en lecture seule sur `vibe.ze.game`
> (zegame-app, branche `pointzero`, tête gelée `5b4a875`). Deuxième pièce de la caractérisation
> catégorie B/transverse, après [caracterisation-progression-omega.md](caracterisation-progression-omega.md).
> Choisi en priorité parce que l'inventaire de portage note explicitement, après la fusion du
> schéma `User` (`c5b59a2`) : « Reste de l'étape : les autorisations (DSL Cans → vérifications
> de rôle), à faire au fil du portage des contrôleurs » — c'est transverse à tout ce qui se porte
> en ce moment, pas un module isolé qu'on peut reporter.

## 1. Authentification — rien de spécifique à caractériser

Devise standard : `database_authenticatable, registerable, recoverable, rememberable,
validatable, confirmable, trackable, omniauthable` (`google_oauth2`, `microsoft_office365`,
`apple`). Déjà noté dans l'inventaire de portage comme fusionné avec le `User` Devise de
`pointzero-app`. Seul point encore ouvert côté produit (pas technique) : conserver ou différer
l'OAuth au Festival (arbitrage Boris, toujours ouvert au 2026-08-02).

## 2. Rôles : un enum à trois valeurs, pas une hiérarchie

```ruby
enum :role, {dff: 1, admin: 2}, instance_methods: false, scopes: false
```

Trois états observables, `role` étant nullable :

| `role` | Méthode | Signification |
|---|---|---|
| `nil` | `has_no_roles?` vrai | joueur ordinaire |
| `"dff"` | `is_dff?` vrai | facilitateur — pouvoirs **scopés à ses communautés** (`dff_communities`, via le modèle de jonction `Dff{community_id, user_id}`) |
| `"admin"` | `is_admin?` vrai, **`has_all_abilities?` vrai** | accès total, court-circuite toutes les règles d'autorisation |

**Ce n'est pas une hiérarchie** (`admin` n'« inclut » pas `dff` par construction du code — c'est
`has_all_abilities?` qui lui donne un accès total, un court-circuit explicite, pas une addition
de permissions). Un DFF n'est jamais automatiquement admin, et son périmètre est **borné à la
liste de communautés** portée par `dffs` — pas par un attribut global.

Deux garde-fous d'intégrité liés au rôle DFF, déclenchés côté `User` (`before_save`/callbacks) :
`keep_only_good_communities` (les communautés d'un DFF sont retaillées à l'intersection de ses
`dff_communities` et des communautés par défaut — jamais une communauté hors de son périmètre) et
`ensure_dff_communities` (vide `dff_communities` si le rôle n'est plus `dff`).

## 3. Le moteur d'autorisation `Cans` — sémantique exacte

Fichier source : `mathieu_core/lib/mathieu_core/models/ability.rb` (74 lignes, reproduites
intégralement ci-dessous car chaque ligne compte pour un portage fidèle) :

```ruby
class AbilityBase
  def model(model) = (@current_model = model; yield; @current_model = nil)

  def no_roles(*actions, &block)
    first = actions.first
    @can_ance_no_roles[@current_model][first] = block || true
    actions[1..].each { |a| @can_ance_no_roles[@current_model][a] = ->(_, obj, **kw) { can? first, obj, **kw } }
  end
  # `roles` est l'exact miroir de `no_roles` sur @can_ance_roles. `all(*actions, &)` appelle les
  # deux (no_roles ET roles) avec le même bloc.

  def scope(&block) = (@can_scopes[@current_model] = block)

  def filter_scope(user, scope, kind = nil)
    return scope.all if user.has_all_abilities?
    model = scope.is_a?(ActiveRecord::Relation) ? scope.klass : scope
    @can_scopes[model].present? ? scope.instance_exec(user, scope, kind, &@can_scopes[model]) : []
  end

  def can?(action, obj, opts = {})
    return true if obj == :redirect_to
    return false if Current.user.nil?
    return true if Current.user.has_all_abilities?
    klass = obj.class
    klass = obj if [Class, Symbol].include?(klass)
    val = (Current.user.has_no_roles? ? @can_ance_no_roles : @can_ance_roles).dig(klass, action.to_sym)
    !val.nil? and (val == true or val.call(Current.user, obj, **opts) == true)
  end
end
```

Quatre points **non évidents**, chacun un piège potentiel s'ils ne sont pas reproduits :

### 3.1. Le dispatch se fait sur AVOIR ou NE PAS AVOIR de rôle, pas sur le rôle précis

`can?` choisit la table `@can_ance_no_roles` (joueurs, `role: nil`) OU `@can_ance_roles` (dff **et**
admin, indistinctement) selon `has_no_roles?`. **`roles(...)` ne distingue donc jamais un DFF
d'un admin** dans son bloc — c'est le bloc lui-même qui doit tester `user.is_admin?` s'il veut
une règle différente pour les deux (ex. `Community#show/edit/update` : `user.is_admin? or
user.dff_community_ids.include?(community.id)`). `all(...)` = `no_roles(...)` + `roles(...)`
avec le **même** bloc — donc le même comportement pour tout le monde, joueur ou DFF/admin
(charge alors au bloc de distinguer, ex. le `:nested` de `CircleMembership` : `user.id ==
m.user_id or user.id == opener_id or user.is_admin? or (...)`, un seul bloc, toutes les
casquettes gérées dedans).

### 3.2. Un seul bloc réel par groupe d'actions — les autres actions APPELLENT la première

`roles(:edit, :update, :destroy) { |user, obj| RULE }` n'enregistre **une vraie logique que pour
`:edit`**. `:update` et `:destroy` reçoivent chacun un lambda qui fait juste `can?(:edit, obj)` —
**ils rejouent la règle de la première action de la liste, ils n'ont pas leur propre logique**.
C'est utilisé partout dans `ability.rb` (ex. `Challenge` : `roles(:edit, :update, :destroy) {
user.is_admin? or user.dff_community_ids.include?(challenge.community_id) }` — trois actions,
une seule règle, aliasée). **Piège de portage** : si une seule des trois actions doit un jour
avoir une règle différente, il faut la sortir de la liste et lui donner son propre bloc — un
CanCanCan/Pundit qui définirait `:edit`, `:update`, `:destroy` séparément avec la MÊME expression
copiée-collée trois fois reproduit fidèlement le comportement actuel ; les redéfinir
indépendamment sans y penser ferait diverger un comportement aujourd'hui garanti identique.

### 3.3. Le retour doit être littéralement `true`, pas juste vrai

`val == true or val.call(...) == true` — un bloc qui renvoie une chaîne non vide, un objet, ou
tout autre truthy-mais-pas-`true` **refuse l'accès**, silencieusement (pas d'erreur). Tous les
blocs de `ability.rb` se terminent par des expressions booléennes strictes (`==`, `is_admin?`,
`.exists?`, `.any?`, `and`/`or`) — c'est cohérent partout, mais un nouveau bloc qui finirait par,
par exemple, `user.dff_communities.find_by(id: x)` (renvoie un `Dff` ou `nil`, pas un booléen)
casserait silencieusement l'autorisation même si l'intention était correcte.

### 3.4. `filter_scope` est fail-closed : `[]` si aucun scope déclaré (sauf admin)

Un modèle non couvert par un bloc `scope do ... end` dans `Ability` renvoie **une liste vide**
via `.cans`, jamais « tout » — sauf pour un admin (`has_all_abilities?` → `scope.all`). C'est
l'inverse du défaut habituel de CanCanCan (qui, sans `can :manage, :all` explicite, refuse aussi
— donc cohérent à reproduire, mais à vérifier explicitement modèle par modèle plutôt que supposer
un comportement par défaut permissif).

## 4. `authorize_resource` — le double contrôle, et son piège classe-vs-instance

Fichier source : `mathieu_core/app/controllers/concern/mathieu_base_application_controller.rb`,
méthode `authorize_resource` (citée en entier, c'est le point le plus dense du fichier) :

```ruby
def authorize_resource(opts = {})
  self.before_action opts do
    if params[:action]&.to_sym == :index or (params[:id].nil? and params[:action].to_sym != :create)
      unless association_chain.all? { |parent| can? :nested, parent }
        raise CanCan::AccessDenied
      end
    end
    unless can? params[:action]&.to_sym,
                ((params[:id] or is_current_action_resource?) ? resource : (params[:action] == :create ? build_resource : resource_class)),
                association_chain.index_by { |o| o.class... }
      raise CanCan::AccessDenied
    end
  end
end
```

**Deux contrôles distincts, dans cet ordre, à chaque requête** :

1. **`:nested` sur toute la chaîne de ressources parentes** (`association_chain` — les segments
   de route emboîtants, ex. `Journey → Challenge → ChallengesUser`), **sauf pour `:create`**.
   Ce contrôle porte sur de **vraies instances**, résolues par les `:id` réels de l'URL — c'est
   le point d'application fiable.
2. **`can?` sur l'action elle-même**, avec un objet dont la nature dépend de la forme de la
   route :
   - si `params[:id]` est présent, ou `is_current_action_resource?` est vrai → une **instance**
     réelle (`resource`) ;
   - sinon, si l'action est `:create` → l'objet **construit mais pas sauvegardé**
     (`build_resource`) ;
   - **sinon (typiquement une route imbriquée singulière `resource :x, only: [:show]`, sans
     `:id` dans l'URL et hors `:create`) → la CLASSE elle-même**, jamais une instance.

**C'est le piège découvert et corrigé en production le 2026-08-01** (`analyse-impact-messagerie-cercles.md`
§0, correctif `7d533fb`) : `ThreadsController#show` est monté en `resource :threads, only:
[:show]` sous `journeys/:id/challenges/:id/challenges_users/:id/threads` — le fil lui-même n'a
pas d'`:id` propre dans l'URL (c'est le `ChallengesUser` parent qui en a un), donc
`authorize_resource` invoque `can?(:show, Messaging::Thread)` **avec la classe**, pas
l'instance du fil consulté. Une règle `:show` écrite en supposant recevoir une instance
(`thread.container...`) plante (`NoMethodError` sur la classe) ou, pire, refuse tout le monde
silencieusement si on la protège maladroitement. **Le vrai point d'application pour cette forme
de route est le contrôle `:nested` (étape 1 ci-dessus), déjà fait sur de vraies instances** — la
règle `:show` du modèle final peut rester large (`all(:show)`) tant qu'elle sait détecter
qu'on lui passe une classe (`!thread.is_a?(Messaging::Thread) or ...`) et laisser passer dans ce
cas, en s'appuyant sur le fait que le vrai contrôle a déjà eu lieu.

**Recommandation de portage** : ce piège n'est pas propre à `mathieu_core` — c'est un cas général
de « autorisation appliquée à une route sans ressource identifiée dans l'URL, mais où
l'utilisateur peut quand même accéder à une donnée précise via un objet imbriqué ». En
CanCanCan/Pundit, la même faute reste possible si l'`:id` de la ressource finale n'apparaît nulle
part dans l'URL : vérifier explicitement, pour **chaque** route imbriquée singulière du nouveau
routeur, quelle instance (ou classe) est effectivement transmise au moment de l'autorisation.

## 5. Le piège du « partage de communauté » — leçon générale de l'incident du 2026-08-01

Plusieurs règles de `ability.rb` s'appuient légitimement sur le partage d'une communauté
(`user.community_ids & other.community_ids`) — **c'est correct quand l'appartenance à la
communauté est elle-même restrictive** (ex. une communauté non par défaut, à laquelle on
n'accède que sur invitation). C'est devenu une faille exactement dans le cas contraire : la
règle `:nested` de `ChallengesUser`/`JourneysUser` s'appuyait sur le partage d'une communauté
**par défaut** (Monde 0, Monde 1) — or **tout joueur rejoint automatiquement toutes les
communautés par défaut** (`User#join_default_communities`, `after_create_commit`). Le test
« partage une communauté » devenait donc toujours vrai entre deux joueurs quelconques,
transformant une règle qui semblait restrictive en un accès universel de fait.

**Règle de vigilance pour le portage** : avant de porter une règle d'autorisation basée sur une
communauté partagée, vérifier si cette communauté est réellement sélective (adhésion volontaire,
invitation, capacité limitée) ou si elle est de facto universelle (communauté par défaut,
rejointe automatiquement). Le correctif appliqué partout dans la série P0→P3 remplace le partage
de communauté par une **participation explicite** (candidat, ouvreur, ou — sous consentement
explicite et borné — membre actif d'un groupe à taille fixe comme un Cercle de 5 à 8 personnes).

## 6. Ce que ce document ne couvre pas

- Les scopes précis par modèle (qui voit quoi dans les listes admin) — `ability.rb` en contient
  une douzaine, chacun avec sa propre règle de filtrage DFF/communauté ; à consulter directement
  dans le fichier source cité plutôt que dupliqués ici, le risque de désynchronisation étant plus
  grand qu'une copie ponctuelle.
- La messagerie (catégorie C, entièrement couverte par les analyses et commits P0→P3).
- Les autorisations spécifiques aux Cercles au-delà de `CircleMembership#:nested` (déjà
  documentées dans `analyse-impact-messagerie-cercles.md` et les commits du 2026-08-01).

## 7. Vérification de parité recommandée

1. Un joueur ordinaire (`role: nil`) ne peut ni éditer ni voir le profil d'un autre joueur, sauf
   lui-même (§2, §3 — `User#nested`/`#sse`).
2. Un DFF ne voit et n'édite que les objets de ses propres communautés (`dff_communities`), même
   sur les modèles où le rôle `dff` a des pouvoirs (Challenge, Journey, Skill, Group, User) — un
   DFF de la communauté A ne doit jamais agir sur un objet de la communauté B.
3. Un admin passe tous les contrôles, y compris sur des objets hors de toute communauté qui lui
   serait rattachée (`has_all_abilities?`).
4. Une route imbriquée singulière sans `:id` propre dans l'URL (typiquement un « mon X du
   contexte Y ») ne doit jamais reposer uniquement sur une règle testée avec une instance — le
   test doit vérifier explicitement le comportement quand seule la classe est disponible (§4).
5. Aucune règle d'autorisation ne doit se satisfaire du partage d'une communauté rejointe
   automatiquement à l'inscription (§5) — reproduire le test négatif « deux joueurs distincts,
   aucun lien explicite, la communauté seule ne suffit pas » sur chaque nouvelle règle sensible.
