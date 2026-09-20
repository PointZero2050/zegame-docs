# Récapitulatif des mini-jeux Point Zéro — 20 septembre 2026

Ce document rassemble les cinq parcours publics et les mini-jeux du Monde 0 retravaillés avec
Codex. Il donne les références à utiliser pour le portage visuel et pédagogique. Les maquettes
simulent leurs états : elles ne font foi ni pour les routes, ni pour les preuves serveur, ni pour la
progression, les gains, les badges ou la persistance.

## 1. Les cinq parcours publics

**Dépôt :** `PointZero2050/zegame-prototypes`

**Branche distante :** `codex/parcours-decouverte-1-a-5`

**Commit :** `85aeb8c`

| # | Parcours | Dossier | Geste central |
|---|---|---|---|
| 1 | Qu'arrive-t-il à l'humanité ? | `parcours-humanite-convergence-cible/` | Signaux, douze cycles, convergence des cinq cycles centraux vers Point Zéro, résistance, possibilité, Trace. |
| 2 | Où allons-nous ? | `parcours-scenarios-triangle-cible/` | Futur redouté, désiré et probable, signes présents, scénario hybride, leviers de bifurcation. |
| 3 | Quelles forces ont façonné nos croyances ? | `parcours-croyances-pratico-inerte-cible/` | Objet, capacité, instruction implicite, croyance, règle consciente, système, Trace. |
| 4 | Pourquoi sommes-nous paralysés ? | `parcours-paralysie-psychokernel-cible/` | Récits Source/Néant, choix du guide, deux séquences libres des cinq cartes, boucle PsychoKernel, niveaux de discernement. |
| 5 | Comment nous réveiller ? | `parcours-reveil-mobilisation-cible/` | Trois actions ordonnées et lecture contextuelle de leurs effets sur la mobilisation. |

Le portage doit partir des faits serveur existants. Toute route, preuve, attribution ou donnée
manquante doit être demandée au portable au lieu d'être inventée dans la vue.

## 2. Mini-jeux M0 disponibles sur `zegame-prototypes/origin/main`

### Éveil des six Puissances

- Dossier : `devoilement-emotion-cible/`
- Historique final : jusqu'au commit `5ab49fe`
- Fichier de contrat : `devoilement-emotion-cible/README.md`
- Structure : **Éprouver → Relier → Retrouver**, trois verbes et figures d'incarnation, activation
  dans la Boussole.
- Variantes : Désir, Volonté, Imagination, Émotion, Communication, Intuition.
- Transcendance reste hors de ce patron polaire.

### Premier cap et dévoilement de Transcendance — E14

- Dossier : `cap-transcendance-m0-cible/`
- Commit complet : `8b4bd79`
- Fichier de contrat : `cap-transcendance-m0-cible/README.md`
- Structure : **Choisir → Lire → Orienter → Relier**.
- La sélection d'une Puissance n'est pas une preuve. La validation attend une évaluation achevée et
  l'enregistrement d'un cap valide sur le même slug.

### Carte du Seuil — E19

- Dossier : `carte-du-seuil-m0-cible/`
- Commit : `e54e5de`
- Fichier de contrat : `carte-du-seuil-m0-cible/README.md`
- Structure : relire la Graine, choisir au moins une Trace réelle, prévisualiser, sceller.
- Le scellement et la preuve `m0-carte-scellee` doivent être écrits atomiquement. Une visite, une
  prévisualisation ou une sélection vide ne valide rien.

## 3. Nouvelles maquettes M0 validées par Boris, encore locales

### L'écosystème Point Zéro — E8

- Branche locale : `codex/ecosysteme-point-zero-m0-v2`
- Commit : `98f212e`
- Dossier : `ecosysteme-point-zero-m0-cible/`
- Chemin complet :
  `C:\Users\pro\Dropbox\Boris\Point Zero 2050\Vibe Coding\.codex-tmp\zegame-prototypes-ecosysteme-m0-20260919\ecosysteme-point-zero-m0-cible\`
- Écrans : `need`, `relays`, `flow`, `result`.
- Geste : partir d'une Graine réelle, choisir deux ou trois relais, nommer ce qui circule et le
  prochain mouvement, puis enregistrer la constellation comme Trace privée.
- Les cartes de démonstration ne constituent pas un registre canonique et aucune action sociale ne
  doit être produite implicitement.

### Conseil Oméga — circulation et futurs évités

- Branche locale : `codex/conseil-omega-circulation-cible`
- Commit : `71ef441`
- Dossier : `conseil-omega-circulation-cible/`
- Chemin complet :
  `C:\Users\pro\Dropbox\Boris\Point Zero 2050\Vibe Coding\.codex-tmp\zegame-prototypes-conseil-omega-20260920\conseil-omega-circulation-cible\`
- Structure : prologue 2040 ; constellation et treizième siège ; lecture des crises ; choix parmi
  les six Puissances ; archive dystopique propre à chacune ; réouverture de la circulation ;
  conséquence éditoriale ; Atlas.
- Une seule archive explorée suffit pour ouvrir la conclusion. Les cinq autres restent accessibles.

Ces deux branches locales sont complètes et vérifiées, mais pas encore poussées. Ne pas les intégrer
silencieusement : attendre l'ordre de Boris, puis demander leur publication si le travail commence
sur un autre poste.

## 4. Avant le Zéro — réserve éditoriale sans prototype

Pistes retenues pour enrichir le LDVELH :

- initiation à l'ayahuasca puis voie chamanique ;
- expérience de mort imminente puis accompagnement au sein des « Conscients » ;
- découverte du plan implicite/explicite par la physique et soupçon d'une réalité simulée ;
- individuation radicale hors des collectifs.

Aucun dossier cible n'existe encore. Il ne s'agit pas d'un fichier manquant : les embranchements
complets doivent d'abord être écrits à partir du corpus actuel d'Avant le Zéro.

## 5. Références communes

- `bandeau-excursion-progression-cible/` : bandeau excursion validé, seconde ligne sombre
  `#20101f`.
- `parcours-lineaire-m0-cible/` : chemin de fer des étapes et reçu d'Omégas de fin d'Expérience.
- Les sélecteurs noirs, paramètres d'URL de démonstration et données fictives ne vont pas dans Rails.
- La preuve serveur, l'idempotence, l'accessibilité, la reprise et le retour à la fiche restent
  obligatoires lors du portage.
