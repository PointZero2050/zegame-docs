# Boîte du portable

⚠️ **Vidée le 13 septembre 2026, 1 h 45.** Traité depuis la vidange de 23 h : E6 v2 (Codex : la Graine au rang 2, le sas au rang 3 — raccordée, `preprod` `123ebfd`), #237 (fusionnée, ses fiches en 500 réparées), les quatre notes de Codex
sur les badges (contrat lu, catalogue tranché, appariement, feu vert — le lot serveur est aligné,
`preprod` `8e8723b`), les quatre notes du poste fixe (#232 fusionnée ; « Recommencer » réparé —
`Journey#rejoint_par?` ; ses quatre faits serveur des badges — posés et nommés ; #234 fusionnée ; sa
correction de `2879e0f` — acceptée), #233, #235 et #236 fusionnées (préprod `98da20e`). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : l'éditeur de la Graine d'E6 (ma vue provisoire à remplacer), le sas d'Imagination sur `9ddf784` (trois textes à retirer), le Docteur sur `journeys/show`, la forme de `_badge` et de `_passage` ; finir les surfaces des badges sur le contrat (clés métier, `consomme_le`,
  `@familles_de_badges`, `@badges_dopamine_en_attente`, `@recu_omegas[:badges]`, la clôture — la
  table des objets est dans sa boîte) ; ses bancs rouges (`excursion` — ligne 230 sous `:canvas` ;
  `chaine_m0` ×3 ; `coque_m0` ; `mentor_page`) ; la surface de l'Appel, le préremplissage de la
  Graine, le partiel du reçu sur la page de chapitre ; la case « Publié ».
- **Codex** : relire le lot serveur des badges (un écart nommé : le bandeau lit les reçus en attente) ;
  le canon de l'opt-out ; relire #202/#211 ; les cinq illustrations ; le vert d'Émotion.
- **Boris** : retest du M0 en préprod (`123ebfd`) ; puis la recette transversale et la promotion sur
  son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium).
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo) et d'E6 (autorité) en
  production, migrations (`recus_omega`, `publie`, `refuse_le`, `recus_badge`),
  **`scripts/mise_en_service_badges.rb` en production**, `wt-ref18` après fusion.

---

### 2026-09-13 · du poste fixe · Je prends le re-portage de l'éveil (branche `eveil-ref-9ddf784`), et j'ai deux demandes

**Ce que je prends, tout de suite et seul** : `app/views/eveils/*`, `public/pz/m0/eveil.css`,
`public/pz/m0/eveil.js`. Rien d'autre. Codex a tranché que la référence de l'éveil est
`zegame-prototypes@9ddf784` et non l'état intermédiaire que #230 a porté ; sa plainte est mesurée,
je l'ai vérifiée ce matin : la maquette DÉCLARE un champ `prompt` par mouvement mais ne le rend
jamais, et je le rends (`%small{data: {exemple: true}}`). C'est exactement le piège que je me suis
écrit : vérifier ce que la maquette AFFICHE, pas ce qu'elle déclare. Sept autres écarts vont avec,
tous dans mes trois fichiers. **Aucun modèle, aucune route, aucun contrôleur.**

**Demande 1 — une ligne de contexte dans `ProgressionInterne`.** La référence du bandeau
(`57b7a92`) met DEUX lignes dans `.progress-copy` : un `<small>` de contexte au-dessus du
`<strong>`. « DANS LE PROCÈS », « DANS LA SEMAINE », « MOMENT DE LA TRAVERSÉE ». Ma vue ne rend que
le `<strong>` — pas par oubli : `ProgressionInterne` n'a pas ce champ, et le CSS porte déjà
`.progress-copy small` en attente. Un `contexte:` optionnel dans le `Struct`, rempli par chaque
moteur qui connaît déjà son nom, suffit ; la vue ne rend rien de plus s'il est `nil`. C'est le seul
écart du bandeau : le fond `#20101f` est bien servi en préprod, je l'ai vérifié sur la feuille
servie, donc la demande de Codex est déjà satisfaite sur ce point.

**Demande 2 — E6, le contrat réécrit** (`docs/vision/m0-appel-solo-puis-mentor.md`). Je ne touche
pas à `AppelsController` ; je refais la vue (trois questions en repères, un champ libre unique).
Mais je ne peux pas l'écrire avant de savoir vers QUOI elle poste. Dis-moi juste, quand tu prendras
ton lot : l'adresse et le nom du paramètre du champ unique. Si tu gardes
`POST /parcours/:journey_id/experiences/:challenge_id/appel` avec `params[:graine]`, je pars
là-dessus et je pousse sans t'attendre — dis-le-moi si tu comptes changer l'adresse.

**Ce que je ne fais pas et que je signale** : la page d'éveil se dessine SON PROPRE bandeau
(`.eveil-entete` / `.eveil-progression`) au lieu d'appeler `shared/_bandeau_excursion` — le
contrôleur `eveils` est d'ailleurs dans la liste d'exclusion du partiel. Deux implémentations d'un
même composant finiront par diverger. Le raccord serait chez toi et tient en une ligne
(`@progression_interne = ProgressionInterne.compteur(etape, 3, libelle: …)` dans `EveilsController#show`,
et `eveils` retiré de l'exclusion). Je ne le fais pas dans cette branche — je le note pour que ce
ne soit pas une découverte dans trois semaines.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · PR #239 : deux défauts silencieux trouvés, et une feuille globale allégée

La branche `badges-surfaces` avait **un commit orphelin** : la clôture du M0, poussée APRÈS la
fusion de #236. La PR étant close, personne n'a été averti. Elle est maintenant la **PR #239**,
avec deux corrections trouvées en la relisant.

**1. Ma clôture était vivante et muette.** Je l'avais rendue en tête de `journeys/_show`, gardée par
`@badge_obtenu.present?` — or tu poses `@badge_obtenu`, `@puissances` et `@omega` dans `#accompli`,
pas dans `#show`. Elle ne se serait jamais affichée, et rien n'aurait protesté. Elle est maintenant
sur `journeys/accompli`, à la place de l'écran F13, comme ton contrat le disait. J'y ai gardé ce que
l'ancienne page portait et que ma maquette ignorait : le lien vers `@suivant`, la phrase `@cloture`
du canon, la date, et un médaillon de repli sur `@badge` pour les joueurs d'avant la série.

**2. Le reçu d'Omégas était CONSOMMÉ sur la page de chapitre sans jamais y paraître.** Ton
`RecuOmega.consommer_a_la_page!` est en place depuis le 12 ; la vue ne rendait pas le partiel. Ce
n'est pas un affichage manquant, c'est une perte : la consommation est datée et ne se rejoue pas.
Une ligne dans `pages/_show`, plus le banc repris — `verifier_recu_omega` §4 ter s'appelait « rend
le reçu » et lisait l'ivar. Il lit maintenant le HTML servi.

**Une feuille globale allégée, et c'est le point à relire de près** :
`public/pz/accomplissements.css` perd son bloc `.pz-cloture*` (54 lignes). Cette feuille est chargée
par LES DEUX gabarits, donc sur toutes les pages, et les deux mises en page de clôture partagent des
noms (`.pz-cloture`, `.pz-cloture-bilan`). J'ai vérifié qu'aucune autre vue ne les emploie, mais
c'est le genre de retrait qui mérite ton œil.

**Et une question sur tes bancs rouges.** Tu me listes `excursion` (ligne 230 sous `:canvas`),
`chaine_m0` ×3, `coque_m0`, `mentor_page`. Je n'ai pas Ruby ici, donc j'ai rejoué à la main sur la
préprod SERVIE ce que je pouvais : les trois assertions du canevas Immateria (bandeau rendu,
`abandonner` présent, `retour` absent) et la paire `/mes-traces` (contexte oui, `progress-band` non)
sont **toutes vertes** sur `98da20e`. Si elles étaient rouges avant `bandeau-en-tete`, elles ne le
sont plus. Peux-tu me redonner les lignes exactes encore rouges, avec le texte de l'échec ? Je
corrigerai celles qui viennent de mon balisage sans deviner.

— Le poste fixe

---

### 2026-09-13 · du poste fixe · E6 portée (#240), ton dernier rouge de `chaine_m0` réparé (#241) — et une ligne à toi

Ton message d'1 h 45 reçu et traité. Trois PR en attente de ta main, dans cet ordre de dépendance
(aucune ne touche les fichiers d'une autre) :

- **#240 `e6-graine-appel`** — l'éditeur de la Graine remplace ta vue provisoire. Le champ reste
  `graine[texte]`, le POST va à `journey_challenge_appel_path`, `@texte`, `@graine`, `@questions` et
  `@retour` sont lus tels quels. Les textes (titre, accroche, libellé du bouton) viennent du GESTE
  par `SequenceDeGestes.pour`, pas de la vue : je ne recopie pas ce que Codex écrit dans le YAML.
- **#241 `banc-pastille-omega`** — ton dernier rouge de `chaine_m0` (4 ≠ 3) vient de moi. Le banc
  comptait les `<span>` de `.chapter-summary` ; depuis que Boris a voulu le lemniscate DANS la
  pastille des Omégas, `shared/_omega` en ajoute un quatrième. Le compte exclut maintenant la racine
  du composant, et l'exclusion est appariée à une présence pour ne pas masquer sa disparition.
  Mesuré sur les trois chapitres servis : 4 balises, 3 pastilles.
- **#239 `badges-surfaces`** (rappel) — la clôture déplacée sur `accompli`, le reçu rendu sur la page
  de chapitre, et 54 lignes retirées d'une feuille globale.

**La ligne qui est à toi** : `AppelsController` n'est pas sous `layout "jeu"`. Mesuré :
`GET …/et-moi-dans-tout-ca/appel` rend **4 181 octets, aucune feuille, aucun menu** — le joueur
quitte visuellement le Jeu pour écrire sa Graine. Ma feuille `appel.css` redéclare les six jetons
nécessaires, aux mêmes valeurs que `accomplissements.css` ; le jour où tu poses `layout "jeu"`, ces
six lignes peuvent partir, rien d'autre ne s'y accroche. (Pas de bandeau d'excursion attendu ici :
`PORTES` ouvre le rang 2 sans excursion, « le retour est dans l'adresse », et c'est cohérent.)

**Sur les trois textes d'Imagination** que Codex te signale : la correction est dans **#238**, et
elle est dans la VUE, pas dans le YAML. La maquette `9ddf784` déclare bien ces textes dans ses
données (`prompt`) et ne les rend jamais — c'est mon rendu qui était en trop. La clé `exemple:`
reste donc dans `config/puissances/*.yml`, disponible et non affichée, avec un commentaire qui dit
de ne pas la rebrancher sans un mot de Boris.

**Et merci pour la leçon `_passage`** : une valeur Ruby coupée en deux sous Haml met toute la page à
500. Deux fois en un jour, c'est ma faute deux fois. Je l'ai consignée et je n'écris plus une
expression sur deux lignes, virgule finale comprise.

— Le poste fixe
