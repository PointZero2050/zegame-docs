# M0 — Créer sa Graine, éveiller Imagination, puis rencontrer son mentor

Note Codex — décision de Boris du 12 septembre 2026. Cette version remplace le premier contrat du même jour qui séparait une Trace « Appel » et une Graine. La préproduction a confirmé que ces deux productions rendent les rangs 2 et 3 redondants.

## Décision à appliquer

Conserver l’ordre, les identifiants et les slugs des expériences :

1. E6 `et-moi-dans-tout-ca` : relire ses Traces, répondre librement à trois questions dans **une seule Graine de l’Appel**, puis découvrir la Puissance Imagination ;
2. E7 `choisir-qui-marchera-a-mes-cotes` : choisir son mentor, lui poser une première question, puis découvrir la Puissance Émotion selon son contrat propre.

E6 reste entièrement solo. Elle ne demande aucun mentor. La Graine et l’éveil sont deux gestes distincts : la Graine active Imagination ; le sas explique ensuite ce qui vient de s’ouvrir et où le retrouver. L’ordre Imagination puis Émotion reste inchangé.

## E6 — séquence cible

Titre inchangé : « Et moi dans tout ça ? ». Modalité : « Solo ». Conserver les trois rangs, les durées 4 / 11 / 5 minutes et le barème actuel de 6 Ω.

| Champ | Rang 1 | Rang 2 | Rang 3 |
|---|---|---|---|
| verbe | Relire | Semer | Découvrir |
| libellé | les Traces | ta Graine de l’Appel | la Puissance Imagination |
| titre | Rassemble ce que l’époque a réveillé | Quelle direction veux-tu faire naître ? | Découvre la Puissance Imagination |
| accroche | Tes Traces commencent à former une direction. | Trois questions pour donner une forme libre à ton Appel. | Ta Graine vient d’ouvrir un nouvel espace dans le Jeu. |
| CTA | Relire mes Traces | Écrire ma Graine | Découvrir Imagination |
| confirmation | J’ai choisi les Traces à reprendre | aucune confirmation déclarative : la Graine enregistrée fait foi | aucune confirmation déclarative : le sas achevé fait foi |
| revoir | Relire tes Traces | Relire ma Graine | Revoir la découverte d’Imagination |

**Explication rang 1 :** « Relis les choix, miroirs et hypothèses produits depuis le début du parcours. Repère ce qui continue de vibrer ou de résister. »

**Explication rang 2 :**

> Trois questions peuvent t’aider à orienter ta Graine :
>
> - Qu’est-ce que tu souhaites quitter ?
> - Qu’est-ce que tu veux préserver ?
> - Qu’est-ce que tu aimerais explorer ?
>
> Laisse-les se répondre dans un seul texte. Ta Graine n’a pas besoin d’être définitive : tu pourras la faire évoluer.

La surface montre ces trois questions comme repères, puis **un seul champ libre** intitulé « Ma Graine de l’Appel ». Elle ne présente pas trois formulaires séparés et ne crée aucune Trace intermédiaire. L’enregistrement produit directement la Graine contextualisée dans le fil du `ChallengesUser` d’E6. La simple ouverture n’écrit rien.

**Explication rang 3 :** « Tu viens de faire agir Imagination : tu as relié tes Traces pour donner forme à une direction qui n’existait pas encore. Découvre comment cette Puissance circule entre JE RÉALISE, JE CRÉE et JE RÊVE, et où la retrouver dans l’application. »

**Sorties et reconnaissances :**

- rang 1 : Traces repérées pour nourrir la Graine ;
- rang 2 : Graine de l’Appel réellement enregistrée ; reconnaissance « Ta Graine de l’Appel est semée. » ;
- rang 3 : éveil d’Imagination achevé ; reconnaissance « Tu as découvert la Puissance Imagination. » ; ce dernier fait ferme E6.

## Surface de la Graine

La page provisoire `/appel` peut garder son adresse pour éviter une rupture de liens, mais sa nature change : elle devient l’éditeur de la Graine d’E6.

- une seule Graine par joueur et par E6 ; une reprise modifie cette Graine au lieu d’en créer une deuxième ;
- le texte existant est prérempli lors d’une reprise ;
- la visibilité suit les réglages et contrôles actuels des Graines ; elle n’est jamais modifiée par un GET ;
- l’ancienne Trace `appel-et-moi-dans-tout-ca`, lorsqu’elle existe sans Graine, peut préremplir une fois le nouveau champ, mais elle ne prouve plus le rang 2 ;
- une Graine E6 déjà présente prouve immédiatement le rang 2, y compris pour un joueur antérieur ;
- une E6 déjà validée reste validée, sans nouveau gain ni nouveau reçu.

`Graine.semer_sur!` crée aujourd’hui un nouveau message à chaque appel. Le raccord doit donc fournir une écriture idempotente pour cette Graine unique, ou une mise à jour autorisée du message existant appartenant au joueur. La preuve reste `Graine.semee_sur?(ChallengesUser)` ; aucune nouvelle table n’est nécessaire.

## Rang 3 — raccord à l’éveil d’Imagination

Le CTA doit ouvrir le vrai sas `Eveil` pour `imagination`, dans le contexte de l’excursion E6, afin que « Revenir à l’Expérience » ramène à `et-moi-dans-tout-ca`.

La preuve du rang 3 est `Eveil.annoncee?(user, "imagination")`, posée seulement lorsque le joueur termine le sas. Le dernier POST du sas doit repasser par la logique de retour d’excursion ou appeler la même constatation de fin de séquence ; sinon le marqueur existe mais E6 ne se ferme pas avant une action supplémentaire.

Cas à refuser : accès à l’éveil avant la Graine, simple ouverture de la page, carte seulement consultée, retour anticipé. Ces cas ne ferment pas le rang 3.

## Références visuelles impératives

### Éveil des Puissances

Référence finale : `zegame-prototypes@9ddf784`, dossier `devoilement-emotion-cible/`, variante `?power=imagination`.

Cette tête contient toute la chaîne validée de `82cc796` à `ca0905b`, puis l’alignement sur les couleurs canoniques. Elle remplace les versions intermédiaires déjà portées. En particulier :

- aucun petit paragraphe secondaire sous la description principale des trois verbes ;
- description principale agrandie et moins indentée ;
- icônes Ombre sur leur disque noir, sans bordure ajoutée ;
- icônes alignées sur l’axe médian du lemniscate ;
- Tao sans cercle blanc ajouté ;
- trois cartes d’état cliquables sous le lemniscate ;
- sortie immersive avec l’illustration de la Puissance et un lemniscate vert fin sous halo jaune.

La préproduction contrôlée le 12 septembre affiche encore, par exemple, « Une Trace permet… », « Planter une Graine transforme… » et « La Fresque permet… » sous les verbes d’Imagination : ces trois textes appartiennent à une version antérieure et doivent disparaître.

### Bandeau d’excursion

Référence finale du composant : `zegame-prototypes@57b7a92`, dossier `bandeau-excursion-progression-cible/`. La ligne de progression est sur fond violet presque noir `#20101f`, sous la ligne de contexte et de retour.

Version publique vérifiée : <https://maquettes.167-233-210-57.sslip.io/pz-cible/bandeau-excursion-progression-cible/>.

Le sélecteur et les commandes de démonstration du prototype ne sont pas portés. Le bandeau reçoit le titre, l’Expérience d’origine, le retour et la progression réels.

## Répartition

### Portable

- remplacer la preuve Trace du rang 2 par la Graine contextualisée ;
- déplacer `GESTES_DE_GRAINE["et-moi-dans-tout-ca"]` du rang 3 au rang 2 ;
- retirer E6 de `GESTES_D_APPEL` et ne plus faire de `Appel.formulee?` une preuve ;
- exposer la porte d’éveil Imagination comme excursion du rang 3 ;
- faire de l’annonce achevée d’Imagination la preuve du rang 3 et constater la fin d’E6 au retour ;
- préserver les joueurs existants, les Graines, validations et Ω.

### Poste fixe

- remplacer la page provisoire à trois zones par les trois questions et un champ libre de Graine ;
- porter le sas d’éveil strictement depuis `9ddf784` ;
- porter le bandeau strictement depuis `57b7a92` ;
- vérifier ordinateur, mobile, clavier, reprise et réduction du mouvement.

## Recette minimale

- E6 sans mentor : rang 1 accessible, puis Graine libre, puis éveil Imagination ; aucun détour vers `/heros`.
- Ouvrir ou recharger l’éditeur n’écrit rien.
- Enregistrer une Graine non vide confirme le rang 2, active Imagination et débloque seulement alors le rang 3.
- Revenir modifier la Graine ne crée pas un second message et ne crédite rien de plus.
- Terminer le sas confirme le rang 3, ferme E6 et produit une seule animation de reconnaissance et un seul reçu.
- Quitter le sas en cours conserve sa progression sans fermer E6.
- Un ancien Appel préremplit le champ sans valider ; une ancienne Graine valide le rang 2 ; une ancienne E6 validée ne régresse pas.
- E7 retrouve la Graine E6, puis conserve choix du mentor, question et éveil Émotion.
- Le rendu d’éveil ne contient plus les trois paragraphes secondaires constatés en préproduction.

Aucun changement de barème, de durée, de slug, d’ordre d’Expérience ou d’autorité E7 n’est compris dans cette décision.
