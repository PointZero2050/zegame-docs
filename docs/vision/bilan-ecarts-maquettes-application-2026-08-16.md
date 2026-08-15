# Bilan des écarts entre maquettes et application — 16 août 2026

> **Audit Codex.** Ce document croise trois références qui n'ont pas la même fraîcheur : les
> maquettes de `zegame-prototypes`, le code Rails local `origin/pointzero` au commit `c4383bb`
> audité en lecture seule, et la passation du portable du 15 août pour les ajouts de préproduction
> plus récents. Il ne prouve pas la promotion en production de ces derniers. Toute divergence
> observée au portage doit être résolue en faveur des modèles et droits réels, jamais par une
> imitation front.

## 1. Légende

| Code | Sens | Décision de portage |
|---|---|---|
| **A** | fonction réelle et source de vérité identifiée | raccorder la vue, sans dupliquer l'état |
| **P** | socle partiel ; la maquette assemble plus que l'application | porter par lots et rendre les absences honnêtes |
| **N** | objet métier ou droit absent | ne pas porter comme fonction réelle |
| **T** | horizon narratif assumé | teaser explicite uniquement |

## 2. Lot Monde 0 : écart écran par écran

| Territoire / maquette | Réel disponible | Écart résiduel | Code | Recommandation |
|---|---|---|---:|---|
| Coque `accueil-puissances-m0-cible` | Monde courant, Journey obligatoire, profils, Omégas ; portage annoncé en cours | résolveur des sept cartes, états découverts, popups vues, roue partagée et navigation | P | un composant de coque + un résolveur en lecture seule ; aucun callback dans les cartes |
| Désir / Immateria | page `/immateria`, jeu Phaser servi par Rails et POST idempotent vers une Trace, livrés en préprod | URL stable finale, état de carte et contrat du prochain geste | A/P | préserver le POST et l'unicité de la Trace ; le flux JS reste remplaçable |
| Volonté `volonte-marelle-m0-cible` | Journey, Challenge, progression, verrou linéaire, durée, validation et Omégas | intensité 1–5, échelle d'effet 1–5 et puissance de parcours 1–10 n'ont pas de source canonique | P/N | porter d'abord la progression réelle ; ajouter les trois données seulement après décision de modèle |
| Imagination / Fresque | Graine actuelle sous forme de message de fin de chapitre ; publication de profil opt-in | pas de type Graine distinct, de Fresque agrégée ni de Résonance | P/N | ne pas requalifier tous les messages ; introduire une identité de production avant la Fresque complète |
| Imagination / Traces | Trace Immateria en préprod ; résultats historiques dispersés | aucun agrégateur canonique multi-formats ni filiation Trace → Graine dans le code audité | P/N | registre de productions avec adaptateurs, puis filiation explicite |
| Émotion / héros et mentors | catalogue, héros choisi, fiches, mentor réel Claude, consentements et mémoire préprod | rendu cible des trois Puissances, parcours associés, navigation unifiée | A/P | raccorder les fiches réelles ; ne pas simuler une association de parcours absente |
| Communication / guides | `/guide`, deux voix, corpus M0, plafond et signalement en préprod | pastille persistante, historique de dialogue et Espace du Seuil communautaire | P/N | page réelle d'abord ; pastille ensuite ; channel seulement avec objet espace et droits explicites |
| Intuition / Point Zéro | dix fiches PZ et Ressourcerie réelle annoncées en production | appropriation QCM → Trace et états de carte | P | la lecture précède le questionnaire ; créer une Trace seulement sur réponse réellement soumise |
| Intuition / événements | agenda WordPress relié à l'accueil | intégration au sous-menu et état vide/erreur | A | réutiliser la source d'événements, sans copie éditoriale |
| Transcendance / Moteur | assessments, caps, questionnaires, `power_breakdown`, pages de Puissances | formule d'alchimisation sur 10 absente du code audité | P/N | afficher les six lemniscates réels ; garder l'alchimisation comme hypothèse tant que formule non versionnée |
| Transcendance / Accomplissements | badges et progression existent selon la passation | constellation, catégories et visibilité globale par catégorie à raccorder | P | identifier la table de vérité de chaque badge avant toute constellation |
| Pastille Oméga | `Point`, total et ventilation Skill/Challenge | aucun actif/passé, aucune dépense, aucun Fonds réel | A | solde unique M0 + provenance ; ne pas afficher million, financement ou part relative avant M1 |
| Menu de compte | routes d'authentification et compte existent | ancres fictives des prototypes, CGU et préférences à confirmer route par route | P | remplacer chaque ancre par une route réelle ou un état indisponible explicite |

## 3. Monde 1 : ce que la coque peut projeter aujourd'hui

| Projection cible | Sources réelles utilisables | Manque métier | Code |
|---|---|---|---:|
| Monde 1 ouvert / Boussole | `Mondes.ouvert?`, Journey `mandatory`, `JourneysUser`, progression | données éditoriales définitives de la Boussole | A/P |
| Prochaine expérience | verrou linéaire, `ChallengesUser`, `ExperienceState`, durée | intensité/effet/puissance cible | A/P |
| Aucun Cercle / candidature / invitation | Circle, cycle, membership et statuts | suggestion algorithmique explicable | A/N |
| Cercle actif | membres, plafond 8, séance, rôles JSON, Pacte versionné | cycle de clôture, reventilation, attestation collective | P |
| Échanges en attente | fils Journey/Challenge/CircleMembership, `last_seen_at` | inbox polymorphe et espaces communautaires | P/N |
| Graines et Résonances du Cercle | message Graine et publication profil | partage scoped Cercle, Résonance et synthèse consentie | N |
| Profil du Cercle / flow | aucune source dédiée | évaluations Puissances + Cadres + protocole 360° | N |
| Omégas M1 | total et ventilation | decay, domaines confirmés, compteur million historisé | P/N |
| Commun et financement | aucune table financière | ledgers, droits, gouvernance et cadrage juridique | N |

La conséquence est simple : la première version Rails de l'accueil Monde 1 peut montrer la
Boussole, la progression, l'état réel d'un Cercle et les fils déjà autorisés. Elle ne doit pas
maquiller le matching, les Résonances, le flow, le million ou le Commun en données disponibles.

## 4. Inventaire des maquettes cibles transversales

| Famille | Maquettes | État applicatif dominant | Code |
|---|---|---|---:|
| Navigation et progression | `application-cible-devoilement`, `accueil-application-cible`, `marelle-freeride-cible`, `experience-vivante-cible` | progression réelle, orchestration cible partielle | P |
| Profil individuel | `profil-joueur-cible`, `alchimisation-cible`, `carte-du-seuil-role-appel` | profil et Moteur partiels ; alchimisation et certaines œuvres absentes | P/N |
| IA et récit | `mentor-fresque-cible`, `heros-mentors-cible` | mentor, consentements et héros réels ; Fresque/Résonances partielles | P |
| Communication | `messagerie-point-zero-cible`, `centre-activite-cible`, `agenda-vivant-cible` | fils et agenda partiels ; espaces, objets structurés et inbox unifiée absents | P/N |
| Cercles | `cercle-croissance-cible`, `facilitateur-cockpit-cible`, `academie-facilitateurs-cible` | adhésion/séances/Pacte partiels ; cockpit, habilitations et 360° absents | P/N |
| Commun et économie | `economie-omega-cible`, `reconnaissance-omega-cible`, `gouvernance-commun-cible`, `missions-commun-cible`, `place-marche-cible` | Omégas individuels seuls ; économie et décisions cibles absentes | N/T |
| Projets et souverainetés | `projet-vivant-cible`, `souverainetes-projets-cible`, `studio-filiation-cible` | pas de modèle cible complet dans le code audité | N/T |
| Organisations | `organisation-vivante-cible`, `sas-organisation-cible` | aucun profil systémique d'organisation | N/T |
| Écosystème | `observatoire-ecosysteme-cible`, `annuaire-vivant-cible`, `ressourcerie-vivante-cible` | annuaire/ressources partiels ; observatoire et rayonnements absents | P/N |
| Consentement et intégrité | `consentement-securite-cible`, `aide-situations-sensibles-cible`, `backoffice-integrite-cible` | consentements LLM, signalement et droits partiels ; registre complet absent | P |
| Monde-miroir | `monde-miroir-cible`, `epreuve-runes-cible` | Immateria séparé et Trace minimale ; univers cible hors Rails | T |

## 5. Écarts éditoriaux déjà résolus

1. Les anciennes figures du Monde 0 ont été remplacées par Cléopâtre, Aragorn, Léonard de
   Vinci, Marie-Madeleine, Socrate et Athéna dans les prototypes concernés.
2. Les verbes canoniques sont **JE M'EXPRIME** et **JE DISCERNE**.
3. Les huit scénarios du banc sont agnostiques du mentor depuis le 16 août.
4. Le corpus des guides comporte trente fiches M0 et vingt-et-une fiches M1 ; ses sources
   citables utilisent des titres publics, jamais des chemins de dépôt.

## 6. Ordre de réduction des écarts

1. **Coque M0 partagée** : navigation, état des cartes et routes réelles.
2. **M0 à backend existant** : Ressourcerie, héros, Moteur, événements, Oméga.
3. **Productions** : identité canonique Graine/Trace puis agrégateur, avant Fresque riche.
4. **Accueil M1 Lot A** : projection Boussole/Cercle/fils réels selon la matrice d'impact.
5. **Messagerie polymorphe et espaces** avant toute promesse d'Espace du Seuil ou d'inbox.
6. **Objets collectifs** : attestation, Résonance, profil de Cercle et 360°.
7. **Économie** uniquement après modèles séparés, droits, audit et cadrage juridique.

## 7. Règle de recette

Pour chaque CTA de maquette, la fiche de portage doit répondre à quatre questions :

1. quel objet détient l'état visible ?
2. quel droit serveur autorise l'action ?
3. quel événement métier produit la transition ?
4. quels callbacks ou effets irréversibles sont déclenchés ?

Si une réponse manque, le CTA reste un lien de découverte, un teasing ou disparaît. Il ne gagne
jamais un Oméga, ne valide jamais une expérience et ne forme jamais un Cercle par convention de vue.
