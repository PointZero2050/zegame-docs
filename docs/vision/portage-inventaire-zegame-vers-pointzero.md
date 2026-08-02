# Portage zegame-app → pointzero-app : inventaire

> Rédigé par Claude le 2026-08-02, en lecture seule sur le serveur `vibe.ze.game`
> (branche `pointzero`, tête `5b4a875`). Objet : donner à Boris la matière pour arbitrer
> la convergence des deux environnements. Aucun code n'a été modifié nulle part.

## 1. Volumétrie

| Zone | Fichiers | Lignes |
|---|---|---|
| Modèles | 45 | 3 151 |
| Contrôleurs | 55 | 2 794 |
| Vues (HAML) | 184 | 5 705 |
| Services | 13 | 1 384 |
| Helpers + lib | 9 | 502 |
| **Total code applicatif** | **~360** | **~13 500** |

46 tables en base. 76 Mo d'assets dans `public/pz` (atlas, covers, thème, lecteur vidéo).

## 2. La surface réelle de `mathieu_core` est étroite

**27 fichiers sur ~360** citent la gem, et le namespace `MathieuCore::` n'est jamais invoqué
directement. La dépendance se réduit à six mécanismes :

| Mécanisme | Occurrences | Remplacement | Difficulté |
|---|---|---|---|
| `Concern::BaseMathieuCoreRecord` + `on_change` | 13 | callbacks Rails natifs (`after_update` ciblés) | faible — mécanique, mais **chaque callback doit être relu** (cf. incident Oméga du 2026-07-25) |
| DSL d'autorisation `Cans` (`ability.rb` + 34 `can?`) | ~35 | vérifications de rôle simples ou CanCanCan | moyenne — réécriture, pas traduction |
| `Slugable` | 8 | `friendly_id` (prévu au cadrage) | faible |
| Uploaders (`SquareImageUploader`, `ImageUploader`) | 9 | CarrierWave standard ou Active Storage | faible |
| `Concern::BaseUser` + colonnes User | 1 modèle | fusion dans le `User` Devise du nouvel environnement | moyenne |
| **Engine `mathieu_core_messaging`** | 20 `Messaging::` + 4 `receive_message` + 4 tables | **réécriture** d'une messagerie minimale | **élevée** |

**Découverte qui change l'estimation : l'appli utilise déjà Devise** (via la gem, mais avec les
modules standard : `database_authenticatable, recoverable, rememberable, validatable,
confirmable, trackable, omniauthable`). L'authentification n'est donc pas à réécrire mais à
**fusionner** avec le `User` déjà en place dans `pointzero-app` (qui a `joueur/facilitateur/
administrateur`). À trancher : conserver l'OAuth (Google/Microsoft/Apple) pour le festival ou
le différer.

## 3. Classement du code

### A — se déplace tel quel (aucune dépendance)
- `config/puissances/*.yml` (6), `config/ressources/*.yml` (5), `coupable_ideal.yml`,
  `experiences_video.yml` ;
- `public/pz` en entier (76 Mo : 162 médaillons d'atlas, covers, `pz_theme.css`, `video.js`) ;
- l'essentiel des vues HAML (5 705 lignes) — à adapter seulement là où passent `can?` (34) et
  les helpers d'upload.

### B — adaptation mécanique (cœur du jeu)
`journey, challenge, challenges_journey, challenges_journeys_user, challenges_user,
journeys_user, page, point, skill, validation, resource, ressource_evaluation,
moteur_assessment, puissance_assessment, conseil_session, coupable_ideal_session, traversee,
experience_quiz_attempt, graine_publiee, pact_source_version, onboarding, news_item,
external_registration, uploaded_file` + les contrôleurs et services associés
(`wordpress_registrations` devient inutile : les inscriptions sont natives désormais).

Travail type : retirer `on_change` → callback natif relu un par un, `Slugable` → `friendly_id`,
uploader → standard. Les pièges connus de la passation (validated_at/Oméga, listes blanches,
locale) s'appliquent ici.

### C — réécriture (messagerie et social)
`circle, circle_cycle, circle_membership, circle_session, blocage, signalement` + contrôleurs
`cercles, graines, profils, signalements, threads`. **C'est précisément la zone des 5 commits
du 2026-08-01** (P1→P3 : annuaire, profil communautaire, fil candidat/référent, blocage,
ouverture consentie). Elle repose sur l'engine `mathieu_core_messaging` (4 tables). Porter ces
écrans suppose une messagerie minimale native — la spec V1 la limite déjà au fil contextuel
candidat/référent, ce qui borne la réécriture.

### D — à abandonner (hors périmètre Point Zéro)
Tables `lti_*` (héritage LTI de ze.game), `dff/groups_dffs` (remplacé par les rôles),
OmniAuth si différé, `community/communities_user/group/groups_user` **à arbitrer** : le
bac à sable les utilise comme conteneurs de Mondes — le cadrage prévoyait déjà un modèle
`World` distinct.

## 4. Séquence de portage proposée

1. **Gel** : plus aucun nouveau chantier sur `zegame-app` ; on y termine ce qui est en vol.
2. ~~Config + assets (catégorie A)~~ **FAIT le 2026-08-02** (commit `7da4277` de
   pointzero-app, source : tête `5b4a875` de zegame-app). Au dépôt : 6 YAML puissances,
   5 YAML ressources, `coupable_ideal` (v1+v2), `experiences_video`, CSS/JS du thème
   (`pz_theme.css`, `conseil.css`, `video.js`, `conseil.js`, `pz_admin.js`) et images de
   racine. En volume monté lecture seule (`/home/deploy/pz`, hors dépôt et hors contexte de
   build, même modèle que les médias WordPress) : 417 fichiers, 76 Mo — atlas des 162
   médaillons, covers ressources, époque, coupable-idéal, polices, moteur. Vérifié servi en
   production (`/pz/...` → 200) et YAML chargés par Rails. ⚠️ Si zegame-app modifie un YAML
   pendant la fin de ses chantiers en vol, re-synchroniser avant la migration des données.
3. ~~Fusion `User`~~ **FAIT le 2026-08-02** (commit `c5b59a2`) : la table `users` de
   pointzero-app porte désormais les champs de profil de zegame-app (civilité, téléphone,
   territoire, présentation, langues, disponibilité, `moteur_caps`, photo, slug,
   `is_anonymized`) plus les colonnes `confirmable` (module désactivé). Correspondance
   d'import documentée dans la migration : `first_name→prenom`, `last_name→nom`,
   `dff→facilitateur`, `admin→administrateur`, `nil→joueur`. `registerable` et OAuth restent
   désactivés (question 3 du §6 toujours ouverte). Conséquence pour le portage des vues :
   remplacement mécanique `first_name/last_name → prenom/nom`.
   Reste de l'étape : les **autorisations** (DSL Cans → vérifications de rôle), à faire au
   fil du portage des contrôleurs.
4. Cœur du jeu (catégorie B) dans l'ordre des dépendances : Journey/Page/Challenge →
   progression/points → évaluations (Moteur, Puissances, Conseil, Traversée, Coupable idéal).
5. Cercles + messagerie minimale (catégorie C) — en dernier car le plus récent et le moins
   stabilisé.
6. Migration contrôlée et rejouable des données (sous-ensemble explicite, répétition
   obligatoire — cadrage §5), puis bascule DNS et extinction progressive.

## 5. Estimation honnête

- A : ~1 jour. B : le gros morceau — de l'ordre de **1 à 2 semaines** de travail concentré,
  la relecture des callbacks étant incompressible. C : ~3-5 jours si la messagerie reste au
  périmètre V1. Migration + répétitions : 2-3 jours.
- **Faisable en août ; intenable si le périmètre de `zegame-app` continue de croître pendant
  le portage.** Chaque fonctionnalité ajoutée là-bas s'ajoute à la facture ici.

## 6. Décisions

1. ~~Acter la cible~~ **ACTÉ (Boris, 2026-08-02)** : `pointzero-app` est l'application du
   Festival.
2. ~~Acter le gel~~ **ACTÉ (Boris, 2026-08-02)** : `zegame-app` est gelée — on termine ce qui
   est en vol, on n'ouvre plus de nouveau chantier. Consigné en tête de `PASSATION-CLAUDE.md`.
3. **Ouvert** — OAuth au festival : garder ou différer ?
4. **Ouvert** — Communities/Groups : porter tel quel ou basculer vers le modèle `World` ?
5. **ACTÉ** comme plan B : si le portage du cœur (B) glisse au-delà de fin août, le festival
   se joue sur `vibe.ze.game` et seul le site+billetterie reste sur la nouvelle pile.
