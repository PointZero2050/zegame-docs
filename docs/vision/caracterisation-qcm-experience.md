# Caractérisation — moteur générique de QCM d'expérience

> Rédigé par Claude (instance bac à sable), 2026-08-02, en lecture seule sur `vibe.ze.game`
> (zegame-app, branche `pointzero`, tête gelée `5b4a875`). Cinquième pièce de caractérisation ;
> ferme la boucle des cinq modules d'évaluation annoncés dans
> [caracterisation-triptyque-monde-0.md](caracterisation-triptyque-monde-0.md) §1. Plus court
> que les précédents : ce module réutilise déjà les patrons documentés ailleurs (deux-écritures,
> version figée à la complétion) et n'ajoute que deux mécanismes vraiment nouveaux — le registre
> d'évaluateurs enfichables, et la sécurité contre la double-création en cas de course.

## 1. Ce qui est déjà documenté ailleurs, non répété ici

`ExperienceQuizAttempt#validate_challenge!` est le même patron « deux écritures » que les cinq
modules du triptyque ([caracterisation-progression-omega.md](caracterisation-progression-omega.md)
§4, [caracterisation-triptyque-monde-0.md](caracterisation-triptyque-monde-0.md) §1) — seule
différence mécanique : le Challenge est résolu par **FK directe** (`belongs_to :challenge`,
posée à la création) plutôt que par `Challenge.find_by(name: ...)`, plus robuste qu'un
rapprochement par titre éditorial. `definition_version` (figée à la création de la tentative)
suit le même principe que `flow_version` du Coupable idéal : une définition YAML modifiée après
coup n'est **jamais** réappliquée à une tentative déjà commencée ou complétée.

## 2. Un moteur générique, cinq expériences enfichées

Contrairement au triptyque (un modèle par bloc), `ExperienceQuizAttempt` est **un seul modèle
Rails** pour cinq expériences distinctes, différenciées par `quiz_key` :

```ruby
EVALUATORS = {
  "le-site-du-point-zero"      => "ExperienceQuizzes::SitePointZero",
  "la-chaine-invisible"        => "ExperienceQuizzes::ChaineInvisible",
  "le-schema-de-circulation"   => "ExperienceQuizzes::SchemaCirculation",
  "le-signe-de-reconnaissance" => "ExperienceQuizzes::SigneReconnaissance",
  "la-boussole-de-passage"     => "ExperienceQuizzes::BoussolePassage",
}.freeze
```

Chaque évaluateur (`app/services/experience_quizzes/*.rb`, modules purs, aucun état) implémente
**exactement deux méthodes**, le contrat d'extension complet :

- `answers_complete?(attempt)` — booléen, valide les réponses actuelles contre la définition
  YAML de ce quiz (jamais contre une définition en dur dans le code Ruby).
- `result_for(attempt)` — construit la restitution finale, **figée dans `attempt.result` à la
  complétion** (même principe de non-réévaluation rétroactive que partout ailleurs).

**Pas de DSL générique de validation** — commentaire explicite dans le code : « les règles
propres à chaque quiz vivent dans un évaluateur dédié, pas de DSL générique tant qu'une seconde
expérience n'a pas démontré quelles règles se répètent. » Un lot ultérieur (« lot B », 4 des 5
évaluateurs) a factorisé un `TypedFlow` commun une fois le besoin réel observé — **décision de
conception à respecter au portage** : ne pas anticiper une abstraction générique avant d'avoir
au moins deux implémentations concrètes à comparer.

**Exemple de validation d'entrée côté évaluateur** (`SitePointZero#normalize_lien`), à
reproduire pour toute saisie d'URL par un joueur : accepte un lien collé sans `https://` (les
navigateurs le retirent parfois en copiant depuis la barre d'adresse) et le restitue, mais
**rejette explicitement tout schéma étranger** (`javascript:`, `data:`, etc.) — jamais de
confiance aveugle dans une saisie libre transformée en lien cliquable.

## 3. Sécurité contre la double-création en cas de course

```ruby
def self.start_for(user, key:)
  ...
  draft.where(...).order(:created_at).last ||
    completed.where(...).order(:completed_at).last ||
    create!(...)
rescue ActiveRecord::RecordNotUnique
  draft.where(...).order(:created_at).last
end
```

Un **index unique partiel** (un seul brouillon par `[user, challenge, quiz_key]`) empêche deux
onglets ouverts simultanément de créer deux tentatives concurrentes ; le second `create!` échoue
avec `RecordNotUnique`, rattrapé pour **relire le brouillon gagnant** plutôt que de laisser
remonter une erreur 500 au joueur. Motif directement transposable à toute ressource « au plus une
ligne en cours par joueur » côté portage (contrainte d'unicité en base + `rescue` de relecture,
jamais une vérification applicative seule — vulnérable à la même course).

## 4. Ce que ce document ne couvre pas

- Le détail des 5 évaluateurs eux-mêmes (règles propres à chaque micro-expérience) — à
  caractériser séparément si le portage les atteint avant que ce document soit mis à jour.
- Le contenu YAML (`config/experience_quizzes/*.yml`) — catégorie A, déjà porté.

## 5. Vérification de parité recommandée

1. Compléter un quiz → Challenge validé, Oméga attribué une seule fois (rejouer ne le double
   jamais — `complete?` bloque, `validate_challenge!` ne revalide jamais un `ChallengesUser`
   déjà validé).
2. Simuler deux créations concurrentes du même brouillon (même joueur, même quiz) → une seule
   ligne en base, aucune erreur visible au joueur.
3. Soumettre un identifiant d'option absent de la définition YAML → réponse rejetée (§2), jamais
   une exception ni une donnée forgée acceptée dans `result`.
4. Coller une URL sans schéma → acceptée et normalisée en `https://` ; coller un schéma
   `javascript:`/`data:` → rejetée avec un message, jamais transformée en lien cliquable.
