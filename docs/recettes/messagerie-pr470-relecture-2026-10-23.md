# Messagerie : relecture de #470 et contre-épreuve supplémentaire

> Note Codex — 23 octobre 2026. Relevé demandé par « r&c ».
> Relecture des sources et tests locaux ; aucun compte, donnée applicative ou
> déploiement modifié par Codex. Le serveur temporaire était limité à 127.0.0.1.

## Correctif relu et état de livraison

[PR #470](https://github.com/PointZero2050/pointzero-app/pull/470), révision
`6c6e5748998ca13f2ded54fda393c9700b08b493`. Fusionnée pendant la relecture ; le
portable rapporte une mise en service à `2975122` et dix bancs Rails verts.
Codex ne rejoue pas ces bancs ni une recette en écriture sur la préprod.

La relecture est [déposée dans la PR](https://github.com/PointZero2050/pointzero-app/pull/470#issuecomment-6361373013).

## Dix tests rejoués localement

`scripts/epreuve_messagerie/index.html` et `cas.js` de la PR ont été servis avec
le `messagerie.js` exact de cette révision. Adaptation locale uniquement :
chemins statiques et bouton visible lançant les tests, avec résultat affiché.
Le `fetch` de l’épreuve est simulé et résolu à la main : aucune requête Rails.

**Résultat sur #470 : 10/10 OK.** Les cas couvrent :

- flux du même contenu ;
- flux A après ouverture de Modifier B, et flux étranger pendant un brouillon ;
- flux étranger sans brouillon et fermeture pendant l’attente ;
- réponses réseau A/B inversées et refus de A après ouverture de B ;
- rechargement de deux pages avec conservation de la position ;
- absence de nouvelle observation dans un document masqué ;
- réponse de 1 000 px dans une zone de 400 px.

Contre-épreuve avec `def67c9` : T2, T3, T8, T9 et T10 échouent dans cette
exécution. T6 passe ici : le bilan de Codex est donc cinq échecs reproduits,
pas la recopie des six annoncés par Claude. Les minuteries du banc au navigateur
restent sensibles au contexte d’exécution ; la garde réseau est également relue
dans le diff. [Sortie exacte des tests](messagerie-pr470-resultats-2026-10-23.txt).

Contrôles de syntaxe locaux : `node --check messagerie.js` et `cas.js`, propres.

## T11 : deux bascules en vol laissent la fenêtre sur le premier état

**Défaut reproduit sur la PR**, à corriger en suivi de sa fusion.

Le gestionnaire garde un seul `envoi`, remplacé à chaque soumission. Sa
`generation` change à chaque repeint et pas seulement à la navigation vers
un autre contenu. Cela combine mal deux réactions rapprochées dans la même
fenêtre :

1. Ouvrir le contenu `emoji-1` ; soumettre deux formulaires distincts A et B
   avant le retour du premier flux.
2. Remplacer le gabarit par v2 puis annoncer le flux de A. Le dernier envoi
   mémorisé est B : A est traité comme étranger et repeint la fenêtre en v2.
   `peindre` avance la génération.
3. Remplacer le gabarit par v3 puis annoncer le flux de B. L’envoi B porte la
   génération précédente ; il est ignoré. La fenêtre garde **v2** au lieu de **v3**.

Le cas a été ajouté localement à la fausse fenêtre avec deux formulaires et
les mêmes événements `submit` / `pz:flux-applique` : résultat v2 reproduit.
`public/pz/m0/fil.js` a également été lu sur la révision de la PR : les réactions
ne sont pas sérialisées et le bouton neutralisé est seulement celui du
composeur. Deux choix distincts peuvent donc être envoyés avant leurs réponses.

Pistes à choisir par le poste fixe : distinguer l’identité d’une ouverture
d’un simple repeint et suivre individuellement les requêtes, ou sérialiser les
bascules. Préserver les gardes de brouillon et de navigation. Ajouter ce T11,
puis tester aussi les retours inversés des deux envois. Ne pas réintroduire
T2/T3 pour réparer le rafraîchissement de la palette.

## Autres points de la boîte

- Liens de profil sur les noms des réponses humaines : cohérents avec la règle
  existante ; pas de profil fictif pour un regard ou guide.
- Coche Point Zéro : les réserves de place du compteur et de la sélection sont
  cohérentes. Une ligne reste préférable là où elle tient ; un repli du libellé
  à très petite largeur évite de diminuer encore le texte. Pas de nouvelle
  mesure du CSS servi en préprod déclarée dans cette passe.
- Textes du Mentor à `0869aa0` : réception du portage au mot près et de la
  recette des trois états rapportée par le portable. Les statuts et marqueurs
  historiques ne sont pas renommés dans ce lot éditorial.
- Arbitrages de navigation rapportés dans [#468](https://github.com/PointZero2050/pointzero-app/pull/468) :
  les trois interactions sont dans les « … » **des messages d’autrui**, avant
  l’éventuelle Mémoire ; gestion des messages personnels inchangée. Entrer par
  Échanges ouvre la messagerie sans le sous-menu J’exprime ; entrer par
  Communication conserve le contexte de rubrique via `depuis=communication`.
  Les notes sont précisées pour refléter cette portée, plutôt que d’étendre
  automatiquement les commandes des menus personnels.

Les trois nouveaux messages traités sont retirés de la seule boîte Codex ;
leurs références et réponses restent dans Git et dans les boîtes destinataires.
