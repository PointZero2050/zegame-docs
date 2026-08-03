# Le parcours qui n'existe pas — spécification du parcours caché

> **Ajout Codex — 2026-08-03 · Recommandation éditoriale, UX et IA à destination de Claude.**
>
> **Statut** : le nom du parcours, son caractère caché, le dialogue avec une IA et le badge
> **Patient Z.E.R.O.** viennent des arbitrages de Boris. Les conditions de révélation, le
> storyboard, le contrat de données et le contenu débloqué ci-dessous sont des recommandations
> à valider par un prototype.
>
> **Sources** :
> [parcours publics du Sas](https://github.com/PointZero2050/zegame-docs/blob/main/docs/site/parcours-publics-sas.md),
> [wireflows mobiles](https://github.com/PointZero2050/zegame-docs/blob/main/docs/site/wireflows-mobiles-parcours-publics.md),
> [voix Point Zéro](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/voix-point-zero.md),
> corpus scénique `Ressources Point Zero/Docteur ZERO/`.

---

## 1. Recommandation en une phrase

**Le parcours caché apparaît lorsque le visiteur a réellement rencontré les deux voix du Point
Zéro ; il confronte plusieurs de ses traces, fait dialoguer le Professeur et le Docteur, puis
rend au visiteur la place du troisième narrateur.**

Ce n'est ni un sixième cours, ni un test secret, ni une récompense pour comportement conforme.
C'est un méta-parcours : il révèle que les cinq questions, les deux guides et les réponses du
visiteur restent des points de vue partiels.

Acquisition :

> Une contradiction n'est pas nécessairement une erreur à supprimer. Elle peut signaler deux
> qualités qui cherchent encore le cadre capable de les remettre en circulation.

---

## 2. Pourquoi ce parcours doit « ne pas exister »

Les cinq parcours visibles organisent le savoir. Le sixième interroge l'organisation elle-même.
Il remplit quatre fonctions :

1. **briser la logique de catalogue** : tout ce qui compte n'était pas annoncé dans le menu ;
2. **retourner le dispositif sur lui-même** : le site reconnaît que ses cartes et ses
   restitutions ont des angles morts ;
3. **faire vivre le Tiers** : Professeur et Docteur cessent d'être deux options de ton et
   deviennent deux polarités que le visiteur doit écouter sans élire un vainqueur ;
4. **préparer le Monde 0** : le système ne parle plus seulement du monde ; il demande comment
   plusieurs lectures contradictoires résonnent chez celui qui les a choisies.

Le parcours ne doit pas expliquer toute la théorie du Tiers inclus. Il la fait éprouver.

---

## 3. Conditions de révélation recommandées

### 3.1 Règle principale

Le parcours devient accessible lorsque les trois conditions suivantes sont réunies localement :

- **trois parcours visibles distincts** sont accomplis ;
- le visiteur a terminé au moins un parcours avec le **Professeur Sirbey** et un autre avec le
  **Docteur Z.E.R.O.** ;
- les traces correspondantes existent encore sur l'appareil.

Cette règle est calculée à partir d'états déjà nécessaires au fonctionnement du Sas. Elle
n'ajoute aucun suivi comportemental invisible.

Elle ne demande pas :

- une opinion particulière ;
- une répartition « équilibrée » ;
- un retour arrière, un temps minimal ou un nombre de clics ;
- l'accomplissement des cinq parcours avec les deux guides, réservé au badge **Le Tiers
  inclus** ;
- un compte ou une adresse électronique.

### 3.2 Cas du visiteur fidèle à un seul guide

Après cinq parcours accomplis avec le même guide, la constellation laisse apparaître un indice :

> **Une voix manque à cette carte.**

CTA secondaire : `Rejouer une question avec l'autre guide`.

Le parcours caché ne se déverrouille qu'après ce nouveau regard. Le site n'accuse pas le
visiteur d'être fermé : il rend visible une possibilité qu'il n'a pas encore rencontrée.

### 3.3 Révélation progressive

Le parcours n'apparaît jamais comme une carte grisée `6/6`.

1. Après la première utilisation du second guide, un très léger point vide apparaît au centre
   de la constellation, sans texte ni compteur.
2. Lorsque les conditions sont réunies, ce vide devient une anomalie active : les cinq lignes
   de la constellation semblent éviter un même point.
3. Au prochain retour à l'accueil ou à la fin d'un parcours, une phrase apparaît :

   > Quelque chose manque. Ce qui est curieux, puisque rien n'était prévu.

4. Un tap ouvre l'écran-seuil. Le titre complet n'apparaît qu'après l'entrée.

L'apparition n'interrompt jamais une autre restitution. Aucun e-mail ni notification externe ne
révèle le secret.

### 3.4 Accès direct et tests

- la route publique n'est ni indexée ni présente dans le sitemap ;
- un accès direct sans état éligible montre une page minimale, sans divulguer les conditions :

  > Ce parcours n'existe pas encore depuis cet appareil.

- un paramètre de prévisualisation réservé à l'administration permet les tests éditoriaux ;
- l'absence ou l'effacement du stockage local ne doit jamais être interprété comme un échec du
  visiteur.

---

## 4. Fiche d'identité

- **Titre révélé** : Le parcours qui n'existe pas.
- **Sous-titre** : Consultation n° 0 — le guide absent.
- **Promesse** : faire comparaître plusieurs traces qui ne racontent pas tout à fait la même
  histoire et découvrir ce qu'elles cherchent à protéger ensemble.
- **Durée cible** : 8 à 10 minutes.
- **Nombre d'écrans** : 11.
- **Narration** : Professeur et Docteur interviennent tous les deux ; le visiteur devient le
  troisième narrateur.
- **Interaction centrale** : dialogue court, fondé sur des traces choisies et contestables.
- **Trace** : une tension reconnue, les deux qualités qu'elle protège et une question de Tiers.
- **Badge** : **Patient Z.E.R.O.**
- **Déblocage recommandé** : accès au mentor spécial **Cabinet Z.E.R.O.** après import dans
  l'application.
- **Non-promesse** : aucune analyse clinique, aucun diagnostic psychologique, aucune mesure de
  conscience.

Le mot `Patient` est un renversement théâtral : le Docteur commence par prétendre examiner le
visiteur, puis reconnaît que son véritable patient est le système de récits révélé par leurs
échanges.

---

## 5. Storyboard détaillé

### X01 — L'anomalie

La constellation occupe l'écran. Les cinq traces tournent autour d'un vide qui n'avait jamais
été nommé.

Texte :

> **Ceci n'est pas un sixième parcours.**
>
> Il n'était pas au programme, ne compte pas dans les 100 % et n'améliorera aucune statistique
> officielle. Voilà déjà trois raisons raisonnables de l'ouvrir.

CTA : **Toucher le point absent**.

### X02 — Le titre et le contrat

Le titre apparaît : **Le parcours qui n'existe pas**.

Le Docteur :

> J'ai lu tes traces. Enfin, « lu »… personne ne me laisse approcher les données sans un écran
> de consentement. L'époque conserve quelques réflexes utiles.

Le système explique littéralement :

- quelles traces locales peuvent être utilisées ;
- qu'aucune donnée n'est encore envoyée ;
- que le visiteur choisira ce qu'il présente au dialogue ;
- qu'un parcours local sans IA reste possible et donne le même badge.

Actions :

- **Préparer ma consultation** ;
- `Continuer sans dialogue IA` ;
- `Retourner à la constellation`.

### X03 — Le dossier qui refuse de conclure

Le système présente les cartes des parcours accomplis : question, guide, trace courte et date.
Les textes libres personnels sont masqués par défaut.

Consigne :

> **Choisis trois traces qui ne disent peut-être pas la même chose.**

Le visiteur peut en sélectionner trois à cinq. Un bouton `Voir les données exactes` ouvre la
représentation structurée qui sera utilisée. Chaque élément peut être retiré.

CTA : **Présenter ces traces**.

### X04 — La consultation commence mal

Le Docteur :

> Très bien. Nous avons donc un patient, trois pièces à conviction et aucune certitude. C'est
> nettement plus sérieux qu'un diagnostic en ligne.

Le Professeur intervient :

> Une précision : le patient n'est pas la personne. Nous observons seulement la cohérence
> provisoire de choix produits dans des situations différentes.

Le Docteur :

> Professeur, laisse-moi faire peur aux gens au moins deux phrases avant la note
> méthodologique.

Le dispositif révèle sa règle fondamentale : toute lecture devra montrer ses sources et pourra
être corrigée.

CTA : **Chercher la contradiction**.

### X05 — Trois tensions possibles

À partir des traces sélectionnées, le système propose au maximum trois tensions formulées comme
des questions, par exemple :

- protéger ce qui existe / laisser mourir ce qui empêche de naître ;
- reprendre sa puissance / ne pas reproduire la domination ;
- agir près de soi / soutenir ce qui bénéficie à un ensemble plus vaste ;
- chercher une carte solide / rester disponible à ce qui la contredit ;
- transformer les cadres / ne pas perdre l'élan des personnes.

Chaque proposition cite deux ou trois choix sources. Le visiteur peut :

- choisir une tension ;
- corriger sa formulation ;
- répondre `Je ne reconnais aucune de ces tensions`.

Dans ce dernier cas, il formule une question libre ou choisit une tension générique. Le refus
ne bloque jamais le badge.

CTA : **Mettre cette tension au centre**.

### X06 — La lecture du Professeur

Le Professeur propose une hypothèse structurée en trois blocs :

1. ce que le premier mouvement rend possible ;
2. ce que le second mouvement rend possible ;
3. le niveau logique qui les rend difficiles à tenir ensemble.

Exemple :

> La proximité rend l'effet concret et la responsabilité visible. Le Commun rend possibles
> des infrastructures qu'aucun Cercle ne peut porter seul. La tension ne porte donc pas entre
> égoïsme et générosité, mais entre deux échelles légitimes de souveraineté.

Le visiteur choisit : `Cela m'aide / C'est partiel / Cela ne me correspond pas`, puis peut
ajouter une correction facultative.

CTA : **Entendre l'autre lecture**.

### X07 — La contre-consultation du Docteur

Le Docteur cherche l'Ombre de la formulation précédente sans ridiculiser le visiteur :

> Le Professeur a raison. C'est toujours inquiétant. Maintenant regardons ce que cette élégante
> symétrie permet de ne pas décider.

Sa lecture suit également trois blocs :

1. la qualité captive derrière chaque position ;
2. la peur ou le confort que chaque position peut protéger ;
3. le risque de transformer l'intégration en compromis tiède.

Le visiteur dispose des mêmes droits de réponse et de correction.

CTA : **Confronter les deux voix**.

### X08 — Ce que chacune protège et efface

Deux colonnes deviennent quatre cartes :

- `Ce que le Professeur voit` ;
- `Ce que le Professeur risque d'effacer` ;
- `Ce que le Docteur voit` ;
- `Ce que le Docteur risque d'effacer`.

Le visiteur choisit ou reformule :

- une qualité à conserver de chaque lecture ;
- une simplification à refuser de chaque lecture.

Le but n'est pas de partager la différence en deux. Le Tiers doit préserver les deux qualités
sans conserver les deux enfermements.

CTA : **Prendre la place du guide absent**.

### X09 — Une question qui n'appartient à aucun guide

Le système compose trois questions de Tiers à partir des éléments confirmés. Forme attendue :

> **Comment pourrais-je / pourrions-nous [préserver la qualité A] sans [capture A], tout en
> [préservant la qualité B] sans [capture B] ?**

Le visiteur peut en choisir une, la modifier ou écrire la sienne. Le dialogue IA peut poser
**une seule relance** visant un geste ou un critère observable, jamais une confession intime.

Exemple de relance :

> À quoi verrais-tu, dans une décision réelle, que les deux qualités circulent — et que l'une
> ne s'est pas simplement déguisée en l'autre ?

CTA : **Garder cette question ouverte**.

### X10 — L'ordonnance n° 0

La restitution prend la forme d'une ordonnance détournée :

- tension examinée ;
- sources mobilisées ;
- qualité du premier pôle ;
- qualité du second pôle ;
- captures refusées ;
- question du Tiers ;
- premier signe observable choisi par le visiteur.

Le Docteur :

> Prescription : ne surtout pas résoudre cette contradiction trop vite. Effets secondaires
> possibles : décision moins automatique, perte momentanée de certitude et réapparition du
> libre arbitre.

Le Professeur :

> Cette ordonnance est une hypothèse de travail. Tu peux la conserver, la modifier ou la
> jeter. Le geste important est d'avoir repris la place depuis laquelle elle peut être
> contestée.

CTA : **Conserver l'ordonnance**.

### X11 — Le patient et le passage

Le badge **Patient Z.E.R.O.** apparaît, sans s'ajouter au pourcentage des cinq parcours.

Le Docteur :

> Résultat de l'examen : le patient n'était pas toi. C'était l'histoire que nous étions en
> train de fabriquer à partir de toi. Elle va mieux depuis qu'elle a cessé de se prendre pour
> la vérité.

La constellation montre désormais le point absent comme un espace ouvert, non comme une
sixième étoile identique aux autres.

Actions :

- **Revenir à la constellation** ;
- `Faire passer cette trace dans le Jeu` si le passage vers l'application est disponible ;
- `Recommencer avec d'autres traces`.

Après import dans l'application, le badge peut ouvrir le **Cabinet Z.E.R.O.**, mentor spécial
consacré aux contradictions et aux polarités. Le site ne promet pas cet accès tant que la
fonction n'existe pas réellement.

---

## 6. Wireflow mobile

| ID | Écran | Patron principal | Action | État produit |
|---|---|---|---|---|
| X01 | Anomalie | appel caché | Toucher le point absent | entrée |
| X02 | Titre et contrat | consentement | Préparer ma consultation | mode IA ou local |
| X03 | Dossier | sélection | Présenter ces traces | corpus choisi |
| X04 | Consultation | révélation dialoguée | Chercher la contradiction | règle comprise |
| X05 | Tensions | choix situé | Mettre cette tension au centre | tension corrigée |
| X06 | Professeur | hypothèse contestable | Entendre l'autre lecture | retour visiteur |
| X07 | Docteur | contre-hypothèse | Confronter les deux voix | retour visiteur |
| X08 | Deux voix | matrice 2 × 2 | Prendre la place du guide absent | qualités/captures |
| X09 | Question du Tiers | composition | Garder cette question ouverte | question + signe |
| X10 | Ordonnance | trace | Conserver l'ordonnance | trace locale |
| X11 | Patient Z.E.R.O. | badge secret | Revenir à la constellation | badge/déblocage |

Sur 360 px, la matrice de X08 n'est jamais affichée en quatre colonnes. Deux onglets
`Professeur / Docteur` contiennent chacun `voit / risque d'effacer`, puis une synthèse verticale
réunit les quatre choix.

---

## 7. Contrat du dialogue IA

### 7.1 Fonction autorisée

Le modèle ne doit accomplir que quatre opérations :

1. rapprocher des choix explicitement sélectionnés ;
2. proposer des tensions appuyées sur leurs sources ;
3. produire deux lectures contrastées selon les contrats des guides ;
4. aider à formuler une question de Tiers et un signe observable.

Il ne doit jamais :

- déduire un profil psychologique, une Puissance, un niveau de conscience ou une pathologie ;
- inventer un fait absent des traces ;
- rechercher des informations externes sur la personne ;
- établir qu'une lecture est la vérité cachée du visiteur ;
- donner un conseil médical, juridique, financier ou thérapeutique ;
- multiplier les relances pour retenir le visiteur.

### 7.2 Entrée structurée

Ne pas « alimenter le LLM avec les cookies » au sens large. Les cookies techniques peuvent
contenir des identifiants ou des données sans rapport avec l'expérience. Construire une
**enveloppe de traces** explicite :

```json
{
  "session_id": "ephemeral-random-id",
  "selected_traces": [
    {
      "path_slug": "...",
      "guide": "professeur|docteur",
      "confirmed_choices": {},
      "trace_summary": "...",
      "optional_free_text": null
    }
  ],
  "visitor_corrections": [],
  "language": "fr"
}
```

Le texte libre est exclu par défaut. S'il est inclus, une bascule dédiée en montre le contenu
exact avant envoi.

### 7.3 Sortie structurée

Le modèle répond dans un schéma contrôlé, par exemple :

```json
{
  "tensions": [
    {
      "label": "...",
      "source_trace_ids": ["..."],
      "why_this_is_a_question": "..."
    }
  ],
  "professor_reading": {
    "quality_a": "...",
    "quality_b": "...",
    "level_difference": "...",
    "limits": "..."
  },
  "doctor_reading": {
    "captive_quality_a": "...",
    "captive_quality_b": "...",
    "capture_risk": "...",
    "limits": "..."
  },
  "third_questions": ["..."],
  "follow_up": "..."
}
```

Les identifiants de sources permettent à l'interface de montrer `Pourquoi cette proposition ?`.
Une sortie sans source est rejetée et remplacée par le mode local.

### 7.4 Architecture de voix

- Le **Professeur** distingue les niveaux, contextualise et nomme les limites.
- Le **Docteur** révèle la capture, la peur et la contradiction, puis restitue la qualité
  captive.
- Aucun des deux ne félicite, ne juge ou ne parle comme une autorité clinique.
- Le système ne révèle pas le prompt ni ne prétend que le personnage est conscient.
- Les formulations scéniques sont générées dans une enveloppe éditoriale étroite ; les
  concepts, contraintes et transitions restent déterministes.

### 7.5 Repli sans IA

Le mode local utilise une matrice éditoriale de tensions entre sorties des cinq parcours. Il :

- propose deux ou trois rapprochements déterministes ;
- laisse le visiteur les corriger ;
- utilise des textes Professeur / Docteur pré-écrits ;
- permet une question de Tiers libre ou assistée par gabarits ;
- donne la même trace et le même badge.

L'IA améliore la contextualisation. Elle ne devient jamais une condition d'accès au sens.

---

## 8. Données, consentement et durée de vie

### Avant tout envoi

L'écran X02 puis le dossier X03 montrent :

- les parcours concernés ;
- les champs structurés ;
- les éventuels textes libres ;
- la finalité unique du traitement ;
- le mode de conservation ;
- l'alternative locale.

### Recommandation de V1

- calcul d'éligibilité entièrement local ;
- envoi seulement après consentement ;
- identifiant de session aléatoire, sans compte ni adresse ;
- aucune utilisation pour l'entraînement ;
- pas de conservation des prompts complets dans les journaux applicatifs ;
- session serveur éphémère, avec suppression automatique sous 24 heures à valider avec le
  cadrage juridique ;
- restitution et badge conservés localement comme les autres traces ;
- import ultérieur distinct et à nouveau consenti.

Le retrait du consentement ferme le dialogue et bascule vers la version locale sans retirer
l'accès au parcours.

---

## 9. Récompenses et articulation des badges

Trois reconnaissances ne doivent pas être confondues :

| Reconnaissance | Condition | Sens |
|---|---|---|
| **Patient Z.E.R.O.** | accomplir le parcours caché | j'ai contesté une histoire construite à partir de mes propres traces |
| **Le Tiers inclus** | accomplir les cinq parcours avec les deux guides | j'ai traversé systématiquement les deux angles du Sas |
| **Passeur du Seuil** | relier la constellation à ce qui se joue en soi, dans l'application | j'ai transformé les fragments publics en entrée consciente dans le Jeu |

Le parcours caché :

- ne donne aucun Oméga sur le site public ;
- ne compte pas dans le pourcentage des cinq parcours ;
- ne remplace pas le Passage du seuil ;
- ne révèle pas à l'avance la condition du Tiers inclus ;
- reste rejouable avec d'autres traces, sans multiplier les badges.

### Contenu spécial recommandé

**V1** : une `Ordonnance n° 0` locale et importable, puis le déblocage du mentor **Cabinet
Z.E.R.O.** lorsque cette fonction est disponible dans l'application.

**Plus tard** : le Cabinet peut proposer une nouvelle consultation après un passage de Monde,
une contradiction de parcours ou une confrontation. Une dédicace, un chapitre caché ou un
contenu scénique peut être ajouté ponctuellement, mais ne doit pas devenir une promesse
logistique permanente.

---

## 10. Direction artistique et sonore

Le parcours utilise la coque analytique des cinq chemins, progressivement contaminée par le
registre du Jeu :

- le vide central de la constellation devient un seuil ;
- les cadres se décalent légèrement, comme un dossier dont les calques ne coïncident plus ;
- le Professeur conserve son médaillon clair et stable ;
- le Docteur apparaît en collage plus contrasté, mais sans effet horrifique ;
- lors de X08, leurs images cessent d'occuper le centre : l'espace vide revient au visiteur ;
- l'ordonnance mêle formulaire médical ancien, annotations contemporaines et symboles Point
  Zéro, sans imiter un document médical réel ;
- un son discret de bande, de papier ou de craie remplace la fanfare de récompense ;
- aucun effet de glitch ne compromet la lecture, le focus ou la sensibilité au mouvement.

La surprise vient d'une rupture de composition, pas d'un soudain changement de marque.

---

## 11. Garde-fous éditoriaux et éthiques

- Le badge **Patient Z.E.R.O.** reste manifestement théâtral ; ne jamais employer de vocabulaire
  de diagnostic réel dans la restitution.
- Ne pas affirmer qu'une contradiction révèle un trauma, une sous-personnalité ou une Ombre
  personnelle.
- Ne pas utiliser les citations scéniques les plus violentes du Docteur dans ce dialogue
  individuel ; son ironie vise ici le dispositif et les récits collectifs.
- Ne pas fabriquer une tension lorsque les traces ne permettent pas de l'étayer.
- Ne pas récompenser l'acceptation de l'hypothèse du modèle ; la correction ou le refus sont des
  accomplissements valides.
- Ne pas présenter le Tiers comme une moyenne, un compromis ou une injonction à réconcilier des
  positions incompatibles.
- Ne pas envoyer de cookies bruts, données de navigation, identifiants publicitaires ou champs
  étrangers aux parcours.
- Ne pas exposer le contenu libre d'une trace sur un écran partagé sans action du visiteur.
- Ne pas bloquer le parcours lorsque l'IA, le réseau ou le consentement font défaut.
- Ne pas attribuer automatiquement un mentor, un avantage ou un contenu qui n'existe pas encore
  dans l'application.

---

## 12. Critères d'acceptation

Le prototype est concluant si :

1. aucun testeur ne voit une sixième carte verrouillée avant la révélation ;
2. la règle d'éligibilité fonctionne sans donnée comportementale nouvelle ;
3. les deux guides ont un apport et un angle mort perceptibles ;
4. le visiteur comprend qu'il est autorisé à contester les deux lectures ;
5. chaque tension proposée cite des choix sources exacts ;
6. un refus de l'analyse permet d'obtenir le badge en construisant une autre question ;
7. le mode local et le mode IA atteignent la même acquisition ;
8. le consentement indique les données exactes avant leur envoi ;
9. aucune sortie n'est formulée comme un diagnostic de la personne ;
10. **Patient Z.E.R.O.**, **Le Tiers inclus** et **Passeur du Seuil** restent distincts ;
11. le parcours tient en 8 à 10 minutes, hors rédaction libre ;
12. le retour à la constellation donne l'impression qu'un espace s'est ouvert, pas qu'une case
    supplémentaire a été cochée.

---

## 13. Séquence de mise en œuvre recommandée

1. Tester sur papier X05 à X09 avec des traces fictives contradictoires.
2. Écrire une matrice locale couvrant les principales tensions entre les cinq parcours.
3. Prototyper la révélation dans la constellation et les onze écrans en 360 px.
4. Tester la compréhension du consentement et la possibilité de refuser les lectures.
5. Valider la voix des deux personnages avec Boris.
6. Implémenter d'abord le mode déterministe local.
7. Ajouter le dialogue IA derrière le même contrat de sortie, sans modifier le wireflow.
8. N'annoncer le Cabinet Z.E.R.O. qu'après livraison réelle du mentor dans l'application.

Cette séquence permet de vérifier que le parcours possède un sens propre avant de confier sa
contextualisation à un modèle.
