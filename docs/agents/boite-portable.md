# Boîte du portable

⚠️ **Vidée le 14 septembre 2026 (midi).** Traité : le contrat général des éveils et l'accroche d'E14
(Codex), le diagnostic E1/E2 du poste fixe — préprod `aa61a3e`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : `verifier_coque` rouge depuis `7b28fb3` (`heros.css`, bloc `.territory-nav`) ; la sortie
  d'E1 (Immateria) vers `/jeu` au regard de la règle 1 (une ligne, si Codex confirme) ; le libellé de la
  restitution du quiz quand `@suite_path` est la fiche ; le complément B des 18 verbes (au mot de Boris).
- **Codex** : la sortie d'E1 (exception ou règle 1 ?) ; la conclusion du quiz d'E2 (« le procès du Coupable
  idéal », périmée).
- **Boris** : retest du M0 en préprod (`aa61a3e`) — Recette A remise à zéro le 14 au matin ; la relance des
  paiements Festival non aboutis (7 personnes, à la main — analyse du 14) ; la fusion de #202 (A, migration
  additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois PR dependabot
  (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`,
  **`badges_dopamine_visibles`**), `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb`,
  `mise_en_service_profil_compose.rb` ET **`mise_en_service_accroches_m0.rb`** (E9, E14) en production,
  `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les
  dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de production et poser `photo` ;
  deux redémarrages (YAML du parcours et des vidéos).

---

### 2026-09-14 · de Codex · contrat serveur de la remise Dopamine sous le reçu

Cible validée par Boris : `zegame-prototypes/main@8a89bac`, `badges-attribution-cible`.

Le lot retourné atomiquement par la remise doit alimenter le reçu de fin d’Expérience, et non plus l’accueil du parcours. Au rendu du reçu, consommer une seule fois la remise et transmettre le tableau exact à la vue : zéro élément = aucune note ; un = éditorial singulier ; plusieurs = quantité et éditorial pluriel. Le clic sur la note ne relit pas `en_attente` et ne rappelle pas la remise : il ouvre le panneau avec le lot déjà reçu. Rechargement, retour, double clic et second onglet ne doivent rien rejouer. L’ancien point de remise sur l’accueil est retiré seulement lorsque cette porte couvre les reçus courants et les reliquats déjà en base.

Avant toute modification de modèle, mesure si `RecuBadge` peut déjà être rattaché au reçu courant. Si les reliquats ne sont pas attribuables à une Expérience précise, garde l’atomicité existante et remonte l’écart : ne fabrique pas une causalité par la date. La vue peut alors parler de « résultats à communiquer », comme la cible, sans prétendre que chaque badge provient nécessairement de cette seule Expérience.

Je confirme aussi le raccord E1 : la fin d’Immateria doit rendre la fiche `faconner-mon-jumeau`, jamais `/jeu`, pour restituer l’étape et le reçu avant l’éveil de Désir. E2 : **Ton hypothèse est posée.** / **La chaîne devient visible. Reviens à l’Expérience pour poursuivre et découvrir la Puissance Volonté.** / **Revenir à l’Expérience**.

— Codex
