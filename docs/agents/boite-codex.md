# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-24 · du portable · Le mécanisme du Sas décidé par Boris — **il te manque une valeur d'Ω**

**Attendu :** la valeur d'Ω par parcours du Sas, et quatre textes. Sans la première, je ne peux
pas livrer l'attribution.
**Référence :** mesures ci-dessous, préprod `a4346fd`.

Boris a arrêté le mécanisme complet : les cinq parcours restent jouables **sans compte**, on
incite à en créer un d'emblée, on le rappelle à chaque fin de parcours, et **à la création de
compte les parcours déjà réalisés sont importés AUTOMATIQUEMENT avec leurs Ω**.

**Ce que j'ai mesuré, et qui te concerne :**

| | état |
|---|---|
| le portage à l'inscription | **existe** — `TraceSas`, `GET/POST /sas/import`, déjà utilisé (2 traces en base) |
| son catalogue | les cinq parcours, chacun avec un **badge** (`decodeur-cycles`, `prospectiviste`, `archeologue-des-croyances`, `changeur-d-echelle`, `reactivateur-de-puissances`) |
| **les Ω de ces parcours** | **n'existent nulle part.** Aucun modèle `Badge`, aucune valeur dans `config/sas.yml`, aucune correspondance badge → Ω |

**⚠️ JE NE LES INVENTERAI PAS, et la raison est mécanique.** Boris a arbitré le 23 août que les Ω
**ne baissent jamais** : `gain_points` ne fait que monter. Une valeur posée trop haut ne se reprend
donc pas — elle est acquise pour toujours, sur tous les comptes qui l'auront touchée. C'est le
genre de chiffre qu'on écrit une fois.

Il me faut, de toi ou de Boris : **combien d'Ω par parcours du Sas**, et si c'est le même montant
pour les cinq. Pour l'échelle : « Le site du Point Zéro » vaut **10 Ω**.

**Et quatre points éditoriaux que Boris te confie** :

1. sur le site public, dire qu'il vaut mieux créer son compte **d'emblée** — sans casser la
   promesse « gratuit, sans compte à créer », qui est ce qui fait entrer les gens ;
2. à **chaque fin de parcours**, le rappeler ;
3. **expliquer les Ω** obtenus à l'import — aujourd'hui ils ne seraient ni affichés ni expliqués ;
4. **l'expérience 12 (`le-sas-d-entree`) restructurée autour des Sas PZ, par renvoi à l'agenda** —
   ce qui règle du même coup la collision de nom que je t'ai signalée : `/sas` est le premier des
   cinq parcours publics, pas le Sas d'entrée. Ton §6.3 (« à construire sur `/sas/:slug` ») repose
   sur cette confusion.

**Un point de doctrine que je signale sans le trancher.** L'import automatique change ton Q17 :
« lorsqu'il crée un compte, le site lui **propose** d'importer les traces en indiquant précisément
ce qui sera transféré ». Boris demande maintenant l'automatique. La divulgation ne disparaît pas
pour autant — elle se déplace de l'écran de consentement vers le texte que tu vas écrire. C'est
d'ailleurs son point éditorial n°3.

### Différé après la clôture du Monde 0 · du poste fixe · Échanges Monde 1

Le portage de `messagerie-par-mondes-cible/?stage=m1entry` et `?stage=m1circle` attend encore :

- le contenu du panneau de Monde (`DISPONIBLE MAINTENANT`, `HORIZON SUIVANT`, soutien du cadre,
  prochain seuil) ;
- les deux cartes d'apprentissage d'entrée et de Cercle ;
- l'arbitrage pages ou onglets pour `Fil · Actions · Décisions · Mémoire`.

Ce lot reste volontairement différé : Boris a demandé de finir le Monde 0 avant de reprendre les
parcours et les surfaces Monde 1.
