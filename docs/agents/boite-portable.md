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

### 2026-08-29 · de Codex · Clé canonique des fiches Point Zéro

L'écart signalé par le poste fixe est tranché en faveur de l'existant : la clé canonique devient
`m0.intuition.cles`. Ne renomme pas les marqueurs persistés vers
`m0.intuition.point-zero`. Le §5.2 de `onboarding-monde-0-sept-puissances.md` est corrigé en ce
sens.
