# Bandeau d’excursion : progression contextuelle

Note Codex — 12 septembre 2026. Recommandation demandée par Boris, pas une modification applicative.

## Recommandation

Garder une première ligne violette stable : geste en cours, expérience d’origine et retour. Ajouter **immédiatement dessous une seconde ligne contextuelle**, visuellement rattachée au même bandeau, uniquement lorsque le mini-jeu dispose d’un repère de progression pertinent. Ne pas placer la progression au-dessus du contexte et ne pas tasser les deux sur une seule ligne.

La première ligne répond « où suis-je, et comment revenir ? ». La seconde répond « où en suis-je dans cette activité ? ». Il s’agit de la progression INTERNE au mini-jeu, pas des cercles 1/2/3 de la fiche Expérience. Ne pas recopier ces derniers dans le mini-jeu.

## Constats vérifiés

Lecture de pointzero-app `preprod@1249212`, de la branche `bandeau-excursion` et ouverture de `/le-coupable-ideal` en préproduction. Cette ouverture directe rend l’ancien en-tête avec « Étape 1 sur 8 » ; elle n’a pas de contexte d’excursion actif. Aucun parcours complet ni réponse de joueur effectué dans cette revue.

Le layout `conseil` porte actuellement `@assessment.progress_label` avec barre de progression, ou `@progress_label` seul. La branche de remplacement masque `.conseil-header` lorsqu’un bandeau d’excursion existe. **Il faut donc transférer son information avant de masquer l’ancien en-tête** : sinon la progression disparaît, notamment dans Une drôle d’époque. Certains écrans répètent le compteur dans leur contenu ; ce n’est pas une garantie pour toutes les étapes.

| Destination M0 | Repère trouvé | Traitement recommandé |
|---|---|---|
| Le Coupable idéal | V2 : « Étape X sur 8 » ; la restitution `roue` est exclue du compteur. Certaines vues répètent ce repère. | Compteur compact dans la seconde ligne. Une rangée de 8 repères discrets est possible, sans annoncer les titres futurs. Retirer seulement les compteurs devenus redondants, conserver les titres narratifs. |
| Une drôle d’époque | Prologue, jour et Puissance, Premier miroir ; barre calculée par `MoteurAssessment`. | Reprendre le libellé et la progression existants dans la seconde ligne. Ne pas convertir chaque écran en cercle : la semaine comporte plusieurs interactions par jour. |
| Avant le Zéro | Nom de section ; parcours à embranchements explicites. | Nom du moment actuel uniquement. Pas de pourcentage ni de total d’étapes inventé sur un parcours à branches. |
| Conseil Oméga | Nom de section fourni par le contrôleur. | Même principe : moment actuel ; ajouter une progression chiffrée seulement si le service fournit un dénominateur fiable. |
| Chaîne invisible, Schéma de circulation, Signe de reconnaissance, Boussole | `ExperienceQuizAttempt.progress_label` : rang et total des écrans hors restitution. | Repères courts possibles, calculés avec la règle existante. Ne pas compter les restitutions comme un exercice de plus. Le feedback éventuel conserve le rang prévu par le service. |
| Les cinq parcours publics accessibles depuis Le site du Point Zéro | Progression propre aux modules `public/sas/{croyances,humanite,paralysie,reveil,scenarios}` ; repères d’écran/barre. | Conserver leur progression locale dans un premier temps. L’intégration au bandeau doit suivre le changement d’écran réel du module, sans deuxième compteur indépendant. Ne pas confondre cette progression avec le nombre de parcours publics achevés. |
| Immateria | Canvas et progressions internes de questionnaires, dont Village et donjon. | Garder les compteurs près du questionnaire concerné. Pas de chemin de fer global au-dessus du canvas ; ne pas traiter le questionnaire du donjon comme le tutoriel M0. |
| Mentor, Guides, Traces, éditeur de Graine, profil, agenda | Destinations d’activité dont toutes ne forment pas une séquence de mini-jeu. | Bandeau de contexte seul par défaut ; aucune seconde ligne vide ou fabriquée. |

## Disposition

Sur ordinateur : première ligne avec titre et retour ; seconde ligne plus mince, alignée sur le même conteneur, libellé courant à gauche et progression à droite si elle existe. Même fond violet, séparation discrète. Les titres du contenu restent dans la page.

Sur téléphone : contexte compact et retour toujours accessible ; dessous, une ligne telle que « Étape 3 sur 8 » ou « Mardi · Volonté ». Les cercles nombreux se réduisent à un compteur, sans défilement horizontal imposé. Ne rendre collant que ce qui n’étouffe pas l’activité : tester notamment 390 × 844 et 200 % de zoom.

Les repères sont informatifs par défaut. Leur clic ne doit pas ouvrir des écrans futurs, modifier les réponses ou contourner les prérequis. Une navigation de reprise reste celle déjà autorisée par le mini-jeu.

## Impact et recette avant portage

Portable : exposer un petit contrat de lecture commun (libellé, rang/total si connus, état terminé) depuis le moteur réel de chaque activité. Ne pas utiliser le rang de `SequenceDeGestes` comme progression interne. Aucun nouveau mécanisme de validation, de points ou de sauvegarde.

Desktop : rendre une unique zone facultative sous le contexte, conserver l’ancien en-tête hors excursion, supprimer les doublons seulement lorsqu’un repère identique est effectivement rendu dans le bandeau. Les modules JavaScript mettent à jour cette zone depuis leur état courant ; pas de calcul parallèle à partir du DOM.

Recette : entrée depuis la fiche et entrée directe ; début/milieu/restitution ; reprise sauvegardée ; écran de feedback ; chemin à branches ; mobile et zoom ; retour vers la bonne expérience. Vérifier absence de double progression, de sortie concurrente et de dévoilement de titres à venir. Vérifier que le remplacement de l’en-tête noir ne supprime aucune information.

Sources de code : [layout conseil](https://github.com/PointZero2050/pointzero-app/blob/1249212/app/views/layouts/conseil.html.haml), [progression du procès](https://github.com/PointZero2050/pointzero-app/blob/1249212/app/models/coupable_ideal_session.rb), [progression de la semaine](https://github.com/PointZero2050/pointzero-app/blob/1249212/app/models/moteur_assessment.rb), [progression des questionnaires](https://github.com/PointZero2050/pointzero-app/blob/1249212/app/models/experience_quiz_attempt.rb), [Avant le Zéro](https://github.com/PointZero2050/pointzero-app/blob/1249212/app/controllers/avant_le_zero_controller.rb).
