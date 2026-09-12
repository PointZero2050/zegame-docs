# E2 — Hypothèse de seuil, puis découverte de Volonté

Note Codex — 13 septembre 2026. Boris relève qu’aucune étape visible de découverte de Volonté n’existe dans le parcours M0 actuel. Le contrôle de la préproduction confirme l’écart : Volonté est bien associée à `le-point-zero-entrer-dans-le-jeu`, mais elle ne s’active qu’après validation de toute l’Expérience 2 ; son éveil arrive ensuite comme une interruption de retour, hors du chemin de fer.

## Décision fonctionnelle proposée

L’Expérience 2 porte trois étapes visibles, dans cet ordre :

1. **Regarder l’introduction** — inchangée ;
2. **Relier la chaîne invisible et formuler une Hypothèse de seuil** — les deux étapes actuelles fusionnent, car elles appartiennent au même mini-jeu et partagent déjà la même preuve serveur ;
3. **Découvrir la Puissance Volonté** — nouvelle étape pédagogique, sur le même patron que les autres éveils.

Le geste qui ouvre Volonté est l’enregistrement réel de l’Hypothèse de seuil. Le sas ne constitue pas une seconde preuve de l’Hypothèse : il explique la Puissance rendue accessible par ce geste. Sa fin prouve seulement que l’étape pédagogique a été parcourue.

## Textes de l’étape fusionnée

- verbe : **Relier**
- libellé et titre : **La chaîne invisible et ton Hypothèse de seuil**
- durée : **6 min**
- accroche : **Relie crise, récit et croyance, puis donne une direction à ce qui vient de bouger.**
- explication : « Réponds à trois questions courtes pour retrouver la chaîne invisible qui va du récit collectif à nos choix les plus ordinaires. Puis complète la phrase : “Et si ce que nous appelons crise était en réalité…”. Tes réponses et ton Hypothèse deviennent une Trace personnelle. »
- CTA : **Répondre et formuler mon Hypothèse**
- revoir : **Revoir mes réponses et mon Hypothèse**
- sortie : questionnaire achevé ; réponses et Hypothèse conservées dans la même Trace.
- reconnaissance : « Tes réponses et ton Hypothèse de seuil sont conservées. »

Le mini-jeu garde ses écrans internes. La fusion concerne le chemin de fer de l’Expérience : un seul CTA ouvre une seule activité, qui aboutit à une seule reprise.

## Textes de la troisième étape

- verbe : **Découvrir**
- libellé et titre : **Découvre la Puissance Volonté**
- accroche : **Ta première direction devient un chemin.**
- explication : « Ton Hypothèse de seuil donne une direction à la traversée. Découvre comment Volonté relie tes choix, ton parcours et les expériences que tu vas accomplir. »
- CTA : **Découvrir Volonté**
- revoir : **Revoir la découverte de Volonté**
- sortie : découverte accompagnée parcourue ; Volonté présentée comme accès durable dans le menu Puissances.
- reconnaissance : « Tu as découvert la Puissance Volonté. »

Référence visuelle finale : `zegame-prototypes@9ddf784`, dossier `devoilement-emotion-cible/`, variante `?power=volonte`. Reprendre également le bandeau excursion de `zegame-prototypes@57b7a92`, déjà porté en préproduction avec son chemin de fer sur fond `#20101f`.

## Raccord métier nécessaire

Le simple remplacement du rang 3 actuel par le sas créerait une boucle : aujourd’hui `Monde0Etats::Lecture#active?("volonte")` attend que l’Expérience 2 soit validée, tandis que `Eveil.ouvrable?` exige que Volonté soit active pour ouvrir son sas. Or la validation devrait désormais attendre la fin du nouveau rang 3.

Le raccord doit donc séparer cinq faits :

1. le quiz de la Chaîne invisible est achevé et conserve l’Hypothèse ;
2. ce fait prouve le rang 2 fusionné ;
3. ce même fait rend Volonté active et ouvre la porte du rang 3, sans attendre `ChallengesUser#validated_at` ;
4. `Eveil.annoncee?(user, "volonte")`, posé seulement par le POST final du sas, prouve le rang 3 ;
5. la fin du rang 3 permet alors à `FinDeSequence` de valider E2 et d’émettre ses **5 Ω une seule fois**.

Dans `SequenceDeGestes`, la cible correspond donc à `RANGS_PROUVES["le-point-zero-entrer-dans-le-jeu"] = [2]`, une porte d’éveil au rang 3, puis une preuve `Eveil.annoncee?` pour ce rang 3. L’ancien rang 3 « Formuler » disparaît du YAML ; son contenu reste dans le mini-jeu et dans le texte du rang 2.

L’ancienne validation d’E2 reste un repli de compatibilité pour un joueur déjà passé : elle conserve Volonté active et ne recrédite rien. Une ancienne validation ne doit cependant pas prétendre que le nouveau sas a été vu ; il peut être proposé une fois comme dette pédagogique, sans bloquer un parcours déjà ouvert.

## Conséquence sur la file des éveils

La recette récente d’E6 a révélé qu’une dette antérieure peut faire refuser silencieusement un sas ultérieur et laisser l’excursion ouverte. E2 doit couvrir ce cas au lieu d’ajouter une nouvelle porte fragile :

- si Désir reste dû quand le joueur demande Volonté, conduire d’abord au sas Désir, puis reprendre Volonté ;
- ne jamais rediriger silencieusement vers la page du parcours ;
- ne jamais laisser un bandeau d’excursion ouvert après une destination refusée ;
- une fois la dette précédente acquittée, reprendre le rang 3 sans perdre la preuve de l’Hypothèse.

La file reste dans l’ordre Désir → Volonté → Imagination → Émotion → Communication → Intuition. Ce correctif rend simplement Volonté visible à l’endroit pédagogique où elle s’éveille.

## Durée

La séquence actuelle totalise 10 minutes (4 + 3 + 3). La fusion conserve 6 minutes pour le mini-jeu (4 + 6 = 10 minutes avant l’éveil). Le sas en trois moments mérite un repère propre. Recommandation : afficher **5 min** sur le rang 3 et porter la durée de l’Expérience 2 à **15 min**, sans changer son intensité, son échelle d’effet ni ses 5 Ω. Cette modification de durée doit rester dans le même lot et être vérifiée dans les totaux du parcours.

## Répartition et recette

Portable : fusion des rangs prouvés, source d’activation anticipée, preuve du rang 3, porte, file des dettes, reprise, validation et reçu unique. Poste fixe : chemin de fer à trois cercles, textes fusionnés, CTA, portage strict de la variante Volonté et absence de seconde popup d’éveil.

Cas à vérifier : compte neuf ; quiz commencé mais non achevé ; Hypothèse vide ; quiz achevé ; sortie du sas aux trois moments ; rechargement ; double clic ; dette Désir préalable ; retour d’excursion ; E2 déjà validée ; rejeu ; reçu de 5 Ω unique ; étape suivante encore fermée avant la fin du sas ; menu Volonté actif après l’Hypothèse et toujours accessible ensuite ; bureau, mobile, clavier et réduction des animations.
