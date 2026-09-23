# Ce que Point Zéro collecte, et ce qui sort — inventaire pour les deux formulaires

Pour **App Privacy** (Apple) et **Data safety** (Google Play). Établi le 23 septembre 2026 en
lisant le code et le schéma de la production, pas la documentation : chaque ligne ci-dessous
renvoie à l'endroit qui l'écrit. Un formulaire de confidentialité inexact se corrige après coup,
mais il est d'abord une déclaration — autant qu'elle soit vraie.

⚠️ **Ce document n'est pas la politique de confidentialité** (`/politique-de-confidentialite`, qui
existe et répond). Il est la matière des deux formulaires, dans leur vocabulaire à eux.

---

## 1. Ce que nous collectons

| Donnée | Où elle vit | Obligatoire ? | Pourquoi |
|---|---|---|---|
| Adresse électronique | `users.email` | oui | identifier le compte, réinitialiser le mot de passe, prévenir |
| Prénom, nom | `users.prenom`, `users.nom` | oui | se nommer auprès des autres joueurs |
| Mot de passe (chiffré) | `users.encrypted_password` | oui | authentifier |
| Téléphone | `users.phone` | **non** | rappel d'un rendez-vous, si le joueur le donne |
| Territoire, présentation, langues, centres d'intérêt, liens | `users.*` | **non** | le profil communautaire, que le joueur compose |
| Photo de profil | ActiveStorage (`photo_televersee`) | **non** | le profil |
| Adresses IP de connexion | `users.current_sign_in_ip`, `last_sign_in_ip` | oui (posé par Devise `trackable`) | sécurité : reconnaître un accès inhabituel |
| Dates et nombre de connexions | `users.sign_in_count`, `*_sign_in_at` | oui | idem |
| Progression de jeu | `challenges_users`, `points`, `recus_omega`, `confirmations_de_geste`, `marqueurs_d_attention` | oui | le Jeu lui-même |
| Contenus écrits par le joueur | `messaging_messages`, `traces`, `graines_publiees`, `moteur_assessments`, `puissance_assessments`, `conseil_sessions` | selon l'usage | ce que le joueur produit et partage |
| Échanges avec le mentor et les guides | `mentor_messages`, `guide_messages` | selon consentement | la conversation, si la porte « mémoire » est ouverte |
| Billet du Festival | `registrations` (email, prénom, nom, montant, références Stripe) | si achat | la billetterie et la comptabilité |

**Ce que nous ne collectons pas**, et qui figure dans les deux formulaires : aucune localisation,
aucun contact du carnet d'adresses, aucune donnée de santé, aucun identifiant publicitaire, aucun
historique de navigation hors de nos pages, **aucun traceur analytique** (vérifié : aucune
occurrence de Google Analytics, Matomo, Plausible, Hotjar ou pixel social dans les pages servies),
**aucun accès caméra ou micro** (`getUserMedia` n'apparaît que dans la bibliothèque Phaser, jamais
appelé par notre code).

**Cookies** : un seul, `_pointzero_app_session` — technique, `httponly`, `samesite=lax`, et
`secure` depuis le 23 septembre. Aucun cookie tiers, aucun cookie publicitaire.

---

## 2. Ce qui SORT, et vers qui

Trois sous-traitants, et rien d'autre.

### Anthropic (le mentor, les guides, l'avatar de l'accueil)

- **Ce qui part** : le texte que le joueur écrit, et un contexte de jeu **conditionné aux
  consentements** (`ConsentementLlm` : traces, graines, moteur, mémoire — chaque porte se referme
  depuis Personnalisation & mémoires).
- **Ce qui NE part pas** : l'identité du joueur. Vérifié dans les trois services — ni prénom, ni
  nom, ni adresse électronique n'entrent dans l'invite ; la figure du mentor y est décrite, pas la
  personne.
- **Ce que nous gardons** : le texte des échanges (`mentor_messages`, `guide_messages`) si la porte
  « mémoire » est ouverte, et **toujours** un journal de coût sans contenu (`avatar_appels` :
  nombre de jetons, statut).
- **Déclaration** : « User Content » et « Usage Data » partagés avec un tiers pour la
  fonctionnalité de l'app ; **jamais** pour du suivi ni de la publicité.

### Stripe (la billetterie)

- **Ce qui part** : l'adresse électronique de l'acheteur, le montant, et trois métadonnées
  (identifiant d'inscription, référence du billet, événement). **Aucune donnée de carte ne transite
  par nos serveurs** : le paiement se joue sur `checkout.stripe.com`.
- **Déclaration** : « Purchases » et « Contact Info », partagés pour la transaction.

### Brevo (les courriels)

- **Ce qui part** : l'adresse électronique, le prénom et le nom — pour la lettre d'information
  (sur consentement) et pour les courriels transactionnels (billet, mot de passe).
- **Déclaration** : « Contact Info », partagée pour la communication.

---

## 3. Fermeture du compte et conservation

⚠️ **Le mot juste est « fermer », et il engage la déclaration.** Arbitrage de Boris du 7 septembre,
confirmé le 23 (« techniquement on effacera les données personnelles ») : la ligne `users` survit
pour la statistique, et **tous les champs personnels sont effacés** — adresse remplacée par
`anonyme-<id>@comptes-clos.invalid`, prénom neutralisé, nom, photo, liens, textes libres et
adresses IP mis à `nil`, mot de passe rendu aléatoire. Le compte ne se rouvre pas.

- **Depuis l'application** : menu Compte → **Fermer mon compte** (`/personnalisation/fermeture`).
  La confirmation se tape (le mot FERMER), l'effet est immédiat. C'est ce qui répond à
  Apple 5.1.1(v) et à Google : le compte cesse d'exister pour la personne, et ses données
  personnelles sont effacées.
- **Adresse web publique** pour qui ne peut plus se connecter :
  `https://pointzero2050.com/suppression-de-compte` — **c'est l'URL à déclarer** dans le formulaire
  Google. L'adresse garde le mot « suppression » (celui que Google attend et que les gens
  cherchent) ; la page, elle, décrit la fermeture.
- **Ce qui subsiste, et il faut le déclarer** : les contributions (messages, Traces, Graines)
  restent **sous un nom neutre** — les retirer trouerait ce que d'autres ont lu ; un billet payé
  reste comme pièce comptable, **détaché** du compte.
- ⚠️ **Limite à connaître avant de l'écrire ailleurs** : sur quelques centaines de personnes,
  retirer un nom ne rend pas toujours méconnaissable. D'où la règle de ne publier que des
  statistiques agrégées.

---

## 4. Les réponses aux deux questionnaires, en clair

**Apple — App Privacy.** Données **liées à l'identité** : Contact Info (courriel, nom, téléphone
optionnel), User Content (messages, photos, écrits de jeu), Identifiers (identifiant de compte),
Usage Data (progression), Diagnostics (IP de connexion), Purchases (billet). **Aucune donnée
utilisée pour le suivi** (*Tracking*) : la réponse est **non** partout, sans exception.

**Google — Data safety.** Collecte : Personal info, Messages, Photos, App activity, Purchase
history. Partage : avec Anthropic (Messages, App activity), Stripe (Personal info, Purchase
history), Brevo (Personal info). **Chiffrement en transit : oui** (HTTPS imposé par l'application
depuis le 23 septembre, HSTS servi). **Suppression des données possible : oui**, dans l'application
(menu Compte → Fermer mon compte) et par l'URL publique ci-dessus.

⚠️ **Et voici comment le dire à Apple sans mentir** : le formulaire demande si l'application permet
de supprimer son compte. La réponse est **oui** — le compte est fermé définitivement et les données
personnelles sont effacées ; ce qui demeure (contributions anonymisées, pièce comptable) est
précisément ce que les deux stores admettent de conserver. Si la revue interroge, la page publique
l'explique déjà, mot pour mot.

---

## 5. Ce qui reste à trancher — et c'est à Boris

1. **La classification d'âge.** Trois surfaces d'IA conversationnelle poussent la note vers le
   haut chez Apple. Le Jeu s'adresse à des adultes : la fiche doit le dire, et le questionnaire
   d'Apple demande de déclarer les fonctionnalités d'IA.
2. **La lettre d'information** : elle est aujourd'hui liée au billet. Si l'application la propose,
   elle devient une collecte déclarée « à des fins de marketing ».
3. **Le téléphone** : facultatif dans le profil, mais dès qu'il est collecté il se déclare.
   Le retirer du profil simplifierait les deux formulaires — décision produit, pas technique.

— le portable, 23 septembre 2026
