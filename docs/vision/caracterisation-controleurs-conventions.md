# Caractérisation — conventions et pièges de la couche contrôleurs

> Rédigé par Claude (instance bac à sable), 2026-08-02, en lecture seule sur `vibe.ze.game`
> (zegame-app, branche `pointzero`, tête gelée `5b4a875`). Sixième pièce de caractérisation,
> choisie parce que le portage catégorie B vient de franchir les modèles (commit `eb96d00`,
> côté `pointzero-app`) et s'apprête à attaquer **les contrôleurs et les vues** — exactement la
> couche que ce document couvre. Complète
> [caracterisation-auth-roles-autorisations.md](caracterisation-auth-roles-autorisations.md)
> (qui couvre `authorize_resource`/`Ability`) par trois mécanismes transverses supplémentaires et
> un patron d'architecture partagé par les quatre contrôleurs d'évaluation du Monde 0.

## 1. Locale : détection navigateur, jamais une préférence stockée

```ruby
# app/controllers/application_controller.rb
load_defaults default_language: Rails.env.local? ? :fr : :browser
```

```ruby
# mathieu_core — load_defaults (extrait)
def get_browser_lg
  @browser_lg ||= (request.env['HTTP_ACCEPT_LANGUAGE'].to_s.split(',').map do |lang|
                     l, q = lang.split(';q='); [l.to_sym, -(q || 1).to_f]
                   end.sort_by(&:last).map(&:first) & [:en, :fr]).first
end

def load_defaults(default_language: :en, default_timezone: "Paris")
  ...
  default_language_calculated = (default_language == :browser ? (get_browser_lg || :en) : default_language)
  I18n.locale = if Rails.env.test?
                 default_language_calculated
               elsif current_user
                 $global_vars.vars.dig(:languages, current_user.try(:language_id), :short) || default_language_calculated
               else
                 default_language_calculated
               end
end
```

Trois faits précis, chacun surprenant si on ne lit que l'usage superficiel :

1. **Seules `:fr` et `:en` sont jamais retenues** (`& [:en, :fr]`) — un `Accept-Language`
   annonçant n'importe quelle autre langue en tête ne change rien, l'intersection l'élimine.
2. **Un mécanisme de préférence de langue *par utilisateur* existe dans `mathieu_core`**
   (`current_user.language_id` → `$global_vars.vars.dig(:languages, ..., :short)`) **mais est
   mort dans cette application** : `User` ne porte **aucune colonne `language_id`** (vérifié —
   absente de `User.column_names`), donc `current_user.try(:language_id)` renvoie toujours
   `nil` et le code retombe systématiquement sur la détection navigateur. Ne pas confondre
   « le mécanisme n'existe pas » et « le mécanisme existe mais n'est jamais nourri » — le second
   est le cas réel, pertinent si le portage envisage un jour un vrai réglage de langue.
3. **En environnement local (`Rails.env.local?`), la langue est forcée à `:fr`**, sans même
   consulter le navigateur — un client HTTP qui n'envoie pas d'en-tête `Accept-Language` (script
   de test, `rails runner` + requête d'intégration) obtient l'anglais **en production**, jamais
   en local. Toute vérification HTTP automatisée contre `vibe.ze.game` doit envoyer
   `Accept-Language: fr-FR,fr` explicitement, sous peine de faux diagnostic de régression de
   traduction (piège déjà rencontré, désormais systématique dans les scripts de vérification de
   ce projet).

## 2. `Slugable` : `find` accepte slug ET id, `find_by` non

Fichier source : `mathieu_core/lib/mathieu_core/models/concerns/slugable.rb`. `slugable_with_slug`
redéfinit **`find`** — sur la classe, sur sa relation, et sur sa relation d'association (trois
redéfinitions distinctes, Rails ayant trois classes différentes pour ces contextes) :

```ruby
FIND_BLOCK = ->(attr_or_id, key) do
  (attr_or_id.to_i.to_s == attr_or_id.to_s) ? find_by!(id: attr_or_id) : find_by!(key => attr_or_id)
end
```

Un argument qui « ressemble » à un entier (`"42".to_i.to_s == "42"`) est traité comme un id ;
sinon, comme un slug. **Seul `find` est concerné — jamais `find_by`, qui reste le comportement
Rails standard.** `find_by(id: params[:x])` avec un slug en valeur ne trouve donc jamais rien,
**silencieusement** (`nil`, pas d'exception) — piège déjà rencontré en production (contrôleur
F2b « Passer cette étape », qui redirigeait vers son chemin d'échec, indiscernable d'un succès,
jusqu'à correction en `find`). **Règle de portage** : partout où la source appelle `Model.find`
sur un modèle `slugable_with_slug`, le remplacement doit accepter les deux formats (id ou slug)
— ne jamais le réduire à un simple `find_by(id:)`, qui casserait silencieusement toute URL
construite avec un slug.

Détails de génération utiles si le portage réimplémente le même confort d'URL (`friendly_id`,
déjà prévu au cadrage, a une sémantique proche mais pas identique — vérifier au cas par cas) :
slug dérivé de `#name` par défaut, régénéré uniquement si le nom change
(`should_generate_new_slug?`), collision ou mot réservé (`new`, `edit`, `first`, `last`,
`current`, `me`, `mine`, ou une chaîne purement numérique) → id ajouté en suffixe ; repli sur un
UUID si aucun candidat ne se libère.

## 3. Listes blanches de params imbriqués — silencieuses, pas des erreurs

```ruby
# Admin::JourneysController
strong_parameted [:name, :photo, ..., :progression_mode, :mandatory, ...,
  challenges_journeys_attributes: [:id, :_destroy, :position, :challenge_id, :required, :optional_note],
  pages_attributes: [:id, :_destroy, :position, :name, :content, :challenge_id, :image, :image_cache, :remove_image]]
```

`accepts_nested_attributes_for` (Rails standard) exige une liste blanche de champs **par
association imbriquée**, explicitement énumérée dans chaque contrôleur admin. Un nouveau champ
ajouté au modèle (migration comprise) et absent de cette liste est **silencieusement ignoré** au
formulaire — la sauvegarde « réussit », sans qu'aucune erreur ne signale que ce champ n'a jamais
été écrit. Même classe de panne qu'un `.create` sans le `!` qui lèverait une exception. **Au
portage, vérifier cette liste avant de déboguer une vue** qui semble ne pas persister une
valeur, et à chaque nouveau champ ajouté aux modèles imbriqués (`ChallengesJourney`, `Page`),
mettre à jour la liste blanche du contrôleur admin correspondant dans le même geste que la
migration.

## 4. Le patron PRG partagé par les quatre contrôleurs d'évaluation

`ConseilOmegaController`, `DroleEpoqueController` (Bloc 1), `CoupableIdealController` et
`ExperienceQuizzesController` sont écrits en miroir les uns des autres (commentaires croisés
explicites dans le code — « Flux PRG (une requête par écran), à l'image de
`ConseilOmegaController` », « Mirroir de `DroleEpoqueController#load_assessment` »). Un seul
patron, à reproduire une fois pour toute nouvelle évaluation plutôt que quatre fois :

- **`before_action` unique de chargement de session** (`load_session`/`load_assessment`) :
  reprend une passation `in_progress`, sinon réaffiche la dernière `completed` (permet aux
  boutons de rétention de l'écran final de recharger la page en GET sans en créer une
  nouvelle), sinon en crée une neuve. Toujours **une ligne active par joueur à la fois** pour un
  module donné (renforcé par un index unique partiel côté `ExperienceQuizAttempt`, §3 de
  [caracterisation-qcm-experience.md](caracterisation-qcm-experience.md)).
- **`GET #show`** résout l'écran courant depuis `current_step`/`current_section` (jamais depuis
  un paramètre d'URL librement choisi par le client) et le rend.
- **`POST` par écran** valide la réponse, l'enregistre (`store_answer`), puis avance
  (`goto!`/`advance!`) et **redirige** (jamais un rendu direct après écriture — le P du PRG).
  C'est ce même canal qui, sur l'écran final, déclenche `complete!` et donc la validation
  Marelle (déjà caractérisée : [progression/Oméga](caracterisation-progression-omega.md) §4,
  [triptyque Monde 0](caracterisation-triptyque-monde-0.md) §1).
- **`current_step`/`current_section` fait foi côté serveur**, jamais côté client — un joueur ne
  peut pas sauter un écran en modifiant l'URL ou en rejouant un POST avec un `step` arbitraire ;
  au mieux il resoumet le même écran (idempotent par construction, `store_answer` fusionne dans
  `answers` sans jamais purger les réponses déjà enregistrées).

## 5. Ce que ce document ne couvre pas

- Le détail des vues HAML (catégorie A, déjà porté).
- Les mécanismes propres à `Ability`/`authorize_resource` (couverts en profondeur par
  [caracterisation-auth-roles-autorisations.md](caracterisation-auth-roles-autorisations.md)).
- Hotwire/turbo-frame (`embedded_frame_layout`, `is_embedded_frame?`) — plomberie de rendu liée
  à `mathieu_core`, non caractérisée ici faute de savoir si la pile cible en a l'équivalent ; à
  documenter séparément si le portage en a besoin.

## 6. Vérification de parité recommandée

1. Une URL contenant un slug résout le même enregistrement qu'une URL contenant son id — pour
   tout modèle qui portait `slugable_with_slug` côté source (§2).
2. Un client de test qui n'envoie pas `Accept-Language` obtient la langue attendue selon
   l'environnement (locale forcé en dev/test, anglais par défaut en prod si aucune préférence
   ne matche) — ne pas prendre un tel résultat pour une régression de traduction sans vérifier
   l'en-tête envoyé.
3. Ajouter un champ à un modèle porté par des attributs imbriqués sans mettre à jour la liste
   blanche du contrôleur correspondant → la valeur ne doit **jamais** apparaître silencieusement
   absente en production ; si le portage garde le même mécanisme Rails, prévoir une revue
   systématique des listes blanches à chaque migration touchant un modèle imbriqué.
4. Sur un des quatre modules d'évaluation : soumettre un POST avec un `step`/`section` arbitraire
   différent de `current_step` → n'affecte pas la progression réelle, qui reste pilotée par
   l'état serveur.
