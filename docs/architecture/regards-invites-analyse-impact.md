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

## Ce que la production demandera

Rien n'y va sans le mot de Boris. Il faudra d'abord :
- la politique de confidentialité complétée : le regard, ce qu'il lit, Anthropic, les 30 jours de rétention ;
- le masquage d'un message d'IA ;
- ~~la décision sur l'ouverture au-delà des administrateurs~~ : tranchée le 20 octobre, les facilitateurs aussi ;
- l'accord ou l'information du groupe, le point « accord du groupe » de Codex.
