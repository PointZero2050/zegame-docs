# Mode événement — spécification

> Rédigée par Claude (portable de Boris) le 2026-08-04, à partir des choix de Boris du même
> jour. Remplace la spécification F7 de `impacts-fonctionnels.md`, écrite avant que la
> billetterie devienne interne. Cible : le New Civilization Festival du 1er octobre 2026.

## 1. Principe

Un événement n'introduit **aucune nouvelle nature d'objet pédagogique**. Un atelier du Festival
est une **expérience** ordinaire — contenu, Ω, compétences, validation — et l'ensemble des
ateliers d'un événement forme un **parcours** ordinaire, qui vit dans la Marelle comme les
autres. Seule la **logistique** est nouvelle : une salle, un horaire, une capacité.

Conséquence directe : le carnet de bord, le profil, les Ω, l'espace pédagogique et la Marelle
fonctionnent sans une ligne de code supplémentaire.

## 2. Modèle

### Le créneau, objet de liaison

Le créneau **n'est pas un attribut de l'expérience**. Un même atelier peut se tenir deux fois
dans la journée, dans deux salles : si l'horaire vivait sur l'expérience, il faudrait la
dupliquer, et les deux exemplaires divergeraient. Le créneau est donc une liaison, exactement
comme `ChallengesJourney` relie déjà une expérience à un parcours.

```
Event (le billet)          — existant
Journey « Parcours du jour » — existant, composition pédagogique
Challenge (un atelier)     — existant, contenu et Ω
Creneau                    — NOUVEAU : event + challenge + salle + début/fin + capacité
InscriptionCreneau         — NOUVEAU : user + creneau
ChallengesUser             — existant : progression, validation, Ω
```

`Creneau` : `event_id`, `challenge_id`, `salle` (chaîne), `debute_le`, `termine_le`,
`capacite`, `note` (précision logistique facultative).

`InscriptionCreneau` : `creneau_id`, `user_id`, `created_at`, `annulee_le`.
Index d'unicité sur (`creneau_id`, `user_id`).

**La salle reste une chaîne**, pas un modèle : une dizaine de salles pour un événement ne
justifie pas une table, et le regroupement par salle se fait très bien sur une chaîne.

### Le parcours du jour

Un `Journey` ordinaire, en mode **libre** (les participants choisissent, il n'y a pas d'ordre
imposé) et **non obligatoire**. Il porte les ateliers via `ChallengesJourney` comme n'importe
quel parcours.

**Question de rattachement, à trancher** : ce parcours appartient à quelle communauté ? Ma
recommandation : **au Monde 0**. Un billet donne alors accès au Monde 0, donc au jeu tout
entier après le Festival — ce qui est précisément l'intention annoncée sur le site
(« entrer dans un parcours collectif soutenu par l'application »). L'alternative, une
communauté « Festival 2026 » dédiée, isolerait les participants et demanderait un second geste
pour les faire entrer dans le jeu.

## 3. Décisions de Boris — 2026-08-04

| Sujet | Décision |
|---|---|
| Inscription à un créneau | **Ferme à capacité pleine** — au-delà, on ne peut plus s'inscrire |
| Moment de la réservation | **Le jour même, sur place** — pas de réservation en amont |
| Chevauchement d'horaires | **Refusé** — réserver une place qu'on ne prendra pas en prive un autre |
| Validation | **Auto-validation par trois questions** (voir §4) |
| Portée des trois questions | **Expériences d'événement seulement** — les parcours existants ne changent pas |
| Troisième réponse | **Privée** — le joueur seul la lit |
| Ω | **Par compétence**, mécanisme existant ; le cadre dérivé les regroupe en puissances |
| Accès au compte le jour J | **QR sur le billet → lien magique** |

## 4. La validation par trois questions

À la fin d'un atelier d'événement, le joueur valide en répondant à :

1. **Qu'est-ce que j'ai apprécié ?**
2. **Qu'est-ce que j'ai appris ?**
3. **Qu'est-ce qui m'a manqué ?**

Les réponses sont stockées sur la progression (`challenges_users`, colonne `retour` en jsonb) et
consultables dans le carnet de bord du joueur. La validation attribue les Ω par le mécanisme
existant — aucune dérogation.

**Les trois réponses sont privées.** Aucune n'est publiée sur le profil communautaire ni lue par
l'équipe. Si un jour un agrégat anonyme des « manques » devait servir à améliorer les ateliers,
**la décision doit être prise avant que les données existent** : on ne peut pas rendre
exploitable après coup ce qui a été recueilli sous promesse de confidentialité.

## 5. Le chaînon billet → compte

C'est le point critique du jour J : sans réservation en amont, deux cents personnes doivent
pouvoir se connecter et réserver **sur place, debout, en quelques minutes**.

### Deux jetons, jamais un seul

⚠️ **Piège de sécurité.** Le code qui ouvre la session du participant et le code que l'équipe
scanne à l'entrée **ne peuvent pas être le même**. Si un membre de l'équipe scanne le lien
magique d'un participant, il ouvre sa session à sa place — et devient lui, avec son profil et ses
Ω.

| Usage | Jeton | Qui l'utilise |
|---|---|---|
| Ouvrir sa session | lien magique signé, envoyé **au participant** par courriel | le participant, sur son téléphone |
| Pointer l'arrivée | référence du billet (`PZ-XXXX`), en QR sur le billet | l'équipe, **authentifiée**, depuis `/gestion/inscriptions` |

Le pointage passe par un espace protégé : même si la référence fuite, elle ne donne aucun accès.

### Le lien magique

- Jeton signé, porté par la `Registration`, valable jusqu'à la fin de l'événement plus quelques
  jours.
- À l'ouverture : retrouve l'inscription, crée le compte si besoin (ou rattache un compte
  existant à la même adresse), ouvre la session, inscrit au parcours du jour.
- **Idempotent** : on peut le rouvrir autant de fois qu'on veut, il ne crée jamais deux comptes.
- Envoyé dans le courriel de confirmation d'achat, et rappelé dans un courriel la veille.

## 6. La ruée sur les créneaux

Réservation le jour même **et** capacité ferme : tout le monde réservera à 10 h 55 pour
l'atelier de 11 h. C'est exactement la situation qui a produit le risque de survente sur la
billetterie, corrigé le 2026-08-04.

Même remède : **verrou sur le créneau** au moment de la réservation, de sorte que deux
participants ne puissent pas prendre ensemble la dernière place. Ce n'est pas une optimisation,
c'est la condition pour que le compteur affiché soit vrai.

**Compteurs** : rendus par le serveur à chaque affichage, avec un rafraîchissement automatique
léger sur la page du programme (quelques dizaines de secondes). Pas de temps réel par flux
poussé — la complexité ne serait pas justifiée pour une journée.

## 7. Écrans

### Participant (mobile d'abord, debout)

1. **Le programme du jour** — les créneaux par tranche horaire, avec pour chacun : titre,
   salle, places restantes, et l'état de sa propre inscription. Les créneaux pleins sont
   visiblement fermés.
2. **La fiche d'un atelier** — la fiche d'expérience habituelle, augmentée de la salle, de
   l'horaire et du bouton de réservation ou d'annulation.
3. **Ma journée** — ses créneaux réservés, dans l'ordre horaire.
4. **La validation** — les trois questions, puis les Ω.

### Équipe (`/gestion`)

5. **Composer la journée** — créer les créneaux : atelier, salle, horaire, capacité.
6. **Affluences** — le remplissage de chaque créneau, pour rééquilibrer en cours de journée.
7. **Pointage** — l'existant (`/gestion/inscriptions`, émargement), inchangé.

## 8. Ce que cette spécification ne couvre pas

- **La liste d'attente** sur un créneau plein : non retenue pour le Festival.
- **Le rattrapage hors ligne** si le réseau du lieu tombe. À traiter comme un risque
  d'exploitation, pas comme une fonctionnalité : prévoir une liste papier des inscrits.
- **Les Ω spécifiques au collectif** (ce que le groupe produit ensemble) : hors périmètre.
- **La réservation en amont**, écartée par Boris — mais le modèle la permet sans changement si
  l'usage la réclame plus tard.

## 9. Ordre de construction

| Tranche | Contenu | Pourquoi dans cet ordre |
|---|---|---|
| 1 | `Creneau` + `InscriptionCreneau`, composition dans `/gestion` | Rien n'est visible sans les données |
| 2 | Programme du jour, réservation, annulation, verrou, compteurs | Le cœur de l'usage participant |
| 3 | Validation par les trois questions | Indépendante du reste, testable seule |
| 4 | Lien magique billet → compte | Le plus délicat : à faire quand le reste est stable, et à répéter en conditions réelles |

La tranche 4 dépend de l'ouverture de la vente : elle a besoin de vrais billets pour être
éprouvée.
