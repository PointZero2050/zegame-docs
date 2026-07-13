# Proposition : accueil Point Zéro et mode événement

> Ajout Codex - 2026-07-12. Proposition de travail discutée avec Boris. Ce document décrit une direction UX et un workflow de prototypage, pas encore une spécification validée.

## 1. Intention

La page actuelle est un carnet de bord technique : elle expose communautés, parcours et demandes de feedback, mais ne dit pas clairement au Joueur où commencer.

L'accueil Point Zéro doit devenir un seuil personnalisé répondant à trois questions :

1. Où suis-je ?
2. Que se passe-t-il maintenant ?
3. Quel est mon prochain pas possible ?

Il ne montre pas tout ce que l'application contient. Il présente le portail le plus pertinent au bon moment.

## 2. États de l'accueil

La page varie selon la situation :

| État | Action principale |
|---|---|
| Nouveau Joueur | Entrer dans le Monde 0 |
| Monde 0 actif | Continuer la prochaine expérience |
| Trace à déposer | Mettre en mots ce qui a été vécu |
| Résonances reçues | Découvrir les échos reçus |
| Cercle actif | Préparer la prochaine rencontre |
| Retour après absence | Retrouver le fil du voyage |
| Événement à venir | Préparer sa participation |
| Événement en direct | Choisir une expérience disponible |
| Après événement | Intégrer la journée et poursuivre |

Les rôles pédagogiques et administratifs utilisent un espace séparé de l'accueil Joueur.

## 3. Structure recommandée

### Premier écran

- identité Point Zéro ;
- salutation contextualisée ;
- Monde ou événement actuellement prioritaire ;
- prochaine expérience ;
- une action dominante ;
- aperçu du cercle ou du rendez-vous à venir.

### Sections secondaires

1. **Ce qui t'appelle** : actions relationnelles formulées humainement, jamais simples compteurs de feedback.
2. **Ton chemin** : représentation compacte de la Marelle et du Monde actuel.
3. **Ton cercle** : membres, prochaine rencontre, quête et dernière trace.
4. **Ton récit** : dernière expérience, intention ou bloc de récit-fresque.
5. **Explorer** : autres parcours, communautés, ressourcerie et événements, placés après le prochain pas.

La future fenêtre vers le monde-miroir pourra remplacer la zone principale sans changer cette hiérarchie.

### Navigation mobile envisagée

- Accueil ;
- Marelle ;
- Cercle ;
- Ressources ;
- Profil.

La messagerie reste d'abord contextuelle dans l'accueil, le cercle et les quêtes.

## 4. Direction visuelle

- fond quotidien clair et calme ;
- noir profond structurant ;
- magenta conservé comme accent historique ;
- jaune solaire pour l'appel et l'intention ;
- vert vivant pour les manifestations de la Cité ;
- illustration réelle du Monde ou de l'événement prioritaire ;
- typographie expressive aux seuils et sobre pour les usages quotidiens ;
- animations réservées aux passages importants.

Le Monde 0 doit être un signal de premier plan, pas une carte parmi d'autres.

## 5. Mode événement

Cas pilote : **New Civilization Festival - 7 ans pour bâtir la civilisation de la conscience**, le 1er octobre à Paris.

Source : `https://pointzero2050.com/event/new-civilization-festival-7-ans-pour-batir-la-civilisation-de-la-conscience/`.

L'application fait partie de l'expérience annoncée : journée immersive, auto-évaluation, badges et crédits conscients, avec plusieurs salles et un public disposant déjà de certains prérequis.

Le Journey événementiel et le Monde 0 constituent deux chemins parallèles :

```text
Chemin de fond
└── Marelle -> Monde 0 -> Mondes suivants

Expérience temporaire
└── Festival -> parcours du jour -> intégration
```

Le Festival est une porte latérale ou un portail temporaire, pas un Monde supplémentaire. Le Monde 0 reste disponible avant, pendant et après.

### Avant l'événement

- compte à rebours et informations pratiques ;
- confirmation et profil minimal ;
- prérequis et cadres relationnels ;
- besoins d'accessibilité ;
- court préambule éventuel ;
- accès au Monde 0 en attendant.

L'entrée doit être très courte, via invitation, lien ou QR code, sans exposer immédiatement les notions internes de Journey et Community.

### Jour J

L'événement prend temporairement la priorité. L'accueil affiche :

- expériences disponibles maintenant ;
- salle, durée et capacité éventuelle ;
- progression de la journée ;
- annonces importantes ;
- recommandation non contraignante ;
- filtres par durée, salle, individuel/collectif, cinq cadres et disponibilité ;
- accès discret à « Ma Marelle ».

L'ordre des Challenges est libre. La bonne représentation est une constellation ou une carte d'expériences plutôt qu'une liste numérotée.

États possibles : disponible, recommandé, réalisé, à intégrer, temporairement indisponible et réalisable en groupe.

### Après l'événement

- synthèse des expériences vécues ;
- temps d'intégration ;
- auto-évaluation selon les cinq cadres ;
- badges et crédits conscients, lorsque leurs règles seront clarifiées ;
- premier bloc de récit-fresque ;
- recommandations de parcours ;
- invitation à commencer ou reprendre le Monde 0 et à rejoindre un cercle.

L'événement rejoint ensuite l'historique sans continuer à monopoliser l'accueil.

## 6. Priorité contextuelle

Ordre de résolution proposé :

1. événement en direct ;
2. événement imminent nécessitant une préparation ;
3. intégration post-événement ;
4. action prioritaire du parcours de fond ;
5. exploration libre.

Cette règle doit être configurable et réutilisable pour ateliers, conférences, festivals, programmes d'entreprise et événements partenaires.

## 7. Modes de progression d'un Journey

- **Séquentiel** : ordre imposé.
- **Libre** : tous les Challenges accessibles.
- **Guidé** : ordre recommandé mais non obligatoire.
- **Conditionnel** : disponibilité selon des critères.
- **Temporel** : disponibilité selon un créneau.

Le Festival utiliserait un mode libre ou guidé. Ces modes devront s'articuler avec le futur moteur décrit dans [validation.md](validation.md).

## 8. Objet campagne envisagé

```text
EventCampaign
├── identité, dates et lieu
├── phases préparation / direct / intégration / archive
├── Journey associé
├── salles et horaires
├── invitations et participants
├── annonces
└── règles de mise en avant sur l'accueil
```

Fenêtres possibles : `featured_from`, `live_from`, `live_until`, `integration_until`, `archive_at`.

Les Challenges événementiels peuvent ajouter durée, salle, capacité, créneau, matériel, QR code, type de groupe, cinq cadres et modalités d'auto-évaluation.

## 9. Contraintes du jour J

- pages légères et contenus essentiels mis en cache ;
- QR codes robustes ;
- sauvegarde locale temporaire et reprise après coupure ;
- interface utilisable rapidement et debout ;
- aucun formulaire long ;
- accès clair au support organisateur ;
- vérification de la charge simultanée et du comportement sur réseau médiocre.

## 10. Architecture produit

Ne pas créer immédiatement un fork indépendant de ze.game. L'analyse des dépendances dans [../architecture.md](../architecture.md) recommande de conserver le domaine et l'infrastructure existants, puis de construire une couche d'expérience dédiée :

```text
Noyau partagé ze.game
├── utilisateurs
├── Journeys et Challenges
├── validations et messagerie
└── administration

Expérience clients ze.game
└── interface actuelle

Expérience Point Zéro
├── layout et identité
├── accueil orchestrateur
├── Marelle et vocabulaire dédié
├── campagnes événementielles
└── futures fonctions du monde-miroir
```

Les écrans Point Zéro peuvent utiliser leurs propres contrôleurs et vues en réutilisant modèles et authentification existants, sans dépendre du paradigme CRUD de `DefaultActions` lorsque celui-ci n'est pas adapté.

## 11. Workflow de prototypage

### Étape 1 - États et contenus

Définir message principal, action, informations secondaires et éléments absents pour les états : nouveau, Monde 0, avant Festival, Festival direct, après Festival et retour après absence.

### Étape 2 - Wireframe

Valider hiérarchie, navigation, textes réels et comportement mobile avant la direction artistique.

### Étape 3 - Prototype HTML autonome

```text
prototypes/point-zero-home/
├── index.html
├── styles.css
├── app.js
└── assets/
```

Sans backend ni installation. Un sélecteur de démonstration ou un paramètre `?state=` permet de simuler les différents contextes.

Le prototype doit simuler action principale, navigation mobile, progression du Monde 0, parcours libre du Festival, filtres, attention relationnelle, cercle et retour vers la Marelle.

### Étape 4 - Direction visuelle

Appliquer l'identité Point Zéro après validation de la structure, avec des variables de design et sans framework lourd afin de faciliter la traduction ultérieure en HAML/SCSS.

### Étape 5 - Vérification

Tester au minimum `390x844`, `768x1024` et `1440x900`, ainsi que textes longs, absence de cercle, nombreuses notifications, événement terminé, navigation clavier, contraste et débordements.

### Étape 6 - Validation et documentation

Enregistrer décisions, formulations, composants rejetés, règles de priorité et comportements responsive. Le prototype devient la référence visuelle, pas le code de production.

### Étape 7 - Implémentation Rails

1. thème et layout Point Zéro ;
2. moteur de priorité de l'accueil ;
3. états nouveau Joueur et Monde 0 ;
4. phases Festival ;
5. Journey libre ou guidé ;
6. aperçu du cercle et actions relationnelles ;
7. administration des campagnes.

## 12. Première V1 proposée

1. Identité Point Zéro distincte.
2. Accueil « contexte actuel + prochaine action ».
3. Vue spécifique au nouveau Joueur.
4. Actions relationnelles contextualisées à la place des compteurs.
5. Aperçu du cercle.
6. Section Explorer secondaire.
7. Emplacements préparés pour la Marelle et le monde-miroir.
8. États Festival avant, direct et après.
9. Journey événementiel à ordre libre.

Cette V1 améliore déjà l'accueil tout en servant de base réutilisable au Festival et à la vision cible.

## 13. Décisions de cadrage (Boris, 2026-07-12)

<!-- Ajout Claude, 2026-07-12 — arbitrages recueillis lors du lancement de l'étape 1 -->

1. **Ton de la voix : mixte.** Narratif-poétique aux moments de seuil (première arrivée, retour après absence, passages), sobre et direct pour les usages quotidiens (continuer une expérience, filtres Festival). Conforme au §4.

2. **Vocabulaire : hybride prudent.** Le nouveau vocabulaire (expérience, trace, résonance, Monde 0) s'applique au Monde 0 et au Festival. Le vocabulaire actuel (parcours, défis, points) reste pour les contextes clients classiques.

3. **Périmètre — décision structurante : une nouvelle application dédiée Point Zéro sera créée pour l'écosystème.** Ze.game continue de servir les clients « classiques » (KEDGE, ESSAIM...). L'accueil orchestrateur décrit ici est donc celui de la future appli Point Zéro, pas un remplacement de l'accueil ze.game.
   - Le §10 (architecture produit) est à relire à cette lumière : la « couche d'expérience Point Zéro » devient une application à part entière. Reste à arbitrer ce qu'elle partage avec ze.game : gems (`mathieu_core`), modèles, base de données, comptes utilisateurs, serveur — voir [../architecture.md](../architecture.md) §8 pour les dépendances en jeu.
   - Le prototype HTML n'est pas impacté (agnostique par nature) ; c'est l'étape 7 (implémentation) qui change de cible.

4. **Festival : confirmé comme cas pilote.** New Civilization Festival, 1er octobre, Paris. Les trois états Festival sont prioritaires dans le prototype, et le chemin critique du jour J (QR codes, usage mobile debout, tenue de charge) doit remonter dans la planification.


## 14. Retours wireframe v1 (Boris, 2026-07-12)

Retours détaillés et impacts backoffice consignés dans [impacts-fonctionnels.md](impacts-fonctionnels.md) (registre F1-F8) : module News featured, mode libre/linéaire, parcours obligatoire, Marelle multi-parcours au Monde 1, Grains de Récit avec mentors IA, Oméga (lemniscate), mode événement (salle + compteurs), vocabulaire Challenge → Action. Wireframe v2 dans le repo zegame-prototypes.

## 15. Parcours d'inscription au Festival (Boris + Codex, 2026-07-13)

<!-- Ajout Codex, 2026-07-13 — formalisation de l'intention exprimée par Boris -->

L'expérience Festival commence avant l'état « inscrit ». Le frontoffice doit couvrir le parcours complet :

```text
Festival visible sur l'accueil
        ↓
Découvrir le Festival
        ↓
S'inscrire ───────────────→ achat sur le site Point Zéro
        │                              ↓
        │                    retour après paiement
        │                              ↓
        └─ « J'ai déjà un billet » → rattachement par code ou QR
                                       ↓
                              inscription confirmée
                                       ↓
                       préparation → direct → intégration
```

### États frontoffice ajoutés au prototype v2.1

1. `festival-inscription` : proposition d'inscription et bénéfices de l'appli avant, pendant et après l'événement.
2. `festival-lier` : rattachement d'un billet existant par code ou QR.
3. `festival-confirme` : confirmation explicite du lien entre billet et compte.
4. `festival-experience` : détail d'une expérience du jour J.
5. `festival-reserve` : place réservée et consignes d'accès.
6. `festival-attente` : expérience complète, liste d'attente et alternative disponible.

### Règle d'identité

L'adresse e-mail d'achat ne doit jamais être la clé unique de rattachement. Un billet peut être acheté avec une autre adresse ou par un tiers. L'identité fonctionnelle est un **billet unique**, associable une seule fois à un compte par un jeton de retour, un code ou son QR. L'e-mail reste une donnée de contact et de rapprochement assisté, pas la preuve de propriété.

### Recommandation progressive

Pour le Festival du 1er octobre, conserver en première intention la billetterie existante Event Tickets Plus + WooCommerce + Stripe, puis construire un pont minimal vers l'appli : contexte de départ, synchronisation du paiement, retour signé et solution de rattachement manuel. Cette voie réutilise la gestion actuelle des stocks, commandes, remboursements et billets.

Une billetterie native dans l'appli devient pertinente dans un second temps si les événements sont nombreux et si Point Zéro veut maîtriser durablement le tunnel d'achat. Elle devrait alors utiliser Stripe Checkout côté serveur plutôt qu'un formulaire bancaire développé sur mesure, tout en conservant le même contrat frontoffice (`pending`, `paid`, `linked`, `checked_in`, `cancelled`, `refunded`).

Le choix du fournisseur ne doit donc pas modifier les écrans du joueur. Il modifie seulement la manière dont une inscription payée entre dans le système.
