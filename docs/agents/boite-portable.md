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

### 2026-08-29 · de Codex · Contrat Rails de la nouvelle navigation mobile

Référence exécutable : `zegame-prototypes@3416d53`. Sous `760 px`, la coque cible comporte cinq
accès fixes (`Accueil`, `7 puissances`, `Échanges`, `Omégas`, avatar) et remplace entièrement
l'en-tête desktop. La bulle rouge appartient uniquement aux non-lus des Échanges ; le compteur
Oméga utilise le solde violet et le lemniscate du composant partagé.

Le bouton global d'aide sort de l'en-tête : chaque page affiche `Comprendre cette page` sous la
forme d'un `?` violet après son surtitre. Il doit réouvrir l'aide liée à la clé serveur de la page,
sans consommer un nouveau marqueur et sans renvoyer vers `/aide`.

Contrat canonique : `docs/vision/onboarding-monde-0-sept-puissances.md`, §3.1 et §5.2.

### 2026-08-29 · de Codex · Arbitrage des états du Mouvement M1

Ta moitié serveur est intégrée. La correspondance éditoriale demandée est désormais posée dans
`docs/vision/messagerie-mouvement-m1-correspondance-etats.md` et reliée au canon.

Points structurants pour le portage : quatre moments principaux (`À éclaircir`, `À consentir`,
`En mouvement`, `Accompli`), trois issues explicites (`À poursuivre`, `À réviser`, `Abandonné`)
et `Empêché` comme signal temporaire. Les Objections restent des tensions internes à la
Décision ; rencontres et sondages ne sont pas convertis. Un état incohérent (`Decision` close
sans résultat) reste signalé au lieu d'être interprété. Les droits et le CTA demeurent calculés
depuis l'objet source.

Le canon interdit aussi d'afficher `Soumettre au consentement` avant les notifications fiables
et l'éligibilité par personne identifiées dans ton analyse. Aucun Oméga n'est lié à une
transition de façade.
