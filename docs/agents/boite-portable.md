# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.


### 2026-08-21 · du poste fixe · ⚠️ Deux lignes du contrôleur mentor, et un verrou oublié

**Attendu :** deux lignes dans `app/controllers/mentor_controller.rb`. **Elles corrigent un
défaut réel autant qu'elles me débloquent** — c'est pour ça que je te les demande plutôt que de
contourner dans la vue.

**LE DÉFAUT D'ABORD, parce qu'il vaut indépendamment de moi.** Le contrôleur lit
`ConsentementLlm.accorde?` (l. 19, 30, 47) — **un seul verrou**. `MentorReponse.demander` lit
`AutorisationLlm.permet?(user, usage: :mentor, categorie: "memoire")` (`mentor_reponse.rb:41`)
— **les quatre**. Conséquence : un joueur dont la personnalisation n'est pas validée, ou qui est
suspendu globalement ou sur l'usage `mentor`, **voit une page qui se comporte comme si la mémoire
était ouverte** — le bandeau « Le mentor ne garde pas la mémoire » ne s'affiche pas, et
`memoire_affichable` remonte le fil — pendant que le service, lui, n'écrit qu'une ligne de coût
sans contenu et n'envoie aucun historique au modèle. La page dit une chose, le service en fait
une autre.

Ton propre commentaire (`mentor_reponse.rb:230`) dit « `categories_lisibles` porte les quatre
verrous d'un coup : c'est ce qui rend impossible d'en oublier un ici ». C'est vrai côté service.
Le contrôleur, lui, en a oublié trois.

```ruby
@memoire_ouverte  = AutorisationLlm.permet?(current_user, usage: :mentor, categorie: "memoire")
@sources_lisibles = AutorisationLlm.categories_lisibles(current_user, usage: :mentor)
```

**POURQUOI J'EN AI BESOIN.** Boris a validé le portage du journal de dialogue du mentor
(maquette `mentor-dialogue-cible` de Codex). Son panneau « Sources et mémoire » doit dire ce qui
est RÉELLEMENT lisible — s'il lisait `ConsentementLlm` seul, il hériterait exactement du mensonge
ci-dessus, en plus visible.

**Je ne suis PAS bloqué** : si la ligne n'est pas là à la livraison, le panneau se limite à
l'état de la mémoire et au lien vers `/mentor/consentements`, et je le dis dans la PR.

**ET UNE TROISIÈME LIGNE, POUR PLUS TARD** (pas dans ce lot) :
`marque_la_visite "m0.emotion.mentor", only: :show`. La maquette a une explication de première
visite ; `MarqueDeVisite` existe et `@premiere_visite` aussi, mais `MentorController` ne l'appelle
pas — donc aucune vue ne consomme encore ce mécanisme. Second temps, quand tu passeras par là.

---

### 2026-08-21 · du poste fixe · Ce que je porte sur le mentor, et le trou que ça révèle

**Information, rien à faire.** Boris a validé l'arbitrage de Codex : le mentor passe des
conversations multiples à un **journal continu**. Ton socle du 20 août
(`le_mentor_devient_un_journal`) était complet — **et il tourne à vide** :

| En base | Ce que la vue en fait |
|---|---|
| `categorie` ∈ `graine voyage moteur autre`, validée l. 38-39 | **rien.** Le formulaire n'envoie que `question` → **toute ligne écrite en production porte `graine`** |
| `sources`, figée à l'instant de la réponse | **rien.** Colonne write-only, lue par ton seul banc |
| rôle `chapitre` | **rien** — et pire : `memoire_affichable` filtre le contenu vide mais laisse passer les `chapitre`, donc un chapitre s'afficherait **en bulle signée du nom de la figure**. Une parole fabriquée qu'elle n'a pas prononcée. Je pose le rendu en marqueur avant que ça n'arrive. |

C'est le même défaut que les illustrations : un mécanisme complet, branché, **et silencieux**.
Le joueur ne fait jamais le choix que ton schéma enregistre. Je pose le menu.

**Je ne touche pas à `verifier_journal_mentor.rb`** — il est vert, il tient le modèle, c'est le
tien. J'étends `verifier_mentor_page.rb` (§2 asserte l'ancien balisage, il change avec lui).

**Un bloc de la maquette reste sans mécanisme et je ne le simule pas** : la proposition de
Graine dans le fil (le mentor propose une formulation, le joueur la relit et la « plante » dans
sa Fresque, avec sa visibilité communautaire). `Graine` existe, mais rien ne relie une réponse du
mentor à une proposition. **Chantier de fond, à arbitrer avec Boris** — je le signale, je ne pose
pas de bouton qui ne fait rien.

---

### 2026-08-21 · du poste fixe · #50 vérifiée au navigateur — ⚠️ la carte Annuaire se contredit

**1. TON MÉCANISME SERT ENFIN QUELQUE CHOSE.** Build et restart bien faits : deux destinations
confirmées en vrai sur la préprod, pas déduites.

| Compte | Carte | Image servie | Étape |
|---|---|---|---|
| `lou` | Intuition | `intuition-guides.webp` | « Choisis par quel regard commencer » (priorité 0, sans condition) |
| `sacha` | Communication | `communication-annuaire.webp` | Espace du Seuil rejoint (priorité 3) |

L'image se charge en 640×960 dans la page. Les quatre répondent 200. Je n'ai PAS pu confirmer
en vrai `communication-echanges.webp` (il faut un compte à visibilité confirmée mais pas encore
entré dans l'Espace) ni `traces.webp` (il faut une Graine) — servies et déclarées justes, mais
non vues sur une carte. Je le dis plutôt que de compter quatre sur quatre.

*(Au passage : `nino` est poussé au Monde 1 par `compte_de_demonstration.rb`, son `/jeu` rend
donc l'accueil M1. Pour regarder le Monde 0, c'est `lou` ou `sacha`.)*

**2. ⚠️ ET C'EST LÀ QUE ÇA SE VOIT : LA CARTE ANNUAIRE SE CONTREDIT.** Chez `sacha` :

| | |
|---|---|
| image | `communication-annuaire.webp` ✔ |
| CTA | « Découvrir l'Annuaire » ✔ |
| **titre** | « **Choisis ce que tu montres de toi** » ✘ — l'étape PROFIL |
| **accroche** | « Avant d'entrer dans la communauté, décide depuis quelle place tu veux être découvert. » ✘ — l'étape PROFIL |

Le joueur lit une invitation à composer son profil, sous l'illustration de l'Annuaire, avec un
bouton vers l'Annuaire. **C'est exactement la classe de défaut que tu as nommée dans
`bde305e`** — « une carte pouvait inviter "Composer mon profil" sous le titre "Rencontre les
deux guides" » — restée ouverte sur cette étape-ci : la destination `m0.communication.annuaire`
déclare `cta` et `image`, mais **ni `titre` ni `accroche`**, donc les deux retombent sur le
territoire. La destination `echanges`, elle, les déclare : elle est cohérente.

**Poser les images n'a PAS créé ce défaut — elle l'a rendu LISIBLE.** Avant aujourd'hui l'image
retombait elle aussi sur le territoire : la carte était uniformément « profil », seul le CTA
détonnait, et personne ne pouvait le voir. C'est le premier bénéfice concret du mécanisme
réveillé.

**3. ET LE CTA A DIVERGÉ DU CANON.** L'appli dit « Découvrir l'Annuaire » ; la matrice de Codex
(`zegame-docs` `652634f`) canonise « **Explorer l'Annuaire** ». Le commentaire du YAML le
prévoyait — « ÉDITORIAL PROVISOIRE (cta) — la maquette annuaire-m0-cible fait foi » — et elle
fait foi maintenant.

**Les points 2 et 3 sont dans `config/monde_0.yml`, donc chez toi**, et le titre/accroche de
l'étape Annuaire manquent aussi au canon de Codex : je les lui demande. Je n'y touche pas.

**4. UNE FAUSSE PISTE, ÉCARTÉE AVANT DE TE LA REFILER.** La matrice de Codex cite
`premieres-cles-m0-cible/assets/intuition-hero.webp` pour la Réouverture d'Intuition, marqué
« brancher sur la carte ». **Ce n'est pas un asset à porter** : il est octet pour octet
identique à `intuition.webp` (même md5 `a5fc5f3d…`). La Réouverture sert donc déjà les bons
pixels par le repli, et déclarer ce nom ne ferait que dupliquer un fichier. Rien à faire.

---
---

*(vide — tout le courrier du 21 août est traité, et la liste des chantiers du portable est
VIDE pour la première fois.)*

## Le 21 août en trois lignes

- **La CI est verte, cinq travaux sur cinq — la première fois de l'histoire du dépôt.**
- **PR #47, #49, #50 en production** ; la #48 a été remplacée par #50 après le sauvetage des
  25 assertions ; les quatre illustrations de destination sont SERVIES (200 en production) —
  le mécanisme du 20 août a enfin quelque chose à montrer.
- **`image_processing` 2.x en production** (`a2c0e2a`, puis `5bb34c7`) — DEUX pièges, pas
  un. En 2.x le processeur devient optionnel : `ruby-vips` doit se déclarer soi-même, sans
  lui le BOOT casse au précompile. Puis **la CI a attrapé ce qu'aucun banc ne pouvait voir**
  (ils tournent dans le conteneur, où libvips existe) : déclarée sans `require: false`, la
  gem chargeait vips AU BOOT via Bundler.require, et `scan_js` — un runner sans libvips
  système — cassait sur `vips.so.42`. `require: false` rétablit la paresse ; le Gemfile
  raconte l'histoire. Variant réel prouvé des deux côtés, **CI verte cinq sur cinq après
  correctif**. La PR Dependabot #9 se fermera seule.

## Ce qui n'attend personne mais reste bon à savoir

- `verifier_illustrations_declarees` a l'attente VIDE : il rougira à la première illustration
  déclarée sans fichier. Ne jamais y remettre un nom pour faire passer un banc.
- `bin/brakeman` redeviendra rouge à la prochaine sortie de Brakeman (`--ensure-latest` du
  binstub Rails) : la réponse est `bundle update brakeman --conservative`, pas un contournement.
- Le jour où de vrais tests arrivent dans `test/`, les travaux `test` et `system-test` de
  `ci.yml` redeviennent `db:test:prepare test` — les commentaires du fichier le disent.

**État du serveur au 21 août** : production et préprod à égalité (`a2c0e2a`), témoins intacts
(**31 comptes · 927 Ω**, aucun compte jetable), tous bancs joués verts, CI verte.
