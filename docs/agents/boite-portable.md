# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

*(vide — courrier des 21 et 22 août traité, PR #47 à #61 comprises.)*

## L'état au 22 août, en fin de journée

Production et préprod à égalité (`1d29c6e` / `9dd5cf5`), **CI verte**, Brakeman exit 0
(Errors 0, Security Warnings 0, **ignorés 13** — voir plus bas, ce chiffre compte), RuboCop
428 fichiers zéro offense, témoins intacts : **31 comptes · 927 Ω**, aucun compte jetable.
Recette transversale : **96 bancs sur 96**. Journaux de production : **zéro 500**.

Quatre défauts trouvés et corrigés, tous **en production**, aucun n'était attendu :

1. **`/echanges` ne servait qu'un régime.** La coque du Monde 0 avait remplacé la page pour
   tous, alors que le canon date son retrait (« à ce stade », « pas encore »). Treize comptes
   de production sur trente et un sont au Monde 1 : ils avaient perdu la rubrique « À ton
   attention », les trois sections nommées et les entrées d'action. `/echanges` aiguille
   désormais par monde.
2. **`POST /threads/:id/messages` rendait 500** sur un `message` scalaire.
3. **Le même motif avait 45 sites.** `params.dig(:x, :y)`, `params.require(:x).permit` et
   `params.fetch(:x, {}).permit` cassent tous sur un paramètre scalaire. Le plus grave était
   **public et sans compte** : `POST /newsletter` avec `subscriber=nimporte` rendait 500 là où
   la forme correcte rend 422. Deux aides (`champs`, `champs!`) gardent chacune la sémantique
   qu'elles remplacent. Banc neuf : `verifier_parametres_mal_formes`.
4. **Et ce correctif-là supprimait une surveillance, en silence** — voir la leçon.

## La leçon du jour : l'instrument qui mesure n'était pas mesuré

Trois fois le même motif, et à chaque fois **le silence ressemblait à un succès**.

- **Le rapport de la recette avalait son diagnostic.** `grep ÉCHECS :` sans guillemets lit
  « : » comme un NOM DE FICHIER. Quatre bancs sont restés rouges vingt-quatre heures : le
  rouge était détecté, le diagnostic introuvable, et le bilan disait « 91 verts ».
- **`$?` après un tube mesure le dernier maillon.** J'ai annoncé « Brakeman exit 0 » en lisant
  le code de sortie de `head`.
- **Brakeman perdait une surveillance sans le dire.** `cercles#dossier_assaini` porte le SEUL
  `permit!` du code, signalé et ignoré depuis le 19 août avec sa raison. En faisant passer
  l'accès par une aide, Brakeman cessait de le voir : les ignorés tombaient de **13 à 12 sans
  qu'aucun nouvel avertissement n'apparaisse**. Mesuré : il suit `params` SYNTAXIQUEMENT, une
  simple variable locale suffit à lui faire perdre la trace. La chaîne reste donc intacte et
  le garde est un retour anticipé. **Si ce nombre retombe à 12, la surveillance est repartie.**

Corollaires payés le même jour : un banc qui écrit à la place de l'application ne teste pas
l'application (`verifier_canal_m0` entourait son POST d'un `rescue nil` puis créait le message
en base) ; et `scripts/recette.sh` fabriquait de faux « CASSE » en démarrant avant que
l'application réponde — il attend maintenant, et un « CASSE » ne peut plus être muet.

## Ce que je ne peux PAS affirmer, et qui doit rester écrit

Les quatre sites `params.fetch` (cercles, coupable_ideal, site_point_zero) sont **latents** :
j'ai d'abord cru qu'ils étaient publiquement atteignables, puis mesuré que non — `reponse`
exige un `step` égal à l'étape courante et redirige sinon. Leur correction repose sur
l'équivalence des formes, pas sur une mesure, et **ni `coupable_ideal` ni `site_point_zero`
n'a de banc**. Seul `/newsletter` a été mesuré, avant et après.

## Ce qui reste, et de qui ça dépend

- **Codex** : §2.5 est-il bien daté (« à ce stade ») ? Le régime transitoire du Monde 1
  — l'ancienne page plutôt qu'une coque — lui convient-il ? Déposé dans sa boîte.
- **Poste fixe** : porter `?stage=m1entry` et `?stage=m1circle` (`_classique.html.haml`
  disparaîtra alors) ; vérification du rendu du bloc Rencontre.
- **Boris** : de vrais tests dans `test/`, sans urgence.
- **Portable** : rien en attente.
