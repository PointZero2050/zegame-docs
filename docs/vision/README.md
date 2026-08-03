# Vision produit — Point Zéro, Marelle Oméga et monde-miroir

<!-- Ajout Claude, 2026-07-12 -->

Cette section rassemble la vision idéale de ze.game, issue d'un brainstorming entre Boris et Codex. **Aucun de ces documents ne constitue une spécification validée ni un périmètre engagé.** Ils décrivent un horizon produit ambitieux destiné à orienter les décisions de conception, pas un plan d'implémentation à court terme.

Pour l'état réel actuel de l'application, voir [../architecture.md](../architecture.md) et [../design.md](../design.md).

## Décision opérationnelle en vigueur

Le cadrage [application-festival-2026.md](application-festival-2026.md), validé le 2026-07-24, fixe la trajectoire de livraison de l'application Point Zéro autonome pour le Festival du 1er octobre 2026. Contrairement aux autres documents de cette section, il constitue une décision opérationnelle et prévaut sur les recommandations antérieures qu'il identifie comme remplacées.

## Ordre de lecture recommandé

> **Synthèse pour le Cercle cœur :**
> [Point Zéro — Questions et réponses sur le fonctionnement global de l'écosystème](ecosysteme-point-zero-questions-reponses-cercle-coeur.md)
> consolide les décisions sur le Sas public, les Mondes 0 à 2, les Cercles, les profils, les
> Rôles d'appel, l'Oméga, les trois circuits financiers et la Ressourcerie. Il distingue
> explicitement ce qui est acté, hypothétique, ouvert ou reporté.

> **Décision canonique récente :** lire en complément prioritaire
> **[cercles-croissance-profils-flow-omega.md](cercles-croissance-profils-flow-omega.md)**. Ce
> document consolide les arbitrages du 31 juillet 2026 sur le Cercle de croissance dès le Monde 1,
> les cycles et lignées, le Pacte-Source, les cinq rôles, les profils systémiques, le flow, le 360°,
> les héros, les missions et le decay des Omégas.

1. **[marelle-mondes.md](marelle-mondes.md)** — Le document fondateur. Traduit la Marelle Oméga (progression par mondes 0 à 10, cercles de croissance, sécurité ontologique) issue du livre source en hypothèses fonctionnelles pour ze.game. Pose la stratégie d'adoption incrémentale.

2. **[monde-miroir.md](monde-miroir.md)** — Le repositionnement le plus ambitieux : avatar/jumeau numérique autonome, monde-miroir narratif, Ombre et Lumière captive, mana, quatrième mur. Sert de hub vers les 4 notes fonctionnelles ci-dessous.

3. **[relations-recits-collectifs.md](relations-recits-collectifs.md)** — Messagerie propre au Point Zéro, récit-fresque personnel, architecture sociale fractale (cercles, quêtes collectives).

4. **[ressourcerie-marketplace.md](ressourcerie-marketplace.md)** — Cartographie vivante des ressources (graphe de connaissance), évaluation par les cinq cadres, marketplace des facilitateurs-designers.

5. **[validation.md](validation.md)** — Moteur de validation pédagogique : distinction preuve/déclaration/validation, conditions composites, architecture par événements métier.

6. **[game-autosubversion.md](game-autosubversion.md)** — Direction de game design : codes de l'Empire détournés progressivement vers la conscience, combats par runes, ton et personnages, direction artistique.

7. **[accueil-point-zero.md](accueil-point-zero.md)** — Première proposition concrète issue de la vision : accueil orchestrateur, états du Joueur, mode événement pour le New Civilization Festival, parcours libre et workflow de prototype HTML avant implémentation Rails.


8. **[navigation-vues-ensemble.md](navigation-vues-ensemble.md)** — Vision coordonnée des vues Marelle, Cercle, Ressourcerie et Profil ; modèle `World` distinct de `Community`, passages automatiques auditables, Open Badges et carte personnelle des puissances.

9. **[impacts-fonctionnels.md](impacts-fonctionnels.md)** — Registre d'analyse d'impact back/front (F1-F18) : chaque page front y est modélisée avec ses impacts backoffice avant implémentation. Règle : aucune implémentation sans ligne d'analyse ici.

10. **[sept-puissances.md](sept-puissances.md)** — Référentiel des 7 puissances et moteur ontologique (synthèse du Livre II) : verbes, polarités Lumière/Ombre, 5 états du moteur, gardiens des Mondes, implications pour l'Oméga et la validation.


11. **[cosmo-coin-omega.md](cosmo-coin-omega.md)** — Référentiel du Cosmo Coin Oméga (synthèse du document source) : ce que l'Ω valorise (4 échelles), mécanisme régénératif (horizon), rôle de l'IA systémique, harmonie des besoins, traduction produit V1 vs horizon, garde-fous.

12. **[monde-1-parcours.md](monde-1-parcours.md)** — Cadre opérationnel pour produire les parcours du Monde 1 : tutoriel obligatoire, catalogue initial, correspondance avec les modèles actuels, matrice disponible/développement, politique de passage vers le Monde 2 et gabarits éditoriaux.

13. **[direction-artistique-point-zero.md](direction-artistique-point-zero.md)** — Système visuel global : néoarchaïsme comme grammaire mère, coque produit stable, univers libres par parcours, invariants de continuité, éthique des références aux peuples premiers et processus de création des assets.

14. **[autofacilitation-monde-1.md](autofacilitation-monde-1.md)** — Cadre des Cercles autofacilités du Monde 1 : rôles tournants, conducteur, accords de sécurité, validation de participation et distinction avec la facilitation professionnelle requise au Monde 2.

15. **[moteur-ontologique-visuel.md](moteur-ontologique-visuel.md)** — Grammaire visuelle du Moteur ontologique sur le Profil : lemniscate vivant à lobes indépendants (Option B), 4 couleurs (gris horizon / violet état 360° / pointillé cap / or progression Oméga), distinction état vs progression, moteur global comme résultante (Transcendance non nommée), 6 puissances en mini-lemniscates, fiche puissance et implications modèle de données. Prototypes dans zegame-prototypes.

16. **[voix-point-zero.md](voix-point-zero.md)** — Charte de voix transversale issue du Monde 0 : ton adulte, décalé et provocateur, humour discret, sortie de la posture « Enfant Adapté », dosage par surface, limites éthiques et traduction graphique du sublime confronté au trivial.

17. **[cartes-experiences-freeride.md](cartes-experiences-freeride.md)** — Architecture UX validée des fiches d'expérience : carte-couverture mobile-first, scène d'image robuste, détails progressifs, actions contextuelles et horizon Freeride à partir du Monde 2. Distingue explicitement l'amélioration immédiate du futur deck adaptatif.

18. **[page-parcours-carte-du-voyage.md](page-parcours-carte-du-voyage.md)** — Spécification validée de la page ordonnée d'un parcours : carte du voyage, prochaine action au premier écran, chapitres narratifs, progression requise distincte des Oméga, cartes compactes et rite final. Inclut lots et critères d'acceptation responsive.

19. **[Atelier-seuil et jeu de l'Intercycle](../pedagogie/atelier-seuil-et-jeu-intercycle-monde-1.md)** — articulation canonique du rite de fin du Monde 0 avec le tutoriel et les Cercles du Monde 1 : trois vidéos, Carte du Seuil enrichie, traversée solo, rejeu collaboratif et débrief sur les conditions de l'intelligence collective.

20. **[analyse-impact-cercles-intercycle.md](analyse-impact-cercles-intercycle.md)** — Analyse d'impact exigée avant tout code Cercles/Intercycle (audit serveur du 2026-07-31) : sémantique exacte d'`on_change`, idempotence des Ω, barème réel du Monde 0 (le marqueur « 100 Ω » est inatteignable), révocation résiduelle sur `JourneysUser`, absence de modèle Graine, schéma proposé pour le Lot 1 et stratégie de retour arrière.

21. **[Rôles d'appel et fonctions civilisationnelles](../pedagogie/roles-appel-fonctions-civilisationnelles.md)** — Décision canonique sur la sortie du Conseil Oméga et son prolongement au Monde 1 : douze fonctions, mode Pulsateur transversal, réintégration non naïve des capacités de l'Empire, Carte du Seuil, Intercycle, Pacte-Source et migration des illustrations historiques.

22. **[Profil communautaire et messagerie des Cercles — V1](profil-communautaire-messagerie-cercles-v1.md)** — visibilité progressive entre joueurs, dossier de rencontre, contact interne candidat/référent, e-mail de notification, réemploi de la messagerie des feedbacks, périmètre reporté et analyse d'impact avant code.

23. **[analyse-impact-messagerie-cercles.md](analyse-impact-messagerie-cercles.md)** — Analyse d'impact P0 (audit serveur du 2026-07-31) : faille d'accès déjà en production sur `Messaging::Thread` (aucune restriction de participation), notifications e-mail jamais implémentées (`GlobalSettings.send_mail_notif_for_thread` non défini), vues d'index/show hard-codées Challenge/Journey, conteneur unique proposé (`CircleMembership`), absence totale de Badge/Contribution/Resonance/Block/Report.

24. **[caracterisation-progression-omega.md](caracterisation-progression-omega.md)** — Caractérisation du cœur du jeu pour le portage catégorie B (2026-08-02) : cycle de vie `end_at`/`validated_at`, règle « une validation ne se révoque jamais », piège du double-écriture `on_change` (incident Oméga du 2026-07-25), dérivation `auto_validated`, progression F2b obligatoire/optionnelle et verrouillage linéaire, scénarios de vérification de parité.

25. **[caracterisation-auth-roles-autorisations.md](caracterisation-auth-roles-autorisations.md)** — Caractérisation de l'authentification, des rôles (`nil`/`dff`/`admin`) et du moteur d'autorisation `Cans` (2026-08-02) : sémantique exacte de `no_roles`/`roles`/`all`/`can?` (aliasing multi-actions, retour strictement `true`), piège classe-vs-instance d'`authorize_resource` sur les routes imbriquées singulières (faille du 2026-08-01), leçon générale sur le partage de communauté par défaut, scénarios de vérification de parité.

26. **[caracterisation-triptyque-monde-0.md](caracterisation-triptyque-monde-0.md)** — Caractérisation du triptyque Monde 0 (2026-08-02) : le patron « auto-validation Marelle » identique dans cinq modules (`MoteurAssessment`, `Traversee`, `ConseilSession`, `CoupableIdealSession`, `ExperienceQuizAttempt`, à fusionner en un seul service au portage), le calcul déterministe et explicable de posture/portes de « Une drôle d'époque », l'absence délibérée de scoring dans « Avant le Zéro » et le Conseil Oméga, le couplage descendant vers le Rôle d'appel du profil communautaire, scénarios de vérification de parité.

27. **[caracterisation-coupable-ideal.md](caracterisation-coupable-ideal.md)** — Caractérisation du mini-jeu « Le Coupable idéal » (2026-08-02) : coexistence V1/V2 sans réévaluation rétroactive, le procès contradictoire déterministe (cause → charges → axes révélés → verdict à quatre volets, roue toujours à 6 axes avec équivalent textuel d'accessibilité, absence délibérée de mapping axe→Puissance), le mode éphémère et sa purge immédiate après restitution, la rétention choisie par le joueur, scénarios de vérification de parité.

28. **[caracterisation-qcm-experience.md](caracterisation-qcm-experience.md)** — Caractérisation du moteur générique de QCM d'expérience (2026-08-02), ferme la boucle des cinq modules d'évaluation : registre d'évaluateurs enfichables (deux méthodes de contrat, pas de DSL générique anticipé), sécurité contre la double-création en cas de course (index unique partiel + rescue), validation/normalisation d'URL saisie par le joueur, scénarios de vérification de parité.

29. **[caracterisation-controleurs-conventions.md](caracterisation-controleurs-conventions.md)** — Caractérisation de la couche contrôleurs (2026-08-02), pour le portage des contrôleurs/vues qui suit celui des modèles : détection de langue par en-tête navigateur (préférence par utilisateur jamais nourrie, `:fr` forcé en dev/test), `Slugable#find` (slug ou id) vs `find_by` (id seulement, échec silencieux), listes blanches de params imbriqués (champ absent = ignoré sans erreur), le patron PRG partagé par les quatre contrôleurs d'évaluation du Monde 0.

## Corpus pédagogique associé

Le corpus détaillé produit par Boris avec ChatGPT est indexé dans [../pedagogie/README.md](../pedagogie/README.md). Lire en priorité sa [note de convergence](../pedagogie/convergence-2026-07-16.md), qui distingue les apports compatibles, les décisions déjà actées et les arbitrages encore ouverts.

## Ce qui manque encore

- **Priorisation inter-documents** : chaque note propose sa propre séquence interne, mais rien n'arbitre l'ordre entre la messagerie, la ressourcerie, la marketplace et le moteur de validation.
- **Application Festival : cadrage opérationnel validé le 2026-07-24** — application Rails autonome, base séparée, retrait progressif des gems privées et gel fonctionnel cible au 15 septembre ; voir [application-festival-2026.md](application-festival-2026.md).
- **Prototype accueil : cadrage validé le 2026-07-12** (ton mixte, vocabulaire hybride, Festival 1er octobre confirmé, et décision structurante : future appli dédiée Point Zéro séparée de ze.game — voir §13 de [accueil-point-zero.md](accueil-point-zero.md)). Wireframes en cours dans le repo zegame-prototypes.
- **Revue légale/éthique dédiée** : plusieurs mécaniques envisagées (quatrième mur via caméra/géolocalisation/notifications, récits personnels sensibles, vocabulaire thérapeutique/initiatique, public potentiellement mineur) dépassent le cadre d'une revue produit ou design classique.
- ~~Clarification de la numérotation des mondes~~ **Tranché (2026-07-14) : 11 positions, Mondes 0 à 10** — matérialisé par les 11 communautés du bac à sable.
