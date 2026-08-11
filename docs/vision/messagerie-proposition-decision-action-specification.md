# Messagerie — spécification Proposition / Décision / Action

> **Statut :** v0.1 arbitrée et auditée — B3 ouvrable (arbitrages Boris et audit Claude du
> 12 août 2026, §13).
> **Décision préalable :** R11 est levé le 11 août 2026. L'intention appartient au fil
> ou au sous-fil ; elle ne qualifie pas chaque message et ne modifie jamais les droits.
> **Périmètre :** étape B de la messagerie capacitante. Ce document n'impose ni noms de
> tables Rails ni migrations avant l'audit de l'existant.

## 1. Finalité

La messagerie doit permettre à une conversation de produire une décision et une action
sans transformer chaque parole en formulaire. Le Fil reste le lieu de l'échange. Les
objets structurés rendent visibles les engagements qui en émergent.

Trois invariants gouvernent toute la fonctionnalité :

1. **un message n'est jamais un objet métier par défaut** ;
2. **toute transformation est explicite, réversible tant qu'elle est au brouillon et
   attribuée à une personne identifiable** ;
3. **les droits viennent du contexte du fil, jamais de l'intention affichée**.

## 2. Modèle mental

```text
Fil ou sous-fil (intention, lecteurs, droits)
├── messages ordinaires
├── Proposition ── versions ── objections
│   └── Décision ── protocole ── participants ── résultat ── révision
└── Action ── porteur(s) ── échéance ── état ── trace d'achèvement
```

- Une **Proposition** formule ce qui pourrait changer.
- Une **Décision** conserve comment et par qui une version précise de la Proposition a
  été tranchée.
- Une **Action** engage une ou plusieurs personnes à accomplir quelque chose dans un
  temps explicite.
- Une **objection** est liée à une Proposition en décision. Elle exprime ce qu'elle
  protège, le risque perçu et la condition de levée. Ce n'est pas une réaction négative.

## 3. Entrées UX

### 3.1. Le composeur

Le composeur s'ouvre comme un message simple. Le bouton `+` propose les objets cohérents
avec l'intention du fil, sans interdire les autres objets autorisés.

| Intention du fil | Objets mis en avant |
|---|---|
| Explorer | Question · Polarité · Proposition |
| Résonner | Graine · Mémoire · Ressource |
| Coordonner | Action · Rencontre · Ressource |
| Décider | Proposition · Décision en cours · Objection |
| Confronter | Objection liée · Polarité · Rencontre |
| Reconnaître | Graine · Mémoire · Rituel |
| Redistribuer | Contribution · Décision · Objection liée |

Une intention ne masque pas un objet auquel le joueur a droit. Elle le rend seulement
plus ou moins saillant.

### 3.2. Transformer un message existant

Le menu d'un message peut proposer `Créer une proposition` ou `Créer une action` aux
personnes habilitées. Le flux comporte toujours :

1. aperçu du texte repris et lien vers le message source ;
2. édition du titre et des champs métier ;
3. affichage des lecteurs du futur objet ;
4. confirmation de création.

Le message source n'est ni remplacé ni déplacé. Il reçoit une référence vers l'objet.
Si l'objet change de contexte ou élargit ses lecteurs, l'auteur du message doit consentir
à la reprise de son texte ; sinon l'objet est créé avec une reformulation et un lien
privé vers la source pour les seules personnes déjà autorisées.

### 3.3. Créer une Décision

Une Décision naît normalement d'une Proposition. Le bouton `Décider` fige la version
soumise et oblige à annoncer avant l'ouverture : protocole, participants éligibles,
visibilité des contributions, date de clôture et personne ou rôle habilité à clore.

La capture d'une décision prise hors de l'application reste possible, mais doit être
nommée `Consigner une décision déjà prise`, indiquer la source et ne pas simuler une
consultation qui n'a pas eu lieu.

## 4. Cycles de vie

### 4.1. Proposition

`brouillon → en exploration → soumise à décision → adoptée / à retravailler / retirée`

- **Brouillon** : visible de l'auteur et des personnes invitées ; supprimable.
- **En exploration** : visible selon les droits du fil ; commentaires et versions.
- **Soumise à décision** : la version soumise est figée ; les versions ultérieures
  créent une nouvelle proposition à examiner ou rouvrent explicitement le processus.
- **Adoptée** : liée à une Décision close.
- **À retravailler** : revient en exploration en conservant le cycle précédent.
- **Retirée** : reste lisible dans l'historique si elle a reçu des contributions.

### 4.2. Décision

`préparation → ouverte → close → révisée / annulée`

- **Préparation** : protocole et participants vérifiables avant ouverture.
- **Ouverte** : contributions selon le protocole ; règles immuables sauf annulation
  motivée et historisée.
- **Close** : résultat brut, éventuelle pondération séparée, formulation de la décision,
  date d'effet et date de révision.
- **Révisée** : une nouvelle Décision remplace la précédente sans l'effacer.
- **Annulée** : motif et autorité visibles ; les contributions restent auditables.

Pour un Cercle de croissance, le protocole v1 est le **consentement avec objections
argumentées**. Les autres protocoles restent annoncés ou réservés aux contextes qui les
justifient. La pondération Oméga n'est jamais proposée dans une décision ordinaire de
Cercle.

### 4.3. Objection

`brouillon → ouverte → répondue → levée / maintenue`

Champs obligatoires :

- ce que je cherche à protéger ;
- le risque que je perçois ;
- ce qui permettrait de lever l'objection.

Seul l'auteur peut déclarer son objection levée. Le rôle qui tient le cadre peut la
marquer `répondue`, jamais `levée` à sa place. Une objection maintenue à la clôture doit
être compatible avec le protocole annoncé : blocage, réserve enregistrée ou autre issue
explicite. Le LLM ne tranche ni la recevabilité ni la levée.

### 4.4. Action

`proposée → acceptée → en cours → bloquée → accomplie / abandonnée`

Une Action comporte : titre, résultat attendu, porteur principal, appuis éventuels,
échéance ou absence assumée d'échéance, contexte et source. L'assignation à une personne
requiert son acceptation. Une Action peut provenir d'une Proposition adoptée, d'une
Décision, d'un message ou être créée directement.

`Accomplie` demande une courte trace de résultat, pas nécessairement une preuve publique.
`Abandonnée` demande un motif. La date collective ne change jamais lorsque le destinataire
choisit de différer sa notification personnelle.

## 5. Droits fonctionnels

Les droits sont évalués objet par objet et héritent du contexte du fil, avec possibilité
de restriction explicite.

| Geste | Droit minimal |
|---|---|
| Lire une carte | lire le fil et l'objet référencé |
| Créer une Proposition | contribuer au fil + capacité `proposer` |
| Modifier une Proposition | auteur ou mandat explicite, tant que la version n'est pas figée |
| Ouvrir une Décision | capacité `ouvrir_decision` dans ce contexte |
| Participer | appartenir à l'électorat figé et avoir accès à l'objet |
| Objecter | participer au protocole et lire la version soumise |
| Clore | rôle ou mandat annoncé avant l'ouverture |
| Créer une Action | contribuer + capacité `creer_action` |
| Assigner | proposer un porteur ; l'acceptation appartient au porteur |
| Marquer accomplie | porteur principal ou rôle habilité, avec trace et historique |

Le facilitateur tient le cadre mais ne possède pas automatiquement tous les droits. Un
administrateur technique ne reçoit aucun droit métier par sa seule fonction technique.

## 6. Représentation dans les quatre vues

### Fil

Les cartes apparaissent à l'endroit de leur création ou de leur partage. Elles montrent
type, titre, statut, porteur, prochaine échéance, action principale selon les droits et
lien vers l'objet complet. Une carte reste compréhensible si son auteur ou une donnée
secondaire devient indisponible.

### Actions

Trois regroupements : `À accepter`, `En cours ou bloquées`, `Terminées récemment`.
Le tri privilégie l'échéance et les dépendances, jamais la popularité. Chaque personne
voit d'abord ce qui attend son geste ; le Cercle peut ensuite afficher l'ensemble.

### Décisions

Trois regroupements : `À préparer`, `Ouvertes`, `Closes et à réviser`. Une objection
ouverte est visible au même niveau que l'état de la Décision, sans exposer son détail à
des lecteurs non autorisés.

### Mémoire

Les décisions closes et les actions accomplies peuvent devenir des traces de Mémoire,
mais la projection ne duplique pas l'objet : elle pointe vers sa version historique.

## 7. Attention et notifications

Une seule source d'attention produit des projections dans l'accueil, les Échanges et le
Centre d'activité. Événements typiques :

- Proposition qui demande une contribution ;
- Action proposée au joueur ou arrivée à échéance ;
- objection qui appelle une réponse du rôle tenant le cadre ;
- Décision ouverte, bientôt close ou révisable ;
- mention ou réponse directe.

Les notifications nomment le geste attendu (`Accepter l'action`, `Répondre à
l'objection`) plutôt que le volume de messages. Un digest peut regrouper les événements.

## 8. Intégrité, suppression et audit

- Une carte et son objet sont distincts : archiver le message ne détruit pas l'objet.
- Une Proposition ayant reçu des contributions ne disparaît pas sans trace.
- Toute Décision conserve version soumise, protocole, électorat pertinent, contributions,
  résultat, clôture et révisions.
- Les changements de droits ou de lecteurs sont journalisés séparément des changements
  d'intention.
- Un export restitue les objets avec leurs liens et états, pas seulement le HTML du Fil.
- La dissolution d'un espace doit définir le devenir de ses objets avant clôture.

## 9. Place du LLM

Le LLM peut, à la demande : proposer une extraction de Proposition ou d'Action, résumer
les arguments avec leurs sources, repérer une objection sans réponse, préparer une
synthèse et signaler une incohérence de calendrier.

Il ne peut pas : publier un objet sans confirmation, assigner une personne, modifier un
protocole ouvert, décider, clore, lever une objection, évaluer une personne ou attribuer
des Omégas. Toute proposition IA porte ses sources et reste contestable.

## 10. Contrat d'événements fonctionnels

Les noms techniques seront définis après audit, mais l'application doit pouvoir produire
des événements équivalents à :

```text
proposal.created | proposal.versioned | proposal.submitted | proposal.withdrawn
decision.opened | decision.contribution_recorded | objection.opened
objection.answered | objection.lifted | decision.closed | decision.revised
action.proposed | action.accepted | action.blocked | action.completed | action.abandoned
```

Chaque événement porte : acteur, contexte, objet, horodatage, visibilité et source. Ces
événements alimentent `ActivityItem` sans y dupliquer la règle métier.

## 11. Découpage d'implémentation

### B3 — créer et transformer

- bouton `+` contextuel ;
- création Proposition et Action ;
- transformation explicite d'un message ;
- cartes dans le Fil ;
- acceptation d'une assignation ;
- bancs négatifs de droits et de changement de contexte.

### B4 — voir et suivre

- vues Actions et Décisions ;
- versions de Proposition ;
- protocole de consentement ;
- attention et échéances ;
- projections dans Mémoire sans duplication.

### B5 — migrer l'objection

- rattacher l'objection en trois temps à la Proposition/Décision ;
- supprimer le double registre comme réaction sémantique autonome ;
- conserver les anciennes objections avec une migration et une provenance explicites ;
- vérifier les autorisations sur chaque état.

## 12. Bancs d'acceptation minimaux

1. un lecteur peut voir une carte sans pouvoir agir ; l'interface le dit honnêtement ;
2. changer l'intention du fil ne change aucun droit ni état d'objet ;
3. transformer un message privé vers un contexte plus large exige le consentement de son
   auteur ou une reformulation sans divulgation ;
4. modifier une Proposition soumise ne réécrit pas la version en décision ;
5. une personne non éligible ne peut ni participer ni objecter ;
6. l'auteur seul lève son objection ; le facilitateur peut seulement la marquer répondue ;
7. une assignation n'engage pas son destinataire avant acceptation ;
8. supprimer une carte ne supprime pas silencieusement sa Décision ou son Action ;
9. différer une notification ne modifie pas l'échéance collective ;
10. les résultats bruts et pondérés restent séparés lorsqu'une pondération est autorisée ;
11. le LLM ne peut accomplir aucun geste engageant sans confirmation humaine ;
12. mobile : création, objection et acceptation sont possibles sans formulaire déplié
    sous un message ni débordement horizontal.

## 13. Arbitrages — tranchés par Boris le 12 août 2026

Les cinq points ci-dessous sont **arbitrés : la recommandation de chacun s'applique
telle quelle.** Le cinquième vient de l'audit Claude, absent de la v0.1 de Codex.

1. Au Monde 1, tout membre d'un Cercle peut-il créer une Proposition, ou ce droit est-il
   confié au gardien du cadre Gouvernance pendant la séance ? **Tranché : création
   ouverte, ouverture de la Décision mandatée.**
2. Une Action sans échéance est-elle autorisée ? **Tranché : oui, mais elle doit être
   explicitement classée `sans échéance`, jamais laissée vide par accident.**
3. À la clôture par consentement, une objection maintenue bloque-t-elle toujours ?
   **Tranché : le protocole choisi le définit avant ouverture ; le consentement du
   Cercle de croissance v1 traite une objection argumentée et maintenue comme
   bloquante.**
4. Qui peut consigner une décision prise hors application ? **Tranché : rôle tenant
   le cadre ou mandat explicite, avec validation d'au moins un autre membre.**
5. *(Ajouté par l'audit Claude.)* Décision et son protocole de consentement
   s'appliquent-ils aux gabarits d'Espace `groupe` et `echange`, ou seulement
   `cercle` ? **Tranché : Décision réservée au gabarit `cercle` en V1 ; Proposition et
   Action restent ouvertes aux trois gabarits.**

## 14. Références

- [Messagerie Point Zéro — vision cible](messagerie-point-zero-vision-cible.md)
- [Registre des impacts fonctionnels](impacts-fonctionnels.md), F21 à F24
- [Revue UX cible consolidée](revue-ux-cible-consolidee.md), R4, R8 et R11
- `zegame-prototypes/messagerie-point-zero-cible/`
