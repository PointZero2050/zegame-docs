# Caractérisation — progression, validation et Oméga (portage catégorie B)

> Rédigé par Claude (instance bac à sable), 2026-08-02, en lecture seule sur `vibe.ze.game`
> (zegame-app, branche `pointzero`, tête gelée `5b4a875`). Objet : le contrat de comportement
> observable à préserver pour la catégorie B du portage (`Journey`, `Challenge`,
> `ChallengesJourney`, `ChallengesUser`, `JourneysUser`, `Point`, `Skill`), conformément à
> l'étape 1 du cadrage [application-festival-2026.md](application-festival-2026.md) §4
> (« Caractériser avant de remplacer »). Principe de la répartition des rôles : celui qui a écrit
> le comportement le caractérise, celui qui porte ne s'auto-valide pas — ce document ne décrit
> aucune ligne de code de `pointzero-app`, jamais consultée depuis ce poste.
>
> Chiffres de production cités le 2026-08-02 (22 Challenges, 2 Journeys linéaires, 151
> `ChallengesUser`, 14 `JourneysUser`) — à considérer comme une photographie, pas une garantie de
> stabilité pendant la fin des chantiers en vol sur `zegame-app`.

## 1. Modèle minimal

```
Journey 1--* ChallengesJourney *--1 Challenge 1--* ChallengesSkill *--1 Skill
Journey 1--* JourneysUser *--1 User
Challenge 1--* ChallengesUser *--1 User
ChallengesJourney 1--* ChallengesJourneysUser *--1 User   (F2b : passage d'une étape optionnelle)
User 1--* Point *--1 Skill                                (Oméga = somme des Point.point)
```

`ChallengesUser`/`JourneysUser` sont les tables de progression — une ligne par (joueur, Challenge)
ou (joueur, Journey), unicité stricte (`validates_uniqueness_of ... scope: [:user_id]`).

## 2. Le cycle de vie tient sur deux colonnes : `end_at`, `validated_at`

Il n'existe **aucune colonne d'état nommée** ni d'enum. Tout le cycle de vie observable se
déduit de la présence/absence de ces deux timestamps nullables (`app/models/challenges_user.rb`,
`app/models/journeys_user.rb` — identiques dans leur structure) :

| `end_at` | `validated_at` | État observable | Comment on y arrive |
|---|---|---|---|
| nil | nil | pas commencé / en cours | ligne créée, rien déclaré |
| présent | nil | terminé, en attente de validation | `mark_as_ended!` appelé, `challenge.auto_validated?` faux (uniquement `validation_authority: "facilitateur"`) |
| présent | présent | validé | `mark_as_ended!` puis (immédiat ou différé) `mark_as_validated!` |

**Invariant vérifié empiriquement le 2026-08-02** (aucune exception en production) :
`validated_at` n'est jamais renseigné si `end_at` est nil — sur 151 `ChallengesUser` et 14
`JourneysUser`, zéro ligne « `end_at` nil + `validated_at` présent ». Sur les 151
`ChallengesUser` : 17 non commencées, 134 validées, **zéro** en attente (`end_at` présent,
`validated_at` nil) — cohérent avec la distribution des Challenges (9 `systeme` + 12
`declarative`, tous deux `auto_validated: true`, contre 1 seul `facilitateur`).

### Given/When/Then — le déclencheur

```
Given un ChallengesUser neuf (end_at: nil, validated_at: nil)
When  #mark_as_ended! est appelé (end_at = maintenant)
Then  le hook déclenché par le changement de end_at (#set_validated_at) s'exécute
      Si challenge.auto_validated? est vrai (validation_authority "declarative" ou "systeme") :
        #mark_as_validated! est appelé dans la foulée → validated_at = maintenant
        → Oméga attribué (voir §4)
      Sinon (validation_authority "facilitateur") :
        rien de plus ; la ligne reste "en attente" jusqu'à une action humaine explicite
```

`#mark_as_ended!` est déclenché soit par une action UI directe, soit via
`#receive_message_extra` (callback du fil de messagerie associé — un message envoyé avec
`extra[:ask_for_validation] == "1"` par l'auteur du ChallengesUser lui-même). La validation par
un facilitateur suit le même canal : `extra[:validation] == "1"`, gardé par
`Current.ability.can?(:edit, self)` — seul quelqu'un ayant le droit d'édition sur cette ligne
(le facilitateur désigné, un DFF, un admin) peut faire basculer `validated_at` à la place du
joueur.

## 3. Règle produit explicite : une validation acquise ne se révoque **jamais**

Décision de Boris (2026-07-28, réaffirmée pour `JourneysUser` le 2026-07-31). `#restart!`
(rejouer une expérience) remet `end_at` à nil mais **`#set_validated_at` ne touche plus jamais
`validated_at` à nil** :

```ruby
def set_validated_at
  if self.end_at.nil?
    # une validation acquise ne se révoque JAMAIS — les Ω restent acquis
  else
    self.mark_as_validated! if self.challenge.auto_validated?
  end
end
```

**Incident historique qui justifie ce garde-fou** (2026-07-25, `ChallengesUser`) : l'ancienne
version révoquait (`validated_at` → nil dès que `end_at` repassait à nil), ce qui déclenchait
`#gain_points` avec `validated_at` nil → `Point.destroy_all` → perte des Ω déjà acquis **et**
reverrouillage de tout le parcours linéaire en aval (§5). Un simple `#restart!` sur une
expérience déjà validée ne doit donc **jamais** faire disparaître ses points ni reverrouiller la
suite — c'est un contrat produit, pas un détail d'implémentation.

## 4. Oméga = recalcul intégral, jamais un delta

```ruby
def gain_points
  Point.where(user_id:, challenge_id:).destroy_all
  if self.validated_at
    self.challenge.challenges_skills.each do |cs|
      Point.create!(user_id:, challenge_id:, skill_id: cs.skill_id, point: cs.point)
    end
  end
end
```

Le total Oméga d'un joueur (`User#omega`) est **`points.sum(:point)`** — une somme brute, sans
ventilation par pilier persistée (une ventilation par Puissance/polarité existe en lecture via
`skills.derived_framework`, pas en écriture). `#gain_points` **détruit puis reconstruit** les
`Point` de ce (joueur, Challenge) à chaque changement de `validated_at` — jamais un delta,
jamais une simple création. Rejouer la même validation (idempotence) ne duplique donc rien.

### Le piège du double-écriture (`on_change`)

`on_change` (`mathieu_core`, `lib/mathieu_core/models/concerns/base_mathieu_core_record.rb:76`)
est un **`after_commit ..., on: [:update]`** — Rails ne le déclenche donc **jamais sur un commit
de pure création**, quel que soit le contenu de la ligne au moment du `INSERT`. Conséquence
directe pour le portage (remplacement prévu : « callbacks/services Rails explicites et testés ») :

```
Given un service qui fait ChallengesUser.create!(user:, challenge:, validated_at: Time.current)
      (une seule instruction, un seul INSERT)
Then  #gain_points ne s'exécute PAS — aucun Point créé, l'Oméga n'est pas attribué,
      silencieusement, sans erreur.
```

C'est un **incident déjà survenu en production** (Oméga, 2026-07-25) et le motif du patron
« deux écritures » employé systématiquement ailleurs dans le code (`ConseilSession`,
`Traversee`, `CoupableIdealSession` : créer la ligne nue, **puis** une seconde écriture qui
positionne `validated_at`). **Toute réimplémentation en callbacks Rails natifs doit reproduire
cette sémantique** : le hook d'attribution des Ω doit se déclencher sur *changement* de
`validated_at` sur une ligne existante, jamais sur la valeur initiale d'un `create`. En Rails
natif, l'équivalent direct est `after_update :gain_points, if: :saved_change_to_validated_at?`
(explicitement **pas** `after_save`, qui se déclenche aussi au `create`).

## 5. `auto_validated` est **dérivé**, jamais la source de vérité indépendante

```ruby
# Challenge
before_validation :derive_auto_validated
def derive_auto_validated
  return if validation_authority.blank?
  self.auto_validated = validation_authority != "facilitateur"
end
```

`validation_authority` (`"declarative" | "systeme" | "facilitateur"`) est la vraie donnée
éditoriale ; `auto_validated` (colonne booléenne historique, encore lue directement par
`ChallengesUser#set_validated_at`/`JourneysUser#set_validated_at`) n'est qu'un reflet calculé —
`facilitateur` → faux, les deux autres → vrai. **Ne jamais porter `auto_validated` comme un
champ éditable indépendant** : porter `validation_authority` et dériver `auto_validated` au
même endroit (`before_validation`), sous peine de désynchronisation.

Répartition en production (2026-08-02, 22 Challenges) : 12 `declarative`, 9 `systeme`,
**1 seul** `facilitateur` (l'Atelier Point Zéro — décision Boris, cf. passation 2026-07-25).

## 6. F2b — progression obligatoire/optionnelle et verrouillage linéaire

`ChallengesJourney` porte `required` (défaut vrai — 18 obligatoires / 2 optionnelles en
production) : une étape optionnelle *dans un Journey donné* peut être explicitement **passée**
(`ChallengesJourneysUser`, disjoint de `ChallengesUser` à dessein — un skip **ne crée jamais de
validation, ne génère aucun Oméga, n'inflige aucune pénalité**) plutôt que faite.

```ruby
# ChallengesJourneysUser
def inclusion_must_be_optional
  errors.add(:challenges_journey_id, "n'est pas optionnelle dans ce parcours") if challenges_journey.required?
end
```

Garde-fou explicite : passer une étape **obligatoire** est rejeté en validation, y compris via
un POST forgé directement sur la route.

### `Journey#completed_by?(user)` — un parcours est accompli

```
Accompli = TOUTES les expériences OBLIGATOIRES du parcours ont validated_at présent.
Les optionnelles (faites, passées ou ignorées) ne bloquent JAMAIS l'accomplissement.
Un parcours 100 % optionnel est considéré accompli d'office (rien ne peut bloquer).
Les skips ne comptent JAMAIS comme validation — seul validated_at fait foi.
```

### `Journey#locked_challenge_ids_for(user)` — verrouillage en mode `lineaire`

Uniquement pertinent si `progression_mode == "lineaire"` (2 Journeys sur ce mode en
production). Parcourt les parties du Journey dans l'ordre (`parts`, pages et challenges
interfoliés) ; une étape est *franchie* si validée, OU optionnelle et explicitement passée. La
première étape non franchie devient l'étape courante ; tout ce qui suit est verrouillé.

**Invariant explicite, à ne pas perdre au portage** : une expérience déjà validée n'est **jamais
reverrouillée**, même si une étape antérieure est ajoutée ou invalidée après coup — le calcul ne
« recule » jamais sur un acquis. C'était un vrai bug corrigé le 2026-07-28 (voir passation,
« Correctif : une expérience validée n'est jamais verrouillée »).

## 7. Ce que ce document ne couvre pas

- Les évaluations spécifiques (Moteur, Puissances, Conseil Oméga, Traversée, Coupable idéal) —
  chacune a son propre modèle et ses propres règles de calcul, hors périmètre de cette
  caractérisation-ci. À documenter séparément si utile au portage.
- L'authentification, les rôles et `Ability` (`can?`) — caractérisation à part.
- La messagerie (catégorie C) — entièrement couverte par la série de commits P0→P3 du
  2026-08-01 et son analyse d'impact dédiée
  ([analyse-impact-messagerie-cercles.md](analyse-impact-messagerie-cercles.md)).
- Les pièges transverses déjà consignés dans `PASSATION-CLAUDE.md` §3 (listes blanches de
  params imbriqués, `Slugable#find` vs `find_by(id:)`, locale = langue du navigateur, CSS non
  recompilable en SSH) restent valables et s'appliqueront de la même façon au portage.

## 8. Vérification de parité recommandée (une fois la catégorie B portée)

Sur une installation neuve, avec un Challenge `auto_validated` et un `facilitateur` :

1. Créer une ligne de progression neuve, la valider via le flux normal (pas un `create!` avec
   `validated_at` déjà rempli) → l'Oméga attendu doit apparaître, correspondant exactement à
   `challenge.challenges_skills.sum(:point)`.
2. Rejouer/`restart!` une expérience déjà validée → l'Oméga ne doit **pas** diminuer, la ligne
   doit rester validée (§3).
3. Sur un Journey linéaire, valider l'étape courante → l'étape suivante s'ouvre, aucune étape
   déjà validée ne se reverrouille si l'on modifie l'ordre des étapes en amont (§6).
4. Passer une étape optionnelle → aucun Oméga, `completed_by?` reste vrai si c'était la seule
   étape non obligatoire restante (§6).
5. `Challenge.validation_authority = "facilitateur"` → `end_at` seul ne suffit pas, il faut une
   action explicite d'un utilisateur ayant `can? :edit` sur la ligne (§2).
