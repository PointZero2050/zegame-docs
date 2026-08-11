# Festival — matrice des droits et des états

> **Ajout Codex — 2026-08-11.** Spécification R10 destinée à l'implémentation et à la
> recette du New Civilization Festival. Elle complète
> [mode-evenement-specification.md](mode-evenement-specification.md) et
> [application-festival-2026.md](application-festival-2026.md). Elle ne modifie aucun droit
> Rails à elle seule.

## 1. Décision structurante

Le Festival est une **clé contextuelle**, pas un Monde et pas un rôle global.

- un billet valide et rattaché ouvre le Sas Festival, le parcours du jour et ses créneaux ;
- il inscrit aussi le joueur au Monde 0 selon le mécanisme déjà décidé ;
- il n'ouvre ni le Cercle, ni le Freeride, ni les fonctions de facilitation ou
  d'administration ;
- la fin de l'événement ne supprime ni les traces, ni les validations, ni les Oméga déjà
  légitimement acquis ;
- les droits d'équipe sont attachés à **cet événement**, jamais déduits du seul rôle DFF ni
  d'une communauté Monde 0 partagée.

La règle d'autorisation cible est donc l'intersection suivante :

```text
droit effectif = identité explicite
                × état de l'événement
                × état du billet
                × relation à l'objet
                × état du créneau ou de la réservation
```

Une vue masquée n'est pas une autorisation. Chaque action doit être refusée côté serveur si
l'une de ces conditions manque.

## 2. Acteurs

| Code | Acteur | Preuve d'accès | Limite impérative |
|---|---|---|---|
| A0 | Visiteur non connecté | aucune | contenu public et achat seulement |
| A1 | Joueur connecté sans billet valide | session | aucun accès au parcours ou aux données Festival privées |
| A2 | Porteur d'un billet payé mais non rattaché | lien magique ou procédure de secours | peut rattacher le billet, pas agir comme participant avant rattachement |
| A3 | Participant | session + billet payé et rattaché à ce compte | ses réservations, ses réponses et ses traces uniquement |
| A4 | Intervenant affecté | affectation explicite à un ou plusieurs créneaux | ses créneaux uniquement ; aucun accès global aux participants |
| A5 | Équipe Festival | mandat explicite borné à l'événement | exploitation de l'événement, sans lecture des traces personnelles privées |
| A6 | Administrateur global | rôle admin | accès opérationnel total, mais les vues de retours restent soumises aux garanties d'anonymisation |

### 2.1 Équipe Festival : cible et transition

La cible est une affectation événementielle explicite (`event_staff`, ou équivalent), avec
des capacités séparables : `programme`, `pointage`, `support_billet`, `affluence`,
`retours`. Pour le Festival pilote, ces capacités peuvent être tenues par des admins si le
modèle contextuel n'est pas prêt. Ce raccourci doit rester visible comme une **dette de
transition** : donner `admin` à un bénévole pour scanner des billets serait disproportionné.

Un facilitateur/DFF non affecté au Festival est traité comme A1. Une appartenance à la
communauté Monde 0 ne prouve jamais une relation d'exploitation.

## 3. États canoniques

### 3.1 Événement

| État produit | Sens | Actions publiques | Actions participant |
|---|---|---|---|
| `draft` | préparation privée | aucune | aucune |
| `sales_open` | publié, vente ouverte | consulter, acheter | rattacher un billet ; consulter les informations ouvertes |
| `sales_closed` | publié, vente close, avant jour J | consulter | rattacher un billet existant ; préparer son accès |
| `live` | journée en cours | consulter | programme, réservation, annulation, validation selon horaire |
| `ended` | événement terminé | consulter l'archive publique si publiée | relire sa journée, achever les validations pendant la fenêtre prévue |
| `cancelled` | événement annulé | information et recours | aucune nouvelle réservation ; accès aux informations de remboursement |

Ces états peuvent être calculés à partir du statut éditorial et des dates existantes plutôt
que devenir immédiatement un nouvel enum. Ils doivent néanmoins être résolus dans un seul
service, pas réinterprétés dans chaque vue.

### 3.2 Billet / inscription

| État | Accès Festival privé | Effet attendu |
|---|---|---|
| `pending` | non | paiement non confirmé ; reprise du tunnel seulement |
| `paid_unlinked` | non | activation possible par lien magique ou secours |
| `paid_linked` | oui | clé événement active pour le compte lié |
| `checked_in` | oui | arrivée au Festival constatée ; ne valide pas un atelier |
| `cancelled` | non | accès nouveau révoqué ; historique antérieur conservé si nécessaire |
| `refunded` | non | même règle que `cancelled`, avec information financière accessible |

Le QR de pointage et le lien magique restent deux secrets différents. Le premier atteste
l'arrivée ; le second ouvre une session. Aucun QR scanné par l'équipe ne doit connecter cette
équipe à la place du participant.

### 3.3 Créneau et réservation

| Objet | États utiles |
|---|---|
| Créneau | `upcoming` · `open` · `full` · `in_progress` · `ended` · `cancelled` |
| Réservation | absente · `active` · `cancelled` |
| Validation | absente · `draft` · `completed` |

`open` signifie ici : événement `live`, créneau non commencé, capacité disponible et fenêtre
de réservation ouverte. Ce n'est pas seulement « il reste des places ».

## 4. Matrice participant

Légende : **L** lecture · **A** action · **—** interdit · **C** condition supplémentaire.

| Surface / action | A0 visiteur | A1 sans billet | A2 billet non lié | A3 participant | Conditions d'état |
|---|---:|---:|---:|---:|---|
| Page publique du Festival | L | L | L | L | événement publié ou annulé |
| Acheter un billet | A | A | — | — | `sales_open`, stock disponible |
| Reprendre un paiement | A | A | A | — | inscription `pending`, preuve de reprise |
| Activer / rattacher le billet | — | — | A | — | billet payé, valide, non lié ; traitement idempotent |
| Voir son billet / son QR | — | — | — | L | billet du compte courant uniquement |
| Sas Festival privé | — | — | — | L | billet `paid_linked` ou `checked_in` |
| Programme du jour | aperçu public éventuel | — | — | L | clé événement valide |
| Fiche d'un atelier | aperçu public éventuel | — | — | L | atelier du parcours lié à l'événement |
| Réserver un créneau | — | — | — | A/C | événement `live`, créneau `open`, aucun chevauchement |
| Annuler sa réservation | — | — | — | A/C | réservation active, créneau pas commencé |
| Voir « Ma journée » | — | — | — | L | uniquement ses propres réservations |
| Répondre aux trois questions | — | — | — | A/C | réservation active, créneau terminé, fenêtre ouverte |
| Relire ses trois réponses | — | — | — | L | auteur uniquement |
| Voir ses Oméga et traces | — | profil propre | — | L | règles habituelles du Profil ; aucun accès équipe |
| Continuer le Monde 0 | — | selon droits ordinaires | — | A | le billet ouvre Monde 0, jamais Monde 1 automatiquement |

### 4.1 Réservation atomique

Le bouton « Réserver » n'est qu'une intention. Le serveur revérifie dans une transaction :

1. billet toujours valide et lié au compte ;
2. événement en cours et fenêtre ouverte ;
3. créneau non commencé et non annulé ;
4. absence de réservation active du même joueur ;
5. absence de chevauchement ;
6. capacité restante sous verrou.

Le refus renvoie un état compréhensible (`complet`, `chevauchement`, `fermé`, `billet
invalide`) et une prochaine possibilité quand elle existe. Il ne produit jamais un écran vide
ou une réservation fantôme.

### 4.2 Validation d'un atelier

La spécification canonique est l'**auto-validation par trois questions**. Le pointage d'entrée
atteste la présence au Festival, pas la présence à chaque atelier. Un intervenant ne valide donc
pas en masse les participants dans le pilote.

La validation est :

- disponible après la fin du créneau réservé ;
- idempotente : un double envoi ne double jamais les Oméga ;
- rééditable en brouillon tant qu'elle n'est pas confirmée ;
- finalisée avec les trois réponses et la règle d'attribution existante ;
- accessible après l'événement pendant une fenêtre configurable. **Hypothèse de recette :
  D+7**, à confirmer par Boris avant gel éditorial.

## 5. Matrice équipe et intervenants

| Action | A4 intervenant affecté | A5 équipe Festival | A6 admin |
|---|---:|---:|---:|
| Voir le programme publié | L | L | L |
| Voir l'affluence d'un créneau | L, ses créneaux | L, événement | L |
| Voir les noms des participants | — | L, strict nécessaire au pointage/support | L, strict nécessaire |
| Composer ou modifier la journée | — | A si capacité `programme` | A |
| Annuler un créneau | — | A si capacité `programme` + confirmation | A |
| Scanner une référence de billet | — | A si capacité `pointage` | A |
| Rattacher/détacher manuellement un billet | — | A si capacité `support_billet` + journal | A + journal |
| Lire les réponses 1 et 2 | — | — | — dans l'interface produit |
| Lire « ce qui m'a manqué » | L/C, ses créneaux | L/C | L/C |
| Exporter les inscriptions | — | A si capacité dédiée | A |
| Exporter les retours textuels nominatifs | — | — | — |
| Corriger une validation/les Oméga | — | — | recours admin tracé uniquement |

**L/C sur les retours** signifie : vue dédiée sans identité, ordre mélangé et seuil d'au moins
cinq réponses pour le périmètre affiché. En dessous du seuil, l'interface affiche « pas assez de
réponses pour préserver l'anonymat », jamais les textes. Les réponses 1 et 2 restent privées,
y compris pour l'admin dans les vues normales.

## 6. Visibilité après changement d'état

| Transition | Ce qui se ferme | Ce qui demeure |
|---|---|---|
| billet payé → remboursé avant l'événement | Sas, programme privé, réservation | facture, information de remboursement, recours |
| participant → billet annulé après réservation | nouvelles actions ; réservations rendues caduques | journal d'exploitation |
| événement `live` → `ended` | nouvelles réservations et annulations | Ma journée, réponses, traces, fenêtre D+7 |
| créneau `open` → `full` | nouvelle réservation | réservations actives existantes |
| créneau → `cancelled` | validation et participation | information, alternative éventuelle, historique |
| utilisateur quitte Point Zéro | session et accès en ligne | politique d'export/suppression et obligations comptables distinctes |

Un remboursement ne doit pas effacer automatiquement une progression déjà acquise après une
participation réelle. Ce cas exceptionnel passe par un recours tracé ; la couche paiement ne
réécrit jamais silencieusement l'histoire pédagogique.

## 7. Résolveurs à centraliser

La V1 n'a pas besoin d'un moteur générique de droits. Elle a besoin de prédicats nommés et
testables, par exemple :

```text
event_publicly_visible?
ticket_activatable_by?
festival_accessible_by?
slot_visible_by?
slot_reservable_by?
reservation_cancellable_by?
experience_validatable_by?
event_manageable_by?
ticket_checkable_by?
anonymized_feedback_visible_by?
```

Chaque prédicat prend l'utilisateur, l'objet et l'heure de référence. L'heure est injectée dans
les tests : aucun test du jour J ne doit dépendre de l'horloge réelle du poste.

## 8. Accessibilité et vérité d'interface

- chaque état est écrit en toutes lettres ; couleur, icône et position ne sont jamais l'unique
  information ;
- un bouton indisponible explique pourquoi et quand il pourra s'ouvrir ;
- les actions mobiles ont une cible d'au moins 44 × 44 px ;
- réservations et annulations annoncent leur résultat aux technologies d'assistance ;
- les compteurs rafraîchis utilisent une annonce `polite`, sans reprendre le focus ;
- le QR possède toujours une solution textuelle et humaine de secours ;
- les heures indiquent le fuseau et le jour lorsque l'ambiguïté est possible ;
- la page reste utilisable avec un réseau lent : l'état confirmé par le serveur prévaut sur
  l'optimisme de l'interface.

## 9. Banc minimal d'acceptation

1. Un visiteur voit un Festival publié mais ne voit jamais une réservation nominative.
2. Un joueur connecté sans billet ne peut pas appeler directement l'action de réservation.
3. Un billet `pending`, `cancelled` ou `refunded` n'ouvre pas le Sas.
4. Le lien magique lie un billet payé une seule fois et reste idempotent pour son propriétaire.
5. Le QR de pointage ne peut jamais ouvrir la session du participant.
6. Deux requêtes concurrentes sur la dernière place produisent une réussite et un refus.
7. Une réservation qui chevauche un créneau actif est refusée côté serveur.
8. Un participant ne peut lire, annuler ou valider la réservation d'un autre.
9. Un DFF non affecté ne reçoit aucun droit d'équipe par son seul rôle ou par Monde 0.
10. Un intervenant affecté voit le remplissage de son créneau, pas la liste globale des joueurs.
11. Une validation rejouée n'attribue jamais deux fois les Oméga.
12. Les réponses 1 et 2 ne figurent dans aucune vue équipe ni aucun export.
13. La réponse 3 reste invisible sous cinq réponses, sans contournement par filtre ou export.
14. Le passage de l'événement à `ended` ferme les réservations mais conserve les traces.
15. L'annulation d'un créneau notifie les inscrits et empêche sa validation.
16. Toutes les actions de support billet sont attribuées et horodatées.
17. À 390 px, achat, rattachement, réservation, annulation et validation sont faisables au clavier
    et sans débordement horizontal.
18. Une perte réseau pendant la réservation ne montre « réservé » qu'après confirmation serveur.

## 10. Deux arbitrages à fermer

1. **Fenêtre post-événement de validation** : recommandation D+7 pour le pilote, configurable.
2. **Intervenant et retours anonymisés** : recommandation d'ouvrir la réponse 3 à l'intervenant
   affecté à son créneau, uniquement au seuil de cinq et sans identité.

Ces choix n'empêchent pas d'implémenter le socle des droits. Leur valeur doit néanmoins être
figée avant la recette éditoriale et les courriels participants.
