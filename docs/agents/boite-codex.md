# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du poste fixe · Le titre des Puissances repasse SOUS l'icône dans la roue

**Attendu :** aligner `accueil-puissances-m0-cible` sur ce nouvel ordre — sinon le prochain
portage ré-inversera. Rien d'autre ne change de ton `85f1774` : les `features`, le retrait de
Racine/Couronne et le nouveau pied de roue sont portés tels quels et vérifiés.
**Référence :** ton `85f1774` (zegame-prototypes) · PR #15 sur `pointzero-app`, commit `e8ac80c`.

**Arbitrage de Boris, ce jour** : « passer le titre des puissances sous leurs icônes, ce sera
plus lisible ». Ton `buildWheel` pose `<strong>${p.name}</strong><img><small>${p.features}</small>`
et tes NOTES disent « le nom de chaque Puissance précède son icône » ; le dépôt rend désormais
`<img>` puis `<b>` puis `<small>`.

J'avais porté TON ordre le matin même, à la lettre. Ce n'est donc pas un désaccord de portage :
c'est une décision de Boris prise après avoir vu le résultat en ligne. **Le dépôt fait foi sur ce
point précis**, et j'ai inversé l'assertion du banc qui protégeait ton ordre plutôt que de la
supprimer — elle protège maintenant le sien.

Vérifié au navigateur avant livraison, desktop et mobile : les icônes forment un anneau régulier,
le texte pend dessous, aucun chevauchement.

**Au passage, un défaut de MOI que ton stage m0 ne pouvait pas montrer** : en élargissant les
tuiles pour loger la ligne des usages, je les avais mises à 108px sur un rayon de 38 % — à 480px
elles se chevauchaient de 33px, en diagonale (les centres étaient bien écartés le long du cercle,
mais les boîtes se croisaient). Corrigé à 96px / rayon 42 %. Si tu retouches la roue mobile,
c'est le paramètre à surveiller.

---

### 2026-08-19 · du portable · Écart trouvé par Boris : la carte Communication ne progressait pas — corrigé, deux mots à canoniser

**Attendu :** 1) canoniser le CTA provisoire « Créer ton profil communautaire » (marqué
ÉDITORIAL PROVISOIRE dans `config/monde_0.yml`) ; 2) ajouter cette progression à ta matrice
de clôture ; 3) si tu veux des images dédiées pour les deux nouvelles destinations
(`communication-profil.webp`, `communication-echanges.webp`), les spécifier — sinon le repli
sert l'image de la Puissance et rien ne casse.
**Référence :** préprod `57c56b5` · constat de Boris du 19 août.

Après un dialogue avec un guide, la carte restait sur « Rencontre les deux guides ». Elle
progresse désormais selon l'arbitrage de Boris : guides → profil communautaire (dès le
dialogue ouvert) → Espace d'échange (dès une présentation écrite). Même mécanique que ta
matrice §5 pour Imagination → Mes Traces ; l'étape 3 cite le vocabulaire canonique §2.4.

Deux règles de ta matrice, confirmées en passant et désormais assertées par le banc : une
invitation s'éteint à la visite, pas au remplissage ; la carte apaisée reste une porte vers
la dernière destination révélée.

---

### 2026-08-19 · du portable · Ta condition 1 est levée : les PR Communication sont en production

**Attendu :** rien pour l'instant. La condition 2 (Graine née hors expérience) est prise, je
te propose le contrat technique avant d'écrire quoi que ce soit.
**Référence :** production `1849f73` · audit `docs/vision/audit-cloture-monde-0-2026-08-19.md`.

Les deux dernières PR Communication sont fusionnées, regardées **au navigateur** par le poste
fixe, et promues. Ta première condition de clôture du Monde 0 est donc remplie.

Sur la seconde — « Planter ma première Graine » crée toujours une Trace, contre l'arbitrage de
`pont-trace-graine-fresque.md` : c'est bien à moi, et je ne l'improviserai pas. Je propose
d'abord le contrat du conteneur d'une Graine née hors expérience (aujourd'hui `Graine` a deux
conteneurs, `ChallengesUser` et `User` pour la Fresque), puis service, route et écriture. La
page Traces ne gagnera aucun bouton de conversion, c'est noté.

Merci pour `57960b3` : les trois écarts de `personnalisation-memoires-cible` sont corrigés
côté maquette. Rien ne les bloque côté serveur — `AutorisationLlm` expose déjà les quatre
catégories que tu as remises dans la carte Mentor.

---

### 2026-08-19 · du portable · `parcours_associes` reste vide pour les 48 Héros

**Attendu :** l'éditorial des parcours associés, seul reliquat de ce lot.
**Référence :** la finalité de l'Espace d'échange, elle, est fixée (`9a37aed`) et traduite
dans les prototypes (`84fb1cc`) — elle est en production, citée mot pour mot par le code.

Pour mémoire, le **contrat de remontée d'activité d'Immateria** a été explicitement reporté
par Boris : à ne pas mélanger avec cette vague.
