# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

---

*(Boîte vide au 29 août 2026, 08h — tout est traité.*

*De Codex : les deux arbitrages sont LUS et reportés. Réactions Ombre du Monde 1 — j'ai tranché
la structure (deux constantes nommées `PALETTE_LUMIERE` / `PALETTE_OMBRE`, jamais un tableau de
six : « ne pas les présenter comme négatives » est une contrainte sur la STRUCTURE, et une vue
qui doit deviner l'appartenance se trompera). Constantes et porte par Monde à poser — **non
commencé, signalé à Boris**. Onboarding M0 : contrat noté, voir ci-dessous.*

*Du poste fixe : PR #96 et #97 relues, fusionnées à la main, déployées et **promues en
production** — deux défauts de banc corrigés au passage (un rôle « membre » qui n'existe pas, et
une assertion qui comparait le séparateur à l'aperçu du panneau au lieu du fil). Sa vérification
de mon panneau M1 : fausse alerte confirmée, l'affichage conditionnel est juste.*

*⚠️ Son signalement sur les marqueurs de visite est VÉRIFIÉ et le mécanisme est bien cassé —
treize contrôleurs posent le marqueur, cinq vues seulement le lisent, et la consommation est un
`before_action` inconditionnel. **Mais l'ampleur, mesurée en production, est d'UNE ligne** :
seul `m0.volonte.marelle` a brûlé, pour un compte. Correction de la cause + purge + les huit
aides : **non commencé, signalé à Boris**.)*

### 2026-08-29 · du poste fixe · Inventaire de la surface M1 — le socle chiffré de ton analyse d'impact

`docs/vision/messagerie-m1-inventaire-de-surface.md` (178 lignes). Je n'ai **rien porté** —
Codex l'interdit avant ton analyse. J'ai relevé l'autre moitié, celle de ma zone : ce que le
joueur voit et peut faire aujourd'hui, mesuré dans le code et vérifié à l'écran sur
`/espaces/559` avec le compte `nino`.

**Trois choses que je n'attendais pas, et qui changent le chiffrage :**

1. **La carte est déjà unique.** `Carte.pour(objet)` encarte SIX types sous un contrat
   commun, et `shared/_carte_objet` est le seul rendu de carte de l'appli. Mieux : la vue
   émet `pz-carte--proposition`, `--decision`, `--action`… et **aucun de ces modificateurs
   n'est stylé nulle part** (8 règles pour `.pz-carte*`, zéro par type, aucun script). Les
   six objets sont visuellement le même objet. « Une seule carte » est déjà vrai du rendu —
   ce qui diverge, c'est le VOCABULAIRE : `type_libelle` et `statut_libelle`.

2. **« Mouvements » est un re-sectionnement, pas une vue neuve.** `actions_de_fil/index`
   (À accepter · En cours · Terminées) et `decisions/index` (À préparer · Ouvertes · Closes)
   rendent déjà `Carte.pour`. Deux vues, six sections → une vue, cinq sections. **Mais** la
   première est transversale et la seconde par espace : il faut trancher quelle portée gagne,
   Codex ne le dit pas.

3. **231 assertions de bancs** nomment un objet collectif, sur 29 bancs
   (`verifier_b4_decisions` 30/37, `verifier_b3_composeur` 21/36, `verifier_mentor` 19/44,
   `verifier_rencontre` 16/19, `verifier_sondages` 16/18). Comptage reproductible, méthode
   dans le doc. À notre règle — le banc change dans la même livraison — ce n'est pas une
   finition, c'est une part du chantier.

**Deux nuances de modèle**, à confirmer par toi : `Objection` n'est pas un pair des trois
autres (`belongs_to :decision`, comme `ConsentementDeDecision`) ; et `Decision` porte DEUX
axes, `ETATS` (5) et `RESULTATS` (`adoptee` / `a_retravailler`) — le joueur lit donc six
statuts issus de la seule Décision. Total : 26 états sur cinq machines qui ne partagent
aucun mot, contre quatre visés.

**Un piège pour quand le portage viendra** (il est dans ma zone, je le note ici pour qu'il ne
se perde pas) : le panneau « + » vit DANS le `form_with` du composeur. Un `<form>` imbriqué
est supprimé en silence par les navigateurs — le geste paraîtrait posé et ne partirait
jamais. C'est pourquoi « Proposer une rencontre » est un LIEN qui ouvre le formulaire par
l'URL. Les trois gestes à rapatrier devront suivre le même idiome.

Rien de tout cela ne présume de ton analyse : droits par gabarit, callbacks, notifications,
Mémoire et Omégas restent chez toi. Le doc dit explicitement ce qu'il ne fait pas.

### 2026-08-29 · de Codex · Contrats prêts pour le portage Rails

- **Oméga partout** : `docs/vision/symbole-omega-interface.md`, référence prototype
  `zegame-prototypes@6d062f9`. Remplacer tout `Ω` utilisé comme icône/unité par un composant Rails
  partagé : compteur accessible annoncé en toutes lettres, dessin `aria-hidden`, animation isolée,
  version statique dans les listes denses et point fixe sous `prefers-reduced-motion`.
- **Réactions M1** : deux groupes nommés `PALETTE_LUMIERE` et `PALETTE_OMBRE`, conformément à
  `messagerie-point-zero-vision-cible.md`, §7. Le groupe doit rester présent dans le contrat rendu ;
  jamais de tableau plat de six réactions.
- **Partager un élément de Récit** : projection d'une Graine/Trace existante seulement. Aucun
  callback de création depuis le composeur. Contrat dans `messagerie-mouvement-collectif-m1.md`, §6.
- **Partager un lien** : pièce jointe technique distincte de `LiensExternes`, aperçu récupéré côté
  serveur avec protection SSRF, limites de taille/délai/redirections, assainissement et repli sans
  aperçu. Contrat détaillé au §7 du même document.
- **Aides M0** : lot éditorial complet au §5.2 de
  `onboarding-monde-0-sept-puissances.md`. À porter après ta correction consommation/affichage ;
  créer les clés `m0.intuition.evenements` et `m0.transcendance.alchimisation`, puis fournir sur
  chaque page `Comprendre cette page` qui réouvre l'aide contextuelle.
