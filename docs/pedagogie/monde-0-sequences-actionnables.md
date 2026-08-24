# Monde 0 — séquences actionnables des expériences

> **Canon éditorial — Codex, 23 août 2026.** Ce document complète
> [Monde 0 — puissance, intensité, effet et séquences d'expérience](monde-0-puissance-intensite-effet.md).
> Il donne au bloc d'action de chaque expérience les contenus qui manquaient dans le YAML :
> titre, durée indicative, accroche, explication et CTA. Il fixe également le contrat entre le
> geste visible et sa reconnaissance technique.

## 1. Décision UX : un seul bloc vivant

Les blocs « À quoi t'attendre » et « Rien à faire ici pour l'instant » sont remplacés par une
surface unique, située sous la séquence : **Passage en cours**.

Avant le commencement, elle présente le premier geste. Pendant l'expérience, elle présente
uniquement le geste courant. Après le dernier geste, elle devient **Passage franchi** et ouvre
l'étape suivante.

Le bloc contient toujours, dans cet ordre :

1. `Étape X sur Y` et le verbe de séquence ;
2. un titre court ;
3. deux ou trois phrases expliquant le sens du geste et le résultat attendu ;
4. un CTA décrivant l'action réelle ;
5. une phrase discrète indiquant comment le Jeu reconnaîtra son accomplissement ;
6. si nécessaire, une action secondaire `Vérifier à nouveau`.

Le CTA répété sous les mots-clés rejoint ce bloc ou ouvre la même action. Il n'accomplit jamais
le geste par sa seule activation.

## 2. Contrat de reconnaissance

Il n'existe actuellement aucun état persistant par geste dans `ChallengesUser`. Une expérience
ne connaît que sa réalisation et sa validation globales. La progression visible repose donc sur
la règle suivante :

- **preuve serveur** lorsqu'un état canonique existe : résultat de mini-jeu ou de QCM, Graine,
  inscription, présence, validation du facilitateur ;
- **événement explicite à ajouter** lorsqu'un outil interne peut produire un signal fiable :
  ouverture ou phase achevée d'un mini-jeu, enregistrement d'un brouillon, choix conservé ;
- **confirmation du Joueur en repli V1** lorsque le geste est réel mais non observable : lecture,
  visionnage ou action accomplie hors de l'application.

L'interface distingue les deux résultats :

- `Confirmé par le Jeu` pour une preuve serveur ;
- `Indiqué comme réalisé` pour une confirmation du Joueur.

Une confirmation ne prétend jamais prouver ce qu'elle ne peut pas mesurer. Elle autorise seulement
le passage au geste suivant. La validation de l'expérience et le gain d'Omégas restent gouvernés
par `ExperienceState`, `ChallengesUser` et les callbacks existants.

Au retour d'une action interne ou externe, la page relit l'état serveur à l'affichage et lors de
`visibilitychange`. Le bouton `Vérifier à nouveau` déclenche la même lecture. Le navigateur ne
devient jamais la source de vérité.

### 2.1. Granularité : une étape visible, un CTA

Les trois mouvements constituent un rythme pédagogique fréquent, pas un gabarit obligatoire.
Une expérience peut exposer une, deux ou trois étapes. **Chaque étape visible porte un CTA
unique**, qui ouvre l'action correspondante. Une phase interne ne devient une étape que si elle
réunit ces trois conditions :

1. le Joueur s'interrompt réellement entre les deux phases ;
2. la fiche peut proposer un CTA distinct qui reprend au bon endroit ;
3. une preuve ou un état fiable permet de reconnaître la transition.

Si le dispositif se joue sans interruption, ses mouvements restent nommés **dans** l'étape :
ils ne produisent ni panneaux successifs, ni confirmations déclaratives. Un CTA final qui mène
à l'expérience suivante est une navigation, jamais une étape supplémentaire.

**Exception de navigation — `Les choses se précisent`.** Les liens `Passer à l'étape 2` et
`Passer à l'étape 3` peuvent déplacer l'affichage sans confirmer l'action quittée, valider
l'expérience ni distribuer d'Omégas. Ils sont visuellement secondaires et ne deviennent jamais
la preuve du geste. À l'étape 3, la navigation vers l'expérience suivante n'apparaît qu'après la
preuve serveur de publication de la Graine de relation.

## 3. Matrice éditoriale des étapes

Les durées répartissent la durée réelle de l'expérience afin de donner un ordre de grandeur. Elles
ne constituent ni un chronomètre ni une condition de validation.

### 1. Le Point Zéro : entrer dans le Jeu — 10 min

#### 1. Regarder — La vidéo d'introduction · 4 min

- **Accroche :** Entre immédiatement dans la question.
- **Explication :** Regarde cette courte introduction. Elle relie la crise du monde, la puissance
  des récits et la possibilité d'un Point Zéro intérieur.
- **CTA :** `Regarder l'introduction`
- **Sortie attendue :** la vidéo est ouverte et regardée ; aucune interprétation n'est encore
  demandée.
- **Reconnaissance :** confirmation du Joueur en V1 ; événement de visionnage possible plus tard,
  sans confondre durée lue et attention réelle.

#### 2. Relier — La chaîne invisible · 3 min

- **Accroche :** Relie crise, récit et croyance.
- **Explication :** Réponds à trois questions courtes pour retrouver la chaîne invisible qui va
  du récit collectif à nos choix les plus ordinaires. Tes réponses deviennent une Trace.
- **CTA :** `Répondre au questionnaire`
- **Sortie attendue :** questionnaire achevé et Trace enregistrée.
- **Reconnaissance :** preuve serveur existante via l'adaptateur de l'expérience.

#### 3. Formuler — Ton Hypothèse de seuil · 3 min

- **Accroche :** Donne une première forme à ce qui vient de bouger.
- **Explication :** Complète la phrase : « Et si ce que nous appelons crise était en réalité… ».
  Cette hypothèse n'est pas une conclusion : c'est la première balise de ton voyage.
- **CTA :** `Conserver mon Hypothèse`
- **Sortie attendue :** texte conservé comme Trace personnelle.
- **Reconnaissance :** événement d'enregistrement à ajouter ; confirmation du Joueur en repli.

### 2. Le Coupable idéal — 10 min

#### Étape unique — Traverser le procès · 10 min

- **Accroche :** Qui a cassé le monde ?
- **Explication :** Traverse le procès d'un seul mouvement. Accuse d'abord les forces que tu tiens
  spontanément pour responsables. Écoute ensuite ce que chacune protège encore, puis rends un
  verdict qui nomme sa charge destructive sans mutiler la puissance qu'elle contient.
- **CTA :** `Ouvrir le procès`, remplacé par `Reprendre le procès` lorsqu'une session est en cours.
- **Sortie attendue :** procès achevé et verdict conservé comme Trace.
- **Reconnaissance :** preuve serveur issue de la session achevée et du verdict enregistré. La
  simple ouverture du mini-jeu ne suffit pas. Aucun bouton `Indiquer comme réalisé` n'est affiché.
- **Après validation :** `Revoir ma roue` ou `Voir cette Trace`. Le CTA `Poursuivre vers Une
  drôle d'époque` mène à l'expérience suivante ; il ne constitue pas une seconde étape.

### 3. Une drôle d'époque — 20 min

#### Étape unique — Traverser une drôle d'époque · 20 min

- **Accroche :** Tes choix mettent déjà ton Moteur en mouvement.
- **Explication :** Traverse une semaine de situations ordinaires, donc légèrement explosives.
  Choisis ton premier mouvement, rencontre celui que tu écartes et rejoins le miroir final. La
  semaine se traverse d'un seul élan, jusqu'au premier reflet du Moteur.
- **CTA :** `Traverser Une drôle d'époque`
- **Sortie attendue :** premier miroir atteint et résultat conservé comme Trace.
- **Reconnaissance :** preuve serveur existante à la complétion du mini-jeu. Les états
  intermédiaires peuvent nourrir son affichage et sa reprise, mais ne créent aucune étape visible.

### 4. Avant le Zéro — 15 min

#### Étape unique — Suivre un devenir jusqu'à son terme · 15 min

- **Accroche :** Entre dans un monde qui a perdu son centre et retrouve le chemin du retour.
- **Explication :** Traverse la dispersion, choisis un devenir et suis sa logique jusque dans ses
  conséquences. La fin atteinte devient la Trace de ce passage et rejoint automatiquement ton
  registre.
- **CTA :** `Entrer dans Avant le Zéro`
- **Sortie attendue :** première fin atteinte et devenir rencontré conservé comme Trace.
- **Reconnaissance :** preuve serveur existante lorsque la traversée atteint une fin. Les phases
  `D` et `R*` restent des repères de reprise internes, pas des étapes de la fiche.

### 5. Et moi dans tout ça ? — 20 min

#### 1. Relire — Rassemble ce que l'époque a réveillé · 4 min

- **Accroche :** Tes Traces commencent à former une direction.
- **Explication :** Relis les choix, miroirs et hypothèses produits depuis le début du parcours.
  Sélectionne ce qui continue de vibrer ou de résister.
- **CTA :** `Relire mes Traces`
- **Sortie attendue :** Traces sélectionnées pour le dialogue.
- **Reconnaissance :** événement de sélection à ajouter ; confirmation en repli.

#### 2. Dialoguer — Cherche l'Appel avec ton mentor · 11 min

- **Accroche :** Fais passer les fragments de la collection à la conversation.
- **Explication :** Dialogue avec ton mentor sur ce qui cherche à prendre forme. Il t'aide à
  relier les tensions sans écrire ton récit à ta place.
- **CTA :** `Dialoguer avec mon mentor`
- **Sortie attendue :** échange rattaché à la thématique `Graine`.
- **Reconnaissance :** preuve à ajouter sur le dialogue thématique ; confirmation en repli.

#### 3. Semer — La Graine de l'Appel · 5 min

- **Accroche :** Écris la phrase qui te met en mouvement.
- **Explication :** Relis la proposition née du dialogue, transforme-la si nécessaire et plante
  ta première Graine de l'Appel dans la Fresque. L'éditeur reprend quatre appuis liés au chapitre :
  ce qui s'est fissuré dans ta manière de voir le monde ; ce qui t'appelle maintenant ; la
  croyance que tu as commencé à interroger ; la tension perçue entre ton besoin et celui du
  système.
- **CTA :** `Planter ma Graine de l'Appel`
- **Sortie attendue :** Graine contextualisée enregistrée dans la Fresque, avec provenance
  parcours + chapitre + expérience, puis retour automatique à cette page d'expérience.
- **Reconnaissance :** preuve serveur liée à la création effective de cette Graine. Ouvrir la
  Fresque ou l'éditeur ne suffit pas ; le retour révèle la suite seulement quand le listener
  retrouve la Graine attendue.

### 6. L'écosystème Point Zéro — 5 min

#### 1. Découvrir — Entre dans la constellation · 2 min

- **Accroche :** Regarde comment le Jeu, les Cercles, les ressources et les projets se répondent.
- **Explication :** Parcours la présentation de l'écosystème. Cherche ce qui circule entre ses
  éléments plutôt que le bureau où serait rangé l'organigramme définitif.
- **CTA :** `Découvrir la constellation`
- **Sortie attendue :** présentation parcourue jusqu'à son terme.
- **Reconnaissance :** listener du dispositif à son écran de sortie ; aucune confirmation
  déclarative si cet événement est disponible.

#### 2. Relier — Compose ton Schéma de circulation · 3 min

- **Accroche :** Retrouve ce qui nourrit quoi.
- **Explication :** Relie les fragments proposés et fais apparaître le mouvement que tu comprends
  aujourd'hui : apprentissage, récit, attention, ressources ou capacité d'agir. Le schéma produit
  rejoint automatiquement tes Traces.
- **CTA :** `Relier les fragments`
- **Sortie attendue :** exercice achevé et Schéma de circulation enregistré comme Trace.
- **Reconnaissance :** preuve serveur existante à la complétion du dispositif. `Conserver mon
  schéma` disparaît : il ne déclenchait aucune action distincte.

### 7. Le site du Point Zéro — 10 à 50 min

Le lien `Explorer les cinq parcours` reste visible dans les deux états de l'expérience. Chaque
parcours public accompli reconnaît ses propres 5 Ω ; l'expérience du Monde 0 ne les attribue pas
une seconde fois.

#### 1. Explorer — Entre par l'une des cinq questions · 10 min minimum

- **Accroche :** Cinq questions ouvrent cinq manières de regarder le basculement.
- **Explication :** Choisis la question qui t'appelle et accomplis au moins un parcours public.
  Tu pourras revenir aux quatre autres quand tu le souhaites ; leur progression reste visible ici.
- **CTA :** `Explorer les cinq parcours`
- **Sortie attendue :** au moins un des cinq parcours publics accompli.
- **Reconnaissance :** présence d'au moins une `TraceSas` importée pour le Joueur. La navigation
  ou la simple ouverture du site ne suffit pas.

#### 2. Situer — Choisis jusqu'où poursuivre · 1 min

- **Accroche :** `X parcours réalisés sur 5.`
- **Explication :** Ton premier passage ouvre la suite du Monde 0. Les autres questions restent
  disponibles : tu peux poursuivre maintenant ou les retrouver plus tard depuis cette page.
- **CTA :** `Passer à l'expérience suivante`
- **Action secondaire permanente :** `Explorer les cinq parcours`
- **Sortie attendue :** expérience reconnue dès l'entrée dans cet état ; le CTA principal est une
  navigation vers l'expérience suivante, pas une nouvelle preuve.
- **Reconnaissance :** le compteur provient exclusivement de `TraceSas.pour(joueur)`.

### 8. Le signe de reconnaissance — 15 min

#### Étape unique — Composer un signe de reconnaissance · 15 min

- **Accroche :** Fais apparaître un geste qui mérite d'être vu.
- **Explication :** Pense à une relation réelle, nomme précisément ce que l'autre a rendu possible
  et compose ton signe. Tu décideras dans le dispositif de l'envoyer, de changer de canal ou de le
  garder pour toi : reconnaître n'oblige pas à publier.
- **CTA :** `Composer mon signe de reconnaissance`
- **Sortie attendue :** signe prêt à envoyer et choix de destination enregistré. L'envoi réel
  reste facultatif.
- **Reconnaissance :** preuve serveur existante à la complétion du dispositif ; ses phases
  `situation`, `composition` et `envoi` ne créent pas trois reprises sur la fiche.

### 9. Les choses se précisent — 30 min

#### 1. Relire — Observe la constellation qui se dessine · 5 min

- **Accroche :** Tes rencontres possibles ne viennent pas de nulle part.
- **Explication :** Relis ton Schéma de circulation, ton signe et les résonances déjà conservées.
  Repère la relation qui pourrait soutenir le prochain mouvement.
- **CTA :** `Relire ma constellation`
- **Navigation secondaire :** `Passer à l'étape 2`
- **Sortie attendue :** éléments transmis au dialogue avec le mentor.
- **Reconnaissance :** événement de sélection à ajouter ; confirmation en repli.

#### 2. Nommer — Explore une relation possible avec ton mentor · 20 min

- **Accroche :** Donne un visage au collectif qui pourrait te soutenir.
- **Explication :** Dialogue avec ton mentor sur une personne, un cercle ou une communauté que tu
  pourrais rejoindre, soutenir ou inviter dans ton mouvement.
- **CTA :** `Explorer cette relation avec mon mentor`
- **Navigation secondaire :** `Passer à l'étape 3`
- **Sortie attendue :** échange rattaché à la thématique `Graine`.
- **Reconnaissance :** preuve à ajouter sur le dialogue thématique ; confirmation en repli.

#### 3. Semer — La Graine de relation · 5 min

- **Accroche :** Formule le lien que tu souhaites rendre possible.
- **Explication :** La popup te propose trois appuis : `La relation que je souhaite rendre
  possible`, `Ce qu'elle rendrait possible` et `Le premier geste que je peux poser`. Compose la
  formulation finale, puis choisis de la publier dans le fil des Graines.
- **CTA :** `Planter ma Graine de relation`
- **Sortie attendue :** Graine publiée dans la Fresque avec la provenance parcours + chapitre +
  expérience, sans changement de page.
- **Reconnaissance :** preuve serveur liée à la création effective de cette Graine. Après sa
  publication, `Passer à l'expérience suivante` apparaît à côté de `Planter ma Graine de
  relation` ; il reste une navigation, pas une seconde reconnaissance.

### 10. Le Conseil Oméga — 25 min

#### Étape unique — Prendre place au Conseil Oméga · 25 min

- **Accroche :** Le futur a laissé une chaise vide. Elle porte ton nom.
- **Explication :** Entre dans le Conseil, arbitre plusieurs futurs incomplets et formule tes caps.
  La restitution fera apparaître un Rôle d'appel à éprouver dans le présent — ainsi qu'une quantité
  raisonnable de paperasse venue de 2040.
- **CTA :** `Entrer dans le Conseil Oméga`
- **Sortie attendue :** restitution finale atteinte, caps conservés et Rôle d'appel choisi ou
  explicitement laissé ouvert.
- **Reconnaissance :** preuve serveur existante à la complétion du Conseil. `TREIZIEME` et
  `cap_desir` restent des bornes internes de reprise, pas des étapes visibles.

### 11. Découvrir les formats — 10 min · facultative

#### 1. Clarifier — De quoi as-tu besoin maintenant ? · 2 min

- **Accroche :** Pars de ton mouvement, pas du catalogue.
- **Explication :** Choisis ce que tu souhaites vivre : comprendre, rencontrer, pratiquer,
  approfondir ou contribuer. Cette intention orientera la comparaison.
- **CTA :** `Préciser mon intention`
- **Sortie attendue :** intention choisie.
- **Reconnaissance :** événement de choix à ajouter ; confirmation en repli.

#### 2. Comparer — Trouve le format qui correspond · 5 min

- **Accroche :** Sas, atelier, formation ou Festival ne font pas vivre la même chose.
- **Explication :** Compare les formats selon leur durée, leur degré de présence et le type de
  rencontre proposé. Ouvre ceux qui répondent le mieux à ton intention.
- **CTA :** `Comparer les formats`
- **Sortie attendue :** formats comparés et au moins une fiche ouverte.
- **Reconnaissance :** événements de consultation à ajouter ; confirmation en repli.

#### 3. Produire — Ta Boussole de passage · 3 min

- **Accroche :** Choisis ton prochain passage possible.
- **Explication :** Conserve un format principal et une alternative. Une inscription réelle pourra
  ensuite confirmer le passage, mais elle n'est pas exigée pour produire la Boussole.
- **CTA :** `Conserver ma Boussole`
- **Sortie attendue :** sélection enregistrée comme Trace.
- **Reconnaissance :** preuve serveur existante via l'adaptateur ; l'inscription réelle peut
  enrichir l'état sans être confondue avec le choix.

### 12. Participer à un Sas Point Zéro — 1 h · facultative

#### 1. Se présenter — Entre dans la rencontre · 10 min

- **Accroche :** Arrive avec ce qui est vivant pour toi aujourd'hui.
- **Explication :** Inscris-toi, rejoins le Sas et présente en quelques mots ce qui t'amène. Tu
  n'as pas à résumer ton parcours ni à produire une identité parfaite.
- **CTA :** `Choisir un Sas`
- **Sortie attendue :** inscription puis présence à la rencontre.
- **Reconnaissance :** inscription ou présence à relier ; confirmation du Joueur en repli.

#### 2. Éprouver — Fais l'expérience d'une première rencontre · 35 min

- **Accroche :** Laisse le collectif déplacer légèrement ton regard.
- **Explication :** Participe aux échanges et aux pratiques proposées. Observe ce qui devient plus
  clair, plus vivant ou plus inconfortable au contact des autres.
- **CTA :** `Vivre la rencontre`
- **Sortie attendue :** participation au temps collectif.
- **Reconnaissance :** présence confirmée par l'événement ou confirmation du Joueur en repli.

#### 3. Clarifier — Formule ton intention de passage · 15 min

- **Accroche :** Repars avec une direction simple.
- **Explication :** À la fin du Sas, écris ce que tu souhaites explorer ensuite et le premier pas
  réaliste que tu peux poser.
- **CTA :** `Conserver mon intention`
- **Sortie attendue :** intention enregistrée comme Trace.
- **Reconnaissance :** événement d'enregistrement à ajouter ; confirmation en repli.

### 13. Vivre l'Atelier Point Zéro — 3 h

#### Étape unique — S'inscrire à un Atelier Point Zéro · 3 h

- **Accroche :** Choisis la date à laquelle les concepts devront supporter la présence de vrais
  humains.
- **Explication :** Consulte les prochains Ateliers, choisis celui qui correspond à tes
  disponibilités et réserve ta place. Une inscription en attente ne suffit pas : le Jeu attend une
  place confirmée.
- **CTA :** `Voir les prochains Ateliers`
- **Sortie attendue :** inscription active à un créneau d'Atelier.
- **Reconnaissance :** preuve serveur sur `InscriptionCreneau.actives`. L'ouverture de l'agenda et
  une inscription placée en liste d'attente ne franchissent pas cette étape.

### 14. Mon récit de passage — 30 min

#### 1. Rassembler — Retrouve les traces de ta traversée · 5 min

- **Accroche :** Regarde le chemin avant d'en faire un récit.
- **Explication :** Rassemble les Traces, Graines, miroirs, résonances et choix qui ont marqué ton
  Monde 0. Sélectionne ce qui porte encore une tension vivante.
- **CTA :** `Rassembler mes traces`
- **Sortie attendue :** éléments choisis pour le dialogue final.
- **Reconnaissance :** événement de sélection à ajouter ; confirmation en repli.

#### 2. Composer — Écris la Graine de passage avec ton mentor · 20 min

- **Accroche :** Relie ce que tu quittes, ce que tu accueilles et ce qui t'appelle.
- **Explication :** Dialogue avec ton mentor, puis compose une Graine qui raconte le déplacement
  réellement vécu. Elle peut contenir une contradiction : le passage n'a pas à devenir une morale.
- **CTA :** `Composer ma Graine de passage`
- **Sortie attendue :** Graine enregistrée dans la Fresque.
- **Reconnaissance :** preuve à relier à la création de la Graine attendue.

#### 3. Sceller — Ta Carte du Seuil · 5 min

- **Accroche :** Donne une forme visible au passage accompli.
- **Explication :** Relis la Graine, choisis les éléments que tu souhaites partager et scelle ta
  Carte du Seuil. Elle rassemble le passage sans exposer ce que tu gardes privé.
- **CTA :** `Sceller ma Carte du Seuil`
- **Sortie attendue :** Carte du Seuil générée et préférences de visibilité enregistrées.
- **Reconnaissance :** événement de génération à ajouter ; la validation globale de l'expérience
  reste distincte.

## 4. Matrice de complétion à vérifier par le portable

Le portage doit établir, pour chaque étape visible, les quatre colonnes suivantes :

| État visible | Source de vérité | Transition | Repli V1 |
|---|---|---|---|
| À accomplir | geste courant résolu côté serveur | CTA ouvre l'action | aucun |
| Action ouverte | événement interne facultatif | retour ou `visibilitychange` relit l'état | retour manuel |
| Confirmé par le Jeu | adaptateur, objet ou autorité canonique | passage automatique au geste suivant | aucun |
| Indiqué comme réalisé | confirmation du Joueur | passage au geste suivant sans valider l'expérience | révocable avant validation globale |
| En attente de reconnaissance | action achevée mais autorité externe requise | callback, synchronisation ou facilitateur | `Vérifier à nouveau` |

Les neuf adaptateurs existants ne couvrent aujourd'hui qu'un geste final ou central :

- `le-point-zero-entrer-dans-le-jeu` ;
- `le-coupable-ideal` ;
- `une-drole-d-epoque` ;
- `avant-le-zero` ;
- `l-ecosysteme-point-zero` ;
- `le-site-du-point-zero` ;
- `le-signe-de-reconnaissance` ;
- `le-conseil-omega` ;
- `decouvrir-les-formats`.

Les cinq expériences suivantes exigent donc au minimum un état déclaré pour rendre la séquence
progressive avant la création de nouvelles preuves :

- `et-moi-dans-tout-ca` ;
- `les-choses-se-precisent` ;
- `le-sas-d-entree` ;
- `vivre-l-atelier` ;
- `mon-recit-de-passage`.

## 5. Critères de recette

1. Une seule surface décrit le geste courant et porte son CTA.
2. Le CTA nomme toujours l'action réelle ; aucun `Valider` générique.
3. Ouvrir un CTA ne marque jamais automatiquement le geste comme accompli.
4. Une preuve serveur fait avancer la séquence après relecture de l'état.
5. Sans preuve, le Joueur peut indiquer le geste comme réalisé et voit clairement la nature
   déclarative de cet état.
6. La dernière étape ne valide l'expérience que si l'autorité canonique l'autorise.
7. Aucun état de geste ne crée, ne retire ou ne recalcule des Omégas.
8. Le rejeu d'une expérience ne révoque aucun Oméga acquis.
9. L'étape suivante du parcours ne s'ouvre qu'après la validation globale de l'expérience.
10. Sur mobile, le CTA et l'état de reconnaissance restent visibles sans faire défiler un bloc vide.

## 6. Arbitrages de raccordement du 23 août 2026

> Ajout Codex - 2026-08-23. Ces décisions ferment les écarts constatés pendant la traversée
> réelle du parcours. Elles n'autorisent ni URL d'événement codée en dur, ni progression fictive.

### 6.1. Une production de mini-jeu reste une Trace, même sans phrase pour la Graine

Dans les restitutions qui proposent de garder une phrase pour une future Graine :

- le bouton de renoncement s'appelle `Passer` ;
- la production structurée du mini-jeu rejoint toujours les Traces ;
- la confirmation distingue explicitement les deux objets :

Le nom de la production suit ce que l'écran montre réellement : `carte` en V1, `roue` en V2.

Si aucune phrase n'est retenue :

> Ta carte est conservée dans tes Traces. Tu n'as gardé aucune phrase pour une future Graine.

Si une phrase est retenue :

> Ta carte est conservée dans tes Traces. La phrase que tu as choisie reste disponible pour nourrir une prochaine Graine.

Ces formulations ne prétendent jamais qu'une Graine existe déjà. La production structurée et la
phrase retenue restent deux objets distincts.

### 6.2. Correspondance avec les dispositifs internes

Les quatre dispositifs couvrent entièrement leur expérience. Leur achèvement prouve la sortie
attendue sans ajouter de confirmation déclarative. Depuis l'arbitrage du 24 août, les phases
internes ne déterminent plus nécessairement le nombre d'étapes visibles :

| Expérience | Étapes visibles | Preuve canonique |
|---|---:|---|
| L'écosystème Point Zéro | 2 | sortie de la présentation, puis complétion du dispositif et `schema` conservé automatiquement |
| Le site du Point Zéro | 2 | au moins une `TraceSas`, puis état de restitution `X parcours réalisés sur 5` |
| Le signe de reconnaissance | 1 | dispositif achevé avec `signe` prêt et décision de destination |
| Découvrir les formats | 3 | phases `intention`, `format` puis `boussole` conservées |

Si le moteur n'expose que `completed`, il ne prétend pas connaître une phase courante. Aucun état
intermédiaire n'est déduit de la seule ouverture du dispositif.

### 6.3. Destinations des six CTA encore sans porte

| Expérience · geste | Arbitrage V1 | Condition de mise en oeuvre |
|---|---|---|
| Les choses se précisent · Relire | `/mes-traces` | La constellation est composée de productions déjà conservées. Un filtre ou une ancre pourra préciser cette vue plus tard. |
| Sas Point Zéro · Choisir un Sas | Agenda filtré sur les rencontres Sas Point Zéro | L'événement doit être associé canoniquement à l'expérience. `/sas` et `/sas/:slug` désignent les parcours publics du site et ne sont jamais utilisés ici. |
| Sas Point Zéro · Conserver mon intention | À construire comme saisie intégrée | L'intention est enregistrée comme Trace ; ce geste n'est pas réduit à une confirmation déclarative. |
| Vivre l'Atelier · étape unique | Agenda filtré sur les Ateliers Point Zéro | L'expérience résout le créneau depuis les données d'événement, sans identifiant codé en dur ; une `InscriptionCreneau.active` est la preuve. |

Tant que les associations métier manquent, les CTA marqués « à construire » restent absents. La
consultation d'une fiche d'Atelier ne valide rien ; seule une inscription active reconnaît
l'étape visible.

### 6.4. Granularité de progression

Les textes détaillés des étapes figurent dans les sections 3.1 à 3.14 de cette spécification :
durée, accroche, explication, CTA, sortie attendue et reconnaissance. Ils constituent la source
éditoriale à verser dans la configuration applicative.

La progression suit une règle hybride :

1. une preuve serveur fait avancer le geste lorsqu'elle existe ;
2. sinon le Joueur peut indiquer le geste comme réalisé ;
3. l'interface distingue une réalisation déclarée d'une reconnaissance par le Jeu ;
4. aucun simple clic d'ouverture ne fait avancer la séquence ;
5. la validation globale de l'expérience et l'attribution des Omégas restent indépendantes.

Un état persistant par geste est donc légitime pour porter cette séquence, mais il ne constitue
jamais une seconde validation de l'expérience.

### 6.5. Nom de la famille issue du retour du Joueur

La famille actuellement appelée `Retours reçus` contient les réponses que le Joueur rédige après
une expérience (`retour_apprecie`, `retour_appris`, `retour_manque`). Elle devient
**Bilans d'expérience**. Le terme `Retours reçus` est réservé à un futur contenu effectivement
produit par un pair, un mentor ou un facilitateur.

### 6.6. Correspondance entre les quatre mini-jeux narratifs et les étapes visibles

La règle reste : **une étape visible = un CTA réel et une reprise distincte**. Les mini-jeux
exposent plusieurs bornes persistées, mais le Joueur les traverse sur une surface continue. Ces
bornes servent à reprendre, analyser et reconnaître le terme du jeu ; elles ne produisent plus de
panneaux successifs sur la fiche.

| Expérience | Étape visible unique | Preuve de sortie ; bornes internes conservées |
|---|---|---|
| Le Coupable idéal | **Traverser le procès** | restitution complète ; `current_step` reste interne |
| Une drôle d'époque | **Traverser une drôle d'époque** | miroir atteint et passation complétée ; `jour_1_e2` et `jour_1_e4` restent des bornes internes |
| Avant le Zéro | **Suivre un devenir jusqu'à son terme** | première fin atteinte ; `D` et `R*` restent des bornes internes |
| Le Conseil Oméga | **Prendre place au Conseil Oméga** | restitution finale, caps et Rôle d'appel ; `TREIZIEME` et `cap_desir` restent des bornes internes |

Pour `Avant le Zéro`, atteindre une fin est la preuve du retour : aucune question artificielle
n'est ajoutée après la fiction. Pour le Conseil, l'ancien champ `posture_cible` reste lisible
comme donnée historique mais ne remplace pas le Rôle d'appel dans le nouveau rite.

### 6.7. Voix narrative du parcours

Les cinq états calculés par `JourneyProgress` reçoivent les textes suivants. Les nombres restent
dans la phrase : ils renseignent la traversée sans transformer l'en-tête en tableau de bord.

| Clé | Texte canonique |
|---|---|
| `depart` | `Le seuil est devant toi. %{total} expériences composent ce voyage ; la première attend ton geste.` |
| `en_chemin` | `Tu as traversé %{faits} expériences sur %{total}. %{restants} passages restent ouverts, avec %{omega_restants} Omégas encore accessibles.` |
| `courant` | `Tu avances dans le chapitre en cours : %{faits} expériences sur %{total} sont traversées et %{omega_gagnes} Omégas portent déjà la trace de ton chemin.` |
| `dernier_chapitre` | `Le dernier chapitre est ouvert. %{restants} passages te séparent encore de la clôture de ce voyage.` |
| `seuil_ouvert` | `Le parcours est accompli. Le seuil suivant est ouvert ; ce que tu en fais t'appartient.` |

### 6.8. Deux règles d'affichage des Puissances

- Une même Puissance peut apparaître deux fois si deux polarités distinctes sont réellement
  mobilisées. Dans `Mon récit de passage`, Communication reste donc visible en Ombre et en
  Lumière : deux polarités, deux verbes, deux lignes lisibles.
- Une attribution de `0 Ω` n'apparaît pas dans la ventilation des Omégas. La Puissance peut rester
  visible dans la liste des capacités mobilisées, sans badge `0 Ω` : les Omégas racontent une
  valeur reconnue, pas un tableau de zéros.

### 6.9. Bloc éditorial de reconnaissance

Le bloc libre historiquement nommé `validations` reste **sans titre**. Il suit directement le
contenu de l'expérience. Un intitulé générique réintroduirait une explication redondante avec la
séquence vivante et son texte de reconnaissance contextuel.
