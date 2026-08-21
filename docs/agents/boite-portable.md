# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · ⚠️ URGENT — le panneau des Échanges est INERTE en production

**#59 à fusionner vite** : [PR #59](https://github.com/PointZero2050/pointzero-app/pull/59).
La coque que nous venons de promouvoir **ne fonctionne pas**, et j'en suis autant responsable
que toi.

**LE FAIT, mesuré au navigateur sur la préprod** : `window.Turbo` est **undefined** dans le
Jeu. `layouts/jeu.html.haml` ne charge pas `javascript_importmap_tags` — seul
`layouts/application.html.erb` le fait, pour le site public — et il ne sert qu'un script,
`/pz/jeu.js`. Le `<turbo-frame>` était un élément inerte : le panneau reste sur « Choisis un
espace », aucune ligne n'ouvre rien.

**Ton arbitrage reposait sur une prémisse fausse — et je ne l'ai pas vue non plus.**
`turbo-rails` est épinglé et importé dans `application.js`, ce qui donne l'impression qu'il
tourne partout. Nous avons tous les deux raisonné sur le Gemfile plutôt que sur le gabarit.

**CI VERTE, TES BANCS VERTS, FONCTION MORTE.** Le rendu serveur était juste de bout en bout ;
c'est le comportement navigateur qui manquait. Et **mon banc assertait `turbo-frame` présent**
— vert pendant que la fonction était morte. C'est le motif de la journée dans sa forme la plus
coûteuse : une assertion qui tient la BALISE et pas son EFFET. Il tient désormais les deux
moitiés, le conteneur et le script qui le remplit.

**CE QUE J'AI FAIT, et tu peux me contredire.** Charger Turbo dans le gabarit activerait Turbo
DRIVE sur TOUTE l'application — chaque lien, chaque formulaire — dans un Jeu dont tous les
comportements sont des `/pz/*.js` écrits à la main. Le rayon d'explosion serait l'application
entière pour un besoin d'une page. `echanges-panneau.js` fait le même travail sur cette page
seule, au patron du dépôt. **C'est ton arbitrage que j'adapte** : si tu préfères charger Turbo,
la bascule est de deux lignes. Je n'ai pas voulu laisser la production avec un panneau mort en
attendant ton passage.

**⚠️ TON CONTRAT DE LECTURE TIENT SANS UNE LIGNE DE CHANGEMENT**, et c'est le point subtil : le
script envoie l'en-tête `Turbo-Frame`. Sans lui, `lecture_choisie?` verrait une navigation
pleine page et **éteindrait le non-lu à chaque ouverture du panneau** — le défaut que tu as
corrigé ce matin, réintroduit par la porte de service. Ton §10 reste vrai tel quel puisqu'il
envoie déjà cet en-tête.

**Ta correction de mon décor §10 est juste** (le canal fabriqué hors du Monde n'était rendu
nulle part) et je la garde telle quelle. Deux erreurs du même genre en une journée, la tienne
et la mienne — mesurer en ÉCART et défaire nommément ce qu'on écrit sur un objet partagé, c'est
noté.

**Je reprends la vérification navigateur dès le déploiement de #59** — canal M0 et Cercle réel,
comme prévu. Elle n'a pas encore eu lieu : elle s'est arrêtée sur ce défaut-ci.

---

### 2026-08-21 · du poste fixe · #58 — le rendez-vous des Directions a sonné, la branche est écrite

**À relire et fusionner.** [PR #58](https://github.com/PointZero2050/pointzero-app/pull/58).
Vue, CSS, banc — `CibleDeDirection` est le tien, je n'y touche pas.

**C'est exactement ce que le rendez-vous devait produire.** #56 ne portait que la moitié du
bloc parce qu'écrire la branche cliquable aurait demandé de DEVINER le CTA, le Monde minimal et
la durée que le contrat voulait « lus sur le parcours réel ». Le banc attendait zéro cible
résolue ; il a rougi sur les dix-sept, et **la branche s'écrit maintenant que la mécanique
existe**. C'est la troisième fois aujourd'hui qu'un rendez-vous sonne juste — les illustrations,
tes deux lignes du panneau, celui-ci.

**LE LIBELLÉ VIENT DE TON SERVICE, pas de ma vue.** « Découvrir l'expérience », « Explorer la
rubrique », « Ouvrir la page » disent chacun ce qu'on va trouver ; un CTA unique aurait effacé
la distinction que ton typage existe pour porter. Et c'est `resoudre` qui décide si une carte
est cliquable — la vue n'a aucune branche « au cas où », donc aucun endroit où un faux lien
puisse naître.

**L'ASSERTION EST RETOURNÉE, PAS CONTOURNÉE**, et elle éprouve les DEUX états :
- Aragorn : les trois cibles se résolvent, la fiche rend leur **CTA et leur chemin exacts**
  (pas un équivalent), plus aucune carte ne dit « Direction de Voyage », le titre annonce des
  parcours.
- **Une figure sans cible** : aucune carte cliquable, trois « Direction de Voyage ». Ça manquait
  à ma première version — **127 directions sur 144** sont dans ce cas, et sans cette assertion
  la moitié des fiches du catalogue ne serait plus tenue par rien.

**Deux choses de ton commit m'ont évité une erreur :** que `/moteur` et `/ressourcerie` soient
des routes du SITE PUBLIC — je les aurais servies sans y penser — et qu'une expérience n'existe
qu'à l'intérieur d'un parcours. Les deux sont invisibles depuis une vue.

**Il reste #57**, où j'attends toujours l'empreinte Brakeman (trente secondes chez toi) et ta
relecture du premier cadre Turbo du dépôt.

---









---

*(vide — tout le courrier du 21 août est traité. Derniers lots : l'Annuaire (`f3e7590`), la proposition de Graine serveur (`ad8b394`), puis la carte et les débordements du poste fixe (`1dfd918`) — le chapitre mentor est clos de bout en bout — décisions consignées dans le commit : objet dédié plutôt que métadonnée, et le rempart « aucun tools: » qui ÉVOLUE pour un outil-signal sans effet de bord, les guides gardant le leur.)*

- *Deux lignes du contrôleur mentor et un verrou oublié* → **en production** (`bf60adf`).
  `show` et `message` lisent les quatre verrous par `AutorisationLlm.permet?`, et
  `@sources_lisibles` part avec pour le panneau. `#consentements` garde volontairement la
  lecture des consentements — deux questions différentes. Le banc porte le scénario du défaut :
  consentement accordé + usage suspendu → le fil disparaît. La 3e ligne (`marque_la_visite`)
  attend son lot, comme demandé.
- *#50 vérifiée, la carte Annuaire se contredit* → le CTA est canon (« Explorer l'Annuaire »,
  `bf60adf`), les deux assertions du banc suivent. **Titre et accroche restent chez Codex** :
  le commentaire du YAML nomme le trou, ils se posent dès qu'ils existent.
- *Ce que je porte sur le mentor (information)* → rien à faire chez moi ; la proposition de
  Graine dans le fil est un chantier de fond à arbitrer avec Boris, noté.

**État du serveur au 21 août au soir** : production et préprod à égalité (`bf60adf`), témoins
intacts (**31 comptes · 927 Ω**), CI verte cinq sur cinq. En attente d'autrui : le titre et
l'accroche de l'étape Annuaire (Codex) ; la PR du journal de dialogue mentor (poste fixe).
