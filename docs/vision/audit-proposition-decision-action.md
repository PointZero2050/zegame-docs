# Audit Claude — spécification Proposition / Décision / Action

> Répond à la demande de la spec elle-même (« pour arbitrage Boris et audit Claude »,
> [messagerie-proposition-decision-action-specification.md](messagerie-proposition-decision-action-specification.md)).
> Confronte les invariants et le découpage B3/B4/B5 à l'état réel du code sur `preprod`
> (relevé le 12 août 2026). Rien n'est codé ici : ce document dit ce qui existe déjà, ce
> qui manque, et ce que B3 doit poser en premier.

## 1. Ce qui est déjà juste — aucun nouveau primitif à inventer

**Les droits (§5).** `ContexteDeFil#visible_par?` (`app/models/contexte_de_fil.rb`) EST
déjà « les droits viennent du contexte du fil, jamais de l'intention affichée » —
l'invariant 3 de la spec décrit littéralement un mécanisme qui existe et qui est le seul
point d'écriture de la règle d'accès depuis S1-A1. B3 n'a rien à réinventer : une carte
Proposition/Décision/Action est visible si `contexte.visible_par?(lecteur)`, point.

**Le protocole de carte (§6, « Fil »).** `Carte` (`app/models/carte.rb`) porte déjà le
contrat exact que la spec redemande (type, statut, porteur, action principale, lien,
disponibilité honnête si les données manquent) — et son commentaire réserve LE point
d'extension : *« Mission, Proposition et Décision viendront avec leurs specs (réserve de
l'audit S0 §6) — ce protocole est leur place. »* B3 ajoute `Carte::Proposition`,
`Carte::Decision`, `Carte::Action` comme sous-classes ; zéro refactor du contrat de base.

**Le mandat explicite (§5, §13.4).** La spec parle de « mandat explicite » sans dire d'où
il vient. Il existe déjà : le mandat de modération (`User`, arbitrage du 2026-08-09,
distinct du rôle administrateur — *« l'administrateur donne la console, le mandat donne
les conversations »*). C'est le même patron à réutiliser pour « qui peut clore une
Décision sans être gardien », pas une nouvelle table de capacités.

**La cible de la migration B5 est déjà identifiable.** `ReactionSemantique::OBJECTION`
porte déjà `protege`, `risque`, `condition_de_levee` — les trois champs que la spec §4.3
demande pour l'objection, au champ près. B5 n'est pas une hypothèse : c'est ce modèle,
augmenté d'un cycle de vie et d'un rattachement à une Proposition/Décision au lieu d'un
simple message.

## 2. Ce qui manque — à poser avant que B3 puisse commencer

**L'intention du fil (§3.1) n'a AUCUN support en base.** `Messaging::Thread` a une colonne
`kind`, mais elle est `nil` sur 100 % des fils existants et rien dans le code ne
l'alimente. Aucune colonne ne porte les sept valeurs de la spec (Explorer, Résonner,
Coordonner, Décider, Confronter, Reconnaître, Redistribuer) — cette matière n'existe
aujourd'hui qu'au niveau des maquettes et des documents de revue (R11, R6b). C'est le
mécanisme central du composeur (§3.1 : *« le bouton `+` propose les objets cohérents avec
l'intention du fil »*) et il n'a pas de colonne. **Premier sous-lot de B3, avant le
composeur lui-même : poser l'attribut (probablement sur `Messaging::Thread`, à confirmer
— les sous-fils de S1-A2 existent déjà, donc « par fil » peut vouloir dire « par sous-fil »
aussi, à trancher), sa validation, et son affichage — sans quoi tout le reste de B3 se
construit sur du vide.**

**`ActivityItem` (F21) n'existe pas.** La spec §7 et §10 assument que les événements
« alimentent `ActivityItem` » — zéro occurrence dans le code, c'est un objet d'horizon
(registre d'impacts F21, non commencé). Recommandation : **B3/B4 ne construisent PAS le
Centre d'activité.** Le contrat d'événements (§10) reste la bonne interface à écrire dès
B3, mais sa consommation se limite à ce qui existe déjà — l'affichage dans le Fil et le
job de notification par courriel (`NotificationFilJob`, déjà branché sur
`EspaceMembership#notifie?` depuis le lot de préférences). Le Centre d'activité se branche
plus tard SANS toucher au modèle de données de B3 — exactement le même contrat de
non-duplication que `Carte`/`ContexteDeFil` prouvent déjà pouvoir tenir.

**Les capacités `proposer` / `ouvrir_decision` / `creer_action` (§5) n'existent pas comme
droits granulaires**, et ne devraient pas être construites comme telles : le code
n'a, nulle part, de table de permissions — le patron constant est rôle + mandat
(`EspaceMembership::ROLES` = `participant`/`gardien`, plus le mandat de modération).
Construire une matrice de capacités serait la première exception à ce patron, sans
qu'aucun besoin réel ne le justifie encore. Recommandation pour l'arbitrage §13.1 :
`proposer` = tout membre actif de l'espace ; `ouvrir_decision` = gardien ou mandat
explicite — deux vérifications qui existent déjà ailleurs dans le code, pas un nouveau
concept.

## 3. Une question que la spec ne pose pas — à ajouter à l'arbitrage §13

`Espace` a trois gabarits : `cercle`, `groupe`, `echange` (à deux, DM). La spec ne dit pas
si Proposition/Décision s'appliquent aux trois ou seulement au Cercle — une Décision dans
un échange à deux n'a pas de sens (pas d'électorat à distinguer du consentement mutuel
ordinaire), et une Proposition dans un groupe informel de douze est ambiguë (gouvernance
de fait sans gardien nommé). **Recommandation : réserver Décision et le protocole de
consentement au gabarit `cercle` en V1 ; Proposition et Action restent ouvertes aux trois
— une Action peut naître d'un échange à deux sans qu'il y ait de Décision derrière.** À
confirmer avec Boris en même temps que les quatre points du §13.

## 4. Conclusion pour le déblocage de B3

Rien dans la spec n'entre en contradiction avec l'architecture existante — c'est même
l'inverse : trois de ses mécanismes centraux (droits, cartes, mandat) sont déjà des
primitifs éprouvés que B3 doit réutiliser tels quels, pas redéfinir. Le seul vrai
préalable technique est l'intention du fil, absente de la base. Une fois les quatre points
du §13 tranchés par Boris (plus le gabarit du §3 ci-dessus), B3 est ouvrable.

## Références

- [Spécification Proposition/Décision/Action](messagerie-proposition-decision-action-specification.md)
- `app/models/contexte_de_fil.rb`, `app/models/carte.rb`, `app/models/reaction_semantique.rb`,
  `app/models/espace.rb`, `app/models/espace_membership.rb` (`pointzero-app`, branche `preprod`)
- [Registre des impacts fonctionnels](impacts-fonctionnels.md), F21
- [Plan de développement général](plan-developpement-general.md), §4
