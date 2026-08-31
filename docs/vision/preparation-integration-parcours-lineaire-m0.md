# Préparer l'intégration du parcours linéaire M0

> **Demandée par Boris le 31 août 2026**, après la livraison par Codex de la documentation et des
> maquettes. Rédigée par le poste fixe.
>
> Elle ne refait pas l'analyse d'impact — celle-ci reste dans
> [`analyse-impact-parcours-lineaire-m0.md`](analyse-impact-parcours-lineaire-m0.md) (surfaces,
> bancs, manques) et dans
> [`analyse-impact-parcours-lineaire-m0-serveur.md`](analyse-impact-parcours-lineaire-m0-serveur.md)
> (le portable, listeners réels). **Celle-ci répond à une autre question : par où commence-t-on,
> qu'est-ce qui est déjà là, et qu'est-ce qui bloque quoi.**
>
> Canon : [`pedagogie/monde-0-parcours-lineaire-appropriation.md`](../pedagogie/monde-0-parcours-lineaire-appropriation.md).
> Réponses de raccord de Codex :
> [`reponses-raccord-parcours-lineaire-m0-2026-08-31.md`](reponses-raccord-parcours-lineaire-m0-2026-08-31.md).
>
> ⚠️ **La maquette a bougé depuis son annonce.** Ma boîte annonce `e02793d` ;
> `codex/parcours-lineaire-m0` est à `f719cd0` (« Formalise l'éveil progressif des Puissances »).
> Ce n'est pas un reproche — c'est la raison pour laquelle chaque lot devra **re-relever la
> maquette au moment de le porter**, et non se fier à une mesure faite la veille.

---

## 1. Ce qui est livré

**Sept vues** dans `parcours-lineaire-m0-cible/` : `journey`, `chapter`, `experience`,
`excursion-game`, `excursion-power`, `unlock`, `dashboard`.

**Un canon complet** : la matrice des 20 lignes (§4), la granularité des étapes visibles (§4.1),
l'absorption de l'ancien métaparcours (§5), le workflow d'éveil (§7.1), la règle d'aide (§7.2),
et le contrat des excursions (README de la maquette).

---

## 2. ⚠️ L'état des lieux, mesuré : 14 des 20 existent déjà

Relevé dans `config/journeys/point-zero-monde-0.yml` — **quatorze expériences déclarées**,
confrontées aux vingt lignes de la matrice :

| # | Expérience de la matrice | dans l'application |
|---:|---|---|
| 1 | Façonner mon jumeau | ⚠️ **à créer** |
| 2 | Le Point Zéro : entrer dans le Jeu | ✅ `le-point-zero-entrer-dans-le-jeu` — à restructurer |
| 3 | Le Coupable idéal | ✅ `le-coupable-ideal` |
| 4 | Une drôle d'époque | ✅ `une-drole-d-epoque` |
| 5 | Avant le Zéro | ✅ `avant-le-zero` |
| 6 | Et moi dans tout ça ? | ✅ `et-moi-dans-tout-ca` — à restructurer |
| 7 | Choisir qui marchera à mes côtés | ⚠️ **à créer** |
| 8 | L'écosystème Point Zéro | ✅ `l-ecosysteme-point-zero` |
| 9 | Choisir ma place parmi les autres | ⚠️ **à créer** (absorbe Communication) |
| 10 | Le site du Point Zéro | ✅ `le-site-du-point-zero` |
| 11 | Le signe de reconnaissance | ✅ `le-signe-de-reconnaissance` |
| 12 | Choisir un double regard | ⚠️ **à créer** (absorbe Intuition) |
| 13 | Les choses se précisent | ✅ `les-choses-se-precisent` |
| 14 | Lire mon Moteur | ⚠️ **à créer** (absorbe Transcendance) |
| 15 | Le Conseil Oméga | ✅ `le-conseil-omega` |
| 16 | Découvrir les formats | ✅ `decouvrir-les-formats` |
| 17 | Participer à un Sas Point Zéro | ✅ `le-sas-d-entree` |
| 18 | Vivre l'Atelier Point Zéro | ✅ `vivre-l-atelier-point-zero` |
| 19 | Mon récit de passage | ✅ `mon-recit-de-passage` |
| 20 | Ton espace est prêt | ⚠️ **à créer** (épilogue) |

**Six éléments à créer : 1, 7, 9, 12, 14 et l'épilogue 20.** Les quatorze autres existent, avec
leurs Ω, leurs séquences de gestes et leurs pages.

**La redistribution par chapitre**, elle, est le vrai déplacement :

| | aujourd'hui | cible |
|---|---|---|
| chapitre 1 | 5 | **7** (+ 1 et 7) |
| chapitre 2 | 4 | **7** (+ 9, 12, 14) |
| chapitre 3 | 5 | **5** — les mêmes cinq, seul l'ordre change |

⚠️ **Le chapitre 3 est déjà bon.** C'est une bonne nouvelle de calendrier : le dernier tiers du
parcours ne demande qu'une remise en ordre, pas de création.

---

## 3. ⚠️ Cinq des sept indicateurs n'ont aucune source — réponse à la demande de Codex

Le README de la maquette le demande explicitement : « les indicateurs proposés pour les autres
Puissances doivent être validés au cas par cas selon les données réellement disponibles ».
Mesuré dans `Monde0Etats::Lecture#avancement` :

| Puissance | indicateur proposé | source aujourd'hui |
|---|---|---|
| Désir | quêtes Immateria | ⚠️ **aucune** |
| **Volonté** | parcours actif | ✅ `n/m Actions` |
| Imagination | Graines et Traces | ⚠️ **aucune** |
| Émotion | mentor | ⚠️ **aucune** |
| Communication | échanges et profil | ⚠️ **aucune** |
| **Intuition** | Guides et Ressources | ✅ `n/10 clés` — mais le compteur réel porte sur les **clés**, pas sur les Guides ni les Ressources |
| Transcendance | Moteur, Accomplissements et Omégas | ⚠️ **aucune** |

`avancement` ne connaît que deux cas ; les cinq autres renvoient `nil`. **Une carte activée sans
indicateur n'est pas un défaut d'intégration, c'est une donnée qui n'existe pas.** Chacun des
cinq demande soit une source réelle, soit d'assumer une carte sans chiffre — jamais un nombre
inventé.

---

## 4. ⚠️ Le contrat d'excursion : le vrai mécanisme neuf

C'est la pièce que je n'avais pas vue dans la première analyse, et c'est la plus structurante
après la dérivation d'activation.

> « Toute page ouverte par un CTA d'Expérience conserve l'origine, l'étape, l'événement attendu
> et l'URL de retour dans un contexte persistant côté serveur ou session. »
> « Le retour ne dépend jamais du bouton précédent du navigateur ou du `referrer`. Sans contexte
> valide, le repli neutre est la carte du parcours, jamais une Puissance arbitraire. »

**Rien de tel n'existe.** Aujourd'hui une page d'expérience mène vers une page de territoire et
le retour se fait par la coque. Le contrat demande un **objet de contexte persistant** qui
survit à la navigation, porte l'événement attendu, sait ce qu'est une sortie anticipée
(« à reprendre », rien de validé) et interdit le rejeu de distribuer des Ω.

⚠️ **C'est un préalable serveur, au même titre que la dérivation d'activation** — et il commande
quatre des sept vues (`experience`, `excursion-game`, `excursion-power`, `unlock`). Sans lui,
elles peuvent être dessinées mais pas branchées.

---

## 5. ✅ Ce qui peut partir tout de suite, sans rien attendre

**Le lot de l'aide contextuelle (§7.2).** Il est validé par Boris, indépendant de toute la
migration, et il améliore l'application d'aujourd'hui.

Mesuré : `MarqueDeVisite` pose `@aide_a_montrer = params[:aide].present? || !deja_vue` — la
bulle s'ouvre **automatiquement à la première visite**, sur **20 appels dans 15 contrôleurs**, et
**18 vues** rendent l'aide. Le canon demande deux choses :

1. **ne plus ouvrir automatiquement** — le `|| !deja_vue` disparaît (une ligne, zone portable) ;
2. **garder le `?` près du titre de CHAQUE page**, y compris après le M0 — or seules 18 vues en
   portent un. ⚠️ **L'écart entre « chaque page » et « dix-huit vues » n'est pas mesuré** : c'est
   le premier travail concret de ce lot, et il est chez moi.

C'est le seul lot livrable avant les décisions serveur. Je propose de le prendre en premier.

---

## 6. Cartographie : vue de la maquette → surface de l'application

| vue | surface | état |
|---|---|---|
| `journey` | `app/views/journeys/_show.html.haml` | ✅ existe — à recomposer (aujourd'hui **4 019 px** sur téléphone) |
| `chapter` | `app/views/pages/_show.html.haml` | ✅ existe — portée le 29 août |
| `experience` | `app/views/challenges/_fiche_joueur.html.haml` | ✅ existe — un seul geste, détails sous le pli |
| `excursion-game` | — | ⚠️ **surface neuve** : coque masquée, barre de mission |
| `excursion-power` | — | ⚠️ **surface neuve** : bandeau de contexte sur une page existante |
| `unlock` | — | ⚠️ **surface neuve** |
| `dashboard` | — | ⚠️ **surface neuve** |

**Trois surfaces sur sept existent.** Les quatre autres sont à créer, et trois d'entre elles
dépendent du contrat d'excursion (§4).

---

## 7. Les préalables serveur, rappelés

Ils ne sont pas de mon ressort, mais aucun lot visuel ne peut être juste avant eux :

1. **la dérivation d'activation** — `JourneyProgress` remplace les sept lectures hétérogènes de
   `Monde0Etats` (voir l'analyse du portable) ;
2. **les gardes d'URL** — une expérience non atteinte ne doit pas s'ouvrir par son adresse ;
3. **le contexte d'excursion** (§4) ;
4. **la reconnaissance de fin de tutoriel Immateria**, sans laquelle l'expérience 1 — la
   toute première du parcours — ne peut pas se valider.

---

## 8. Ce que ça coûte aux bancs

Quatorze fichiers de `scripts/` assertent le modèle à sept cartes ou lisent `Monde0Etats`
(détail dans l'analyse d'impact, §6). S'y ajoutent maintenant :

- `verifier_marelle` et `verifier_chaine_m0`, qui gardent l'ordre et la traversée du parcours :
  ils **changent de sujet** quand le parcours devient le Monde 0 lui-même ;
- `verifier_aide_de_page`, qui garde l'ouverture automatique de la bulle — ⚠️ **cette assertion
  doit se retourner**, pas disparaître : elle protégera désormais que la bulle ne s'ouvre PLUS
  toute seule, et que le `?` est présent partout.

---

## 9. Ordre proposé — des lots vérifiables seuls

| lot | contenu | dépend de |
|---|---|---|
| **A** | l'aide contextuelle : plus d'ouverture automatique, un `?` sur chaque page | rien — **livrable maintenant** |
| **B** | la matrice dans `config/journeys` : ordre, chapitres 7/7/5, statut facultatif | arbitrage éditorial des Ω |
| **C** | la dérivation d'activation + les gardes d'URL | portable |
| **D** | `/jeu` rend la vue parcours ; recomposition mobile (4 019 px → un écran) | B, C |
| **E** | le contexte d'excursion, puis `excursion-game` et `excursion-power` | C |
| **F** | l'écran d'éveil + le menu Puissances à quatre états | C, E |
| **G** | le tableau de bord et l'épilogue « Ton espace est prêt » | C |
| **H** | les six expériences nouvelles (1, 7, 9, 12, 14, 20) | B, et le canal Immateria pour la 1 |

**A** ne dépend de rien et vaut pour l'application actuelle. **B** est éditorial et peut avancer
en parallèle de **C**. Tout le reste attend **C**.

---

## 10. Ce qui reste à arbitrer

1. **Les Ω des six expériences nouvelles** restent `à chiffrer`. Le §4 le dit honnêtement ; il
   faudra les fixer avant **B**.
2. ✅ **Le `Signe de reconnaissance` reste facultatif**, confirmé par Boris le 31 août 2026.
   Il rapporte ses Omégas lorsqu'il est accompli et ne bloque jamais l'Expérience suivante.
3. **Les cinq indicateurs sans source** (§3) : source réelle, ou carte sans chiffre ?
4. **Le sort des sept pages de territoire** : le menu Puissances devient-il leur seul accès ?
   (question déjà posée à Codex, sans réponse à ce jour).
5. **La reconnaissance Immateria** : dans le périmètre, ou première version avec un bouton ?
