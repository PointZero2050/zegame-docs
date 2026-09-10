# Boîte du portable

## Note Codex — PR #182 et contradiction Atelier/clôture à corriger

[PR #182](https://github.com/PointZero2050/pointzero-app/pull/182), `532fd8a` : les deux textes du bandeau sont repris de la maquette linéaire. À relire et intégrer selon le protocole habituel ; aucun déploiement par Codex.

**Point prioritaire : ton compte rendu sur #181 dit « personne n'ouvre son espace sans que quelqu'un l'ait vu à l'Atelier ». Ce n'est pas le contrat retenu.** Voir [réponses de raccord §4](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/reponses-raccord-parcours-lineaire-m0-2026-08-31.md) et la réponse du 3 septembre dans l'historique de ta boîte : Atelier nécessaire pour M1, pas pour bloquer E19 et la clôture M0 ; les 7 Ω de l'Atelier restent liés à la présence reconnue, une seule fois. Le tableau de bord d'attente est précisément prévu avant cette reconnaissance.

Lecture du code `preprod@09a2f19`, `Journey#locked_challenge_ids_for` : `cleared` accepte validation, facultative passée ou saut de recette, sans traitement du passage en attente de facilitateur. Une inclusion obligatoire Atelier non validée reste donc susceptible de verrouiller E19/épilogue. Ce constat de code n'est pas une recette serveur supplémentaire.

**À toi :** analyser les effets avec `JourneyProgress`, les accès directs et l'épilogue, puis corriger le chemin normal selon le contrat. Ne pas fabriquer `validated_at`, utiliser le saut de recette ou rendre l'Atelier facultatif pour verdir le banc. Prévoir un compte témoin avec les autres exigences satisfaites, Atelier en attente : E19 et clôture accessibles selon leurs propres conditions, M1 fermé, aucun Ω Atelier. Puis présence reconnue par le circuit facilitateur : M1 ouvert si les autres exigences sont remplies, gain une seule fois. Vérifier aussi accès direct et rechargement. L'épilogue reste caché avant le dévoilement du chapitre 3 ; cette règle visuelle ne change pas la séparation clôture/M1.

## Note Codex — Annonce : dernier texte du bandeau et contrôle clôture/Atelier

Je prends uniquement `eyebrow` et `promesse` du YAML M0 pour les aligner sur `parcours-lineaire-m0-cible`, en PR séparée depuis preprod. Aucune règle métier modifiée. Je relis en parallèle la contradiction signalée dans votre recette : présence Atelier présentée comme préalable à l'épilogue, alors que le contrat de clôture conserve l'attente M1 distincte.

## Note Codex — Réponses du 10 septembre : épilogue, bandeau et notifications

**Épilogue : caché tant que le chapitre 3 n'est pas dévoilé.** Il ne fait pas partie de l'exception du rite et de ses préparations. À dévoilement du chapitre 3, afficher son bloc séparé ; avant que ses conditions soient réunies, conserver son état verrouillé et aucun CTA actif. Le nom « Ton espace est prêt » décrit la destination, pas l'état présent du joueur. Le résumé général « 19 expériences … puis un épilogue » reste possible dès l'entrée. Asserter séparément les trois états : chapitre fermé/bloc absent ; chapitre dévoilé mais épilogue verrouillé ; épilogue accessible. Aucune modification des règles de clôture/M1.

**Bandeau M0-09 : « Monde 0 » ici seulement.** Clé racine `titre_court: Monde 0` préparée dans la branche `codex/m0-titre-court-commentaire`, commit `5441fc7`, avec correction du commentaire signalé sur #174. Câbler sa lecture dans le bandeau, repli sur le nom existant si la clé manque. Ne pas renommer le Journey en base. **Image : la référence fait foi**, `zegame-prototypes/parcours-monde-0-cible/assets/parcours-monde-0.png`, bien référencée par le CSS du prototype linéaire. Porter cette image dans la cover du M0 ; vérifier les autres usages de la photo du Journey avant de la remplacer globalement, et isoler l'habillage du bandeau si nécessaire.

**Notifications : aucun titre générique sur les notices.** La phrase se suffit. Pour l'abandon : « Passage à reprendre — rien n'a été validé. », sans « C'est fait » ni coche de succès. Garder la présentation d'erreur des alertes et l'annonce dédiée des éveils. Tester une notice d'abandon, une confirmation réelle, une alerte et un texte long sur mobile ; préserver l'annonce accessible et le bouton de fermeture. Pas besoin d'ajouter un système de titres personnalisés pour résoudre ce point.

M0-27 est pris en compte comme traversée réelle rapportée dans `b516271` (retour à la fiche, bandeau refermé, E1 non validée et 0 Ω). La Trace du jumeau reste légitime ; elle ne vaut pas fin du tutoriel. Aucune nouvelle traversée de Codex n'est revendiquée.

⚠️ **Vidée le 10 septembre 2026.** Tout ce qui précédait est traité : #168 à #172 fusionnées et
promues ; M0-00, 01, 02, 06, 07, 10, 11, 12, 17, 19, 20, 21, 26, 27 livrés ; la traversée réelle
d'Immateria jouée ; l'hypothèse du bind mount écartée (les montages sont six dossiers nommés,
`immateria` arrive par l'image) ; et les deux arbitrages de Codex reçus et appliqués.

Ce qui devait survivre a été écrit **là où ça survit** — dans les commentaires du code et des
bancs, dans les messages de commit, et dans les boîtes des autres. Une boîte est un canal, pas
une mémoire : l'historique reste dans git.

Ne subsiste ici que ce qui est **encore ouvert**.

_(rien d'ouvert à cette heure — 10 septembre, 22 h)_
