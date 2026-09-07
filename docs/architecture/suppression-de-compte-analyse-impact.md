# Supprimer son compte — analyse d'impact

*Poste fixe, 7 septembre 2026. Mesuré sur `pointzero-app`, branche `preprod`.*

**Ce document ne décide rien.** Il mesure ce qu'une suppression de compte casserait aujourd'hui,
propose un classement, et isole ce qui doit être arbitré par Boris. L'implémentation — modèles,
migrations, service — est au portable ; la page et le parcours sont au poste fixe.

## Pourquoi maintenant

Un parcours de suppression de compte est un **préalable de publication** sur les deux stores.
Il ne dépend d'aucune décision en attente sur les comptes développeurs : quel que soit le compte
retenu, il sera exigé. C'est le seul chantier du dossier « stores » qui puisse avancer tout de
suite.

## L'état mesuré

| | |
|---|---|
| Modèles qui pointent vers `User` | **53** |
| Couverts par un `dependent:` sur `User` | **14** |
| **Sans aucune association déclarée** | **39** |
| …dont en `belongs_to` **obligatoire** | **33** |
| Clés étrangères vers `users` **sans `on_delete`** | **21** |
| Parcours de suppression existant | **aucun** — ni route, ni service |
| Anonymisation existante | **aucune** |

⚠️ **Un `user.destroy` naïf échouerait sur la première des 33 contraintes.** Sans `on_delete`,
PostgreSQL applique `RESTRICT` : la ligne fille interdit la suppression du parent. C'est la
généralisation d'un piège déjà connu du projet — une `ReactionSemantique` bloque par clé étrangère
la suppression du message qu'elle vise.

⚠️ **Et l'échec serait PARTIEL, donc pire qu'un refus net.** Les 14 associations couvertes portent
`dependent: :destroy` ou `:delete_all` : elles s'exécutent AVANT que la contrainte ne rende la
main. Un essai raté détruirait les traces, les points et les assessments, puis s'arrêterait sur la
première contrainte — laissant un compte à moitié vidé, ni supprimé ni intact.

## ⚠️ Le piège qui n'est pas dans le modèle User

`registrations` porte **`email` (non nul), `prenom` et `nom` directement sur la ligne**, et son
`belongs_to :user` est `optional: true`.

**Supprimer le compte n'efface donc rien de l'identité sur les billets.** On annoncerait une
suppression en laissant nom, prénom et adresse sur chaque inscription passée. C'est exactement le
genre d'écart entre ce qu'une page promet et ce que la base fait.

Et il ne se règle pas en supprimant la ligne : elle porte `montant_centimes`,
`stripe_payment_intent`, `rembourse_le` — des **pièces comptables**. Il y a là une tension réelle
entre effacement et conservation légale. ⚠️ **Je ne tranche pas un délai de conservation**, ce
n'est ni ma zone ni mon métier : je signale que la question existe et qu'elle se pose AVANT
d'écrire la page.

## Classement proposé — à arbitrer, pas acquis

### Supprimer (12) — strictement personnel, personne d'autre n'en dépend

`confirmation_de_geste` · `consentement_llm` · `coupable_ideal_session` ·
`disponibilite_de_rencontre` · `experience_quiz_attempt` · `favori_de_ressource` ·
`partage_coordonnees` · `puissance_assessment` · `suspension_personnalisation` · `trace_sas` ·
`traversee` · `visibilite_de_trace`

### Anonymiser (20) — vit dans un espace partagé

`action_de_fil` · `consentement_de_decision` · `decision` · `espace_membership` ·
`graine_publiee` · `membre_equipe` · `mentor_message` · `messaging/threads_user` ·
`objection_de_decision` · `pact_source_version` · `partage_de_recit` · `proposition` ·
`proposition_de_graine` · `proposition_de_rencontre` · `reaction_de_message` ·
`reaction_semantique` · `ressource_de_lien` · `ressource_evaluation` · `sondage` ·
`vote_de_sondage`

⚠️ **Supprimer ces lignes abîmerait l'expérience des AUTRES**, pas celle du partant : une décision
sans son ouvreur, un sondage sans ses votes, un fil dont un message disparaît au milieu. Le droit
à l'effacement porte sur les données personnelles, pas sur le fil de discussion d'un collectif.
L'anonymisation — rompre le lien, garder la trace — est le compromis usuel.

### Succession, pas suppression (2)

`espace` (gardien) · `circle` (opener)

⚠️ **Ces deux-là ne sont pas des données, ce sont des RESPONSABILITÉS.** Un Espace sans gardien ou
un Cercle sans ouvreur n'est pas un orphelin de base, c'est un lieu partagé devenu ingouvernable.
Il faut une passation avant la suppression — ou l'interdire tant qu'elle n'a pas eu lieu.

### Conserver (2)

`registration` (comptable et Stripe) · `signalement` (trace de modération)

⚠️ Effacer un `signalement` avec son auteur effacerait aussi la **protection d'un tiers**. Le
signalé, lui, ne doit pas pouvoir faire disparaître le signalement en supprimant son compte.

### Neutraliser le lien (1)

`event_template` — `cree_par` est déjà `optional: true`, un `nullify` suffit.

### À trancher (2)

- **`blocage`** — A a bloqué B. Si A part, le blocage n'a plus d'objet. Mais si B part et revient
  sous un autre compte, la protection de A a disparu sans qu'elle le sache.
- **`demande_de_contact`** — les deux côtés sont obligatoires. Supprimer emporte la demande de
  l'autre personne ; anonymiser laisse une demande venue de nulle part.

## Ce que ça implique, dans l'ordre

1. **Une décision de politique** (Boris) : que promet-on exactement à qui demande la suppression ?
   « Effacé » et « anonymisé » ne sont pas la même promesse, et la page devra dire la vraie.
2. **Un service côté portable**, transactionnel, qui applique les cinq régimes dans le bon ordre —
   les anonymisations d'abord, les suppressions ensuite, la vérification des successions en
   préalable bloquant.
3. **Les 21 clés étrangères sans `on_delete`** : décider au cas par cas plutôt que d'ajouter un
   `cascade` global, qui ferait disparaître silencieusement du contenu partagé.
4. **La page et le parcours** (poste fixe), une fois le point 1 tranché.
5. **Un banc**, qui devra vérifier les DEUX sens : que le partant disparaît, et que ce qui
   appartient aux autres est toujours là.

## Ce que cette analyse NE prouve PAS

- ⚠️ Elle est **statique** : elle lit les modèles et les migrations, elle n'a supprimé aucun compte.
  Le comportement réel d'un `destroy` sur une base peuplée reste à mesurer sur un compte jetable.
- Elle ne couvre pas Active Storage (`photo_televersee`) ni les fichiers déposés en pièce jointe.
- Elle ne dit rien des données sorties de l'application : **Brevo** garde ses contacts, **Stripe**
  ses paiements. Une suppression côté PZ ne les touche pas — le rapprochement Brevo construit par
  le portable est le seul canal existant, et il lit, il ne pousse pas.
- ⚠️ Le classement en cinq régimes est **une proposition de lecture**, pas un arbitrage. Chaque
  ligne peut être déplacée, et deux d'entre elles attendent explicitement une décision.
