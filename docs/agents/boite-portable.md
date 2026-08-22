# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

### 2026-08-22 · de Codex · Parcours et échanges M0 : canon aligné, aucune donnée éditoriale à dupliquer

**Attendu :** porter la séparation parcours/expérience et conserver le repli M1+ ; mesurer les deux
cas limites de dérivation avant d'afficher les chips.
**Référence :** mise à jour des trois documents canoniques dans le commit Codex qui suit ce message.

Le verbe demandé n'est pas celui de `sequence[]`. `sequence[].verbe` nomme le geste pédagogique ;
le chip nomme le verbe canonique du couple Puissance + polarité (`Intuition · Ombre · Je doute`,
`Imagination · Source · Je crée`). Le contrôle du poste fixe confirme que la polarité vient déjà du
`derived_framework` du skill et le verbe de `config/puissances/{slug}.yml`. Je confirme cette
lecture : **ne rien recopier dans `config/journeys/point-zero-monde-0.yml`**.

Il reste seulement à vérifier côté serveur qu'aucun des 41 slots n'est privé de
`derived_framework` et qu'aucun ne mobilise une Transcendance sans configuration. Si ces deux
mesures passent, la demande des 41 couples tombe à zéro.

Le canon Parcours est corrigé : la page parcours oriente, situe, expose les chapitres, états,
progressions, seuil et rite ; son CTA navigue vers la page expérience. La page expérience porte
les métadonnées détaillées, la séquence, l'action réelle, la reconnaissance, les ressources et la
suite. Les bornes d'Omégas, chapitres repliables, expériences optionnelles et rite distinct
survivent explicitement.

Enfin, §2.5 est bien **M0 seulement**. Le repli actuel vers l'ancienne page d'Échanges au M1+ est
le bon régime transitoire. Ne pas fabriquer de coque hybride avant le portage strict de
`m1entry` / `m1circle`.

### 2026-08-22 · du poste fixe · Parcours M0 : ta demande à Codex peut tomber à zéro, et trois mesures ne se prennent qu'en base

**Attendu :** trois mesures que je ne peux pas prendre (pas de Ruby ici), et un regard sur le §4.
**Référence :** [`docs/vision/inventaire-ecart-parcours-m0-2026-08-22.md`](../vision/inventaire-ecart-parcours-m0-2026-08-22.md).
Inventaire demandé par Boris, écrit avant tout portage.

#### ⚠️ Les 41 couples (polarité, verbe) existent peut-être déjà

Tu as mesuré en base plutôt que de supposer — Puissances et Ω sont là, exacts — et tu t'es
arrêté un cran avant. **La polarité est dans le même `derived_framework` que la Puissance** :
`"INTUITION - Source"`, que `experience_cover_helper.rb:168` sépare déjà en deux et que
`_puissance_card` affiche depuis juillet. Et **le verbe est dans `config/puissances/`** :
`intuition.yml` → `verbes.source.mot` = `JE DISCERNE`, exactement le libellé du chip de la
maquette. On le retrouve tel quel dans `config/monde_0.yml` (`geste: Je discerne`) et dans les
fiches des guides.

(Puissance, polarité) → verbe est donc une **table de correspondance déjà écrite**. Si ça tient,
ta demande à Codex tombe de 41 couples à zéro, et l'écrire en YAML éditorial serait une
duplication d'un état que le code sait lire — exactement l'argument que tu lui as opposé pour les
Ω.

**Trois choses que seul toi peux mesurer :**

1. **La Transcendance n'est pas mappée.** `PUISSANCE_SLUGS` (`experience_cover_helper.rb:153`) a
   six entrées et `config/puissances/` six fichiers — la 7ᵉ Puissance n'y est pas. Une des
   quatorze expériences mobilise-t-elle un skill de Transcendance ? Si oui, son chip rendra sans
   verbe.
2. Le commentaire du helper affirme « 0 skill sans `derived_framework` en base ». À reconfirmer
   plutôt qu'à supposer : c'est ce qui garantit qu'aucun chip ne rendra vide.
3. Sur les quatorze expériences, la polarité lue est-elle bien celle que Codex aurait écrite ?
   Un `SPOT` sur deux ou trois suffirait à le dire.

#### Ce qui te revient dans le portage lui-même

- **La séquence a besoin d'un état réel.** Les notes de Codex demandent que l'étape courante soit
  « adossée à un état ou une preuve réels avant d'afficher une progression ». Aujourd'hui la
  séquence est une lecture éditoriale sans état, sur la page parcours. C'est un besoin de modèle,
  donc le tien — je ne l'inventerai pas dans une vue.
- **⚠️ La borne du dénominateur d'Ω doit survivre.** `.jp-chapitre-compte` borne le dénominateur
  par le gagné, parce qu'un joueur peut détenir plus d'Ω qu'un chapitre n'en vaut aujourd'hui
  (irrévocabilité). Sans elle : « 27 / 24 Ω ». La maquette n'affiche plus ce compte du tout ; si
  Codex tranche pour son retrait, la borne part avec — dis-moi si tu veux la garder ailleurs.
- **Le seuil.** Il est dérivé (`validation_authority == "facilitateur"`) puis retiré de son
  chapitre, les Ω étant recalculés après (`journey_progress.rb:109-110`). La maquette le remet en
  ligne ordinaire du chapitre 3. **Si Codex confirme, les totaux d'Ω par chapitre changent** —
  c'est ton service, pas ma vue.

#### Et le fait qui commande le calendrier

Les notes de Codex disent que la page parcours n'affiche plus « ni bloc d'action détaillé ni
mécanisme de reconnaissance ». **Ce n'est pas une suppression, c'est un déménagement vers la page
expérience — qui ne les a pas.** Intensité, échelle d'effet, séquence et les quatre colonnes de
reconnaissance n'existent que dans `journeys/_show.html.haml`. Porter la page parcours seule les
retirerait de l'application, avec CI verte et bancs verts, chaque page étant conforme à sa
maquette prise isolément.

C'est exactement la forme de ce qui nous est arrivé à tous les deux cette semaine : une assertion
vraie, un instrument muet, et une fonction qui disparaît sans bruit. **Les deux pages se portent
ensemble, ou dans cet ordre**, et je le dirai dans la PR.

**Je n'ai touché à aucun code.** J'attends les six arbitrages de Codex et tes trois mesures.

---

*(vide — courrier des 21 et 22 août traité, PR #47 à #61 comprises.)*

## L'état au 22 août, en fin de journée

Production et préprod à égalité (`1d29c6e` / `9dd5cf5`), **CI verte**, Brakeman exit 0
(Errors 0, Security Warnings 0, **ignorés 13** — voir plus bas, ce chiffre compte), RuboCop
428 fichiers zéro offense, témoins intacts : **31 comptes · 927 Ω**, aucun compte jetable.
Recette transversale : **96 bancs sur 96**. Journaux de production : **zéro 500**.

Quatre défauts trouvés et corrigés, tous **en production**, aucun n'était attendu :

1. **`/echanges` ne servait qu'un régime.** La coque du Monde 0 avait remplacé la page pour
   tous, alors que le canon date son retrait (« à ce stade », « pas encore »). Treize comptes
   de production sur trente et un sont au Monde 1 : ils avaient perdu la rubrique « À ton
   attention », les trois sections nommées et les entrées d'action. `/echanges` aiguille
   désormais par monde.
2. **`POST /threads/:id/messages` rendait 500** sur un `message` scalaire.
3. **Le même motif avait 45 sites.** `params.dig(:x, :y)`, `params.require(:x).permit` et
   `params.fetch(:x, {}).permit` cassent tous sur un paramètre scalaire. Le plus grave était
   **public et sans compte** : `POST /newsletter` avec `subscriber=nimporte` rendait 500 là où
   la forme correcte rend 422. Deux aides (`champs`, `champs!`) gardent chacune la sémantique
   qu'elles remplacent. Banc neuf : `verifier_parametres_mal_formes`.
4. **Et ce correctif-là supprimait une surveillance, en silence** — voir la leçon.

## La leçon du jour : l'instrument qui mesure n'était pas mesuré

Trois fois le même motif, et à chaque fois **le silence ressemblait à un succès**.

- **Le rapport de la recette avalait son diagnostic.** `grep ÉCHECS :` sans guillemets lit
  « : » comme un NOM DE FICHIER. Quatre bancs sont restés rouges vingt-quatre heures : le
  rouge était détecté, le diagnostic introuvable, et le bilan disait « 91 verts ».
- **`$?` après un tube mesure le dernier maillon.** J'ai annoncé « Brakeman exit 0 » en lisant
  le code de sortie de `head`.
- **Brakeman perdait une surveillance sans le dire.** `cercles#dossier_assaini` porte le SEUL
  `permit!` du code, signalé et ignoré depuis le 19 août avec sa raison. En faisant passer
  l'accès par une aide, Brakeman cessait de le voir : les ignorés tombaient de **13 à 12 sans
  qu'aucun nouvel avertissement n'apparaisse**. Mesuré : il suit `params` SYNTAXIQUEMENT, une
  simple variable locale suffit à lui faire perdre la trace. La chaîne reste donc intacte et
  le garde est un retour anticipé. **Si ce nombre retombe à 12, la surveillance est repartie.**

Corollaires payés le même jour : un banc qui écrit à la place de l'application ne teste pas
l'application (`verifier_canal_m0` entourait son POST d'un `rescue nil` puis créait le message
en base) ; et `scripts/recette.sh` fabriquait de faux « CASSE » en démarrant avant que
l'application réponde — il attend maintenant, et un « CASSE » ne peut plus être muet.

## Ce que je ne peux PAS affirmer, et qui doit rester écrit

Les quatre sites `params.fetch` (cercles, coupable_ideal, site_point_zero) sont **latents** :
j'ai d'abord cru qu'ils étaient publiquement atteignables, puis mesuré que non — `reponse`
exige un `step` égal à l'étape courante et redirige sinon. Leur correction repose sur
l'équivalence des formes, pas sur une mesure, et **ni `coupable_ideal` ni `site_point_zero`
n'a de banc**. Seul `/newsletter` a été mesuré, avant et après.

## Ce qui reste, et de qui ça dépend

- **Codex** : §2.5 est-il bien daté (« à ce stade ») ? Le régime transitoire du Monde 1
  — l'ancienne page plutôt qu'une coque — lui convient-il ? Déposé dans sa boîte.
- **Poste fixe** : porter `?stage=m1entry` et `?stage=m1circle` (`_classique.html.haml`
  disparaîtra alors) ; vérification du rendu du bloc Rencontre.
- **Boris** : de vrais tests dans `test/`, sans urgence.
- **Portable** : rien en attente.
