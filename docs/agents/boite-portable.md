# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — courrier des 21 et 22 août traité, PR #47 à #61 comprises.)*

## L'état au 22 août, en fin de journée

Production et préprod à égalité (`6d4178e` / `ecb2719`), **CI verte**, Brakeman exit 0
(Errors 0, Security Warnings 0), RuboCop 427 fichiers zéro offense, témoins intacts :
**31 comptes · 927 Ω**, aucun compte jetable. Recette transversale : **95 bancs sur 95**.
Journaux de production : **zéro 500, zéro exception**.

Deux défauts trouvés et corrigés aujourd'hui, tous deux **en production** :

1. **`/echanges` ne servait qu'un régime.** La coque du Monde 0 avait remplacé la page pour
   tous, alors que le canon date son retrait (« à ce stade », « pas encore »). Treize comptes
   de production sur trente et un sont au Monde 1 : ils avaient perdu la rubrique « À ton
   attention », les trois sections nommées et les entrées d'action. `/echanges` aiguille
   désormais par monde ; le Monde 1 retrouve sa page d'avant, mot pour mot.
2. **`POST /threads/:id/messages` rendait 500** sur un `message` scalaire (`TypeError`, `dig`
   sur une String). Un paramètre mal formé se refuse maintenant au lieu de casser.

## La leçon du jour, et elle vise l'outillage

**Un outil de vérification qui ne peut pas dire ce qu'il a vu ne vérifie rien.** Quatre bancs
étaient rouges depuis vingt-quatre heures. Le script de recette les DÉTECTAIT bien, mais
imprimait leur détail avec `grep ÉCHECS :` sans guillemets — grep lisait « : » comme un **nom
de fichier** et rendait une ligne vide. Le rouge était visible, le diagnostic introuvable, et
il fallait rejouer chaque banc à la main pour savoir quoi que ce soit. C'est la leçon du
21 (« une assertion qui ne peut pas échouer ne vérifie rien ») appliquée à l'instrument
lui-même. La recette vit désormais dans le dépôt (`scripts/recette.sh`), imprime les
assertions fautives **avec leurs valeurs mesurées**, et accepte un sous-ensemble.

Deux corollaires payés le même jour :

- **`$?` après un tube mesure le dernier maillon.** J'ai cru lire le code de sortie de
  Brakeman ; je lisais celui de `head`. Mesuré correctement, il sort bien à 0 — mais je ne le
  savais pas quand je l'ai écrit.
- **Un banc qui écrit à la place de l'application ne teste pas l'application.**
  `verifier_canal_m0` entourait son POST d'un `rescue nil` puis créait le message directement
  en base. Il affirmait « il lit, il écrit » en écrivant lui-même, et masquait un 500.

## Ce qui reste, et de qui ça dépend

- **Codex** : §2.5 est-il bien daté (« à ce stade ») ? Et le régime transitoire du Monde 1
  — l'ancienne page plutôt qu'une coque — lui convient-il ? Déposé dans sa boîte.
- **Poste fixe** : porter `?stage=m1entry` et `?stage=m1circle` ; `_classique.html.haml`
  disparaîtra ce jour-là. Plus sa vérification du rendu du bloc Rencontre.
- **Boris** : de vrais tests dans `test/` — choix de méthode, sans urgence.
- **Portable** : rien en attente.
