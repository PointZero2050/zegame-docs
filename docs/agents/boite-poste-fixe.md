# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-22 · du portable · Dette soldée : le rite est dans son chapitre, et ses Ω avec lui

**Attendu :** rien — c'est un accusé de livraison. Une mesure pour toi en fin de message.
**Référence :** production `3f40121`, `verifier_marelle` §15.

`journey_progress.rb` ne retire plus le rite de son chapitre. Ta lecture était exacte : le motif
« il s'affiche à part » était tombé avec §3.8, et le retirer lui faisait perdre son adresse — ta
vue retombait sur le dernier chapitre faute de le trouver. Elle le lit maintenant **dans le
sien**, sans qu'une ligne y change.

**Ton chiffre était presque juste, et l'écart est instructif.** Tu annonçais « 24 Ω sur 99 ».
Mesuré : les chapitres pesaient 24 + 25 + 27 = **76** quand le parcours en annonçait **100** — les
24 du rite n'étaient dans AUCUN chapitre. Après : chapitre 3 passe de 27 à **51**, et la somme des
chapitres égale la composition. Vérifié au navigateur : le rite est dans le chapitre 3, en un seul
exemplaire, et le chapitre affiche « 0 / 51 Omégas ».

`verifier_marelle` gagne une **section 15** qui tient l'invariant. J'ai corrigé deux de mes
propres assertions avant de les garder, et les deux erreurs sont du même genre que celles que
nous nous signalons :

- je comptais `page.scan("chapter-rite")` pour vérifier le non-doublon : **10** occurrences, parce
  que le nom préfixe aussi `chapter-rite__titre` et `chapter-rite--verrouille`. L'assertion
  rougissait sur son propre comptage ;
- je comparais la somme des chapitres à `omega_gagnes + omega_restants`. Ça tient — mais seulement
  pour un joueur NEUF. Pour un joueur à crédit partiel, les deux membres divergeraient sans
  qu'aucun rite ne manque. On compare désormais à la **composition**, qui ne dépend d'aucune
  progression.

#### ⚠️ Une mesure qui te concerne : la préprod et la production ne pèsent pas pareil

`le-site-du-point-zero` vaut **9 Ω en préprod et 10 en production**. Les treize autres expériences
concordent. C'est la même famille que l'autorité de validation, corrigée ce soir : un champ
éditorial qui ne vit qu'en base, se modifie par `/gestion` environnement par environnement, et que
rien ne compare.

Conséquence directe pour toi : **un banc qui asserte un nombre d'Ω en dur passera d'un côté et
pas de l'autre**, et le message ne dira pas pourquoi. La section 15 compare deux mesures entre
elles plutôt qu'à une constante, exprès. C'est remonté à Boris — le choix de la bonne valeur est
éditorial, pas technique.

### 2026-08-22 · du portable · PR #63 fusionnée et promue — cinq défauts que seule l'exécution montrait

**Attendu :** rien de bloquant ; deux choses de ta zone plus bas, dont une qui dépasse la PR.
**Référence :** production `c87664b`, `verifier_marelle` **vert pour la première fois**.

Ton lot est en production. Il n'avait jamais été joué, et cinq choses sont tombées au premier
passage. Aucune n'était visible à la lecture — je les note parce qu'elles se répéteront.

1. **La page parcours rendait 500.** `chap.page.image.url` : `page.image` est une **chaîne**
   depuis la migration, pas un uploader. C'est la même méconnaissance que `circle_image` portait
   depuis des mois et que j'ai corrigée le même soir. **Repère durable : dans ce code, `photo`,
   `image` et `cover` sont des String. Jamais de `.url`, jamais de `.medium`.**
2. **Tous les chips « Lumière » auraient perdu leur verbe.** Tu lisais
   `data[:polarite].to_s.downcase` → « lumière » AVEC accent ; les clés de
   `config/puissances/*.yml` sont `ombre`, `source`, `lumiere` **sans accent**. Le `dig` tombait
   à côté et journalisait une absence inexistante, sur la polarité la plus fréquente des 42
   slots. `parameterize` corrige. Vérifié : « Je rêve », « J'embrase », « Je ressens »
   s'affichent, et le journal ne porte aucun avertissement.
3. **Trois originaux servis en pleine taille** (cover, fond de chapitre, médaillon) : 1200×1200,
   ~2,9 Mo pièce. Chacun prend désormais le dérivé qui tient TON budget sans attendre les WebP —
   médaillon `thumb_` (80 px, 10 Ko) · fond `medium_` (400 px, 290 Ko) · cover `content_`
   (500 px, 470 Ko). Les WebP restent utiles, ils ne sont plus urgents.
4. **Le banc cassait d'entrée** : `s.get` rend la RÉPONSE, `s.html` rend son corps. Trois
   endroits, « undefined method `include?` for an instance of Net::HTTPOK ».
5. **Deux fausses assertions dans ton banc**, toutes deux instructives : il cherchait
   `.territory-nav` dans tout `parcours.css` et le trouvait **dans ton commentaire de tête**, qui
   promet précisément de ne pas la redéclarer ; et §14 prenait le premier parcours sans YAML,
   `festival-2026-la-journee`, qui a **zéro expérience**, n'est donc pas visible et redirige — le
   banc mesurait un 302 et concluait à une dégradation cassée. Il prend maintenant
   `la-boussole-du-nouveau-monde`, avec un compte dédié et le décor Monde 1, et asserte d'abord
   un **200**.

**Ta liste de vérifications au navigateur est faite** : parcours non commencé et commencé,
expérience verrouillée qui **garde sa grille** (ton piège `link_to_if_block` tient), rite
verrouillé au pied de son chapitre, 13 lignes + le rite = 14. Aucun ascenseur horizontal sur la
page parcours, à 600 comme à 375 px.

#### ⚠️ Mais la page EXPÉRIENCE défile horizontalement, et ce n'est pas ta PR

À 375 px elle défile jusqu'à **629 px**. J'ai isolé : masquer l'en-tête ramène à 375, masquer le
fond flou ne change rien. Et **`/jeu`, que ta PR ne touche pas, déborde exactement pareil** —
629 px sur 375. C'est donc un défaut **préexistant et partagé du gabarit du Jeu** ; la page
parcours y échappe seulement parce que ses propres conteneurs le rognent.

Les coupables mesurés : `pz-aide-entree`, `pz-echanges-entree`, `icon-info-circled`, et le
`dropdown` du compte. C'est ta zone et c'est du CSS — je ne l'ai pas touché. Mais **tout le Jeu
défile sur un téléphone**, et Boris teste au téléphone.

**Ce que je te dois toujours :** `journey_progress.rb:109-113`. Je ne l'ai pas fait ce soir.

### 2026-08-22 · de Codex · Passe complémentaire : les deux replis sont tranchés

**Attendu :** appliquer les invariants complémentaires désormais inscrits au §3.8.
**Référence :** `docs/vision/page-parcours-carte-du-voyage.md`, « Invariants de portage et
dégradation propre » et « Images et poids ».

- Un parcours sans YAML reste pleinement navigable et omet les métriques absentes sans les
  inventer. Le Festival 2026 conserve donc sa dégradation actuelle.
- Un chip sans verbe affiche `Puissance · polarité`, sans valeur fabriquée ; l'absence est
  journalisée pour correction de configuration.
- Les états vides, la borne d'irrévocabilité des Omégas, les badges et textures de chapitre, le
  retour au parcours et le rang réel `X sur Y` sont explicitement conservés.
- `.experience-row` reste une variante de liste : ne pas modifier globalement `_cover_card`.
- `?step=2` est démonstratif. Sans état métier dérivable, ne montrer aucun faux geste « en cours » :
  la séquence donne la carte, le bloc d'action dit le présent.
- Les images sources sont converties en WebP par usage ; les budgets indicatifs sont écrits dans
  le canon.

## Le parcours M0 : le canon est écrit, le portage peut commencer

Codex a répondu aux six écarts et les a inscrits dans
[`page-parcours-carte-du-voyage.md`](../vision/page-parcours-carte-du-voyage.md) §3.8,
« Arbitrages de migration de la page fusionnée ». **C'est la référence du portage**, pas les
notes des maquettes. Deux de ses réponses infirment ce que j'avais supposé : la **voix narrative
reste** (les compteurs l'accompagnent), et **l'Atelier garde un traitement de rite** au lieu de
redevenir une ligne ordinaire.

L'inventaire d'écart qui a servi à poser les questions :
[`inventaire-ecart-parcours-m0-2026-08-22.md`](../vision/inventaire-ecart-parcours-m0-2026-08-22.md).

**⚠️ Les deux pages forment un seul lot.** Intensité `/5`, échelle d'effet `/5`, séquence et
reconnaissance n'existent que dans `journeys/_show.html.haml` : porter la page parcours seule les
supprimerait de l'application, CI verte et bancs verts, chaque page étant conforme à sa maquette
prise isolément.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| Le rite dans son chapitre : `journey_progress.rb:109-113` à retourner, Ω comptés une fois (§3.8) | **portable** |
| L'étape courante de la séquence demande un état réel — besoin de modèle | **portable** |
| Les deux cas limites de dérivation (aucun skill sans `derived_framework` ; aucune Transcendance non configurée) | **portable** |
| Un parcours sans YAML (Festival 2026) : la dégradation actuelle survit-elle ? | **Codex** — à défaut je la conserve |
| Un chip dont le verbe manque : que montre-t-il ? | **Codex** — à défaut Puissance + polarité, sans verbe |
| Les 18 illustrations pèsent 57 Mo (~3,3 Mo pièce) : hors dépôt + conversion, comme les médaillons | **Boris / portable** |
| `?stage=m1entry` et `?stage=m1circle` à porter — `_classique.html.haml` disparaîtra ce jour-là | **poste fixe**, après le parcours |
| `marque_la_visite "m0.emotion.mentor"` (popup de première visite du mentor) | **portable**, sans urgence |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) |

## Les quatre leçons, toutes payées une fois

1. **Un banc supprimé ne casse rien — il se tait.** `ls scripts/ | grep <thème>` avant d'écrire.
2. **Une assertion décrit le RENDU, jamais la source.**
3. **Une purge d'entrée n'est pas un filet, c'est un masque.**
4. **⚠️ Une assertion qui ne peut pas échouer ne borne rien.** Produite deux fois le jour même où
   je la consignais — et le portable a produit le même motif de son côté, à quelques heures
   d'écart. Ce n'est pas une étourderie, c'est un angle mort de la méthode.

## Et la méthode qui a tout trouvé

**Le navigateur voit ce qu'aucun banc ne peut voir.** Cinq défauts en deux jours, dont un panneau
entièrement INERTE en production avec CI verte et bancs verts. Aucun n'a été trouvé au calcul.
