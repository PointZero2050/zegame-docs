# Revalidation des CGU — textes de l'écran

> Note Codex — livraison éditoriale du 21 octobre 2026 pour le poste fixe et le portable.
> Répond aux demandes sur #450 et #442. À intégrer et vérifier en préproduction ;
> ce document ne publie ni les textes juridiques ni l'interrupteur de revalidation.

## Sources et périmètre

Écran relu dans la PR [#450](https://github.com/PointZero2050/pointzero-app/pull/450),
révision `f3fa352180e9509d54ed04efd2c02b8ad95cf5f4` ; contrôleur relu sur
`preprod` à `e59ebf2d92399f6224e0b42bd2ec1774ac967e3f`. Les ajouts aux articles
9 et 15, les versions CGU 1.1 / confidentialité 1.2 et la réacceptation demandée
par Boris proviennent de [#442](https://github.com/PointZero2050/pointzero-app/pull/442),
révision `61e069ea5e497a8a22f10c0bb4ebe8e1cca97d28`.

Les valeurs entre crochets ci-dessous sont dynamiques. Employer `@version`,
`@entree_en_vigueur` et `@deja_acceptee`, sans figer la date proposée dans #442.
Ne présenter une version comme applicable qu'avec le texte correspondant servi.
La variante dépend de l'enregistrement retrouvé, pas de l'origine du compte.

## Variante : une version antérieure a été acceptée

**Surtitre** : Conditions générales

**Titre** : Les conditions du Jeu évoluent.

**Introduction** :

> La version [version en vigueur], applicable à partir du [date], remplace la
> version [version déjà acceptée] que tu avais acceptée. Elle précise notamment
> la place des regards IA dans les échanges et les règles de modération. Prends
> le temps de la lire avant de renouveler ton acceptation.

**Intertitre** : Ce qui évolue

- Un mentor ou un Enfant Libre peut rejoindre certains fils comme regard IA, à
  l'invitation d'un facilitateur ou d'un administrateur habilité.
- Tu choisis séparément, pour chaque regard dans chaque fil, s'il peut lire tes
  nouveaux messages. Tu peux refuser ou retirer ton accord et continuer à échanger.
- Les conditions précisent comment signaler une réponse IA et dans quels cas
  elle peut être masquée pour tous. La politique de confidentialité détaille
  l'utilisation des données.

Ce résumé ne remplace pas les textes complets, accessibles juste après.

## Variante : aucune acceptation n'est enregistrée

**Surtitre** : Conditions générales

**Titre** : Avant de continuer dans le Jeu

**Introduction** :

> Les conditions générales définissent le cadre du Jeu et des échanges. La
> politique de confidentialité explique l'utilisation de tes données. Lis ces
> textes, puis accepte les conditions pour continuer.

**Métadonnées sous l'introduction** :

> Conditions générales · version [version en vigueur] · applicables à partir du [date]

Ne pas écrire « tu n'as jamais accepté » : l'absence d'enregistrement suffit à
présenter ce premier recueil, sans attribuer au joueur un comportement passé.
Le résumé « Ce qui évolue » est réservé à la première variante.

## Partie commune aux deux variantes

Liens explicites, avant la case :

- **Lire les conditions générales** → `/cgu`.
- **Lire la politique de confidentialité** → `/politique-de-confidentialite`.

**Note avant la case**, visible sans ouvrir d'aide :

> Accepter les CGU n'autorise pas un regard IA à lire tes messages. Ce choix se
> fait séparément dans chaque fil.

**Case, décochée à l'ouverture** :

> J'accepte les conditions générales d'utilisation et j'ai pris connaissance de
> la politique de confidentialité.

**CTA** : Accepter et continuer →

**Sous le CTA** : Après acceptation, tu retrouves le Jeu.

Cette formulation couvre aussi le retour de secours vers l'accueil lorsque la
page initialement demandée n'est plus disponible en session. Conserver la
destination réelle du contrôleur, sans forcer un retour vers M0 pour un compte M1.

## Encadré des autres issues

**Surtitre** : Tes autres choix

**Titre** : Prends le temps de choisir.

| Lien | Complément |
| --- | --- |
| Lire les conditions générales | Le texte complet de la version [version en vigueur]. |
| Lire la politique de confidentialité | L'utilisation de tes données et tes droits. |
| Poser une question | L'aide reste accessible. |
| Fermer mon compte | Consulter la procédure et ses conséquences avant de confirmer. |
| Me déconnecter | Revenir plus tard. |

Conserver les routes déjà prévues : aide `/aide`, procédure
`fermeture_personnalisation_path`, déconnexion en DELETE. Le lien de fermeture
ouvre la procédure existante, il ne supprime pas immédiatement le compte.
Ne pas promettre l'effacement de toutes les contributions collectives.

## Avis du contrôleur — portable

**Tentative sans case cochée** :

> Coche la case pour accepter les conditions générales et continuer dans le Jeu.

**Confirmation, uniquement après enregistrement réussi** :

> Ton acceptation des conditions générales a été enregistrée.

Le POST, le nom `cgu`, la valeur `1` et le mécanisme d'enregistrement restent
ceux du contrat serveur. Aucune acceptation au chargement de la page ni par
simple poursuite de navigation. Ne pas enregistrer une autorisation IA à cette occasion.

## Repères de recette

Vérifier les deux variantes, les versions/dates réellement servies, les deux
textes complets, l'aide, l'ouverture de la procédure de fermeture et la
déconnexion. Vérifier le refus sans écriture, puis le retour après succès.
Les pages d'événement restent accessibles selon le contrat du portable.
Les choix individuels de regards ne sont pas modifiés par ce formulaire.

Le libellé distingue l'acceptation contractuelle de l'information sur les données.
Il ne transforme pas la politique de confidentialité en consentement général :
la CNIL rappelle qu'un consentement doit correspondre à une finalité précise et
pouvoir être retiré. [Référence CNIL](https://www.cnil.fr/fr/les-bases-legales/consentement).
