# Monde 1 — matrice d’impact de l’onboarding par les sept Puissances

> **Ajout Codex — 2026-08-16.** Préalable technique demandé au §11 de
> [onboarding-monde-1-sept-puissances.md](onboarding-monde-1-sept-puissances.md). Audit en lecture
> seule de la référence locale `origin/pointzero` de `zegame-app`, commit `c4383bb`. Cette matrice
> décrit le code observé ; elle ne prouve pas à elle seule l’état de la base ou du code chargé en
> production. Aucun modèle, callback, droit ou déploiement n’a été modifié.

## 1. Règle d’architecture

Une carte de l’accueil ne possède aucun état métier. Elle **projette** un état détenu ailleurs et
propose une transition déjà autorisée par le domaine concerné.

```text
carte visible
  = résolution en lecture seule de sources existantes
  + priorité éditoriale explicable
  + CTA vers une action métier gardée côté serveur
```

Conséquences impératives :

- aucun bouton de carte ne pose directement `validated_at` ;
- aucun bouton de carte ne crée de `Point` ni n’appelle `gain_points` ;
- aucun bouton de carte ne forme ou n’active directement un Cercle ;
- un état absent du modèle n’est jamais simulé comme une donnée réelle ;
- un nouvel état d’interface ne justifie pas automatiquement une nouvelle colonne ;
- la disparition visuelle d’un bouton ne constitue jamais un droit.

L’accueil cible appelle un résolveur de présentation, par exemple `Monde1HomeState`, sans callback
et sans méthode d’écriture. Ce service peut assembler les sept territoires, mais chaque transition
reste la responsabilité du contrôleur ou du service métier déjà propriétaire de l’objet.

## 2. Légende de maturité

| Code | Sens |
|---|---|
| **E** | Source de vérité existante et exploitable sans nouveau modèle |
| **R** | État calculable par un nouveau résolveur en lecture seule |
| **N** | Nouvel objet ou nouveau contrat métier nécessaire avant affichage réel |
| **T** | Teasing éditorial seulement ; aucune donnée personnelle ou collective ne peut être prétendue |

## 3. Progression : Journey, Challenge et ExperienceState

| ID | État visible / action | Maturité | Source de vérité | Droit ou garde serveur | Événement de transition | Effets et interdits |
|---|---|---:|---|---|---|---|
| P01 | Monde 1 fermé | E | `Mondes.ouvert?(community_id, user)` ; `config/mondes.yml` | Monde déclaré et parcours `mandatory` de la communauté prérequise non accomplis ; admin excepté | Validation de toutes les expériences requises de tous les parcours obligatoires du Monde 0 | Jamais un seuil d’Omégas |
| P02 | Monde 1 ouvert | E | même résolveur ; `Community#mandatory_completed_by?` → `Journey#completed_by?` | joueur authentifié | dernière expérience requise du Monde 0 validée, Atelier compris | Une validation acquise reste irrévocable |
| P03 | Boussole disponible mais non commencée | R | Journey Monde 1 `mandatory: true` + absence de `JourneysUser` | `can?(:show, journey)` et `Mondes.ouvert?` | `JourneysUsersController#create` | Crée seulement l’inscription ; aucun Oméga |
| P04 | Boussole en cours | E | `JourneysUser` présent + `JourneyProgress.for` + expériences requises non toutes validées | propriétaire ; visibilité Journey/Community | ouverture d’une expérience ou création nue d’un `ChallengesUser` | `JourneysUser#validated_at` n’est pas la source du taux d’accomplissement |
| P05 | Catalogue encore fermé | E | au moins un Journey `mandatory` de la communauté incomplet | garde de `JourneysController#show` sur les parcours non obligatoires | validation de la dernière expérience requise de tous les parcours `mandatory` | Ne pas reproduire ce verrou dans la vue |
| P06 | Catalogue ouvert | E | `Community#mandatory_completed_by? == true` | Journey visible dans la communauté | même transition que P05 | L’ordre d’exploration du catalogue reste libre |
| P07 | Expérience verrouillée | E | `Journey#locked_challenge_ids_for(user)` en mode `lineaire` | garde de `ChallengesController#show` | validation d’une étape antérieure ou passage explicite d’une optionnelle | Une expérience déjà validée n’est jamais reverrouillée |
| P08 | Expérience ouverte, pas commencée | E | absence de `ChallengesUser` | joueur inscrit au Journey ; `can?(:create, ChallengesUser)` | affichage de la fiche après les gardes, puis `find_or_create_by!` | Création nue : `end_at` et `validated_at` restent nuls |
| P09 | Expérience en cours | E | `ChallengesUser` présent, deux timestamps nuls ; `ExperienceState :in_progress` si preuve réelle absente | propriétaire du `ChallengesUser` | action dans la fiche, mini-jeu ou format associé | La carte ne conclut rien depuis un simple clic |
| P10 | Preuve prête | E/R | `ExperienceState :evidence_ready` ; adaptateur par slug ou absence d’adaptateur | propriétaire | session/quiz réellement complété | Un format neuf exige un adaptateur explicite si son geste est observable |
| P11 | Soumise au facilitateur | E | `end_at` présent, `validated_at` nul ; `ExperienceState :submitted` | auteur via message `ask_for_validation`; lecture bornée au propriétaire/facilitateur/admin | `ChallengesUser#mark_as_ended!` | Seulement pour `validation_authority: facilitateur` |
| P12 | Expérience validée | E | `ChallengesUser#validated_at` présent ; `ExperienceState :validated` | système, déclaratif du propriétaire ou facilitateur autorisé selon l’autorité | `ChallengesUser#mark_as_validated!` par une mise à jour | Déclenche le callback Oméga ; jamais de création directement validée |
| P13 | Étape optionnelle passée | E | `ChallengesJourneysUser` unique pour l’inclusion et le joueur | propriétaire, Journey visible, inclusion réellement optionnelle | action `passer` | Aucun `ChallengesUser`, aucune validation, aucun Oméga |
| P14 | Étape optionnelle reprise | E | suppression de `ChallengesJourneysUser` | propriétaire | action `reprendre` | Ne retire aucun acquis antérieur |
| P15 | Parcours accompli | E | `Journey#completed_by?` : toutes les inclusions `required` validées | lecture propriétaire / droits Journey | validation de la dernière requise | Les optionnelles et leurs skips ne peuvent fabriquer cet état |
| P16 | Rejouer une expérience | E | `ChallengesUser#validated_at` conservé ; session propre au format recréée/réinitialisée | propriétaire | CTA « revoir/refaire » de l’adaptateur | Ne jamais appeler le `restart!` générique depuis la nouvelle coque |

### 3.1. Piège callback non négociable

`ChallengesUser` porte `on_change :validated_at, :gain_points`. Dans `mathieu_core`, ce hook est un
`after_commit` limité aux mises à jour. Une ligne créée avec `validated_at` déjà renseigné ne
produit donc aucun Oméga. Toute expérience dédiée doit suivre le motif existant :

1. `find_or_create_by!` d’une ligne nue ;
2. retour immédiat si elle est déjà validée ;
3. mise à jour de `end_at` et `validated_at` ;
4. le callback recalcule seul les `Point`.

## 4. Parcours obligatoire et intensités

| ID | État visible / action | Maturité | Source de vérité | Droit ou garde | Transition | Vigilance |
|---|---|---:|---|---|---|---|
| M01 | « Tutoriel obligatoire » | E | `Journey#mandatory` | édition admin/DFF de la communauté ; lecture joueur autorisé | donnée éditoriale du Journey | Ne pas confondre avec `ChallengesJourney#required` |
| M02 | Expérience obligatoire dans ce parcours | E | `ChallengesJourney#required` | inclusion administrée dans le Journey | modification éditoriale | Le même Challenge peut être optionnel ailleurs |
| M03 | Durée d’expérience | E | `Challenge#duration` + `duration_unit` | lecture | édition du Challenge | Déjà exploitable pour les filtres |
| M04 | Intensité joueur sur 5 | N | aucune colonne canonique ; `difficulty` vaut actuellement 1–10 et porte une sémantique historique ambiguë | — | décision de modèle puis migration ou mapping éditorial versionné | Ne pas renommer silencieusement `difficulty` |
| M05 | Rayon d’effet sur 5 | N | aucune source | — | nouveau champ éditorial/versionné | Distinct de l’intensité |
| M06 | Puissance globale d’un parcours sur 10 | N | aucune source ni formule | — | évaluation éditoriale/LLM validée humainement | Ne pas calculer depuis la somme des Omégas |
| M07 | Niveau minimal de Monde | N/R | accessibilité actuelle portée par `community_id` et `Mondes`, pas par un champ de niveau | garde structurelle existante | rattachement du Journey à la communauté correspondante ; contrainte spécifique à concevoir pour les expériences réutilisées | Une expérience 4–5 ne devient pas interdite par son seul score |

## 5. Cercle, cycle, membres, rôles et Pacte-Source

| ID | État visible / action | Maturité | Source de vérité | Droit ou garde serveur | Événement de transition | Effets et limites |
|---|---|---:|---|---|---|---|
| C01 | Rubrique Cercle verrouillée | E | `Mondes.communaute_du_monde(1)` + `Mondes.ouvert?` | `CerclesController#verifier_monde_1` fail-closed | ouverture structurelle du Monde 1 | Pas de seuil Ω |
| C02 | Aucun Cercle | E | aucune membership active/invitation/demande | joueur Monde 1 | choix d’ouvrir, demander ou accepter une invitation | L’algorithme ne doit pas affecter un joueur |
| C03 | Suggestions de partenaires | N | aucun modèle de matching ou de suggestion | futur consentement/visibilité des profils | proposition calculée puis choix humain | La maquette ne peut afficher que du fictif tant que cet objet manque |
| C04 | Cercle ouvert par moi | E | `Circle` + cycle `ouvert` + membership active de l’ouvreur | tout joueur Monde 1 authentifié | `Circle.ouvrir!` dans une transaction | Crée identité, cycle et membership ; aucun Ω |
| C05 | Demande en attente | E | `CircleMembership.status == demande` | candidat ; lien non bloqué ; cercle cherche des membres et non complet dans la liste | `CerclesController#demander` | Puis redirection vers le fil candidat/ouvreur |
| C06 | Invitation reçue | E | `status == invitation` | invitation créée uniquement par l’ouvreur ; réponse uniquement par l’invité | `Circle#inviter!`, puis accepter/refuser | Aucun tiers ne décide pour l’invité |
| C07 | Membre actif | E | `status == actif`, `joined_at` | ouvreur accepte une demande ou invité accepte | `activer!` / `accepter_invitation!` | maximum dur de 8 ; minimum 5 seulement cible d’animation |
| C08 | Demande/invitation refusée | E | `status == refuse` | décideur légitime selon l’origine | `refuser!` / `refuser_invitation!` | Historique conservé sur la même ligne ; nouvelle demande possible |
| C09 | Membre parti | E | `status == parti`, `left_at` | membre actif sauf ouvreur dans le Lot 1 | `quitter!` | L’ouvreur attend le futur mécanisme de transmission |
| C10 | Cercle complet | E | `memberships.actifs.count >= 8` | validation modèle lors de l’activation | huitième activation | Les demandes ne réservent pas de place |
| C11 | Séance planifiée | E | `CircleSession#scheduled_at`, `mode`, `roles` JSON | membre actif ou admin | `CerclesController#seance` | seuls les ids de membres actifs sont conservés |
| C12 | Mon rôle de séance | E/R | `CircleSession#roles` + référentiel constant `ROLES` | membre actif | affectation lors de la planification | Service temporaire, jamais statut permanent |
| C13 | Pacte-Source absent | E | aucune `PactSourceVersion` | membre actif | publier au moins une réponse | Pas de texte vide |
| C14 | Pacte-Source courant | E | dernière version ordonnée du cycle | membre actif pour publier ; membres pour lire selon page Cercle | création d’une nouvelle version | V1 : `adopted_at` posé immédiatement ; aucun consentement individuel formel |
| C15 | Cycle clos / reventilation | N | constantes prévues, aucune action de clôture ni nouveau cycle exposée | — | Lot 2 à concevoir | Ne pas afficher comme fonction disponible |
| C16 | Traversée collaborative attestée | N | aucune attestation multi-acteurs reliée à `CircleSession` | participants et/ou facilitateur à définir | nouvel objet d’attestation idempotent | Ne pas étendre `validation_authority` pour simuler le multi-acteurs |

## 6. Espaces, fils, messages et notifications

| ID | État visible / action | Maturité | Source de vérité | Droit ou garde serveur | Événement de transition | Effets et limites |
|---|---|---:|---|---|---|---|
| E01 | Fil d’une expérience/parcours | E | `Messaging::Thread` polymorphe, `has_one` sur `ChallengesUser`/`JourneysUser` | propriétaire ou acteur ayant réellement `can?(:edit, container)` | première ouverture : création paresseuse du fil | Un fil ne prouve pas une participation collective |
| E02 | Fil candidat/ouvreur | E | thread dont le conteneur est `CircleMembership` | candidat, ouvreur, admin | demande ou première ouverture | un message ne change jamais le statut de membership |
| E03 | Fil ouvert au Cercle | E | `ouvert_au_cercle` + timestamp sur la membership | consentement du candidat/invité uniquement ; membres actifs du cycle | action explicite `ouvrir_au_cercle` | Opt-in, jamais basculé par l’ouvreur |
| E04 | Envoyer un message | E | `Messaging::Message` | `can?(:show, message.thread)` ; ce droit réutilise `:nested` du conteneur réel | création du message | tester négativement deux joueurs ne partageant qu’une communauté par défaut |
| E05 | Messages non lus | E/R | `messaging_threads_users.last_seen_at` dans la gem | utilisateur concerné | lecture/mark as read de la gem | Le compteur global demande un agrégateur, pas une nouvelle colonne |
| E06 | Notification e-mail de mise en relation | E | `GlobalSettings.notify_of_new_message` + `CircleMembership#thread_participants` | destinataire candidat/ouvreur, sauf auteur | nouveau message → job async | Les fils historiques de Graines restent silencieux |
| E07 | Boîte d’échanges unifiée | N | l’index actuel ne sait agréger que Journey/Challenge et ne remonte pas les fils CircleMembership | droit sur chaque conteneur | interface polymorphe de conteneur à concevoir | Ne pas charger tous les fils puis filtrer en mémoire |
| E08 | Espace communautaire Monde 1 | N | `Community` et index de fils existent, mais aucun modèle d’espace/channel avec intention, participants et cycle de vie | à définir ; jamais la communauté par défaut seule | création d’un espace explicite | La maquette « Espace du Seuil » ne doit pas pointer vers un faux channel |
| E09 | Proposition, objection, consentement, action, mémoire | N | aucun objet structuré dans la messagerie actuelle | à définir par type de fil/action | nouveaux objets/événements, pas simple texte parsé | Un emoji ou mot-clé ne devient pas une décision métier |

## 7. Graines, Traces, Résonances et consentements

| ID | État visible / action | Maturité | Source de vérité | Droit ou garde serveur | Événement de transition | Effets et limites |
|---|---|---:|---|---|---|---|
| G01 | Graine de fin de chapitre présente | E | au moins un message du joueur dans le thread du `ChallengesUser` de fin de chapitre | auteur du fil | envoi du message | L’implémentation ne distingue pas encore une Graine d’un autre message de l’auteur |
| G02 | Validation de fin de chapitre disponible | E | G01 + `end_at` nul | propriétaire | `mark_as_ended` après la garde contrôleur | La présence de la Graine précède la validation |
| G03 | Graine publiée sur le profil | E | `GrainePubliee` unique `(user, message)` | auteur du message uniquement | `publier` | Opt-in explicite et révocable |
| G04 | Graine retirée du profil | E | absence de `GrainePubliee` | auteur | `depublier` | Le message source demeure ; seule la publication disparaît |
| G05 | Graine partagée uniquement avec le Cercle | N | aucun scope de visibilité par Cercle | auteur, consentement à définir | nouvel objet/politique de visibilité | Ne pas détourner `ouvert_au_cercle` d’une candidature |
| G06 | Trace personnelle | N | aucun modèle `Trace` | auteur | nouveau modèle ou registre de productions | Les résultats des mini-jeux existent dans des tables hétérogènes, sans agrégateur canonique |
| G07 | Trace transformée en Graine | N | aucune relation de filiation | auteur + mentor selon contrat futur | événement de cristallisation explicite | Ne pas déduire la transformation d’un texte ressemblant |
| G08 | Résonance reçue | N | aucun modèle `Resonance` | destinataire/auteur et visibilité à définir | création volontaire reliée à une Graine | Un message ou une réaction générique n’est pas une Résonance PZ |
| G09 | Synthèse commune | N | aucun objet ; un futur thread de séance ne suffit pas à distinguer texte commun et discussion | membres/consentement à définir | production puis consentement collectif | Ne jamais absorber les Traces privées dans la synthèse |

## 8. Omégas et callbacks `mathieu_core`

| ID | État visible / action | Maturité | Source de vérité | Droit ou garde serveur | Événement de transition | Effets et limites |
|---|---|---:|---|---|---|---|
| O01 | Total Oméga du joueur | E | `User#omega == points.sum(:point)` | profil propre ; publication communautaire selon politique dédiée | callback de validation d’expérience | Pas de solde actif/passé ni de dépense |
| O02 | Ventilation par expérience | E/R | `Point#challenge_id` | propriétaire | agrégation en lecture | Conserver le lien à l’origine |
| O03 | Ventilation par Puissance/polarité | E | `Point` joint à `Skill#derived_framework`; `User#power_breakdown` | propriétaire ; visibilité publique à consentir | agrégation en lecture | Le référentiel doit employer les libellés canoniques |
| O04 | Attribution | E | `ChallengesUser#validated_at` + `Challenge#challenges_skills` | uniquement chemin de validation autorisé | callback `gain_points` après update | Détruit/recrée les Points du couple user/challenge ; idempotent, ne jamais appeler directement |
| O05 | Rejeu sans perte | E | validation conservée ; Points existants | propriétaire | nouvelle session de format | Ne jamais remettre `validated_at` à nil |
| O06 | Cap collectif 1 000 000 Ω | T/N | aucune table de palier, aucun agrégat historisé ou périmètre validé | — | modèle d’Observatoire à définir | Peut être expliqué au Monde 1, pas affiché comme compteur réel fiable |
| O07 | Domaine de souveraineté | T/N | ventilation Skill utile mais aucune reconnaissance/confirmation de domaine | — | futur mécanisme de proposition et confirmation | Ne pas confondre corrélation de points et expertise constatée |
| O08 | Fonds du Commun / capacité de financement | N | aucune table financière ni règle d’allocation | — | cadrage juridique et comptable puis objets séparés | Les Omégas restent non fongibles et ne sont jamais débités |
| O09 | Cagnotte du Cercle | N | aucune table | consentement du Cercle à définir | futur ledger financier | Strictement séparée des Omégas des membres |

## 9. Profils individuels, profil de Cercle et flow

| ID | État visible / action | Maturité | Source de vérité | Droit ou garde serveur | Événement de transition | Effets et limites |
|---|---|---:|---|---|---|---|
| F01 | Première hypothèse du Moteur individuel | E | dernière `MoteurAssessment` complétée | joueur | fin d’« Une drôle d’époque » | Hypothèse de navigation, confiance faible/moyenne, jamais diagnostic |
| F02 | Caps individuels par Puissance | E | dernière `ConseilSession` complétée, surchargée par `users.moteur_caps` | joueur | Conseil Oméga ou ajustement volontaire | Ne pas moyenner avec les points |
| F03 | État/position d’une Puissance | E/R | configuration de la Puissance + assessment/cap + `power_breakdown` | joueur ; publication par puissance via consentement existant | questionnaire, parcours, nouvelle évaluation | La position Oméga ne mesure pas seule la circulation |
| F04 | Degré d’alchimisation individuel sur 10 | N | aucune formule ou valeur persistée dans le code audité | joueur | formule versionnée et explicable à concevoir | Ne pas inférer seulement de la quantité d’Omégas |
| F05 | Profil du Cercle | N | aucune évaluation des cinq Cadres ni des Puissances systémiques | membres ; périmètre de visibilité à définir | 360° mi/fin de cycle ou expérience complexe | N’est jamais la moyenne des profils individuels |
| F06 | Flow du Cercle | N | aucune mesure ponctuelle ni historique | membres/facilitateur à définir | synthèse d’évaluation systémique | Distinguer état ponctuel, Cadres et Puissances du système |
| F07 | Profil d’organisation | N | aucun modèle | mandat organisationnel et confidentialité à définir | prédiagnostic puis entrée consentie dans le Jeu | Ne jamais agréger silencieusement les Cercles |

## 10. Correspondance des quatre projections de la maquette

| Projection | Montrable avec données réelles aujourd’hui | À garder en teasing ou données fictives |
|---|---|---|
| `entry` | Monde 1 ouvert, Boussole disponible, absence de Cercle, total/ventilation Ω, ressources externes | Espace du Seuil comme channel, compteur du million, domaine reconnu |
| `boussole` | progression du Journey, prochaine expérience, Graine-message existante, invitation/demande de Cercle | traversée solo dédiée tant que son modèle/adaptateur n’existe pas, matching de Cercle, Traces agrégées |
| `circle` | membership active, membres, séance, rôles JSON, Pacte courant, fil de candidature | traversée collaborative attestée, Fresque du Cercle, boîte unifiée, profil systémique |
| `living` | messages accessibles par leurs routes, séances et rôles, catalogue, Pacte versionné | décisions structurées, Résonances, flow, synthèse commune consentie, Commun financier |

## 11. Ordre de portage recommandé

### Lot A — projection sûre sans nouveau métier

1. résolveur `Monde1HomeState` en lecture seule ;
2. états P01–P16, C01–C14, O01–O05 ;
3. liens vers les pages réelles, sans action métier dans la carte ;
4. tests négatifs de droits et tests de requêtes ;
5. états vide, chargement, erreur et données périmées.

### Lot B — unités pédagogiques manquantes

1. parcours Boussole et données d’intensité/rayon/puissance après arbitrage M04–M07 ;
2. session/adaptateur de traversée solo ;
3. attestation multi-acteurs de traversée collective ;
4. agrégateur de productions, puis vrai modèle Trace/Graine si le pilote confirme le besoin.

### Lot C — vie collective

1. espace/channel Monde 1 explicite ;
2. interface polymorphe de conteneur et boîte unifiée ;
3. Résonances ;
4. proposition → objection → consentement → action → mémoire ;
5. profil de Cercle et flow, après protocole d’évaluation validé.

### Lot D — économie et impact

1. Observatoire et paliers Oméga versionnés ;
2. domaines proposés puis confirmés ;
3. Commun financier et ledgers séparés, après cadrage juridique ;
4. aucun débit, transfert ou dépense d’Omégas.

## 12. Recette obligatoire avant tout portage Rails

1. joueur sans Monde 1 : aucun POST Cercle ou Journey Monde 1 ne passe ;
2. joueur Monde 1 : Boussole accessible, catalogue fermé tant qu’elle est incomplète ;
3. étape optionnelle passée : aucun `ChallengesUser`, Point ou validation créé ;
4. ouverture d’une fiche : `ChallengesUser` nu uniquement ;
5. validation : une seule attribution même après double POST ;
6. rejeu : validation et Omégas conservés ;
7. deux joueurs partageant seulement une communauté par défaut ne voient ni n’écrivent dans le fil de l’autre ;
8. candidat et ouvreur voient leur fil ; les membres du Cercle ne le voient qu’après opt-in du candidat ;
9. une demande ou un message ne forme jamais automatiquement un Cercle ;
10. neuf actifs refusés, huit actifs acceptés ;
11. seuls les membres actifs tiennent un rôle ou publient une version du Pacte ;
12. aucune carte ne prétend disposer d’une Trace, Résonance, flow, Commun ou compteur réel absent ;
13. le profil du Cercle, lorsqu’il existera, n’est jamais calculé comme moyenne des membres.

## 13. Décision de sortie

Le **Lot A peut être prototypé dans Rails** après relecture du portable, car il n’écrit aucun nouvel
état métier. Les Lots B à D restent conditionnés aux objets signalés `N`. La maquette interactive
demeure une vision cible : ses données fictives ne deviennent jamais, par simple portage visuel,
des promesses de données disponibles.
