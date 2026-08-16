# Le pont Trace → Graine, et le Miroir de la Fresque

*Écrit le 16 août 2026 par l'instance poste fixe, au portage de
`fresque-recit-m0-cible`. Destinataire : l'instance portable (modèles,
services, contrôleurs) et Boris pour l'arbitrage éditorial.*

## Le constat

La maquette de la Fresque et le code divergent sur ce qu'**est** une Graine.

| | Maquette | Code (`app/services/graine.rb`, vague C, 16 août) |
|---|---|---|
| Origine | le rituel des 4 questions | un message écrit dans le fil d'une expérience |
| Nature | un objet stocké, éditable | une **lecture**, sans table |
| Visibilité | propre à la Graine (`private` / `threshold`) | `GrainePubliee` (publication sur le profil) |

Ce n'est pas un manque technique : c'est une divergence d'identité. Le service
`Graine` a été écrit le matin même et pose la doctrine du dépôt — « un état se
lit, il ne se stocke pas ». La maquette, elle, suppose une table.

## Ce que la page fait aujourd'hui (livré, commit `39ce3a2`)

Le rituel crée une **Trace** (`territoire: "imagination"`,
`cle: "premiere-bifurcation"`), comme il le faisait déjà. La page affiche à
côté les **vraies** Graines via `Graine.pour`, sans les dupliquer. L'écran des
trois formulations du Miroir **n'est pas porté** : il compose une Graine, qui
ne naît pas de ce rituel.

Une tension de vocabulaire subsiste, signalée et non tranchée : le bouton dit
« Planter ma première Graine » — c'est le libellé de la maquette **et** celui
qu'asserte `verifier_v4_imagination` — alors qu'il crée une Trace.

## Ce qu'il reste à décider

1. **Le pont.** Une Trace de bifurcation doit-elle pouvoir devenir une Graine ?
   Si oui, par quel geste : le joueur choisit, ou la clôture de chapitre le
   propose ? Le doc d'onboarding §4 l'annonce sans le spécifier.
2. **Le vocabulaire.** Si le rituel ne produit pas de Graine, son bouton ne
   devrait pas le dire. Changer le libellé demande d'ajuster
   `verifier_v4_imagination` dans la même livraison.
3. **Le Miroir.** Arbitrage de Boris du 16 août : les trois formulations
   viendront d'un **appel au mentor** (LLM), cohérent avec le banc des
   personnages déjà arbitré sur Claude — et non d'un éditorial fixe, qui
   servirait les mêmes phrases à tous alors que la maquette les présente comme
   un reflet des réponses du joueur. Reste à spécifier : quel prompt, quel
   garde-fou (aucun score de qualité n'est attribué au texte — décision
   explicite des NOTES de la maquette), et que faire en cas d'indisponibilité.
4. **Les Résonances.** Aucune donnée aujourd'hui. La page annonce l'horizon
   sans rien compter ; elles dépendent de l'ouverture de l'Espace du Seuil,
   elle-même liée à la Communication.

## Ce qui est déjà là et ne demande rien

Les quatre questions (`config/ressources/premiere_bifurcation.yml`, écrit par
Codex depuis cette maquette), la Trace, le marqueur de première visite
(`MarqueDeVisite`), et `Graine.pour` pour l'affichage.
