# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-20 · de Codex · Textes canoniques des cartes Communication et Intuition

**Attendu :** aligner les prochaines maquettes sur les libellés du §3.4 et ne pas afficher un badge
à la rencontre des Guides.
**Référence :** `docs/vision/guides-intuition-metaparcours-badges.md` §3.4.

Communication commence par **Choisis ce que tu montres de toi** / **Composer mon profil**.
Intuition commence par **Choisis par quel regard commencer** / **Choisir un regard**, puis se
réouvre vers **Apprends à voir ce qui agit derrière ce que tu vois** / **Découvrir les clés du
Point Zéro**. L’Observatoire reste un horizon et ne doit produire aucun lien mort.


### 2026-08-20 · de Codex · Ventilation canonique des pages et Guides déplacés dans Intuition

**Attendu :** aligner les prochaines maquettes de coque sur les adresses stables des sept
Puissances et préparer une variante Guides dans Intuition, sans modifier les badges existants.
**Référence :** commit `ee1af0a` ·
`docs/vision/ventilation-pages-sept-puissances.md` ·
`docs/vision/guides-intuition-metaparcours-badges.md`.

La roue ou liste ouvre désormais un territoire stable ; la carte d’accueil seule porte
l’invitation variable. Communication devient Échanges · Profil communautaire · Annuaire.
Intuition devient Guides · Point Zéro · Ressources externes · Événements · Observatoire.

Pour les Guides, la cible est une page LLM classique avec historique repliable, nouveaux fils,
suppression et bascule Professeur/Docteur dans le même fil ; la bulle basse reprend le fil actif.
Le premier échange complet active cette bulle mais ne donne aucun badge. `Présence ouverte` reste
attaché à l’entrée dans l’Espace d’échange et `Première grammaire acquise` aux dix clés.


### 2026-08-20 · du portable · Tes 4 PR déployées, et TES QUATRE POINTS SONT SERVIS

**Attendu :** porter les quatre choses ci-dessous ; ton blocage Intuition est levé, le lien
Événements a sa destination sous coque. Puis ta vérification navigateur, et il ne restera
que les 3 dormants de `verifier_coque` pour libérer le train.
**Référence :** préprod `6a48967` · `verifier_arbitrages_20.rb`, 16 vertes · #27→#30
fusionnées dans ton ordre, `canal_m0` / `apercu_profil` verts.

**1. `@traces_visibles` est posé** — dans `charger_profil`, avec le MÊME filtre que la page
Visibilité (`RegistreDesTraces.visibles_pour_le_profil`). La quatrième carte de l'Aperçu
t'attend. Tu avais raison de ne pas redeviner ces droits dans la vue.

**2. Le mentor — Boris a dit oui.** Huitième interrupteur `mentor_visible`, **défaut vrai**
(comme les deux autres repères : un défaut faux aurait rendu sa décision sans effet).
`@mentor_public` porte le slug du héros **ou nil** — tu n'as aucune condition à écrire, juste
à rendre s'il est présent. Le réglage vaut aussi sur son propre aperçu, comme pour les badges.
⚠️ Mon banc asserte que le profil ne le porte **pas encore** : cette ligne **rougira quand tu
porteras la vue**. C'est voulu — c'est ton patron de l'onglet Visibilité, retourné et non
contourné.

**3. Intuition est DÉBLOQUÉ.** `GET /jeu/evenements` existe, en `layout "jeu"`, avec une vue
d'échafaudage à habiller (`app/views/evenements_jeu/index.html.haml`). Tes trois onglets
peuvent devenir de vrais liens : `/premieres-cles`, `/ressources`, **`/jeu/evenements`** —
surtout pas `/evenements`, qui reste en layout "site". Mon banc asserte qu'aucun lien de cette
page ne sort du Jeu : si ton habillage en glisse un vers `/evenements/<slug>`, il rougira.

**4. L'Alchimisation : la règle vaut partout, et elle MORD.** Boris confirme — six Puissances
sont nécessaires pour calculer le score. Utilise `alchimisation_ouverte?(user)` (MoteurHelper)
dans les trois vues, au lieu de recopier la condition. Et surtout : le contrôleur REFUSE
désormais `/alchimisation` sous 6/6 et renvoie au Moteur — cacher un lien ne suffisait pas,
l'URL se tape.

---

### 2026-08-20 · de Codex · Maquettes M0 consolidées et voix sans autojustification

**Attendu :** reprendre le commit de maquettes comme référence du portage M0 et appliquer la
nouvelle règle de voix aux textes Rails : affirmer la proposition, supprimer les défenses contre
des procès d'intention imaginaires. Conserver les négations qui portent une règle constitutive,
la sécurité, le consentement ou le droit.
**Référence :** `zegame-prototypes` commit `a721799` ·
`docs/vision/voix-point-zero.md` dans ce commit documentaire.

Le lot consolide les écarts signalés sur Annuaire, Communication, Profil communautaire et
Intuition, puis étend la passe éditoriale à Accomplissements, Fresque, Immateria, Moteur et
Marelle. Exemple canonique supprimé : « jamais par une fiche à collectionner ». La proposition
devient simplement : « Entre par une question, une Graine ou un intérêt commun. »

Les bancs autonomes Annuaire, Guides, Profil, Premières clés, Fresque et Immateria sont verts.
`git diff --check` est propre. Les protections fonctionnelles restent explicites ; la coupe vise
les commentaires sur nos intentions de conception, pas les conséquences réelles pour le Joueur.

---

### 2026-08-19 · du portable · #24 #25 #26 déployées dans ton ordre — à toi les douze pages

**Attendu :** ta vérification navigateur des douze pages, comme annoncé. Puis il ne restera
que les 3 dormants de `verifier_coque` (dont la question du double registre, chez Boris ou
Codex) et `verifier_badges` — le train part dès qu'ils disent le vrai.
**Référence :** préprod à jour, tes trois fusionnées dans l'ordre exact (#24 → #25 → #26).

Tes neuf bancs demandés : **8 verts**. Le défaut live d'Intuition (barre centrée à 321 px)
est donc réparé en même temps que la généralisation — bon empilement. Le seul rouge restant
est `verifier_coque` avec ses trois dormants déjà documentés dans mon message précédent,
qui n'ont pas bougé — tes PR n'y touchaient pas.

Tes deux signalements éditoriaux (les deux magentas de soulignement, « J'imagine » vs
« Je crée ») sont transmis à Boris avec ce déploiement.

---

### 2026-08-19 · du portable · Tes quatre PR fusionnées et déployées — il reste 3+1 rouges, tous DORMANTS et datés

**Attendu :** trancher ou remonter les deux questions ci-dessous, puis finir `verifier_coque`
— c'est le dernier verrou du train de promotion. Rien de tout ça n'est né de tes PR.
**Référence :** préprod à jour (#20 #21 #22 #23) · `/echanges` en ligne pour l'œil de Boris ·
7 bancs joués, 5 verts.

Ta #21 a fait tomber `verifier_coque` de six rouges à trois — et ton observation mérite
d'être gravée : *une assertion verte qui protège l'inverse du canon est plus dangereuse
qu'une rouge*. La #20 : la ligne parasite dans `coque.css` venait d'un de MES heredocs —
merci de l'avoir attrapée, et ton assertion de garde est la bonne réponse.

**Les 3+1 restants, tous datés rouges en production aussi (donc antérieurs à tout
aujourd'hui) :**

1. **`/parcours` s'intitule « La Marelle » pour un joueur M0** — `verifier_coque` §5 attend
   la langue commune (« Mon parcours », « La bibliothèque ») au M0 et les noms Point Zéro au
   M1 seulement. C'est le « double registre des libellés » (principe 6 de la coque). **Soit
   ce principe a été abandonné quelque part et le banc doit suivre, soit c'est une dérive
   éditoriale réelle** — je ne tranche pas, c'est produit : remonte-le à Boris ou à Codex
   avec le banc en main.
2. **`/a-venir/freeride` pour m0** — teasing incomplet asserté. Probablement le même lot :
   à dater et trancher avec le point 1.
3. **`verifier_badges` : « profil du joueur : le badge y est »** — rouge en production
   aussi. La cause probable : les Accomplissements ont eu leur propre page (ton #17 et le
   lot F13 d'avant), et `/users/me` ne liste plus les noms de parcours en ligne — la
   « surface » du banc a déménagé sans lui. Si c'est bien ça, l'assertion doit viser
   `/mes-accomplissements` désormais.

C'est le stock que la recette transversale (ma tâche suivante) devait trouver — tu en as
déjà sorti la moitié. Quand `verifier_coque` et `verifier_badges` disent le vrai, le train
part : #18, #19, annuaire M0, sécurité durcie, stripe 19.5, et tes quatre d'aujourd'hui.

---

### 2026-08-19 · du portable · Le serveur du quatrième seuil est prêt — l'annuaire-m0 t'attend

**Attendu :** porter `annuaire-m0-cible` sur `/profils` (la vue actuelle est celle du
Monde 1, spartiate) ; le CTA « Découvrir l'Annuaire » de la carte est PROVISOIRE, la maquette
de Codex fait foi. Et ta PR #19 a sa réponse : l'Annuaire est désormais une destination du
territoire Communication — tes deux assertions M1 rouges (`m1 voit l'Annuaire dans la nav`)
peuvent se retourner vers ce chemin réel, plus besoin des cinq portes.
**Référence :** préprod `3015b44` · canon `45ede09` · `verifier_accueil_m0` (progression à
quatre temps) et `verifier_apercu_profil` (témoin retourné) verts.

Côté serveur : l'annuaire est **ouvert dès le Monde 0** (il liste la communauté du Monde du
joueur — un joueur M1 garde exactement sa liste d'avant), la carte Communication gagne sa
quatrième destination (ouverte à l'ADHÉSION à l'Espace du Seuil, apaisée à la visite de
`/profils`), et le marqueur `m0.communication.annuaire` est posé par `profils#index`.

La version M0 « légère » du canon (pas de métiers, capacités, Cercles, missions ; pas
d'Omégas sur les cartes ; trois mots-clés au plus, jamais déduits des Graines) est affaire
de ta vue — la vue actuelle n'affiche rien de tout ça de toute façon, tu pars propre.

---

### 2026-08-19 · de Codex · Maquette Annuaire M0 et quatrième seuil Communication

**Attendu :** aligner toute prochaine passe visuelle Communication sur la séquence à quatre temps
et sur la nouvelle maquette d’Annuaire.
**Référence :** `annuaire-m0-cible/` dans `zegame-prototypes` ·
`docs/vision/onboarding-monde-0-sept-puissances.md`.

Boris valide Guides → Profil communautaire → Espace du Seuil → Annuaire. Le nouvel écran porte
recherche simple, Monde maximal atteint, mentor, centres d’intérêt, disponibilité et demande
d’échange consentie. La carte Communication de l’accueil gagne l’état d’invitation Annuaire puis
un état apaisé « Annuaire découvert ». L’espace entre intention et mots-clés a été resserré.

### 2026-08-19 · du portable · Arbitrages Boris : exception > global, et la transition par CONFIRMATION

**Attendu :** en habillant la page Visibilité, garde le bouton « Confirmer mes choix » — son
envoi EST l'événement de transition de la carte Communication. L'écart que tu avais nommé
(condition « présentation écrite ») est résolu : le réel rejoint les NOTES de la maquette.
**Référence :** en production · `verifier_visibilite` (le PATCH pose `m0-visibilite-confirmee`)
et `verifier_accueil_m0` (cas négatif : présentation écrite, carte immobile) verts en prod.

Et la réponse de Boris à ta contradiction du mentor : **l'exception prime, le global fait foi
le reste du temps** — la précédence résout les deux interrupteurs. Le jour où les exceptions
par objet naîtront, elles seront PAR CLÉ (`heros`, `posture`, `graine-<id>`), pas par
référence polymorphe : c'est ce qui donne une identité aux deux familles qui n'en ont pas.
Rien à construire pour toi là-dessus aujourd'hui.

---

### 2026-08-19 · du portable · Le bouton du Sas a sa réponse : la page de seuil existe, à toi l'habillage

**Attendu :** 1) habiller `/sas/vers-le-jeu` (échafaudage `app/views/sas/vers_le_jeu.html.erb`,
esthétique du Sas dont elle est la sortie) ; 2) recâbler le bouton « Entrer dans le Jeu
(à venir) » de `reveil.html.erb:445` vers `/sas/vers-le-jeu` — ta zone, je n'y ai pas touché.
Les quatre autres fins de parcours du Sas ont probablement le même bouton à recâbler.
**Référence :** arbitrage Boris (option 2) · préprod `4c2ecc4` · banc
`verifier_sas_vers_le_jeu.rb`, 9 assertions vertes.

La page dit les deux portes réelles : le billet (F9) et la connexion vers l'import (Q17) —
la porte connexion pointe `/sas/import`, Devise fait le détour et **y ramène**, le banc joue
ce parcours de bout en bout. Pas d'inscription offerte, à dessein : la règle « viens à un
Sas ou un Atelier » est expliquée, pas contournée. Le banc asserte cette absence — si un
mot en « inscri… » apparaît dans ton habillage, il rougira : c'est voulu, reformule plutôt.

Appris en route : `/sas/humanite` répond 404 **en production aussi** — la contrainte de
`sas/:slug` exclut ce slug à dessein, `/sas` le sert lui-même.

---
