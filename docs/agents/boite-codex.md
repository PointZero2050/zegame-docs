# Boîte de Codex

### 2026-09-20 · du poste fixe · Tes arbitrages d'Immateria sont portés (#318) — un écart à connaître sur mobile

Portés mot pour mot dans #318 :
- le badge (« Tu as ramené quelque chose de la cave… ») ;
- la quête (« Poursuivre ton voyage dans Materia ») ;
- la réponse sur la maison ;
- la fenêtre MageOS ;
- l'avis « Immateria a changé » (au-dessus des deux plans : sans Enfant, pas de dialogue pour le porter) ;
- l'attention F21 (visible sous le premier message, vers le Centre) ;
- le lien vers les vingt (« Revoir le Monde 0 » mène à la liste) ;
- la carte Puissance (la définition du verbe pour un joueur).

**L'écart, à 375 px** : relever « MageOS » à 10 px élargissait le compteur, et le nom de l'Enfant tombait à « Lu… ». J'ai donc empilé le compteur (lemniscate au-dessus du libellé et du nombre), passé le statut sur deux lignes et remonté la silhouette. Rien n'est sous 10 px, et les noms restent entiers à 375 comme à 320. Le bureau ne change pas. Si tu préfères une autre disposition, dis-le.

**Un point sur « Retrouver mes accomplissements »** : ta formule est gardée, mais le lien n'est offert qu'une fois la page ouverte. En jouant E1 sur la préprod, il menait avant Transcendance à « Cette page t'attend un peu plus loin » ; le message du badge reste.

— le poste fixe

---

### 2026-09-20 · du portable · Tes arbitrages du premier lot sont portés (préprod `8f17edc`) — ce que j'ai mesuré en route

Tout est porté, mot pour mot :
- `config/badges.yml` : les mots de la famille (gardien, intro) et du badge (phrase, condition, obtention).
- **L'ancien joueur réel** : `ImmateriaE1.ancien_tutoriel_reel?` = `tutoriel_termine` ET les faits que l'ancien jeu posait (`name`, `charKey`, `archetype`…), rien de la V2. **Mesuré en production** : deux joueurs (ids 60 et 76), les onze clés de l'ancien tutoriel, `name` et jamais `avatarName` ; aucun compte de recette n'y ressemble (E1 validée sans Trace, ou une Trace réduite au marqueur) — le banc tient les deux moitiés. L'avis « IMMATERIA A CHANGÉ » (ta copie exacte, CTA « Retrouver mon Enfant » vers la porte d'E1) est posé dans `@accueil[:avis]` UNE fois, atomiquement ; la vue est au poste fixe. La reprise pose la fin V2 (`termine_le`, un fait à elle — lire l'ancien `tutoriel_termine` aurait fait tomber la flamme dans la cave) et le badge, sans un Oméga de plus.
- **Les vingt Expériences après la clôture** : `/parcours/point-zero-monde-0/experiences` rend la carte du voyage dans tous les états ; le lien secondaire sur le tableau de bord est au poste fixe.
- **F21** : la première ligne de `Engagements.pour(user)`, en tête des actions de l'avatar, vers le Centre. Aucune règle nouvelle.
- MageOS = Ω, ta copie transmise au poste fixe pour la fenêtre de ressource.

Rien ne te revient de ce lot. Reste ouvert chez toi : la carte Puissance après le regroupement, l'état `empty` de la Carte du Seuil.

— le portable

---


⚠️ **Vidée le 19 septembre 2026.** Les demandes Immateria sont traitées : libellés définitifs du
badge et de sa famille, reprise des anciens joueurs sans retrait ni second gain, MageOS temporairement
alignés sur les Omégas, maintien d’une attention contextuelle, géographie `/jeu` / parcours, Monde 1,
carte Puissance et état vide de la Carte du Seuil. Les contrats et les boîtes des deux postes ont été
mis à jour. Rien n’attend ici.
