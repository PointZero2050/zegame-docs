# Caractérisation — le triptyque Monde 0 et le patron « auto-validation Marelle »

> Rédigé par Claude (instance bac à sable), 2026-08-02, en lecture seule sur `vibe.ze.game`
> (zegame-app, branche `pointzero`, tête gelée `5b4a875`). Troisième pièce de caractérisation,
> après [progression/Oméga](caracterisation-progression-omega.md) et
> [auth/rôles/autorisations](caracterisation-auth-roles-autorisations.md). Choisi parce que c'est
> la suite naturelle de la séquence de portage catégorie B annoncée dans l'inventaire
> (« progression/points → évaluations ») et que Monde 0 est le chemin critique du Festival
> (cadrage [application-festival-2026.md](application-festival-2026.md) §2 — connexion → Monde 0
> → profil, la « tranche verticale autonome »).
>
> Chiffres de production au 2026-08-02 : `MoteurAssessment` 11 lignes (8 complétées),
> `Traversee` 3 (2 complétées), `ConseilSession` 2 (1 complétée), `CoupableIdealSession` 6,
> `ExperienceQuizAttempt` 4, `PuissanceAssessment` 25 (0 publiée — cohérent, la publication
> volontaire est une fonctionnalité du 2026-08-01, catégorie C).

## 1. Le patron transverse : « auto-validation Marelle » (5 modules identiques)

**C'est le fait le plus important de ce document.** Cinq modules d'évaluation, sans lien de
code entre eux, implémentent chacun leur propre copie **quasi verbatim** de la même méthode :

```ruby
def validate_marelle_experience!  # ou validate_challenge! pour ExperienceQuizAttempt
  ch = Challenge.find_by(name: "<Titre exact du Challenge>")  # ou challenge_id direct
  return unless ch
  # DEUX écritures, pas une : `on_change` de mathieu_core est un after_commit
  # `on: [:update]`, qui ne se déclenche jamais sur un commit de création.
  cu = ChallengesUser.find_or_create_by!(user_id: user_id, challenge_id: ch.id)
  return if cu.validated_at.present?
  cu.end_at ||= Time.current if cu.respond_to?(:end_at)
  cu.validated_at = Time.current
  cu.save!
rescue => e
  Rails.logger.warn("...")
end
```

Présent, à l'identique près le nom de la méthode et la résolution du Challenge (par `name` ou
par FK directe), dans `MoteurAssessment`, `Traversee`, `ConseilSession`, `CoupableIdealSession`
et `ExperienceQuizAttempt`. Appelé en toute fin du propre cycle de vie de chaque module (quand
son propre `status` passe à `"completed"`), **jamais** par un callback `on_change` de
`ChallengesUser` lui-même — c'est le module d'évaluation qui pousse la validation vers la
Marelle, pas l'inverse.

**Pour le portage, ceci doit devenir un seul concern/service partagé** (`MarelleValidatable` ou
équivalent), pas cinq copies indépendantes à réécrire une par une — le risque de divergence
silencieuse (une des cinq copies corrigée, les quatre autres oubliées) est déjà arrivé dans
l'historique du projet (cf. `PASSATION-CLAUDE.md`, correctif du 2026-07-28 sur la révocation
`ChallengesUser`/`JourneysUser` : deux implémentations similaires, une seule corrigée d'abord).
Contrat minimal du service : `(user, challenge)` → trouve-ou-crée la ligne `ChallengesUser` nue,
**puis** une seconde écriture qui pose `validated_at` (et `end_at` si absent) — jamais un seul
`create!` avec `validated_at` déjà rempli (voir
[caracterisation-progression-omega.md](caracterisation-progression-omega.md) §4 pour le pourquoi
exact). `return if cu.validated_at.present?` rend l'appel **idempotent** : rejouer un module déjà
complété ne touche plus jamais l'Oméga déjà acquis, cohérent avec la règle « une validation ne se
révoque jamais ».

## 2. Bloc 1 — `MoteurAssessment` (« Une drôle d'époque »)

Un questionnaire narratif de 7 jours (6 Puissances + Transcendance), contenu dans
`config/une_drole_depoque.yml`. **Chaque passation est un instantané historisé** — rejouer crée
une **nouvelle ligne**, jamais une réécriture (commentaire du modèle, à respecter tel quel : la
donnée n'est jamais mutée rétroactivement).

- `STEPS` est une séquence figée (prologue ×2, jour 1..7 × 4 écrans, miroir) ; `current_step`
  avance/recule un pas à la fois (`advance!`/`step_back!`, jamais un saut arbitraire).
- `compute_result!` est un calcul **déterministe et explicable**, pas un scoring pondéré caché :
  pour chaque jour 1-6, la polarité spontanée (É2), l'amplitude déclarée (É3, `clamp(1,3)`) et le
  rapport au mouvement inverse (É4 : `bloque`/`cadre`/`libre` → `circulation_hypothesis` +
  `confidence`) déterminent une **posture** (catalogue de 24, croisant puissance dominante ×
  polarité × rapport « enracinée/passante ») et **trois portes** (circulation, élan disponible,
  conscientisation) par des règles explicites de tri (`sort_by` amplitude puis circulation puis
  jour le plus tardif — jamais un score agrégé opaque).
- **Garde-fou explicite dans le code** : « l'amplitude de la polarité NON choisie reste inconnue
  (`nil`), jamais zéro » — ne pas confondre « non observé » et « nul » au portage (un champ
  `nil` a un sens différent d'un `0`, à préserver dans le schéma cible).
- Valide l'expérience Marelle nommée exactement `content["titre"]` (le titre YAML, pas une
  constante Ruby) — **le titre du Challenge en base et celui du YAML doivent rester synchronisés
  au mot près**, sans quoi `Challenge.find_by(name: ...)` renvoie `nil` et `return unless ch`
  avale silencieusement l'échec (pas d'exception, juste rien ne se passe).

## 3. Bloc 2 — `Traversee` (« Avant le Zéro »)

Un parcours arborescent (« sablier ») à choix, contenu fusionné depuis
`config/avant_le_zero/*.yml` (un fichier par voie). **Garde-fou acté explicitement dans le
code : AUCUN scoring** — les seules traces conservées sont les voies parcourues, les *fins*
atteintes (`fin_id`) et le nombre de traversées jouées. Ne pas réintroduire de score au portage,
c'est une décision produit délibérée, pas un oubli.

- Rejouer ne repart pas de zéro : `Traversee.start_for(user)` reprend une ligne `in_progress` si
  elle existe, sinon **hérite les réponses de l'Acte I** (`A1..A10`) de la dernière traversée
  complétée et redémarre à la `Dispersion` (`D`) — seul l'acte I (le tronc commun) est réputé
  stable d'une traversée à l'autre, jamais les branches.
- `rendered_echos` : chaque écho affiché choisit sa variante de texte selon une réponse
  **mémorisée plus tôt dans la même traversée** (`answers[echo["ref"]]`), avec un texte par
  défaut si la réponse n'existe pas — un mécanisme de callback narratif simple (map statique),
  pas un moteur de règles.
- `complete_at!(fin_section_id)` est **idempotent** (`return if completed?`) — atteindre une fin
  déjà atteinte ne recrée rien.
- Sert de donnée d'entrée à `ConseilSession` (§4) via `Traversee.fins_for(user)` — **les fins de
  toutes les traversées du joueur, cumulées**, pas seulement la dernière.

## 4. Bloc 3 — `ConseilSession` (« Le Conseil Oméga »)

Contenu fusionné depuis `config/conseil_omega/*.yml`. Séquence de sections démarrant à
`ELLIPSE1`. **Aucun scoring évaluatif non plus** (commentaire du modèle : « le vote est
l'expérience, le cap est la trace »).

- Se nourrit de **deux traces des blocs précédents**, jamais recalculées, seulement lues :
  - `devenirs` = `Traversee.fins_for(user)` (protégé par un `rescue []` — l'absence de
    traversée ne bloque jamais le Conseil) ;
  - `posture_seuil` = lit `MoteurAssessment` (le dernier avec `result` non vide) et en extrait
    `result["posture_nom"] || result.dig("posture","nom") || result["posture"]` — **trois clés
    différentes tolérées pour compatibilité** avec d'anciennes passations qui utilisaient un
    format antérieur (« conseil_du_seuil », cf. commentaire de `MoteurAssessment`). Au portage,
    décider explicitement si cette rétrocompatibilité de format a encore un sens (données
    migrées une fois) ou si elle peut être simplifiée à une seule clé.
- `rendered_echos` a **deux références spéciales** en plus du mécanisme simple de Traversee :
  `"DEVENIRS"` (choisit la variante dont la clé correspond à un devenir atteint) et `"POSTURE"`
  (choisit la variante correspondant à `posture_seuil`) — donc ce module réutilise le même
  patron générique que Traversee mais l'étend.
- `suggested_postures` : scoring **explicable** (pas cosmétique) = nombre de Puissances engagées
  (caps `assumer`/`circuler`) en intersection avec les puissances de la posture, + 0,5 par
  intersection avec les devenirs atteints ; classement stable (`sort_by.with_index`, l'ordre du
  catalogue départage les ex æquo) ; les 3 premières sont proposées, le joueur choisit
  explicitement (`posture_cible`) — **la machine suggère, ne décide jamais**.
- `complete!` : mêmes deux écritures que partout ailleurs, `validate_marelle_experience!` cible
  le Challenge nommé exactement `"Le Conseil Oméga"`.
- **Sert de source pour le « Rôle d'appel » provisoire du profil communautaire** (P1,
  `User#role_appel_provisoire` → `posture_choisie&.dig("nom")`) — un couplage descendant à
  refaire au portage si le profil communautaire (catégorie C) est porté après ce bloc.

## 5. Les deux autres modules du même patron (non détaillés ici)

- **`CoupableIdealSession`** (mini-jeu, 6 lignes en production) — même recette
  `validate_marelle_experience!` à l'identique. Contenu et logique propres non caractérisés dans
  ce document ; à faire séparément si le portage l'atteint avant que cette caractérisation soit
  mise à jour.
- **`ExperienceQuizAttempt`** (QCM d'expérience, spec V1, 4 lignes) — même recette sous le nom
  `validate_challenge!` (privée), avec une variante : résolution du Challenge par FK directe
  (`challenge_id` porté par le modèle) plutôt que par `Challenge.find_by(name:)` — plus robuste
  qu'un nom éditorial, à préférer si le portage réécrit le patron commun (§1).

## 6. Ce que ce document ne couvre pas

- Le contenu éditorial complet des YAML (`une_drole_depoque.yml`, `avant_le_zero/*.yml`,
  `conseil_omega/*.yml`) — catégorie A du portage, déjà migré tel quel (`7da4277`).
- `PuissanceAssessment` (Monde 1, 25 lignes, 0 publiée) — hors triptyque Monde 0, pédagogiquement
  postérieur ; à caractériser séparément si utile, son mécanisme de publication volontaire est
  déjà documenté dans [caracterisation-progression-omega.md](caracterisation-progression-omega.md)
  et les commits P1b.
- Le détail des vues/contrôleurs de chaque module (HAML, catégorie A pour l'essentiel).

## 7. Vérification de parité recommandée

1. Compléter `MoteurAssessment` de bout en bout → l'expérience Marelle correspondante passe
   validée, l'Oméga attendu apparaît, `result["posture"]` est non nul et cohérent avec les
   réponses saisies (§2).
2. Rejouer `MoteurAssessment` une seconde fois → **nouvelle ligne créée**, l'ancienne reste
   intacte et lisible (jamais de réécriture).
3. Compléter `Traversee` jusqu'à une fin → aucun score nulle part dans la donnée persistée ;
   rejouer → l'Acte I est prérempli, la Dispersion est le point de reprise.
4. Compléter `ConseilSession` → `devenirs`/`posture_seuil` reflètent bien les traces des blocs 1
   et 2 déjà complétés par ce joueur ; `suggested_postures` change si on fait varier les caps
   engagés ou les fins de Traversee atteintes.
5. Sur les cinq modules : rejouer un module déjà validé ne doit **jamais** faire baisser l'Oméga
   du joueur ni re-verrouiller une étape en aval (cohérence avec la règle générale du §3 de
   [caracterisation-progression-omega.md](caracterisation-progression-omega.md)).
6. Renommer (ou dépublier) le Challenge cible d'un module sans mettre à jour la référence
   (`name` ou FK) → la validation doit échouer silencieusement (`return unless ch`), sans lever
   d'exception visible au joueur ; vérifier que ce silence est bien voulu au portage et pas
   remplacé par une 500 surprise.
