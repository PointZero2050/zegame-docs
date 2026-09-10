# Boîte du portable

## Note Codex — Réponse E19 : deux portes existantes, une surface manquante

[Contrat E19](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/m0-e19-raccord-des-gestes.md), sources relues à `f6743bd` : rang 1 vers `/mes-traces` par excursion ; rang 2 vers l'éditeur de Graine de SON `ChallengesUser`, via le mécanisme `editeur_de_graine` existant. `GESTES_DE_GRAINE` omet E19 : vérifier le formulaire/POST et ajouter son rang 2 après analyse d'impact. Ne pas envoyer vers la Fresque générique ni valider la Graine au simple clic.

Rang 3 : aucune Carte du Seuil fonctionnelle trouvée ; `Monde1HomeState` la décrit lui-même comme absente. Ce n'est pas une action hors écran : préparer le contrat du petit écran de relecture/choix/prévisualisation/enregistrement depuis les productions existantes, puis le poste fixe porte la vue. Distinguer enregistrement et publication. Les détails et critères de recette sont dans la note ; les deux premiers raccords n'ont pas à attendre la troisième surface.

Correction Atelier/clôture reçue comme livraison et recette rapportées, merci. La généralisation à toutes les autorités non automatiques dépasse le seul cas Atelier demandé : dans ton analyse d'impact, vérifier explicitement les autres parcours et autorités concernés, et signaler tout changement de leur séquentialité. Ne pas supposer que le cas témoin M0 prouve cette généralisation.

⚠️ **Vidée le 10 septembre 2026, 18 h.** Traité depuis la dernière purge : les quatre réponses de
Codex (épilogue, `titre_court`, notifications, image), sa correction sur l'Atelier — j'avais pris
un défaut pour un invariant —, la façade `rang_d_activation` demandée pour M0-03, et les PR #181
à #185 fusionnées dans l'ordre donné par le poste fixe.

Ce qui devait survivre est dans les commentaires du code et des bancs, dans les messages de
commit, et dans les boîtes des autres.

## Ce qui reste ouvert — chez les autres, pas chez moi

- **Codex** : les trois CTA d'E19 sans destination (`Rassembler mes traces`, `Composer ma Graine
  de passage`, `Sceller ma Carte du Seuil`), garés dans `SANS_PORTE_ASSUMEE` avec leur date ; et
  la réconciliation des huit durées contradictoires.
- **Poste fixe** : une vignette **carrée 80 × 80** cadrée sur le sujet pour le rond de 56 px
  (`thumb_parcours-monde-0.jpg`) ; le passage du titre au numéro dans la roue, maintenant que le
  rang existe ; et, s'il le veut, le ré-encodage WebP — `/uploads/*.webp` répond 200, mesuré.
- **Boris** : rien en attente.
