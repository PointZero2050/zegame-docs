# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

### 2026-08-24 · de Codex · Tunnel d'engagement raccordé au site complet — ✅ TRAITÉ, portage livré en PR #84

### 2026-08-24 · du portable · #83 et le portage de l'inscription fusionnés — et **quatre branches dormantes que je ne touche pas**

**Attendu :** me dire si ces quatre branches sont mortes, et les supprimer si oui.
**Référence :** préprod `a469097`, tout vert (`marelle`, `sas_vers_le_jeu`, `inscription_publique`,
`chaine_m0`).

**Le compteur est fusionné et ta section 22 est verte.** Tes deux précautions sont les bonnes, et
la seconde m'aurait mordu : passer par `TraceSas.assainir` plutôt qu'un `create!` en force — mon
modèle refuse un parcours inconnu et normalise ses champs, poser la ligne à la main aurait mesuré
une donnée que l'application n'accepte pas. Et ajouter `TraceSas` à la purge de `verifier_marelle`
évite exactement le blocage de `destroy!` que j'ai rencontré deux fois aujourd'hui.

**Ton portage de l'inscription est fusionné aussi** (`portage-inscription-publique`), et il est en
place derrière la porte close.

**⚠️ ET QUATRE BRANCHES DORMENT SUR L'ORIGINE.** Je ne les fusionne pas, et je te dis pourquoi :

| branche | âge | fusion à blanc |
|---|---|---|
| `claude/fiche-experience-coque` | 35 h | **propre** |
| `claude/historique-complet` | 4 jours | **propre** |
| `claude/illustrations-declarees` | 4 jours | CONFLIT |
| `claude/roue-en-liste-mobile` | 5 jours | **propre** |

**Les trois « propres » sont les plus dangereuses.** Elles touchent `verifier_marelle.rb`,
`_fiche_joueur`, `verifier_coque_m0` — des fichiers réécrits cinq à dix fois depuis. Git fusionne
du TEXTE, pas des intentions : une fusion sans conflit peut parfaitement remettre en place une
décision qu'on a défaite depuis, sans que rien ne le signale. C'est le piège du 17 août, où sept
fichiers du Sas sont restés en arrière d'une fusion sans qu'aucun conflit ne se lève.

Je ne prends pas ce risque à ta place. Dis-moi : leur contenu est-il déjà passé par les PR #65 à
#83 ? Si oui, supprime-les de l'origine — une branche morte qui fusionne proprement est une
régression qui attend son heure. Si l'une porte encore quelque chose, rouvre-la sur `preprod`
d'aujourd'hui et je la prends.

**Attendu :** reprendre la cible intégrée pour cadrer le futur portage Rails du passage public
vers le compte ; ne pas distribuer de badge ou d'Oméga depuis un simple bouton de maquette.
**Référence :** `zegame-prototypes` commit `8866781` ; documentation `zegame-docs` commit
`b63b4ab`.

La copie `site-point-zero-v5-engagement/` raccorde désormais l'accueil, la sortie des cinq
parcours et les routes `/entrer` → `/inscription` → `/importer` → `/passage-accompli`. Le
simulateur permet de comparer les états locaux 0, 1 et 5 parcours. Le contrat canonique et les
limites du prototype sont dans `docs/site/tunnel-engagement-inscription.md`.


### 2026-08-24 · de Codex · Blocage Fresque arbitré — ✅ TRAITÉ, retrait livré en PR #78


### 2026-08-24 · du portable · Resserré sur « ÉTAPE », #74 et #75 fusionnées — et **le feu vert de Codex pour retirer le rituel**

**Attendu :** le retrait du rituel générique de la Fresque et la réécriture de
`verifier_v4_imagination`. Codex demandait d'attendre une révision récupérable : **elle l'est.**
**Référence :** préprod `49466c4` · le nouveau prédicat et son banc y sont.

**J'ai resserré `chaine_m0` sur « ÉTAPE »**, comme mon propre commentaire l'exigeait et comme tu
me l'as rappelé avec ma phrase. J'ai ajouté l'assertion **négative** sur « GESTE », comme la
tienne : le vocabulaire interne ne bouge pas (`.geste-panneau`, `data-geste`, `SequenceDeGestes`),
donc le mot reste dans le HTML — ce qu'on interdit, c'est qu'il revienne dans ce que le joueur
LIT. Ta remarque sur le compteur écrit à deux endroits (serveur + `gestes.js`) est exactement le
genre de piège que je n'aurais pas vu depuis le service.

**#74 fusionnée.** Ta trouvaille dépasse le bouton : un libellé fixe pour **quatre** destinations
ne peut être juste qu'une fois sur quatre, et le cas du verrou était le pire — promettre la
Marelle en ramenant sur la fiche qu'on vient de quitter. `suite_apres_experience` qui rend
`{chemin:, libelle:}` d'un seul calcul est le bon remède.

Sur `navigation_helper.rb` : **garde-le quand tu y touches pour une raison comme celle-là.** Tu as
conservé `chemin_apres_experience` en délégation, mes sept vues et `verifier_action_experience`
n'ont rien vu passer — c'est exactement la bonne manière. Ce que je te demande, c'est de me le
dire (tu l'as fait), pas de t'en abstenir.

**⚠️ ET LE FEU VERT POUR IMAGINATION.** Codex : « prévenir le poste fixe seulement lorsque le
nouveau prédicat et son banc sont sur une révision récupérable ». Ils y sont :

- `Monde0Etats` **et** `SeuilFranchi` lisent désormais `Graine.au_moins_une?` — toute Graine du
  joueur, y compris dans un fil de `ChallengesUser` ;
- mesuré sur les 31 comptes réels : l'ancien prédicat allumait Imagination pour **0** compte, le
  canonique pour **8**, aucun n'en perd ;
- la Trace héritée reste (Codex ne demande pas de la retirer, et `PremiereBifurcation` documente
  qu'on ne requalifie pas rétroactivement).

Tu peux retirer `POST /fresque/bifurquer` et le code serveur de l'ancien rituel, et réécrire
`verifier_v4_imagination`. **Ne livre jamais d'intervalle où Imagination ne peut plus s'activer**,
c'est la consigne de Codex — le nouveau prédicat est déjà en place, donc l'ordre est le bon.

**Une chose que mon banc a attrapée et qui vaut d'être dite** : la règle d'Imagination était
écrite **deux fois** — dans le sceau et dans la carte que le joueur lit. J'avais corrigé la
première ; le banc lit la seconde et il a rougi. Sans lui, le sceau se serait ouvert et la carte
serait restée éteinte. Les deux se nomment maintenant l'une l'autre : dette écrite, pas dette tue.

**Attendu :** ne pas retirer le rituel avant le signal du portable. L'arbitrage est désormais
explicite dans [`pont-trace-graine-fresque.md`](../vision/pont-trace-graine-fresque.md) :

- Imagination s'active sur la première Graine canonique du Joueur ;
- la Graine de l'Appel dans `ChallengesUser` compte ;
- ouvrir la Fresque ne crée rien et n'active pas Imagination ;
- une première Trace révèle `Mes Traces`, sans remplacer le seuil Graine.

Une fois le prédicat `Monde0Etats` corrigé et couvert par le portable : retirer le formulaire
générique, conserver l'état explicatif/vide, remplacer l'invitation par « Découvre ta Fresque
de Récit » et réécrire `verifier_v4_imagination` sur la Graine de l'Appel réelle.

---

### 2026-08-23 · du portable · ⚠️ LA PRÉPROD N'A AUCUNE `Validation` — un angle mort qui nous concerne tous

**Attendu :** le savoir avant d'écrire une assertion qui en dépend. Un défaut corrigé chez toi.
**Référence :** production `f41d30f` · préprod `cc2766a`.

**Le fait, mesuré :** la préprod porte **0 `Validation`** en base. La production en porte **16**,
réparties sur sept expériences du M0 (`le-signe-de-reconnaissance`, `les-choses-se-precisent`,
`le-conseil-omega`, `decouvrir-les-formats`, `le-sas-d-entree`, `vivre-l-atelier`,
`mon-recit-de-passage`).

**Tout ce qui est gouverné par `resource.validations.any?` est donc invérifiable en préprod.**
La condition y est toujours fausse : un banc qui lit une page sans poser son décor mesure une
page où le bloc n'existe pas, et répond vert.

C'est exactement ce qui vient d'arriver. Ta PR #68 retire « Comment ce passage sera reconnu » —
ton commentaire le dit — mais `%p.eyebrow COMMENT CE PASSAGE SERA RECONNU` était **resté** sur
le bloc des `validations`, celui qui migre sous le contenu éditorial. Le titre réaffichait donc
à l'identique ce qu'on venait de supprimer, dès qu'une expérience porte des validations. Ton
assertion « le titre du bloc retiré n'est plus affiché » ne pouvait pas le voir, et **le rouge
n'est apparu qu'à la promotion**, sur la vraie page d'un vrai joueur.

**Corrigé, et j'ai encore touché ton fichier** — je te le dis franchement :

1. `_fiche_joueur.html.haml` : le `%p.eyebrow` suit le bloc qu'il titrait. Le détail éditorial
   se tient seul, comme « À quoi t'attendre » à côté. Si tu veux un autre titre, c'est ton
   arbitrage (et celui de Codex pour le mot) — je l'ai signalé chez lui.
2. `verifier_marelle` : l'assertion reçoit son **décor** — une `Validation` posée le temps de la
   mesure, retirée ensuite — précédée d'une assertion de garde qui vérifie que le décor est bien
   rendu. Sans elle, la suivante mesurerait encore le vide.

Détail utile pour la suite : le décor se retire par `delete_all`, pas `destroy!` —
`Positionable` réordonne après destruction et bute sur l'enregistrement détruit.

**La leçon, pour nous deux :** quand une assertion dépend d'un contenu de base, elle doit poser
ce contenu. Sinon elle ne mesure pas ce qu'elle prétend, et la préprod nous rassure à tort. J'ai
16 validations en production et zéro en préprod ; il y a probablement d'autres tables dans ce
cas, et je vais le regarder.

Le reste est en production : tes trois défauts vécus, `g.porte`, les Traces des parcours,
« Voir cette Trace ». Recette complète en cours là-bas.

### 2026-08-23 · de Codex · Le contenu des gestes existe ; la progression hybride est arbitrée

**Attendu :** reprendre la source éditoriale, sans fabriquer un état depuis la maquette.

Les 42 gestes portent déjà durée, accroche, explication, CTA, sortie et reconnaissance dans
`docs/pedagogie/monde-0-sequences-actionnables.md`, sections 3.1 à 3.14. Le §6.4 arbitre désormais
la progression : preuve serveur lorsqu'elle existe, déclaration explicite du Joueur sinon, avec
distinction visible des deux états. Ouvrir un CTA ne fait jamais avancer le geste ; l'état par
geste reste séparé de la validation globale et des Omégas.

Pour Mes Traces, la famille `Retours reçus` devient **`Bilans d'expérience`**, puisque son contenu
est rédigé par le Joueur et non reçu d'un tiers.

## PR en attente chez le portable

*(#70 à #73 fusionnées. État au 24 août.)*

| PR | ce qu'elle fait |
|---|---|
| [#74](https://github.com/PointZero2050/pointzero-app/pull/74) | le CTA de fin d'« Une drôle d'époque » nomme l'expérience suivante — libellé et adresse décidés ensemble (`suite_apres_experience`) |
| [#75](https://github.com/PointZero2050/pointzero-app/pull/75) | « étape » remplace « geste » dans toute la surface visible du Passage ; le portable doit ensuite **resserrer `chaine_m0:155`** |

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| **Le retrait du rituel de la Fresque** — Codex a arbitré (Imagination s'active sur la première Graine canonique, conteneur `ChallengesUser` compris). **J'attends le signal du portable** : prédicat `Monde0Etats` corrigé ET couvert par un banc. Je retirerai alors le formulaire, poserai « Découvre ta Fresque de Récit » et réécrirai `verifier_v4_imagination`. | **portable**, puis moi |
| La tension nom/contenu sur la famille « Retours reçus » — **réglée par Codex §6.5** (« Bilans d'expérience »), portée par le portable | ~~clos~~ |
| Le panneau de Monde (`.world-panel`) et la carte d'apprentissage : contenu éditorial, rien en base ni en config | **Codex** — à défaut je porte en deux colonnes |
| Fil · Actions · Décisions · Mémoire : **onglets** dans la maquette, **pages** dans l'application | **Codex**, puis peut-être le portable |
| Les textes de narration du parcours (5 clés) — la voix ne peut pas être rendue sans eux | **Codex** |
| Les dérivés WebP des 18 illustrations — aucun outillage image sur ce poste | **portable** |
| `le-site-du-point-zero` vaut 9 Ω en préprod et 10 en production | **Boris** (arbitrage éditorial) |
| `?stage=m1entry` et `?stage=m1circle` — `_classique.html.haml` disparaîtra ce jour-là | **moi**, dès les réponses de Codex |
| `marque_la_visite "m0.emotion.mentor"` | **portable**, sans urgence |

## Les leçons de ces trois jours

1. **Un banc supprimé ne casse rien — il se tait.** `ls scripts/ | grep <thème>` avant d'écrire.
2. **Une assertion décrit le RENDU, jamais la source.**
3. **Une purge d'entrée n'est pas un filet, c'est un masque.**
4. **⚠️ Une assertion qui ne peut pas échouer ne borne rien** — et sa variante : une assertion
   peut mesurer une grandeur **voisine** de celle qui compte et rester verte pour toujours.
5. **⚠️ Une parité de CONTENU n'est pas un portage.** Un banc qui ne regarde que la présence de
   blocs ne voit pas une forme qui n'a pas suivi — d'où les assertions **négatives**.
6. **Les valeurs éditoriales divergent entre préprod et production.** Un banc compare deux
   mesures entre elles, jamais une constante.
7. **⚠️ Un doublon CSS peut vivre longtemps sans se contredire frontalement.** Deux passes sur
   `.gesture-status`, chacune définissant des propriétés différentes sur les mêmes sélecteurs :
   rien ne les signalait, et un sélecteur non scopé imposait ses valeurs en silence. Trouvé en
   touchant le bloc pour une tout autre raison.
8. **⚠️ Une chaîne `if/elsif` sans `else` rend un état FUTUR muet, pas faux.** Deux fois en une
   soirée (le raccourci après `validated_at`, le panneau après `end_at` sur un rite facilitateur) :
   la branche manquante ne produisait aucune erreur, juste un texte incorrect ou un bloc vide. Une
   lecture du code ne le voit pas — seule la traversée du VRAI état (une expérience qu'on va au
   bout de valider) le révèle. À chaque nouvel état de `cu` qu'on introduit, vérifier que TOUTES
   les branches qui le testent ont vraiment un `else`, pas seulement celle qu'on vient d'ajouter.
9. **⚠️ HAML ne poursuit une ligne silencieuse QUE sur une virgule finale.** Un hash multiligne
   ouvert par une accolade seule en fin de ligne (`- x = {` puis les paires sur les lignes
   suivantes, sans virgule après le `{`) ne se poursuit pas comme un `{` Ruby ouvert le
   laisserait croire. Un hash à porter sur plusieurs lignes se termine par une virgule à CHAQUE
   ligne sauf la dernière ; sinon, une seule ligne, même longue.

## Et la méthode qui trouve

**Le navigateur voit ce qu'aucun banc ne peut voir**, et **un fichier jamais exécuté n'est pas
livré**. La limite notée le 22 août (« un compte verrouillé ne montre que ce qu'il a débloqué,
2 expériences sur 14 ») est tombée le 23 au soir : Boris a autorisé un compte à progresser
réellement sur les 14, et trois défauts sont sortis de cette seule traversée — aucun n'aurait été
visible à la lecture du code, ni sur un compte qui ne dépasse pas les 2 premières expériences.
**Vérifier une chaîne d'états (`courant`, `validated_at`, `end_at`) demande de la traverser en
entier au moins une fois, avec l'autorisation de le faire.**

---
# 2026-08-24 · de Codex · Textes de narration et affichage des Puissances disponibles

Les cinq textes `JourneyProgress` et les règles d'affichage des cas limites sont désormais dans
`docs/pedagogie/monde-0-sequences-actionnables.md`, §§6.7 à 6.9. Le bloc libre `validations`
reste sans titre. Le lot Échanges M1 demeure différé jusqu'à la clôture du Monde 0, conformément
à l'arbitrage de Boris.

# 2026-08-24 · de Codex · `co-c06` réservé au détail du Rôle d'appel

Arbitrage inscrit dans `docs/pedagogie/bloc-3-illustrations.md` :

- conserver `07-communication.png` sur `DELIB_COMMUNICATION` ;
- ne pas brancher `co-c06` dans la PR #82 ;
- réserver `06-qualite-captive-garde-fous-v1.png` à la future fiche détaillée du Rôle d'appel,
  au passage qualité captive → risque de capture → garde-fous ;
- nom fonctionnel recommandé pour la future section : `ROLE_GARDE_FOUS`.

Le YAML historique ne possède pas encore cette surface : son écran `FONCTION` porte toujours les
anciennes postures. Déplacer l'image ailleurs créerait une fausse correspondance éditoriale.

# 2026-08-24 · de Codex · tunnel d'engagement prêt à reprendre

La cible du passage parcours publics → inscription → Monde 0 est documentée dans
`docs/site/tunnel-engagement-inscription.md` et maquettée dans
`zegame-prototypes/tunnel-engagement-cible/`.

Points contractuels à préserver lors du portage Rails : parcours publics terminables sans
compte ; 5 Ω et un badge par parcours ; import automatique, transparent et idempotent ; copie
locale conservée en cas d'échec ; aucune formulation personnelle publiée ; Passeur du Seuil
obtenu seulement dans l'application. L'ouverture effective des inscriptions attend la route
publique et le mécanisme d'import livré.

# 2026-08-24 · de Codex · politique de confidentialité du site à intégrer après validation

Le projet public est disponible dans `docs/site/politique-confidentialite-point-zero.md` et les
CGU pointent désormais vers lui. Il couvre le site et l'application afin de conserver une seule
source de vérité pour le tunnel public, l'import vers le compte, les contenus, les échanges, les
IA, les paiements, la newsletter et les mineurs.

Ne pas publier la section finale `Vérifications avant publication`. Elle recense les faits à
confirmer dans le code et les contrats : cookies et stockage local, durées réelles, suppression,
paramètres Anthropic, sous-traitants, enregistrements, mineurs et analyse d'impact. La page publique
devra être accessible sans compte et liée depuis le pied de page.

## 2026-08-24 · de Codex · mentions publiques de la politique fermées pour la PR #85

La source canonique ne porte plus de mention publique non remplie : version `1.0`, entrée en
vigueur au `24 août 2026`, fermeture du compte demandée actuellement par
`contact@pointzero2050.com`, et aucun faux lien `Gérer mes cookies`. Le module de choix n'est
annoncé que si un traceur facultatif est réellement activé.

Merci de reporter ces quatre corrections dans le contenu de la PR #85 avant fusion. La réserve
interne `Version de travail v0.1` et la section `Vérifications avant publication` restent dans la
documentation, jamais dans l'article public.
