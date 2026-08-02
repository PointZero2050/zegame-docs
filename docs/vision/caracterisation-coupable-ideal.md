# Caractérisation — « Le Coupable idéal » (mini-jeu, Monde 0)

> Rédigé par Claude (instance bac à sable), 2026-08-02, en lecture seule sur `vibe.ze.game`
> (zegame-app, branche `pointzero`, tête gelée `5b4a875`). Quatrième pièce de caractérisation,
> après [progression/Oméga](caracterisation-progression-omega.md),
> [auth/rôles/autorisations](caracterisation-auth-roles-autorisations.md) et
> [le triptyque Monde 0](caracterisation-triptyque-monde-0.md), qui l'annonçait comme « même
> patron, non détaillé ». Expérience à part entière du Monde 0 (Challenge 257) depuis la
> scission du 2026-07-26 — donc chemin critique du Festival.
>
> Chiffres de production au 2026-08-02 : 6 `CoupableIdealSession` en base.

## 1. Deux flux qui coexistent, jamais réévalués l'un par l'autre

`flow_version` (1 ou 2) fige à jamais quelle définition de contenu et quelles règles de calcul
s'appliquent à une session. **`start_for` crée systématiquement en `flow_version: 2`** — la V1
n'est plus jouable, mais ses anciennes lignes restent lisibles telles quelles :

```ruby
def content = v2? ? self.class.content_v2 : self.class.content   # deux YAML distincts
def steps   = v2? ? self.class.steps_v2 : STEPS                  # deux séquences distinctes
```

**Principe de portage général, au-delà de ce seul module** : une session déjà complétée ne doit
**jamais** être recalculée avec des règles plus récentes que celles en vigueur au moment de sa
complétion. Le résultat (`result`, jsonb) est un instantané figé, pas une vue dérivée — le
persister est le contrat, pas une optimisation.

## 2. V2 — le procès contradictoire (`CoupableIdeal::Proces`, `app/services/`)

Entièrement déterministe, aucun appel externe, aucune IA (rappelé explicitement dans le code à
deux endroits). Chaîne de calcul, dans l'ordre :

1. **Cause principale** = poids maximal au « banc des accusés » (jetons distribués par le
   joueur) ; en cas d'égalité, **c'est le joueur qui tranche** explicitement (pas un ordre
   arbitraire) ; repli stable sur la première si rien n'est choisi.
2. **Charges retenues** (choisies par le joueur parmi celles disponibles pour la cause
   principale, `charge_keys_valides` — **toute clé absente de la définition YAML est rejetée**,
   garde-fou anti-paramètre-forgé, limite à 3 choix) → chacune référence un **axe de polarité**
   et un **pôle**.
3. **Axes révélés** = un axe par charge retenue (première occurrence gagnante si deux charges
   touchent le même axe), chacun porteur d'un `pole_fort` (le mouvement accusé) et d'un
   `pole_exile` (son opposé, calculé par `pole_oppose`, jamais saisi).
4. **Verdict** = quatre volets indépendants (`responsabilite`, `cause_unique`, `fonction`,
   `contrepoids`), chacun un texte parmi deux variantes YAML choisi par une condition booléenne
   simple sur les réponses des écrans intermédiaires (réquisitoire, plaidoirie,
   contre-interrogatoire) — **jamais un score agrégé, quatre décisions indépendantes et
   explicables**.
5. **La roue** montre **toujours les 6 axes**, y compris ceux non instruits par ce procès — un
   axe non exploré est marqué `explore: false` (pointillés côté vue), **jamais absent de la
   structure de données**. Une **lecture textuelle intégrale équivalente** est générée en
   parallèle (`lecture_textuelle`) — la roue graphique n'est jamais le seul porteur de
   l'information (accessibilité).
6. **La Graine** (passage du collectif à l'individuel) : le joueur choisit **lui-même** la
   Puissance où il reconnaît le mouvement exilé — **principe produit explicite, cité dans le
   code** : « AUCUN mapping automatique entre un axe de polarité et une Puissance ». Ne jamais
   introduire une table de correspondance axe→Puissance au portage, même si elle semblerait
   simplifier l'écran : c'est un choix délibéré, pas un manque.

## 3. Mode éphémère — « Découvrir sans enregistrer mes réponses »

```ruby
after_action :purge_ephemeral_after_carte, only: :show
def purge_ephemeral_after_carte
  return unless @session&.ephemeral? && @session.completed?
  return unless %w(carte roue).include?(@session.current_step)
  @session.destroy
end
```

La session éphémère **traverse exactement le même flux et la même table** que le mode normal
(même `store_answer`, même calcul de restitution) — la différence n'est **que la destinée finale
de la ligne**. Suppression **immédiatement après le rendu de l'écran de restitution** (`carte`
en V1, `roue` en V2), via un `after_action` sur `:show` — donc après que la réponse HTTP a déjà
été construite avec les données. Aucune trace ne survit à ce rendu : ni Oméga, ni ligne
`CoupableIdealSession`, ni validation Marelle (`validate_marelle_experience! unless ephemeral?`
dans `#complete!` — le garde-fou est au niveau du modèle, pas seulement du contrôleur, donc
même un appel direct au modèle sans passer par cette action respecte la règle).
`start_for` **exclut explicitement les sessions éphémères complétées** de son repêchage
(`completed.where(user:, ephemeral: false)`) — cohérent, elles n'existent déjà plus.

## 4. Rétention choisie par le joueur (sessions non éphémères)

Sur l'écran final, un joueur en mode normal choisit explicitement ce qui est conservé :

| `retention_choice` | Effet |
|---|---|
| `"none"` | rien de plus que le `result` déjà calculé |
| `"seed_excerpt"` | un extrait de texte libre choisi par le joueur est conservé (`retained_excerpt`, tronqué à `LIBRE_MAX` = 240 caractères) |
| `"profile"` | (à vérifier côté vue — non détaillé dans ce document, cf. §6) |

Ignoré si `@session.ephemeral?` (la rétention n'a pas de sens pour une ligne qui va être
détruite). Même principe que le « choix trace par trace » déjà documenté pour la publication
volontaire de Puissances/Graines (catégorie C, P1b) — un joueur ne voit jamais une donnée
sensible devenir visible ou conservée par défaut.

## 5. Ce que ce document ne couvre pas

- Le détail écran-par-écran (`config/coupable_ideal.yml`, `coupable_ideal_v2.yml`) et les 13
  vues HAML associées — catégorie A, contenu déjà porté (`7da4277`).
- La table des dérives (`config/coupable_ideal.yml`, clé `derives`) — signalée en passation
  comme partiellement en brouillon éditorial, à relire avant mise en avant publique,
  indépendamment du portage.
- Le détail exact de l'effet `retention_choice: "profile"` — non vérifié dans ce passage, à
  confirmer côté vue (`_carte.html.haml`/`_v2_roue.html.haml`) avant de porter ce mécanisme.

## 6. Vérification de parité recommandée

1. Compléter une session normale (V2) → le Challenge 257 se valide, l'Oméga attendu apparaît,
   `result` contient les 6 axes de la roue (jamais moins), ceux non instruits marqués
   `explore: false`.
2. Compléter en mode éphémère → après le rendu de l'écran final, la ligne
   `CoupableIdealSession` n'existe plus en base, aucun Challenge validé, aucun Oméga attribué ;
   revenir sur la page crée une session **neuve** (pas de reprise).
3. Soumettre une clé de charge absente du YAML (paramètre forgé) → rejetée silencieusement
   (`charge_keys_valides`), jamais une exception visible au joueur.
4. Deux charges pointant vers le même axe → un seul axe révélé dans le résultat (première
   occurrence), pas de doublon ni d'écrasement muet.
5. Une session V1 historique (s'il en existe une donnée de test) doit continuer à afficher sa
   restitution originale sans jamais être recalculée avec les règles V2 (§1).
