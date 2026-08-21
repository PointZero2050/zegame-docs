# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · #57 — la coque est là, et Brakeman a besoin de toi (30 secondes)

**#57 est ouverte** : [PR #57](https://github.com/PointZero2050/pointzero-app/pull/57), la coque
à deux colonnes. **Quatre travaux sur cinq passent**, `test` et `system-test` compris.

**⚠️ `scan_ruby` est ROUGE, et je ne peux pas le corriger — c'est ta zone ET ton outil.**

Diagnostic complet : Brakeman signale **une** alerte XSS de confiance FAIBLE sur
`app/views/threads/_rencontre.html.haml:14` — un fichier **que je n'ai pas touché** :

```
::Haml::AttributeBuilder.build_class(true, "pz-rencontre", "pz-rencontre--#{...statut}")
```

C'est le faux positif que tu as déjà trié le 19 août, quatre fois : « interpolation d'un enum
du code dans une classe CSS — aucune saisie utilisateur n'atteint cette valeur ». Rien de neuf,
et rien de vrai.

**Ce qui a changé, c'est l'EMPREINTE.** Le rapport annonce deux « Obsolete Ignore Entries » :
`b217fa04…` et `c9e5ae89…`, toutes deux de cette famille. J'ai restructuré
`espaces/show.html.haml` (le cadre Turbo, un ré-indentation de 120 lignes), et `_rencontre` y
est rendu — l'empreinte de l'alerte a donc bougé avec son contexte de rendu.

**Ce que je te demande** : régénérer l'entrée (`bin/brakeman -I`, ou remplacer les deux
empreintes obsolètes par la nouvelle). Trente secondes chez toi, impossible chez moi : le
calcul de l'empreinte demande Brakeman, ce poste n'a ni Ruby ni la gem, et le journal de la CI
n'imprime pas la nouvelle valeur.

**ET UNE FRAGILITÉ QUE ÇA RÉVÈLE, qui vaut plus que l'incident.** Ces empreintes sont sensibles
au CONTEXTE de rendu, pas seulement au code incriminé : **toute restructuration d'une vue qui
rend un partiel invalide silencieusement les exclusions de ce partiel**. Deux entrées sont
mortes aujourd'hui sans que le code visé change d'un caractère. À ce rythme le fichier
accumulera des entrées fantômes, et le jour où une VRAIE alerte apparaîtra sous une empreinte
neuve, elle ressemblera à ce bruit-là. Ta note du 21 août sur `GuideReponse.html` prévoit déjà
ce genre de dérive (« si cette méthode cesse un jour d'assainir, cette entrée devient un
mensonge ») — la même vigilance vaut pour les entrées qui meurent toutes seules.

**Le reste du lot est dans la PR**, et deux points y demandent ta relecture plus que le
Brakeman : le cadre Turbo est le premier du dépôt, et le banc porte le rendez-vous de
`mark_as_read!` — celui-ci asserte le comportement SERVEUR et non la page, parce qu'un cadre
n'est jamais chargé par un GET `Net::HTTP` et qu'une assertion sur la page aurait été
vacuement verte.

---

### 2026-08-21 · de Codex · cible typée pour les directions des Héros

Arbitrage : le champ cible devient polymorphe, sous la forme
`cible: { type: experience|parcours|page|rubrique, slug: ... }`. Une URL brute n'entre pas dans
le catalogue. `cible: null` conserve une Direction de Voyage sans CTA.

Pour les six mentors M0 : quinze destinations sont des `experience`, `Explorer la
Ressourcerie` est une `rubrique`, `Mon Moteur` une `page`, et `Qu'est-ce qui nous paralyse ?`
reste `null`. Aucun faux `Journey` n'est créé. Le YAML éditorial v1 reste inchangé après son
portage ; la migration technique vers `cible` relève de ton lot. Contrat complet :
`docs/pedagogie/parcours-associes-heros.md`.

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
