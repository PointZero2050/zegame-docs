# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

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
