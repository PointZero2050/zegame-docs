# Billetterie — gestion collaborative des événements

> Rédigé par Claude le 2026-08-01 après arbitrage de Boris. Remplace la gestion par plugins
> WordPress (The Events Calendar Pro + Event Tickets Plus + WooCommerce).
> Contexte : [refonte-site-plan-migration.md](refonte-site-plan-migration.md).

## 1. Décision de fond : les événements ne sont pas gérés par LLM

Le site adopte la gestion par LLM pour son **contenu** — de la prose, versionnée en fichiers,
écrite par une ou deux personnes et relue avant publication. Les événements relèvent d'une
autre nature et suivent une autre voie : ce sont des **données opérationnelles structurées**,
créées par plusieurs intervenants, souvent dans l'urgence, et qui engagent de l'argent.

Quatre raisons de les tenir en base plutôt qu'en fichiers :

1. **Concurrence** — plusieurs intervenants éditent en parallèle ; une base gère nativement ce
   que des fichiers versionnés transforment en conflits.
2. **Immédiateté** — corriger une date erronée doit prendre trente secondes, pas un cycle de
   déploiement.
3. **Contributeurs non techniques** — décrire un événement dans une conversation puis attendre
   une mise en ligne, sans pouvoir se corriger soi-même, est un dispositif fragile.
4. **Intégrité référentielle** — les inscriptions vivent en base et référencent l'événement.
   Un événement en fichier créerait une jointure à cheval entre disque et base, avec des
   capacités et des références qui divergent silencieusement.

**Où le LLM apporte réellement quelque chose** : rédiger accroche et description à partir d'un
brief, générer une série récurrente, répondre à des questions de lecture (« combien de places
restantes en octobre ? »). De la matière et de la lecture, pas de la saisie structurée.

## 2. Arbitrages de Boris — 2026-08-01

| Sujet | Décision |
|---|---|
| Publication | **Directe pour tous** les intervenants habilités, sans étape de validation |
| Accès aux inscrits | **Chacun pour ses propres événements** ; les administrateurs voient tout |
| Récurrence | **Série générée depuis un gabarit** (Sas mensuels, Ateliers) |
| Périmètre admin | Événements, **inscriptions**, **abonnés newsletter** |
| Pages de contenu | **Hors périmètre** — elles restent en fichiers versionnés, gérées par LLM |

Ajout de Boris : **connecter les événements et la lettre d'information**, en proposant aux
participants de s'y inscrire par une invitation envoyée par courriel.

## 3. Comptes et rôles

L'application n'a pas encore d'authentification. C'est le premier besoin réel — et ce n'est
pas du travail jetable : le cadrage Festival prévoit déjà Devise en remplacement de
`mathieu_core`.

**Décision de conception : un seul modèle `User` porteur de rôles**, plutôt que deux systèmes
d'identité. Sans cela, il faudra réconcilier comptes d'organisateurs et comptes de joueurs au
moment du Festival — exactement ce que le cadrage cherche à éviter.

Rôles prévus : `administrateur` (tout), `organisateur` (crée et publie des événements, voit
les inscrits des siens). Le rôle `joueur` viendra avec l'application Festival.

**Traçabilité** : chaque événement porte son créateur et l'auteur de la dernière modification.
Sur des enregistrements qui touchent à l'argent, savoir qui a changé un prix et quand n'est
pas du confort.

## 4. Gabarits et récurrence

Un **gabarit** décrit ce qui ne change pas d'une occurrence à l'autre — titre, catégorie,
durée, lieu ou visio, capacité, prix, description — et une **règle de récurrence** décrit le
rythme (par exemple le premier lundi de chaque mois, à 17 h 30). La génération produit des
événements ordinaires, ensuite modifiables un par un : le gabarit sert à créer, il ne pilote
pas en continu. C'est volontaire — une occurrence annulée ou déplacée ne doit pas être
réécrasée par son gabarit.

## 5. Passerelle événements → lettre d'information

Deux chemins, tous deux à consentement explicite :

1. **À l'inscription** : une case à cocher, **jamais pré-cochée**, déjà en place
   (`newsletter_acceptee`).
2. **Par invitation** : un courriel proposant de s'inscrire, contenant un lien unique.

⚠️ **Contrainte non négociable** : l'invitation **n'inscrit personne**. Seul le clic vaut
consentement, et il passe par le même double opt-in que le formulaire public. Une adresse
donnée pour s'inscrire à un événement n'est pas un consentement marketing ; l'assimiler
exposerait le Point Zéro et, plus simplement, ce serait déloyal.

Garde-fous complémentaires : ne jamais envoyer l'invitation à une personne **déjà désabonnée**,
ni à une adresse en rebond ; ne l'envoyer qu'une fois par personne ; et la rendre inutile pour
qui a déjà coché la case à l'inscription.

## 6. Lots de réalisation

| Lot | Contenu | Dépend de |
|---|---|---|
| A | Devise, modèle `User`, rôles, traçabilité | — |
| B | Administration des événements : liste, création, édition, publication directe | A |
| C | Inscriptions : consultation filtrée par propriété, recherche, export CSV, émargement | B |
| D | Gabarits et génération de séries récurrentes | B |
| E | Administration des abonnés : consultation, désinscription, export | A |
| F | Invitation newsletter aux participants, à consentement explicite | C, E |

## 7. Points ouverts

- Combien d'intervenants, et qui ? Cela conditionne la finesse des rôles.
- Les organisateurs doivent-ils pouvoir **annuler** un événement déjà vendu — et alors,
  comment sont traités les remboursements Stripe ?
- Faut-il une **liste d'attente** quand un événement est complet ?
- L'émargement du jour J se fait-il dans cette interface, ou dans l'application Festival ?
