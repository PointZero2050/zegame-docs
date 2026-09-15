# M0 · E13 — contexte du mentor et Graine de relation

## Problème constaté

Lorsqu’un joueur ouvre le mentor depuis E13, le dialogue actuel ne reçoit pas l’Expérience ni
l’étape qui l’a ouvert. Les vingt derniers messages peuvent appartenir à E7 ; ils sont néanmoins
comptés comme le début de la consultation courante. Le modèle peut donc proposer dès sa première
réponse une Graine déjà formulée et plantée au chapitre précédent.

Le contexte joueur ne couvre en outre qu’une partie des productions. Le Schéma de circulation,
le signe de reconnaissance et les résonances ne parviennent pas au mentor, alors que le rang 1
d’E13 annonce que ces éléments seront transmis au dialogue.

Enfin, accepter la proposition avec « Planter dans ma Fresque » crée une Graine générale, mais ne
la rattache pas au `ChallengesUser` d’E13. Le geste visible et la preuve attendue divergent.

## Décision de produit

Une entrée dans le mentor depuis une étape ouvre une **nouvelle séquence pédagogique**, rattachée
à l’Expérience et au rang d’origine. L’historique plus ancien reste un arrière-plan utile ; il ne
compte jamais comme les tours de la séquence courante et ne peut pas déclencher à lui seul une
nouvelle proposition de Graine.

Le mentor reçoit quatre éléments issus d’une même origine serveur :

1. l’Expérience et le rang qui ont ouvert le dialogue ;
2. l’intention pédagogique, l’explication et la sortie déclarées dans le YAML du rang ;
3. les productions que le joueur a choisi de rendre lisibles pour cet usage, par
   `RegistreDesTraces` plutôt que par la seule table `Trace` ;
4. les Graines déjà proposées avec leur état : plantée, écartée ou encore ouverte.

Les autorisations LLM restent la garde. Le registre élargit les familles de productions prises en
charge ; il ne rouvre aucune catégorie désactivée par le joueur.

## Consigne à fournir au modèle

Le bloc est construit côté serveur et précède la consigne de dialogue :

```text
<etape-en-cours>
Expérience : Les choses se précisent
Étape : Explore une relation possible avec ton mentor
Intention : Dialogue sur une personne, un cercle ou une communauté à partir de ce que le joueur
vient de traverser.
</etape-en-cours>

Cette étape ouvre une nouvelle séquence de dialogue. Utilise les échanges antérieurs comme
contexte, mais ne les compte pas comme des échanges de cette séquence. Réponds d’abord au message
actuel et aide le joueur à préciser la relation qu’il souhaite explorer. Ne propose pas de Graine
dès la première réponse : fais émerger au moins une situation concrète et ce qu’elle met en jeu
pour lui. Ne repropose jamais une Graine déjà plantée ou écartée. Une nouvelle proposition doit
formuler ce qui s’est dégagé dans la séquence actuelle.
```

Le titre et l’intention ne sont pas écrits en dur dans le service : ils sont lus dans la
configuration du rang. La carte générale du Monde 0 suit la même règle et ne nomme que les
éléments réellement ouverts au joueur.

## Graine et preuve d’E13

Quand le dialogue a été ouvert depuis E13, **« Planter dans ma Fresque »** réalise un seul geste
atomique et idempotent :

- la Graine rejoint la Fresque selon le mécanisme existant ;
- la même Graine est rattachée au `ChallengesUser` d’E13 ;
- le rang 3 relit ce rattachement comme sa preuve réelle.

Un second clic, un rechargement ou deux onglets ne créent ni seconde Graine, ni seconde preuve.
Une proposition seulement affichée ne valide rien. Une proposition écartée ne valide rien.

Le même principe s’applique à E19 lorsqu’une proposition de Graine y est explicitement ouverte
depuis l’étape concernée : le contexte d’origine détermine le rattachement, jamais la date du
message ni la dernière Expérience visitée.

## Recette minimale

- E7 puis E13 : le premier message d’E13 reçoit une réponse sur la relation actuelle, sans reprise
  immédiate de la Graine d’E7.
- Les messages d’E7 restent disponibles comme contexte, mais le compteur de la séquence E13
  repart à zéro.
- Une Graine plantée ou écartée n’est jamais reproposée mot pour mot.
- Les productions du chapitre 2 présentes dans `RegistreDesTraces` sont transmises si leur
  catégorie est ouverte, et absentes si elle est fermée.
- Accepter une proposition issue d’E13 la rend visible dans la Fresque et satisfait la preuve du
  rang 3 d’E13 avec le même identifiant.
- Accès direct au mentor sans Expérience : aucune attribution artificielle à E13 ou E19.
- La carte du Monde 0 transmise au modèle suit la configuration et le dévoilement courants.
