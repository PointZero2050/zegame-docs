# Regards invités — analyse d'impact (lot A, serveur)

> **Ajout Codex — arbitrage complémentaire de Boris, 20 octobre 2026.** Pour la
> production, Boris retient **l'accord explicite par fil**, en complément de
> l'annonce d'arrivée et de la suspension globale. Le lot A décrit ci-dessous
> reste le comportement de préprod et ne recueille pas cet accord. La déclinaison
> individuelle proposée, les clauses et les conditions de publication sont dans
> [la livraison éditoriale](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/confidentialite-sas-regards-2026-10-20.md). L'annonce seule ne suffit plus pour ouvrir
> la production. Aucun backend modifié par cette note.

> Demandée par Codex avant tout code (« la messagerie est une zone sensible »). Écrite par le portable le
> 20 octobre 2026, avec les arbitrages de Boris du même jour. Le contrat de vue est celui du poste fixe (#435,
> en préprod, inerte tant que le serveur ne sert rien).

## Ce qui est décidé

**Boris, 19 octobre** (plan validé avec le poste fixe) :
- **Où** : préprod seulement, derrière l'interrupteur `REGARDS_INVITES=1`.
- **Qui agit** : en V1, les administrateurs seuls invitent, sollicitent, mettent en pause et retirent.
- **Les voix** : les six mentors du Monde 0 (`Heros.monde_0`) ou l'Enfant Libre de l'inviteur
  (`ImmateriaE1.avatar_de`). Un seul regard de chaque genre par fil.
- **Ce qu'il lit** : depuis son arrivée, 8 messages humains au plus. Jamais un Récit, une mémoire privée ni un
  message d'IA.
- **La conduite** : une voix par message, et **jamais d'IA déclenchée par une IA**.

**Boris, 20 octobre** :
1. **Consentement** : le regard ne lit que les messages écrits **après l'annonce de son arrivée**, qui est
   visible de tous. Il ne lit **jamais** ceux d'un membre qui a suspendu l'IA dans sa personnalisation (la
   suspension « tout »).
2. **Notifications** : **aucun courriel** ni récapitulatif pour un message de regard. Il compte comme non lu pour
   les autres, pas pour qui l'a sollicité.
3. **L'Enfant devant le groupe** : son **nom** et son **caractère** seulement (apparence, ton de l'archétype),
   jamais le désir ni les réponses d'Immateria de l'inviteur.
4. **Plafond** : **20 sollicitations par fil et par jour**. Le plafond global (`PlafondLlm`, 20 $/jour) reste le
   dernier recours.
5. **Qui agit, élargi le soir même** : « Je vais étendre aux facilitateurs ». Les facilitateurs invitent,
   sollicitent, mettent en pause et retirent comme les administrateurs (`RegardInvite::HABILITES`, préprod
   `f83efc4`). Un joueur, non.

## Ce qu'un auteur non humain touche dans la messagerie

| Où | Le risque | Ce que fait le lot A |
|---|---|---|
| `NotificationFilJob#destinataires` | n'exclut l'auteur que s'il est un `User` : chaque réponse d'IA écrirait à tous, signée « Point Zéro t'a écrit » | le message de regard ne planifie aucun envoi |
| `DigestNotificationsJob` | le récapitulatif compte tout auteur non `User` | les messages de regard n'y entrent pas |
| Non-lus (`boite_d_echanges`, séparateur du fil) | un message d'IA est non lu pour tous, sollicitant compris | il reste non lu pour les autres ; le fil est marqué lu pour le sollicitant |
| `Engagements#mentions_non_lues` | un « @Prénom » écrit par l'IA deviendrait une tâche | les auteurs `RegardInvite` sont exclus |
| `includes(:author)` polymorphe (six lecteurs) | un `author_type` sans classe lève une erreur | le modèle arrive avec la migration et ne se renomme jamais |
| Modération (`mine?`, `Signalement` lié à un `User`) | un message d'IA n'est ni masquable ni signalable | V1 : l'administrateur retire le regard, et ses messages restent ; **à prévoir avant la production** |
| `scripts/nettoyer_canal.rb` | il supprimerait les messages d'IA comme orphelins | il les épargne |
| Suppression d'un compte, d'un fil | les clés étrangères des tables neuves | `dependent:` sur `User` et sur le fil ; `purge_de_compte` balaie déjà les clés vers `users` |
| `PlafondLlm.depense_du_jour` | il ne compte que trois tables | les tickets `RegardAppel` y entrent |
| Consentement (`ConsentementLlm`, `AutorisationLlm`, politique § 4.7-4.8, CGU art. 9) | rien ne couvre la lecture des messages d'AUTRES membres par une IA | arbitrage 1 ; **la politique est à compléter avant la production** (Codex) |
| La vie privée de l'inviteur | `AvatarReponse` met le désir du joueur dans son prompt | l'Enfant du groupe a sa propre consigne, sans `<faits>` (arbitrage 3) |

**Ce qui tient déjà** :
- le rendu des messages, avec les replis « — » / « · » et le profil seulement pour un `User` ;
- les réactions ;
- les Graines, déjà gardées par `author_type == "User"` ;
- l'export (`auteur_de` → « — »).

## Lot B — l'accord explicite par fil (préprod, `a8363ef`, 20 octobre au soir)

La règle de Codex, avec deux arbitrages de Boris : la **portée est le regard** (un autre personnage, ou le
même réinvité, demande un nouveau choix), et **personne ne voit les choix des autres** (le sollicitant voit
un nombre).

| Où | Ce que fait le lot B |
|---|---|
| `accords_de_regard` | Un journal qu'on ne réécrit jamais : `accorde`, `refuse`, `retire`, avec la date et la version de l'information. L'état est la dernière ligne. |
| `RegardInvite#messages_lisibles` | Seulement les membres dont l'accord est EN COURS, chacun après CET accord, sans les suspendus ; filtré en SQL avant la limite. Sans accord, rien. |
| `RegardReponse.solliciter` | La question passe la même porte (accord, suspension), par le formulaire comme par la @mention. La @mention n'est plus envoyée deux fois. |
| `AccordsDeRegardController` | Ouvert à tout lecteur du fil. Accorder exige un regard présent, un fil ouvert et la version montrée ; refuser et retirer passent toujours. |
| `FermetureDeCompte` | La fermeture vaut retrait ; les lignes restent, preuve sous le compte neutralisé. |

**Ce qui les efface** : la purge du compte, un fil détruit, ou le compte de l'inviteur purgé (le regard part,
et les accords des autres sur lui avec).

**Bancs** : `verifier_accords_regard` (35 assertions, avec la contre-épreuve `CONTRE_EPREUVE=1`, qui rougit
les §§ 1 à 6) et `verifier_regards`, dont le décor fait autoriser ses membres.

## Lot C — masquer et signaler la réponse d'un regard (préprod, `6a21280`, 20 octobre au soir)

**Arbitrages de Boris** :
- les facilitateurs et les administrateurs masquent, pour tous, sans rien effacer ;
- tout membre signale, et le signalement est une trace pour l'équipe ;
- les preuves d'accord sont gardées **tant que le fil existe** (déjà le comportement).

| Où | Ce que fait le lot C |
|---|---|
| `Messaging::Message#masquer!` | Le texte passe dans `texte_masque`, et `message` reste vide : le fil, l'export, la recherche et les aperçus ne montrent plus rien sans qu'on les touche. `retablir!` le remet. Seule une RÉPONSE de regard se masque. |
| `Signalement` | Il vise un membre OU un regard, et garde le sollicitant (via le ticket `RegardAppel`, qui pointe sa réponse). |
| `MessagesDeRegardController` | Masquer et rétablir (`RegardInvite.moderateur?`, sans l'interrupteur) ; signaler (tout lecteur). |
| Migration | Clés neuves en `on_delete: :nullify` : un compte purgé ou un fil détruit ne bloque rien. |

**Banc** : `verifier_moderation_regards` (18 assertions). Chaque « rien ne fuit » y est mesuré avant le
masquage.

## Ce que la production demandera

> Note Codex — relecture éditoriale du 20 octobre, après le lot C.

Rien n'y va sans le mot de Boris. Restent :
- la politique Regards complétée par la modération et la conservation des preuves,
  prête dans [la livraison éditoriale](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/confidentialite-sas-regards-2026-10-20.md) ;
- les [compléments relus aux articles 9 et 15 des CGU](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/cgu-article-9-regards-invites-2026-10-20.md) ;
- le portage des vues de modération, puis leur recette avec les textes exacts.

Déjà tranchés et présents côté serveur : accord individuel par regard (lot B),
facilitateurs habilités avec les administrateurs, masquage et signalement (lot C),
preuves conservées tant que le fil existe, sauf suppression définitive du regard
ou purge d'un compte concerné. La fermeture du compte vaut retrait mais ne supprime
pas ces preuves. Le retrait d'un regard du fil n'est pas sa destruction en base.

Le formulaire d'accord versionné 2026-10-20 n'est pas modifié par cette relecture.
La mention à porter pour tous est **Réponse du regard masquée.** Le microtexte
contre la copie des propos d'autrui dans la question reste celui de #439.
