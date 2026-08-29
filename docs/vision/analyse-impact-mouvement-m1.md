# Analyse d'impact — le Mouvement collectif du Monde 1

> **Demandée par** Codex, `messagerie-mouvement-collectif-m1.md` §11 : « Avant portage,
> l'analyse d'impact doit cartographier… ». Cette note est la moitié SERVEUR ; la moitié
> INTERFACE a été livrée par le poste fixe.
> **Auteur :** instance portable, 29 août 2026. **Tout ce qui suit est mesuré dans le code
> déployé**, pas déduit d'une lecture de documentation.

## Ce que cette note conclut, en une phrase

**Le portage est plus sûr et moins cher qu'il n'en a l'air côté modèle — aucun callback,
aucun Oméga, aucune notification à démêler — et beaucoup plus cher côté bancs : 21 bancs et
733 assertions vivent sur ces objets.** Le risque n'est pas dans la fusion des tables, il est
dans le vocabulaire que 231 de ces assertions figent.

---

## Axe 1 — Proposition, Décision, Action, Objection et leurs callbacks

| objet | états | liens notables |
|---|---|---|
| `Proposition` | 6 : brouillon, en exploration, soumise, adoptée, à retravailler, retirée | `message_source`, `versions` (historique), `has_many :decisions` (`nullify`) |
| `Decision` | 5 états **+ 2 résultats** (adoptée / à retravailler) | `proposition` (optionnel), `ouvreur`, `validee_par`, `consentements`, `objections` |
| `ActionDeFil` | 6 : proposée, acceptée, en cours, bloquée, accomplie, abandonnée | `message_source`, `auteur`, `porteur` |
| `ObjectionDeDecision` | 4 : ouverte, répondue, levée, maintenue | `belongs_to :decision` |
| `ConsentementDeDecision` | — | `belongs_to :decision` |

### ⚠️ Constat 1 — **aucun callback, sur aucun des sept modèles**
`after_*`, `before_*`, `around_*` : zéro occurrence sur `Proposition`, `Decision`,
`ActionDeFil`, `ObjectionDeDecision`, `ConsentementDeDecision`, `Sondage` et
`PropositionDeRencontre`. **Rien ne se déclenche implicitement quand un état change.**

C'est la meilleure nouvelle de cette analyse : la crainte ordinaire d'une fusion — « qu'est-ce
qui va se déclencher tout seul ? » — n'a pas d'objet ici. Tout ce qui arrive est écrit dans un
contrôleur, donc lisible et déplaçable.

### ⚠️ Constat 2 — **Objection et Consentement ne sont pas des pairs des trois autres**
Ils n'ont pas de fil à eux : ils appartiennent à une `Decision`. Le poste fixe l'avait vu, et
c'est exact. Les **objets de fil** sont donc **trois**, pas quatre — ce qui rapproche déjà le
réel du Mouvement unique que Codex décrit.

### ⚠️ Constat 3 — **26 états sur cinq machines qui ne partagent aucun mot**
6 + 5 (+2 résultats) + 6 + 4 = 23, plus les résultats et l'absence d'état des consentements.
Le canon en vise **quatre** (`À éclaircir`, `À consentir`, `En mouvement`, `Accompli`) plus
trois issues (`À poursuivre`, `Abandonné`, `À réviser`). La correspondance n'est pas une
bijection : elle demandera un arbitrage éditorial, pas une table de conversion mécanique.

⚠️ Et `Decision` porte **deux axes** (état ET résultat) : un joueur y lit six statuts issus du
seul objet Décision. Le Mouvement n'en montre qu'un.

---

## Axe 2 — Sondages, rencontres, messages sources et projections dans le Fil

- **Projection actuelle** : `espaces#show` compose `@propositions + @actions_de_fil +
  @decisions` et les rend par `threads/objets` ; `@objets_derives` rattache en plus un objet à
  SON message d'origine dans le fil.
- **Sondage et rencontre restent distincts** (canon §8) et le sont déjà : deux modèles à part,
  deux rendus à part. **Rien à défaire.** Le canon demande seulement de pouvoir « mettre en
  mouvement » depuis eux, en gardant un lien vers l'objet source — un champ, pas une refonte.

### ⚠️ Constat 4 — le message source est un **pointeur pendant**
`propositions.messaging_message_id` et `actions_de_fil.messaging_message_id` **n'ont AUCUNE
clé étrangère** : les seules FK de ces tables portent sur `messaging_thread_id` et sur les
utilisateurs. Détruire le message d'origine laisse donc un objet qui pointe vers rien, en
silence.

Ce n'est pas théorique depuis le 28 août : **les messages s'éditent et se suppriment**. La
suppression est douce (le texte est vidé, la ligne reste), donc rien ne casse aujourd'hui —
mais un objet dérivé d'un message supprimé affiche une origine VIDE, et personne n'est
prévenu. **À traiter dans le portage**, où le Mouvement remontera cette origine dans sa carte.

---

## Axe 3 — Droits par gabarit `échange`, `groupe`, `cercle`

Une seule règle porte presque tout : `Espace#actions_avancees? = gabarit != "canal"`.

| gabarit | objets collectifs | Décisions |
|---|---|---|
| `canal` (Monde 0) | **non** | non |
| `echange` | oui | non |
| `groupe` | oui | non |
| `cercle` | oui | **oui, seul gabarit** |

Les gardes vivent dans **trois contrôleurs** (`propositions`, `sondages`, `actions_de_fil`)
plus `decisions_controller`, qui exige `gabarit == "cercle"` à deux endroits.

### ⚠️ Constat 5 — la règle est bonne, sa RÉPÉTITION est le risque
Quatre contrôleurs redisent la même chose de quatre façons. Un Mouvement unique doit poser
cette garde **une fois** — sans quoi le cinquième circuit l'oubliera. C'est exactement le
défaut qu'on a corrigé cette semaine sur la palette des réactions : « un libellé que la page
offrirait et que le contrôleur refuserait serait un bouton mort ».

⚠️ Et le canon §9 ajoute une exigence que le code **ne porte pas encore** : « seules les
personnes réellement impactées et explicitement éligibles participent au consentement ».
Aujourd'hui, tout membre du Cercle peut consentir. L'éligibilité par personne est **un objet
nouveau**, pas un filtre à ajouter.

---

## Axe 4 — Notifications, historique, suppression, Mémoire

- **Notifications** : elles partent d'un seul endroit, `Messaging::Message` →
  `NotificationFilJob.planifier`. **Aucun des objets collectifs ne notifie.** Un Mouvement
  dont la carte vit dans le fil héritera donc des notifications du message qui la porte, et de
  rien d'autre. ⚠️ Le canon §5 exige pourtant « des notifications fiables » pour qu'une règle
  d'absence-vaut-consentement soit seulement envisageable : **c'est un manque à combler avant,
  pas après.**
- **Historique** : `VersionDeProposition` existe et fonctionne. Le canon §4.2 demande la même
  chose pour le Mouvement (« une modification substantielle crée une nouvelle version »). **Le
  patron est déjà écrit** — il se généralise, il ne s'invente pas.
- **Suppression** : voir le constat 4.
- ### ⚠️ Constat 6 — **la Mémoire n'existe pas**
  Le canon §4.4 écrit « la projection dans la Mémoire pointe vers le Mouvement historique et
  sa Trace ». Il n'y a **aucun modèle Mémoire** dans l'application. Le seul objet qui portait
  ce mot était le libellé de réaction « À garder dans la Mémoire » — **retiré ce 29 août** par
  l'arbitrage sur la palette Ombre/Lumière. Cette projection est donc **entièrement à créer**,
  et elle n'est chiffrée nulle part.

---

## Axe 5 — Validations et Omégas

### ⚠️ Constat 7 — **aucun Oméga, nulle part, sur aucun de ces objets**
Mesuré sur les sept modèles ET sur leurs six contrôleurs : zéro `Point.create`, zéro
`Validation.create`, zéro `omega`. L'exigence du canon §9 — « aucun clic, sondage,
consentement ou passage d'état ne distribue automatiquement d'Oméga » — **est déjà vraie, par
absence**.

C'est un acquis à PROTÉGER plutôt qu'à construire : le portage doit s'interdire d'ajouter ce
que personne n'a jamais mis. Un banc à témoins chiffrés autour du cycle complet le tiendrait.

---

## Le coût réel : les bancs

**21 bancs** mentionnent un objet collectif ; ils portent **733 assertions au total**, dont le
poste fixe a compté **231 qui nomment un objet collectif** (sa méthode est dans sa note ; la
mienne compte les fichiers concernés et leurs assertions totales — les deux mesures ne disent
pas la même chose et se complètent).

À notre règle — « un balisage asserté qui change → le banc change dans la même livraison » —
**ce n'est pas une finition, c'est une part du chantier**. C'est le poste conclusion de cette
analyse : *le risque n'est pas dans les tables, il est dans le vocabulaire.*

---

## Recommandation

1. **Ne pas fusionner les tables.** Le canon l'autorise explicitement (« l'implémentation peut
   conserver plusieurs enregistrements internes »). Aucun callback ne l'exige, et l'audit y
   gagne. Un `Mouvement` peut être une **façade de lecture** au-dessus des trois objets
   existants — le patron de `RegistreDesTraces`, déjà éprouvé ici.
2. **Poser la garde de gabarit une seule fois**, avant tout le reste.
3. **Combler trois manques AVANT le portage**, parce qu'ils ne sont ni des détails ni des
   finitions : les notifications fiables (§5), l'éligibilité par personne (§9), et la Mémoire
   (§4.4) — cette dernière n'existe pas du tout.
4. **Traiter le pointeur pendant** du message source dans la même livraison.
5. **Chiffrer les bancs dans le lot**, pas après.

## Ce que cette analyse ne dit pas

Elle ne tranche aucun arbitrage éditorial : la correspondance entre les 26 états actuels et
les quatre du Mouvement est un choix de produit, pas une conversion. Elle ne dit rien non plus
du rendu — c'est la moitié du poste fixe.

> **Arbitrage livré le 29 août 2026.** La correspondance produit est désormais définie dans
> [`messagerie-mouvement-m1-correspondance-etats.md`](messagerie-mouvement-m1-correspondance-etats.md).
> Elle conserve les états techniques pour l'audit, traite les tensions comme des enfants de la
> Décision et maintient sondages et rencontres hors du cycle du Mouvement.
