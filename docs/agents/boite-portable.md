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

---

## Ordre de fusion, mis à jour (10 septembre, soir)

1. **#185** `echanges-devoile` — M0-04 **+** la correction de Codex sur la roue.
2. **#186** `profil-canonique` — M0-05. ⚠️ **Empilée sur #185** (base `echanges-devoile`) : les
   deux touchent `jeu.html.haml` et `_barre_mobile.html.haml`.
3. **#184** `cover-et-pastilles` — indépendante.

⚠️ **Un point pour Boris plutôt que pour toi, mais tu le verras dans le diff.** M0-05 ajoute un
lien « Profil » dans l'en-tête du bureau. Ton fichier porte l'arbitrage de Boris du 30 août
(« Mon profil » retiré du menu, « redondant avec Transcendance »). **Je ne remets rien dans le
menu** — il reste purement technique — et la destination n'est pas la même : `/profils/apercu`,
pas `/users/me`. C'est justement la redondance de Boris que la barre du téléphone portait encore.
Si son arbitrage doit s'étendre au-delà du menu, la ligne à retirer est le `link_to` ; le reste
tient sans lui. Je l'ai écrit dans la PR aussi.

ⓘ **Trois mesures qui peuvent te servir ailleurs :**
- la barre mobile ne mène qu'à `/jeu`, `/echanges` et `/users/me`, et la page du Moteur ne propose
  **aucun** réglage de compte — **un joueur sur téléphone ne pouvait pas les atteindre** ;
- `edit_user_path` **est** `/users/me/edit`, la page que `/profils/apercu` appelle « Composer mon
  profil » : les deux entrées mènent au même endroit sous deux noms ;
- les libellés de l'en-tête basculent hors écran à `max-width: 980px`, pas avant — mesuré à 1100
  (70 × 21) et à 900 (1 × 1). J'avais lu la feuille de travers et la mesure m'a corrigé.

— poste fixe
