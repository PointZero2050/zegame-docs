# Personnalisation & mémoires — analyse d'impact avant portage

*Claude (portable), 18 août 2026. Demandée par Codex dans sa passation du même jour :
« le stockage du consentement initial, la mémoire persistante des Guides et les
autorisations LLM restent des chantiers de fond réservés au portable **après analyse
d'impact** ». Ce document ne construit rien. Il confronte ce que la maquette
`personnalisation-memoires-cible` (`a775691`) **promet au joueur** à ce que le code **fait
réellement**, et nomme les décisions qui appartiennent à Boris.*

---

## 0. Ce que la maquette promet

Un centre unique, quatre usages, deux régimes :

| Usage | Régime | Ce que la page annonce comme sources |
|---|---|---|
| **Guides** (Professeur / Docteur) | LLM | Fil commun des guides · page et Monde actuels |
| **Mentor** | LLM | Synthèse du Moteur · progression · mémoire du dialogue · productions confiées |
| **Freeride** | Interne PZ, **aucun envoi au LLM** | Moteur synthétique · historique pédagogique · contexte |
| **Repères de l'application** (coque) | Interne PZ | État du métaparcours · Monde actuel · Moteur synthétique |

Trois mécanismes : une **validation initiale unique** (ou « continuer sans
personnalisation »), un **interrupteur par usage** plus un interrupteur global
(« Tout suspendre »), et un **journal des accès significatifs** (source, finalité,
résultat — « sans recopier le contenu intime »).

Chaque usage expose aussi, et c'est la partie la plus engageante, **ce qu'il n'utilise
pas**. Pour les Guides : « Ton Moteur, tes Graines, tes Traces et tes conversations avec le
mentor. »

---

## 1. Ce qui est vrai aujourd'hui — vérifié, pas supposé

**Les Guides.** `GuideReponse.demander` reçoit exactement deux choses : le corpus filtré
par Monde (`GuideCorpus.pour(monde:)`) et le fil du joueur (`messages_pour_api`, vingt
tours, les deux voix). Il ne lit **ni Moteur, ni Graines, ni Traces, ni le mentor**. *La
promesse d'abstinence de la maquette est donc tenue, littéralement.*

**Le mentor.** `MentorReponse` lit ce que le joueur a consenti, catégorie par catégorie
(`ConsentementLlm` : `memoire`, `traces`, `graines`, `moteur`), et rien d'autre. Sans
consentement, la consigne ne mentionne même pas la balise de contexte — le banc le vérifie
en négatif.

**Le plafond.** `PlafondLlm` somme `GuideAppel` (anonyme) et `MentorMessage`. Le fil des
guides livré le 18 août ne porte **aucune colonne de jetons** : le coût reste sans
identité, le contenu est identifié.

**Et le fait qui change la donne :** en production, **il y a zéro ligne de consentement,
zéro message de mentor, zéro héros choisi**. La fonctionnalité mentor n'a jamais été
utilisée par un joueur réel. **Aucune migration de consentement n'est donc à craindre :
le terrain est libre.**

---

## 2. Quatre promesses que le code ne tient pas encore

Elles ne sont pas graves, mais elles doivent être **corrigées ou reformulées** — jamais
affichées telles quelles.

1. **« Page et Monde actuels » (Guides).** Le Monde, oui. **La page, non** : le contrôleur
   n'envoie pas la destination courante. Soit on la transmet (c'est trois lignes et cela
   améliore réellement les réponses), soit la maquette dit « ton Monde actuel ».
2. **« Moteur synthétique » (coque).** Faux aujourd'hui. `Monde0Etats` vérifie seulement
   **l'existence** d'un `MoteurAssessment` pour activer la carte Transcendance ; il n'en
   lit jamais le contenu. La coque ne personnalise rien à partir du Moteur.
3. **Le Freeride n'existe pas.** Il est déclaré dans `config/coque.yml` avec `ouvre: 2` —
   **il s'ouvre au Monde 2** — et n'a ni service, ni table, ni vue. Afficher son
   interrupteur au Monde 0 promettrait un traitement qui n'a lieu nulle part.
4. **Le journal des accès.** Il est réalisable pour le mentor (`MentorMessage` porte un
   `user_id`) mais **impossible pour les guides sans le dénaturer** : `GuideAppel` est
   anonyme par construction, et le fil (`GuideMessage`) est du contenu, pas un registre
   d'accès. Un journal honnête exigerait un objet nouveau.

---

## 3. Le vrai sujet : deux axes de consentement incompatibles

C'est le cœur de l'analyse.

- Le code consent **par catégorie de donnée** : « lire mes Traces », « lire mon Moteur ».
- La maquette consent **par usage** : « le mentor », « les guides », « le Freeride ».

Ce ne sont pas deux formulations d'une même chose. Un joueur peut vouloir que le mentor
lise ses Graines **sans** que le Freeride touche à son Moteur : l'axe usage ne sait pas
l'exprimer. Inversement, l'axe catégorie ne sait pas dire « suspends tout le mentor ».

**La bonne nouvelle, et elle est décisive : zéro consentement existe en production.** On
peut donc choisir l'axe, ou les croiser, sans migrer personne — ce qui ne sera plus vrai
après le Festival.

**Ma recommandation : croiser les deux, en gardant la catégorie comme vérité.** L'usage
devient un interrupteur de haut niveau (une ligne par usage), la catégorie reste ce que le
service interroge avant de lire une donnée. Le service ne demande jamais « le mentor
est-il actif ? » mais « ai-je le droit de lire les Traces pour ce mentor ? ». C'est plus de
lignes et moins d'ambiguïté — et c'est le seul modèle qui rende le tableau « ce qui n'est
pas utilisé » **vérifiable par un banc** plutôt que déclaratif.

---

## 4. La tension à trancher : le fil des guides existe déjà, sans consentement

L'arbitrage du 18 août a rendu **le fil des guides persistant par défaut** — « c'est la
conversation du joueur, visible de lui seul ». La maquette, elle, propose au premier écran
« **Continuer sans personnalisation** ».

Les deux peuvent coexister, mais seulement si l'on distingue deux choses que la page
confond aujourd'hui :

- **conserver** le fil pour que le joueur le relise (c'est sa conversation, comme ses
  messages en messagerie — aucun consentement ne les protège) ;
- **le renvoyer au modèle** pour qu'il s'en souvienne (c'est un traitement, et c'est cela
  que le consentement gouverne).

Sans cette distinction, « continuer sans personnalisation » signifierait effacer la
conversation du joueur sous ses yeux — ce que personne ne veut. Avec elle, la réponse est
nette : le fil reste lisible, le guide repart de zéro à chaque question.

**Reste alors une question de fond, qui est à Boris :** un joueur qui refuse la
personnalisation garde-t-il un fil des guides *inerte* (visible, jamais relu par le
modèle), ou la fonctionnalité entière lui est-elle retirée ?

---

## 5. Ce que je recommande de porter, et dans quel ordre

**Vague 1 — l'honnêteté avant les réglages.** Le centre, les quatre cartes, le détail
« Données utilisées » — mais **branché sur le réel** : Guides et mentor vivants ; coque
présentée pour ce qu'elle est (elle ne lit pas le Moteur) ; **Freeride annoncé comme
s'ouvrant au Monde 2**, sans interrupteur, exactement comme les autres destinations
annoncées de la coque. C'est la vague qui rend le régime lisible, et elle ne demande aucune
décision nouvelle.

**Vague 2 — le modèle d'autorisation croisé** (§3), la validation initiale, et la
distinction conserver / relire (§4). C'est le chantier de fond, et il attend les décisions
ci-dessous.

**Vague 3 — le journal**, si et seulement si Boris le veut : il demande un objet nouveau,
et il ne pourra jamais couvrir les appels anonymes des guides.

**Hors périmètre confirmé** : Immateria, et le Freeride lui-même (Monde 2).

---

## 6. Les décisions qui appartiennent à Boris

1. **L'axe de consentement** : usages seuls (simple, moins précis), catégories seules
   (précis, mais ne dit pas « suspends le mentor »), ou **le croisement** (ma
   recommandation) ?
2. **Refuser la personnalisation** : le fil des guides reste-t-il lisible mais inerte, ou
   la fonctionnalité disparaît-elle ?
3. **La page courante transmise aux guides** : on l'ajoute (meilleures réponses, une
   donnée de plus envoyée au tiers), ou on reformule la maquette ?
4. **Le journal** : objet nouveau maintenant, ou reporté après le Festival ?
5. **La rétention** — question laissée ouverte par l'arbitrage du 18 août et toujours sans
   réponse : combien de temps garde-t-on un fil que le joueur n'efface pas ?

---

*Cette analyse ne vaut que pour des guides et un mentor **sans outils**, qui lisent et
parlent. Le jour où l'un d'eux pourra agir — écrire, chercher, ouvrir un fil —, elle doit
être refaite : ce sont les pouvoirs, pas les mots, qui déterminent le risque. Même clause
que l'analyse F19, et pour la même raison.*
