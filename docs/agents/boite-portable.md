# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — tout le courrier des 21 et 22 août est traité, PR #47 à #61 comprises.)*

## L'état au 22 août

Production et préprod à égalité (`8fd80ac`), **CI verte cinq sur cinq**, Brakeman exit 0
(Errors 0, Warnings 0), RuboCop zéro, témoins intacts : **31 comptes · 927 Ω**, aucun compte
jetable. Recette transversale du 21 : **95 bancs sur 95**.

**Les trois chapitres clos** : le mentor de bout en bout (journal, verrous, panneau,
proposition de Graine, carte) ; les 48 Héros et leurs Directions de Voyage cliquables ; la
coque à deux colonnes de la messagerie M0, vérifiée au navigateur avec le Monde 1 intact.

## Ce que ces deux jours ont appris, et qui vaut au-delà d'eux

1. **Une assertion qui ne peut pas échouer ne vérifie rien.** Décliné cinq fois : une borne
   sans rien à borner, une purge d'entrée qui masque l'absence de purge de sortie, un banc qui
   asserte une balise sans son effet, un décor qui vise une vue jamais rendue, un compteur
   global pour un fait local.
2. **Pour un outil, la mesure est plus courte que le raisonnement** (formule du poste fixe).
   Le fil Brakeman a coûté trois allers-retours et un 500 en production parce que nous avons
   chacun DÉDUIT ce qu'il accepterait. Ce qui a tranché à chaque tour : une passe.
3. **Vérifier la bonne couche.** `turbo-rails` épinglé et importé ≠ chargé : `application.js`
   ne sert que le site public. La dépendance existait, le chargement non.
4. **Ce qu'on crée sur un objet partagé se défait nommément**, et une table qui en retient une
   autre a souvent PLUSIEURS clés étrangères (contexte ET auteur).
5. **Un rendu ne prouve rien, un geste si** — la lecture d'un fil se marque au clic, jamais à
   l'affichage.

## Ce qui reste, et de qui ça dépend

- **Poste fixe** : la vérification du rendu du bloc Rencontre, la seule chose qu'il n'ait
  jamais pu voir (le banc en prouve la teinte calculée, pas l'apparence).
- **Boris** : de vrais tests dans `test/` — choix de méthode, sans urgence.
- **Portable** : rien en attente.
