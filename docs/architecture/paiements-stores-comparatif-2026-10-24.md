# Comparer les paiements intégrés et externalisés pour Point Zéro

> Note Codex — 24 octobre 2026. Analyse demandée par Boris. Hypothèse de lancement
> en France et UE/EEE ; recommandation à arbitrer, pas décision d’implémentation.
> Aucun compte développeur, contrat ou tarif personnalisé consulté.

## Recommandation pour le lancement

**M1 : achat intégré lorsqu’on souscrit depuis l’application ; Stripe lorsqu’on
souscrit directement sur le site.** Le serveur Point Zéro centralise les droits
M1, quel que soit l’origine de l’achat. Une personne déjà abonnée ne doit pas
payer une deuxième fois sur un autre appareil.

Cette recommandation privilégie un parcours sans sortie de l’application et
limite les obligations supplémentaires des programmes de renvoi externe. Elle
ne signifie pas que le site doit cesser de vendre M1. Réexaminer les liens
externes depuis l’app lorsque le volume, les tarifs et la conversion seront connus.

M0 reste gratuit. L’Atelier présentiel conserve une billetterie Stripe distincte.
Pour l’Atelier collectif en ligne vendu depuis l’app, examiner les règles
applicables aux services collectifs numériques, pas celles du présentiel.

## Trois circuits à ne pas confondre

| Circuit | Parcours | Ce qu’il faut comparer |
|---|---|---|
| Achat intégré | App → achat Apple/Google → droits M1 | Commission, intégration native et gestion des droits |
| Renvoi externe | App → dispositif autorisé → site/Stripe → retour app | Commission du store possible + Stripe + API, reporting et assistance |
| Vente web indépendante | Site/événement/courriel → site/Stripe → connexion dans l’app | Stripe et gestion web ; ne pas la traiter automatiquement comme une vente attribuée à un lien dans l’app |

Un paiement web indépendant n’est pas synonyme d’autorisation de retirer toute
possibilité d’achat du binaire iOS. Pour les services multiplateformes Apple,
les conditions d’accès et les options de paiement proposées dans l’app comptent.
[Apple, section 3.1](https://developer.apple.com/app-store/review/guidelines/#business).

## Frais publiés vérifiés

Les chiffres suivants sont ceux des pages officielles consultées le 24 octobre.
L’admission de PZ aux programmes réduits n’a pas été vérifiée : elle doit être
obtenue, pas déduite de la création récente des comptes entreprise.

| Plateforme ou circuit | Achat intégré | Paiement alternatif ou lien externe |
|---|---|---|
| Apple, UE, participant Small Business | 15 % | 10 % pour les transactions concernées, plus les frais du prestataire |
| Apple, UE, hors programmes réduits | 26 % ; taux réduit prévu pour les abonnements renouvelables après leur première année | Paiement alternatif dans l’app : 20 % ; lien externe : 15 %, plus prestataire ; cas réduits précisés par Apple |
| Google Play, France/EEE, abonnement à renouvellement automatique | 10 % de service + 5 % de facturation = 15 % | 10 % de service, plus prestataire, via programme applicable |
| Google Play, premier palier de 1 M USD, autres achats | 10 % + 5 % = 15 % | 10 % plus prestataire ; hors palier, tarif selon produit et installation |
| Stripe, carte EEE standard | Sans objet | 1,5 % + 0,25 euro par encaissement ; Billing à l’usage ajoute 0,7 % si utilisé |

Les taux Apple UE proviennent de la page des conditions entrées en vigueur
le 1er octobre 2026. Les chiffres Google cités sont ceux du déploiement EEE de
2026 ; les anciens calculs automatiques « commission moins 3 ou 4 points » ne
sont pas une base suffisante pour le programme retenu.
[Apple UE](https://developer.apple.com/support/payment-options-on-the-app-store-in-the-eu/),
[Small Business](https://developer.apple.com/app-store/small-business-program/),
[Google, frais](https://support.google.com/googleplay/android-developer/answer/112622?hl=en),
[Stripe France](https://stripe.com/fr/pricing).

La formule annuelle PZ n’a pas encore de règle de renouvellement précisée.
Ne pas lui appliquer automatiquement le régime d’un abonnement renouvelable.
Le palier Google et l’admission Small Business Apple sont donc importants.

## Simulation du premier encaissement attribué au renvoi

**Hypothèses pédagogiques, pas tarifs PZ** : même assiette de calcul P, TVA
neutralisée ; achat intégré à 15 % ; commission externe à 10 % lorsque la vente
est attribuable au renvoi ; Stripe carte EEE standard et Billing à l’usage,
soit 2,2 % + 0,25 euro. Frais de taxe, litiges, remboursements, conversion,
logiciel tiers et développement exclus. Ce n’est pas un calcul de revenu net TTC.

| Assiette fictive | Frais intégrés 15 % | Frais externes attribués 12,2 % + 0,25 euro | Gain du renvoi |
|---:|---:|---:|---:|
| 20 euros | 3,00 euros | 2,69 euros | 0,31 euro |
| 200 euros | 30,00 euros | 24,65 euros | 5,35 euros |

Si la vente est véritablement indépendante du renvoi et qu’aucune commission
store n’est due, Stripe + Billing seul donne respectivement 0,69 et 4,65 euros
dans ce modèle. Le canal d’acquisition fait donc une différence majeure.

Apple publie une fenêtre de sept jours après le lien pour la commission sur
les offres externes ; Google publie une fenêtre de 24 heures dans les programmes
cités. **Ne pas appliquer 10 % à tous les renouvellements à vie**, ni présumer
leur gratuité : tracer et appliquer les conditions du contrat retenu. Cette
simulation n’extrapole pas la valeur totale d’un abonnement.
[Apple, commissions et reporting](https://developer.apple.com/support/payment-options-on-the-app-store-in-the-eu/#commissions-reporting-and-payments),
[Google Billing Choice](https://support.google.com/googleplay/android-developer/answer/17161464?hl=en-GB),
[Google External Offers](https://support.google.com/googleplay/android-developer/answer/14372887).

## Développement et expérience utilisateur

| Sujet | Paiement intégré | Paiement externalisé depuis l’app |
|---|---|---|
| Souscription | Reste dans le parcours natif ; avantage UX attendu à mesurer | Passage vers le site, connexion/paiement et retour à fiabiliser |
| Technique | StoreKit et Play Billing ; validation serveur et notifications de cycle de vie | Stripe ne suffit pas : programmes, API, attribution et déclarations supplémentaires |
| Annulation et assistance | Gestion de l’achat dans son store, selon ses règles | PZ porte le portail, les remboursements et l’assistance du paiement externe |
| Territoires et appareils | Options natives avec tests iOS/Android | Règles par région, version de système et programme ; davantage de cas à tester |
| Comptabilité | Plusieurs sources de ventes à rapprocher | Facturation Stripe et rapprochement avec les commissions stores attribuées |

Un programme de lien externe n’est pas nécessairement plus simple à développer
que l’achat intégré. Dans Billing Choice, Google exige aussi de proposer Play
Billing. External Offers EEE est un programme distinct qui exclut au contraire
Play Billing. Le choix du programme précède donc l’implémentation.
[Google Billing Choice](https://support.google.com/googleplay/android-developer/answer/17161464?hl=en-GB),
[Google External Offers](https://support.google.com/googleplay/android-developer/answer/14372887).

Apple exige des autorisations/API et du reporting pour ses options alternatives.
Ses règles UE des services multiplateformes ne se résument pas à un bouton vers
le navigateur ; elles prévoient une possibilité de paiement dans l’app. Le choix
est à maintenir pendant douze mois dans les conditions publiées. Cela réduit
l’intérêt d’un détour externe improvisé pour la première version.
[Apple UE](https://developer.apple.com/support/payment-options-on-the-app-store-in-the-eu/).

Google permet par ailleurs une application sans achat, donnant accès à un service
payé ailleurs. C’est une vraie variante pour Android si toutes les ventes sont
acquises hors app. Ce n’est pas une exemption générale aux règles des liens
externes, ni une réponse automatique pour le jeu iOS.
[FAQ Google](https://support.google.com/googleplay/android-developer/answer/10281818?hl=en).

## Atelier et modèle PZ

- **M0 gratuit** : conserver un parcours complet gratuit et l’information claire
  sur l’accès payant à l’Atelier/M1.
- **Atelier présentiel** : service vécu hors app ; billetterie distincte via Stripe.
- **Atelier collectif en ligne** : ne pas utiliser automatiquement l’exception
  du service physique ou du tête-à-tête. Apple distingue les services individuels
  en temps réel des services à plusieurs. Décrire la prestation et son mode
  de vente avant de fixer le circuit.
- **M1 numérique** : mensuel et annuel à mapper aux produits adéquats. Ne pas
  inventer d’auto-renouvellement pour l’annuel ; dates, prix et réduction restent
  à fixer avant construction des produits.
[Apple, section 3.1.3](https://developer.apple.com/app-store/review/guidelines/#business),
[Google, politique de paiements](https://support.google.com/googleplay/android-developer/answer/9858738?hl=en).

## Travail nécessaire avant implémentation

1. Boris valide le circuit recommandé et les territoires de lancement.
2. Vérifier les programmes/tarifs effectivement disponibles dans les comptes PZ.
3. Fixer les prix, la réduction annuelle et son renouvellement éventuel.
4. Décrire le produit Atelier en ligne et ses offres groupées éventuelles.
5. Préparer un contrat de droits M1 commun aux achats web, Apple et Google :
   validation serveur, expiration, remboursement, rétablissement, changement
   d’appareil et protection contre un double abonnement.
6. Faire chiffrer au portable l’achat intégré et l’externe sur le même périmètre.

Aucun frais de développement chiffré n’est inventé ici ; aucune commission réduite
n’est tenue pour acquise au nom de PZ. L’option recommandée reste une proposition,
avec réexamen après mesure de la conversion et de la marge.
