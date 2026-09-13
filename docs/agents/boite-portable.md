# Boîte du portable

⚠️ **Vidée le 14 septembre 2026, petit matin.** Traité depuis la vidange de la nuit : le contrat
E9 v2 de Codex (le Profil composé comme preuve, `4fb359e`), les noms du poste fixe (repris tels
quels), #259, puis #260 (la vue de l'éditeur, après mon lot) — préprod `aa08773`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le complément B des 18 verbes (après A, au mot de Boris).
- **Codex** : deux points tranchés sans lui sur E9 (le sceau « Présence choisie » suit le profil
  composé, Communication s'éveille toujours à la validation ; l'Annuaire `facultatif: true`) — à
  confirmer ou corriger.
- **Boris** : retest du M0 en préprod (`aa08773`) — Recette A à E7, Émotion due ; la fusion de #202
  (A, migration additive) puis #211 ; la recette transversale et la promotion sur son mot ; les trois
  PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb` ET `mise_en_service_profil_compose.rb`
  en production, `wt-ref18` après fusion ; **les six photos** (E1 `faconner-mon-jumeau-v2`, E15–E19
  `*-v1`) : copier les dossiers `~/uploads/challenge/photo/<id préprod>` vers les identifiants de
  production et poser `photo`.

---

### 2026-09-14 · du poste fixe · Espace 1827 : branche `espace-composeur-stable` poussée — le composeur sort du fil, PR sur `preprod`

Cible Codex `7bd93cd`, validée par Boris. **Aucun contrôleur, modèle ni route.**

1. **`espaces/show`** : `.pz-fil-pied`, frère de `.workspace`, porte le composeur, ou l'état clos ou suspendu. Les formulaires d'objets restent dans le fil. `rencontre_possible` se calcule avant le fil.
2. **Hauteur** : la coque ne fait plus `100dvh - 68px`. La chaîne part de `body` (`height: 100dvh`) et passe par `main`, `.p-lg-5` et `#inner-main`, par `:has(.pz-m0-echanges--fil)` à toutes les largeurs et `--liste` au-dessus de 1121 px. Motif : avec une excursion ouverte, le bandeau (84 px) faisait déborder la page et poussait le composeur hors de l'écran. Sous 1121 px, la coque montait à 6 807 px.
3. **`composer.css`** : les marges négatives des Espaces sont retirées, et la réserve des messages passe de 110 à 16 px. Le `#composer` collant des fils d'expérience (`threads/show`) est **intact**.
4. **Bancs, avec un `ruby -c` d'abord** :
   - `verifier_espaces_s1` (fratrie du fil et du pied), `verifier_accueil_echanges` (chaîne de hauteur, §2 réécrit) et `verifier_apercu_espace` (le pied se cache avec le fil) ;
   - à rejouer aussi : `verifier_bascule_mobile`, `verifier_canal_m0`, `verifier_echanges`, `verifier_coque_m0`, et les bancs des réactions.
5. **À regarder sur la vraie page une fois déployée** (je ne l'ai vue qu'en simulation) : envoyer sans rechargement, répondre à un message, un espace clos, et `?objet=sondage`.

— poste fixe
