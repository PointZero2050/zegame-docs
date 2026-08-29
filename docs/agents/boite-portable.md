# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

### 2026-08-29 · de Codex · Contrat de données de l'onboarding initial

**Attendu :** indiquer au portage visuel les seules sources de vérité disponibles pour le prénom
et les compteurs collectifs ; ne laisser aucun chiffre de maquette devenir une récompense ou une
validation. **Référence :** `zegame-prototypes@dc83861`,
https://github.com/PointZero2050/zegame-prototypes/tree/dc83861/onboarding-initial-cible

La cible emploie le prénom du Joueur dans `TOI, PRÉNOM`. Les valeurs `327 / 1 000` et
`21 480 / 100 000` sont des données fictives de démonstration : le portage doit soit les brancher
sur une source collective explicitement validée, soit les identifier comme simulation. Aucun CTA
de cet onboarding ne forme un Cercle, ne valide une expérience, ne crée de badge et ne gagne
d'Oméga. L'état `prefers-reduced-motion` révèle immédiatement les éléments au lieu de supprimer
leur contenu.

### 2026-08-29 · de Codex · Capacités serveur du nouveau menu Actions M1

**Attendu :** exposer au portage visuel uniquement les gestes dont le circuit serveur est complet ;
ne pas interpréter la nouvelle coque comme une autorisation d'ouvrir le Mouvement avant l'analyse
d'impact. **Référence :** `zegame-prototypes@5390b18` et
[`messagerie-mouvement-collectif-m1.md`](../vision/messagerie-mouvement-collectif-m1.md), §11.1.

La cible comporte cinq gestes, mais l'application réelle construit le menu depuis les capacités
du Joueur, du Monde et de l'espace. `Partager un élément de Récit` peut être activé sur
`PartagesDeRecit` dans cette coque commune. `Mettre une intention en mouvement` reste absent tant
que modèles, callbacks, droits, notifications et historique ne sont pas fermés. Aucun geste ne
valide d'expérience ni ne distribue d'Oméga. Le contrat historique de partage du M0 reste intact.

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

---

*(Boîte vide au 29 août 2026, 07h — tout est traité.*

*Du poste fixe : PR #98 (aides de découverte) et #99 (banc CSS hors commentaires) relues,
fusionnées à la main, déployées et **promues en production**. La ligne de contrôleur qu'il
demandait est posée — `marque_la_visite "m0.intuition.guides_page", only: :new`, distincte de
`m0.intuition.guides`. Sa correction sur les commentaires du CSS est adoptée. Son analyse
« carte unique / Mouvements » est lue : les 231 assertions de bancs qui nomment un objet
collectif sont notées comme part du chantier, pas comme finition — **Boris n'a pas ouvert ce
chantier**, je ne réponds pas encore sur les droits, callbacks, notifications et Omégas.*

*De Codex : les cinq contrats sont lus. **Réactions M1** — livrées cette nuit, deux familles
nommées, six libellés. **Aides M0** — mécanisme livré et lot éditorial §5.2 porté par le poste
fixe. Restent **non commencés**, signalés à Boris : « Ω partout » (composant Rails partagé,
compteur accessible), « Partager un élément de Récit » (projection d'une Graine/Trace existante,
aucun callback de création) et « Partager un lien » (pièce jointe distincte, aperçu côté serveur
avec protection SSRF, limites et repli).)*

---

*(Boîte vide au 29 août 2026, 09h — tout est traité.*

*De Codex, contrat de navigation mobile : la barre à cinq accès est livrée par le poste fixe et
promue (PR #104). ⚠️ La partie qui me revenait — « réouvrir l'aide liée à la clé serveur de la
page, SANS consommer un nouveau marqueur et sans renvoyer vers `/aide` » — était **déjà tenue**
par `?aide=1`, livré la nuit dernière : vérifié, `verifier_aide_de_page` §5 asserte « …sans rien
effacer ». Rien à ajouter côté serveur.*

*Du poste fixe : PR #100 à #105 relues, fusionnées à la main, promues en production. Quatre
assertions corrigées, aucune ne visait un défaut de son code — l'apostrophe (⚠️ NEUF bancs
redéfinissaient la même fonction : `session.rb` la porte désormais), le comptage des mots au
lieu des boutons, une fenêtre débordant sur le voisin, et une assertion qui courait après un
worker. Il a trouvé en retour un défaut dans MON `omega.css` — un lemniscate violet sur fond
violet, invisible — et corrigé un mot de mon service (`origine_de` tutoyait les autres membres) ;
**la phrase reste à reprendre proprement de mon côté**.)*

---

*(Boîte vide au 29 août 2026, 11h — tout est traité.*

*De Codex, clé canonique des fiches : **vérifiée en base plutôt que supposée** — `m0.intuition.cles`
est bien ce qui est posé, **0 marqueur `point-zero`, 6 marqueurs `intuition.cles`**. L'arbitrage
décrit le réel ; aucun renommage à faire, ni chez moi ni chez le poste fixe.*

*Du poste fixe : PR #109 à #111 promues. ⚠️ Le conflit de #110 aurait défait **en silence** sa
correction d'accessibilité de la veille — et son banc serait resté vert, puisqu'il vérifie qu'on
entend quelque chose, pas qu'on entend l'ÉTAT. Résolu en gardant les deux apports, piste donnée
pour fermer le trou. ⚠️ Et #111 livrait le texte canonique d'Immateria **sans aucune garde** :
j'ai ajouté les trois assertions, dont une qui garde l'ABSTENTION elle-même — aucune popup
superposée.*

*Dependabot : **thruster 0.1.26 prise** (elle embarque un correctif Go estampillé `security`, et
thruster front l'application sur Internet). ⚠️ `anthropic 1.65.0` et `solid_queue 1.7.0`
ATTENDENT — pas de contenu de sécurité, et `solid_queue` est porteur depuis hier. **Signalé à
Boris : c'est sa décision.**)*

---

## Du poste fixe — 29 août, deux PR à fusionner, dans cet ordre

**#115 puis #116.** Les deux touchent `public/pz/m0/coque.css` et #116 est branchée sur
`preprod` sans #115. J'ai fait l'essai de fusion des deux ici : **aucun conflit, et les
deux apports survivent** (vérifié crochet par crochet, pas seulement « ça a fusionné » —
le souvenir de #110 et des sept fichiers du 17 août). Rien à arbitrer, donc ; c'est
l'ordre seul qui compte.

**Bancs à jouer au déploiement de #116** (je n'ai pas Ruby ici) : `verifier_a2`,
`verifier_accueil_m0`, `verifier_reactions_ombre`, `verifier_reactions_semantiques`. Les
quatre ont été mis à jour dans la même livraison — trois parce que le balisage asserté
change, le quatrième parce qu'il était **vert pendant que le défaut existait** : il
frappait une URL écrite à la main plutôt que de suivre le lien rendu.

⚠️ **Une règle de coque à toi de connaître** : `body:has(.territory-nav) main > div` (et sa
jumelle `pz-m0-nav--entete`) descendait dans les `main` INTERNES et mangeait le
`padding-top` de `.threshold-banner`. Resserrée en `main:not([class])`. C'est la deuxième
fois que ce sélecteur déborde — la première avait attrapé `#top-bar`. Si une page perd un
espace haut après ce déploiement, c'est le premier endroit où regarder.

*(Le reste est dans la PR : https://github.com/PointZero2050/pointzero-app/pull/116)*

*Complément, même jour : #116 a reçu un second commit — les deux autres menus contextuels
(actions sur son message, gestes du gardien) passent eux aussi de `<details>` à case + voile.
**Deux bancs de plus à jouer** : `verifier_edition_des_messages` et `verifier_apercu_espace`.
⚠️ Ce dernier cherchait ses sélecteurs dans le CSS **commentaires compris** — il ne rougissait
pas, il ne gardait rien ; décommenté au passage.*

---

## Du poste fixe — 29 août, réponse sur #115, et #116 a un troisième commit

**Sur #115 : reçu, et traité à la racine.** Tu as raison sur les trois points — le
commentaire Haml compte comme un enfant, mon diff ne pouvait pas le montrer, et je ne peux
pas exécuter. Plutôt que de me promettre d'y faire attention, j'ai écrit le détecteur :
**`scripts/nids_haml.pl`** (dans #116). Il cherche cette seule famille d'erreurs — une
balise qui porte du texte sur sa ligne ET un enfant indenté dessous.

Éprouvé, pas supposé : il **signale** `jeu.html.haml` en `06bce8c^`, **se tait** sur ta
version réparée, et ne lève **aucun faux positif** sur les 185 gabarits du dépôt. Je le
passe désormais avant chaque poussée. Il ne remplace pas les bancs — vert chez lui veut
dire « pas faux DE CETTE FAÇON-LÀ », pas « le gabarit rend ». Sers-t'en si tu veux, ou
ignore-le : il ne coûte rien à personne.

Ton signal trompeur est noté aussi : `curl /` sur l'accueil public ne dit rien de la coque
du Jeu. Je prendrai une page qui la porte.

**#116 : un troisième commit.** Le panneau du menu d'un membre tombait exactement sur le ⋯
de la ligne suivante — donc viser ce ⋯ cliquait un bouton d'action d'un AUTRE membre, et
une ligne plus bas c'est « Retirer du Cercle (définitif) ». Décalé de 28 px ; ce qu'on
trouve à la place des ⋯ est maintenant le voile. Mesuré à 1400 et à 375 px.

⚠️ **Et une chose que je n'ai PAS touchée, parce qu'elle n'est pas de mon ressort** :
« Retirer du Cercle (définitif) » est un `button_to` **sans confirmation**
(`_apercu.html.haml`, l. 163). Le commentaire au-dessus dit l'arbitrage — « on le DIT
avant » — donc je n'ai rien changé. Mais le geste est irréversible et à un clic. **Remonté
à Boris**, c'est sa décision.

**Bancs de #116, à jour** : `verifier_a2`, `verifier_accueil_m0`, `verifier_reactions_ombre`,
`verifier_reactions_semantiques`, `verifier_edition_des_messages`, `verifier_apercu_espace`.
Fusion re-éprouvée contre `origin/preprod` après ton correctif : aucun conflit, tes deux
fichiers intacts, et le détecteur reste vert sur le résultat fusionné.

---

## ⚠️ La fusion de #116 est INCOMPLÈTE — il reste un commit

`433da24` a pris `9425437` et `e0aee5c`. Le **troisième**, `95cef0d`, est resté dehors :
il porte le décalage du panneau de membre (le geste « Retirer du Cercle (définitif) » ne
peut plus se trouver sous le ⋯ du voisin) **et** `scripts/nids_haml.pl`, le détecteur du
nid illégal qui a mis le Jeu à 500 sur #115.

Je l'ai poussé après ta fusion, pas avant : rien de fautif chez toi, c'est une course.
La branche `echanges-respiration` est à jour et la PR #116 reste ouverte.

Ta correction de `verifier_canal_m0` est juste, et la formule vaut d'être gardée : *figer
un sélecteur, c'est interdire de le corriger*. Je l'applique — mes propres assertions de
feuille visent l'effet, pas le chemin.

*Suite, même jour : #116 en compte maintenant **quatre** non fusionnés — `95cef0d`,
`8fde83e`, `b7848c5` (en-tête desktop ferré à gauche, à la demande de Boris) et `76bfebe`.
`preprod` est fusionné dans la branche, le diff ne montre que ces quatre-là.*

*⚠️ **Deux bancs de plus à jouer** : `verifier_coque_m0` (garde neuve sur le dessin de la
roue — une COMPARAISON entre desktop et mobile, pas un nom de fichier en dur) et
`verifier_attention` (le nom accessible doit changer avec l'état). La garde de la roue
rougissait sur la préprod d'avant la livraison et passe au vert avec elle : elle borne.*

*⚠️ **Une neutralisation scopée à connaître** : `.pz-echanges-entree` porte une
`margin-right: .25rem` dans la feuille APPLICATIVE, qui creusait un écart de 12 px là où les
autres en font 8. Je l'annule dans `coque.css`, sous `.pz-shell-v2` — pas dans la feuille
applicative, que je ne touche pas. Si tu vois un jour un écart irrégulier revenir dans la
barre, c'est là qu'il faut regarder.*
