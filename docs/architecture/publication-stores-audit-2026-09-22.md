# Publier Point Zéro sur les stores — audit technique du 22 septembre 2026

Demande de Boris : « préparer la publication de l'appli sur les stores Google et Apple ; les
comptes organisation sont créés ; audit technique pour identifier les points à traiter pour une
première soumission ».

Tout ce qui suit est **mesuré sur la production** (`pointzero2050.com`, `9eb0706` → `a74a300`) ou
lu dans `pointzero-app`, le 22 septembre 2026 au soir. Les points marqués ⚠️ bloquent une
soumission ; les points ⓘ sont des décisions qui reviennent à Boris.

---

## 0. La vérité de calendrier, d'abord

**Le Festival est le 1er octobre 2026 : dans neuf jours.** Une première soumission ne tiendra pas
ce délai, et il faut le dire avant de planifier quoi que ce soit :

- il n'existe **aucun projet natif** aujourd'hui (ni iOS, ni Android, ni Capacitor — vérifié) ;
- Apple demande un binaire signé, un compte de démonstration, une fiche complète, et une revue
  dont le délai usuel est de 24 à 48 h **mais qui n'est pas garanti sur une première soumission
  d'organisation** ;
- Google demande la même fiche, plus les déclarations de sécurité des données.

**Pour le Festival, la voie réaliste est celle déjà en place : le site installable (PWA).** Le
manifeste et le service worker existent, Android propose déjà « Ajouter à l'écran d'accueil », et
iOS le permet depuis Safari. Les stores sont un chantier d'octobre, pas de septembre — et c'est
tant mieux : soumettre une application dans la semaine du Festival, c'est déployer sans pouvoir
corriger, parce qu'entre deux corrections il y a désormais une revue.

---

## 1. La décision qui commande tout le reste : comment un Rails arrive sur un store

Point Zéro est une application Rails 8 rendue au serveur (HAML + Turbo + Stimulus). Trois voies
existent, et elles ne se valent pas.

| Voie | Android | iOS | Ce qu'elle coûte | Risque de refus |
|---|---|---|---|---|
| **A. PWA seule** | installable aujourd'hui | installable depuis Safari | zéro | — (hors store) |
| **B. TWA / webview nue** | acceptée par Google | **refusée par Apple** (règle 4.2, « minimum functionality ») | faible | **élevé côté Apple** |
| **C. Hotwire Native** | coquille native + Turbo | coquille native + Turbo | un projet par plateforme | faible |

**Recommandation : la voie C, Hotwire Native** (l'ancien Turbo Native, maintenu par 37signals pour
exactement ce cas). Raisons mesurables, pas de préférence :

1. **Apple refuse les sites emballés.** La règle 4.2 exige qu'une application apporte autre chose
   qu'un navigateur : navigation native, notifications, hors-ligne, intégrations système. Une TWA
   passe chez Google et se fait refuser chez Apple — ce serait payer deux fois le même travail.
2. **Nous avons déjà Turbo partout.** Hotwire Native consomme les pages telles quelles, remplace la
   navigation par une pile native, et permet de remplacer écran par écran (`path configuration`)
   ce qui mérite du natif. Aucune réécriture, aucun second front à maintenir.
3. **Un seul serveur, un seul canon.** Les bancs continuent de mesurer ce que les joueurs voient,
   parce que c'est la même page.

ⓘ **Décision de Boris** : accepter ce coût (deux projets natifs à maintenir, deux signatures, deux
revues) ou rester en PWA. Tant qu'elle n'est pas prise, tout le reste de cet audit vaut quand même :
les points ci-dessous sont des dettes du SITE, pas de la coquille.

---

## 2. ⚠️ Les bloquants applicatifs (à construire avant toute soumission)

### 2.1 ⚠️ La suppression de compte n'existe pas

Mesuré : `devise_for :users, path: "comptes", skip: [:registrations]` — il n'y a **aucun chemin de
suppression de compte** dans l'application, et aucune vue ne l'offre.

Or les deux stores l'exigent **quand l'application permet de créer un compte** — et c'est notre
cas (`POST /billet/:jeton` → `billets#creer_compte`) :

- **Apple, règle 5.1.1(v)** : la suppression doit être *dans l'application*, pas seulement par
  courriel, et elle doit supprimer le compte, pas seulement le désactiver ;
- **Google Play, Data deletion** : un chemin dans l'application **et** une URL web de demande.

⚠️ **Ce n'est pas `raz_compte.rb`.** Ce script remet un compte à zéro (il garde le compte, son mot
de passe, ses communautés) : c'est l'outil d'une recette, pas une suppression. Il en fournit
cependant la moitié difficile — la lecture du schéma qui trouve **toutes** les tables portant le
joueur, couples polymorphes compris. Le lot à écrire :

- un écran « Supprimer mon compte » (double confirmation, mot de passe redemandé) ;
- la suppression effective, plus l'**anonymisation** de ce qui appartient au collectif : les
  messages d'un Espace partagé ne peuvent pas disparaître sans trouer les fils des autres — il faut
  un auteur « Joueur supprimé » (le canal du Monde 0 en portait 60 le 22 septembre, et leur état
  montre exactement ce qu'il ne faut pas laisser) ;
- ce que la suppression NE peut pas emporter (facture Stripe, obligation comptable) doit être
  nommé dans la politique de confidentialité ;
- un banc : le compte part, ses faits partent, le fil des autres tient debout.

### 2.2 ⚠️ Les paiements : ce que nous vendons, et où il faut le vendre

Mesuré : `StripeCheckout` crée une session `mode: "payment"` au prix de l'événement, et
`registrations#demarre_paiement` fait une **redirection pleine page** vers `checkout.stripe.com`.

- **Ce que nous vendons est un billet pour un événement réel.** Les deux stores l'autorisent hors
  achat intégré : Apple (3.1.3(e), services du monde réel) et Google traitent le billet comme un
  bien physique. **Aucune commission de 30 % n'est due**, et c'est la bonne nouvelle.
- ⚠️ **La règle se retourne dès qu'on vend du numérique.** Un Oméga acheté, un chapitre débloqué
  contre paiement, un abonnement au Jeu : tout cela devient un achat intégré obligatoire chez
  Apple. Aujourd'hui les Ω se gagnent et rien de numérique ne se vend — **cette ligne doit être
  tenue, ou le modèle change**.
- ⚠️ **Le paiement ne doit pas se jouer dans la webview.** Dans une coquille native, un `redirect_to`
  vers `checkout.stripe.com` sort du domaine : il faut l'ouvrir dans le navigateur système
  (`SFSafariViewController` / Custom Tabs). C'est une ligne de configuration côté coquille, mais
  c'est un refus assuré si on l'oublie (3-D Secure casse, et le joueur se retrouve coincé).
- ⓘ Apple exige aussi, pour les biens du monde réel achetés hors IAP, qu'aucun écran n'invite
  explicitement à « payer moins cher sur le site » (anti-steering). Le parcours actuel n'en parle
  pas ; il ne faudra pas commencer.

### 2.3 ⚠️ L'IA — trois surfaces, et les stores les regardent de près

Mesuré : `AvatarReponse`, `GuideReponse` et `MentorReponse` envoient du texte du joueur à Anthropic.

- **Contenu généré = modération obligatoire** (Apple 1.2, Google UGC). Nous avons déjà de quoi
  répondre : `/aide`, `POST /signalements`, le blocage dans les fils, le signalement d'un appel de
  Guide. Il faut le **rendre visible depuis chaque surface d'IA**, et le déclarer dans la fiche.
- **Classification d'âge** : une IA conversationnelle pousse la classification vers le haut chez
  Apple. ⓘ Boris tranche la cible (le Jeu s'adresse à des adultes ; la fiche doit le dire).
- **Déclaration de partage de données** : le texte du joueur part chez un tiers (Anthropic). C'est
  à déclarer dans les deux formulaires, et la politique de confidentialité doit le nommer
  explicitement. Elle parle déjà d'IA ; il faudra vérifier mot pour mot qu'elle nomme le
  sous-traitant et la finalité.

### 2.4 ⚠️ Le compte de démonstration pour la revue

Apple **rejette** une application dont le contenu est derrière un compte sans identifiants de test.

- Notre création de compte passe par un **billet** (`/billet/:jeton`) : un relecteur ne peut pas
  s'inscrire seul.
- Et `acces-verification`, notre entrée sans mot de passe, est **fermée en production** (mesuré :
  la variable d'environnement n'y est pas — et elle doit le rester).
- À prévoir : un compte de démonstration permanent, avec mot de passe, **de rôle joueur**, déjà
  avancé dans le Monde 0 pour que la revue voie le Jeu ; ses identifiants vont dans les notes de
  revue, pas dans le dépôt.

---

## 3. Ce que le site doit corriger, mesuré aujourd'hui

| Point | État mesuré | Pourquoi il compte |
|---|---|---|
| ⚠️ `config.force_ssl` | **désactivé** (commenté) | Le cookie de session sort **sans `Secure`** (`path=/; httponly; samesite=lax`) et **aucun HSTS** n'est servi. Caddy redirige bien le HTTP en 308, mais l'application ne borne rien elle-même. |
| ⚠️ CSP | **aucune** (initialiseur entièrement commenté) | Pas un bloquant de store, mais une webview qui charge un tiers sans politique est une surface offerte. |
| ⚠️ `assetlinks.json` / `apple-app-site-association` | **404 tous les deux** | Sans eux : pas de TWA vérifiée, pas d'Universal Links, et les liens du Jeu (courriels, billets) rouvrent le navigateur au lieu de l'application. |
| ⓘ Service worker | **minimal, sans cache** | Suffit à l'installabilité Android. Ne sert à rien sur iOS (WKWebView n'exécute pas les service workers) : le hors-ligne d'une coquille iOS est un autre chantier. |
| ⓘ Icônes | 192 et 512 présentes | Il manque le **1024×1024** d'App Store, les jeux d'icônes natives, et les captures d'écran par taille d'appareil. |
| ✔ Pages légales | `/cgu` **200**, `/politique-de-confidentialite` **200** | Les deux stores demandent ces URL ; elles existent et répondent. |
| ✔ Santé | `/up` **200** | Utile aux sondes et aux coquilles. |
| ⓘ Session | Devise `rememberable` actif, `remember_for` laissé au défaut | Dans une application installée, on ne se reconnecte pas toutes les deux semaines : à rallonger, et à éprouver. |

---

## 4. Le dossier, côté stores (les comptes organisation sont créés)

**Apple** : identifiant d'application et profils de signature ; build via Xcode/TestFlight ;
captures par taille d'écran ; description, mots-clés, catégorie ; **App Privacy** (étiquettes de
données, Anthropic et Stripe compris) ; classification d'âge ; URL d'assistance et de
confidentialité ; **compte de démonstration** ; notes de revue expliquant le Festival et le billet.

**Google Play** : signature d'application (Play App Signing) ; fiche et captures ; **Data safety**
(collecte, partage, suppression) ; questionnaire de contenu ; politique de confidentialité ;
déclaration IA ; **test fermé** avant production selon le type de compte (à vérifier sur le compte
organisation, la règle des 12 testeurs vise les comptes personnels).

---

## 4 bis. ✅ FAIT le 23 septembre — lots 1 et 2, en production (`54370c4`)

Boris a tranché : **on publie avant le Festival, le web en secours.** Les deux premiers lots sont
livrés et promus ; ce qui suit remplace leur description au futur.

- ⚠️ **§2.1 ÉTAIT FAUX, ET C'EST MA FAUTE.** J'ai écrit « la suppression de compte n'existe pas »
  après avoir cherché dans le code d'authentification et dans les boîtes des agents — pas dans ce
  dossier, où vivait la décision. **Elle existait** : `FermetureDeCompte`, la page du poste fixe,
  un banc de 45 assertions, et l'arbitrage de Boris du 7 septembre
  ([analyse d'impact](suppression-de-compte-analyse-impact.md)) : *« anonymisé, pas effacé »*.
  J'ai construit un second chemin qui EFFAÇAIT, et les deux ont coexisté en production le
  23 septembre, avec des promesses contradictoires.
  ⓘ **Ce qui l'avait rendue invisible** : la décision n'était pas BRANCHÉE — la page répondait,
  son banc était vert, et aucun lien n'y menait.
  **Réparé le 23 sur la parole de Boris** (« Option A, techniquement on effacera les données
  personnelles ») : le menu mène à `/personnalisation/fermeture`, mon chemin est retiré, la page
  publique `/suppression-de-compte` décrit la fermeture (l'URL garde le mot que Google attend, le
  texte dit ce qui se passe), et `verifier_fermeture_de_compte` gagne la moitié « stores » — le
  chemin se TROUVE depuis le menu, la page publique répond sans session.
- **Le durcissement est en place** (§3) : `assume_ssl` + `force_ssl`, cookie de session `secure`,
  HSTS un an borné à l'apex, `/up` exclu de la redirection. ⚠️ **La CSP est en observation** :
  mesuré au navigateur, deux scripts EN LIGNE violent `script-src 'self'` — en blocage, le Jeu
  casserait. La refermer demande de sortir ces scripts des vues (zone du poste fixe).
- **Les deux fichiers de liens profonds sont servis** (§3), par variables d'environnement, et
  répondent **404 tant que les identifiants réels manquent** — publier un fichier faux, c'est le
  faire mettre en cache chez Google et Apple.
- **Au passage** : huit courriels différés étaient morts en production (33 en préprod), tous
  `DeserializationError` — un sujet disparu pendant le délai. `LivraisonDeCourriel` les abandonne
  en le disant. La suppression de compte rendait cette course courante : corrigée avant de la livrer.

⚠️ **CE QUI BLOQUE, ET CE N'EST PLUS DU CODE.** État au 24 septembre, relevé dans la Play Console
avec Boris :

| À fournir | D'où il vient | État |
|---|---|---|
| `ANDROID_PACKAGE` | Play Console | ✅ **`com.pointzero2050.app`**, posé les 24 septembre sur les deux serveurs |
| `ANDROID_SHA256` | Play Console → Signature d'application | ✅ **posée**, et le fichier servi est **identique au bloc que Google génère** (comparé programme contre programme) |
| `APPLE_TEAM_ID` | Apple Developer → Membership | ⏳ manquant |
| `APPLE_BUNDLE_ID` | choix de Boris, déclaré dans App Store Connect | ⏳ manquant |

Et une décision : **le compte de démonstration pour la revue** (§2.4) — quelle adresse, et qui
reçoit le courriel de mot de passe. Le compte sera de rôle joueur et avancé dans le Monde 0.
⚠️ Côté Google, ce compte n'est pas optionnel non plus : la tâche « **Informations de connexion** »
de la configuration attend des identifiants de test.

### L'état de la fiche Play, au 24 septembre

L'application **« Point Zero » existe en BROUILLON** (`com.pointzero2050.app`, créée le
9 septembre, 0 installation) sous le compte d'organisation « Point Zero 2050 ». Le nom de paquet
est **enregistré** au titre de la validation des développeurs Android (échéance du 30 septembre
2026 : une appli non enregistrée est retirée de Play — ce point-là est donc tenu).

**Configuration : 1 tâche sur 11.** Seule « Définir les règles de confidentialité » est faite.
Restent : *Informations de connexion* (le compte de démonstration), *Annonces*, *Classification du
contenu*, *Cible* (public visé), **Sécurité des données**, *Applis gouvernementales*,
*Fonctionnalités financières*, *Santé*, la *catégorie et les coordonnées*, et la *fiche Play
Store*. Tout le reste (tests fermés, production) reste **verrouillé** tant que ces tâches ne sont
pas faites.

ⓘ **Cinq de ces onze tâches sont déjà répondues** par
[l'inventaire de données](donnees-formulaires-stores-2026-09-23.md) : sécurité des données,
classification (les trois surfaces d'IA), annonces (aucune), fonctionnalités financières (billet
d'événement réel, hors achat intégré), santé (aucune donnée).

## 5. L'ordre de travail que je recommande

1. **Après le Festival** — décision de Boris sur la voie (§1).
2. **Lot 1, dette du site, utile même sans store** : suppression de compte (§2.1), `force_ssl` et
   cookie `Secure`, HSTS, CSP (§3).
3. **Lot 2, liens profonds** : `assetlinks.json` et `apple-app-site-association`, puis les liens du
   Jeu qui rouvrent l'application.
4. **Lot 3, coquilles** : Hotwire Native iOS et Android, paiement hors webview, `path
   configuration`, une capacité native assumée (notifications ou hors-ligne) pour la règle 4.2.
5. **Lot 4, dossier** : icônes, captures, formulaires de confidentialité, compte de démonstration.

---

## 6. Ce que cet audit ne dit pas

- Il ne remplace **aucune revue** : les deux stores jugent aussi le contenu, et la première
  soumission d'une organisation attire l'attention.
- Il ne mesure **pas la performance mobile réelle** (temps de premier rendu sur un téléphone
  d'entrée de gamme) : ça se prend au navigateur, pas dans un dépôt.
- La **classification d'âge**, le **périmètre commercial** et la décision **PWA ou natif** sont des
  arbitrages de Boris, pas des constats techniques.

— le portable, 22 septembre 2026
