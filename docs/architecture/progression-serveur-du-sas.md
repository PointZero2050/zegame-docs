# La progression des cinq jeux passe sur le serveur ; le stockage du navigateur disparaît

> Plan validé par Boris le 19 octobre 2026. Tenu par le portable : les temps 1 et 2 sont en préprod
> (`pointzero-app`, branche `preprod`, `ed748f7`). Le temps 4 revient au poste fixe, et les textes à Codex.
>
> **État au 20 octobre 2026 (nuit) : LES CINQ TEMPS SONT EN PRÉPROD** (`ee33ba4`).
> - Temps 1 à 3 : le portable (`57d771e`, `28170d0`).
> - Temps 4 : le poste fixe, #441 (`65f4c8e`), recetté sur `m0` de bout en bout, puis les textes de Codex par
>   #443 (`c45d054`).
> - Temps 5 : le portable (`68cd6f5`).
>
> La politique 1.1 (#438) dit vrai depuis. **Rien en production** : #438, #441, #443 et le temps 5 partiront
> ensemble, sur le mot de Boris.

## Contexte

Boris, 19 octobre 2026 : « le stockage est un reliquat de la V1 des parcours, il faut le supprimer et
avoir une progression serveur », puis « il n'y aura plus de parcours non-connectés ».

**Aujourd'hui** :
- Les cinq jeux du Sas gardent tout leur état dans le `localStorage` : écran, réponses, textes libres,
  achèvement, badge.
- Le serveur ne reçoit qu'une trace achevée (`TraceSas`), envoyée par une page : le M0, l'écran
  `/sas/import` ou le bandeau d'excursion.
- #420 (en préprod) range cet état par compte, mais toujours dans le navigateur : une partie ne suit pas
  le joueur d'un appareil à l'autre.

**Mesuré** :
- Production : 58 comptes, **aucune** `TraceSas`. Préprod : 37 traces, sur 10 comptes d'essai.
- **Rien à migrer.** Les états restés dans les navigateurs sont abandonnés, et effacés à la première
  visite.

**Le résultat attendu** :
- Une partie se reprend sur tout appareil où l'on est connecté.
- Le serveur constate lui-même l'achèvement (trace, 5 Ω, badge).
- Le Sas n'est plus jouable sans compte.

**Le précédent à suivre** : Immateria, `app/controllers/immateria_controller.rb:13-63`.
- L'état du jeu est enregistré sur le serveur.
- Il est rendu dans la page, ce qui garde une lecture synchrone au chargement.

**Le partage** (répartition de phase 2) :

| Qui | Quoi |
|---|---|
| **Le portable (moi)** | Modèle, migration, route, contrôleur, portes, nettoyage serveur et bancs serveur. |
| **Le poste fixe** | Les JS du Sas et du M0, les vues et leurs textes, et ses bancs, d'après un **contrat** que je dépose dans sa boîte. |
| **Codex** | La politique de confidentialité (§ 4.2, et la « mémoire locale » vers la l. 294) et les canons qui promettent le stockage local (wireflows § 11, canon du Sas, Q17). Ils sont à marquer caducs. |

## Le contrat serveur

**`PartieSas`** :
- Table `parties_sas`, avec `self.table_name` et des `class_name` explicites : Rails singularise
  « sas » en « sa ».
- Colonnes :
  - `user_id` (clé étrangère, non nul) ;
  - `path_slug` (non nul) ;
  - `etat` (jsonb, non nul) ;
  - **`revision`** (entier, non nul, 0 par défaut) ;
  - horodatages.
- Index unique `[user_id, path_slug]`.
- `PartieSas.assainir_etat` reprend `TraceSas.choix_de`, `valeur` et `badge_de` (`app/models/trace_sas.rb`) :
  - il rend la forme qu'attend le jeu : `schema_version`, `path_slug`, `guide_slug`,
    `last_confirmed_screen`, `started_at`, `updated_at`, `completed_at`, `choices`,
    `badge {slug, acquired_at}`, `completed_guides` ;
  - `visitor_local_id`, un identifiant d'appareil, et `import_status` disparaissent.

**`PUT /sas/parties/:slug`**, `PartiesSasController#update`, en JSON :
- **Garde-fous** :
  - `before_action :authenticate_user!` sans option : les deux portes lisent ce rappel ;
  - `wrap_parameters false` ;
  - corps brut parsé une fois et mémoïsé, plafonné à 32 Ko ;
  - `path_slug` doit valoir le slug ;
  - `rate_limit`, déclaré après l'authentification ;
  - upsert rejoué si `RecordNotUnique`.
- **Révision** : le client envoie `revision = base + 1`. Le serveur n'écrit que si la révision reçue
  dépasse la sienne. Sinon il répond 409 avec l'état courant, ce qui couvre deux onglets, le retour
  arrière et les envois croisés.
- **Achèvement** : si l'état porte `completed_at` et le badge du parcours, le serveur importe la trace.
  - **`premiere: true`** seulement si la trace n'avait pas d'`achevee_le`.
  - `achevee_le` n'est jamais effacée ; la plus ancienne reste (tolérance d'une seconde).
  - « Rejouer » ne touche ni la trace, ni les Ω, ni le badge.
- **Contrôle des badges** :
  - `skip_around_action :guetter_les_accomplissements, unless: :achevement_a_importer?`.
  - Le contrôle ne tourne donc que sur l'enregistrement qui achève, avec les mêmes annonces de seuils
    qu'aujourd'hui.
- **Réponse** : `{revision, achevee, premiere, omegas}`.

**Le rendu** : le partiel `sas/_partie_serveur` est rendu dans le `<head>` des cinq vues. Il porte :
- `csrf_meta_tags` (les pages du Sas n'en ont pas) ;
- l'URL de l'API ;
- `<script type="application/json" id="pz-parties">` :
  - les états du joueur et leurs révisions ;
  - **les parcours achevés selon `TraceSas`**, pour que la galerie dise « Accompli » même après un
    « Rejouer » ;
  - le tout passé par `json_escape`, contre un `</script>` dans un texte libre.
- Les pages du Sas sont servies en `no_store`, contre le HTML périmé du retour arrière.

**Les portes** : `"sas"` et `"parties_sas"` entrent dans `PorteDuMondeUn::AUTORISES`
(`app/controllers/concerns/porte_du_monde_un.rb:22`).
- Sans elles, le joueur qui n'a pas passé le M0 perd l'iframe : redirection en HTML, 403 en JSON.
- On ne touche pas `PorteDuModeEvenement` : un compte « Festival seulement » est refusé, ce qui est
  voulu.

## Le contrat client, pour le poste fixe

**`public/sas/partie.js`**, chargé avant `galerie.js` et `app.js`, expose `window.PZPartie` :
- `lire(slug)` : synchrone, depuis `#pz-parties` ;
- `achevee(slug)` : vrai si le parcours est achevé selon le serveur ;
- `enregistrer(slug, etat)` :
  - PUT immédiat à chaque écran, choix, conclusion ou remise à zéro ;
  - 800 ms d'attente pour le texte ;
  - **`keepalive` sur chaque PUT** : l'iframe annule sinon ses envois quand le M0 navigue ;
  - un envoi en vol et un en attente, au plus ;
  - sur 409, il adopte l'état du serveur ;
  - sur 401, un avis « reconnecte-toi » ;
- `vider()` : une promesse que les liens de sortie attendent, quatre secondes au plus ;
- l'événement `pz:partie` sur `document`, avec la réponse du serveur.
- **Une fois**, il efface les clés `pz_parcours_*`.

**Le reste du lot client** :
- **Les cinq `app.js`** :
  - `loadState` lit `PZPartie.lire` et reste un normaliseur ;
  - `saveState` appelle `PZPartie.enregistrer` ;
  - toujours **aucun envoi au chargement** (`persist:false`) ;
  - `initLocalTools` disparaît.
- **`galerie.js`** lit `PZPartie.achevee` et `lire`.
- **`pont-m0.js`** écoute `pz:partie`, ne sonde plus le stockage, et envoie au M0 `pending`, puis
  `done{premiere, omegas}`.
- **`panorama.js`** ne poste plus rien. `partir()` attend tant qu'un enregistrement est en vol, et le
  reçu vient du message.
- **Les liens `data-import-sas`** deviennent « attendre l'enregistrement ».
- **Les textes** : « sans compte », « sur cet appareil », « Quitter et conserver ma progression »,
  `_passage_accompli`, `_sortie_vers_le_jeu` (son lien public mène à l'entrée du jeu).

## La livraison, en cinq temps — la préprod marche à chaque étape

1. **Correctifs serveur, tout de suite (moi)** :
   - `TraceSas.importer!` ne crédite les Ω que d'une trace achevée, et n'efface plus une `achevee_le` ;
   - `User` reçoit `has_many :traces_sas` (`dependent: :delete_all`), qui manque : `User#destroy`
     échouerait sur la clé étrangère.
2. **Serveur additif (moi)** :
   - migration, `PartieSas`, route, contrôleur et portes ;
   - le partiel, rendu à côté de `_compte_local` ;
   - `EtatDuMondeZero` lit `PartieSas` pour l'état « commencée », en une seule requête avec
     `TraceSas` (son budget de requêtes, l. 65-67) ;
   - `FermetureDeCompte.fermer!` efface les parties et vide le texte libre des `choices` des traces
     (son commentaire de doctrine est amendé) ;
   - le banc neuf.
   - L'ancien client continue de lire son navigateur.
3. **La porte du Sas (moi)** :
   - `SasController` exige un compte ; l'anonyme passe par la connexion et revient à son jeu ;
   - `/sas/vers-le-jeu` devient une redirection dans les routes, et non plus une action publique ;
   - `PlanDuSite` ne publie plus `sas` ;
   - les bancs qui lisaient le Sas sans compte se connectent.
4. **La bascule du client (poste fixe), d'un bloc** : `partie.js`, les cinq jeux, la galerie, le pont,
   le panorama et les vues partagent un protocole de messages. Avec eux partent :
   - les socles d'import de `_bandeau` et de `challenges/_passage` ;
   - ses bancs ;
   - la politique de confidentialité réécrite (Codex).
5. **Le retrait (moi), en dernier**, pour qu'un onglet du M0 ouvert avec l'ancien `panorama.js` ne
   tombe pas sur une 404 :
   - `/sas/import` : le GET redirige vers l'accueil du joueur, le POST est supprimé ;
   - `TracesSasController`, `traces_sas/new`, `_compte_local` et ses huit inclusions,
     `import-sas.js`, `passages[]` et la redirection d'`inscriptions`, `IMPORT_DES_TRACES`,
     l'entrée `traces_sas` des portes ;
   - les commentaires périmés.

## Les bancs

**Neuf, `verifier_parties_sas`**, avec `Session.new(email, monde: 0)` pour éprouver la vraie porte, et
le PUT ajouté à `scripts/session.rb`. Il vérifie :
- **L'accès** :
  - `/sas` anonyme → connexion, puis retour au jeu ;
  - un PUT anonyme → 401 ;
  - un joueur du M0 → 200 sur `/sas?dans=m0` et sur le PUT ;
  - un compte « Festival seulement » est refusé.
- **Le rendu** :
  - seulement les états de ce compte, deux comptes ayant deux contenus ;
  - un `</script>` enregistré revient échappé ;
  - sans jeton CSRF, le PUT est refusé.
- **Rien n'est écrit** pour un slug étranger, un corps trop gros, un JSON invalide ou un badge forgé.
- **Les Ω** :
  - un état inachevé ne donne ni trace ni Ω ; contre-épreuve : le même état achevé donne +5 ;
  - un renvoi donne `premiere:false` et Ω inchangés ;
  - « Rejouer » puis achever garde la trace, sans Ω de plus.
- **Les révisions** : une révision 4 après une révision 5 → 409, et la 5 reste.
- **Le coût** : un PUT qui n'achève pas ne lit pas les badges.
- **`EtatDuMondeZero`** dit à faire / commencée / faite, en une seule requête.
- **Les comptes** : `User#destroy` passe, tables pleines ; la fermeture efface les parties.
- **Contraposée** : `pz_parcours`, `pz-compte-local` et `/sas/import` n'apparaissent plus dans
  `app/` ni `public/`, hors du nettoyage. Le chercheur trouve une chaîne plantée exprès.

**À reprendre côté serveur** :
- `verifier_sas_vers_le_jeu` (§ 1 à 5, et 16) ;
- `verifier_porte_du_prologue` (l. 66-69) ;
- `verifier_inscription_ouverte` (l. 58-62) ;
- `verifier_bascule_m0_m1` (l. 166) ;
- `verifier_moteur_conscience` (l. 148) ;
- `verifier_excursion` (l. 589-600) ;
- `verifier_plan_du_site` (l. 200) ;
- `verifier_fermeture_de_compte` ;
- `verifier_omegas_du_sas` ;
- ceux qui lisent le Sas sans compte : `accueil_public`, `scenarios_neoarchaiques`,
  `films_scenarios`, `sortie_sas` ;
- `verifier_import_sas_sans_heritage` est supprimé : son objet disparaît.

**À reprendre côté client (poste fixe)** :
- `verifier_monde_zero_panorama` (§ 10, 12) ;
- `verifier_prelude_video` ;
- `verifier_monde_zero_aiguillage` ;
- `verifier_excursion` (l. 770-800) ;
- `verifier_marelle` (l. 2183-2206) ;
- `verifier_sas_vers_le_jeu` (§ 6 à 15, et les « dix lecteurs » du § 16).

## Vérification

1. **Avant le chantier** : sauvegarde de la base de préprod, vérifiée par son contenu, et du code
   serveur.
2. **Temps 1 à 3** :
   - à chaque temps : migration, build, banc neuf et bancs touchés ;
   - contre-épreuve : l'ancien `importer!`, remis dans le conteneur, rougit sur « inachevé → aucun Ω ».
3. **Temps 4 et 5**, recette des bancs touchés, puis au navigateur sur un compte de démo :
   - jouer Humanité jusqu'à h03 ;
   - rouvrir dans une fenêtre privée sur le même compte : reprise à h03 ;
   - achever dans le M0 : trace, +5 Ω et reçu ;
   - aucune clé `pz_parcours_*` ;
   - deux onglets : le plus ancien adopte l'état du serveur.
4. **Essai de Boris en préprod.** Promotion **sur son mot seulement**, avec la migration avant le build.
