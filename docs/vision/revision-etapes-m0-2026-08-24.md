# Révision du nombre d'étapes — neuf expériences du Monde 0

> **Demande de Boris, 24 août 2026**, dans la logique de l'arbitrage « Le Coupable idéal passe à
> une étape » (Codex `d827597`, §2.1). Ce document ne tranche rien : il **mesure** l'état réel,
> nomme ce que chaque demande exige, et dit chez qui elle tombe.
>
> Rédigé par le poste fixe. Toutes les mesures viennent de la préprod et du dépôt, aucune n'est
> déduite.

## 1. Ce que Boris demande

| # | Expérience | Demande |
|---|---|---|
| 1 | `une-drole-d-epoque` | passe à **une** étape, validée par contrôleur (sinon les Ω ne sont pas distribués) |
| 2 | `avant-le-zero` | passe à **une** étape |
| 3 | `l-ecosysteme-point-zero` | passe à **deux** étapes — « Conserver mon schéma ne correspond à rien » |
| 4 | `le-site-du-point-zero` | **restructuration complète** autour des cinq parcours du site public |
| 5 | `le-signe-de-reconnaissance` | passe à **une** étape |
| 6 | `les-choses-se-precisent` | reste à **trois** étapes, avec des CTA « Passer à l'étape N » et une popup de Graine |
| 7 | `le-conseil-omega` | passe à **une** étape |
| 8 | `le-sas-d-entree` | reste à **trois** étapes ; corriger « Rejoindre le Sas », qui mène au mauvais endroit |
| 9 | `vivre-l-atelier-point-zero` | passe à **une** étape : s'inscrire à un atelier, vérifié par contrôleur |

## 2. L'état mesuré aujourd'hui (préprod, compte de lecture)

| Expérience | étapes | destinations des CTA |
|---|---|---|
| `une-drole-d-epoque` | 3 | `/une-drole-depoque` ×3 — **une seule surface** |
| `avant-le-zero` | 3 | `/avant-le-zero` ×3 — **une seule surface** |
| `l-ecosysteme-point-zero` | 3 | bouton vidéo · `/le-schema-de-circulation` · `/le-schema-de-circulation` |
| `le-site-du-point-zero` | 3 | `/le-site-du-point-zero` ×3 — **une seule surface** |
| `le-signe-de-reconnaissance` | 3 | `/le-signe-de-reconnaissance` ×3 — **une seule surface** |
| `les-choses-se-precisent` | 3 | `/mes-traces` · `/mentor` · éditeur de Graine de l'expérience |
| `le-conseil-omega` | 3 | `/conseil-omega` ×3 — **une seule surface** |
| `le-sas-d-entree` | verrouillée pour ce compte | `PORTES` : `{1 => "/sas"}` |
| `vivre-l-atelier-point-zero` | verrouillée pour ce compte | aucune porte (Codex §6.3 : « à construire ») |

**La mesure conforte la demande.** Six expériences sur neuf n'ont qu'**une seule surface** derrière
leurs trois CTA : les trois « étapes » y sont trois moments d'un mini-jeu continu, exactement le cas
que le §2.1 de Codex range dans « ses mouvements restent nommés **dans** l'étape ».

Et le point 3 se vérifie littéralement : sur `l-ecosysteme-point-zero`, **« Conserver mon schéma »
pointe sur la même URL que « Relier les fragments »** (`/le-schema-de-circulation`). L'étape 3 ne
mène nulle part de neuf.

## 3. ⚠️ Trois constats qui changent la forme du travail

### 3.1. `/sas` est le PREMIER des cinq parcours de découverte, pas le Sas d'entrée

C'est la cause exacte du défaut signalé par Boris. Mesuré :

- la page d'accueil du site public annonce « **Cinq parcours de découverte** […] gratuit, **sans
  compte à créer**, et se termine par un badge » ;
- leurs cinq adresses sont `/sas`, `/sas/scenarios`, `/sas/croyances`, `/sas/paralysie`,
  `/sas/reveil` ;
- `/sas` rend « **Qu'arrive-t-il à l'humanité ?** — Cinq questions pour changer d'échelle ».

Or `SequenceDeGestes::PORTES` porte `"le-sas-d-entree" => { 1 => "/sas" }`. Le CTA « Rejoindre le
Sas » envoie donc le joueur dans un questionnaire public, au lieu des **dates du Sas d'entrée**.
Pure collision de nom.

**⚠️ Et l'arbitrage §6.3 de Codex repose sur la même collision** : il écrit « Le Sas d'entrée ·
Ouvrir les repères → **à construire sur `/sas/:slug`** ». Or `/sas/:slug` est précisément la route
des cinq parcours de découverte (`get "sas/:slug" => "sas#parcours"`). Cette destination est donc à
rouvrir, pas à construire là.

### 3.2. Les cinq parcours du site ne persistent RIEN — le point 4 demande une donnée qui n'existe pas

`app/controllers/sas_controller.rb` fait **30 lignes** et ne contient **aucune** occurrence de
`current_user`, `save`, `create`, `Trace`, `Badge` ni `session[]`. Ces parcours sont entièrement
sans état — ce qui est cohérent avec la promesse affichée du site : « sans compte à créer ».

Conséquence directe : « **X parcours réalisés sur 5** » et « faire au moins un parcours (suivi par
contrôleur) » **ne peuvent pas se lire aujourd'hui**. Il n'y a rien à lire. Cela demande une
mécanique neuve — et une décision, parce qu'elle touche la promesse « sans compte » du site public :

- soit on n'enregistre que pour un joueur **connecté**, et le parcours reste anonyme pour les autres ;
- soit le badge de fin devient la trace, et il faut alors le rattacher à un compte.

**C'est le seul des neuf points qui ne soit pas un portage.** Il demande un arbitrage (Boris et
Codex) puis un modèle (portable).

### 3.3. `InscriptionCreneau` existe déjà — le point 9 est un portage, pas une construction

`app/models/inscription_creneau.rb` porte exactement ce qu'il faut, avec sa sémantique écrite :

```ruby
scope :vivantes, -> { where(annulee_le: nil) }
scope :actives,  -> { vivantes.where(attente_le: nil) }   # une personne en attente n'est PAS inscrite
```

« S'inscrire à un atelier, vérifié par contrôleur » a donc une source de vérité disponible
immédiatement. Le commentaire du modèle prévient déjà du piège : ne pas confondre une place en
attente avec une inscription.

## 4. Une question de doctrine à trancher (Codex)

Le point 6 demande des CTA « **Passer à l'étape 2** » / « Passer à l'étape 3 » **à côté** du CTA
d'action de chaque étape. Deux règles du canon s'en approchent sans le couvrir :

- §2.1 : « **Chaque étape visible porte un CTA unique**, qui ouvre l'action correspondante » ;
- §1 et §5.3 : « Ouvrir un CTA **ne fait jamais progresser** » l'étape.

Un bouton « Passer à l'étape 2 » est-il un **second** CTA (interdit par §2.1), ou une simple
navigation d'affichage — ce que les cartes d'étapes, déjà cliquables, permettent aujourd'hui ? Et
s'il fait avancer la séquence sans preuve, il entre en tension avec §1.

Je ne trancherai pas cela dans une vue : c'est la même limite qu'en août sur le `current_step`.

## 5. Répartition

| # | Ce qu'il faut | Chez qui |
|---|---|---|
| 1, 2, 5, 7 | contenu éditorial de l'étape fusionnée, puis YAML + `RANGS_PROUVES` au rang 1 | **Codex**, puis **portable** |
| 3 | idem, à deux étapes | **Codex**, puis **portable** |
| 9 | idem + preuve sur `InscriptionCreneau.actives` | **Codex**, puis **portable** |
| 8 | corriger `PORTES["le-sas-d-entree"]` — et décider de la vraie adresse des dates | **portable**, avec **Codex** pour la destination |
| 4 | arbitrage « sans compte » + mécanique de suivi + nouvelle structure d'étapes | **Boris et Codex**, puis **portable** |
| 6 | doctrine des CTA de navigation (§4 ci-dessus), puis la popup de Graine | **Codex**, puis **portable** et **moi** |

## 6. Ce qui est déjà prêt côté vue

**Aucune de ces réductions ne demande de travail de vue.** `challenges/_passage.html.haml` lit
`gestes.size` partout, sans aucun 3 en dur : une séquence d'une, deux ou trois étapes se rend déjà.
Le titre s'accorde au singulier depuis la PR #75 (« 1 étape pour franchir ce passage »), et
`affiche = courant || gestes.last` tient le cas d'une séquence à une seule étape.

Le jour où le YAML change, la page suit sans qu'on y touche. La seule vue à écrire est la **popup
de Graine** du point 6, une fois sa doctrine tranchée.
