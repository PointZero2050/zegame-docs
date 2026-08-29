# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

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
