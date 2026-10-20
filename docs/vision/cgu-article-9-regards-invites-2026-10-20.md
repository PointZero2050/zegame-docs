# CGU articles 9 et 15 pour les regards invités

> Proposition du poste fixe (Claude), relue et corrigée par Codex le 20 octobre
> 2026 à partir du serveur de préprod `6a212809` et des arbitrages transmis par le
> portable. Ces ajouts ne sont pas publiés. Leur intégration attend la recette des
> vues et l'autorisation de Boris avant toute production des regards.

La [politique de confidentialité préparée par Codex](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/confidentialite-sas-regards-2026-10-20.md)
porte les données transmises, le destinataire, les durées et les droits.
Les présents ajouts portent les règles d'usage et la modération. Conserver
l'article 9 actuel et ajouter son complément ci-dessous, puis compléter
l'article 15. Les autres clauses restent inchangées.

## Texte public à ajouter à la fin de l'article 9

Dans les espaces d'échange, un facilitateur ou un administrateur habilité peut
inviter un **regard** : un mentor ou l'Enfant Libre d'un membre, animé par un
système d'intelligence artificielle. Son arrivée est annoncée dans le fil avec
son identité, sa mission et la personne qui l'a invité. Ses interventions sont
identifiées comme produites par une IA. Il répond uniquement sur sollicitation
d'une personne habilitée ; ses réponses sont visibles par les lecteurs du fil.

Le regard ne lit les messages d'un membre que si ce membre l'a explicitement
autorisé pour ce regard dans ce fil. Ni l'accord d'un autre membre, ni celui donné
à un autre regard ou dans un autre fil, ni le fait de continuer à écrire ne
valent autorisation. Les messages retenus sont postérieurs à l'arrivée du regard
et à l'accord en cours de leur auteur. Une nouvelle invitation ou une nouvelle
mission demande un nouveau choix.

Le Joueur peut refuser ou retirer son accord à tout moment sans perdre l'accès à
la conversation. La suspension globale de l'IA exclut également ses messages.
Les choix individuels ne sont pas montrés aux autres membres ; la personne qui
sollicite le regard voit seulement un nombre de membres l'ayant autorisé. Les
données transmises et leur conservation sont décrites dans la politique de
confidentialité.

Le Joueur qui sollicite un regard ne recopie pas dans sa demande les propos ou
les données personnelles d'un autre membre sans son accord. Les autorisations
accordées pour personnaliser un mentor individuel ne sont pas transférées au
regard du groupe. L'Enfant Libre invité ne reçoit ni le désir ni les réponses
d'Immateria de la personne qui l'a invité.

Les réponses d'un regard peuvent être inexactes. Elles ne décident pas pour le
groupe et ne remplacent ni une décision collective, ni l'intervention d'un
facilitateur, ni un avis professionnel. Elles peuvent être signalées ou masquées
selon l'article 15.

## Texte public à ajouter dans l'article 15 après le premier paragraphe

Tout lecteur d'un fil peut signaler la réponse d'un regard invité. Le signalement
est transmis à l'équipe sans masquer automatiquement la réponse. Un facilitateur
ou un administrateur habilité peut la masquer pour tous les lecteurs : une mention
remplace alors son texte. Le texte reste conservé à part pour l'examen d'un
signalement ou d'un litige ; cette mesure n'est pas un effacement. Une personne
habilitée peut rétablir la réponse. Les règles de conservation et les droits
applicables sont précisés dans la politique de confidentialité.

## Relecture et consignes de publication

- **Portée corrigée** : la sollicitation est réservée à une personne habilitée,
  facilitateur ou administrateur, et l'accord vise un regard dans un fil.
- **Responsabilité** : la formule initiale « n'engagent ni le groupe ni Point Zéro »
  est remplacée par la limite précise « ne décident pas pour le groupe ». Le texte
  ne doit pas devenir une exclusion générale de responsabilité du Service.
- **Modération** : le serveur du lot C existe ; les vues et la recette restent à
  vérifier. Signaler ne masque pas. Masquer conserve le texte à part et permet
  le rétablissement ; ne jamais afficher « supprimé » pour ce geste.
- **Preuves** : leur durée appartient à la politique, pas à une nouvelle durée
  inventée dans les CGU. La fermeture du compte vaut retrait, sans effacement de
  la preuve conservée tant que le fil existe, sous réserve des suppressions
  définitives prévues par le serveur.
- **Microtexte de sollicitation** : conserver celui déjà porté en #439 :
  « Ne recopie pas dans ta question les propos ou les données personnelles d'un
  autre membre sans son accord. »
- **Texte d'accord versionné** : aucune modification du bloc « Autoriser ce regard
  dans ce fil ? » ; ne pas changer `VERSION_INFORMATION` pour cette seule relecture.
- **Version et date** : préparer la prochaine version des CGU et de la politique
  avec leur date effective, à fixer à publication ; garder les notes internes hors
  des articles publics. La proposition reste soumise à la recette et au mot de
  Boris pour la production.

Sources relues : `content/legal/cgu.md` (articles 9 et 15),
`app/models/accord_de_regard.rb`, `app/models/regard_invite.rb`,
`app/controllers/messages_de_regard_controller.rb` et `Messaging::Message`,
préprod `6a212809`. Les références CNIL et Anthropic sont jointes à la politique
préparée ci-dessus. Cette relecture éditoriale n'est pas une certification de
conformité juridique ni une recette du déploiement.
