# M0 · E9 — Composer le Profil communautaire

> **Ajout Codex — décision validée par Boris le 13 septembre 2026.**
> Ce contrat remplace, pour le premier geste de « Choisir ma place parmi les
> autres », la confirmation de visibilité par la composition effective du
> Profil communautaire.

## 1. Décision

Le CTA **« Composer mon Profil »** ouvre `/users/me/edit`, dans le contexte de
l'excursion d'E9. La simple ouverture de la page ne prouve rien. Le geste est
reconnu après une sauvegarde réussie d'un profil communautaire minimal.

Les réglages de `/profils/visibilite` restent accessibles et révocables, mais
ils deviennent facultatifs pour la progression. Le marqueur
`m0-visibilite-confirmee` ne prouve plus ce geste, n'ouvre plus l'étape suivante
et n'attribue plus le seuil de Communication.

## 2. Profil minimal

Le profil est composé lorsque les deux conditions suivantes sont réunies :

1. `presentation` est non vide après normalisation des espaces ;
2. au moins un de ces quatre champs est non vide : `centres_interet`,
   `ce_qui_mamene`, `ce_que_je_cherche`, `ce_que_je_rends_possible`.

`prenom` reste l'obligation générale déjà portée par `User`; elle ne devient
pas une nouvelle règle de parcours. Restent facultatifs : photo, nom,
civilité, territoire, langues, année d'entrée, liens externes, préférence de
rencontre, téléphone, politique de contact, canal et appels.

Ne pas ajouter ces conditions aux validations globales de `User`. Le formulaire
doit pouvoir enregistrer un brouillon incomplet ; il indique alors ce qui
manque et l'étape reste **En cours**. Ne pas noter le contenu, ni lui imposer un
seuil de longueur arbitraire : la présence de deux contributions enregistrées
est la preuve attendue.

Ces contributions de base apparaissent sur le Profil communautaire actuel. La
page doit donc le dire avant l'enregistrement. Les réglages facultatifs de
visibilité continuent de régir séparément les œuvres, Traces, badges et mentor.

## 3. Preuve et progression

Créer un prédicat unique, réutilisable par les contrôleurs et services, par
exemple `User#profil_communautaire_compose?`. Après un `UsersController#update`
réussi qui satisfait ce prédicat, poser un fait dédié
`m0-profil-compose`. Ne jamais le poser sur un GET ni sur une sauvegarde
incomplète.

Le fait est historique : effacer ou modifier plus tard une présentation ne
retire pas un geste déjà accompli. Pour les profils existants, la preuve peut
lire `m0-profil-compose` **ou** le prédicat tant que la mise en service n'a pas
rattrapé les profils déjà complets. Auditer les comptes avant tout rattrapage ;
ne retirer ni validation, ni Oméga, ni badge déjà acquis.

Le contrat d'E9 devient :

- rang 1 : profil communautaire composé ;
- rang 2 : appartenance active à l'Espace du Monde 0 et première réaction
  persistée ;
- rang 3 : Annuaire facultatif, jamais condition de validation.

Le contrôle global de l'expérience lit donc `profil composé + appartenance +
réaction`. La condition `visibilite_confirmee` de la carte Communication devient
`profil_compose` afin que l'Espace s'ouvre après le même fait que l'étape 1.

Le badge **Présence choisie** suit également `m0-profil-compose`. Sa description
devient : **« Tu as composé la présence depuis laquelle la communauté peut te
rencontrer. »** Les attributions historiques restent intactes.

## 4. Textes d'E9, rang 1

- **libellé / titre** : `Compose ton Profil`
- **accroche** : `Choisis comment te présenter aux autres.`
- **explication** : `Écris une courte présentation et complète au moins un repère sur ce qui t’amène, ce que tu explores, ce que tu cherches ou ce que tu aimerais rendre possible. Ces éléments seront lisibles sur ton Profil communautaire ; tes œuvres, Traces, badges et mentor gardent leurs réglages de visibilité séparés.`
- **CTA** : `Composer mon Profil`
- **sortie** : `profil communautaire minimal enregistré.`
- **reconnaissance** : `présentation et au moins un repère enregistrés — contrôleur du profil.`

La durée de 5 minutes et les autres champs de l'expérience restent inchangés.

## 5. Navigation cible

`/users/me/edit` quitte la rubrique **Paramètres du compte** et rejoint le
territoire Communication. Il reprend la même barre de rubrique et les mêmes
onglets que l'aperçu et la visibilité :

1. **Composer mon profil** — `/users/me/edit` ;
2. **Aperçu communautaire** — `/profils/apercu` ;
3. **Visibilité** — `/profils/visibilite`.

Le formulaire se répartit en trois ensembles :

- **Ma présence** : présentation et repère nécessaires, avec la condition
  visible et un état de complétion ;
- **Pour me rencontrer** : informations facultatives ;
- **Contact et préférences** : informations facultatives et consentements
  explicites.

La sous-navigation technique `Paramètres du compte · Connexion & sécurité ·
Notifications · CGU` disparaît de cette page. Dans le menu avatar, l'entrée
actuelle `Paramètres du compte` devient **Mon profil communautaire**, avec un
libellé secondaire consacré à la présentation. Le groupe technique conserve
Connexion et sécurité, Notifications et rythme, Personnalisation et mémoires,
CGU et consentements. Ne pas créer une page « Paramètres » vide uniquement pour
conserver l'ancien mot.

## 6. Retour d'excursion

La sauvegarde de `/users/me/edit` redirige aujourd'hui vers `/users/me`, donc le
Moteur. Dans l'excursion d'E9 :

- sauvegarde complète : passer par la route de retour de l'excursion afin de
  fermer proprement le contexte, laisser un éventuel éveil s'interposer, puis
  revenir à l'expérience et afficher la reconnaissance du rang 1 ;
- brouillon incomplet : rester sur l'éditeur, conserver l'excursion et montrer
  la condition manquante ;
- édition hors excursion : revenir à l'Aperçu communautaire, destination qui
  montre immédiatement le résultat de la sauvegarde.

Ne pas recalculer une URL depuis le `referrer` et ne pas fermer la session
d'excursion directement dans `UsersController` : utiliser le mécanisme commun
déjà porté par `ExcursionsController#revenir`.

## 7. Analyse d'impact et recette

Zones concernées : porte et preuve de `ExperienceState` / `SequenceDeGestes`,
`UsersController#update`, état Communication de `Monde0Etats`, YAML M0,
catalogue du seuil, formulaire et navigation du profil, menu avatar et bancs.
Ne modifier ni les règles du rang 2, ni la validation globale hors E9, ni les
Omégas, ni la visibilité réelle des contenus.

Cas minimaux à protéger :

1. ouvrir l'éditeur ou enregistrer seulement le prénom ne valide rien ;
2. présentation seule : brouillon enregistré, rang 1 encore en cours ;
3. présentation + un repère : rang 1 reconnu une fois ;
4. modifier seulement la visibilité ne change plus la progression ;
5. un profil déjà complet est reconnu sans nouvelle saisie ;
6. un ancien E9 validé reste validé ;
7. appartenance sans réaction ne ferme pas E9 ; la première réaction la ferme ;
8. depuis l'excursion, le retour mène à E9 et l'animation de reconnaissance est
   visible ; hors excursion, la sauvegarde mène à l'aperçu ;
9. contrôles ordinateur, 700 px et 390 px, clavier, erreurs et brouillon.

## 8. Répartition

- **Portable** : prédicat, fait, preuve, compatibilité des comptes, état
  Communication, badge, retour d'excursion et bancs métier.
- **Poste fixe** : formulaire, navigation Communication, menu avatar, états
  incomplet/complet, responsive et accessibilité, après accord sur les noms
  exacts exposés par le portable.
