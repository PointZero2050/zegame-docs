# Confidentialité des parcours et des regards invités

> Note Codex — 20 octobre 2026. Textes de remplacement pour le poste fixe et contrat
> de production à vérifier avec le portable. Les blocs publics ci-dessous ne sont
> pas encore intégrés à `pointzero-app`.

## Décisions et état de livraison

Les cinq explorations du Monde 0 exigent un compte. La partie est enregistrée sur
le serveur ; l'ancien dispositif anonyme, stockage local puis import est caduc.
Les sources de préprod `45fea863` confirment cette règle dans `SasController`,
`PartiesSasController`, `PartieSas` et `FermetureDeCompte`.

Les regards invités sont un essai en préprod réservé aux administrateurs, derrière
`REGARDS_INVITES`. Le lot A exclut les messages antérieurs à l'arrivée et ceux des
membres ayant suspendu toute personnalisation IA. **Il ne recueille pas encore
d'accord explicite par fil.**

**Boris, 20 octobre : accord explicite par fil pour la production.** La déclinaison
proposée ci-dessous est individuelle : chacun autorise la lecture de ses propres
messages. L'accord d'un administrateur, une majorité du groupe, une annonce ou la
poursuite de la discussion ne valent pas accord pour les autres. Cette déclinaison
n'impose pas l'unanimité pour qu'un regard existe dans le fil : le contenu des
membres qui n'ont pas accepté reste exclu. Si Boris souhaite une unanimité avant
toute sollicitation, ce serait une règle collective supplémentaire à arbitrer.

Le lot éditorial Parcours peut être porté avec la sauvegarde serveur. Le lot
Regards ci-dessous attend le mécanisme d'accord et sa recette avant publication.
Il ne suffit pas de modifier la politique pour ouvrir la fonctionnalité.

## Texte public à remplacer maintenant pour les parcours

### Remplacer le paragraphe 4.2

### 4.2 Parcours de découverte du Monde 0

Les cinq parcours de découverte se jouent avec un compte Point Zéro. Dès le premier
écran, votre partie est rattachée à ce compte. Nous enregistrons sur nos serveurs
l'écran atteint, le guide choisi, les réponses, les choix et les textes libres que
vous saisissez, ainsi que les dates nécessaires à la reprise de la partie.

À la fin d'un parcours, une Trace conserve les éléments de votre passage et la
reconnaissance obtenue : badge et Omégas. Rejouer ce parcours ne donne pas une
seconde fois les Omégas déjà obtenus. Vos réponses et textes ne sont pas publiés
automatiquement.

**Finalités :** permettre la reprise de votre partie, conserver vos réponses et
reconnaître les parcours accomplis.  
**Base juridique :** exécution du Service demandé.  
**Durée :** pendant la vie du compte. À sa fermeture, les parties enregistrées sont
supprimées et les réponses et textes libres des Traces de ces parcours sont
effacés. La reconnaissance du parcours, son badge et ses Omégas restent associés
à la ligne de compte neutralisée, selon les modalités de la section 13.

La progression de ces parcours n'est pas conservée dans la mémoire locale de
votre navigateur. Les informations présentes dans la page pendant une session
servent à afficher et à jouer le parcours ; la reprise repose sur les données
enregistrées sur le serveur.

### Remplacer le premier paragraphe de la section 9

Le Service utilise des traceurs strictement nécessaires pour maintenir votre
session, sécuriser votre compte et mémoriser les préférences nécessaires à son
fonctionnement. Ces traceurs ne nécessitent pas votre consentement lorsqu'ils
restent strictement limités à ces finalités. La progression des cinq parcours de
découverte est enregistrée sur le serveur, comme indiqué en section 4.2.

### Remplacer le dernier paragraphe de la section 9

Effacer les données du site dans votre navigateur peut fermer votre session ou
réinitialiser certaines préférences. Cela ne supprime pas les parties ni les
Traces enregistrées sur nos serveurs. Pour demander leur effacement, utilisez les
modalités de la section 12 ; la fermeture du compte est décrite en section 13.

### Ajouter dans la section 13 après le paragraphe sur les contributions partagées

Les parties des cinq parcours de découverte sont supprimées à la fermeture du
compte. Les réponses et textes libres conservés dans leurs Traces sont effacés ;
les badges et Omégas acquis restent associés à la ligne de compte neutralisée.
Les copies résiduelles suivent la rotation des sauvegardes décrite ci-dessous.

## Texte public pour les regards après livraison de l'accord

### Préciser le principe de la section 3

- publier un contenu ou rejoindre un fil ne donne pas automatiquement accès à vos
  messages à une IA ; la lecture par un regard invité dépend de votre accord
  explicite dans ce fil, selon la section 4.8.1 ;

### Ajouter à la fin de la section 4.7

Lorsqu'un mentor ou un Enfant Libre intervient comme regard invité dans un fil
collectif, son accès est limité au contexte de ce fil décrit en section 4.8.1.
Vos autorisations de personnalisation d'un mentor individuel ne sont pas
transférées à ce regard. L'Enfant Libre invité utilise son nom et le ton de son
archétype ; il ne reçoit ni le désir ni les réponses d'Immateria de la personne
qui l'a invité.

### Ajouter après la section 4.8

### 4.8.1 Regards invités dans une conversation

Un regard invité est un personnage assisté par intelligence artificielle : un
mentor ou l'Enfant Libre d'un membre. Une personne habilitée dans le fil peut
l'inviter pour questionner les évidences, apporter une autre perspective ou aider
à concrétiser les échanges. L'annonce d'arrivée indique son identité, sa mission
et la personne qui l'a invité. Ses interventions sont identifiées comme produites
par une IA et visibles par les membres autorisés de la conversation.

Avant que vos messages soient utilisés dans ce cadre, vous choisissez
explicitement d'autoriser ou de refuser leur lecture dans ce fil. Le fait de
continuer à écrire, l'accord d'un autre membre ou votre accord dans un autre fil
ne remplace pas ce choix. Vous pouvez continuer à participer à la conversation
si vous refusez.

Lorsqu'une personne sollicite le regard, Point Zéro transmet à l'API commerciale
d'Anthropic la question et un contexte limité à huit messages humains au maximum,
avec le prénom de leur auteur. Les messages retenus ont été écrits après
l'annonce d'arrivée du regard et après l'accord de leur auteur dans ce fil.
Les messages des membres qui n'ont pas donné leur accord ou qui ont suspendu
l'IA sont exclus. Les pièces jointes, les objets de Récit, les mémoires privées
et les réponses d'autres IA ne font pas partie de ce contexte.

Le regard répond sur sollicitation humaine. Sa réponse ne déclenche aucun
courriel ni récapitulatif par courriel. Elle reste dans l'historique du fil après
la pause ou le retrait du personnage.

Vous pouvez retirer votre accord depuis les réglages du fil. La suspension
globale de l'IA dans votre personnalisation exclut également vos messages des
appels suivants. Le retrait arrête les nouvelles utilisations de vos messages ;
il n'annule pas les traitements déjà réalisés ni les délais de conservation
applicables aux données déjà transmises. Ne copiez pas dans une sollicitation
les propos ou les données personnelles d'un autre membre sans son autorisation.

**Finalité :** enrichir les échanges du fil par une intervention IA demandée par
une personne habilitée.  
**Base juridique pour la transmission de vos messages :** votre consentement
spécifique à ce fil. Les règles de la section 4.5 s'appliquent si des données
sensibles sont concernées.  
**Destinataire technique :** Anthropic, via son API commerciale ; les garanties de
transfert sont décrites en sections 7 et 8.  
**Durée chez Anthropic :** jusqu'à trente jours selon les conditions de rétention
de l'API, avec les exceptions de sécurité, de lutte contre les abus ou
d'obligation légale prévues par le fournisseur.  
**Durée chez Point Zéro :** les messages et réponses restent soumis à la durée de
conservation de la conversation définie en section 4.8. L'historique des choix
d'autorisation est conservé pour appliquer et justifier ces choix pendant la
durée nécessaire à ces finalités et à la défense des droits.

## Libellés proposés pour l'accord dans le fil

Texte d'information avant le choix :

> **Autoriser ce regard dans ce fil ?** À chaque sollicitation, la question et
> jusqu'à huit messages humains peuvent être transmis à Anthropic. Seuls tes
> messages écrits après ton accord et après l'arrivée du regard pourront entrer
> dans ce contexte. Les réponses seront visibles dans le fil. Tu peux refuser ou
> retirer ton accord dans les réglages, et continuer à échanger.

Choix de même niveau : **Autoriser mes messages** / **Continuer sans autoriser**.
Lien : **Voir les données utilisées**, puis accès à la politique complète.
Réglage durable : **Retirer mon accord dans ce fil**.

Annonce d'arrivée proposée :

> [Nom] rejoint le fil, invité par [Prénom], pour [mission]. C'est un regard IA.
> Il ne pourra lire que les messages des membres qui l'ont autorisé ici, écrits
> après leur accord et après son arrivée. Chacun garde la main sur son choix.

Un nouvel arrivant n'hérite d'aucun accord. Un autre personnage, une nouvelle
mission ou une modification du contexte doit faire vérifier si le périmètre
reste celui présenté lors du consentement ; sinon un nouveau choix est requis.

## Contrôle avant publication

- Le serveur doit exclure par défaut les messages sans accord individuel enregistré
  pour ce fil. Date, portée, version de l'information et retrait doivent être
  traçables. Retirer une suspension globale ne doit pas transformer un refus ou
  une absence d'accord en autorisation.
- Filtrer avant l'appel, y compris les questions envoyées par mention ou formulaire.
  Dans le lot A, `RegardReponse.tour` ajoute séparément la question du sollicitant :
  un filtre du seul `contexte_lisible` ne suffit pas. Une personne ayant suspendu
  l'IA ne doit pas pouvoir envoyer ses propres messages à l'IA par cette autre voie.
- Le filtre d'auteurs ne détecte pas une citation manuelle des propos d'un membre
  non consentant. Ne pas promettre une exclusion sémantique parfaite ; prévoir
  information du sollicitant et traitement des incidents ou signalements.
- Revoir le masquage/signalement des réponses IA, déjà signalé par le portable,
  l'ouverture au-delà des administrateurs et la conservation des preuves d'accord.
- La rétention fournisseur de trente jours n'est pas un délai de suppression des
  messages dans Point Zéro. Vérifier le contrat Anthropic et le modèle réellement
  déployé ; ne pas annoncer une conservation nulle par défaut.
- Relire l'article 9 des CGU avec cette règle et incrémenter version/date effective
  de la politique à la publication. Les blocs internes de ce document ne doivent
  pas être copiés dans l'article public.

## Sources et périmètre documentaire

Sources applicatives consultées sur `pointzero-app`, préprod `45fea863` :
`app/models/regard_invite.rb`, `app/services/regard_reponse.rb`,
`app/controllers/regards_controller.rb`, `app/models/partie_sas.rb`,
`app/controllers/parties_sas_controller.rb`, `app/controllers/sas_controller.rb`,
`app/services/fermeture_de_compte.rb` et la politique actuelle version 1.0.
Cette lecture de code n'est pas une recette du serveur déployé.

Les contrats historiques de stockage local sont explicitement marqués caducs
dans les cinq documents signalés par le portable. Q17 est remplacée. Le canon
de réorganisation M0/M1 du 15 octobre prime également sur les anciennes
descriptions du Monde 0 présentes dans ces archives.

Références officielles vérifiées le 20 octobre 2026 :

- [CNIL LINC, le consentement](https://design.cnil.fr/concepts/consentement/) :
  choix libre et spécifique, acte positif préalable, retrait possible.
- [Anthropic, rétention des données commerciales](https://privacy.claude.com/en/articles/7996866-how-long-do-you-store-my-organization-s-data) :
  suppression des entrées/sorties API sous trente jours, avec exceptions.
- [Anthropic, modèles à rétention obligatoire](https://support.claude.com/en/articles/15425996-data-retention-practices-for-covered-models) :
  vérifier les conditions du modèle et du contrat avant toute promesse de ZDR.
