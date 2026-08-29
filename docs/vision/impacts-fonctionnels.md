# Analyse fonctionnelle — impacts back/front

<!-- Ajout Claude, 2026-07-12, sur demande de Boris (retours wireframe accueil v1) -->

Ce document est le registre d'analyse d'impact : chaque nouvelle page ou fonctionnalité front y est modélisée avec ses impacts sur le backoffice, les modèles de données et la cohérence d'ensemble. **Règle de travail : aucune page ne passe en implémentation sans sa ligne d'analyse ici.** Claude et Codex le tiennent à jour ; les arbitrages restent à Boris.

Contexte : ces impacts visent l'**application dédiée Point Zéro** (décision du 2026-07-12, cf. [accueil-point-zero.md](accueil-point-zero.md) §13). Depuis le 2026-07-24, sa trajectoire Festival est cadrée dans [application-festival-2026.md](application-festival-2026.md) : code issu de l'existant, base séparée et aucune dépendance d'exécution aux gems privées. Les modalités précises de migration des comptes restent à arbitrer.

## 1. Registre des impacts identifiés

### F1 — Module News ✅ IMPLÉMENTÉ (2026-07-14)

Implémenté dans vibe.ze.game. **Architecture retenue : sync WordPress → table locale unique** (`news_items`, source `internal`/`wordpress`).
- Modèle `NewsItem` : title, excerpt, content, link, image_url, source, external_id, featured (un seul à la fois via after_save), published_at, expires_at (les news expirées disparaissent). Scope `visible` = publiée et non expirée.
- Service `NewsSync` : récupère les événements WordPress (API The Events Calendar `tribe/events/v1/events`), upsert par external_id, supprime les WP disparus, décode les entités sur-encodées (Nokogiri). Le flag `featured` posé en admin n'est jamais écrasé. Cron horaire installé (crontab daployar → `NewsSync.call`).
- Admin `/admin/news_items` : liste (source, featured, dates), bouton « Synchroniser WordPress », CRUD interne, toggle featured.
- Accueil : bloc « À la une » (featured, fallback = news la plus récente) + « Autres actualités » (liste). Le Festival WP est featured pour la démo.
- Reste : blog WP (wp/v2/posts) en V2 ; labels admin en anglais/humanisés (polish i18n).

### F1 (ancienne fiche) — Module News

**Origine front** : bloc "À la une" sur l'accueil (état nouveau joueur, extensible aux autres états).

| Aspect | Impact |
|---|---|
| Modèle | Nouvelle entité `News` : titre, corps, lien, image, dates de publication/expiration, flag `featured` |
| Backoffice | CRUD News + choix de la featured news (une seule à la fois ?) |
| Front | Bloc "À la une" (featured) ; à décider : liste des news non-featured (où ?) |
| Questions | Une news par communauté/monde ou globale ? Qui peut publier ? |

### F2 — Mode de progression d'un parcours (libre / linéaire) ✅ IMPLÉMENTÉ (2026-07-14)

Implémenté dans vibe.ze.game : colonne `progression_mode` (libre/lineaire, défaut libre), option dans le formulaire admin parcours, verrous dans la vue parcours, garde d'accès (redirection vers le parcours avec message), Monde 0 passé en linéaire. Décisions associées : les Pages/chapitres ne sont plus cliquables (leur vue dédiée était inutile) ; le numéro/nom du chapitre s'affiche dans le détail de l'Action ; une Action en attente de validation pédagogique bloque la suivante.


**Origine front** : Monde 0 linéaire (une Action accomplie ouvre la suivante) ; parcours actuels libres.

| Aspect | Impact |
|---|---|
| Modèle | Champ `progression_mode` sur Journey : `libre` (défaut, comportement actuel) / `linéaire` |
| Backoffice | Option dans la page de gestion d'un parcours |
| Front | Mode linéaire : Actions verrouillées 🔒 après l'Action courante ; vue "parcours entier" avec états fait/en cours/verrouillé |
| Logique | Le déverrouillage suit l'ordre `challenges_journeys.position` ; définir l'interaction avec `auto_validated` (validation pédagogique bloque-t-elle la suite ?) |
| Lien vision | Modes envisagés dans [accueil-point-zero.md](accueil-point-zero.md) §7 (séquentiel/libre/guidé/conditionnel/temporel) — commencer par libre/linéaire |

### F2b — Expérience obligatoire ou optionnelle dans un parcours ✅ IMPLÉMENTÉ (2026-07-24)

<!-- Ajout Codex - 2026-07-24. Décision Boris : permettre de passer une expérience exigeante, notamment un Sas d'entrée, sans abandonner le parcours. -->

Implémenté dans vibe.ze.game par Claude, commit `3c675d0` : `required` et `optional_note` sur l'inclusion `ChallengesJourney`, état de saut séparé dans `ChallengesJourneysUser`, déverrouillage de la suite en progression linéaire, reprise possible, absence d'Oméga et de fausse validation lors du saut, prise en compte des seules expériences obligatoires pour l'accomplissement. Vérifié en lecture le 2026-07-24 sur la branche serveur `pointzero`, worktree propre. Le parcours Monde 0 expose les nouveaux contrôles, mais ses treize expériences sont encore toutes cochées obligatoires : la configuration du Sas reste à appliquer.

Une expérience peut être **obligatoire ou optionnelle dans un parcours donné**. Ce caractère appartient à son inclusion dans le parcours (`ChallengesJourney`), et non au `Challenge` lui-même : une même expérience peut être structurante dans un parcours et facultative dans un autre.

| Aspect | Impact |
|---|---|
| Modèle | Ajouter `required` (booléen, défaut `true`, non nul) à `challenges_journeys`. Le défaut obligatoire préserve le comportement de tous les parcours existants. |
| Progression joueur | Enregistrer le saut séparément de la validation, par joueur et par inclusion dans le parcours (`user_id`, `challenges_journey_id`, `skipped_at`). Un saut ne doit jamais créer une fausse validation de l'expérience. |
| Parcours linéaire | Une expérience optionnelle atteinte reste l'étape courante jusqu'à ce que le joueur l'accomplisse ou choisisse explicitement « Passer cette étape ». Le saut déverrouille alors la suite. |
| Accomplissement | Seules les expériences obligatoires doivent être validées pour accomplir le parcours. Les expériences optionnelles non commencées ou passées ne bloquent ni la fin du chapitre ni celle du parcours. |
| Retour | Une expérience passée reste accessible avec une action « Reprendre cette expérience ». Si elle est ensuite accomplie, son état visible devient « réalisée » tout en conservant l'historique du saut si cette information est utile. |
| Oméga | Passer une expérience ne génère aucun Oméga et n'entraîne aucune pénalité. Les Oméga sont attribués uniquement si l'expérience est réellement accomplie selon ses critères. |
| Backoffice | Dans la construction du parcours, proposer « Obligatoire » / « Optionnelle » sur chaque expérience ajoutée, avec une courte explication éditoriale facultative pour justifier l'option. |
| Front | Badge « Optionnelle » sur la carte et le détail ; bouton secondaire « Passer cette étape » ; confirmation sobre : « Cette expérience est optionnelle. Tu pourras y revenir plus tard. » |
| Statistiques | Distinguer `réalisée`, `passée`, `en cours` et `non commencée`. Ne pas compter un saut comme un accomplissement de l'expérience. |
| Garde-fou | Une expérience indispensable à la sécurité, au consentement ou à la compréhension d'une activité ne doit pas devenir optionnelle sans proposer une voie équivalente. |

Pour le Monde 0, le **Sas d'entrée** devient le premier cas d'expérience optionnelle. L'**Atelier Point Zéro reste obligatoire** : il est le rite de passage vers le Monde 1 et peut être vécu en présentiel ou en distanciel. La matrice de révision complète se trouve dans [monde-0-matrice-revision.md](../pedagogie/monde-0-matrice-revision.md).

### F3 — Parcours obligatoire (tutoriel de Monde) ✅ IMPLÉMENTÉ (2026-07-14)

Implémenté dans vibe.ze.game : colonne `mandatory` (bool, défaut false) sur journeys, switch dans le formulaire admin, gating au niveau du Monde (= communauté). Design retenu (question « un seul obligatoire ? ») : pas de contrainte d'unicité — un Monde se déverrouille quand TOUS ses parcours obligatoires sont accomplis (`Community#mandatory_completed_by?`), ce qui couvre 1 tutoriel ou plusieurs prérequis. « Accompli » = tous les challenges du parcours validés (`Journey#completed_by?`). Front : dans le catalogue, les parcours non-obligatoires d'un Monde verrouillé sont grisés 🔒 avec un message, le tutoriel porte un badge « À commencer » ; garde d'accès sur la vue parcours. Monde 0 marqué obligatoire. Effet front peu visible pour l'instant (Monde 0 = un seul parcours) — mécanique validée par test, pleinement utile dès que le Monde 1 aura plusieurs parcours (F4).

### F3 (ancienne fiche) — Parcours obligatoire (tutoriel de Monde)

**Origine front** : chaque Monde s'ouvre par un petit parcours de base servant de tutoriel.

| Aspect | Impact |
|---|---|
| Modèle | Flag `mandatory` sur Journey + rattachement Journey → Monde (préfigure la hiérarchie Marelle → Monde → parcours) |
| Backoffice | Option "parcours obligatoire" dans la gestion d'un parcours |
| Front | Le parcours obligatoire non accompli masque/verrouille le reste du Monde ; l'accueil le met en avant |
| Questions | Un seul obligatoire par Monde ? Que voit un joueur qui saute le tutoriel d'un Monde déjà exploré ? |

### F4 — Marelle : passage mono-parcours → multi-parcours

**Origine front** : Monde 0 = un seul parcours ; dès le Monde 1, choix multiple. L'entrée "Marelle" de la nav correspond à une page type `/journeys`.

| Aspect | Impact |
|---|---|
| Modèle | **Décision 2026-07-13 : modèle `World` distinct**, contenant plusieurs Journeys ; `Community` reste un collectif et `WorldAccess` porte le droit d'accès du joueur. Cf. [navigation-vues-ensemble.md](navigation-vues-ensemble.md) |
| Front | Page Marelle = catalogue de parcours du Monde courant + pédagogie explicite du passage ("tu peux désormais mener plusieurs parcours de front") |
| UX | Moment de seuil à soigner : l'arrivée au Monde 1 change la règle du jeu |

### F5 — Récit, Graines de Récit et mentors IA

**Origine front** : remplace le feedback actuel. À la fin d'un parcours ou à des étapes-clés, le joueur fait le point avec un mentor IA (héros d'une bibliothèque de mentors) et produit une **Graine de Récit**. Les résonances des autres joueurs germent sur les Graines.

| Aspect | Impact |
|---|---|
| Modèle | `Mentor` (bibliothèque : nom, personnage, prompt/persona, visuel) ; `StorySeed` (auteur, parcours/étape source, contenu issu de la conversation, mentor, visibilité) ; destinataires explicites si la Graine est partagée avec des personnes choisies ; résonances rattachées aux Graines (évolution de la messagerie actuelle ou nouvel objet) |
| Backoffice | Gestion de la bibliothèque de mentors ; configuration des déclencheurs (fin de parcours / étapes-clés d'un parcours long) |
| IA | Conversation mentor = intégration LLM (nouveau composant technique — API, coûts, modération) ; le joueur valide/corrige la Graine produit (garde-fou : l'IA n'impose jamais le sens, cf. [relations-recits-collectifs.md](relations-recits-collectifs.md) §2) |
| Existant | Un exemple de mentor existe dans le parcours Monde 0 actuel de vibe.ze.game — à documenter comme référence |
| Lien vision | Concrétise le "récit-fresque" ([relations-recits-collectifs.md](relations-recits-collectifs.md)) : Graine ≈ bloc narratif |

#### Visibilité choisie Graine par Graine

<!-- Ajout Codex - 2026-07-24. Décision Boris : le joueur choisit à qui il partage chaque Graine de Récit. -->

La création d'une Graine et son partage sont deux actes distincts. **Une Graine privée satisfait le prérequis de fin de chapitre** : le joueur n'a jamais à rendre public un récit intime pour progresser.

Le joueur choisit, pour chaque Graine :

- **Moi uniquement** — choix par défaut ;
- **une ou plusieurs personnes choisies** ;
- **mon Cercle** ;
- **une communauté choisie** ;
- **public**, avec confirmation explicite et possibilité de produire une version publique distincte ou anonymisée.

Avant le partage, il peut préciser le type de Résonance souhaité : **être seulement écouté**, recevoir des **questions**, demander un **miroir**, chercher une **mise en relation** ou ouvrir une **proposition d'action**. La visibilité reste modifiable et révocable ; sa réduction coupe les nouveaux accès sans effacer silencieusement les Résonances déjà reçues. Les destinataires ne peuvent résonner que tant qu'ils ont accès à la Graine. Aucun like, classement ou partage par défaut n'est ajouté.

### F6 — Oméga (Cosmo Coin Oméga)

**Origine front** : indicateur de progression manquant. Monnaie de conscience = points des Actions + progression dans les 7 puissances. Représentation : lemniscate Lumière — Point Zéro — Ombre, animée selon l'amplitude.

| Aspect | Impact |
|---|---|
| Modèle | **Décision Boris, 2026-07-24** : les points par compétence gagnés dans les parcours constituent le **socle V1 de l'Oméga**. Une couche ultérieure de Contributions Oméga pourra compléter ou pondérer ce socle à partir de capacités manifestées, de Résonances et d'effets concrets documentés. La formule et le statut de cette pondération restent à expérimenter ; cf. [cosmo-coin-omega.md](cosmo-coin-omega.md) §1.1. |
| Front | Composant lemniscate réutilisable (chip compacte + carte détaillée) ; animation d'amplitude Ombre/Lumière à définir en fonction de données réelles |
| Garde-fou | L'Oméga ne doit pas devenir un score de conscience public ni un classement ([monde-miroir.md](monde-miroir.md) §13). Une contribution ne se réduit ni à un nombre de réactions ni à une validation IA. Le vocabulaire d'interface retenu est uniquement « Oméga ». |
| Prototype | Première interprétation visuelle dans le proto `point-zero-home` (état `monde0`) |

### F7 — Mode événement d'un parcours

**Origine front** : page Festival-direct. Les expériences d'un événement correspondent à un parcours, avec un mode d'affichage et des champs spécifiques.

| Aspect | Impact |
|---|---|
| Modèle | Flag/mode `event` sur Journey + champs par Action : `format`, `salle`/`lieu`, référentiels multiples (7 puissances, 5 cadres...) + **`Session`** : un même atelier proposé plusieurs fois dans la journée (tranche horaire, capacité et compteur de participants PAR session) |
| Facilitateurs | Rattachement d'un ou plusieurs facilitateurs à une expérience ; interface de **validation en masse** (principalement : valider la présence réelle à l'atelier) ; pas de bouton feedbacks côté joueur en mode événement |
| Vue détail | Réutilise la vue Action existante (type journeys/.../challenges/...) sans le bouton FEEDBACKS, avec ajout Format / Lieu / Tranche horaire et sélecteur de créneau ; le bloc Ressources des challenges actuels est conservé, rempli ou non par les facilitateurs (section masquée si vide) |
| Backoffice | Statut « événement » activable sur un parcours → les expériences s'affichent en mosaïque (au lieu de linéaire) ; gestion des salles et des sessions ; suivi des compteurs ; rattachement des facilitateurs |
| Front | Affichage mosaïque (grille filtrable) au lieu de la liste ; états disponible/recommandé/vécu/à intégrer/complet ; compteur "8/15" visible |
| Technique | Compteur de participants = donnée temps réel (SSE existant réutilisable ?) ; contraintes jour J : cache, QR codes, charge (cf. [accueil-point-zero.md](accueil-point-zero.md) §9) |
| Deadline | Festival confirmé le 1er octobre — chemin critique |

### F8 — Vocabulaire

| Décision | Détail |
|---|---|
| Challenge → **Action** | Retenu (lien sociétariat : en entrant dans la Marelle, les joueurs deviennent sociétaires du Point Zéro et génèrent des Oméga). "Expérience" conservé pour les moments vécus en événement. À confirmer définitivement avant implémentation. |
| Feedback → **Graine de Récit + résonances** | Cf. F5 |
| Points → **Oméga (Ω)** | Cf. F6 |

### F9 — Inscription événement et rattachement du billet

<!-- Ajout Codex, 2026-07-13 -->

**Origine front** : états `festival-inscription`, `festival-lier` et `festival-confirme` du wireframe v2.1. Le joueur doit passer de « intéressé » à « inscrit » même si l'adresse e-mail de son compte diffère de celle de l'achat.

| Aspect | Impact |
|---|---|
| Modèle | `EventRegistration` séparé du compte : événement, fournisseur (`woocommerce`/`stripe`/manuel), identifiants externes de commande et de billet, statut de paiement, statut de rattachement, `user_id` nullable, code/jeton à usage unique, date de check-in |
| Identité | **DÉCIDÉ (Boris, 2026-07-13) : lien magique par billet = mécanisme principal, code de secours en backup.** Chaque billet émis contient dans son e-mail un lien signé « Activer mon billet dans l'appli » (jeton à usage unique, expirable). Cas multi-billets : l'acheteur transfère à chaque participant l'e-mail de son billet — chacun active le sien sur son propre compte (dispatch naturel). Si le lien échoue (e-mail perdu, transfert raté) : saisie du code inscrit sur le billet ou scan de son QR. Pistes non retenues pour le pilote : jeton de contexte au départ de l'appli, rapprochement automatique/assisté par e-mail — un seul chemin à expliquer aux participants et à implémenter côté WordPress. L'e-mail d'achat reste une donnée de contact, jamais une preuve de propriété |
| Backoffice | Pour chaque événement : mode d'inscription, URL externe, identifiant fournisseur, dates de vente, capacité, URL de retour ; recherche et rattachement manuel d'un billet ; resynchronisation ; journal d'erreurs |
| Front | CTA « M'inscrire », retour après paiement, « J'ai déjà un billet », confirmation, billet disponible hors connexion ; l'état inscrit pilote la priorité de l'accueil |
| Pont WordPress | Extension légère côté WordPress : à l'émission de chaque billet, générer le jeton d'activation, l'injecter dans l'e-mail du billet (bouton « Activer mon billet dans l'appli ») et notifier l'appli des changements de statut de commande. L'API Event Tickets permet l'accès authentifié aux participants ; les webhooks WooCommerce peuvent notifier les changements de commande |
| Exploitation | Vérifier le statut WooCommerce qui déclenche la création et l'envoi du billet. Event Tickets Plus attend par défaut une commande `completed`, avec possibilité de choisir d'autres statuts dans ses réglages d'intégration |
| Paiement natif | Alternative ultérieure avec Stripe Checkout et webhook idempotent. L'appli devient alors propriétaire des produits, prix, taxes, remboursements, stocks, billets et support de paiement |
| Sécurité | Vérifier les signatures, rendre les traitements idempotents, ne jamais exposer les identifiants de commande comme preuve suffisante, expirer les jetons de rattachement et journaliser les changements d'utilisateur |

**Décision proposée pour le Festival pilote** : conserver Event Tickets Plus + WooCommerce + Stripe et développer le pont d'identité. La billetterie native n'est à envisager qu'après mesure des limites réelles du tunnel existant et confirmation d'un besoin récurrent multi-événements.

Références techniques officielles : [intégration Event Tickets + WooCommerce](https://theeventscalendar.com/knowledgebase/woocommerce-integration-feature/), [API REST Event Tickets](https://theeventscalendar.com/knowledgebase/event-tickets-rest-api/), [webhooks WooCommerce](https://developer.woocommerce.com/docs/best-practices/urls-and-routing/webhooks/), [Stripe Checkout et fulfillment](https://docs.stripe.com/checkout/fulfillment).

### F10 — Mondes, accès et passages automatiques

<!-- Ajout Codex, 2026-07-13 -->

| Aspect | Impact |
|---|---|
| Modèle | `World`, `WorldAccess`, `WorldUnlockRule` et journal des passages ; association World → Journeys et optionnelle World ↔ Communities |
| Règles | Types progression, validation humaine, invitation, rôle/certification, manuel et code historique |
| Technique | Événement métier après validation, job idempotent après commit, notification, reprise sur erreur et override admin ; ne pas densifier les callbacks sensibles |
| Visibilité | Mondes principaux visibles verrouillés ; Mondes privés invisibles sans entitlement |
| Migration | Les tokens de Community restent une compatibilité/invitation, pas le passage normal entre Mondes |

### F11 — Cercle progressif (révisé Boris 2026-07-13)

> **Révision canonique Boris/Codex - 2026-07-31.** F11 doit désormais être relu à travers
> [cercles-croissance-profils-flow-omega.md](cercles-croissance-profils-flow-omega.md). Le Cercle de
> croissance commence au Monde 1, réunit 5 à 8 personnes, apprend cinq rôles liés aux cinq cadres,
> possède un Pacte-Source et distingue identité durable, cycles et lignées. Au Monde 2 s'ajoutent
> facilitateur certifié, abonnement et engagement annuel. La « comptabilité Ω du Cercle » ci-dessous
> est remplacée par des enveloppes de mission temporaires, intégralement distribuées aux individus.

| Aspect | Impact |
|---|---|
| Front | Monde 0 : écran de seuil + vidéo ; Monde 1+ : **Mes Cercles**, **Ouvrir un Cercle**, **Cercles à découvrir**, puis page du Cercle avec cycle, rôles, Pacte-Source, séances, profil systémique, missions et lignée |
| Modèle | Un seul Cercle de croissance dès le Monde 1 ; identité durable `Circle`, incarnations `CircleCycle`, appartenances multiples, Pacte-Source versionné, rôles, facilitateur, évaluations systémiques et enveloppes de mission sans solde Ω collectif |
| Profil et contact V1 | Annuaire et profil communautaire à visibilité choisie ; dossier de rencontre partagé avec un Cercle précis ; coordonnées révélées uniquement par consentement explicite |
| Messagerie V1 | Réemploi de `Messaging::Thread` / `Messaging::Message` pour un fil rattaché à la demande d'adhésion ou invitation ; e-mail de notification seulement ; pas de messagerie directe générale |
| Audit additionnel | Conteneur polymorphe, participants et scopes de `mathieu_core_messaging`, vues supposant Challenge/Journey, callbacks `receive_message_extra`, notifications, droits inter-communautés et suppressions en cascade ; voir [spec V1](profil-communautaire-messagerie-cercles-v1.md) |
| Écarté | Page dédiée « cercle Monde 2 » ; distinction DiscussionCircle/GrowthCircle |

### F12 — Ressourcerie en six cartographies

| Aspect | Impact |
|---|---|
| Taxonomie | Pensées, Pratiques, Experts, Projets, Communautés, Événements ; `Chrysalide` devient un sous-type/qualificatif de Projet |
| Modèle | Graphe de noeuds et relations, pas six silos ; recherche globale, facettes par type et relations affichables |
| Front | Six portes orientées Comprendre, Pratiquer, Rencontrer, Soutenir, Rejoindre, Vivre ; vues liste/carte |

### F13 — Profil, accomplissements, contributions et puissances

<!-- Note Codex - 2026-07-24. Les Open Badges sont différés. La première version du Profil ne présente que des badges internes. -->

| Aspect | Impact |
|---|---|
| Oméga | Séparer solde disponible et contribution cumulée ; bloc « Ce que tes Oméga ouvrent » = texte d'ambition + vidéo (mécanisme régénératif complet en horizon, cf. [cosmo-coin-omega.md](cosmo-coin-omega.md)) ; aucune lecture comme score de conscience ; représentation lemniscate animée en synthèse du profil |
| Mon Récit | **4e sous-menu du profil (Boris, 2026-07-13)** : page dédiée avec résumé global évolutif en entrée (régénéré avec le mentor à chaque Graine, toujours validé par le joueur) + fil des Graines avec résonances consultables. Limite par Graine : 800 caractères (recommandation Claude dans la fourchette 500-1 000 décidée par Boris — ajustable) |
| Navigation | Cinq dimensions cibles : **Vue d'ensemble**, **Puissances**, **Mes Récits**, **Accomplissements**, **Contributions**. Leur profondeur peut être déployée progressivement sans multiplier les concepts dans la première interface. |
| Accomplissements | Deux familles de badges internes : **complétion de parcours**, reconnaissable immédiatement et illustrée par l'image du parcours recadrée en médaillon ; **seuils gamifiés**, visibles ou secrets, représentés par des sceaux géométriques. Aucun standard Open Badge ni valeur d'attestation externe dans le périmètre actuel. |
| Obtention | Petit seuil : notification discrète. Seuil narratif ou secret : carte de révélation à une respiration du parcours. Fin de parcours : médaillon intégré à l'écran final. Tous restent consultables dans « Accomplissements » sans rejouer l'animation. Les obtentions simultanées sont regroupées. |
| Contributions | Une Contribution Oméga relie capacités manifestées, Résonances chez d'autres personnes et effets concrets sur le collectif ou le monde. Elle est documentée par des regards et traces proportionnés à son enjeu. Le Profil doit raconter cette manifestation, pas afficher une note de popularité. |
| Puissances | Six axes Ombre/Lumière et Transcendance en synthèse ; **échelle révisée Boris 2026-07-31 : Entravé · Fragile · En chemin · Intégré · En flow**, synthétisée dans l'interface en Bloqué / En chemin / Intégré ; évaluation individuelle alimentée par les parcours, distincte des profils systémiques de Cercle et d'organisation ; source/date/visibilité des lectures ; privé par défaut |
| Sécurité | Pas de diagnostic automatisé, de classement public ou de partage sans consentement explicite |

Pour le Monde 0, un premier lot resserré de seuils peut tester cette grammaire sans saturer le Profil : **Entrer dans le Jeu**, **Le Moteur s'éveille**, **Un futur regardé en face**, **Graine semée**, **Le futur renvoie la balle**, et le secret **Les futurs sont pluriels**. Le seuil des **100 premiers Oméga** reste transversal et devrait marquer le passage vers le Monde 1 plutôt que la seule conclusion du Monde 0 ; vérifier le barème courant avant implémentation.

### F14 — Conseil du Seuil (évaluation initiale du Moteur) ✅ IMPLÉMENTÉ v0.1 (2026-07-16)

Implémenté dans vibe.ze.game par Claude, d'après [11_evaluation_initiale_moteur.md](../pedagogie/corpus-point-zero/11_evaluation_initiale_moteur.md) et les arbitrages de [conseil-du-seuil-design.md](../pedagogie/conseil-du-seuil-design.md).
- **Modèle `MoteurAssessment`** (table `moteur_assessments`) : passations historisées (jamais réécrites), versionnées (dispositif + scoring), `answers`/`result` en JSONB, contexte de passation, statuts in_progress/completed/abandoned. `User has_many :moteur_assessments`.
- **Contenu versionné** : `config/conseil_du_seuil.yml` — Appel resserré à 5 questions (A6 verticales différée), 6 scènes avec gestes-sources (inspiration documentée + mention adaptation Point Zéro), Don au Commun (2 gestes familiers + 1 difficile), formulations adoucies avant restitution (aucun libellé O1-O3/L1-L3 ni terme chargé).
- **Flow** : `/conseil-du-seuil` (layout immersif dédié, DA « archéologie civique du futur », progression, reprise automatique, retour arrière). Étapes : seuil+contexte → Appel ×5 → ouverture narrative → 6 scènes (polarité → geste-source révélé → intensité, textes adaptés à la polarité choisie → mouvement inverse) → Don au Commun → premier miroir.
- **Calcul provisoire** (corpus §15) : amplitude de la polarité non choisie = inconnue (jamais zéro) ; circulation `bloque_probable`/`intermediaire_probable`/`libre_declare` ; confiance faible/moyenne au maximum ; « libre » toujours déclaratif.
- **Premier miroir** : Appel restitué (sans moyenne générale), lemniscate provisoire (lobes = moyennes des amplitudes déclarées par polarité), 6 tendances (mouvement spontané + « à explorer » + confiance), 3 portes explicables (circulation / élan disponible / conscientisation — jamais uniquement correctif), message de clôture canonique, « Refaire le Conseil » (nouvelle passation).
- **Profil** (révisé Boris, 2026-07-16) : le **lemniscate vivant du Moteur** est affiché sur le Profil (fond Ombre→Lumière, horizon gris, lobes violets indépendants, pôles, Source, point d'or en circulation — partial `users/_moteur.html.haml`). Sans passation : état graine + CTA « Franchir le seuil ». Avec passation : lobes = moyennes des amplitudes déclarées par polarité du premier miroir, avec mention explicite « Évaluation provisoire, issue de ton Conseil du Seuil du [date]. Elle évoluera au fil de tes parcours, de tes Graines de Récit et des regards croisés. » Le garde-fou initial (le miroir n'alimente pas le violet) est **assoupli par décision de Boris** : le violet affiche le provisoire tant que l'évaluation 360° consolidée n'existe pas, la provisorité étant toujours nommée. L'ancien lemniscate placeholder du bloc Oméga est retiré.
- **Voix Point Zéro appliquée (contenus v0.2, 2026-07-16)** : réécriture éditoriale de `conseil_du_seuil.yml` selon la [charte de voix](voix-point-zero.md) — une torsion par écran narratif, un détail révélateur par scène (tableur défunt, pendule arrêtée, slides des deux camps, pause café inaudible, micro à moitié fidèle, graphiques contradictoires, vidéoprojecteur sans transcendance), autodérision du dispositif dans le miroir. Consentement, microcopy d'action et gestes-sources laissés littéraux (dosage §5, limites §6 de la charte).
- **« Une drôle d'époque » implémenté v1.0 (2026-07-17)** : le bloc 1 refondu remplace le flow Conseil du Seuil en production. `/une-drole-depoque` (ancienne URL redirigée) : 30 écrans simples (prologue ×2 + 7 jours × 4 + miroir), variantes É3/É4 rendues côté serveur selon la polarité choisie, gestes-sources révélés en É3, jour 7 = profil Transcendance (2 gestes familiers + 1 difficile). Contenu : `config/une_drole_depoque.yml` v1.0 (script intégral de [bloc-1-une-drole-depoque.md](../pedagogie/bloc-1-une-drole-depoque.md)). Nouveau dans le miroir : la **Posture Point Zéro** (catalogue des 24 en paires enracinée/passante, dérivation déterministe dominante × polarité × rapport au mouvement inverse, teinte Transcendance, 2 postures voisines, note « position sur une carte, pas une case d'identité »). Les passations `conseil_du_seuil` restent lisibles (miroir avec panneau « dispositif précédent » + invitation à retraverser). L'Appel (A1-A5) est retiré du flow — données et mécanique prêtes pour le bloc 4. `MoteurAssessment` : kind `une_drole_depoque`, scoring §15 inchangé.
- **Profil connecté à l'évaluation (2026-07-17)** : les 6 puissances du Profil passent des échelles linéaires Oméga aux **mini-lemniscates** (partial `users/_puissances.html.haml`) : lobe violet = polarité et amplitude déclarées au premier miroir (l'autre polarité reste graine/inconnue), or = Oméga gagnés par puissance (`power_breakdown`), zone cap en placeholder (« Définir un cap » — attendra le Conseil Oméga). Transcendance = note sous la carte (résultante = grand lemniscate). Correctif : en É3 du dimanche, les deux gestes familiers choisis sont retirés des options du geste difficile (vue + validation serveur).
- **Profil : états activé / non activé + boucle Marelle (2026-07-17)** : le Moteur et les 6 puissances ont deux états. **Non activé** (aucune passation) : lemniscate graine + message « Cette brique de ton Profil est encore en sommeil : ton Moteur s'active en réalisant l'expérience n°X — “Une drôle d'époque” — du parcours du Monde 0 » avec bouton vers le parcours (numéro et lien calculés dynamiquement depuis la Marelle) ; puissances en graine avec note. Prévisualisation : `/users/me?apercu=inactif`. **Activé** : lemniscate + Posture Point Zéro rappelée sous le Moteur + 6 mini-lemniscates avec points d'or en circulation (durées décalées) et graine proportionnelle à l'horizon (plus de débordement). **Boucle complète avec la Marelle** : terminer la traversée valide automatiquement l'expérience n°3 du parcours Monde 0 (challenge 238, `validate_marelle_experience!`, Ω attribués par le mécanisme normal) ; le contenu de l'expérience a été aligné sur la traversée réelle (lien direct, mention « déjà faite = comptée automatiquement »).
- **Reste (v0.2+)** : illustrations des scènes (en production côté Boris), micro-récits adaptatifs post-restitution, recommandations réelles branchées sur le catalogue Monde 1, expérience dédiée dans le parcours du Monde 0 (skip si déjà réalisé), admin d'édition des contenus, sauvegarde fine intra-scène.

### F15 — « Avant le Zéro » (bloc 2 du triptyque, LDVELH) ✅ IMPLÉMENTÉ v1.0 (2026-07-17)

<!-- Ajout Claude, 2026-07-17 -->

- **Front** : `/avant-le-zero` (layout conseil, même DA que le bloc 1). Sablier narratif 2026-2033 : acte I commun (A1-A10), **Dispersion** (8 portes + le bord), 8 voies × 13 écrans (descente ×5, goulot ×3 dont **écran muet** G2, choix majeur, remontée ×2, 2 fins), 17 fins. Règle « une page = une interaction » partout sauf les huit G2 (bouton « … » unique). `/avant-le-zero/carte` : la **carte des devenirs** (17 cristallisations révélées ou en silhouette « ??? », compteur de traversées, ligne Conseil Oméga 2040).
- **Back** : modèle `Traversee` (table `traversees` : user, status, current_section, answers jsonb, fin_id) — traversées **historisées** : rejouer crée une nouvelle ligne repartant de la Dispersion avec les réponses d'acte I copiées, pour que les **échos différés** continuent de fonctionner (A1 → panneau du verger au G-T2 ; A3/A9 → variantes dans les huit G2 ; A7 → teinte en F3/S3/T3). Contenu : `config/avant_le_zero/*.yml` (un fichier acte I + un par voie, fusionnés au chargement — 117 sections, graphe validé). **Aucun scoring** (garde-fou acté) : seules traces = voies parcourues, fins atteintes, nombre de traversées.
- **Boucle Marelle** : atteindre sa première fin valide automatiquement l'expérience n°2 du Monde 0 (challenge 237 « Avant le Zéro », même mécanisme `validate_marelle_experience!` que le bloc 1) ; contenu du challenge réécrit (présentation + lien direct + mention validation auto).
- **Reste** : illustrations (21 images, liste et prompts pour Codex dans [bloc-2-illustrations.md](../pedagogie/bloc-2-illustrations.md) — champ `image` déjà supporté par toutes les vues), Graine de Récit optionnelle aux fins, exposition des devenirs rencontrés sur le Profil, bloc 3 (Conseil Oméga 2040).

### F16 — « Le Conseil Oméga » (bloc 3 du triptyque, 2040) ✅ IMPLÉMENTÉ v1.0 (2026-07-17)

<!-- Ajout Claude, 2026-07-17. Conception : ../pedagogie/bloc-3-conseil-omega.md -->

- **Front** : `/conseil-omega` (layout conseil). 34 écrans, charnière Purification → Conjonction (« qu'est-ce qu'on épouse ? »). Ellipse 2033→2040 · convocation (résolution du signal du bloc 2) · seuil (salle Simone-Veil, Nadia) · tour des absents · treizième siège (= le mental, évocation indirecte du Diviseur) · **6 séances = 6 puissances** (chaque : dossier de Conjonction → délibération avec invocation d'un devenir → vote + cap) · rite de clôture (posture-cible parmi 3 suggérées, Ombre/Lumière, fonction, engagement texte libre) · restitution du Monde 0 · **retour métaleptique en 2026** (le registre porte la date réelle du joueur ; le Greffier se révèle = **Docteur Z.E.R.O.**).
- **Back** : modèle `ConseilSession` (passation historisée, même philosophie que `Traversee`) — `answers` jsonb (votes + caps), `posture_cible`, `engagement`, `completed_at`. **Le joueur tranche les 6 dossiers** (le vote est l'expérience, le cap est la trace). Invocations des devenirs via `Traversee.fins_for(user)` (variantes indexées par devenir, sinon silhouette « quelqu'un, quelque part… ») ; Posture de Seuil via `MoteurAssessment`. **Posture-cible** : 3 suggestions sur 9, score = puissances où le cap est « assumer/circuler » + affinité avec les devenirs atteints ; le joueur en choisit une. Contenu : `config/conseil_omega/conseil.yml` (34 sections + 9 postures), moteur de sections du bloc 2 réutilisé + écrans `posture`/`engagement`/`restitution`/`verrou`.
- **Prérequis** : au moins un devenir complété au bloc 2 (sinon écran de verrou tenu par Nadia + lien `/avant-le-zero`).
- **Parcours (Journey 14)** : restructuré (voir [bloc-3-conseil-omega.md §7bis](../pedagogie/bloc-3-conseil-omega.md)). **Chapitre 1** = traversée intérieure (Entrer dans le Jeu → Une drôle d'époque → Avant le Zéro → Et moi dans tout ça ?), **Chapitre 2** = écosystème, **Chapitre 3** = engagement (**Le Conseil Oméga** [nouveau challenge 254, en tête] → Découvrir les formats → … → Mon récit de passage). Ordre bloc 1/bloc 2 rétabli (238 puis 237). Le Conseil ouvre le Ch3 comme sas métaleptique vers l'atelier réel.
- **Validation & Profil** : validation auto du challenge 254 à la clôture (mécanisme `validate_marelle_experience!`). Pas de Graine de Récit sur le bloc 3 (portée par « Mon récit de passage », fin du Ch3). Illustration de la carte = *Un groupe qui forme un cercle* (Ressources), en attendant la série papier découpé.
- **Caps du Moteur sur le Profil (2026-07-17)** : les 6 caps posés au Conseil remontent dans les mini-lemniscates. **Affichage en pointillés = axes d'amélioration** (arbitrages Boris) : trait plein violet = état évalué (où tu es), **pointillé = axe d'amélioration** (marge de progression vers une polarité). **Règle : le pointillé n'apparaît que là où il reste de la marge** — jamais sur une polarité déjà pleine (amp ≥ ~3 / « L3 ») : dans ce cas, « ✓ Acquis » et aucun pointillé (lève la contradiction « amélioration affichée sur un axe maxé »). **1 ou 2 axes** : `assumer`→Lumière et `accueillir`→Ombre donnent 1 axe (ou 0 si maxé) ; `circuler`→jusqu'à 2 axes (les deux polarités avec marge ; 1 seule si l'autre est pleine). **Niveau du cap = état actuel + 1** (arbitrage Boris) : le pointillé vise le prochain palier de la polarité (pas toujours L3), plafonné à L3 ; une polarité non explorée vise L1 (premier pas). Produit des caps à niveaux variés (L1/L2/L3) selon l'état — le cap est un *prochain pas* réaliste, pas le sommet absolu. Cas notable : circulation sur un pôle déjà maxé → premier pas L1 sur le pôle négligé (restaurer la circulation). Pointillé **violet des deux côtés** ; libellé = direction de progression (Vers la Lumière ↗ / Vers l'Ombre ↘ / Circulation ∞ / Acquis ✓). Marge par côté : polarité spontanée = `declared_amplitude` du bloc 1 ; polarité opposée = considérée comme non explorée (marge pleine). **Géométrie (arbitrage Boris) : le lemniscate gris = horizon infini.** L'amplitude L0→L3 se cale sur `mls` (134) strictement inférieur à `ml` (160 = gris), donc **même le niveau 3 (état ou cap) vit à l'intérieur du gris**, avec une marge — il ne recouvre jamais le contenant. Lecture en anneaux emboîtés : état plein (violet) → cap/axe d'amélioration (violet pointillé, hauteur L3) → horizon infini (gris). Colonne `users.moteur_caps` (jsonb, ajoutée à `always_loaded_attributes`) ; `User#effective_moteur_caps` = caps de la dernière `ConseilSession` complétée **surchargés par les ajustements manuels** ; panneau repliable « Ajuster mes caps » (6 selects) → `MoteurCapsController#update` (isolé, `update_columns` pour ne pas déclencher mathieu_core), route `patch /moteur-caps`. Sans Conseil : placeholder « Définir au Conseil → ». **Liens de rejeu des 3 blocs** sur le Profil (conditionnels), faits.
- **Reste (v1.1+)** : afficher « De [Posture de Seuil] vers [posture-cible] » sous le Moteur ; 12 illustrations Codex ([bloc-3-illustrations.md](../pedagogie/bloc-3-illustrations.md)) ; **bloc 4 (l'Appel) à l'entrée du Monde 1** (décidé — la clôture du bloc 3 laisse la « porte suspendue » que le bloc 4 rouvrira).
- **Décision ultérieure — 2026-07-31** : la `posture-cible` de la V1 est conservée comme donnée
  historique, mais la prochaine évolution du rite de clôture produit un **Rôle d'appel** et un
  premier geste d'exploration. Ne pas implémenter la ligne `Reste (v1.1+)` ci-dessus sans appliquer
  la migration et l'analyse d'impact de
  [Rôles d'appel et fonctions civilisationnelles](../pedagogie/roles-appel-fonctions-civilisationnelles.md).

### F17 — Fiche puissance + questionnaire dédié (Monde 1) ✅ PILOTE Désir v0.1 (2026-07-18)

<!-- Ajout Claude, 2026-07-18. Modèle validé avec Boris ; contenu = corpus-point-zero/03_archetypes + 11_evaluation. -->

- **Modèle** : chaque puissance a **une position** (niveau Ombre 1-3 × niveau Lumière 1-3) **× un état** de circulation (bloqué / intermédiaire / libre) — soit la grille des **27 archétypes** de l'atlas (`corpus-point-zero/03_archetypes/*.md`). L'état est une qualité unique sur les deux pôles (pas un état par pôle).
- **Questionnaire dédié par puissance** (arbitrage Boris) : précise position + état, et **surdétermine blocs 1 & 3** (priorité au questionnaire pour la posture si le joueur rejoue les jeux). Modèle `PuissanceAssessment` (user, puissance, o_level, l_level, etat, answers). Garde-fou canon : « libre » requalifié « intermédiaire » si un mobile de peur pilote encore.
- **Fiche** `/puissances/:slug` (layout conseil) : les 3 verbes (Ombre/Source/Lumière) → **état actuel** (label bloqué/intermédiaire/libre + phrase + niveau O-L + archétype actuel + lemniscate dont le point d'or circule selon l'état) → **cap d'évolution**. Cliquable depuis les mini-lemniscates du Profil.
- **Cap contraint** (arbitrage Boris, cohérent avec le « +1 » des caps du Profil) : bloqué→intermédiaire→libre (même position, on ouvre la circulation d'abord), puis élargissement d'amplitude n→n+1 (jamais n+2, jamais bloqué→libre). O3-L3 libre = sommet (« Le Vivant total »).
- **Placement** : expériences du parcours d'entrée Monde 1 (les 7 parcours fondamentaux, boucle Conscientiser→Nommer→Mettre en mouvement→Transférer→Intégrer, cf. `Intro Monde 1.txt`). Validation de l'expérience = au moins un questionnaire fait (listener) — **à câbler**.
- **Pilote livré** : Désir (`config/puissances/desir.yml`, 27 archétypes + questionnaire 4 questions). Vérifié : O1-L3 bloqué = « Le Feu qui refuse la nuit » → cap Intermédiaire « Le Porte-Flamme en initiation ».
- **Reste** : généraliser aux 5 autres puissances (contenu atlas prêt) ; **illustrations d'archétypes** (Codex ; fallback = illustrations rondes par pôle) ; polir les croyances depuis `Evaluation-Puissances.pptx` ; propager la surdétermination sur la posture/les caps du Profil ; créer l'expérience Monde 1 + listener de validation.

### F18 — Carte-couverture d'expérience et horizon Freeride

<!-- Ajout Codex - 2026-07-25. Principe validé par Boris. La carte-couverture relève de l'amélioration actuelle ; le deck Freeride reste un lot ultérieur à cadrer séparément. -->

Documents canoniques :

- [Cartes-couvertures d'expérience et mode Freeride](cartes-experiences-freeride.md) pour la fiche
  d'expérience et l'horizon du deck ;
- [Page parcours — la carte du voyage](page-parcours-carte-du-voyage.md) pour la vue ordonnée d'un
  parcours.

#### Lot actuel — fiche et composants

| Aspect | Impact |
|---|---|
| Front fiche | Remplacer le bandeau à médaillon par une carte-couverture mobile-first : scène d'image, titre, accroche, format, durée, Oméga, statut contextuel et action principale |
| Vidéo-first | Pour une expérience portée par une vidéo, transformer la couverture en affiche vidéo ; lecture immersive sur la même URL, reprise mémorisable, synthèse/transcription accessibles et sortie directe vers l'action suivante |
| Responsive | Mobile plein écran utile ; affiche horizontale à largeur maximale sur grand écran ; image entière par défaut sur fond dérivé, mode plein cadre facultatif |
| Détails | Conserver une URL canonique ; placer description, validation, Puissances, conditions et ressources sous l'ancre `#details` |
| Page parcours | Décliner une version compacte du même composant sans supprimer chapitres, ordre ni progression |
| Navigation | Actions et `Précédent` / `Suivant` dépendent du contexte d'ouverture ; ne pas coder la fiche comme exclusivement linéaire |
| Orientation | Remonter `Précédente / Voir le déroulé / Suivante` sous la couverture ; ne pas pointer vers les anciennes Pages de chapitre ; remplacer la navigation basse dupliquée par une carte de prochaine étape |
| Statuts | Distinguer obligatoire, optionnelle, alternative, libre, recommandée et verrouillée ; obligatoire/optionnelle reste porté par `ChallengesJourney` |
| Prochaine action | Le CTA décrit l'action concrète disponible (`Regarder`, `Discuter`, `Reprendre`, `Produire ma Graine`, `Envoyer au facilitateur`) et peut afficher `Étape n sur n` sans confondre progression et validation |
| Média principal | Une vidéo, un jeu ou une pratique indispensable apparaît avant la complétion et n'est pas classé comme ressource complémentaire |
| Puissances | Cartes lisibles : Puissance, aspect, axe Ombre/Point Zéro/Lumière, versant travaillé et Oméga par association ; aucune chaîne framework brute ni lecture comme évaluation du joueur |
| Cohérence données | Vérifier compétence et `derived_framework` ; anomalie relevée : `Intuition : Conviction` associée à `Communication - Lumière` sur `L'écosystème Point Zéro` |
| Libellés | `n Ω à gagner` ou `n Ω gagnés`, intensité nommée, autorité déclarative formulée en langage joueur ; retirer `Validation Autonome` de la couverture |
| Contrat d'achèvement | Séparer parcours d'action, preuve de traversée, autorité de validation et attribution des Oméga ; autorités déclarative, système ou facilitateur |
| Trajectoire technique | V1 configurable par expérience avec validation existante ; puis résolveur de présentation fondé sur les traces métier ; aucun moteur générique de workflow dans le lot actuel |
| Backoffice | Préparer une accroche courte et des métadonnées éditoriales ; vérifier les champs existants avant toute migration |
| Accessibilité | Un seul CTA principal, boutons équivalents aux gestes futurs, aucun texte essentiel incrusté dans l'image, respect du clavier et des lecteurs d'écran |

Une IA peut accompagner une production, mais ne valide pas automatiquement sa qualité ni un niveau de conscience. Pour une Graine de Récit, le système peut reconnaître l'existence de la trace ; une éventuelle appréciation qualitative reste humaine et proportionnée à l'enjeu.

Avant toute évolution du moteur de validation, produire une analyse d'impact sur `Challenge`, `ChallengesUser`, la progression linéaire, les expériences optionnelles, l'idempotence de l'attribution des Oméga, les callbacks de `mathieu_core` et la compatibilité des traversées déjà commencées.

#### Sous-lot validé — page parcours

<!-- Ajout Codex - 2026-07-25. Décision Boris après audit de la page Monde 0 déployée. -->

| Aspect | Impact |
|---|---|
| Rôle | La page devient la carte verticale du voyage ; elle ne devient ni catalogue ni deck |
| Premier écran | Promesse courte, progression narrative, prochaine expérience accessible et CTA unique avant la description longue |
| Chapitres | Afficher mouvements, fil rouge, état et progression ; chapitre actuel ouvert, accomplis et futurs repliables |
| Cartes | Réutiliser la carte-couverture compacte ; retirer la répétition du mode de validation ; nommer les états |
| Progression | Séparer étapes requises accomplies et Oméga gagnés/disponibles ; éviter le pourcentage composite |
| Optionnel | Montrer `Détour facultatif` et `Passée pour l'instant` ; permettre la reprise sans fausse validation |
| Rite | Sortir l'Atelier de la liste ordinaire et le présenter comme seuil requis vers le Monde 1 ; Sas facultatif |
| Puissances | Déplacer la ventilation détaillée sous une restitution secondaire repliable |
| Responsive | Aucun débordement horizontal ; CTA au-dessus de la navigation basse ; états et titres lisibles à 320–390 px |
| Accessibilité | `h1` parcours, `h2` chapitres, `h3` expériences ; accordéons clavier ; états textuels et contrastes suffisants |
| Modèle | Réutiliser l'ordre, les validations, `progression_mode`, `ChallengesJourney.required`, les sauts et les totaux existants avant toute migration |
| Calcul | Centraliser un résolveur de présentation pour prochaine étape, reprise, comptes requis, Oméga accessibles et rite ; ne pas recopier les règles dans HAML |

Le premier lot est principalement front et présentation. Toute modification de la sémantique
d'accomplissement, de la formule d'Oméga ou des modèles centraux reste soumise à une analyse
d'impact séparée.

#### Horizon — Freeride à partir du Monde 2

| Aspect | Impact |
|---|---|
| UX | Main de trois cartes `Élan / Circulation / Ouverture`, pas de flux infini |
| Geste | Droite = choisir ; gauche = pas maintenant ; toucher = détails ; boutons visibles équivalents |
| Trajectoire | Une expérience active, deux en réserve, expériences programmées et prochain rite visibles dans `Ma ligne de jeu` |
| Recommandation | `Pourquoi maintenant ?`, raisons, confiance, alternatives et correction des sources par le joueur |
| Profil | Un swipe ou un refus ne modifie jamais le Moteur ; signal contextuel de faible confiance et durée limitée |
| Sécurité | Prérequis, intensité, Cercle, facilitateur et protocoles d'arrêt filtrent les cartes avant tout classement |
| Oméga | Aucun gain pour choisir ou swiper ; gain sur accomplissement réel ; le Freeride ne remplace aucun rite |
| Données futures | Distinguer expérience réutilisable, main/recommandation, ligne de jeu et occurrence vécue ; aucun nouveau modèle n'est décidé dans ce cadrage |

#### À ne pas lancer dans le lot actuel

- gestes de swipe ;
- pile ou persistance de cartes ;
- moteur de recommandation adaptatif ;
- apprentissage à partir des refus ;
- génération d'expériences par IA ;
- refonte spéculative du modèle de données.

### F19 — Guides LLM transversaux du Point Zéro

**Origine front** : prolonger dans l'application le choix entre le Professeur Sirbey et
le Docteur Z.E.R.O. Le guide répond aux questions sur le Point Zéro, la page courante et
les fonctionnalités, depuis une pastille persistante de la coque.

| Aspect | Impact |
|---|---|
| Front | Pastille non bloquante en bas à droite, dialogue refermable, choix de la voix, suggestions liées au contexte et accès clavier/mobile ; la fonction ne devient pas une rubrique de navigation supplémentaire |
| Autorité | Les deux voix utilisent le même corpus, les mêmes sources, les mêmes outils et les mêmes permissions ; seule la formulation change |
| Contexte | Enveloppe minimale fournie par la coque : Monde, droits ouverts, destination, panneau et rôle actif ; aucune déduction à partir d'une page simplement annoncée |
| Données | Aucune lecture par défaut des Graines, du profil détaillé du Moteur, des conversations privées ou de la mémoire du mentor ; toute extension exige un consentement explicite, finalisé et révocable |
| IA | Recherche augmentée sur le corpus PZ avec références consultables, degré d'incertitude, mécanisme de correction/signalement et protection contre les instructions contenues dans les documents indexés |
| Mémoire | Première version éphémère ou locale ; aucune mémoire personnelle implicite. Une continuité ultérieure doit être visible, éditable et désactivable par le joueur |
| Sécurité | Le guide ne diagnostique pas, n'évalue pas une Puissance et ne remplace ni le mentor, ni le facilitateur, ni l'Aide. Il redirige explicitement hors de son périmètre |
| Backoffice | Version du corpus et des instructions, sources autorisées, journal technique sans contenu intime, suivi des réponses signalées, coûts et limites d'usage |
| Déploiement | Prototype front réalisé ; aucun appel LLM réel ni modèle Rails décidé à ce stade. Une analyse d'impact dédiée est requise avant intégration |

**Analyse d'impact rendue le 12 août 2026** —
[analyse-impact-guides-llm.md](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/analyse-impact-guides-llm.md).
Elle remplit l'exigence ci-dessus. Cinq conclusions à retenir ici :

1. **Le chemin critique est éditorial, pas technique.** Le corpus joueur n'existe pas :
   `docs/vision/` est de la documentation interne (arbitrages, plans, Mondes non ouverts) et
   l'indexer contredirait le dévoilement progressif. Le corpus curaté tiendra en revanche
   entièrement dans le prompt — aucune base vectorielle n'est nécessaire (et `pgvector`
   n'est pas disponible sur notre Postgres).
2. **La pastille suppose un JavaScript que l'application n'a pas** (32 lignes en tout dans
   la coque). Recommandation : livrer d'abord une page « Demander au guide » sans JS, la
   pastille ensuite.
3. **Le Docteur Z.E.R.O. est le risque humain principal.** L'humour caustique généré en
   direct, sur un public non trié, dans un jeu qui travaille l'Ombre, est le registre qui
   échoue le plus mal. Recommandation : ouvrir avec le Professeur seul.
4. **Le coût n'est pas une contrainte** (~9 $ pour une journée de Festival sur Sonnet 5) —
   il ne doit donc pas justifier un modèle moins capable. Un plafond de dépense reste requis.
5. **Le rempart contre l'injection de prompt, ce sont les pouvoirs, pas les mots** : tant
   que le guide n'a aucun outil, une injection réussie ne peut que faire dire une bêtise.
   L'analyse est à refaire entièrement le jour où on lui donne une capacité d'action.

Invariant confirmé par l'analyse : **l'Aide et les recours humains ne passent jamais par le
modèle** — `/aide` est statique et doit le rester.

La conversation du guide ne produit ni Graine, ni validation, ni Oméga. Si un échange
fait émerger un travail personnel, le guide propose d'ouvrir le mentor ou l'expérience
pertinente et laisse le joueur décider du transfert de contexte.

**Effacement sur les surfaces sensibles** (ajout Claude, 2026-08-11). La pastille est
persistante, mais pas universelle : elle **disparaît** — et ne se contente pas de changer de
ton — sur l'Aide et les situations sensibles, le signalement, la médiation, le blocage, la
contestation d'une évaluation et tout écran de vulnérabilité. Motif : la maquette
`aide-situations-sensibles-cible` pose que « l'humour du Jeu est absent des écrans de
sécurité et de vulnérabilité », et la voix du Docteur Z.E.R.O. y serait blessante quel que
soit le soin de sa formulation. Un guide qui se tait est préférable à un guide qui
s'excuse. Corollaire déjà écrit dans la maquette, à tenir : l'Aide et les recours restent
atteignables **sans** passer par le guide.

### F20 — Rencontre (`Meeting`) : l'objet de rendez-vous généralisé

**Origine front** : `agenda-vivant-cible` — journée unifiée, propositions de créneaux, cycle
`proposée → disponibilités recueillies → confirmée → passée / annulée`.

**État réel** : une V1 existe déjà, mais **restreinte à un seul contexte** —
`PropositionDeRencontre` ne vit que sur les mises en relation de Cercle
(`circle_membership`), avec les états `proposee / retenue / declinee / retiree`.

| Aspect | Impact |
|---|---|
| Modèle | Généraliser vers un contexte **polymorphe** (espace, candidature, projet, mission, événement) plutôt que créer un second objet concurrent ; conserver la sobriété acquise : créneaux en toutes lettres, pas d'agenda synchronisé |
| Droits | Le droit de proposer et de répondre suit le contexte porteur, jamais un rôle global — réutiliser `ContexteDeFil` plutôt qu'une nouvelle table d'autorisations |
| États | Ajouter `disponibilités recueillies` entre `proposée` et `confirmée` (la V1 saute cette étape) ; l'annulation et les changements de participants restent historisés |
| Front | Une carte structurée (grammaire `Carte`, F-B2) dans le fil + une vue agenda transversale ; la présence réelle reste distincte de l'inscription |
| Backoffice | Aucun besoin nouveau : un rendez-vous n'est pas un événement de billetterie et ne doit pas encombrer la console Festival |
| Piège | Ne jamais remplir automatiquement une plage libre ; une disponibilité n'est pas un engagement |

**Réalisé le 12 août 2026** (`pointzero-app`, prod `8624117`). Le contexte est devenu
polymorphe — `ContexteDeFil` gouverne qui participe et qui agit, aucune table
d'autorisations nouvelle — et l'état `disponibilites` s'intercale entre `proposee` et
`retenue`. Le piège est tenu par une règle explicite, vérifiée au banc : **même lorsque
tous les participants se disent libres au même créneau, rien ne se retient** — il faut
encore un geste, et il appartient à l'autre que le proposeur. La rencontre se propose
depuis tout fil vivant à plusieurs (espace, candidature) ; un fil à un seul participant
n'en offre pas. **Reste pour l'UI agenda transversale** (desktop) : la vue qui
rassemblera les rendez-vous de tous les fils — le modèle est prêt et son contrat est
`PropositionDeRencontre.pour_contexte` / `#participants`.

### F21 — Source d'attention unique (`ActivityItem`)

**Origine front** : `centre-activite-cible`, plus les trois inboxes concurrentes relevées en
revue (accueil, Centre d'activité, accueil des Échanges).

**État réel** : les **engagements** de l'accueil des Échanges (lot S1-A4) sont déjà une
projection de cette source — mentions non lues, rencontres et contacts à répondre,
candidatures à décider, invitations, revues échues — mais calculés à la volée, sans objet
transversal.

| Aspect | Impact |
|---|---|
| Modèle | Un `ActivityItem` (ou une projection équivalente) **référence** l'objet métier, ne le remplace pas et ne duplique pas son contenu |
| États | `vu` doit rester distinct de `traité`, `refusé`, `expiré`, `annulé` — voir une notification ne vaut jamais traitement |
| Droits | Le centre **réutilise** les autorisations du contexte source ; aucune ligne ne doit être lisible hors des droits de l'objet qu'elle pointe |
| Front | Trois projections d'une seule source : accueil (sélection courte, nommée et non comptée), Centre (archive complète et auditable), Échanges (part conversationnelle) |
| Notifications | Préférences portées par l'**appartenance** (`EspaceMembership`), pas par le gabarit ; digest et plages de repos |
| Piège | Pas de défilement infini, pas de série, pas de relance artificielle ; différer ne modifie jamais une échéance collective |

**Réalisé le 12 août 2026** (`pointzero-app`, prod `51c7eb0`) — avec un **arbitrage de
Boris qui amende la ligne « Modèle »** : il n'y a **pas de journal d'événements**. Les
objets métier SONT l'archive (ils portent déjà leurs dates et leurs états) ; persister une
seconde fois créerait une vérité à resynchroniser, ce que la doctrine du corpus refuse
partout ailleurs (`SeuilFranchi`, `BadgeDeParcours`, `BoiteDEchanges` : « un état se lit,
il ne se stocke pas »). `Engagements` est donc la source unique, avec deux lectures : le
présent (borné, pour l'accueil) et `archive` (sans fenêtre, le traité compris). La seule
persistance est **`vu`** (`marqueurs_d_attention`), parce qu'il ne se déduit d'aucun objet
— et il ne vaut jamais traitement.

**Conséquence pour la spec P/D/A §10** (contrat d'événements) : les événements y restent
la bonne façon de NOMMER ce qui se passe, mais aucune table ne les enregistre — ce sont
les transitions d'état des objets qui en tiennent lieu. À prendre en compte si un besoin
d'audit externe apparaît un jour (il justifierait alors son propre lot, et sa propre
décision).

### F22 — Proposition, Décision et objection

> **Arbitrage du 29 août 2026 :** ces distinctions restent pertinentes pour l'audit et
> l'historique, mais ne constituent plus quatre entrées UX. Elles sont projetées dans le
> cycle unique du **Mouvement** : `à éclaircir → à consentir → en mouvement → accompli`.
> Voir [Messagerie M1 — mettre une intention en mouvement](messagerie-mouvement-collectif-m1.md).

**Origine front** : `messagerie-point-zero-cible` — vues Décisions, composeur `+`, objection
en trois temps.

**État réel** : l'**objection est construite** (lot S1-B1) comme réaction sémantique
précisable (ce qu'elle protège / le risque / la condition de levée) ; les **cartes** et leur
contrat sont construits (S1-B2) ; les **sondages** existent (S1-A8) et préfigurent le vote.

✅ **Préalable levé le 2026-08-11** : R11 retient l'intention au niveau du fil ou du
sous-fil, affichée par un bouton compact à côté du titre. Une Proposition s'accroche donc
au fil qui la porte ; un message ordinaire ne porte pas d'intention autonome. La
spécification Proposition/Décision/Action peut commencer.

| Aspect | Impact |
|---|---|
| Modèle | `Proposition` portée par un fil, avec états `brouillon → exploration → décision → adoptée / retirée / à retravailler` ; la `Décision` conserve protocole, participants, objections, résultat et historique (critère cible §22.5) |
| Migration | L'objection B1 **migre** vers la Proposition/Décision — elle ne coexiste pas en double registre |
| Droits | Proposer, objecter et clore sont trois droits distincts ; aucun ne découle d'un rôle global |
| Front | Réutiliser la grammaire `Carte` ; une objection reste un objet lié, jamais un emoji négatif |
| Piège | Un message ne change jamais un statut (invariant V1) ; le protocole de décision est explicite avant le vote, pas déduit après |

### F23 — Action / mission portée dans un espace

> **Arbitrage du 29 août 2026 :** l'Action ordinaire n'est plus créée comme un objet visible
> séparé. Elle est la phase `En mouvement` du Mouvement. Une Mission du Commun demeure un
> objet plus large et ne doit pas être fusionnée par analogie sans analyse dédiée.

**Origine front** : vue `Actions` de la messagerie-cible, `missions-commun-cible`,
`projet-vivant-cible`.

| Aspect | Impact |
|---|---|
| Modèle | `Action` avec porteur, échéance facultative, états `proposée → prise → en cours → achevée / abandonnée` ; distinguer le **besoin borné** (contribution ponctuelle) de la **mission du Commun** (œuvre collective) — la Place de marché est la porte unique (arbitrage Boris, R3) |
| Droits | Se porter volontaire est un acte de la personne : **aucune affectation** par le système ni par un tiers |
| Reconnaissance | Une action achevée n'attribue **aucun** Oméga automatiquement — elle alimente le dossier du rituel de reconnaissance (F-horizon) |
| Front | Carte structurée + vue Mouvements par espace ; l'intention et le besoin s'affichent avant toute récompense estimée |
| Piège | Une candidature ouvre un échange, elle n'attribue pas une place |

### F24 — Mémoire d'espace (du Fil à la Mémoire)

**Origine front** : vue `Mémoire` de la messagerie-cible, cible §9.

| Aspect | Impact |
|---|---|
| Modèle | Élévation **explicite** d'un message ou d'un objet en trace conservée : qui propose, qui confirme, quel contexte d'origine |
| Consentement | Une Graine ou une conversation privée ne change jamais de contexte sans consentement (critère §22.6) ; la trace conserve auteur, contexte, lecteurs et consentements (§15.2) |
| Droits | Lire la Mémoire suit les droits de l'espace ; une élévation ne peut pas élargir l'audience d'origine sans acte explicite |
| Front | Réutiliser `Carte` ; l'export d'espace (lot S1-A10) doit inclure la Mémoire |
| Piège | Ne pas confondre archivage (l'espace se clôt) et élévation (une trace est jugée durable) |

### F25 — Objets d'horizon : à spécifier avant toute ligne d'analyse complète

Les maquettes introduisent d'autres objets dont la **spec métier n'existe pas encore**.
Écrire leur ligne d'impact maintenant produirait une analyse fictive ; les nommer avec leur
préalable bloquant est plus utile. Aucun ne passe en implémentation sans franchir ce
préalable **et** recevoir sa propre ligne F.

| Objet | Maquette | Préalable bloquant |
|---|---|---|
| Habilitation, mandat, métier PZ | `academie-facilitateurs`, `facilitateur-cockpit` | critères de qualification, garant, durée, veille (politique de formation) |
| Domaine de souveraineté | `souverainetes-projets` | définition des niveaux qualitatifs et de leur constat |
| Œuvre, version, filiation, clé de circulation | `studio-filiation` | droits d'auteur, assiette comptable, fiscalité |
| Besoin, offre, devis, contrat | `place-marche` | **frontières juridiques** marketplace / prestation / don ; TVA ; responsabilités |
| Consultation du Commun | `gouvernance-commun` | doctrine de pondération et gouvernance exacte des consultations |
| Contribution reconnue, enveloppe de reconnaissance | `reconnaissance-omega` | spec du rituel (canon 31/07 §11-15) |
| Espace sensible, médiation, recours | `aide-situations-sensibles`, `consentement-securite` | cadre de responsabilité et de récusation ; conservation |
| Indicateur d'alchimisation | `alchimisation-cible` | confrontation du calcul (échelles clarifiées le 2026-08-11, cf. [sept-puissances.md](sept-puissances.md)) |

### Décisions UX transverses (Boris, 2026-07-13)

- **Cercles progressifs** : l'entrée existe dès le Monde 0 comme teaser ; tout Cercle constitué au
  Monde 1 est déjà un Cercle de croissance autofacilité ; le Monde 2 introduit le facilitateur
  certifié, l'abonnement et le cycle annuel.
- **Vocabulaire : « Graine de Récit »** (et non « Grain ») — on sème une Graine, les résonances y germent.
- **Mondes 0-1 : mantra « JE DISCERNE »** (Boris, 2026-07-13) — le « JE SUIS » (Désir) est la puissance la plus profonde à toucher, pas la première affichée. Cohérent avec le gardien de l'Intuition (sept-puissances.md §4).
- **Marelle** : intro actée (« dispositif de transformation personnelle et collective en 10 mondes d'intensité progressive ») ; bloc Monde actuel collapsable, rouvert automatiquement à l'ouverture d'un nouveau monde, nourri par les fiches Mondes (Dropbox Point Zéro/img/Mondes) ; recherche libre titre+description ; filtres : thématique, durée, intensité, puissance, monde.
- **Fresque de Récit dans le profil** : Graines (titre + contenu) affichées en fresque, visibilité par la communauté choisie Graine par Graine.
- **Statut des concepts** : le prototype marque désormais décidé / à l'essai / exploratoire (cf. NOTES.md du proto) — les concepts exploratoires (Open Badges, trophées secrets, attestations, quêtes inter-cercles) ne passent pas en implémentation sans arbitrage.

## 2. Vue d'ensemble — dépendances entre chantiers

```text
F2 (libre/linéaire) ──┐
F3 (obligatoire)  ────┼── prérequis du Monde 0 jouable
F6 (Oméga)        ────┘
F5 (Récit/mentors) ── indépendant, gros chantier IA — peut suivre
F1 (News)          ── indépendant, petit — quick win
F7 (mode événement)── chemin critique Festival (1er octobre)
F9 (inscription)   ── chemin critique avant F7 — identité et billet
F4 + F10 (Marelle) ── modèle World et accès nécessaires à l'ouverture du Monde 1
F11 (Cercles)      ── dépend de F10 et des droits Monde 1/Monde 2
F12 (Ressourcerie) ── chantier indépendant, graphe réutilisable par les parcours
F13 (Profil)       ── dépend de F6, F10, validation et politique de credentials
```

Ordre suggéré : **F9** (inscription et billet, à éprouver en premier) → **F1 + F2 + F3** (socle Monde 0, petits chantiers backoffice) → **F7** (expériences du Festival) → **F4 + F10** (Marelle et Monde 1) → **F11** (Cercle progressif) → **F6 + F13** (Oméga et Profil, après arbitrage) → **F5** (Récit/IA). **F12** peut avancer en parallèle après validation du modèle de graphe.

## 3. Décisions transverses (Boris, 2026-07-12)

1. **Programme Festival révisé le 2026-07-24 : validation produit et autonomie avancent en parallèle.** `vibe.ze.game` reste le bac à sable où les parcours sont éprouvés, mais l'extraction vers l'application autonome commence avant la fin de toutes les itérations produit. Le précédent report de cette extraction après validation complète est remplacé par [le cadrage Festival](application-festival-2026.md). La branche `pointzero` reste une référence déployable ; une branche d'autonomie distincte portera le retrait progressif des gems privées.
2. **Implémentation démarrée dans vibe.ze.game (2026-07-14).** Layout Point Zéro en place (logo, chip Ω temps réel, nav Accueil/Marelle/Cercle/Ressources/Profil — Cercle et Ressources désactivés) + accueil orchestrateur V1 (états : seuil nouveau joueur avec news Festival / Monde 0 en cours avec prochaine Action, progression, lemniscate Ω). Particularités techniques : les assets de prod sont buildés hors serveur (Capistrano copy public/assets) → les ajouts PZ sont servis en statique depuis public/pz/ (CSS pur, fonts, logos) sans toucher à la chaîne de build. Versioning : git local dans ~/zegame/current (branche pointzero) — ATTENTION, un cap deploy de Mathieu écraserait le dossier : à coordonner avec lui.
3. **Bac à sable réinitialisé (2026-07-14).** vibe.ze.game est une instance sandbox séparée de la préprod — aucune précaution multi-clients nécessaire. Contenu réduit au seul parcours « Point Zéro - Monde 0 » (12 Actions, 13 inscrits). **11 communautés « Point Zéro - Monde N » créées (N = 0 à 10)** — ce qui tranche la question ouverte de la numérotation : 11 positions. Monde 0 = communauté default + joinable ; les membres d'une communauté Monde = les joueurs entrés dans ce Monde. Communauté « Cercle pédagogique PZ » conservée (facilitateurs). Tous les utilisateurs conservés. Sauvegarde : ~/backup-avant-reset-pz-*.sql sur le serveur.
3. **Charte graphique actée** : base violet identique à ze.game ; titres Roboto Slab, texte Poppins ; logos dans Dropbox/Vibe Coding/Ressources Point Zero/Logos (spirale PZ + Cosmo Coin infini). DA appliquée au proto (v3.0, étape 4 du workflow).
4. **Base de données séparée (confirmé le 2026-07-24).** La nouvelle appli Point Zéro ne partage pas la BDD de ze.game. Pour le Festival, le transfert est un import contrôlé et rejouable, sans synchronisation bidirectionnelle permanente. Nouveau compte sur les stores (Apple/Google) dédié au Point Zéro et mention « powered by ze.game » dans l'appli. Le **SSO** reste un chantier à cadrer et n'entre dans le chemin critique que s'il est confirmé indispensable.
5. **Une seule monnaie : l'Oméga (révisé 2026-07-13).** Le jeu en réalité alternée (monde-miroir) n'apparaît pas à ce stade du produit : toute mention au mana est éliminée de l'interface et des chantiers F1-F13. Les docs de vision monde-miroir restent un horizon non planifié.
6. **7 puissances : référentiel existant de l'app.** Les compétences actuelles au format « PUISSANCE : ASPECT » avec framework « Point Zéro - Puissance - Lumière/Ombre » servent de base — pas de nouvelle couche de données pour la V1. Approfondissement théorique dans [sept-puissances.md](sept-puissances.md).

## 4. Questions ouvertes restantes

1. Le SSO est-il indispensable au Festival ? Si oui : protocole, sens de la fédération (ze.game IdP ?) et rapprochement des comptes existants.
2. Compteurs temps réel du Festival : SSE existant ou solution dédiée ?
3. Quel sous-ensemble du Monde 0 actuel (comptes, contenus, progression) est importé dans la base séparée, et quels contrôles valident cette migration ?
4. Quel mécanisme WordPress porte le contexte du compte applicatif jusqu'au billet : métadonnée de commande, champ participant dédié ou jeton de rattachement créé après paiement ?
5. Quelle source fait foi pour les capacités : stock global de billets WordPress, réservations d'expériences dans l'appli, ou deux niveaux distincts ?
6. Combien d'événements payants par an justifieraient le remplacement de WooCommerce par une billetterie Stripe native ?

## Journal d'implémentation UX/vocabulaire (vibe.ze.game)

<!-- Ajout Claude, 2026-07-14 -->

- **Détail expérience** : Oméga reçus / total (challenge + parcours), chapitre en fil d'Ariane (au-dessus de la carte, fix collision mobile), section Validation en liste à puces simple (sans check ni marqueur), padding des flèches Précédent/Suivant sur mobile.
- **Vocabulaire** : « POINT » → « OMÉGA » (labels), montants inline = nombre + logo infini violet. « FEEDBACKS » → « Graine de Récit », affichée uniquement sur les expériences de **fin de chapitre** (calcul auto : dernière expérience avant le chapitre suivant / la fin) ; bouton de niveau parcours retiré.
- **À traiter (éditorial, contenu Boris)** : certaines expériences du Monde 0 ont un texte de validation qui dit « clique sur FEEDBACKS » — à réécrire pour le modèle Graine de Récit (le bouton n'existe plus que sur les fins de chapitre).

- **Validation autonome restaurée (2026-07-14)** : bouton « J'ai réalisé cette expérience » (mark_as_ended, hors LTI) sur les expériences non-fin-de-chapitre — corrige la régression du retrait de FEEDBACKS. Aux fins de chapitre : bouton de complétion + « Graine de Récit ».

- **Graine de Récit = prérequis de validation en fin de chapitre (2026-07-14)** : sur les expériences de fin de chapitre, le bouton « Graine de Récit » s'affiche AVANT « J'ai réalisé cette expérience » ; la complétion est verrouillée (bouton désactivé + message « Sème d'abord ta Graine de Récit pour valider ») tant qu'aucune Graine n'a été semée, avec une garde serveur (`ChallengesUsersController#mark_as_ended`) qui refuse la validation. **Rattachement Graine ↔ chapitre** : la Graine est un message du joueur dans le fil (`Messaging::Thread`) dont le container est la ChallengesUser de fin de chapitre — le lien Graine → expérience de fin de chapitre → chapitre accompli est donc porté par ce fil. Méthode réutilisable `Journey#chapter_end_challenge?`. V1 : « Graine présente » = au moins un message du joueur dans le fil ; le modèle explicite (StorySeed, conversation mentor IA) reste le chantier F5.

- **Personnalisation du contenu** : helper `personalize` remplace `[Prénom]` (toutes casses) par le prénom du joueur, appliqué au contenu des chapitres (Page) et des expériences (Challenge). Extensible à dautres variables.
- **Fix perte dimages TinyMCE (Firefox)** : les éditeurs inline (mode utilisé quand `document.moveBefore` absent, ex. Firefox) ne synchronisaient pas les images insérées vers le champ soumis. Corrigé par `public/pz/pz_forms.js` (statique, inclus dans les layouts) qui force la synchro à la soumission. Le chemin serveur préservait déjà les images.

### Correction (le vrai diagnostic)

Le fix images TinyMCE décrit plus haut (pz_forms.js, mode full) était une **mauvaise piste** et a été **reverté**. Vraie cause découverte grâce à un indice de Boris (limage disparaît seulement si on la redimensionne/aligne) : le modèle `Page` faisait `clean_html_tiny :content` **sans `extended: %i(img video)`**. La sanitization garde une image brute mais **retire une image portant un attribut `style`** (alignement float/marges). Correctif définitif : `clean_html_tiny :content, extended: %i(img video)` sur `Page` (comme `Challenge`). Le mode inline_unless_movebefore et le JS de synchro nont jamais été en cause — limage atteignait le serveur puis y était nettoyée.

- **Points par compétence (2026-07-14)** : le point ne vit plus sur l'expérience mais sur chaque association compétence↔expérience (colonne `challenges_skills.point`). Total expérience = somme des points par compétence (`Challenge#total_point`). Formulaire admin : lignes « compétence + ses points » (champs imbriqués) avec **total Oméga calculé en direct** (public/pz/pz_admin.js). Migration : chaque compétence a reçu le point de son expérience → totaux préservés à l'identique. Impacts couverts : gain_points (crédit par compétence), Journey#skill_details (SQL sum(challenges_skills.point)), score max LTI, affichages (détail expérience, parcours, catalogue), import/export JSON (skills = [{name, point}]).

- **Page Profil Point Zéro (2026-07-14)** : construite sur données réelles. (1) Oméga total + lemniscate animé Ombre/Point Zéro/Lumière. (2) Carte des 7 puissances : agrégation des Oméga par puissance et polarité lue depuis skills.derived_framework (`Puissance - Ombre|Source|Lumière`), marqueur positionné sur laxe selon léquilibre Ombre/Lumière (Émotion très Lumière, Communication très Ombre chez le compte test). Les 5 degrés du moteur (360°) restent à collecter → mentionnés comme à venir. (3) Mon Récit : fresque des Graines = messages du joueur dans les fils dexpériences (approximation V1 ; le vrai StorySeed via mentor IA reste F5). Méthodes User: omega, power_breakdown, power_position, recit_graines.
