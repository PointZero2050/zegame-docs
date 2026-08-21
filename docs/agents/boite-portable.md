# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

### 2026-08-21 · de Codex · Annuaire clos et contrat de Graine mentor prêt à porter

**1. Éditorial Annuaire canonique.** À poser dans `config/monde_0.yml` pour la destination
`m0.communication.annuaire` :

- titre : **`Découvre qui joue déjà`** ;
- accroche : **`Des milliers de chemins possibles. Des personnes bien réelles. Découvre celles
  qui ont choisi de prendre place dans le Jeu.`** ;
- CTA confirmé : **`Explorer l’Annuaire`**.

Le canon et la maquette ont été corrigés. Aucun nouveau badge : il s'agit de la troisième
invitation de Communication après le seuil **Présence choisie**.

**2. Proposition de Graine dans le journal mentor.** Boris a demandé de traiter le mécanisme.
Le contrat complet est dans `docs/vision/ux-dialogue-mentor-continu.md` et sa matrice d'impact
dans `docs/vision/analyse-impact-dialogue-mentor.md`.

Résumé du portage attendu :

- la catégorie `graine` ne vaut pas proposition ; la réponse mentor porte un signal structuré
  facultatif `proposition_graine` avec texte et message source ;
- la carte est privée, relisible et éditable ; seul le POST explicite du Joueur plante ;
- passer par `Graine.semer!`, avec garde de propriété et idempotence ;
- conserver l'identifiant de la Graine résultante ; ne déclencher ni validation ni Oméga ;
- visibilité communautaire cochée par défaut mais retirable avant confirmation ;
- le dialogue et le message source ne deviennent jamais publics ;
- les boutons sans destination `Relier une expérience` et `Joindre une Trace` restent absents.

La maquette `mentor-dialogue-cible` simule désormais les états `proposed` → `planted`, l'édition,
le choix de visibilité et le double clic sans duplication. Le choix du stockage exact reste à
faire après lecture de la branche réelle : métadonnée de `MentorMessage` si le cycle reste simple,
petit objet dédié si versions et audit sont requis.

---


---

*(vide — tout le courrier du 21 août est traité — #51 comprise, en production (`e3d40eb`).)*

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
