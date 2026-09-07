# Supprimer son compte — analyse d'impact

*Poste fixe, 7 septembre 2026. Mesuré sur `pointzero-app`, branche `preprod`.*

**Ce document mesure d'abord, décide ensuite.** Les sections qui suivent constatent ce qu'une
suppression casserait aujourd'hui ; la dernière — [« La décision est prise »](#la-décision-est-prise--anonymiser-pas-effacer)
— porte l'arbitrage de Boris du 7 septembre et sa traduction champ par champ. L'implémentation —
modèles, migrations, service — est au portable ; la page et le parcours sont au poste fixe.

⚠️ **Lire l'arbitrage avant d'agir sur l'analyse** : il rend une grande partie des obstacles
ci-dessous sans objet, parce que rien n'est plus supprimé.

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

---

# La décision est prise — anonymiser, pas effacer

*Arbitrage de Boris, 7 septembre 2026 : « Anonymisé, pas effacé, c'est par ailleurs nécessaire
pour garder des statistiques. »*

## Ce que la décision change, et c'est considérable

**La ligne `users` survit.** Donc rien n'est supprimé, donc :

- les **33 contraintes bloquantes ne se déclenchent jamais** ;
- les **21 clés étrangères sans `on_delete`** deviennent sans objet ;
- les 14 `dependent: :destroy` ne s'exécutent pas non plus — plus de risque d'échec **partiel** ;
- les deux cas de **succession** (`espace`, `circle`) cessent d'être bloquants : le gardien reste
  gardien, sous un nom neutre. ⓘ Une passation reste souhaitable, mais elle n'est plus un
  préalable technique.

Le chantier passe de « démonter 39 dépendances » à « neutraliser des champs ». C'est plus petit,
plus sûr, et réversible tant que rien n'est écrit.

⚠️ **En échange, la promesse faite à la personne change.** On ne peut plus écrire « vos données
sont effacées ». La page devra dire ce qui se passe vraiment : le compte est fermé, l'identité
retirée, les contributions restent sous un nom neutre. C'est plus long à écrire et c'est plus
honnête.

⚠️ **Et « anonymisé » n'est pas un mot libre.** Une donnée réellement anonyme sort du champ des
données personnelles — c'est ce qui autorise à la garder pour des statistiques. Une donnée dont le
lien est seulement rompu, mais qui reste rattachable, est **pseudonymisée** et reste dans le champ.
La différence ne se décrète pas dans la page, elle se gagne champ par champ ci-dessous.

## `users` — ce qui est neutralisé

| champ | devient | pourquoi ce n'est pas `nil` |
|---|---|---|
| `email` | `anonyme-<id>@comptes-clos.invalid` | ⚠️ index **UNIQUE** et `null: false`. Ni vide ni nul. `.invalid` est réservé par la RFC 2606 : aucune adresse réelle ne peut collisionner |
| `prenom` | `Membre` | ⚠️ **`validates :prenom, presence: true`** — à `nil`, la ligne devient invalide POUR TOUJOURS et plus aucun `save` ne passe |
| `encrypted_password` | aléatoire, non conservé | interdit toute reconnexion |
| `nom` · `slug` | `nil` | `slug` est unique mais `allow_nil` ; il sert l'URL du profil public |
| `photo_televersee` | pièce jointe **purgée** | un visage identifie plus sûrement qu'un nom |
| `liens_externes` | `nil` | un profil externe ramène à la personne |
| `centres_interet` · `ce_qui_mamene` · `ce_que_je_cherche` · `ce_que_je_rends_possible` | `nil` | texte libre : la ré-identification s'y loge |
| `current_sign_in_ip` · `last_sign_in_ip` | `nil` | une adresse IP est une donnée personnelle |
| `reset_password_token` · `confirmation_token` · `jeton_de_session` | `nil` | trois index uniques, et autant de portes |
| `canal_prefere` · `politique_contact` · `accepte_appels` · `preference_rencontre` | valeurs par défaut | il n'y a plus personne à joindre |
| `anonymise_le` | horodatage | ⚠️ **colonne à créer** : sans elle, l'état n'est ni vérifiable, ni opposable, ni assertable par un banc |

## `users` — ce qui reste, et c'est la statistique

`role` · `annee_entree` · `heros_slug` · les drapeaux de visibilité et de badges · `sign_in_count`
et les dates de connexion · `moderation` — et **tout ce qui pend de l'utilisateur** : traces,
points, assessments, parcours, communautés, contributions anonymisées.

C'est exactement la matière dont les statistiques ont besoin, et plus rien n'y désigne quelqu'un.

## ⚠️ Le cas qui ne se règle pas ici : `registrations`

La table porte `email` **non nul**, `prenom` et `nom` **sur sa propre ligne**. La neutralisation de
`users` ne l'atteint pas.

Et on ne peut pas simplement la vider : la même ligne porte `montant_centimes`,
`stripe_payment_intent` et `rembourse_le` — une **pièce comptable**, dont la conservation
n'obéit pas au même régime que les données de profil.

**C'est le seul point où la décision « anonymiser » ne suffit pas à trancher**, parce que deux
obligations s'y opposent. ⚠️ Je ne fixe ni délai de conservation ni règle comptable : ce n'est ni
ma zone ni mon métier. Ce qu'il faut décider, en une phrase : *l'identité de l'acheteur est-elle
une mention obligatoire de la pièce, ou peut-elle être remplacée par la référence du billet ?*
La réponse détermine si la page peut promettre l'anonymisation **complète** ou seulement celle du
profil.

## La limite honnête de l'exercice

⚠️ **Sur une population petite, l'anonymat n'est pas garanti par le retrait du nom.** Une année
d'entrée rare, un héros peu choisi et deux ou trois traces datées peuvent suffire à reconnaître
quelqu'un dans un groupe de quelques centaines. C'est une limite structurelle de l'anonymisation,
pas un défaut d'implémentation — elle mérite d'être connue avant d'être écrite dans une page, et
elle plaide pour ne publier des statistiques qu'agrégées.

## Ce qu'il reste à faire, dans l'ordre

1. **Trancher `registrations`** (Boris) — c'est le seul verrou restant sur le texte de la page.
2. **La migration `anonymise_le` et le service d'anonymisation** (portable), transactionnel, avec
   la purge de la pièce jointe.
3. **La page et le parcours** (poste fixe), qui diront la vraie promesse.
4. **Le banc**, dans les deux sens : que l'identité a bien disparu — les onze champs ci-dessus —
   **et** que les contributions partagées sont toujours là, sous leur nom neutre. ⚠️ Un banc qui ne
   vérifierait que le premier sens serait vert sur une base vidée par erreur.
