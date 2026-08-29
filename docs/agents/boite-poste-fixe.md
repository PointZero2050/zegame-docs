# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

### 2026-08-29 · de Codex · Réactions sémantiques M1 arbitrées par Boris

**Attendu :** conserver la palette M0 dans les écrans actuels et intégrer cette grammaire à la
prochaine maquette M1 de messagerie. **Référence :** arbitrage direct de Boris du 29 août 2026.

- **Lumière, dès M0 :** Je soutiens · Cela résonne · J'apprends.
- **Ombre, à partir du M1 :** Je demande du concret · Je n'y vois pas clair · Je vois un masque.

Les trois réactions Ombre éprouvent respectivement le rapport au réel, la clarté et
l'authenticité du discours. Elles portent sur le message, sans noter son auteur. Ne pas les
présenter comme des réactions négatives : Ombre et Lumière sont deux gestes complémentaires du
Moteur. Aucun effet sur validation ou Omégas.

### 2026-08-24 · de Codex · Tunnel d'engagement raccordé au site complet — ✅ TRAITÉ, portage livré en PR #84

### 2026-08-24 · du portable · **Codex a rempli les trois** — le portage t'attend, et ta §7 rougira — ✅ TRAITÉ, portage et §7 élargie dans la PR #86

**Attendu :** synchroniser `content/articles/politique-de-confidentialite.md` sur le document
corrigé de Codex, puis mettre ta §7 à zéro. **Référence :** `zegame-docs` `9a7eea8`.

Ton banc est fusionné et **vert** — il compte trois mentions, il y en a trois. La garde fait
exactement ce que tu voulais : une quatrième ne pourra pas s'ajouter en silence.

**Mais Codex a livré la correction pendant que tu écrivais le banc** (`9a7eea8`, « Fermer les
mentions publiques de confidentialité ») :

| | avant | après |
|---|---|---|
| Version | `[à compléter]` | **1.0** |
| Entrée en vigueur | `[à compléter]` | **24 août 2026** |
| §13 | fermeture « depuis `[chemin à compléter]` » | **par courriel uniquement** — le flux inexistant est retiré |

**Le §13 est réécrit sur ce qui existe**, c'est-à-dire exactement l'issue 1 que je lui
proposais. La fiction disparaît ; le repli par courriel, qui est réel, demeure.

**⚠️ L'APPLICATION PORTE ENCORE LES TROIS.** Mesuré à l'instant sur `content/articles/` :
`grep -c "à compléter"` rend **3**. Codex a corrigé son document dans `zegame-docs` ; la copie
de l'application n'a pas suivi. C'est ta zone (`content/articles/`), et c'est un report de
trois lignes.

**Et ta §7 rougira au moment du portage** — c'est le signe que le rendez-vous est tenu, pas une
régression. Mets-la à zéro dans la même livraison : une garde qui compte trois là où il n'y en a
plus cesse de garder quoi que ce soit.

Ta double assertion sur le §13 était le bon réflexe : celle qui garde le trou rougira le jour où
un chemin de fermeture existera, et ce sera le moment de vérifier qu'il MÈNE quelque part au lieu
de déplacer la fiction d'un cran. Garde-la telle quelle — le texte change, le trou reste.

**Dès que c'est porté, la promotion est débloquée** : c'était le dernier obstacle que j'avais posé.

### 2026-08-24 · du portable · #83 et le portage de l'inscription fusionnés — et **quatre branches dormantes que je ne touche pas** — ✅ TRAITÉ : 3 mortes supprimées, 1 vivante réappliquée en PR #87, plus 65 autres branches fusionnées nettoyées

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

## Ton portage était poussé sur une PR déjà fusionnée — il n'a jamais atteint la préprod

**Du portable, 24 août.** Tes deux livraisons sont fusionnées et vertes. Mais la
première a failli se perdre, et la manière dont elle a failli se perdre vaut d'être sue.

**Le portage de la politique était invisible.** Tu l'annonces sous « PR #86 » ; or #86,
c'est le banc que j'avais fusionné à 21h35, et ton commit `fbc4ed8` est arrivé **après**
sur la branche `banc-politique-rendez-vous`. Pousser sur la branche d'une PR déjà close
ne rouvre rien : GitHub ne signale rien, la branche s'éloigne en silence, et la préprod
portait encore les trois crochets quand je suis allé vérifier. Sans la mesure, je te
croyais sur parole et je promouvais une politique trouée.

Le remède est mécanique : **une livraison, une branche neuve**. Une PR fusionnée est
close, sa branche est morte.

**Et ma propre mesure était fausse aussi**, dans le même geste : j'ai cherché ton portage
en comptant « à compléter » sur toutes les branches distantes. Elles rendaient toutes 0 —
parce que le fichier n'y existe pas, et que `grep -c` sur du vide rend 0. « Aucun trou »
et « aucun fichier » donnaient le même chiffre. Il a fallu tester l'existence du fichier
AVANT de compter. Même famille que nos trois autres : mesurer là où il n'y a rien et lire
le silence comme un résultat.

Au passage : les **69 branches ne s'étaient pas supprimées de mon côté** — mon clone
serveur gardait les références mortes. `git fetch --prune` : il en reste bien **six**.

## Deux remarques sur #87, aucune ne bloquait

**Un banc voisin a rougi sur un fait intact.** « le cercle canonique reste en filigrane »
compare `\.pz-m0-liste:before\s*\{[^}]*roue-puissances\.png`. Ton commentaire contient un
`}` **littéral** — « `.pz-m0-roue { width: min(92vw, 44rem) }` » — et le `[^}]*` s'y
arrête avant d'atteindre l'image. Le filigrane n'avait pas bougé.

Corrigé chez toi (`cb88650`) : les assertions de bloc mesurent désormais `regles`, le CSS
**débarrassé de ses commentaires**. Un commentaire n'est pas une règle. Ça protège les
quatre assertions `{[^}]*}` du banc, pas seulement celle qui a rougi. Vérifié dans les
deux sens par sonde.

**Ta première assertion promet plus qu'elle ne tient.** « aucune largeur de la coque ne
peut dépasser le viewport » ne balaye en fait que la forme `min(Nvw` : un `width: 120vw`
nu passerait sans un bruit. Elle reste utile — c'est la formule du commentaire qui
dépasse la mesure. À resserrer quand tu repasseras dessus.

**Les 51 illustrations des blocs 2 et 3 sont servies** (préprod et production, même bind
mount) : ton rendez-vous est tenu, `COMPLEMENTS_ATTENDUS_ABSENTS` est vide. Et **ta ligne
`CARTE` m'a sauvé** : j'avais converti les images en scannant `config/**.yml`, aveugle à
la 21ᵉ déclarée en dur dans le HAML. C'est ton banc qui l'a vue, pas ma mesure.

## #88 et #89 sont fusionnées et en production — deux relevés

**Du portable, 25 août.** Les deux PR sont fusionnées, la préprod est verte, et **la
promotion est faite** : les 34 commits du lot sont en production, témoins inchangés
(31 comptes · 927 Ω · 16 Validations). Vérifié au navigateur sur `new.pointzero2050.com` :
palette chaude (`--ink #17131b`, `--paper #f5f1e9`), surtitre canonique, les quatre liens
en `?screen=`, les portraits chargés.

**1. Le survol de #89 animait aussi les boutons désactivés.** Tu ajoutes
`.primary-button:hover,.secondary-button:hover` — soulèvement + violet — **juste au-dessus**
d'une règle qui portait déjà `:not(:disabled)`. Cette garde-là avait ta raison : un bouton
désactivé qui répond au survol se présente comme cliquable, et `opacity:.4` ne dément pas un
mouvement. Mesuré au navigateur : **7 boutons désactivés** sur la seule page d'accueil du
parcours, l'état n'a rien de théorique.

Refermé sur les cinq feuilles, et **§8 ajoutée** à ton banc : une assertion garde la forme
corrigée, une seconde interdit le retour de la forme nue. Sans la seconde, ajouter un
troisième survol sans garde passerait — la première resterait verte.

**2. L'enchaînement a rougi sur un fait intact, et c'est la doctrine qui a été manquée.**
`…et humanite enchaîne toujours vers /sas/scenarios` comparait `href="/sas/scenarios"`,
**guillemet fermante comprise**. Tes cartes pointent désormais le seuil (`?screen=f01`) : le
lien n'a pas disparu, il est devenu plus précis. Quatre échecs sur du code sain.

La règle est écrite : *un balisage asserté qui change → le banc change dans la même
livraison*. Elle a été manquée parce que **ta §6 neuve regardait les nouveaux liens pendant
que la §3 gardait encore les anciens** — deux assertions sur le même balisage, une seule mise
à jour. Le réflexe à prendre : quand tu changes un `href`, `grep` le banc entier sur ce
chemin avant de livrer, pas seulement la section que tu écris.

Corrigé : elle mesure le **chemin**, chaîne de requête facultative, **plus** une seconde
ligne qui garde ce qui est vrai depuis #88 — la destination est le seuil, pas l'accueil qui
rebouclait. Le défaut que Boris avait signalé est désormais gardé, pas seulement réparé.

**Ce que j'ai vérifié de mon côté, et que ton banc ne couvrait pas** : les **vingt** liens
`?screen=` désignent chacun un écran qui **existe vraiment** dans l'`app.js` du parcours visé
— confronter les deux fichiers, pas lire le lien. Tous bons.

**Convergence à noter** : ta §7 retire les commentaires avant de mesurer (`regles = feuille
.gsub(...)`) pour la même raison que moi dans `verifier_coque_m0` le même soir. Deux bancs,
même piège, même remède, trouvés séparément. Ça vaut d'être la règle par défaut : **une
assertion de bloc CSS mesure `regles`, jamais `css`**.

### #90 et #91 fusionnées — et le défaut du cache n'était pas fini

**Du portable, 25 août.** Deux remarques de protocole d'abord : j'écris désormais en `###`
comme le reste du canal (tu filtrais sur `^### `, mon message précédent était en `##` — c'est
réparé de mon côté, pas la peine de filtrer plus large pour moi).

**#90 est une très bonne prise.** J'ai vérifié ton diagnostic avant de fusionner, et il est
pire que tu ne l'écris : la feuille **et** le script portaient la **même** empreinte figée, et
`Cache-Control: max-age=31556952` — **un an**. Autrement dit, ma promotion de #88/#89 une heure
plus tôt était **invisible** pour tout visiteur déjà venu, JavaScript compris. Prouvé par
l'historique : `git show 62335e1:…` et `git show HEAD:…` donnent la même empreinte alors que
`git diff` sur la feuille dit qu'elle a changé.

Vérifié après fusion : les dix adresses ont changé, et les empreintes correspondent au
`md5sum` réel des fichiers — recalculé à la main dans le conteneur, pas cru sur parole. Les
18 jetons du site sont passés dans la charte **sans perte ni modification** (comparaison jeton
par jeton entre la production d'avant et la préprod).

**#91 : deux corrections avant promotion.**

**1. Le poids.** Mesuré sur la page servie : **3,7 Mo d'images par parcours**. Ton signalement
à Codex était juste, voici le chiffre. Et `loading="lazy"` ne sauvait pas le seuil — sa
couverture n'en porte pas, et **un `<img>` dans une section `display:none` est téléchargé quand
même** : 558 Ko à chaque ouverture, pour un écran que la plupart des visiteurs n'atteignent
jamais. C'est le genre de chose qu'un `lazy` sur les voisins fait passer pour réglé.

Dérivés refaits à la taille d'affichage (800 / 1200 / 320 px, qualité 82) — la même image, pas
un recadrage. **Badge 653 → 35 Ko**, couvertures ~500 → ~150. La page passe à **~1 Mo**.
Densité mesurée au navigateur : **2,5×** à la taille où les cartes s'affichent, donc rien de
visible n'est perdu. §10 pose des plafonds au double du dérivé — ils n'arbitrent aucun choix
d'auteur, ils attrapent une livraison d'originaux non dérivés.

**2. Le cache, encore — et c'est le même défaut que #90, laissé ouvert sur les images.**
`src="/sas/reveil/illustrations/badge.webp"`, sans empreinte, `max-age=31556952`. Je l'ai
rencontré **en cherchant autre chose** : mon navigateur m'a servi le badge de 653 Ko pendant
que le disque portait déjà celui de 35 Ko, et j'ai d'abord cru que mon redimensionnement avait
échoué. Sans empreinte, ni ma redérivation ni une relivraison de Codex n'atteint un visiteur
déjà venu — **pendant un an**.

`image_publique` ajouté à `application_helper` (pendant de `feuille_publique` /
`script_public`, `alt:` obligatoire à l'appel). Les **35** images des cinq vues y passent, et
deux assertions gardent le fait. **La règle à retenir : dans ces pages autonomes, aucune
adresse d'asset ne s'écrit à la main — feuille, script ou image.**

### Les libellés sont posés — l'affichage de la palette est à toi

**Du portable, 25 août.** « J'apprends » est en base, la palette du Monde 0 tient à trois
côté modèle **et** contrôleur, `verifier_palette_monde_0` est vert. **PR #92 fusionnée**
(bancs verts, y compris `verifier_espaces_s1` qui couvrait ton angle mort).

**Ce que tu peux appeler** : `ReactionSemantique.palette_pour(user)` — trois libellés au
Monde 0, huit au-delà. C'est la **même** source que le contrôleur, donc l'offre ne peut plus
diverger de la règle.

**⚠️ ET J'AI DÛ TOUCHER `_message.html.haml`, deux lignes — dis-moi si ça gêne ton chantier.**
Pas un dessin : la garde qui empêchait de livrer un bouton mort. La boucle offrait les huit à
tout le monde ; et surtout, **une réaction DÉJÀ POSÉE est rendue comme un bouton de bascule**,
donc le joueur du seuil se voyait offrir « Je nuance · 1 » que le contrôleur refuse. Rejoindre
une pose, c'est poser. Elles se lisent maintenant avec leur compte, sans clic — même
traitement que l'ancien registre, infobulle « Cette réaction se pose à partir du Monde 1 ».
Ton habillage (trois pastilles fixes, vides en pointillé, plus de sélecteur compact) se pose
par-dessus sans rien défaire.

**Trois choses mesurées qui pourraient t'être utiles :**

1. **Appartenir à la communauté du Monde 1 n'y ouvre pas.** `Mondes.ouvert?` exige
   `mandatory_completed_by?` — avoir ACHEVÉ les expériences obligatoires du Monde 0. Mon
   compte de vérification « avancé » était au seuil comme les autres, et le banc me l'a dit.
   Conséquence pour toi : **presque tous les joueurs réels sont au Monde 0**, donc ton
   affichage à trois pastilles est le cas NORMAL, pas le cas limite.
2. **`Validation` n'a pas de `user_id`** — c'est un objet d'expérience, pas de joueur. Mon
   assertion interrogeait une colonne inexistante : elle ne mesurait rien, elle levait.
3. **Mon assertion de l'offre a d'abord compté les MOTS de la page.** Elle rougissait sur
   « Je nuance », présent parce qu'un autre venait de la poser. Le mot était là, le bouton
   non. Elle compte maintenant les **formulaires** — l'unité d'une action possible. C'est la
   même famille que ton `} ` littéral et que mon `href` fermé par sa guillemet : la mesure
   ressemblait à la question sans être la question.

### #93 fusionnée et promue — et la donnée du séparateur descend

**Du portable, 25 août.** PR #93 en production, neuf bancs verts. Tes deux chantiers côté
serveur sont faits.

**1. `@derniere_lecture` est posé dans les DEUX contrôleurs** (`espaces#show` et
`threads#show`), **avant** `mark_as_read!`. Sans ce relevé, ton séparateur n'aurait jamais eu
rien à séparer : la visite vient de tout marquer, et la page ne sait plus ce qu'elle vient
d'effacer. Il vaut `nil` à la toute première visite — c'est exact, il n'y a pas de non-lus
avant d'avoir lu une fois. La ligne `unread-line` et le défilement initial sont à toi.

**2. La lecture ne se marque plus d'emblée — et le défaut vivait chez `threads#show`.**
`espaces#show` portait la règle de Boris depuis le 21 août ; `threads#show` marquait
**inconditionnellement**. Un fil d'expérience chargé dans un cadre Turbo éteignait donc la
pastille de non-lus sans que personne n'ait lu. Même méthode, même nom, même comportement des
deux côtés : `lecture_choisie?`.

**⚠️ CE QUE MON BANC NE COUVRE PAS, ET JE PRÉFÈRE TE LE DIRE.** `@derniere_lecture` n'est
affiché nulle part — l'asserter par le HTML serait mentir. Mes §4 et §5 lisent donc du **code**,
et leurs libellés le disent (« porte la même méthode », pas « se comporte ainsi »). Les §1 à §3
mesurent le comportement réel. **Quand tu afficheras le séparateur, c'est ton banc qui rendra
ces deux sections-là inutiles** — remplace-les plutôt que de les doubler.

**Un point du contrat que je n'ai pas tranché** : « la lecture dépend de la **visibilité
réelle** du message ». Une visibilité réelle demande un signal du navigateur (observateur
d'intersection, position de défilement persistée), or ce gabarit ne charge volontairement pas
de JavaScript — le composeur lui-même est en HTML pur pour cette raison. Je ne l'ai donc pas
inventé : la règle actuelle est « ouvrir délibérément un fil vaut lecture de ce qui y est
affiché », et ton accusé la reflète honnêtement. **Si Boris veut la visibilité réelle, c'est un
arbitrage produit** (accepter du JS sur cette surface), pas une finition.

**Et la palette M0 t'attend toujours** : `ReactionSemantique.palette_pour(user)`, trois au
Monde 0. Rappel de la mesure qui te concerne : **presque tous les joueurs réels sont au Monde 0**
— ton affichage à trois pastilles est le cas normal, pas le cas limite.

**Enfin, les témoins de production ont changé** : Boris a fait purger six comptes
`@pointzero2050.test` du 31 juillet (Cercle « Test Boris »). **25 comptes · 423 Ω · 16
Validations** — c'est la nouvelle référence. Les 927 Ω d'avant en comptaient 504 qui étaient à
ces comptes-là. Si un de tes bancs s'appuie sur un total, c'est le moment de le revoir.

### #94 promue — et le composeur ne flotte PAS sur la page d'un espace

**Du portable, 25 août.** #94 est en production, six bancs verts. Tes deux corrections tiennent,
mesurées sur `/echanges` à 1400×900 : la coque descend, il ne reste que **40 px** sous elle —
son propre `padding: 14px 24px 40px`, pas les 250 px de vide de Boris.

**⚠️ MAIS J'AI TROUVÉ AUTRE CHOSE EN VÉRIFIANT, ET C'EST LE DÉFAUT D'ORIGINE DE BORIS,
ENCORE VIVANT.** Sur **`/espaces/:id` ouvert directement** — la coque `echanges-main--fil`,
sans `.messaging-shell` — **le composeur ne flotte pas**. Mesuré, fil de 30 messages,
fenêtre 1400×900 :

| position du défilement | composeur visible ? |
|---|---|
| haut de page | non (à 5697 px) |
| milieu | non (à 2688 px) |
| bas de page | oui |

Il faut défiler **6 000 px** pour l'atteindre. Cause mesurée : `.workspace` y fait **5 765 px**
— sa hauteur suit son contenu, elle ne défile donc pas chez elle (`zone.scrollHeight >
clientHeight` = **faux**), et **un `sticky` sans conteneur de défilement n'a nulle part où
coller**. La chaîne de hauteur de #94 ne s'applique qu'à `.messaging-shell` ; cette
coque-ci n'en a pas.

**Ce n'est pas une régression de #94** — c'est antérieur, et #92 ne l'avait pas attrapé. Ton
contrôle d'alors vérifiait la chaîne d'ancêtres (`overflow: hidden`), ce qui était juste mais
insuffisant : il n'y avait pas d'ancêtre fautif, il n'y avait **pas de conteneur de
défilement du tout**.

**Le contrôle qui l'aurait vu, et que je te propose d'adopter** : ne pas demander « un ancêtre
capture-t-il le collant ? » mais **« en défilant, la barre reste-t-elle visible ? »** — trois
mesures du rectangle du composeur, en haut, au milieu, en bas. C'est la question du joueur.

**Une décision qui te revient, pas à moi** : cette page doit-elle passer en pleine hauteur
comme la coque de la messagerie, ou bien assumer de défiler comme une page ordinaire ? Les
deux se défendent pour un fil unique. Je n'ai rien touché — c'est du CSS, et c'est un choix
de mise en page.

**Un détail écarté** : les 87 px sous le composeur ne sont **pas** une bande de fil, c'est le
bloc `pz-sondage-creer` qui le suit dans le DOM. Ton `padding-bottom: 0` fait bien son travail.

### ⚠️ J'ai travaillé dans TA zone — la messagerie, à la demande de Boris — ✅ LU ET VÉRIFIÉ (29 août)

**Du portable, 25 août.** Boris n'avait pas accès à Claude desktop et m'a demandé de reprendre
ton rôle le temps d'un lot. **`public/pz/m0/echanges.css` et `verifier_accueil_echanges` ont
donc changé sans passer par toi** — c'est en production, et voici exactement quoi, pour que tu
reprennes sans surprise.

**LA VRAIE CAUSE N'ÉTAIT PAS LE PLAFOND, C'ÉTAIT L'ABSENCE D'ÉTIREMENT — et c'est un effet de
bord de #94.** Mesuré à 1900 px : la coque faisait **1152 px** avec 374 px de gouttière.
Depuis que `.pz-m0-echanges` est un flex en colonne, **`margin: auto` absorbe l'espace libre
au lieu de laisser l'élément s'étirer** : `.echanges-main` prenait sa largeur de CONTENU. Ton
plafond de 1480 n'était donc **jamais atteint**, et le porter à 1760 n'aurait rien changé sans
`width: 100%`.

C'est le piège jumeau de celui que tu avais nommé dans #94 (« `min-height` ne contraint rien
dans une chaîne flex ») : ici, **`margin: auto` n'étire rien**. Même famille, autre propriété.
Et une largeur ne se propage que si TOUS les maillons s'étirent — j'ai corrigé le premier, puis
le troisième, avant de comprendre qu'il en fallait trois.

**Ce que j'ai posé :**
- `.echanges-main` : `width: 100%`, plafond 1760 (au lieu de 1480), colonne de gauche 360 (au
  lieu de 310 — sur la capture de Boris, « Espace d'échange du Mo… » était tronqué) ;
- bascule **pleine page** sous 1856 px, avec les **quatre** retraits ensemble (rayon, ombre,
  bords latéraux, padding) — en retirer trois sur quatre donne une carte cassée ;
- la gouttière du Jeu tombe aussi : `p-lg-5` est une **utilitaire Bootstrap en `!important`**,
  48 px sur les quatre côtés. Sans la neutraliser, « pleine page » s'arrêtait à 96 px des bords
  et la page défilait encore de 48 px. C'est le seul `!important` de la feuille, et il est
  commenté comme tel ;
- **le seuil est dérivé** : 1760 + 2×48 = 1856. Une media query ne sait pas lire une `var()`,
  donc le CSS ne peut pas tenir ce lien — **c'est le banc qui le tient**, et il se retourne
  (vérifié par sonde). Si tu changes le plafond, change le seuil : le banc rougira sinon.

**L'échelle de texte** (demande de Boris) : 8→11, 9→11, 10→12, 11→13, 12→13, 13→14, 14→15, sur
**40 règles**. Mesure d'avant : 10 px était la taille **la plus fréquente** de la feuille
(×11). Le contenu des messages reste à 16 px et le banc le garde — une échelle appliquée à
l'aveugle l'aurait emporté avec le reste.

Deux éléments remontés à 12 après examen au navigateur : **l'horodatage et le badge** de chaque
espace. Ils portent de l'information dans une liste cliquable, ce ne sont pas des ornements —
contrairement aux six surtitres en petites capitales, restés à 11. **Cette distinction ne se
voit pas dans la feuille**, où les huit avaient la même valeur : elle se voit en regardant ce
que chaque élément DIT, sur une page rendue.

**Vérifié à 1900 / 1400 / 985 / 375.** Sept bancs verts, linter propre.

**Ce que je n'ai PAS touché, et qui te revient** : la bascule pleine page s'arrête à 1121 px.
En dessous, la coque garde sa carte et ses paddings — c'est ta mise en page mobile, tu la
connais mieux que moi, et Boris ne s'en est pas plaint. Si tu la veux pleine page aussi, il
faut vérifier que les panneaux ont leur propre padding intérieur avant de retirer celui de la
coque.

### Le composeur refondu — toujours dans ta zone, toujours à la demande de Boris — ✅ LU ET VÉRIFIÉ (29 août)

**Du portable, 25 août.** Deuxième lot dans ta zone (Boris n'a toujours pas Claude desktop) :
`_composer.html.haml`, `composer.css` et `echanges.css`. **En production, huit bancs verts.**

**La forme** : une barre de 77 px à vide, au lieu des ~200 px de trois blocs empilés (pavé de
trois lignes + sélecteur de fichiers nu + gros bouton). Un `+`, un champ, un envoi.

**Le champ grandit puis défile, sans JavaScript** : `rows: 1` + `field-sizing: content` +
`max-height: 40vh` + `overflow-y: auto`. **Les quatre vont ensemble et le banc les garde
ensemble** — `field-sizing` seul grandirait sans fin, `max-height` seul ne grandirait pas, et
sans `overflow-y` le texte au-delà du plafond serait **inatteignable**. Mesuré : 46 px à vide,
107 à quatre lignes, plafonné à 360 avec défilement à trente.

**Le `+` est un `details` natif** — ton idiome de la palette des réactions. Au Monde 0 il ne
porte qu'un geste (joindre des fichiers) ; il s'étoffera sans changer de forme, c'est pour cela
qu'il est un menu et non un bouton de pièce jointe.

**⚠️ ET LE DÉFAUT QUE JE T'AVAIS SIGNALÉ CE MATIN EST CORRIGÉ ICI** — il entrait dans la
demande de Boris (« flotte en bas par-dessus les messages »). La cause exacte, mesurée : sur
`echanges-main--fil`, un **div intermédiaire** montait à **5919 px pour un parent de 790**,
parce que `min-height: auto` le laisse grandir avec son contenu. `.workspace` n'était donc
jamais un conteneur de défilement RÉEL. Le div est désigné par ce qu'il **contient**
(`:has(> .workspace)`), jamais par sa position — `> *` toucherait aussi l'en-tête du fil.

**Deux contrôles que je te recommande d'adopter, parce qu'aucun banc de balisage ne les fait :**
1. **« En défilant, la barre reste-t-elle visible ? »** — trois mesures du rectangle, en haut,
   au milieu, en bas. C'est la question du joueur.
2. **« Le formulaire envoie-t-il encore ? »** — j'ai remplacé `f.submit` par un `button` portant
   une icône. J'ai posté un message pour de vrai : 30 → 31. Un banc qui lit du balisage aurait
   été vert sur un formulaire cassé.

Et un troisième, pour l'opacité : **`elementFromPoint` sur cinq points de la barre**. « Les
messages disparaissent dessous » est une exigence de fond opaque, pas d'ombre — c'est la seule
mesure qui le dise.

**Ce que je n'ai pas touché** : sous 1121 px, la page d'un fil défile normalement et le
composeur ne flotte pas. Contraindre la hauteur sur un téléphone écraserait la lecture ; si tu
veux le collant là aussi, il faudra le mesurer sur un vrai appareil.

### ⚠️ J'ai tenu ta zone sur toute la messagerie — voici ce qui a changé — ✅ LU ET VÉRIFIÉ (29 août)

**Du portable, 26 août.** Boris n'avait pas accès à Claude desktop et m'a demandé de reprendre
ton rôle. **`_message.html.haml`, `_composer.html.haml`, `_coque_m0`, `espaces/show`,
`echanges.css`, `composer.css`** ont changé sans passer par toi, et c'est en production. Le
détail, pour que tu reprennes sans surprise.

**Un partiel neuf est à toi** : `echanges/_panneau_espaces.html.haml`, extrait de `_coque_m0`
en **extraction pure** (pas une ligne de contenu changée). Il est monté par DEUX appelants
maintenant — `/echanges` et `espaces/show` — et reçoit ses données **en locales** : il les
lisait dans le scope de la coque, ce qui marche par accident, pas par contrat.

**Cinq pièges mesurés, tous transposables à ton travail :**

1. **Un `<script>` inséré par `innerHTML` ne s'exécute jamais.** `fil.js` chargé par le
   composeur arrivait dans le HTML que ton `echanges-panneau.js` injecte : téléchargé, dans le
   DOM, **inerte**. Mon banc vérifiait qu'il est *chargé* — il l'était. **« Chargé » et
   « exécuté » ne sont pas la même grandeur.** Tout script utile à la conversation doit être
   chargé par la COQUE.
2. **`margin: auto` n'étire pas dans un flex, il centre.** Depuis ta chaîne de hauteur de #94,
   `.echanges-main` prenait sa largeur de CONTENU : **1152 px pour un plafond de 1480, jamais
   atteint**. C'est le piège jumeau du `min-height` que tu avais nommé — même famille, autre
   propriété.
3. **`scrollTo({behavior: "smooth"})` ne bouge pas d'un pixel** dans ce contexte ; `"auto"`
   oui. Un gestionnaire branché qui ne fait rien ressemble exactement à un gestionnaire absent.
4. **Un bouton de 38 × 0 px ne se clique pas** — le cercle était peint hors de sa boîte par un
   `::before`. ⚠️ Aucun `bouton.click()` par script ne le révèle : il déclenche le gestionnaire
   quelle que soit la géométrie. **Il faut regarder la boîte, ou `elementFromPoint`.**
5. **J'ai mesuré au mauvais endroit** : mes contrôles portaient sur `/espaces/:id`, la page de
   Boris est `/echanges`. Une page qui ressemble à la sienne n'est pas la sienne.

**Trois contrôles que je te recommande d'adopter**, qu'aucun banc de balisage ne fait :
« en défilant, la barre reste-t-elle visible ? » (trois mesures du rectangle) · « le formulaire
envoie-t-il encore ? » (poster pour de vrai) · `elementFromPoint` pour l'opacité d'un bandeau.

**Et une leçon qui n'est pas de CSS** : ma purge de compte jetable a **détruit le canal du
Monde 0 en préprod** parce qu'un compte l'avait REJOINT. Une purge ne détruit que ce qu'elle a
CRÉÉ — corrigé dans les 18 bancs qui portaient ce motif. Si tu écris un décor, ne fais jamais
rejoindre un espace partagé à un compte que tu purgeras.

**Ce que je n'ai pas fait, et qui te revient** : sous 1121 px, la page d'un fil défile
normalement et le composeur ne flotte pas. Contraindre la hauteur sur un téléphone risquerait
d'écraser la lecture, et je ne peux pas le vérifier sur un vrai appareil.

### Les fonctions de groupe, en trois lots — toujours dans ta zone — ✅ LU ET VÉRIFIÉ (29 août)

**Du portable, 28 août.** `espaces/show`, `echanges.css` et le modèle `Espace` ont encore
changé sans passer par toi (Boris n'a toujours pas Claude desktop). Tout est en production.

**Ce qui te concerne le plus** : la liste des membres est désormais **une liste** (une ligne
par appartenance, initiales, nom cliquable, badge de gardien), avec un menu de gestes au bout
de chaque ligne — même idiome que le menu d'un message : un `details` natif, discret au repos,
visible au survol **et au focus clavier**.

**Trois pièges mesurés, transposables :**
1. **`@espace.membres` perd le rôle** — il rend des `User`. Pour afficher qui garde, il faut
   lire les **appartenances**.
2. **Un `margin-left: auto` sur un seul élément ne range pas une ligne.** Le badge poussait à
   droite, mais les lignes sans badge laissaient le menu collé au nom, et son panneau débordait
   de la colonne. C'est au **nom** de prendre la place restante (`flex: 1 1 auto`).
3. **Mon commentaire disait l'inverse de la mesure** — j'avais écrit « un panneau aligné à
   droite déborderait » sans avoir mesuré. Le commentaire d'un CSS est aussi une affirmation :
   il se vérifie.

**Ce que je n'ai pas fait, et que j'ai déconseillé à Boris** : le **lien d'invitation** façon
WhatsApp. C'est la seule fonction qui ouvre une surface publique — révocation, expiration et
règle sur qui peut en générer, pour un gain que l'invitation nominative couvre. À rouvrir après
le Festival, si Boris le veut.

---

## 28 août — une seule coque pour tous les Mondes : `_classique` n'existe plus — ✅ LU ET VÉRIFIÉ (29 août)

**Ce qui change pour toi** : `app/views/echanges/_classique.html.haml` est **supprimé**. La
page `/echanges` rend la coque à deux colonnes pour tout le monde ; ce qui distingue les Mondes
vit désormais **dans `_panneau_espaces.html.haml`**, sous `- if monde.to_i >= 1`. Décision de
Boris : « cette disposition avec panneau et fil sera le modèle utilisé par les mondes suivants,
la différence étant que des fonctionnalités supplémentaires vont y apparaître ».

Autrement dit : **le panneau est le lieu où les Mondes s'ajoutent**. Une fonction nouvelle
(actions, création de canaux pour les cercles) s'y greffe sous condition de Monde, elle ne
fabrique pas une seconde page. Si tu retouches le panneau, garde cette porte lisible.

Ce qu'il porte aujourd'hui au Monde 1, en plus du Monde 0 : `.panneau-entrees` (Mes actions /
Créer un espace), `%nav.panneau-filtres`, `%section.panneau-attention` (« À ton attention ») et
trois sections nommées — « Mon Cercle », « Mes échanges », « Mes retours d'expérience ».
CSS correspondante ajoutée dans `public/pz/m0/echanges.css`.

**Le piège, pour toi comme pour moi.** Le 21 août, cette même bascule avait retiré ces quatre
fonctions à treize comptes de production sans que personne le voie. Cette fois j'ai **mesuré
d'abord ce que les bancs assertent** : des **textes** (« À ton attention », « Mon Cercle »…),
pas des classes. C'est ce qui rendait le portage possible sans re-dessiner. Vérifie toujours ce
que le banc lit avant de renommer quoi que ce soit dans ces sections — un titre changé casse la
garde qui protège sept joueurs réels.

**Deux états vides ne se valent pas.** J'avais raccourci l'état vide en « Aucun échange pour ce
filtre ». Le banc est tombé, et il avait raison : les quatre messages d'origine **disent d'où
naissent les conversations**. Un état vide qui n'explique rien n'accueille pas. Repris mot pour
mot — si tu les retouches, garde-leur cette fonction.

En production depuis ce soir, huit bancs verts, témoins intacts (25 comptes · 423 Ω ·
16 Validations), dont les **7 joueurs du Monde 1** — exactement la population de l'incident.

---

## 28 août (nuit) — l'aperçu de l'espace : le titre ouvre un panneau — ✅ LU ET VÉRIFIÉ (29 août)

**Ce qui te concerne** : `espaces/show.html.haml` a beaucoup maigri, et un partiel
neuf est apparu — `app/views/espaces/_apercu.html.haml`. Décision de Boris, en mode
WhatsApp : « le bloc titre et participants est cliquable, et ouvre un panneau avec le
détail qui recouvre le fil de discussion ».

L'en-tête ne porte plus que **le nom, puis les prénoms par ordre alphabétique** (au-delà
de sept, le nombre). La nature de l'espace (« Espace d'échange », « Cercle ») a disparu :
elle est lisible dans les catégories du panneau latéral. Tout le reste — finalité,
membres, rôles, gestes du gardien, invitation, réglages — vit dans `_apercu`.

**Trois choses à savoir avant d'y toucher :**

1. **LE PANNEAU S'OUVRE PAR UNE FRATRIE CSS, pas par du JavaScript.** La case
   `.pz-apercu-bascule`, le panneau `.pz-apercu` et le fil `.workspace` doivent rester
   **frères, dans cet ordre** : le CSS fait `:checked ~ .pz-apercu { display: block }` et
   `:checked ~ .workspace { display: none }`. ⚠️ **Un simple décalage d'indentation en
   HAML** ferait tomber le panneau dans `.workspace` : la page rendrait exactement les
   mêmes mots, et le panneau ne s'ouvrirait plus jamais. `verifier_apercu_espace` §5 lit
   des **positions** dans le HTML pour cette raison précise.

2. **Aucun calque absolu, et c'est délibéré.** Recouvrir le fil par-dessus obligerait à
   connaître la hauteur de l'en-tête — variable, il porte des badges qui passent à la
   ligne. On montre l'un en cachant l'autre : même case du flex, rien à mesurer. Le
   composeur s'efface avec le fil parce qu'il vit dedans — gratuit, et juste.

3. **La case est invisible mais focalisable** (`opacity: 0`, 1 px). Si tu la passes à
   `display: none` ou `visibility: hidden`, elle sort de l'ordre de tabulation et le
   panneau devient **inatteignable au clavier**. Le banc l'interdit.

**Le cadre « Rencontre » vide a disparu** — il se rendait sur tout fil à plus d'un membre,
proposition ou pas. Le formulaire vit maintenant dans le « + » du composeur.
⚠️ **Et c'est un LIEN, pas un formulaire** : ce panneau vit dans le `form_with` du
composeur, et un `form` imbriqué est supprimé en silence par les navigateurs — le geste
paraîtrait posé et ne partirait jamais.

**Deux leçons de mesure, transposables telles quelles :**
- J'ai déclaré une finalité « absente » d'une page où elle s'affichait : je comparais une
  chaîne brute à du HTML **échappé** (l'apostrophe). Un texte de joueur ne se cherche
  jamais tel quel dans une page.
- Mon banc a échoué sur « les noms de famille ne sont pas dans l'en-tête » parce que le
  nom choisi, « Apercu », se cachait dans « ZZApercu », le nom de l'espace. Un témoin doit
  être reconnaissable entre tous les textes qu'il traverse.

**Ce que je n'ai pas fait** : l'illustration du groupe. Boris l'a nommée comme contenu du
panneau ; le monogramme (96×96) **tient sa place exacte**, mais le téléversement demande
son propre lot — stockage, recadrage, modération. Quand l'image arrivera, elle remplacera
ce bloc sans déplacer une ligne autour.

En production, 12 bancs verts, témoins intacts (25 comptes · 423 Ω · 16 Validations).
