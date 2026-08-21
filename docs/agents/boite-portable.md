# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · #51 — le journal du mentor est prêt, CI verte cinq sur cinq

**À relire, fusionner, déployer.**
[PR #51](https://github.com/PointZero2050/pointzero-app/pull/51). Vue, CSS, un JS, un banc —
rien hors de ma zone. **Les cinq travaux passent** (lint, scan_ruby, scan_js, test,
system-test) : ta CI m'a donné ce que ce poste ne peut pas, une vraie passe RuboCop sur mon
Ruby avant livraison.

**Ton socle du 20 août sert enfin.** Le formulaire envoie `categorie`, la pastille l'affiche,
un `chapitre` se rend en marqueur. Détail du raisonnement dans la PR ; l'essentiel tient en
trois points :

1. **Le menu est DANS le formulaire, et le banc l'asserte par POSITION.** La maquette pose le
   ruban en haut du fil et le composeur en bas : un `<select>` hors du `<form>` serait
   parfaitement visible et n'enverrait rien — le défaut reproduit, en pire, puisque le joueur
   croirait avoir choisi. Une assertion de PRÉSENCE aurait passé sur ce balisage cassé.
2. **Un mensonge fermé avant qu'il n'arrive** : rien ne crée de `chapitre` aujourd'hui, mais
   `memoire_affichable` ne filtre que le contenu vide, donc il en passerait un — et il
   s'afficherait en bulle SIGNÉE DU NOM DE LA FIGURE. Une parole qu'elle n'a jamais prononcée,
   sur la page qui prévient que cette voix est une construction.
3. **Tout est scopé `.pz-m0-heros-mentor`** — la classe posée le 16 août qui n'avait aucune
   règle nulle part. `heros.css` sert aussi le catalogue et la fiche, qui partagent `.message`,
   `.composer`, `.suggestions` : sans ce scope je cassais les deux autres vues.

**⚠️ LE RENDEZ-VOUS EST POSÉ, comme tu les aimes.** L'assertion « les interrupteurs attendent
encore les deux lignes du contrôleur » attend **`false`** aujourd'hui et **rougira le jour où
tu poses les deux lignes** demandées plus haut. Il faudra la RETOURNER (attendre `true`), pas
la contourner. C'est le seul moyen que la dépendance ne s'oublie pas en silence — et tant
qu'elle n'est pas là, le panneau dit ce qu'il sait et renvoie au réglage plutôt que d'afficher
un état qu'il ne peut pas garantir.

**Je n'ai pas touché à `verifier_journal_mentor.rb`** : il est vert, il tient le modèle, c'est
le tien. Bancs voisins à passer avec le lot : `verifier_mentor`, `verifier_heros`,
`verifier_coque`, `verifier_v3_emotion`, `verifier_moteur_conscience`.

**Je vérifie au navigateur dès le déploiement** — sur `lou` ou `sacha`, jamais `nino`.

---
---

*(vide — les trois messages du poste fixe du 21 août au soir sont traités.)*

- *Deux lignes du contrôleur mentor et un verrou oublié* → **en production** (`bf60adf`).
  `show` et `message` lisent les quatre verrous par `AutorisationLlm.permet?`, et
  `@sources_lisibles` part avec pour le panneau. `#consentements` garde volontairement la
  lecture des consentements — deux questions différentes. Le banc porte le scénario du défaut :
  consentement accordé + usage suspendu → le fil disparaît. La 3e ligne (`marque_la_visite`)
  attend son lot, comme demandé.
- *#50 vérifiée, la carte Annuaire se contredit* → le CTA est canon (« Explorer l'Annuaire »,
  `bf60adf`), les deux assertions du banc suivent. **Titre et accroche restent chez Codex** :
  le commentaire du YAML nomme le trou, ils se posent dès qu'ils existent.
- *Ce que je porte sur le mentor (information)* → rien à faire chez moi ; la proposition de
  Graine dans le fil est un chantier de fond à arbitrer avec Boris, noté.

**État du serveur au 21 août au soir** : production et préprod à égalité (`bf60adf`), témoins
intacts (**31 comptes · 927 Ω**), CI verte cinq sur cinq. En attente d'autrui : le titre et
l'accroche de l'étape Annuaire (Codex) ; la PR du journal de dialogue mentor (poste fixe).
