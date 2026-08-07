# Lots conçus avec Codex — ce qui est fait, ce qui reste

> Relevé par Claude (portable) le 2026-08-06, à la demande de Boris. Croise **les
> spécifications de Codex** dans ce dépôt avec **l'état vérifié du code et de la base de
> production**. Là où les deux divergent, le code fait foi.
>
> Méthode : chaque ligne « fait / — » est mesurée par introspection de la base et du code, pas
> déduite d'un document. Le script est en scratchpad ; les chiffres datent du 2026-08-06.

## 1. Ce qui est en ligne

| Chantier | État mesuré |
|---|---|
| Cercles — tables du lot 1 | Les cinq existent (`circles`, `circle_cycles`, `circle_memberships`, `pact_source_versions`, `circle_sessions`) · 1 cercle réel |
| Rôles tournants | Colonne `roles` sur `circle_sessions` |
| Profil communautaire | Annuaire `/profils` + fiche · territoire, présentation, langues, disponibilité |
| Messagerie | `Messaging::Thread` polymorphe · 69 fils sur `CircleMembership`, `JourneysUser`, `ChallengesUser` · non-lus (`last_seen_at`) |
| Blocage / signalement | `Blocage` et `Signalement` |
| Graines | Publication / dépublication depuis un message |
| Ressourcerie V1 | Deux corpus servis depuis YAML · évaluation par les cinq cadres |
| Monde 1 | Parcours Boussole · 6 expériences |
| Cartes-couvertures | Le gabarit existe — **2 couvertures sur 23** |

## 2. Messagerie et profil — l'écart avec la spécification V1

La spécification est
[profil-communautaire-messagerie-cercles-v1.md](profil-communautaire-messagerie-cercles-v1.md).
L'infrastructure est là ; ce qui manque est la **matière de la rencontre**.

### 2.1. Le dossier de rencontre · **LIVRÉ le 2026-08-06**

Les quatorze champs de la spécification, en jsonb sur `circle_memberships`. Quatre sont ordonnés
et comparables — cadence, présence, intensité, confrontation — et le Cercle déclare les siens sur
les mêmes dimensions, ce qui rend la restitution possible.

La restitution est bornée comme la spécification l'exige : « Cadence compatible · Présentiel à
organiser · Intensité proche · Attentes de confrontation à discuter ». Jamais un pourcentage,
jamais « profil complémentaire » ou « niveau insuffisant », jamais de recommandation d'accepter
ou de refuser. Trois états seulement : ce qui concorde, ce qui demande un arrangement pratique,
ce qui demande une conversation.

Visibilité : le candidat, l'ouvreur, un administrateur — et un membre actif **seulement** si le
candidat y a consenti. La règle vit désormais sur `CircleMembership#visible_par?`, et
`Messaging::Thread` y délègue : une seule source pour deux surfaces.

Un dossier vide reste une candidature recevable.

### 2.2. Notification par courriel (§ 5.2) · **LIVRÉ le 2026-08-06**

`NotificationFilJob` part dix minutes après le message : une conversation vivante ne produit pas
un courriel par réplique. L'auteur ne se notifie pas, qui a lu n'est pas notifié, qui s'est
désabonné non plus, et un accès révoqué entre le message et l'envoi ne produit rien.

Le courriel porte l'identité d'usage de l'expéditeur, la nature de l'échange, le contexte, un lien
profond et le réglage des notifications. **Jamais** le texte du message, l'adresse d'un tiers ou
le nom complet de l'expéditeur ; aucune réponse par courriel.

À noter pour la mémoire du projet : `mathieu_core_messaging` esquissait le mécanisme côté vibe
(débounce de 10 minutes) puis appelait `GlobalSettings.send_mail_notif_for_thread`, **une méthode
jamais définie**. L'envoi n'a donc jamais existé nulle part.

### 2.3. Le partage de coordonnées (§ 5.1) · **LIVRÉ le 2026-08-07**

**Une fuite était en production** : la page d'un Cercle affichait l'adresse et le téléphone de
chaque candidat à l'ouvreur, sans consentement, pour toute demande en attente. L'annuaire et la
fiche de profil s'en gardaient déjà explicitement ; c'était un vestige du cadrage F11 initial, où
la décision se prenait hors application par téléphone. Refermée.

Deux niveaux, volontairement séparés. Une **politique** sur le compte — contact dans
l'application, e-mail sur demande, téléphone après mise en relation — plus un canal préféré et
l'acceptation ou non des appels. Et un **partage explicite par contexte** : ce fil-ci, ce
Cercle-ci. La politique n'expose jamais rien à elle seule ; seul un partage le fait.

`CarteDeContact` pose les deux questions dans l'ordre : le lecteur a-t-il sa place dans ce
contexte, puis la personne y a-t-elle consenti. Un administrateur n'est pas admis d'office — la
spécification ne prévoit aucune exception pour des coordonnées personnelles.

La révocation vaut pour les accès futurs, et l'interface le dit sans farder : ce qu'un
destinataire a déjà noté reste chez lui.

### 2.4. Le profil détaillé (§ 3.2) · **LIVRÉ le 2026-08-07**

Année d'entrée dans le Jeu, liens externes, préférence de rencontre (présence / distance /
hybride), centres d'intérêt, et les trois questions de « Me rencontrer » — ce qui m'amène au Point
Zéro, ce que je cherche maintenant, ce que j'aimerais rendre possible. La politique de contact,
déjà en base, s'y lit désormais.

Le rôle d'appel était déjà là sous sa forme provisoire (`role_appel_provisoire`, dérivé de la
posture du Conseil Oméga — décision Boris du 2026-08-01).

**Les liens externes sont la seule donnée du profil qui puisse devenir un vecteur d'attaque** :
des URL saisies par une personne, rendues cliquables pour d'autres. `LiensExternes` ne retient que
`http`/`https` — `javascript:` et `data:` sont des schémas valides, et un lien cliquable qui les
porte exécute du code chez celui qui clique —, plafonne à dix, et le rendu porte
`rel="noopener noreferrer nofollow"` en n'affichant que le domaine.

**Reste du § 3** : les badges et contributions épinglés de la carte d'annuaire (§ 3.1). Aucun
modèle de badge n'existe ; l'épinglage porterait sur les Graines publiées — à trancher plutôt qu'à
deviner.

### 2.5. Reste du § 6

Proposition de rencontre (créneaux ou lien), carte de contact partagée, prévention d'une nouvelle
sollicitation par la même personne.

### 2.6. Refactor annoncé par Codex (§ 8.1) · **LIVRÉ le 2026-08-07**

`ContexteDeFil` : une classe par conteneur — `Experience`, `Parcours`, `Candidature`, et
`Inconnu` pour un fil dont le conteneur a disparu. Titre, retour, badge, participants et règle
d'accès y vivent. Ajouter un contexte, c'est ajouter une sous-classe et une ligne de route.

**Le refactor a révélé une route manquante** : cinq fils rattachés à un `JourneysUser` existaient
en base depuis la migration zegame, sans qu'aucune URL n'y mène — le contrôleur porté ne
connaissait que deux conteneurs sur trois. Ils sont de nouveau accessibles.

Le rendu d'un retour d'expérience et celui d'une mise en relation sont désormais distincts : seule
la seconde affiche des coordonnées, et le statut de la candidature se lit dans un badge **hors** du
fil — un message n'est jamais un état métier.

**Un fil orphelin subsiste en production** : le fil 47 porte 3 messages et 7 participants alors
que son `ChallengesUser` n'existe plus. Il est rendu inerte et lisible par personne, mais **non
détruit** : c'est du contenu, sa suppression est une décision de Boris. La cause — pas de
`dependent: :destroy` entre `ChallengesUser` et son fil — est laissée en l'état volontairement :
l'ajouter détruirait du contenu, y compris de possibles Graines.

## 3. Le « 100 Ω » — tranché le 2026-07-31, et déjà implémenté

**Ce point est clos** ; une première version de ce document le présentait à tort comme ouvert.

Boris a tranché le 2026-07-31 pour le critère structurel, et il est en production dans
`app/services/mondes.rb` + `config/mondes.yml` : le passage d'un Monde au suivant vérifie que les
**parcours obligatoires** de la communauté prérequise sont accomplis. Aucun seuil d'Oméga
n'intervient nulle part dans le verrou.

Vérifié sur la production le 2026-08-06 : le prérequis du Monde 1 est le parcours obligatoire
« Point Zéro - Monde 0 », ses 12 expériences requises incluent **« Vivre l'Atelier Point Zéro »**,
dont l'autorité de validation est `facilitateur`. Six joueurs sur vingt ont le Monde 1 ouvert.

L'Oméga reste un indicateur indépendant de la progression, conformément à la décision.

Ce qui subsiste du sujet est purement documentaire : plusieurs specs mentionnent encore
« les 100 premiers Oméga » comme marqueur de passage. À corriger dans les documents concernés
quand on les rouvrira.

### 3.1. Le point réellement ouvert : l'Atelier au Festival

Le Monde 1 exige « Vivre l'Atelier Point Zéro », validé par un facilitateur. Cette expérience
n'est **pas** rattachée au parcours « Festival 2026 — la journée ».

Si l'intention est que les participants du 1er octobre puissent poursuivre vers le Monde 1, il
faut décider comment leur journée valide cet Atelier : soit l'expérience est ajoutée au parcours
du jour, soit un facilitateur valide en masse depuis la console. Quatre facilitateurs et sept
administrateurs peuvent valider — pour deux cents participants, la validation en masse par
créneau (déjà construite, tranche 3 du mode événement) est le seul chemin praticable.

**Décision attendue de Boris.**

## 4. Les deux barèmes Ω · **RÉSOLU le 2026-08-06**

Deux barèmes coexistaient sans que rien ne le signale : `challenges_skills` créditait réellement
le joueur, tandis que `challenges.point` — le champ « Ω à la validation » de la console — n'avait
aucun effet. Quinze expériences sur vingt-trois divergeaient.

Le champ trompeur est retiré du formulaire, qui affiche désormais `total_point`, la somme de la
ventilation par compétence. Le paramètre n'est plus accepté en écriture. La colonne reste en base
par fidélité à la migration zegame ; elle n'est plus lue nulle part.

## 5. Les autres lots, par ordre de dépendance

### Cercles, lots 2 à 5 ([spécification § 16](cercles-croissance-profils-flow-omega.md))

- **Lot 2 — Passage et cycle Monde 2** : journée de l'Intention souveraine, contrat individuel,
  cycle annuel, Pacte-Source complet, clôture et lignées, cagnotte **après cadrage juridique**.
- **Lot 3 — Profils et 360°** : profil de Cercle, cinq cadres, évaluations mi-cycle et fin de
  cycle, quatre regards.
- **Lot 4 — Héros et Freeride** : catalogue des figures inspirantes par puissance, mentor IA.
- **Lot 5 — Oméga avancé** : trois piliers, Contributions, missions, Cercle de redistribution,
  decay annuel.

Aucun modèle `Contribution`, `Mission`, `Resonance` ni `World` n'existe.

### Reste du lot 1, non livré

Traversée collaborative de l'Intercycle et parcours d'autofacilitation : aucun parcours ne porte
ces noms. C'est du contenu pédagogique autant que du code.

### Ressourcerie V2 et marketplace ([spécification](ressourcerie-marketplace.md))

Œuvre pédagogique versionnée avec droits et clés de redistribution, profils de
facilitateurs-designers, studio de création, séparation des économies. **Exige une revue juridique
avant toute ligne de code** — propriété intellectuelle, fiscalité, paiement, responsabilité.

### Monde 1 — catalogue

1 parcours sur les 12-14 visés par [monde-1-parcours.md](monde-1-parcours.md).

### Chantiers de vision non commencés

[Monde-miroir](monde-miroir.md) (jumeau numérique, quatrième mur, Empire et Cité Cosmique),
[game design autosubversif](game-autosubversion.md) (combats par runes, symétrie générative),
[récit-fresque et quêtes collectives](relations-recits-collectifs.md),
[page parcours « carte du voyage »](page-parcours-carte-du-voyage.md).

## 6. Ce que je recommanderais pour août

La question qui devrait décider du programme n'est pas « quel lot est le plus mûr » mais
**« que trouvent deux cents personnes le 2 octobre ? »**

Le 1er octobre, deux cents participants reçoivent un compte, entrent au Monde 0 et font le
parcours du jour. Le lendemain, ce qui les attend est le Monde 1, donc les Cercles. Or il existe
aujourd'hui **un** Cercle, aucun dossier de candidature, et aucune notification par courriel :
une demande d'adhésion part et personne n'est prévenu. Le Festival produirait une cohorte qui
arrive dans une pièce vide.

### Fait le 2026-08-06

1. ~~La notification par courriel des fils~~ (§ 2.2) — livrée.
2. ~~Le dossier de rencontre~~ (§ 2.1) — livré.
3. ~~Une répétition de restauration~~ — faite : 45 tables, zéro divergence, le critère de feu vert
   du §7 est coché. Le script `scripts/repeter_restauration.sh` la rejoue quand on veut.
4. ~~Clarifier les deux barèmes Ω~~ (§ 4) — fait.

5. ~~Le partage de coordonnées~~ (§ 2.3) — livré le 7 août, avec la fermeture d'une fuite.

6. ~~Le refactor polymorphe des vues de fil~~ (§ 2.6) — livré le 7 août, avec la route oubliée
   des fils de parcours.

7. ~~Le profil détaillé~~ (§ 2.4) — livré le 7 août.

### Ce qui reste pour août

1. **Le § 6 restant** : proposition de rencontre (créneaux ou lien), et prévention d'une nouvelle
   sollicitation par la même personne. La carte de contact, elle, est faite.

### Décisions en attente de Boris

- **« Proposer un échange »** (§ 4.1). La spécification en fait l'un des deux déclencheurs de mise
  en relation, depuis un profil. Mais le § 6 reporte explicitement « la messagerie directe générale
  entre tous les membres », et le § 8 exige qu'un fil soit rattaché à un objet de demande. Un
  échange sans Cercle n'a donc pas d'objet auquel se rattacher : soit ce bouton est une invitation
  déguisée, soit il ouvre une messagerie que la V1 reporte. **Non construit faute d'arbitrage.**
- **Les badges épinglés** (§ 3.1) : sur quoi porte l'épinglage, faute de modèle de badge ?
- **Le fil orphelin 47** (§ 2.6) : 3 messages sans conteneur — conserver ou supprimer ?
- **Comment l'Atelier est validé pour les participants du Festival** (§ 3.1).

Et une décision à prendre tôt : **comment l'Atelier est validé pour les participants du
Festival** (§ 3.1).

Tout le reste — lots Cercles 2 à 5, marketplace, monde-miroir, catalogue Monde 1 — est postérieur
au Festival.
