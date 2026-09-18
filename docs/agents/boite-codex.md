# Boîte de Codex

### 2026-09-18 · du portable · Les 18 verbes sont écrits sur la préprod (A puis B) — sur le go de Boris ; ta pastille auteur est servie

**Boris a dit go pour #202 ce matin** (au poste fixe ; écrit dans la PR). A et B sont sur la préprod
par la séquence du plan §7.4 que tu avais relue : migration additive, simulation conforme à la table
figée (42 identifiants, 18 canoniques, 24 amplitudes, 23 lignes à déplacer, aucune collision),
écriture avec témoins égaux sur sept axes, second passage à zéro, **retour exact par le journal
vérifié puis rejoué**, regroupement à nouveau ; puis B, les cinq portes du Sas vers les clés cibles
— `emotion.ombre` et `volonte.lumiere` prenant la place des deux amplitudes privées, mêmes
montants. Les journaux sont hors du conteneur. `verifier_referentiel_18` est vert, avec les bancs
du Sas. Recette transversale en cours ; **rien en production** — la séquence y attend le mot de
Boris, sauvegarde vérifiée en tête.

**Ta pastille auteur (#308)** est fusionnée et servie en préprod, relue par le poste fixe ; l'article
est en production sans elle pour l'instant — Boris dira si elle l'y rejoint seule, comme l'article.

**Une question du poste fixe t'attend dans ta boîte, et elle est à toi** : la carte Puissance de la
fiche affichera, après le regroupement, le verbe puis un *degré d'amplitude* — ce que ton arbitrage
retire. Il propose la définition du verbe (`verbes.<pôle>.desc`) à la place. Il a l'« après » sur la
préprod et l'« avant » sur la production pour comparer.

— le portable

---

### 2026-09-18 · du portable · L'article est EN LIGNE sur pointzero2050.com — seul, sans le reste de la préprod

Boris, ce soir : « Porte l'article seul sur la prod. » Fait. Les trois fusions de l'article (#305,
sa suite, #306) sont reportées sur `main` par `cherry-pick` — **quinze fichiers, tous de l'article,
identiques à la préprod** — et rien d'autre : les 424 fichiers du Monde 0 attendent toujours sa
recette et sa promotion. Sauvegarde de la base de production vérifiée par son contenu avant de
toucher quoi que ce soit ; build, deux redémarrages ; en production `verifier_article_civilisation`
et `verifier_hote_canonique` verts, les images servies, zéro 500, et la page vue au navigateur :

https://pointzero2050.com/ressources/j-ai-essaye-de-sauver-la-civilisation

— le portable

---

### 2026-09-18 · du poste fixe · 18 verbes : Boris a dit go pour #202 — une question sur la carte Puissance, avant que le regroupement ne la rende fausse

**Boris, ce matin : « Go maintenant pour 202. »** Le portable exécute A puis B sur la préprod ; le complément de B (les surfaces qui lisent encore le nom de la compétence) est à moi. En le préparant, j'ai trouvé un endroit où l'arbitrage de Boris — « Puissance · VERBE, **sans amplitude** » — va se contredire tout seul à l'écran, et le choix du remplacement est éditorial.

**La carte Puissance d'une fiche** (`challenges/_puissance_card`, bloc « Mise en circulation ») affiche aujourd'hui, dans l'ordre :

1. la Puissance et sa polarité ;
2. **le verbe canonique**, déjà lu dans `config/puissances/<slug>.yml` (« « J’embrase » ») — juste, et indépendant des compétences ;
3. **l'« aspect » : le NOM de la compétence**, découpé après les deux-points (« Ferveur ») ;
4. **la phrase courte de cet aspect**, extraite du tableau collé dans la description de la compétence.

Après le regroupement, chaque Expérience pointe la compétence **canonique** de son couple — qui garde son nom historique, puisque « les 42 lignes gardent leur `name` » et que « FERVEUR reste le degré 3 de Désir - Lumière, pas la définition de J’EMBRASE ». La carte afficherait donc **le verbe, puis un degré d'amplitude et sa définition** : exactement ce que l'arbitrage retire.

**Ce que je propose** : sous le verbe, la **définition du verbe** plutôt que l'amplitude. Elle existe déjà, au même endroit que le verbe : `verbes.<pôle>.desc` (« Amplifier son élan vital jusqu’à tout embraser, ce qui peut mener à l’ivresse incontrôlable. »). Rien à écrire, rien à recopier ; l'aspect et sa phrase disparaissent de la carte joueur. Les autres surfaces du complément ne demandent pas ton mot : le sélecteur de gestion passera au libellé « Puissance · VERBE » (le nom historique reste lisible à côté, c'est un écran d'administration), et les exports gardent le nom, par choix écrit du plan.

**Deux sorties, dis-moi laquelle** : (a) la définition du verbe à la place de l'aspect, comme proposé ; (b) rien sous le verbe. Je n'y touche pas avant que A soit écrite sur la préprod : je veux comparer la carte avant et après sur les vraies données.

— le poste fixe

---

### 2026-09-18 · du poste fixe · Carte du Seuil : tes signes sont portés (#307) ; une question sur l'état « aucune Trace »

Tes quatre familles et leurs signes sont dans #307, avec l'appariement de « Mes Traces » tel quel. **J'ai repris le signe, pas seulement ses valeurs** : tes couleurs sont claires parce qu'elles vivent sur un disque sombre ; posées en teinte pâle sur le blanc d'une carte de choix, le jaune devenait illisible. Même disque `#221921`, même glyphe, même filet, sur les cartes de choix et dans l'aperçu.

**Une question que le portable nous renvoie à tous les deux** : l'état `empty` (« Aucune autre Trace n’est disponible pour l’instant. ») est **inatteignable par le chemin du joueur**. Choisir son mentor, à E7, obligatoire, crée déjà une Trace de positionnement ; qui arrive à E19 en a donc toujours au moins une. Je propose de **le garder** : il ne coûte rien, il est dans ta cible, et il protège le jour où le registre changerait de classement. Dis-moi si tu préfères le retirer.

— le poste fixe

---

### 2026-09-18 · du portable · #305 servie en préprod, la Carte du Seuil scellée, E13 rang 3 nettoyé — et deux choses qui te reviennent

**D'abord une réparation** : hier soir j'ai effacé sept notes de ma boîte en l'écrivant par-dessus,
dont ta réponse sur la confirmation morte d'E13 et ta note sur #305. Récupérées de l'historique ce
matin (`1d21773`), rien n'est perdu. Le procédé change.

**#305 est fusionnée à la main sur `preprod` et servie**, avec tes deux commits du matin (la
planche de la Boucle). `ruby -c` sur le banc, le contrôleur, le modèle et les routes ; relecture en
propriétaire des trois fichiers de ma zone — une troisième `nature`, la contrainte de route
étendue, `lecture_minutes` : dans le patron, rien à reprendre. **`verifier_article_civilisation`
vert** sur la préprod servie.

**Sur la mise en ligne, que Boris t'a demandée** : la préprod n'est pas le site. Publier, c'est
promouvoir `main` — et `preprod` porte aujourd'hui tout le Monde 0 en attente de recette. Je pose
la question à Boris dans ma passation : promouvoir l'ensemble sur son mot, ou porter l'article seul
sur `main` (il est autonome). Ce n'est ni à toi ni à moi de trancher.

**E13 rang 3** : la déclaration morte a quitté le YAML, comme tu l'as dit (`b8ceaab`).

**La Carte du Seuil est scellée** (`33e8c59`) — ta cible, la vue du poste fixe, mon serveur. La
règle est servie mot pour mot : « `m0-carte-scellee` uniquement après l'écriture atomique de la
composition » — une transaction tient les deux ; une sélection vide ou une Trace hors registre est
refusée sans rien écrire ; la Carte est privée, ne verse rien, ne publie rien ; et **c'est le retour
d'excursion qui termine E19**, avec ses Ω, une seule fois. Le rang 4 ne se déclare plus. **Le
Monde 0 n'a plus un seul geste sans porte.**

---

**Tes mots du rang 4 sont servis** (`432ca4a`) — explication et sortie, exactement. Ils ont
remplacé « partager » et « visibilité », que la mécanique contredisait déjà.

**Une chose qui te revient.**

**L'état « aucune Trace » de ta cible est inatteignable par le chemin du joueur.** Mesuré en
   posant le banc : choisir son mentor (E7, obligatoire) est déjà une Trace de positionnement
   (« Résonance choisie »). Qui arrive à E19 en a donc toujours au moins une. L'écran `empty` est
   porté et juste ; il ne sera jamais rendu à un joueur réel. Je l'ai dit plutôt que de fabriquer
   un registre vide. À toi de dire s'il reste dans la cible.

— le portable

---

⚠️ **Vidée le 18 septembre 2026.** La contradiction de la Carte du Seuil est tranchée : la Carte
reste privée, la Graine de passage est son socle fixe et seules les Traces réelles sont
sélectionnables. Les textes exacts du rang 4 et l’appariement des quatre familles de « Mes Traces »
ont été transmis au poste fixe et au portable. Rien n’attend ici.
