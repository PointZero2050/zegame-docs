# Tunnel d'engagement et inscription en ligne

## Statut

Spécification cible issue de l'analyse de `/entrer` et des cinq parcours publics. Elle cadre
le passage du site vers l'application ; elle n'ouvre pas à elle seule les inscriptions en
production.

Prototype navigable : `zegame-prototypes/tunnel-engagement-cible/`.

## Intention

Les cinq parcours publics font goûter le Jeu sans imposer de compte. L'inscription devient
désirable après une valeur réellement reçue : elle stabilise ce qui n'existait jusque-là que
sur un appareil et permet aux reconnaissances du Sas de rejoindre le Jeu.

Le tunnel ne doit donc pas être une barrière placée avant l'expérience. Il apparaît après un
premier passage accompli, puis gagne en intensité à mesure que la constellation se complète.

## Contrat canonique

- Les cinq parcours restent consultables, terminables et rejouables sans compte.
- Chaque parcours public accompli reconnaît un badge et **5 Omégas**, soit 25 Omégas pour les
  cinq parcours.
- La mémoire avant inscription est locale au navigateur et liée à l'appareil. Elle n'est pas
  présentée comme un compte.
- Après création du compte, l'import est automatique, idempotent et conserve la provenance de
  chaque reconnaissance. Un rejeu ou un nouvel import ne crée pas un doublon.
- L'utilisateur voit avant l'import ce qui a été retrouvé, puis reçoit une restitution exacte
  de ce qui a été importé, ignoré ou conservé localement.
- Une erreur d'import ne supprime jamais la copie locale.
- Aucune formulation personnelle n'est publiée automatiquement. Les choix de visibilité se
  font plus tard, dans l'application.
- L'Oméga n'est ni un actif financier, ni un moyen de paiement, ni une valeur échangeable.
- Le badge **Passeur du Seuil** reste obtenu dans l'application, par son expérience dédiée.

## Les quatre mouvements du passage

### 1. Créer son espace

Formulaire minimal : e-mail, mot de passe, acceptation des CGU et de la politique de
confidentialité. Les compléments de profil appartiennent au Monde 0 et ne doivent pas alourdir
l'inscription.

### 2. Annoncer l'import

Avant exécution, une page récapitule chaque parcours retrouvé avec son badge, la Puissance
associée et les 5 Omégas reconnus. Le total et le nombre de doublons sont visibles.

### 3. Importer une seule fois

L'opération rattache les reconnaissances locales au compte. La clé technique doit permettre
de rejouer le parcours et de relancer l'import sans distribuer une seconde fois le badge ou
les Omégas.

### 4. Restituer et entrer dans le Monde 0

La page finale distingue les nouveaux imports des éléments déjà présents, confirme que les
données personnelles restent privées et ouvre le Monde 0. C'est à ce seuil que la voix peut
basculer du registre public vers le tutoiement du Jeu.

## Surfaces d'invitation

Le même tunnel peut être appelé depuis plusieurs endroits sans rendre le site répétitif :

| Moment | Forme | CTA recommandé |
|---|---|---|
| Aucun parcours accompli | CTA stable de `/entrer` et de l'en-tête | `Créer mon espace` |
| Fin du premier parcours | Panneau principal après la restitution | `Conserver ce passage` |
| Retour ultérieur | Rappel discret dans l'en-tête ou sur l'accueil | `1 badge · 5 Ω à ancrer` |
| Plusieurs parcours | État local synthétique | `Conserver mes passages` |
| Cinq parcours accomplis | Constellation complète et invitation forte | `Faire entrer ma constellation dans le Jeu` |
| Depuis un événement ou une page Agir | Invitation contextualisée, sans inventer de récompense | `Créer mon espace Point Zéro` |

L'invitation ne doit jamais recouvrir le contenu, interrompre un parcours ou laisser croire
que l'inscription est nécessaire pour obtenir son résultat public.

## Données locales minimales

Pour chaque parcours : identifiant stable, version, date d'accomplissement, badge reconnu,
Puissance associée, quantité d'Omégas, langue, état d'import et identifiant d'import si
présent. Les réponses détaillées restent dans le contrat propre au parcours et ne doivent pas
être utilisées pour inférer un profil psychologique ou politique.

## Conditions d'ouverture des inscriptions

Avant de remplacer le CTA actuel de connexion :

1. route d'inscription publique disponible et testée ;
2. CGU et politique de confidentialité acceptables en ligne ;
3. format local des cinq parcours stabilisé ;
4. import idempotent livré avec journal de restitution ;
5. gestion explicite des erreurs et reprise sans perte ;
6. tests mobile, multi-onglets, navigation privée et changement d'appareil ;
7. mesure des abandons sans envoyer le contenu personnel des réponses.

## Hors périmètre du premier lot

- profil communautaire détaillé pendant l'inscription ;
- exposition publique des Graines ou Traces ;
- objectif collectif du million d'Omégas ;
- économie du Commun et capacité de financement ;
- parcours caché comme condition d'inscription.
