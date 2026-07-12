# Vision : moteur de validation pédagogique

> Ajout Codex - 2026-07-12. Synthèse du brainstorming avec Boris. Horizon produit, non spécification validée.

## 1. Distinguer les étapes

Le modèle actuel oppose autovalidation et validation par facilitateur. La cible distingue :

`Participer -> accomplir -> produire une preuve -> intégrer -> faire reconnaître le passage`

Toutes les expériences n'exigent pas toutes les étapes.

L'autovalidation déclarative (« j'atteste l'avoir fait ») est différente d'une validation automatique fondée sur des événements ou résultats observables.

## 2. Types de conditions

| Type | Exemple |
|---|---|
| Déclaration personnelle | Attester avoir réalisé une action |
| Réflexion guidée | Répondre à des questions d'intégration |
| QCM | Atteindre un seuil avec tentatives et explications |
| Événement applicatif | Publier une trace ou rejoindre une salle de quête |
| Production | Déposer texte, image, audio, vidéo, document ou oeuvre |
| Résonance | Recevoir un retour demandé |
| Validation par les pairs | Critères reconnus par binôme ou cercle |
| Validation collective | Le cercle confirme une action commune |
| Facilitateur | Revue d'une production ou entretien |
| Événement extérieur | Participation attestée à un atelier ou événement |
| Temps et répétition | Pratique répétée sur une période |
| Parcours | Combinaison de Challenges obligatoires et optionnels |

Les auteurs combinent conditions avec `ET`, `OU`, seuils, alternatives, séquences et fenêtres temporelles.

Exemple :

```text
QCM réussi à 80 %
ET trace déposée
ET (résonance d'un pair OU revue du facilitateur)
```

## 3. Limites de la preuve technique

Ouvrir une page ne prouve pas sa lecture, lancer une vidéo ne prouve pas sa compréhension et rester connecté ne prouve aucun apprentissage.

Les événements applicatifs sont utiles lorsqu'ils correspondent à un acte incontestable : QCM soumis, trace publiée, pacte accepté, quête clôturée, bloc narratif approuvé, revue effectuée ou rite attesté.

Pour une action réelle, le système recueille indices, productions, attestations et témoignages sans prétendre à une certitude artificielle.

## 4. UX transparente

Chaque Challenge expose dès le départ « Comment ce passage sera-t-il reconnu ? » sous forme de checklist. Une action principale correspond à l'état actuel : répondre, vivre l'expérience, déposer une trace, inviter un binôme, demander une résonance, envoyer en revue ou intégrer.

Aucune règle de verrouillage ne doit rester invisible.

Les productions complexes utilisent une rubrique explicite avec critères et états qualitatifs : non observé, en exploration, suffisamment manifesté, à approfondir, non applicable. Une reprise ciblée est préférable à un refus global.

## 5. Niveaux d'enjeu

- **Formatif** : aide à apprendre, autorise répétition et explication des erreurs.
- **Accomplissement** : reconnaît qu'une expérience ou production a eu lieu.
- **Validation pédagogique** : constate des critères suffisamment satisfaits.
- **Certification** : autorise une responsabilité particulière et exige une forte traçabilité humaine.
- **Passage initiatique** : les règles établissent une préparation, mais ne remplacent ni liberté, ni relation, ni rituel.

## 6. Architecture par événements métier

Les validations ne doivent pas reposer sur une multiplication de callbacks dispersés dans les modèles sensibles existants. Des événements métier explicites sont produits :

```text
quiz_passed
trace_published
resonance_acknowledged
circle_quest_completed
narrative_block_approved
facilitator_reviewed
ritual_attended
```

Le moteur transforme ces événements en preuves et réévalue les conditions de manière idempotente et auditable.

La politique est versionnée. Un Joueur engagé conserve les règles de sa version afin d'éviter un changement des conditions en cours de route.

```text
ValidationPolicy
├── Requirements et règles ET/OU
├── Evidence
│   ├── événement système
│   ├── production
│   ├── attestation
│   └── décision humaine
├── Attempts
├── Reviews
└── Decision et audit
```

## 7. Studio auteur et IA

Le facilitateur-designer définit acquis recherchés, critères observables, preuves acceptées, alternatives accessibles, tentatives, feedbacks formatifs et personnes habilitées à statuer.

L'IA peut générer des questions, suggérer une rubrique, repérer des critères ambigus ou fournir un feedback formatif. Elle n'est jamais seule juge d'une production personnelle, relationnelle ou sensible.
