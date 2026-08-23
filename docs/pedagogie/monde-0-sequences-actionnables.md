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

#### 1. Choisir — Prends position dans l'époque · 12 min

- **Accroche :** Tes choix racontent déjà une manière de voir le monde.
- **Explication :** Traverse les situations proposées et choisis les réponses qui te ressemblent
  aujourd'hui. Ne cherche pas la bonne réponse : le jeu a besoin de ton mouvement réel.
- **CTA :** `Entrer dans les situations`
- **Sortie attendue :** série de choix achevée.
- **Reconnaissance :** événements intermédiaires à ajouter ; la preuve finale existe déjà.

#### 2. Rencontrer — Laisse revenir le mouvement inverse · 5 min

- **Accroche :** Ce que tu écartes continue d'agir.
- **Explication :** Découvre la polarité que tes réponses ont laissée dans l'ombre. Observe ce
  qu'elle pourrait rendre à ton regard si elle cessait d'être un adversaire.
- **CTA :** `Découvrir le mouvement inverse`
- **Sortie attendue :** miroir de polarité affiché.
- **Reconnaissance :** événement d'affichage du résultat à ajouter ; confirmation en repli.

#### 3. Lire — Ton premier miroir · 3 min

- **Accroche :** Regarde une posture, pas une identité.
- **Explication :** Lis le miroir proposé et choisis ce que tu souhaites en garder. Il décrit une
  manière ponctuelle de traverser l'époque et pourra évoluer avec toi.
- **CTA :** `Conserver mon premier miroir`
- **Sortie attendue :** résultat du mini-jeu conservé comme Trace.
- **Reconnaissance :** preuve serveur existante à la complétion du mini-jeu.

### 4. Avant le Zéro — 15 min

#### 1. Entrer — Traverse la dispersion · 6 min

- **Accroche :** Entre dans un monde qui a perdu son centre.
- **Explication :** Parcours les fragments proposés et observe comment des récits séparés
  organisent le réel. Laisse-toi d'abord affecter avant de chercher une explication.
- **CTA :** `Entrer dans l'expérience`
- **Sortie attendue :** première phase du mini-jeu parcourue.
- **Reconnaissance :** événement de phase à ajouter ; confirmation en repli.

#### 2. Traverser — Suis un devenir possible · 6 min

- **Accroche :** Une époque devient ce qu'elle répète.
- **Explication :** Choisis un chemin parmi les devenirs proposés et observe la logique qui le
  rend possible. Tu suis un récit jusqu'à ses conséquences.
- **CTA :** `Choisir un devenir`
- **Sortie attendue :** chemin parcouru jusqu'à son issue.
- **Reconnaissance :** événement de phase à ajouter ; la preuve finale existe déjà.

#### 3. Revenir — Rapporte une Trace du passage · 3 min

- **Accroche :** Reviens avec ce que tu ne peux plus ne pas voir.
- **Explication :** Choisis l'image, la phrase ou la tension qui résume le mieux ta traversée.
  Elle rejoint tes Traces et pourra nourrir une future Graine.
- **CTA :** `Conserver ma Trace`
- **Sortie attendue :** résultat de l'expérience enregistré.
- **Reconnaissance :** preuve serveur existante à la fin du mini-jeu.

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

- **Accroche :** Le Point Zéro n'est pas un programme : c'est un écosystème.
- **Explication :** Explore les grandes fonctions qui relient le Jeu, les Cercles, les ressources
  et les projets. Cherche les circulations plutôt qu'un organigramme.
- **CTA :** `Découvrir la constellation`
- **Sortie attendue :** carte de l'écosystème ouverte.
- **Reconnaissance :** événement d'ouverture à ajouter ; confirmation en repli.

#### 2. Relier — Recompose trois fragments · 2 min

- **Accroche :** Retrouve ce qui nourrit quoi.
- **Explication :** Relie trois éléments de l'écosystème et observe ce qui circule entre eux :
  apprentissage, récit, attention, ressources ou capacité d'agir.
- **CTA :** `Relier les fragments`
- **Sortie attendue :** exercice de mise en relation achevé.
- **Reconnaissance :** preuve serveur existante via l'adaptateur.

#### 3. Produire — Ton Schéma de circulation · 1 min

- **Accroche :** Dessine le mouvement que tu as compris.
- **Explication :** Choisis le circuit qui te paraît aujourd'hui le plus vivant. Ce premier
  schéma reste provisoire et rejoint tes Traces.
- **CTA :** `Conserver mon schéma`
- **Sortie attendue :** schéma choisi et enregistré comme Trace.
- **Reconnaissance :** événement d'enregistrement à ajouter ; confirmation en repli.

### 7. Le site du Point Zéro — 30 min

#### 1. Explorer — Choisis un chemin dans le site · 18 min

- **Accroche :** Entre dans la profondeur sans chercher à tout lire.
- **Explication :** Parcours les contenus proposés et suis les liens qui déplacent réellement ton
  regard. Le Jeu conserve les pages visitées dans ce parcours, pas ton activité générale.
- **CTA :** `Explorer le site`
- **Sortie attendue :** parcours thématique achevé ou pages requises consultées.
- **Reconnaissance :** événements de navigation à relier ; confirmation en repli.

#### 2. Éprouver — Vérifie ce que tu as réellement compris · 7 min

- **Accroche :** Fais passer les idées par tes propres mots.
- **Explication :** Réponds au questionnaire d'appropriation. Il ne mesure pas une culture du Point
  Zéro : il révèle les notions qui demandent encore à être reliées.
- **CTA :** `Répondre au questionnaire`
- **Sortie attendue :** questionnaire achevé et résultat enregistré.
- **Reconnaissance :** preuve serveur existante via l'adaptateur.

#### 3. Cartographier — Garde deux résonances · 5 min

- **Accroche :** Choisis deux idées qui continueront de travailler en toi.
- **Explication :** Sélectionne une idée qui t'ouvre et une idée qui te résiste. Ensemble, elles
  forment une petite carte de ton exploration.
- **CTA :** `Conserver mes deux résonances`
- **Sortie attendue :** deux résonances enregistrées comme Trace.
- **Reconnaissance :** événement d'enregistrement à ajouter ; confirmation en repli.

### 8. Le signe de reconnaissance — 15 min

#### 1. Choisir — Fais apparaître une relation · 3 min

- **Accroche :** Pense à quelqu'un dont le geste mérite d'être vu.
- **Explication :** Choisis une relation réelle et nomme ce que cette personne a rendu possible
  pour toi, pour d'autres ou pour un projet.
- **CTA :** `Choisir une personne`
- **Sortie attendue :** destinataire ou relation désignée, sans envoi automatique.
- **Reconnaissance :** événement de sélection à ajouter ; confirmation en repli.

#### 2. Composer — Écris un signe qui reconnaît précisément · 7 min

- **Accroche :** Reconnais un acte, pas une étiquette.
- **Explication :** Compose un message bref qui nomme le geste observé, son effet et ce qu'il a
  éveillé. La précision donne sa force au signe.
- **CTA :** `Composer mon signe`
- **Sortie attendue :** message rédigé et conservé en brouillon.
- **Reconnaissance :** événement de brouillon à ajouter ; confirmation en repli.

#### 3. Décider — Choisis le destin de ton signe · 5 min

- **Accroche :** Envoie-le, change de canal ou garde-le pour toi.
- **Explication :** Décide librement de transmettre ce signe dans l'application, par un autre
  moyen, ou de le conserver. Le choix du canal fait partie du geste.
- **CTA :** `Choisir comment le transmettre`
- **Sortie attendue :** décision enregistrée ; l'envoi reste facultatif.
- **Reconnaissance :** preuve serveur existante sur l'achèvement du dispositif, sans exiger
  l'envoi.

### 9. Les choses se précisent — 30 min

#### 1. Relire — Observe la constellation qui se dessine · 5 min

- **Accroche :** Tes rencontres possibles ne viennent pas de nulle part.
- **Explication :** Relis ton Schéma de circulation, ton signe et les résonances déjà conservées.
  Repère la relation qui pourrait soutenir le prochain mouvement.
- **CTA :** `Relire ma constellation`
- **Sortie attendue :** éléments transmis au dialogue avec le mentor.
- **Reconnaissance :** événement de sélection à ajouter ; confirmation en repli.

#### 2. Nommer — Explore une relation possible avec ton mentor · 20 min

- **Accroche :** Donne un visage au collectif qui pourrait te soutenir.
- **Explication :** Dialogue avec ton mentor sur une personne, un cercle ou une communauté que tu
  pourrais rejoindre, soutenir ou inviter dans ton mouvement.
- **CTA :** `Explorer cette relation avec mon mentor`
- **Sortie attendue :** échange rattaché à la thématique `Graine`.
- **Reconnaissance :** preuve à ajouter sur le dialogue thématique ; confirmation en repli.

#### 3. Semer — La Graine de relation · 5 min

- **Accroche :** Formule le lien que tu souhaites rendre possible.
- **Explication :** Écris une Graine qui nomme la qualité de relation recherchée et le premier
  geste que tu peux poser sans attendre l'autre.
- **CTA :** `Planter ma Graine de relation`
- **Sortie attendue :** Graine enregistrée dans la Fresque.
- **Reconnaissance :** preuve à relier à la création de la Graine attendue.

### 10. Le Conseil Oméga — 25 min

#### 1. Être convoqué — Entre dans le Conseil · 3 min

- **Accroche :** Le futur te demande de prendre place.
- **Explication :** Entre dans la scène du Conseil Oméga et découvre les tensions qui traversent
  la décision. Tu n'es pas invité à commenter le monde, mais à y tenir une fonction.
- **CTA :** `Entrer dans le Conseil`
- **Sortie attendue :** introduction du mini-jeu traversée.
- **Reconnaissance :** événement de phase à ajouter ; confirmation en repli.

#### 2. Arbitrer — Choisis entre plusieurs futurs incomplets · 17 min

- **Accroche :** Aucun futur ne sauvera toutes les polarités à ta place.
- **Explication :** Examine les scénarios et arbitre les tensions qu'ils révèlent. Tes décisions
  font apparaître les fonctions de civilisation que tu es prêt à servir.
- **CTA :** `Participer aux arbitrages`
- **Sortie attendue :** série d'arbitrages achevée.
- **Reconnaissance :** événements intermédiaires à ajouter ; la preuve finale existe déjà.

#### 3. Signer — Ton Rôle d'appel et tes caps · 5 min

- **Accroche :** Sors du Conseil avec une fonction à éprouver.
- **Explication :** Découvre le métier ou rôle Oméga proposé, ajuste les caps associés et signe-le
  comme une hypothèse d'action. Il préfigure une responsabilité possible, pas une identité figée.
- **CTA :** `Signer mon Rôle d'appel`
- **Sortie attendue :** rôle et caps conservés comme Trace.
- **Reconnaissance :** preuve serveur existante à la fin du mini-jeu.

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

### 12. Le Sas d'entrée — 1 h · facultative

#### 1. Se présenter — Entre dans la rencontre · 10 min

- **Accroche :** Arrive avec ce qui est vivant pour toi aujourd'hui.
- **Explication :** Inscris-toi, rejoins le Sas et présente en quelques mots ce qui t'amène. Tu
  n'as pas à résumer ton parcours ni à produire une identité parfaite.
- **CTA :** `Rejoindre le Sas`
- **Sortie attendue :** inscription puis présence à la rencontre.
- **Reconnaissance :** inscription ou présence à relier ; confirmation du Joueur en repli.

#### 2. Éprouver — Fais l'expérience d'une première rencontre · 35 min

- **Accroche :** Laisse le collectif déplacer légèrement ton regard.
- **Explication :** Participe aux échanges et aux pratiques proposées. Observe ce qui devient plus
  clair, plus vivant ou plus inconfortable au contact des autres.
- **CTA :** `Ouvrir les repères du Sas`
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

#### 1. Explorer — Compose avec plusieurs futurs · 45 min

- **Accroche :** Entre dans les futurs avant de choisir celui qui te rassure.
- **Explication :** Traverse les scénarios proposés avec le groupe et observe les forces qu'ils
  libèrent, les peurs qu'ils réveillent et les impensés qu'ils transportent.
- **CTA :** `Préparer l'Atelier`
- **Sortie attendue :** préparation consultée puis participation à la première séquence.
- **Reconnaissance :** facilitateur et présence ; aucune preuve automatique par geste aujourd'hui.

#### 2. Reconnaître — Retrouve le système en toi · 1 h 30

- **Accroche :** Le monde que tu veux transformer traverse aussi ton Moteur.
- **Explication :** Participe aux pratiques de l'Atelier et observe comment les polarités
  collectives se rejouent dans tes propres manières de décider, créer, ressentir, t'exprimer et
  discerner.
- **CTA :** `Voir le cadre de l'Atelier`
- **Sortie attendue :** participation à la séquence centrale.
- **Reconnaissance :** facilitateur et présence ; confirmation du Joueur en repli d'affichage.

#### 3. Franchir — Passe le seuil en Cercle · 45 min

- **Accroche :** Termine la traversée en présence des autres.
- **Explication :** Prends part au temps de clôture, partage ce que tu choisis de rendre visible et
  formule l'engagement minimal avec lequel tu repars.
- **CTA :** `Retrouver les informations de l'Atelier`
- **Sortie attendue :** Atelier achevé et présence reconnue par le facilitateur.
- **Reconnaissance :** autorité du facilitateur ; elle valide l'expérience entière.

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

> Ta roue est conservée dans tes Traces. Aucune phrase n'a été gardée pour ta Graine.

### 6.2. Correspondance entre les quatre quiz et les trois gestes

Les quatre quiz couvrent entièrement leur expérience. Leur achèvement peut donc prouver les
trois gestes. Lorsqu'un état intermédiaire persistant est disponible, la correspondance est :

| Expérience | Geste 1 | Geste 2 | Geste 3 |
|---|---|---|---|
| L'écosystème Point Zéro | Découvrir : `mission`, `fragments` | Relier : `liens`, `manque` | Produire : `schema` |
| Le site du Point Zéro | Explorer : `mission`, `repere_1`, `repere_2` | Éprouver : `langage`, `feedback`, `geste` | Cartographier : `produire`, `carte` |
| Le signe de reconnaissance | Choisir : `mission`, `situation` | Composer : `composition` | Décider : `envoi`, `signe` |
| Découvrir les formats | Clarifier : `mission`, `intention` | Comparer : `format`, `geste` | Produire : `boussole` |

Si le moteur n'expose que `completed`, il ne prétend pas connaître un geste courant : la preuve
globale confirme les trois gestes ensemble. Aucun état intermédiaire n'est déduit de la seule
ouverture du quiz.

### 6.3. Destinations des six CTA encore sans porte

| Expérience · geste | Arbitrage V1 | Condition de mise en oeuvre |
|---|---|---|
| Les choses se précisent · Relire | `/mes-traces` | La constellation est composée de productions déjà conservées. Un filtre ou une ancre pourra préciser cette vue plus tard. |
| Le Sas d'entrée · Ouvrir les repères | À construire sur `/sas/:slug` | Le Sas doit être relié à l'expérience ou à l'inscription du Joueur. Aucun slug n'est codé en dur. |
| Le Sas d'entrée · Conserver mon intention | À construire comme saisie intégrée | L'intention est enregistrée comme Trace ; ce geste n'est pas réduit à une confirmation déclarative. |
| Vivre l'Atelier · les trois gestes | À construire sur la fiche de l'Atelier lié | L'expérience doit résoudre l'événement et l'atelier depuis une association ou une configuration canonique. Aucun identifiant courant n'est codé en dur. |

Tant que les associations métier manquent, les cinq CTA marqués « à construire » restent absents.
La présence ou le facilitateur reconnaît l'expérience Atelier ; la consultation de sa fiche ne la
valide pas.

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
