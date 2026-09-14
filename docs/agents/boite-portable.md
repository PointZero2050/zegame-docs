# Boîte du portable

⚠️ **Vidée le 14 septembre 2026 (nuit).** Traité : #266 → #274 du poste fixe (Guides, Dopamine, Moteur,
bandeau, profil, reçu, E16, Puissance, E14 v2), le contrat E14 de Codex, le contrat de vue du poste fixe —
préprod `91c2456`. Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : le libellé du bouton de suite quand il mène à un éveil (`suite_experience[:libelle]`) ;
  le mot du tiroir avant E14 (selon Codex) ; le complément B des 18 verbes (au mot de Boris) ; la V3 du
  profil communautaire (cible Codex) ; les helpers de route du tutoriel E14 (facultatif).
- **Codex** : le contrat d'éveil (ordre éveil/fiche au retour — et le cas E14 : le moment 4 vaut-il
  annonce ?) ; les textes du rang 2 d'E14 (YAML) ; `titre`/`texte` de l'écran de fin d'E16 ; le mot du
  tiroir Dopamine avant E14 ; la `description` d'E9 ; les deux points d'E9 (sceau, Annuaire facultatif).
- **Boris** : retest du M0 en préprod (`91c2456`) — Recette A à E14 validée ; E16 et E14 v2 à revoir ;
  la fusion de #202 (A, migration additive) puis #211 ; la recette transversale et la promotion sur son
  mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo), d'E6 (autorité),
  **d'E2 (durée 15)** en production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`,
  **`badges_dopamine_visibles`**), `mise_en_service_badges.rb`, `mise_en_service_preuve_du_sas.rb` ET
  `mise_en_service_profil_compose.rb` en production, `wt-ref18` après fusion ; **les six photos** (E1
  `faconner-mon-jumeau-v2`, E15–E19 `*-v1`) : copier les dossiers `~/uploads/challenge/photo/<id préprod>`
  vers les identifiants de production et poser `photo` ; deux redémarrages (YAML du parcours et des vidéos).

---

### 2026-09-14 · du poste fixe · Je prends la V3 du profil communautaire (Codex `22aee12`) — vue, feuille et bancs seulement

Branche `profil-apercu-v3` depuis `origin/preprod`. `/profils/apercu` et `/profils/:id` (même vue) passent en quatre vues : Aperçu, Accomplissement, Graines, Traces. Les onglets sont des liens `?vue=…` rendus par le serveur, et un petit script les bascule sans rechargement. Les Traces ont des filtres de famille et un chargement par cinq.

- **Aucun contrôleur, modèle ni route** : tout est déjà dans `charger_profil`.
- **Plus aucune commande de propriétaire sur le profil** : le retrait d'une Graine reste sur `/profils/visibilite`.
- **Fichiers que je touche** : `profils/show.html.haml`, `public/pz/m0/profil.css`, `public/pz/m0/profil-apercu.js` (neuf).
- **Bancs que je modifie** : `verifier_apercu_profil`, `verifier_cartes` (§2), `verifier_profil` (§8), `verifier_profil_m0` (§1). La PR suit, avec le `ruby -c` à te demander.

— poste fixe
