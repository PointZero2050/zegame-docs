# Audit S0 — messagerie de `pointzero-app` et modèle de droits

> Ajout Claude — 2026-08-09. Livrable du lot **S0** exigé par
> [Messagerie Point Zéro — vision cible](messagerie-point-zero-vision-cible.md) § 23 et
> [Espaces de discussion et apprentissage au Monde 1](messagerie-espaces-discussion-monde-1.md)
> § 13, avant tout code des étapes A/S1. Méthode : lecture du code réellement déployé
> (`pointzero-app`, main `2d44869`), mesures sur la base de **production**, et tests
> d'isolation négatifs **exécutés en préprod** — pas déduits.
>
> Les tests d'isolation sont rejouables : `scripts/verifier_isolation_messagerie.rb`
> (28 contrôles, tous verts le 2026-08-09, aucune fuite).

## 1. Carte de l'existant

### 1.1. Tables

| Table | Colonnes | Observations mesurées |
|---|---|---|
| `messaging_threads` | `name, container_type, container_id, photo, kind` | 73 fils. `photo` jamais renseignée, `kind` **partout nul** — deux colonnes héritées de vibe, mortes |
| `messaging_messages` | `message, messaging_thread_id, messaging_message_id, author_type, author_id` | 86 messages. `messaging_message_id` (réponse à un message) existe mais **0 usage** : les sous-fils sont câblés en base, jamais en UI. `author_type` : 100 % `User` |
| `messaging_threads_users` | `last_seen_at, last_notified_at` | 176 lignes. **Marqueurs de lecture, pas participation** : la liste des lecteurs autorisés ne vit pas là |
| `messaging_mentions` | — | **Absente** (existait dans vibe, non portée) |

Conteneurs des 73 fils : `ChallengesUser` 62 (Graines/feedback), `CircleMembership` 6
(candidatures), `JourneysUser` 5 (retours de parcours). Aucun orphelin au jour de l'audit
(l'incident du fil 47 a été purgé le 2026-08-07 ; le risque structurel demeure, § 3.4).

### 1.2. Code — ce qui a été construit depuis la V1

La messagerie actuelle n'est plus celle auditée le 2026-07-31 dans
[analyse-impact-messagerie-cercles.md](analyse-impact-messagerie-cercles.md). Les acquis :

- **`ContexteDeFil`** (spec V1 § 8.1) : une classe par conteneur porte titre, badge, nature
  (`feedback` / `mise_en_relation`), **règle d'accès `visible_par?`**, participants désignés,
  `conteneurs_de(user)` et `chemin_du_fil`. C'est l'unique point d'écriture des droits — la
  faille historique de vibe (`all(:show, :index)` inconditionnel) est fermée, et *testée
  négativement*.
- **Boîte d'Échanges** (`/echanges`) : lecture sans table, non-lus fiables (un fil jamais
  ouvert compte ses non-lus), filtres Tout / Cercles / Expériences et parcours, badge dans la
  barre du haut.
- **Notifications** : `NotificationFilJob`, débounce 10 min, verrou par ligne contre le double
  envoi, courriel sans texte du message ni adresse de tiers, préférence `notifie_par_courriel`
  (globale, par joueur).
- **Candidatures** : dossier de rencontre, `ouvert_au_cercle` (consentement), partage de
  coordonnées (`PartageCoordonnees`/`CarteDeContact` — contexte vérifié AVANT consentement),
  `Blocage` (nouveau contact seulement), `Signalement` (journal minimal), `GrainePubliee`
  (publication par l'auteur seul).

### 1.3. Correspondance avec la taxonomie cible (dix gabarits)

| Gabarit (espaces § 2) | État dans `pointzero-app` |
|---|---|
| Échange individuel | **Partiel** : uniquement contextualisé (candidature). Pas de conversation directe libre |
| Groupe informel | Absent |
| Cercle de croissance | **Le Cercle existe** (cycles, Pacte-Source, séances) mais n'a **aucun espace de discussion** : seuls les fils individuels de candidature existent. Un Cercle constitué n'a nulle part où se parler |
| Cercle fonctionnel | Absent |
| Projet ou mission | Absent |
| Cohorte d'apprentissage | Absent |
| Événement ou territoire | Absent (le mode événement existe, sans discussion) |
| Consultation du Commun | Absent |
| Espace communautaire | Absent (les annonces passent par la newsletter Brevo) |
| Espace sensible temporaire | Absent |

**Le constat central de l'audit** : tout ce qui existe est un fil **1-à-1 adossé à un objet
métier**. Aucune conversation *collective* n'existe — pas même pour le Cercle cœur, premier
utilisateur pressenti de l'étape A.

## 2. Écarts par rapport à l'étape A (souveraineté fonctionnelle)

| Exigence couche 1 | État | Écart |
|---|---|---|
| Conversations privées | Partiel | Seulement contextualisées ; pas de DM libre (question ouverte § 24 de la cible, à arbitrer) |
| Conversations collectives | **Absent** | Le plus gros morceau : aucun modèle d'espace ni de participation explicite |
| Réponses et sous-fils | Absent en UI | La colonne `messaging_message_id` existe, inutilisée — un acquis de schéma |
| Médias et fichiers | Absent | Active Storage installé (photos de profil) : le socle technique est là, tout le reste manque (droits par pièce, antivirus, limites) |
| Réactions emojis | Absent | — |
| Sondages | Absent | — |
| Mentions | Absent | Table non portée |
| Messages épinglés | Absent | — |
| Recherche | Absent | Vérifié négativement (« la recherche n'existe pas, donc ne fuit pas ») |
| Non-lus fiables | **Fait** | Livré le 2026-08-08, 33 contrôles |
| Notifications par espace | Partiel | Préférence globale par joueur ; ni par-espace, ni digest, ni plages de repos |
| Mobile / PWA | Partiel | Vues `pwa/` générées (manifest, service worker) mais **aucune route ne les sert** ; l'UI est responsive |
| Export des données | Absent | — |
| Temps réel | Absent | Solid Cable dans la pile, zéro usage : la page se rafraîchit à la main |
| Édition/suppression d'un message | Absent | Aucun chemin utilisateur — un message est immuable de fait |

Deux manques d'hygiène hors liste : **aucun plafond de longueur** sur `message` (un texte de
plusieurs Mo est accepté) — recommandation : 5 000 caractères ; et **aucune limite de
fréquence** d'écriture.

## 3. Modèle de droits

### 3.1. Règles en vigueur (testées négativement le 2026-08-09)

| Contexte | Lecture = écriture, accordée à |
|---|---|
| Fil d'expérience / de parcours | le joueur concerné, ou **tout administrateur** |
| Fil de candidature | le candidat, l'ouvreur du Cercle, tout administrateur, ou — si `ouvert_au_cercle` — un membre **actif** de ce cycle |
| Fil orphelin | personne, pas même un administrateur |

Invariants vérifiés : l'écriture suit la lecture (même règle, un seul point d'écriture) ; le
consentement `ouvert_au_cercle` se retire ; un refus ne confisque pas le fil au refusé ; la
boîte d'Échanges n'élargit jamais les droits (elle rassemble largement puis `visible_par?`
tranche) ; visiter le fil d'autrui **ne crée plus** le fil (défaut corrigé par ce lot :
le contrôle précède désormais la création).

### 3.2. Écarts de droits vis-à-vis de la cible

1. **« Tout administrateur »** lit tous les fils. La V1 (critère 4) dit « administrateurs
   *habilités* », la cible (principe 7) que voir un contexte ne donne jamais accès à ses
   conversations. Acceptable tant que les fils sont du feedback pédagogique ; **inacceptable
   pour des espaces privés d'étape A**. À restreindre par rôle ou par espace avant S1.
2. **La participation n'est pas un objet** : elle se déduit du conteneur. Tenable pour du
   1-à-1 ; les espaces collectifs exigent une participation explicite (qui est membre, depuis
   quand, avec quel rôle) — c'est LE prérequis de l'étape A.
3. **Le blocage** n'est vérifié qu'à la création d'une candidature. Règle assumée (« ne ferme
   jamais rétroactivement »), mais les espaces libres (DM, groupes) devront le vérifier à
   l'entrée ET à l'écriture.

### 3.3. Modèle minimal proposé — `Espace` sans deuxième système

La cible interdit « un deuxième système de messages sans stratégie de convergence ». Le modèle
minimal qui porte les dix gabarits sans réécrire l'existant :

```text
Espace (nouvelle table)
├── gabarit        : echange | groupe | cercle | ... (string, PAS un droit)
├── contexte       : polymorphe optionnel (Circle, Event, Journey…)
├── finalite       : texte affiché, obligatoire (création guidée, espaces § 5)
├── etat           : prepare | ouvert | en_pause | clos | archive
├── gardien_id     : User
└── EspaceMembership (nouvelle table)
    └── user, role (participant | gardien), rejoint_le, quitte_le, notification (tout | mentions | digest | silencieux)

Messaging::Thread
└── espace_id      : NULLABLE — un fil appartient à un espace OU à un conteneur
```

- **Les fils actuels ne migrent pas** : un fil de feedback (`ChallengesUser`, `JourneysUser`)
  n'est *pas* un espace de discussion — c'est une carte de la couche 2 avant l'heure. Ils
  gardent `ContexteDeFil` tel quel.
- **La règle d'accès reste unique** : `visible_par?` s'enrichit d'une branche — si le fil a un
  `espace_id`, la participation explicite décide ; sinon le contexte décide, comme
  aujourd'hui. Un seul point d'écriture, testé négativement dans les deux branches.
- La candidature de Cercle *pourra* devenir le premier `Espace` (gabarit « échange
  individuel ») par une migration de données réversible — mais rien ne l'exige pour démarrer.
- `kind` ne donne jamais un droit (invariant des espaces § 11) : `gabarit` choisit l'UI et les
  protocoles, `EspaceMembership` donne l'accès.

## 4. Proposition de migration

Ordonnée pour que chaque pas soit utile seul et réversible seul :

1. **A0 — hygiène** (peut précéder tout le reste) : plafond de longueur des messages,
   restriction du droit administrateur (rôle `moderation` explicite), décision sur les deux
   colonnes mortes (`photo`, `kind`).
2. **A1 — `Espace` + `EspaceMembership`**, gabarits `groupe` et `cercle` seulement, création
   réservée à l'administration : le **Cercle cœur** devient le pilote (critère 1 de la cible),
   avec son espace de discussion collectif. `Messaging::Thread.espace_id` nullable — retour
   arrière = ignorer la colonne.
3. **A2 — le socle conversationnel** dans les espaces : sous-fils (la colonne existe),
   mentions, réactions emojis. Rien de tout cela ne touche les fils contextuels existants.
4. **A3 — médias** (Active Storage, droits portés par le message, limites et antivirus à
   arbitrer), puis sondages.
5. **A4 — notifications par espace** (la colonne `notification` d'`EspaceMembership` § 3.3),
   digest, PWA réellement servie.
6. **A5 — recherche et export**, contraints par `visible_par?` dès la conception (le contrôle
   négatif § 10 du script tombera ce jour-là et le rappellera).

À chaque étape : `pg_dump` avant migration (pratique en place), vérification en préprod,
promotion par cherry-pick — la mécanique éprouvée depuis vingt lots.

## 5. Stratégie de tests et de retour arrière

- **Le harnais existe et est au dépôt** : `verifier_isolation_messagerie.rb` (28 contrôles
  négatifs), `verifier_echanges.rb` (33), `verifier_fils*.rb`, `verifier_partage*.rb`. Règle
  du lot : *aucun nouveau gabarit d'espace ne s'active sans ses contrôles négatifs propres* —
  y compris les « tests négatifs entre espaces » (critère 11 de la cible).
- Les contrôles d'**absence** (recherche, § 10) transforment chaque fonctionnalité future en
  rappel explicite de sa contrainte de droits.
- **Retour arrière** : `espace_id` nullable et branche conditionnelle dans `visible_par?` —
  désactiver la branche restaure l'existant à l'identique ; les tables nouvelles se suppriment
  sans toucher `messaging_*` ; sauvegardes quotidiennes + `pg_dump` pré-migration, restauration
  répétée le 2026-08-06.

## 6. Estimation séparée (en lots de la cadence actuelle)

Un « lot » = une séance construite-vérifiée-promue, comme les vingt derniers.

| Étape | Contenu | Estimation | Risque dominant |
|---|---|---|---|
| **A0** | hygiène (longueur, droits admin, colonnes mortes) | 1 lot | aucun |
| **A** | A1→A5 ci-dessus | **8 à 12 lots** | les médias (droits, stockage, antivirus) et la PWA hors-ligne ; le reste est du connu |
| **B** | espaces Projets/Commun, vues Fil/Actions/Décisions/Mémoire, cartes structurées, réactions sémantiques, consentement | **10 à 15 lots** | dépend d'objets qui n'existent pas encore (Mission, Décision, Résonance) : l'estimation est conditionnée à leurs specs |
| **C** | polarités, cinq Cadres, miroir IA, redistribution | **non estimable en lots** | à prototyper avec un Cercle pilote (ce que la cible prescrit elle-même) ; exige les arbitrages § 24 |

L'étape A n'a **pas sa place avant le Festival** : rien du 1er octobre n'en dépend, et le
chemin critique (composition de la journée, feu vert, DNS) passe devant. A0 peut se glisser
n'importe quand ; A1 est un bon premier chantier d'octobre, avec le Cercle cœur comme pilote.

## 7. Corrections déjà appliquées par ce lot

- **Le fil se créait avant le contrôle d'accès** (`threads_controller.rb`) : un tiers renvoyé
  laissait derrière lui un fil créé à son passage. Le contrôle précède désormais la création —
  testé négativement (« visiter ne crée pas »).

## 8. Décisions avant S1 — **arbitrées par Boris le 2026-08-09**

1. Les **conversations directes libres** : **sur consentement de contact**. Le gabarit
   « échange individuel » s'ouvre par un consentement explicite (dans l'esprit du partage de
   coordonnées §5.1 déjà en place), pas par l'appartenance à un Monde. Le blocage se vérifie à
   l'entrée ET à l'écriture. → chantier S1.
2. Le **droit de lecture des administrateurs** : **rôle modération explicite**.
   **Fait le 2026-08-09** (`pointzero-app`, A0) : colonne `users.moderation`, habilitation
   orthogonale au rôle, révocable en console, personne par défaut ; les trois portes
   (expérience, parcours, candidature) exigent le mandat, testé négativement sur ses deux
   faces. Mandat accordé au seul opérateur réel (boris@ze.game).
3. **Importer l'historique WhatsApp** du Cercle cœur : **oui, si possible**. C'est possible :
   WhatsApp exporte chaque conversation en `.txt` horodaté (médias optionnels), parsable par un
   script d'import une fois l'espace du Cercle créé (A1). À prévoir comme un lot propre —
   auteurs à rapprocher des comptes, médias à décider, et l'import reste une copie : rien ne
   se synchronise.
4. Le **plafond de longueur** : **5 000 caractères**. **Fait le 2026-08-09** (A0), refus poli
   plutôt qu'erreur serveur, testé.
