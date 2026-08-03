# Caractérisation — `PuissanceAssessment` et les caps du Moteur (Monde 1)

> Rédigé par Claude (instance bac à sable), 2026-08-03, en lecture seule sur `vibe.ze.game`
> (zegame-app, branche `pointzero`, tête gelée `5b4a875`). Septième pièce de caractérisation ;
> ferme la liste des « évaluations » nommées dans l'inventaire de portage (Moteur, **Puissances**,
> Conseil, Traversée, Coupable idéal) — la seule qui restait sans document dédié. Pédagogiquement
> Monde 1, donc **hors chemin critique immédiat** selon le cadrage (à la différence des cinq
> modules déjà caractérisés, tous Monde 0) ; utile surtout si le portage l'atteint avant la
> bascule, ou pour confirmer les choix déjà faits en le portant directement depuis le code
> (le commit `eb96d00` mentionne l'avoir déjà chargé et vérifié en partie).
>
> Chiffres de production au 2026-08-02 : 25 `PuissanceAssessment`, 0 publiée (avant l'existence
> même de la fonctionnalité de publication, ajoutée le 2026-08-01 — cohérent).

## 1. Chaque passation est un instantané historisé — même principe que le triptyque

```ruby
def self.latest_for(user, slug)
  where(user: user, puissance: slug).where.not(completed_at: nil).order(:completed_at).last
end
```

Refaire le questionnaire d'une Puissance crée une **nouvelle ligne** ; seule la plus récente
compte pour l'affichage courant (`latest_for`), mais l'historique reste intact et interrogeable
— aucune ligne n'est jamais réécrite. Identique en esprit à `MoteurAssessment`/`Traversee`
([caracterisation-triptyque-monde-0.md](caracterisation-triptyque-monde-0.md)).

## 2. Diagnostic déterministe : position O-L, état, garde-fou éditorial

```ruby
def self.from_answers(user, slug, answers)
  spheres = %w(corps autres monde).filter_map { |s| answers[s] }
  o = (spheres.select { |v| v.to_s.start_with?("o") }.map { |v| v[1].to_i }.max || 1).clamp(1, 3)
  l = (spheres.select { |v| v.to_s.start_with?("l") }.map { |v| v[1].to_i }.max || 1).clamp(1, 3)
  etat = ETATS.include?(answers["circulation"]) ? answers["circulation"] : "bloque"
  new(user:, puissance: slug, o_level: o, l_level: l, etat:, answers: a,
      illustration: answers["illustration"].presence, completed_at: Time.current)
end
```

- **Position O-L** (Ombre 1-3, Lumière 1-3) = le niveau **le plus engagé** rapporté par le joueur
  à travers trois sphères (corps, autres, monde) — un maximum, pas une moyenne : une seule sphère
  qui rapporte une Ombre 3 suffit à fixer `o_level = 3`, même si les deux autres sont plus
  timides.
- **État de circulation** (`bloque` / `intermediaire` / `libre`) déclaré directement par le
  joueur, avec repli sur `bloque` si la valeur est absente ou hors énumération — **jamais un état
  plus favorable par défaut**.
- **Garde-fou éditorial explicite, porté par le code, pas seulement la vue** : le champ
  `illustration` (une situation réelle décrite par le joueur) est saisi à la question
  correspondante, mais **rien dans le modèle n'empêche un état « libre » sans illustration** —
  c'est la vue qui rend ce champ obligatoire à la saisie pour cet état (à vérifier côté vue avant
  de porter, ce document ne l'a pas confirmé au niveau du contrôleur/formulaire).

## 3. Le cap d'évolution — une règle à un seul pas, jamais un saut

```ruby
def cap
  case etat
  when "bloque"        then {o: o_level, l: l_level, etat: "intermediaire", type: "circulation"}
  when "intermediaire"  then {o: o_level, l: l_level, etat: "libre",         type: "circulation"}
  when "libre"
    if o_level < 3 && o_level <= l_level
      {o: o_level + 1, l: l_level, etat: "libre", type: "amplitude"}
    elsif l_level < 3
      {o: o_level, l: l_level + 1, etat: "libre", type: "amplitude"}
    end # O3-L3 libre : pas de cap, sommet atteint ("Le Vivant total")
  end
end
```

Deux natures de progression, jamais mélangées : d'abord **ouvrir la circulation** (même
position O-L, juste changer d'état bloqué→intermédiaire→libre), puis, une fois libre, **élargir
l'amplitude** du pôle le plus faible (+1, jamais les deux pôles à la fois, jamais un saut de plus
d'un cran). Le sommet (O3-L3, libre) n'a explicitement **aucun cap** — la method renvoie `nil`,
la vue bascule alors sur un texte de clôture (« le cap devient un autre verbe : transmettre »).
**Ne jamais reconstruire cette règle comme un score continu** : c'est une machine à états à un
pas, avec un point d'arrêt délibéré.

## 4. Les caps « Moteur » — une surcouche éditable, pas recalculée

```ruby
# User
def effective_moteur_caps
  base = (conseil_sessions.completed.order(:completed_at).last&.caps || {}).compact
  base.merge(moteur_caps || {})
rescue StandardError
  (moteur_caps || {})
end
```

**Deux sources, avec priorité claire** : les caps posés une fois pour toutes par la dernière
`ConseilSession` complétée (`caps`, un hash par puissance parmi `accueillir`/`circuler`/
`assumer` — cf.
[caracterisation-triptyque-monde-0.md](caracterisation-triptyque-monde-0.md) §4) servent de
**base**, mais tout ajustement manuel enregistré sur `User#moteur_caps` (jsonb) **l'emporte**
puissance par puissance (`Hash#merge`, le second argument gagne). Le Conseil ne se rejoue pas à
chaque lecture — c'est un point de départ, jamais recalculé après coup.

L'écriture (`MoteurCapsController#update`) a deux choix techniques à reproduire :

- **`current_user.update_columns(moteur_caps: caps)`**, explicitement pour **éviter tout
  callback `mathieu_core`** sur le modèle `User` central — commentaire du code : « pas de
  callback mathieu_core sur le User central ». Un `update!` standard aurait déclenché les hooks
  usuels (validations, `on_change`, etc.) sur un modèle qui en porte plusieurs ; ce n'est pas
  souhaité pour un simple ajustement de préférence. **Vérifier au portage** si l'équivalent Rails
  natif de `User` porte des callbacks dont on doit ou non se prémunir de la même façon — la
  raison technique (éviter des effets de bord non désirés sur un modèle central) peut disparaître
  si le portage retire les callbacks concernés, mais alors `update_columns` devient un choix à
  reconsidérer plutôt qu'à recopier aveuglément.
- **Fusion partielle explicite** (`(current_user.moteur_caps || {}).merge(updates)`) : un POST
  ne touche que les puissances soumises, jamais les autres — permet d'ajuster les 6 caps depuis
  le Profil en une fois, ou une seule depuis sa fiche, sans écraser le reste.
- **Garde anti-open-redirect** sur `return_to` (`safe_return_to`) : n'accepte qu'un chemin
  interne commençant par `/` et rejetant explicitement `//` (protocole-relatif, qui pointerait
  vers un autre hôte). Motif générique à reproduire **partout où un contrôleur redirige vers un
  paramètre fourni par le client** — jamais une confiance aveugle dans une valeur de retour.

## 5. `PuissancesController` : un contrôleur « self-only » implicite

Ni `:id` ni `user_id` en paramètre — `@slug` identifie la Puissance, jamais un autre joueur.
Toutes les actions (`show`, `questionnaire`, `submit`, `publier`) opèrent implicitement sur
`current_user`, sans garde d'autorisation explicite nécessaire : il n'existe structurellement
aucun chemin pour agir sur les données d'un tiers via ce contrôleur. Même famille de patron que
`UsersController#only_me_resource` (source : `mathieu_core`, déjà signalé au P1 comme bloquant
toute vue du profil d'un tiers) — **au portage, un contrôleur « self-only » n'a besoin d'aucune
vérification de propriété, seulement d'authentification** ; ajouter une garde de propriété ici
serait une sur-ingénierie, pas une amélioration de sécurité.

## 6. Ce que ce document ne couvre pas

- Le contenu éditorial complet (`config/puissances/*.yml`, 6 fichiers, 162 archétypes) —
  catégorie A, déjà porté (`7da4277`).
- La publication volontaire (`publie`, Lot P1b) — déjà caractérisée dans
  [caracterisation-progression-omega.md](caracterisation-progression-omega.md) et les commits
  P1b du 2026-08-01 ; seulement rappelée ici par référence.
- Le détail exact de la validation « illustration obligatoire si libre » côté vue/formulaire
  (§2) — non confirmé au niveau modèle/contrôleur dans ce passage.

## 7. Vérification de parité recommandée

1. Compléter un questionnaire avec des réponses de sphères hétérogènes (ex. Ombre 3 sur une
   sphère, Ombre 1 sur les deux autres) → `o_level` retient le **maximum** (3), jamais une
   moyenne.
2. Refaire le questionnaire d'une Puissance déjà évaluée → nouvelle ligne créée, l'ancienne reste
   lisible ; `latest_for` reflète la nouvelle.
3. Un joueur en état « libre » à O3-L3 → `cap` renvoie `nil`, la vue affiche un texte de clôture,
   jamais une erreur ni un cap fantôme.
4. Ajuster un seul cap depuis la fiche d'une Puissance → les 5 autres caps du joueur restent
   inchangés (fusion partielle, §4).
5. Un `return_to` forgé en `//attaquant.example.com` (ou toute valeur ne commençant pas par un
   `/` simple) → jamais suivi, repli sur `/users/me`.

## 8. Parité vérifiée sur pointzero-app — 2026-08-03 (instance pile neuve)

Les cinq vérifications du §7 passent sur `pointzero-app` (commit `c5eceee`), exécutées en
conteneur contre le code porté avec un compte jetable détruit ensuite :

1. Sphères hétérogènes (o3/o1/l2) → `o_level = 3`, maximum et non moyenne. ✓
2. Requestionnaire → deuxième ligne, l'ancienne intacte, `latest_for` suit. ✓
3. O3-L3 libre → `cap` nil ; bloqué → cap `circulation`, jamais `amplitude`. ✓
4. Fusion partielle : un cap ajusté, les cinq autres intacts ; le manuel prime sur le
   Conseil (`effective_moteur_caps`). ✓
5. `return_to` en `//attaquant.example.com` et `https://…` → repli `/users/me` ;
   `/parcours` → suivi. ✓

Le point laissé ouvert au §4 (recopier ou reconsidérer `update_columns`) est tranché et
documenté dans le code : la raison mathieu_core a disparu, mais `update_columns` reste juste —
un `update!` standard revaliderait tout le profil (prénom obligatoire…), et un compte incomplet
ne doit pas être empêché d'ajuster un cap. La valeur est déjà filtrée par la liste `VALID`.

Le point du §6 (« illustration obligatoire si libre » côté formulaire) reste non confirmé —
même statut qu'à la source, le questionnaire porté est identique.
