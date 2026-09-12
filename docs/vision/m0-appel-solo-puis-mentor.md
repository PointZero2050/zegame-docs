# M0 — Formuler son Appel, puis rencontrer son mentor

Note Codex — décision de Boris du 12 septembre 2026 : séparation proposée validée, avec maintien explicite de l’ordre de dévoilement des Puissances. Destinataire principal : Claude desktop ; raccord métier : Claude portable.

## Décision à appliquer

Conserver l’ordre, les identifiants et les slugs des expériences :

1. E6 `et-moi-dans-tout-ca` : **faire émerger son Appel seul**, à partir des Traces, puis planter sa Graine de l’Appel.
2. E7 `choisir-qui-marchera-a-mes-cotes` : **choisir son mentor, puis ouvrir un premier échange à partir de cette Graine**.

E6 ne demande plus de mentor choisi ni de dialogue préalable. E7 garde la première rencontre et le premier échange. Préserver le dévoilement Imagination puis Émotion, et toutes les autres portes du M0. Ne pas intervertir les expériences ni avancer l’éveil d’Émotion. Les Graine et échange sont deux réalisations distinctes, pas deux confirmations d’une même action.

## E6 — texte cible à porter

Titre inchangé : « Et moi dans tout ça ? ». Modalité : « Solo ». Conserver les trois rangs, les durées existantes 4 / 11 / 5 minutes et le barème actuel 6 Ω : cette décision ne les révise pas.

| Champ | Rang 1 | Rang 2 | Rang 3 |
|---|---|---|---|
| verbe | Relire | Formuler | Semer |
| libellé | les Traces | ton Appel | la Graine de l’Appel |
| titre | Rassemble ce que l’époque a réveillé | Qu’est-ce qui t’appelle ? | La Graine de l’Appel |
| accroche | Tes Traces commencent à former une direction. | Donne une première forme à ce qui cherche à bouger. | Écris la phrase qui te met en mouvement. |
| CTA | Relire mes Traces | Formuler mon Appel | Planter ma Graine de l’Appel |
| confirmation | J’ai choisi les Traces à reprendre | J’ai formulé mon Appel | J’ai planté ma Graine de l’Appel |
| revoir | Relire tes Traces | Revoir ton Appel | Relire ta Graine de l’Appel |

**Explication rang 1 :** « Relis les choix, miroirs et hypothèses produits depuis le début du parcours. Repère ce qui continue de vibrer ou de résister. »

**Explication rang 2 :** « À partir de tes Traces, formule ce que tu souhaites quitter, ce que tu veux préserver et ce que tu aimerais explorer. Quelques mots suffisent pour faire apparaître une direction. »

**Explication rang 3 :** « Relis ce que tu viens de formuler et plante ta Graine de l’Appel dans la Fresque. Elle pourra évoluer au fil de tes rencontres. »

**Sorties/reconnaissances :** rang 1 : Traces repérées pour formuler l’Appel / « Repère les Traces que tu souhaites reprendre dans ta Graine. » ; rang 2 : première formulation de l’Appel / « Formule ce que tu souhaites explorer à partir de tes Traces. » ; rang 3 : Graine enregistrée dans la Fresque / « Enregistre ta Graine de l’Appel dans la Fresque. »

Remplacer aussi « Un premier récit de soi, tenu par le mentor » par « Un premier récit de soi à partir de ses Traces ». Retirer les mentions d’un échange préalable et d’une proposition née du dialogue, y compris dans les aides et confirmations/revoir récemment livrés (#210/#220). Ne pas retirer les dialogues avec le mentor des expériences ultérieures, notamment E13.

## E7 — conserver la rencontre, préciser son point de départ

Les deux étapes restent : choisir le mentor ; lui poser une première question sur la Graine de l’Appel. Rang 2, explication proposée : « Retrouve ta Graine de l’Appel et adresse une première question au mentor que tu as choisi. Ce premier échange ouvre un regard sur ce que tu viens de formuler. »

Conserver les preuves distinctes du choix, de la question envoyée et de la réponse reçue, ainsi que l’état « réponse attendue ». Le gain et l’éveil d’Émotion ne doivent pas être anticipés au simple affichage de la page ou au choix seul. Aucun changement du barème de 4 Ω dans ce lot.

## Raccord indispensable — portable

Le code lu avant la décision n’est pas seulement redondant dans ses textes : le YAML E6 porte `validation_authority: mentor`, `SequenceDeGestes::GESTES_DE_MENTOR` associe E6 au rang 2 et `porte_du_mentor` ouvre `/heros` ou la fiche du mentor choisi. Les changer visuellement sans modifier ces dépendances laisserait le mauvais parcours actif.

1. Retirer **E6 seulement** du routage vers le mentor ; garder E13. Relever toutes les conditions métier et données de validation E6 qui exigent le mentor. Aligner la configuration de référence et la donnée effective après analyse d’impact.
2. Donner au rang 2 une surface réelle de formulation, accessible avant l’éveil d’Imagination. Réutiliser la préparation de Graine existante si elle peut garder le texte jusqu’au rang 3. Aucune création automatique de Graine ni publication au rang 2. Si la surface n’existe pas, fournir la porte au desktop ; ne pas laisser « Formuler mon Appel » ouvrir un mentor ou une page inexistante.
3. Préciser le statut de cette formulation : si elle est enregistrée, lire cette preuve ; sinon ne pas annoncer un texte sauvegardé. Le libellé « Revoir ton Appel » exige que la formulation soit effectivement retrouvable. Ne pas fabriquer une preuve d’écriture à partir d’une visite.
4. Conserver le rang 3 comme Graine réellement enregistrée, avec les règles de visibilité existantes. La validation E6 et l’éveil d’Imagination doivent être possibles **sans mentor**, puis E7 ouvre le choix et le dialogue qui conduisent à Émotion. Ne pas substituer une simple confirmation à la Graine réelle.
5. Ne pas remettre à zéro les joueurs existants, leurs Graines, leurs échanges, leurs validations ou leurs Ω. Une ancienne réalisation avec mentor reste acquise. Un joueur en cours peut poursuivre dans la nouvelle séquence sans perte de production. Pas de re-crédit ni de nouveau reçu pour une expérience déjà validée.

Desktop porte les contenus, la surface existante et les états. Portable traite services, routes, autorités, données et tests métier. Une seule livraison coordonnée doit rendre les textes et les portes cohérents.

## Recette attendue

- Compte M0 arrivant à E6 sans mentor : Traces accessibles, formulation puis Graine conservée ; aucun détour vers `/heros` avant E7.
- Avant/après E6 : ordre de dévoilement inchangé ; Imagination s’ouvre au fait prévu, Émotion reste fermée.
- E7 : Graine E6 retrouvable ; choix puis question ; attente de réponse correctement affichée ; aucune validation anticipée.
- Joueur déjà engagé : Graine et échanges antérieurs conservés ; aucune régression de validation, de portes ou d’Ω.
- Consultation/reprise : formulation et Graine retrouvables ; texte saisi non perdu entre rangs 2 et 3 ; pas de gain en double.
- Vérifier les aides, fiche, boutons `confirmation`/`revoir`, preuve affichée, fin de séquence et reçu Omégas ; E13 conserve son dialogue avec le mentor.

Décision de produit validée par Boris ; ce document transmet le travail à faire. Aucun changement de base, de validation ou déploiement effectué par Codex dans cette transmission.
