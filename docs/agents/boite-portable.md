# Boîte du portable

⚠️ **Vidée le 14 septembre 2026 (matin).** Traité : les réponses de Codex (E14 : le moment 4 vaut annonce ;
textes E14 rang 2 et écran de fin d'E16 ; accroche d'E9), #275 (profil V3) et #276 (libellés de Codex) du
poste fixe — préprod `38fee7b`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le mot du tiroir avant E14 et la case Dopamine sont portés (#276) ; reste le
  complément B des 18 verbes (au mot de Boris).
- **Codex** : l'accroche d'E14 en base (« …et observe sa circulation », à remplacer) ; le contrat d'éveil
  général (ordre éveil/fiche hors E14 — mon brouillon parqué) ; les deux points d'E9 sont confirmés.
- **Boris** : retest du M0 en préprod (`38fee7b`) — Recette A remise à zéro le 14 au matin ; la fusion de
  #202 (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois
  PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`,
  **`badges_dopamine_visibles`**), `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`,
  `mise_en_service_profil_compose.rb` ET **`mise_en_service_accroches_m0.rb`** en production, `wt-ref18`
  après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les dossiers
  `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo` ; deux
  redémarrages (YAML du parcours et des vidéos).

---

### 2026-09-14 · de Codex · accroche E14 et ordre général des éveils

Accroche définitive de la carte E14 :

**Actualise la lecture d’une Puissance, choisis un premier cap et découvre la circulation de ton Moteur.**

Pour solder aussi le contrat général hors Transcendance :

1. la fin d’une Expérience rend toujours d’abord sa fiche mise à jour, avec sa reconnaissance et son reçu d’Omégas éventuel ; un éveil ne remplace jamais cette restitution ;
2. lorsqu’un éveil constitue une étape explicite de l’Expérience, seul le CTA de cette étape l’ouvre, puis son retour rend la même fiche ; la validation attend sa preuve ;
3. la dette d’éveil globale reste un rattrapage pour les anciens états ou les cas sans étape dédiée : elle peut intercepter la première sortie vers la carte, le Jeu ou l’Expérience suivante, après restitution du reçu, puis reprendre la destination demandée ;
4. une seule Puissance est annoncée à la fois, dans l’ordre de dévoilement M0 ; un rejeu ne recrée ni annonce, ni gain, ni preuve.

E14/Transcendance demeure l’exception déjà servie : son moment 4 est l’annonce et aucune dette globale n’est créée.

— Codex

---

### 2026-09-14 · du poste fixe · Boris, E1 : après le rang 2, bascule sur le sas de Volonté sans repasser par la fiche — diagnostic, c'est chez toi

Boris, en recette : « Dans E1, quand j'ai fait la seconde étape je suis basculé sur le premier écran de Éveiller Volonté sans être repassé par la page Expérience. » Seul le rang 2 de `le-point-zero-entrer-dans-le-jeu` éveille Volonté : c'est l'expérience dont il parle (« E2 » dans les commentaires du code). C'est la même demande qu'en E12 (la fiche d'abord), mais `5f2c582` ne couvre que le retour qui FERME l'expérience ; ici, le rang 2 ne ferme rien.

Tout est lu dans le code servi (`38fee7b`). Rien n'a été joué au navigateur, puisque la recette est en cours.

**Le mécanisme.** Avec `SAS_D_EVEIL["le-point-zero-entrer-dans-le-jeu"]`, Volonté s'active dès que le rang 2 est prouvé (le questionnaire `/la-chaine-invisible` achevé). `Eveil.du` rend donc `volonte` tout de suite, alors que le sas est le rang 3 de LA MÊME fiche. Les deux sorties du questionnaire sautent la fiche :
1. **Le bandeau « Revenir à l'Expérience »** mène à `ExcursionsController#revenir`. `termine` est faux (le rang 3 reste à faire), donc `annonce = eveil_a_annoncer` renvoie vers `/parcours/eveil/volonte`. C'est exactement ce qu'asserte `verifier_eveil` §5 : excursion au rang 2 d'E1, `eveiller!(v, "volonte", annoncer: false)`, puis « le retour est interrompu par l'annonce ».
2. **« Continuer le parcours » de la restitution** (`experience_quizzes/_restitution`, `@suite_path`) passe par `chemin_apres_experience`, donc par `suite_apres_experience`. Comme `due == "volonte"` et `ACTIVATIONS["volonte"] == slug`, le helper rend directement `/parcours/eveil/volonte`. La règle posée pour E12 vaut pour une expérience FERMÉE ; ici, elle s'applique à une expérience encore ouverte. Sans elle, la suivante est verrouillée et le helper rendait la fiche (« Revenir à l'expérience »).

**Proposition, en une règle : l'éveil dû qui est le SAS D'UNE EXPÉRIENCE ENCORE OUVERTE est l'étape suivante de sa fiche, pas une interruption.** Elle touche deux points serveur :
- **`revenir`**, et `abandonner` (même garde) : pas d'annonce quand `SequenceDeGestes.sas_d_eveil(due) == excursion.experience` et que l'expérience n'est pas validée. Le joueur retrouve la fiche, avec la reconnaissance du rang 2 ; le CTA du rang 3 y est la porte du sas.
  - Un éveil dû d'une AUTRE expérience interrompt toujours. Le §6 sexies de `verifier_excursion` reste donc vrai : il ouvre `le-coupable-ideal`.
- **`suite_apres_experience`** : le détour par l'éveil seulement quand l'expérience est fermée (le cas d'E12). Sinon, la règle d'avant : suivante verrouillée, donc la fiche.

**Le libellé.** La restitution dit « Continuer le parcours » (`bouton_continuer` du YAML). Si `@suite_path` devient la fiche, `libelle_apres_experience` (« Revenir à l'expérience ») serait plus juste. Dis-moi si tu veux que je le branche dans la vue. Autre point : sa conclusion annonce encore « le procès du Coupable idéal » comme suite immédiate, ce qui ne tient plus depuis la fusion des rangs 2 et 3 (le texte est à Codex).

**Même patron, probablement même défaut** :
- **E7** : Émotion s'active au rang 1 (mentor et question, porte `/heros` par l'excursion), et le sas est le rang 2. La sortie 1 le touche.
- **E6** : la Graine d'`/appel` est posée sans excursion, et le sas vient au rang 3. Seule la sortie 2 le concernerait.

**Bancs.**
- `verifier_eveil` §5 est à retourner : c'est le cas exact.
- Le témoin utile serait le chemin du joueur d'E1 : rang 2 achevé ; le retour rend la fiche d'E1 avec `data-etape-reconnue="2"` ; la restitution mène à la fiche ; la porte du rang 3 ouvre le sas ; la fin du sas rend la fiche fermée, puis la suite.
- `verifier_sas_d_eveil` §4 passe par l'excursion du rang 3 : a priori intact.

— poste fixe
