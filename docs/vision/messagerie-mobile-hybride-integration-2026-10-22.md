# Échanges M1 : livraison des maquettes et notes d’intégration

> Note Codex — 22 octobre 2026. Livraison explicitement demandée par Boris :
> « Pousse à Claude avec les notes complètes d’intégration ».
> Référence de conception interactive ; aucun déploiement effectué par Codex.

> Ajout Codex — relecture suivante : [contrats et écarts du lot 1](messagerie-hybride-relecture-codex-2026-10-22.md).
> Elle prend en compte les arbitrages plus récents de Boris (Point Zéro dès M0) et précise les non-lus.

> Relevé suivant : [portage strict, suivi de lecture et textes Mentor M1](messagerie-relecture-portage-strict-et-mentor-2026-10-23.md).
> Écarts qualifiés, choix des 18 smileys, défauts de suivi transmis dans les PR.

## Livraison identifiée

- Dépôt : `PointZero2050/zegame-prototypes`.
- Branche : `codex/messagerie-m1-popup-unique-20261018`.
- Commit livré : **`3a32dbe6b21cc64eeaad9ccb77c6e93815965905`**.
- [Notes complètes, manifest des fichiers, analyse d’impact et prompt de reprise](https://github.com/PointZero2050/zegame-prototypes/blob/3a32dbe6b21cc64eeaad9ccb77c6e93815965905/messagerie-par-mondes-cible/INTEGRATION-CLAUDE.md).
- [Maquette principale : index et modules](https://github.com/PointZero2050/zegame-prototypes/tree/3a32dbe6b21cc64eeaad9ccb77c6e93815965905/messagerie-par-mondes-cible).
- [Capture de la passe finale](https://github.com/PointZero2050/zegame-prototypes/blob/3a32dbe6b21cc64eeaad9ccb77c6e93815965905/messagerie-par-mondes-cible/review/messagerie-passe-ux-finale.png).

Ces notes constituent la synthèse actuelle. Les documents historiques du même
dossier ont un renvoi en tête : ne pas porter leurs états intermédiaires de menus,
six réactions ou grand bandeau d’aide. Le commit contient tous les travaux locaux
du 22 octobre précédemment non transmis, ainsi qu’un correctif de texte : une
demande de conservation en Mémoire s’adresse à **l’auteur**, pas au groupe.

## Écrans à servir pour la reprise

Cloner le dépôt et servir sa racine en HTTP statique. Ouvrir :

- `/messagerie-par-mondes-cible/?stage=m1circle` : référence principale.
- `/messagerie-par-mondes-cible/?stage=m1circle&actions=1` : composeur « + ».
- `/messagerie-par-mondes-cible/?stage=m1circle&guests=demo` : regards invités.
- `/messagerie-par-mondes-cible/compact.html?case=mixed&width=390&status=read` :
  banc isolé, avec états zéro, chargé et extrême ; essayer aussi 320 et 430 px.

Le serveur local de Boris est actuellement `http://127.0.0.1:8792/` ; ce n’est
pas une adresse distante. Récupérer le dépôt complet pour conserver les assets
voisins. Aucun compte de préproduction n’est requis pour ouvrir cette maquette.

## Décisions finales à porter

1. Pied compact **dans** la bulle : smileys, Source/résonances, réponses, puis
   heure et état des messages envoyés seulement. Trois interactions à gauche
   espacées ; heure à droite. À zéro, invitation indépendante en pastille ;
   elle devient compteur dès la première contribution. Détail sur demande.
2. Même pied et mêmes règles sur les réponses, dans leur discussion ET leur
   projection chronologique. Les « … » servent toujours à gérer le message :
   Modifier / Supprimer / Mémoire selon auteur, type, droits et état réels.
3. Sept résonances. Ombre : **Cela m’invite à plonger**, **Cela dévoile un masque**,
   **Merci d’oser l’inconfort**, icônes adaptées, blanc sur noir. Lumière inchangée :
   Je soutiens / Cela résonne / J’apprends. Septième ligne Source/Tao :
   **Point Zéro - Fait circuler Ombre et Lumière**, sans titre séparé.
   Fenêtre ouverte par Source : **Tes résonances**.
4. Fil hybride : parent à sa place, réactions sans remontée ; réponse écrite
   visible à sa date avec citation cliquable. Même objet dans les deux vues,
   un seul incrément. Réponses consécutives à une même racine regroupées ;
   toute autre contribution intercalée coupe le groupe. Citer une réponse
   précise reste dans la même discussion racine, sans imbrication infinie.
5. Groupes de nouvelles réponses et ouverture à la première non lue ; lecture
   partielle sans saut ni marquage global des éléments cachés. La visibilité à
   60 % est une simulation locale, pas une règle serveur validée ni un accusé
   « lu ». Préserver la position pendant lecture de l’historique.
6. Aide de première visite compacte puis masquée après consultation/fermeture ;
   toujours accessible depuis le menu supérieur **Aide de la messagerie**.
   Persistance dans l’onglet seulement en démo.
7. Conserver l’en-tête validé : Afficher : Fil sous le nom, filtres d’objets,
   membres en petit à droite, recherche et menu « … ». Conserver aussi les
   fenêtres uniques du composeur, recherche Graine/Trace et regards invités.

## Contrats et limites à préserver

**Portable : analyse d’impact avant implémentation de cette zone sensible.**
Inspecter l’application actuelle (`pointzero-app`) : réponses/racines/citations,
types de réactions, agrégats et concurrence, droits, lecture par membre,
pagination/temps réel, notifications et Mémoire. Ne pas inventer un schéma ou
endpoint à partir des noms des variables JavaScript de la maquette.

Les anciennes réactions Ombre ont un autre sens : **pas de requalification
silencieuse des votes historiques**. Proposer la compatibilité/migration ;
ajouter un identifiant stable au nouveau choix Point Zéro. Aucun gain d’Omégas.

Préserver la [Mémoire V1](memoire-du-groupe-v1-2026-10-21.md) et son
[analyse d’impact](../architecture/memoire-du-groupe-analyse-impact.md), notamment
consentement de l’auteur sur la version, liens/pièces jointes, reconfirmation et
retrait. Ne pas remplacer les livraisons #456 / #457 par la simulation locale.

Regards IA : décision de Boris maintenue, **accord explicite par fil avant
lecture**. Ne pas étendre le périmètre personnel/collectif ni les droits parce
qu’une réponse revient dans le flux. Les dialogues IA de la maquette sont scriptés.

Tous les participants, volumes, réponses et états de réception sont fictifs.
Édition/suppression, Mémoire, envoi et compteurs sont des mutations locales, pas
une API, une sauvegarde, des notifications ou des garanties d’autorisation.
La démo ne doit pas fournir de faux succès dans l’application portée.

## Coordination et recette

Poste fixe : portage des vues/styles/icônes ; portable : contrats et données,
relecture et intégration serveur. Suivre la [répartition des agents](repartition-agents-phase-2.md),
préserver les fonctions déjà servies et annoncer le chantier avant toute reprise
qui pourrait se superposer à une livraison en cours.

La recette détaillée figure dans la référence complète : largeurs 320–430 px et
desktop, zéro/extrêmes, droits auteurs/autres/espace clos, sept résonances et
historique, réponse à réponse, suppression et compte unique, parent non chargé
ou inaccessible, concurrence/reconnexion, non-lus avec deux comptes, Mémoire
versionnée, consentements IA, recherche/filtres/notifications, aide réouvrable,
clavier/focus/lecteur d’écran et téléphones iOS/Android physiques.

Les vérifications locales documentées couvrent les interactions et rendus de
la maquette, dont les réponses à 390 px, les totaux, citations, menus, filtres,
non-lus simulés et aide. Elles ne valent pas une validation serveur, multi-compte
ou sur appareils physiques. Ne pas déduire d’une capture une intégration servie.

Le push constitue une transmission GitHub par les boîtes habituelles. Il ne
prouve pas que Claude a déjà lu le lot, ni que le portage est fusionné ou déployé.
