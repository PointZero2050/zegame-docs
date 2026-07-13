# Analyse fonctionnelle — impacts back/front

<!-- Ajout Claude, 2026-07-12, sur demande de Boris (retours wireframe accueil v1) -->

Ce document est le registre d'analyse d'impact : chaque nouvelle page ou fonctionnalité front y est modélisée avec ses impacts sur le backoffice, les modèles de données et la cohérence d'ensemble. **Règle de travail : aucune page ne passe en implémentation sans sa ligne d'analyse ici.** Claude et Codex le tiennent à jour ; les arbitrages restent à Boris.

Contexte : ces impacts visent la **future application dédiée Point Zéro** (décision du 2026-07-12, cf. [accueil-point-zero.md](accueil-point-zero.md) §13). La question de ce qui est partagé avec ze.game (modèles, gems, base, comptes) reste ouverte.

## 1. Registre des impacts identifiés

### F1 — Module News

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

### F3 — Parcours obligatoire (tutoriel de Monde)

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

**Origine front** : remplace le feedback actuel. À la fin d'un parcours ou à des étapes-clés, le joueur fait le point avec un mentor IA (héros d'une bibliothèque de mentors) et produit un **Graine de Récit**. Les résonances des autres joueurs germent sur les Graines.

| Aspect | Impact |
|---|---|
| Modèle | `Mentor` (bibliothèque : nom, personnage, prompt/persona, visuel) ; `StorySeed` (auteur, parcours/étape source, contenu issu de la conversation, mentor, visibilité) ; résonances rattachées aux Graines (évolution de la messagerie actuelle ou nouvel objet) |
| Backoffice | Gestion de la bibliothèque de mentors ; configuration des déclencheurs (fin de parcours / étapes-clés d'un parcours long) |
| IA | Conversation mentor = intégration LLM (nouveau composant technique — API, coûts, modération) ; le joueur valide/corrige la Graine produit (garde-fou : l'IA n'impose jamais le sens, cf. [relations-recits-collectifs.md](relations-recits-collectifs.md) §2) |
| Existant | Un exemple de mentor existe dans le parcours Monde 0 actuel de vibe.ze.game — à documenter comme référence |
| Lien vision | Concrétise le "récit-fresque" ([relations-recits-collectifs.md](relations-recits-collectifs.md)) : Grain ≈ bloc narratif |

### F6 — Oméga (Cosmo Coin Oméga)

**Origine front** : indicateur de progression manquant. Monnaie de conscience = points des Actions + progression dans les 7 puissances. Représentation : lemniscate Lumière — Point Zéro — Ombre, animée selon l'amplitude.

| Aspect | Impact |
|---|---|
| Modèle | À articuler avec `Point` existant (points par compétence) : l'Oméga est-il la somme des points, ou un calcul distinct intégrant les 7 puissances ? Les 7 puissances doivent-elles devenir des données structurées (aujourd'hui : noms de compétences "PUISSANCE : ASPECT") ? |
| Front | Composant lemniscate réutilisable (chip compacte + carte détaillée) ; animation d'amplitude Ombre/Lumière à définir en fonction de données réelles |
| Garde-fou | L'Oméga ne doit pas devenir un score de conscience public ni un classement ([monde-miroir.md](monde-miroir.md) §13) ; c'est le "mana" de la vision — vocabulaire à unifier (mana vs Oméga) |
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

| Aspect | Impact |
|---|---|
| Front | Monde 0 : écran de seuil + vidéo (à l'essai, groupe test) ; Monde 1+ : page unique avec trois blocs — **Mes cercles** (nature du cercle, Ω générés par le cercle et part revenue au joueur), **Ouvrir un cercle** (nom, thématique, description), **Cercles à découvrir** (cercles cherchant des membres ; l'ouvreur reçoit les demandes et contacte par téléphone/e-mail) |
| Modèle | Un seul objet Cercle — pas de distinction discussion/croissance : tous les cercles deviennent de fait des cercles de croissance à partir du Monde 2 ; membres, ouvreur, thématique, description, comptabilité Ω (généré / redistribué) |
| Écarté | Page dédiée « cercle Monde 2 » ; distinction DiscussionCircle/GrowthCircle |

### F12 — Ressourcerie en six cartographies

| Aspect | Impact |
|---|---|
| Taxonomie | Pensées, Pratiques, Experts, Projets, Communautés, Événements ; `Chrysalide` devient un sous-type/qualificatif de Projet |
| Modèle | Graphe de noeuds et relations, pas six silos ; recherche globale, facettes par type et relations affichables |
| Front | Six portes orientées Comprendre, Pratiquer, Rencontrer, Soutenir, Rejoindre, Vivre ; vues liste/carte |

### F13 — Profil, droits, Open Badges et puissances

| Aspect | Impact |
|---|---|
| Oméga | Séparer solde disponible et contribution cumulée ; bloc « Ce que tes Oméga ouvrent » = texte d'ambition + vidéo (mécanisme régénératif complet en horizon, cf. [cosmo-coin-omega.md](cosmo-coin-omega.md)) ; aucune lecture comme score de conscience ; représentation lemniscate animée en synthèse du profil |
| Mon Récit | **4e sous-menu du profil (Boris, 2026-07-13)** : page dédiée avec résumé global évolutif en entrée (régénéré avec le mentor à chaque Graine, toujours validé par le joueur) + fil des Graines avec résonances consultables. Limite par Graine : 800 caractères (recommandation Claude dans la fourchette 500-1 000 décidée par Boris — ajustable) |
| Badges | Credentials Open Badges avec émetteur, critères et preuves distincts des trophées ludiques internes |
| Puissances | Six axes Ombre/Lumière et Transcendance en synthèse ; **degrés officiels du moteur (Boris, 2026-07-13) : Blocage · Tiédeur · Alignement · Alchimisation · Hyperconscience**, évalués en 360° (collecte depuis les expériences concernées à concevoir) ; lemniscate de synthèse en tête ; source/date/visibilité des lectures ; privé par défaut |
| Sécurité | Pas de diagnostic automatisé, de classement public ou de partage sans consentement explicite |

### Décisions UX transverses (Boris, 2026-07-13)

- **Cercles progressifs** : l'ancienne décision de masquer totalement l'entrée avant le Monde 2 est remplacée par F11. L'entrée existe dès le Monde 0 comme teaser ; discussions au Monde 1 ; croissance au Monde 2.
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

1. **Programme V1 (révisé 2026-07-14) : tout se construit d'abord DANS vibe.ze.game.** Objectif : un proto fonctionnel à montrer au cercle cœur du Point Zéro et à Mathieu avant de lancer l'appli autonome. La décision d'appli dédiée (BDD séparée, stores, SSO, « powered by ze.game ») reste actée mais son exécution est différée après cette validation.
2. **Implémentation démarrée dans vibe.ze.game (2026-07-14).** Layout Point Zéro en place (logo, chip Ω temps réel, nav Accueil/Marelle/Cercle/Ressources/Profil — Cercle et Ressources désactivés) + accueil orchestrateur V1 (états : seuil nouveau joueur avec news Festival / Monde 0 en cours avec prochaine Action, progression, lemniscate Ω). Particularités techniques : les assets de prod sont buildés hors serveur (Capistrano copy public/assets) → les ajouts PZ sont servis en statique depuis public/pz/ (CSS pur, fonts, logos) sans toucher à la chaîne de build. Versioning : git local dans ~/zegame/current (branche pointzero) — ATTENTION, un cap deploy de Mathieu écraserait le dossier : à coordonner avec lui.
3. **Bac à sable réinitialisé (2026-07-14).** vibe.ze.game est une instance sandbox séparée de la préprod — aucune précaution multi-clients nécessaire. Contenu réduit au seul parcours « Point Zéro - Monde 0 » (12 Actions, 13 inscrits). **11 communautés « Point Zéro - Monde N » créées (N = 0 à 10)** — ce qui tranche la question ouverte de la numérotation : 11 positions. Monde 0 = communauté default + joinable ; les membres d'une communauté Monde = les joueurs entrés dans ce Monde. Communauté « Cercle pédagogique PZ » conservée (facilitateurs). Tous les utilisateurs conservés. Sauvegarde : ~/backup-avant-reset-pz-*.sql sur le serveur.
3. **Charte graphique actée** : base violet identique à ze.game ; titres Roboto Slab, texte Poppins ; logos dans Dropbox/Vibe Coding/Ressources Point Zero/Logos (spirale PZ + Cosmo Coin infini). DA appliquée au proto (v3.0, étape 4 du workflow).
4. **Base de données séparée (différé).** La nouvelle appli Point Zéro ne partage pas la BDD de ze.game. Nouveau compte sur les stores (Apple/Google) dédié au Point Zéro. Mention « powered by ze.game » dans l'appli, et **SSO** entre les deux plateformes (chantier technique à cadrer : ze.game comme fournisseur d'identité ? OIDC ?).
5. **Une seule monnaie : l'Oméga (révisé 2026-07-13).** Le jeu en réalité alternée (monde-miroir) n'apparaît pas à ce stade du produit : toute mention au mana est éliminée de l'interface et des chantiers F1-F13. Les docs de vision monde-miroir restent un horizon non planifié.
6. **7 puissances : référentiel existant de l'app.** Les compétences actuelles au format « PUISSANCE : ASPECT » avec framework « Point Zéro - Puissance - Lumière/Ombre » servent de base — pas de nouvelle couche de données pour la V1. Approfondissement théorique dans [sept-puissances.md](sept-puissances.md).

## 4. Questions ouvertes restantes

1. Architecture SSO : protocole, sens de la fédération (ze.game IdP ?), partage ou non des comptes existants.
2. Compteurs temps réel du Festival : SSE existant ou solution dédiée ?
3. Si BDD séparée : comment le Monde 0 actuel (données dans vibe.ze.game) migre-t-il vers la nouvelle appli ?
4. Quel mécanisme WordPress porte le contexte du compte applicatif jusqu'au billet : métadonnée de commande, champ participant dédié ou jeton de rattachement créé après paiement ?
5. Quelle source fait foi pour les capacités : stock global de billets WordPress, réservations d'expériences dans l'appli, ou deux niveaux distincts ?
6. Combien d'événements payants par an justifieraient le remplacement de WooCommerce par une billetterie Stripe native ?
