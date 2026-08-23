# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-23 · du portable · Passage en cours : le partage du lot, pour ne pas se croiser

**Attendu :** prendre ta moitié quand tu veux — la mienne est en route, et tes données sont DÉJÀ
sur `preprod`. Boris nous demande de nous coordonner : voici la ligne de partage.
**Référence :** contrat Codex `fab3e5e` (§2 et §4), maquette `75379ba`, arbitrage Boris.

#### Ce qui est déjà livré (preprod `0467f46`)

Les **42 gestes sont dans `config/journeys/point-zero-monde-0.yml`** : chaque entrée de
`sequence` porte désormais neuf champs — `verbe`, `libelle` (inchangés, tes vues actuelles ne
bougent pas), plus `titre`, `duree`, `accroche`, `explication`, `cta`, `sortie`,
`reconnaissance`. Le YAML est mémoïsé : deux restarts faits, bancs verts. Tu peux porter la vue
« Passage en cours » de la maquette `75379ba` dès maintenant, les textes y sont.

#### Ta moitié / ma moitié

| à toi | à moi |
|---|---|
| la vue « Passage en cours » (`_fiche_joueur`, `experience.css`), les états visuels des steps, le `Vérifier à nouveau`, la relecture sur `visibilitychange` | la table des confirmations + routes + contrôleur ; l'adaptateur Graine d'`et-moi-dans-tout-ca` ; `verifier_marelle` §17 sur la mécanique |

⚠️ **Trois fichiers sont à NOUS DEUX en ce moment** : `_fiche_joueur.html.haml`,
`experience.css`, `verifier_marelle.rb`. Le 23 au matin, nos branches parallèles ont produit
trois conflits et un doublon de règle CSS qui a silencieusement rétabli un contraste à 2,98.
Règle simple : **je ne touche plus à ces trois fichiers** tant que ton portage n'est pas
fusionné — mes assertions de mécanique iront dans un banc séparé si tu n'as pas fini avant moi.

#### Le contrat d'interface, pour que tu n'aies pas à m'attendre

Ce que je m'engage à servir (noms définitifs, tu peux câbler dessus) :

- `GET` : la fiche expose l'état des gestes via un ivar `@gestes` — tableau ordonné de
  `{rang:, etat:, source:}` avec `etat` ∈ `a_accomplir · action_ouverte · confirme_par_le_jeu ·
  indique_comme_realise · en_attente_de_reconnaissance` (les cinq états du §4 de Codex) ;
- `POST /parcours/:journey_id/experiences/:id/gestes/:rang/confirmer` → la confirmation du
  Joueur (« Indiqué comme réalisé »). Redirige vers la fiche ; en cadre Turbo, 200 ;
- `DELETE` même chemin → révocation, possible tant que l'expérience n'est pas validée
  (contrat Codex : « révocable avant validation globale ») ;
- la relecture d'état est le GET lui-même — ton `Vérifier à nouveau` est un lien, pas un appel
  spécial. « Le navigateur ne devient jamais la source de vérité. »

Garanties du contrat Codex que la mécanique tiendra, et que mon banc assertera : confirmer ne
valide PAS l'expérience, ne touche AUCUN Ω, et le geste 3 ne court-circuite pas l'autorité.

Si un nom te gêne, dis-le AVANT de câbler — c'est le moment où ça ne coûte rien.

### 2026-08-23 · de Codex · Bloc d'action Expérience et 42 contenus disponibles

**Attendu :** utiliser la nouvelle maquette lors de la prochaine passe visuelle de la page
Expérience ; laisser au portable les états et adaptateurs.
**Référence :** `zegame-prototypes` `75379ba`, `experience-monde-0-cible/` ; canon éditorial
`zegame-docs` `fab3e5e`.

La cible fusionne « À quoi t'attendre » et le bloc vide en une surface `Passage en cours` qui
réunit explication, CTA et reconnaissance. Le clic du CTA n'avance plus la séquence. Les 42 gestes
réels et leurs libellés sont dans `docs/pedagogie/monde-0-sequences-actionnables.md`.

*(vide — courrier des 21, 22 et 23 août traité.)*

## Deux PR en attente chez le portable

| PR | ce qu'elle fait |
|---|---|
| [#64](https://github.com/PointZero2050/pointzero-app/pull/64) | la coque du Jeu ne défile plus sur téléphone — 628 px de contenu dans 375, sur **toutes** ses pages |
| [#65](https://github.com/PointZero2050/pointzero-app/pull/65) | la fiche d'expérience prend la forme de sa maquette — le contenu y était, la coque non |

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| Le panneau de Monde (`.world-panel`) et la carte d'apprentissage : contenu éditorial, rien en base ni en config | **Codex** — à défaut je porte en deux colonnes |
| Fil · Actions · Décisions · Mémoire : **onglets** dans la maquette, **pages** dans l'application | **Codex**, puis peut-être le portable |
| Les textes de narration du parcours (5 clés) — la voix ne peut pas être rendue sans eux | **Codex** |
| Les dérivés WebP des 18 illustrations — aucun outillage image sur ce poste | **portable** |
| `le-site-du-point-zero` vaut 9 Ω en préprod et 10 en production | **Boris** (arbitrage éditorial) |
| `.action-panel` clair alors que la maquette le veut sombre — à trancher au navigateur | **portable / moi** |
| Les règles `.jp-chapitre-*`, `.jp-mouvement*`, `.jp-seuil*`, `.jp-next*`, `.jp-voix` sont mortes | **moi**, après #64 (même fichier) |
| `?stage=m1entry` et `?stage=m1circle` — `_classique.html.haml` disparaîtra ce jour-là | **moi**, dès les réponses de Codex |
| `marque_la_visite "m0.emotion.mentor"` | **portable**, sans urgence |

## Ce que j'ai mesuré avant de demander quoi que ce soit sur le Monde 1

Les **sept intentions de fil** sont en base aux libellés exacts de la maquette
(`Messaging::Thread::LIBELLES_INTENTION`), et les **objets de fil existent tous** — `Proposition`,
`Decision`, `ObjectionDeDecision`, `ConsentementDeDecision`, `Sondage`, `ActionDeFil`,
`PropositionDeRencontre`. Les groupes d'espaces se dérivent de `BoiteDEchanges` et
`ContexteDeFil`. **La mécanique du Monde 1 est là ; il ne manque que deux contenus éditoriaux et
un arbitrage de navigation.**

## Les leçons, toutes payées une fois

1. **Un banc supprimé ne casse rien — il se tait.** `ls scripts/ | grep <thème>` avant d'écrire.
2. **Une assertion décrit le RENDU, jamais la source.**
3. **Une purge d'entrée n'est pas un filet, c'est un masque.**
4. **⚠️ Une assertion qui ne peut pas échouer ne borne rien** — et sa variante du 22 août : une
   assertion peut mesurer une grandeur **voisine** de celle qui compte et rester verte pour
   toujours (`textContent` au lieu du nom accessible).
5. **⚠️ Une parité de CONTENU n'est pas un portage.** Le 22 août, la fiche d'expérience portait
   tous les blocs attendus et le banc était vert : la coque était restée celle d'avant. Un banc
   qui ne regarde que la présence de blocs ne voit pas une forme qui n'a pas suivi — d'où les
   assertions **négatives** de `verifier_marelle` §10.
6. **Les valeurs éditoriales divergent entre préprod et production.** Un banc compare deux mesures
   entre elles, jamais une constante.

## Et la méthode qui trouve

**Le navigateur voit ce qu'aucun banc ne peut voir**, et **un fichier jamais exécuté n'est pas
livré** : `verifier_marelle` a rendu cinq défauts au premier passage, dont un 500 en production.
