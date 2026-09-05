# Protocole des newsletters Point Zéro

*Proposé le 6 septembre 2026 par le portable, à la demande de Boris. Mesuré sur le déployé, pas
supposé. Ce document est une proposition : il ne vaut qu'une fois arbitré.*

---

## 1. Le principe : une seule source de vérité, et elle est chez nous

C'est déjà écrit dans le code, en toutes lettres (`BrevoClient`) :

> « Le fichier d'abonnés reste la propriété de l'application : Brevo est un tuyau, jamais la
> source de vérité. »

Tout le reste de ce protocole découle de cette phrase. Si un jour on la contredit — en gérant des
contacts directement dans Brevo, par exemple — il faudra la réécrire d'abord, et assumer ce qu'on
perd.

**Aujourd'hui** : `Subscriber` en base (635 confirmés), poussés dans la **liste 3** de Brevo par
`SynchroniseSubscriberJob` au moment de la confirmation.

---

## 2. ⚠️ Ce qui ne marche pas aujourd'hui, et qui doit être réparé avant la première campagne

**Les deux listes ne se parlent que dans un sens, et jamais pour le désabonnement.** Mesuré le
6 septembre 2026 :

| geste | ce qui se passe chez nous | ce qui se passe chez Brevo |
|---|---|---|
| inscription confirmée | `statut: confirme` | contact ajouté à la liste 3 ✅ |
| **désinscription depuis notre site** | `statut: desabonne` | **rien — la personne reste dans la liste** |
| **désinscription depuis un courriel Brevo** | **rien — elle reste `confirme`** | contact désinscrit |

`BrevoClient` ne porte qu'une méthode, `televerser_contact` : il **ajoute**. `Subscriber#desabonner!`
ne fait qu'un `update!` local. Aucun webhook Brevo n'est reçu.

**Les deux conséquences :**

⚠️ **Une personne qui se désinscrit sur `pointzero2050.com` continue de recevoir la newsletter.**
C'est une obligation légale non tenue (le retrait du consentement doit être honoré), et c'est le
plus sûr moyen de faire s'effondrer la délivrabilité : quelqu'un qui a demandé à partir et qui
reçoit quand même ne se désinscrit pas une seconde fois — il signale comme spam. Un taux de
plainte se paie ensuite sur **tous** les envois, y compris les courriels de billet.

⚠️ **Nos chiffres sont faux.** « 635 abonnés » est le nombre de personnes que *nous* croyons
joignables, pas celui que Brevo enverra. L'écart ne se voit nulle part.

**À construire avant la première campagne** (portable) :

1. `desabonner!` **prévient Brevo** — un `PUT /contacts/{email}` avec `emailBlacklisted: true`,
   rejoué en tâche de fond comme l'inscription, et idempotent.
2. **Un rapprochement périodique** dans l'autre sens : lire les désinscrits de Brevo et les passer
   `desabonne` chez nous. Sans lui, une désinscription faite depuis un courriel reste invisible.
3. **Un banc** qui garde les deux sens — c'est un droit, il se mesure comme un droit : se
   désinscrire ici retire là-bas, et réciproquement.

⚠️ **Et le lien de désinscription des campagnes doit rester celui de Brevo**, pas le nôtre : c'est
lui que les clients de messagerie reconnaissent (`List-Unsubscribe`), et c'est ce qui évite le
bouton « spam ». Le rapprochement le rend fiable de notre côté.

---

## 3. Le cycle d'une newsletter — qui fait quoi

Chaque étape a **un** propriétaire. Ce n'est pas une hiérarchie, c'est une manière de savoir à qui
poser une question.

| étape | qui | où ça vit |
|---|---|---|
| 1. **Le texte** — angle, promesse, formulations | **Codex** (canon éditorial) | `zegame-docs` |
| 2. **Validation du fond** | **Boris** | — |
| 3. **La maquette HTML** — composition, responsive, contraintes e-mail | **poste fixe** | `zegame-prototypes/<nom>-cible/` |
| 4. **Le routage** — adaptation, liens, test, envoi | **Boris**, dans Brevo | Brevo |
| 5. **La mesure d'après** | **portable** | ce dépôt |

⚠️ **L'application n'envoie AUCUNE campagne.** Elle n'envoie que du transactionnel — billet,
confirmation, accès. Une campagne part de Brevo, à la main, par une personne. C'est la consigne de
Codex du 5 septembre, et elle vaut comme règle permanente : un envoi de masse déclenché par du
code est un envoi qu'on ne peut plus arrêter.

**Chaque newsletter validée est archivée ici**, datée, avec ses liens et l'état mesuré de la
chaîne au moment de l'envoi — comme
[`prospection-festival-2026-10-01.md`](prospection-festival-2026-10-01.md). Une campagne qui n'a
laissé aucune trace ne peut pas être relue six mois plus tard, quand on cherchera pourquoi celle-ci
a mieux marché que la suivante.

---

## 4. La liste avant chaque envoi

À faire dans l'ordre. Chaque ligne est **mesurable** : si on ne peut pas la mesurer, on ne peut pas
la cocher.

**Les liens**
- [ ] chaque lien pointe la **production**, jamais la préprod ni `new.pointzero2050.com`
- [ ] chaque lien répond **200** (les vérifier un par un, pas « ça devrait marcher »)
- [ ] le CTA principal mène à la page qui **vend**, pas à l'accueil

**La chaîne derrière le lien**
- [ ] la page d'inscription rend le bon prix et le bon nombre de places
- [ ] le tunnel part vers Stripe (sonde serveur, sans payer)
- [ ] un refus (adresse déjà inscrite) affiche son message **visiblement**

**L'envoi**
- [ ] le domaine authentifie : SPF, DKIM, DMARC (aujourd'hui : oui, DMARC en `p=none`)
- [ ] désinscription en un clic, et elle **redescend jusqu'à notre base** (voir §2)
- [ ] un **envoi d'essai à soi-même** d'abord, lu sur téléphone et sur ordinateur
- [ ] segment et volume écrits **avant** d'envoyer, pas décidés en cliquant

**Les images**
- [ ] URL HTTPS absolues, jamais de chemin relatif
- [ ] chaque image a un `alt` : beaucoup de clients ne les chargent pas par défaut

---

## 5. Après l'envoi — ce qu'on lit, et ce qu'on en fait

À relever **48 h après**, et à consigner dans le fichier de la campagne :

| indicateur | seuil d'alerte | ce qu'on fait s'il est franchi |
|---|---|---|
| taux de plainte | **> 0,1 %** | on arrête les envois de masse et on cherche la cause avant tout autre envoi |
| bounces durs | **> 2 %** | on nettoie la liste avant l'envoi suivant |
| désinscriptions | > 1 % | on relit l'angle : ce n'est pas une panne, c'est un désaccord |
| ouvertures / clics | — | à comparer d'une campagne à l'autre, jamais dans l'absolu |

⚠️ **Le taux de plainte est le seul chiffre qui coûte quelque chose d'irréversible.** Les autres se
rattrapent ; une réputation de domaine abîmée met des mois à revenir, et elle emporte avec elle les
courriels de billet, qui n'ont rien demandé.

---

## 6. Ce qui n'a pas encore de réponse, et qui appartient à Boris

- **Le rythme.** Une newsletter tous les combien ? Sans réponse, chaque envoi se décide dans
  l'urgence et le rythme se lit comme du bruit.
- **Une liste ou plusieurs ?** Les 635 abonnés, les acheteurs de billet, les contacts personnels et
  les sociétaires n'ont ni le même consentement ni la même attente. Aujourd'hui il n'y a qu'une
  liste, la 3.
- **Les contacts personnels de Boris.** Ils ne sont pas des abonnés. ⚠️ Les importer dans Brevo est
  exactement le cas où un compte se fait suspendre et où la délivrabilité du domaine se dégrade
  pour tout le reste. Le message personnel part de la messagerie personnelle — c'est ce qui a été
  décidé le 5 septembre, et c'est le bon choix.
- **DMARC en `p=none`.** Il observe sans appliquer. Passer à `quarantine` protège le domaine contre
  l'usurpation, mais demande d'avoir lu les rapports d'abord.
