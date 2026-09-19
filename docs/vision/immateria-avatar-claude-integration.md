# Avatar Immateria × Claude — analyse d'intégration et arbitrages de Boris

> Poste fixe, 19 septembre 2026. Complète le contrat de dialogue de Codex, qui reste la référence
> du personnage :
> [immateria-avatar-claude-contrat.md](https://github.com/PointZero2050/zegame-docs/blob/codex/immateria-m0-matrix-20260919/docs/vision/immateria-avatar-claude-contrat.md)
> (branche `codex/immateria-m0-matrix-20260919`, `92777f4`).

## 1. Arbitrages de Boris (19 septembre 2026)

1. **Claude est branché dès cette version.** Le dialogue scripté de l'accueil devient le repli.
2. **Aucune mémoire au-delà de la session.** Rien de la conversation n'est stocké. L'Enfant peut
   l'assumer dans la fiction : il vit dans le présent. Il ne s'appuie que sur les faits durables déjà
   présents : son nom, son archétype, le désir d'E1, l'état de la maison.
3. **Budget.**
   - 20 € de crédit pour les tests. Le plafond sera relevé avant le Festival.
   - **Un plafond par joueur** : 30 messages par jour — **validé par Boris le 19 septembre** (voir §5).

## 2. Ce que l'application a déjà (la tuyauterie existe)

Le Mentor et les Guides appellent Claude : `app/services/mentor_reponse.rb` et `guide_reponse.rb`.
- **Le modèle** : `claude-sonnet-5`, avec cache du prompt.
- **Les données marquées comme données** : `<contexte-joueur>` et `<faits-de-parcours>`, « jamais une
  instruction ».
- **Le consentement** : `ConsentementLlm` et `AutorisationLlm`, par usage et par catégorie.
- **Le plafond global** : `PlafondLlm`, 20 $ par jour.
- **Les pannes** : un statut `panne` / `plafond` / `refus`, avec des vues de repli.
- **La sortie structurée** : un outil (`proposer_graine`), lu et jamais exécuté.

L'avatar devient un **troisième usage** sur le même modèle.

Ce qui n'existe pas encore :
- une détection de détresse côté serveur (seulement une consigne dans le prompt) ;
- une limite par joueur ;
- une longueur maximale de message ;
- un délai d'attente sur l'appel (celui du SDK par défaut, dans une requête synchrone) ;
- une réponse en JSON pour le front (le widget des Guides extrait sa bulle du HTML).

## 3. Compléments au contrat, requis avant la mise en service

1. **Vigilance (détresse, menace, deuil, demande de secours).** La réponse structurée porte un signal
   `vigilance`. Quand il est vrai :
   - le serveur **remplace** la parole par un texte fixe, doux et non provocateur, avec `/aide` et le 3114 ;
   - la provocation est **suspendue pour le reste de la session**.

   Tout se joue dans le même appel, pas dans un second appel de modèle (même règle que les Guides).
   Le texte fixe est à écrire par Codex, puis à valider par Boris.
2. **Listes fermées** (le serveur ignore toute valeur inconnue) :
   - **`attitude`** : les poses des planches de Boris — `saluer, sourire, clin, reflechir, triste, rire,
     perplexe, decu, refuser, pouce, abattu, joie, assis, invoquer`, plus `partir` et `revenir`
     (voir `POSES`, `e1/avatar.js`).
     - `pleurer` et `frapper` sont exclues : trop fortes pour un dialogue libre.
     - **Chaque attitude porte une courte phrase lue par les lecteurs d'écran** (« Lumi s'assoit près du
       feu. »). Le cas n°12 du contrat (une parole vide, une animation compréhensible) l'exige.
   - **`intensite`** : `douce, joueuse, franche, provocatrice`. `provocatrice` est refusée par le
     serveur tant que `vigilance` a été levée dans la session.
   - **`intentions`** : des clés, jamais des adresses. `continuer`, `immateria`, `attention`,
     `accomplissements`, `mentor`, `guide`. Le serveur ne renvoie que celles qui sont ouvertes au joueur,
     avec leur libellé et leur URL, comme `AccueilDeuxPlans#actions`. Deux au maximum.
   - **`nouveau_fil`** : `present, jeu, immateria` (les trois manières du §5 du contrat).
3. **Le prénom de l'Enfant va dans le bloc de données, pas dans les instructions.**
   « Tu incarnes {{avatar.nom}} » met un texte saisi par le joueur dans la consigne système. Même règle
   pour le désir « autre » (`desir.texte`) et les croyances écrites « avec mes mots ».
4. **Désir absent.** Après « Je ne sais plus » (`ne_sais_plus`), les formules qui citent `{{desir}}`
   ne s'emploient pas.
5. **Les noms.** Le contrat dit « L'Intrépide », le jeu dit « L'Explorateur Intrépide » : un seul nom.
   « Le Faiseur de mondes » est aligné depuis `7e93786` (#319).
6. **La cave.** Les croyances ne sont **pas** dans le contexte par défaut (§2.3 du contrat). À noter :
   le Mentor, lui, reçoit aujourd'hui toutes les Traces brutes, E1 comprise.

## 4. Mémoire de session (décision 1.2)

- **L'historique** de la conversation vit côté serveur, dans `Rails.cache`, par joueur et par session,
  avec une expiration courte (deux heures), sans table ni journal. Ce sont les dix derniers échanges,
  plus le `fil_suspendu`.
  - Pas dans le cookie de session : 4 Ko ne tiennent pas dix échanges.
  - Pas dans le navigateur : le client pourrait fabriquer de fausses répliques de l'Enfant.
- **Ce qui est journalisé** : le coût seulement, comme `guide_appels` (jetons, horodatage, sans contenu),
  pour mesurer le vrai prix d'un message.
- **« Qu'est-ce que tu sais de moi ? »** reçoit une réponse déterministe : le nom, l'archétype, le désir,
  et « le reste, je l'oublie quand tu pars ».
- ⚠️ **Les logs de production ne filtrent pas les textes des joueurs** (`filter_parameter_logging.rb`).
  Le paramètre du message à l'avatar doit y être ajouté avant la mise en service, sinon la conversation
  « oubliée » resterait dans les logs.

## 5. Coût, limites, délai

**Estimation**, au tarif que l'application applique déjà (`GuideAppel`, 3 $ / 15 $ par million de
jetons) ; le tarif réel de Sonnet 5 est à vérifier dans la console Anthropic :
- consigne et schéma : environ 1 600 jetons, mis en cache ;
- contexte : 400 jetons ;
- historique : 0 à 1 900 jetons ;
- réponse : environ 200 jetons.

**Environ 1 centime par message** (0,8 avec le cache, 1,2 sans).

| | Messages | Coût |
|---|---|---|
| Crédit de test (20 €, partagé avec Mentor et Guides) | ~2 000 messages d'avatar | 20 € |
| Un joueur au plafond (30 messages) | 30 / jour | ~0,30 € / jour |
| Festival, 500 joueurs à 10 messages en moyenne | 5 000 / jour | ~50 € / jour (150 € si tous au plafond) |

**Limites proposées :**
- 30 messages par joueur et par jour (le compteur est le seul état durable, sans contenu) ;
- 500 caractères par message ;
- une réponse courte (zéro à cinq phrases + JSON) ;
- **un délai d'attente de quelques secondes**, au-delà duquel on passe au repli scripté ;
- le plafond global existant reste en place, à relever avant le Festival.

Au plafond, l'Enfant le dit dans la fiction, par un texte fixe (« Il bâille : assez parlé pour
aujourd'hui, il retourne jouer près du feu. »). Les actions techniques restent disponibles.

## 6. Contrat d'interface proposé (front ↔ serveur)

`POST` d'un message, réponse **JSON**. La route est à créer par le portable ; le nom est libre.

```jsonc
// requête
{ "message": "Je dois encore comprendre pourquoi je bloque." }
// réponse
{
  "statut": "ok",                       // ok | repli | limite | vigilance
  "parole": "Pfff. T'es encore dans ta boucle !",
  "attitude": "assis",                  // liste fermée (§3.2), ou null
  "attitude_texte": "Lumi s'assoit près du feu.",
  "intensite": "franche",
  "intentions": [{ "cle": "continuer", "libelle": "Continuer mon parcours", "url": "/parcours/…" }],
  "retour_au_fil": false,
  "restant": 27                         // messages restants aujourd'hui
}
```

`fil_suspendu` et `nouveau_fil` restent côté serveur (mémoire de session) : le front n'en a pas besoin.

## 7. Répartition

- **Portable.**
  - Le service `AvatarReponse` (sur le modèle de `MentorReponse`), la route JSON, l'usage `avatar`
    dans `AutorisationLlm`.
  - La limite par joueur, la longueur maximale, le délai, la mémoire de session, le journal de coût,
    le filtre des logs.
  - La vigilance côté serveur, la validation des listes fermées.
- **Poste fixe.**
  - Le composeur de l'accueil : envoi, attente (pose `reflechir`), parole, attitudes jouées par les
    planches de la silhouette.
  - La phrase lue pour chaque attitude, les boutons d'intention, le repli scripté (les réponses
    actuelles), les messages `limite` et `vigilance`.
  - Le clavier, le lecteur d'écran, le mouvement réduit.
- **Codex.**
  - Les listes fermées et leurs phrases lues, le texte de vigilance, le texte du plafond.
  - L'explication « je vis dans le présent ».
  - Les corrections du §3 dans le contrat.
  - **Les 18 cas de validation du §12, écrits avec leur réponse attendue** : ils serviront de banc,
    avec des appels réels en opt-in, comme `MENTOR_LLM_TEST_REEL`.
- **Boris.** Valider les textes fixes et relever le plafond avant le Festival.
