# Relecture du plan de migration des 18 verbes

Note Codex — 11 septembre 2026. Relecture du plan portable ; précise la mise en œuvre de la décision de Boris, sans annoncer une migration exécutée.

## Les décisions déjà couvertes

- Les 18 couples Puissance/polarité sont communs, y compris Imagination · JE CRÉE (#86). Le choix de Boris couvre les six Puissances et leurs trois verbes ; inutile de redemander une autorisation pour cette Source. Les droits du cercle restent indépendants.
- Affichage : **Puissance · VERBE**, sans nom d’amplitude ajouté au libellé courant. Les anciens noms restent dans la traçabilité et les descriptions pédagogiques.
- Les cinq destinations de `sas.yml` doivent désigner les clés Puissance/polarité, avec les mêmes montants et conditions. Vérifier chaque correspondance depuis le nom actuel. Une lecture de compatibilité peut servir au déploiement progressif, sans perpétuer les amplitudes comme destinations nouvelles.
- Le choix de l’identifiant conservé est technique : il ne fait pas de DISSOCIATION une signification privilégiée de JE DISTANCIE. La table mécanique proposée peut être conservée (#66 et #81 compris), à condition que tous les producteurs de points, dont le Sas, résolvent la cible unique. Ne pas recalculer cette désignation à chaque exécution : figer la table revue et arrêter sur divergence de données.

## Corrections nécessaires avant implémentation

### 1. Un référentiel sélectionnable de 18 compétences, pas 18 plus les anciennes

La voie (b) est adaptée à un référentiel commun distinct des droits des communautés. Mais la condition proposée « communauté publique OU canonique » et la liste « compétences de la communauté PLUS canoniques » continuent d’autoriser des amplitudes non canoniques, notamment publiques. Après bascule, les 24 anciennes lignes remplacées doivent être exclues de tous les nouveaux rattachements et attributions, côté serveur autant que dans le sélecteur. Les lectures historiques restent possibles selon les droits existants.

Traiter import, édition d’expérience, saisie directe d’identifiants et producteurs de points. L’import ne doit pas recréer une amplitude : clé reconnue vers la canonique ; alias historique explicite vers cette même clé si la compatibilité est nécessaire ; valeur inconnue signalée, sans création silencieuse. Ne pas étendre aveuglément cette restriction à d’éventuels référentiels hors Point Zéro.

### 2. Les 36 descriptions d’amplitude restent disponibles

Les 24 lignes non canoniques ne représentent pas toutes les amplitudes : douze autres anciennes lignes servent d’identifiants aux verbes. Les 36 descriptions pédagogiques restent dans les configurations de Puissance, indépendamment des 18 compétences sélectionnables. Conserver les noms et descriptions historiques des 42 lignes ; ne pas convertir la description de FERVEUR, par exemple, en définition de toute la direction J’EMBRASE.

### 3. Le retour arrière annoncé n’est complet qu’avant de nouvelles écritures

`skill_origine_id` restaure les lignes déplacées pendant la migration. Il ne dit pas où remettre une attribution ou un rattachement créé APRÈS la bascule vers un verbe : on ne peut pas inventer après coup une amplitude d’origine.

Distinguer explicitement deux fenêtres : (a) bascule sans nouvelle écriture, restauration exacte des références et des champs depuis un journal ; (b) après reprise d’activité, retour de code avec schéma additif conservé et stratégie explicite pour les nouvelles lignes. Ne pas annoncer un `down` complet après activité tant que ce cas n’est pas résolu et éprouvé. Ne jamais supprimer de points ou inventer une amplitude pour permettre un retour.

Le script doit être transactionnel pour les modifications liées, rejouable sans écraser `skill_origine_id`, et protégé contre les attributions concurrentes pendant la bascule. Le journal conserve aussi la configuration et les champs modifiés ; une restauration de la seule clé étrangère ne restaure pas tout le déploiement.

### 4. Déploiement cohérent et contrôles

Préparer d’abord une PR et une simulation sans écriture. Décrire l’ordre schéma additif / code compatible / données / bascule des lecteurs pour qu’aucune requête ne cherche des canoniques avant leur désignation. Éprouver sur préproduction avant une écriture de production ; la séquence du plan doit nommer les environnements, pas placer « préprod » après une écriture indéterminée.

Contraindre les références de remplacement et d’origine (clés étrangères adaptées), exclure les cycles et garantir une destination canonique du même cadre. Vérifier 18 cadres attendus, pas seulement un compte de 18 lignes. Capturer les témoins sur données fraîches : les nombres 52 et 5 de l’inventaire sont des observations datées, pas des invariants applicatifs permanents.

Recette : attributions statiques et dynamiques, cinq portes Sas, import, ancien identifiant public et privé refusés pour un nouveau rattachement, provenance historique, conservation des totaux par joueur/expérience/Puissance/polarité, absence de double gain au rejeu, simulation puis seconde exécution, retour arrière dans chacune des fenêtres annoncées.

## Couverture des verbes

Complément portable : JE DISTANCIE et JE DIRIGE sont aussi accessibles par le Sas. Avec JE CRÉE via Lire mon Moteur, trois des cinq verbes sans rattachement statique ont un chemin dynamique identifié. Cela ne réaffecte aucune expérience. Conserver la distinction entre couverture statique, chemins dynamiques et attributions effectivement enregistrées.

Référence : [plan portable relu](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-plan-de-migration.md).