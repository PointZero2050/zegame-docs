# Newsletter — New Civilization Festival, 1er octobre 2026

*Maquette de Codex (`zegame-prototypes` `4183f69`), adaptée au routage par le poste fixe le
6 septembre 2026. Archivée selon le [protocole des newsletters](protocole-newsletters-point-zero.md),
§3 : « chaque newsletter validée est archivée ici, datée, avec ses liens et l'état mesuré de la
chaîne au moment de l'envoi ».*

---

## Les deux blocages sont levés — 6 septembre 2026, au soir

*Cette section disait l'inverse il y a deux heures. Elle est réécrite plutôt que complétée : une
archive qui garde un blocage périmé finit par empêcher un envoi légitime.*

**1. Le désabonnement redescend jusqu'à Brevo.** Construit et promu en production par le portable :
`BrevoClient#desinscrire_contact`, un travail de fond, et un rapprochement qui lit Brevo pour
corriger notre base dans l'autre sens — il ne pousse rien, écrire des deux côtés depuis le même
endroit fabriquerait une boucle. Le banc fait l'aller-retour **réel** sur le compte, avec un
contact témoin créé **hors de toute liste** : s'il survivait à un plantage, il ne recevrait aucune
campagne.

⚠️ **Et une mesure a corrigé le constat que j'avais repris en tête de ce document.** J'avais écrit
que les désinscrits continuaient de recevoir. Vérifié personne par personne par le portable : nos
**36 désabonnés étaient inconnus de Brevo**, jamais poussés. **Personne ne recevait contre son
gré.** Le trou était réel mais **pas encore rempli** — il se serait rempli à la première personne
qui confirme puis se désinscrit, donc dans les jours suivant un envoi. La mise en tête restait
juste sur le fond ; c'est la conséquence qui était annoncée trop fort, et je la corrige ici plutôt
que de la laisser courir.

**2. Les quatre images sont en production.** Mesuré par moi le 6 septembre au soir, après la
promotion de `lot-ux-1` :

| fichier | statut | type servi | poids |
|---|---|---|---|
| `festival-cover.jpg` | **200** | `image/jpeg` | 172 ko |
| `festival-ombre.jpg` | **200** | `image/jpeg` | 214 ko |
| `app-monde-0.jpg` | **200** | `image/jpeg` | 38 ko |
| `festival-sceau.png` | **200** | `image/png` | 16 ko |

**440 ko servis.** ⚠️ Les `content-type` sont vérifiés, pas seulement les extensions : c'est ce qui
prouve que le serveur annonce bien du JPEG et du PNG, et non du WebP sous un autre nom.

---

## Les fichiers

| quoi | où |
|---|---|
| maquette de référence (composition, responsive) | `zegame-prototypes/newsletter-festival-cible/index.html` |
| **version prête au routage** | `zegame-prototypes/newsletter-festival-cible/index-routage.html` |
| images servies | `pointzero-app` → `public/site/assets/newsletter/` |

⚠️ **Ne pas éditer les deux HTML en parallèle.** La maquette reste la référence de composition ;
la version de routage n'en est que la sortie adaptée. Une divergence entre les deux ne se verrait
qu'au moment de l'envoi.

## Objet et préheader (de Codex)

- **Objet** : `New Civilization Festival : rendez-vous le 1er octobre`
- **Préheader** : `Le 1er octobre 2026 à Paris, le Point Zéro franchit une nouvelle étape.`

## Les trois adaptations, et pourquoi

**1. Images en URL HTTPS absolues — et en JPEG/PNG, pas en WebP.**
⚠️ Les huit images du Festival que sert le site sont en **WebP**. Outlook pour Windows rend les
images par le moteur de Word, **qui ne connaît pas ce format** : l'abonné verrait quatre cadres
vides. Des dérivés dédiés ont donc été produits — le web a le format le plus léger, le courriel a
le plus ancien.

| fichier | source | servi | format |
|---|---|---|---|
| `festival-cover.jpg` | 2 573 ko, 1672 px | **172 ko**, 1360 px | JPEG |
| `festival-ombre.jpg` | 3 233 ko, 1672 px | **214 ko**, 1360 px | JPEG |
| `app-monde-0.jpg` | 936 ko, 1080 px | **38 ko**, 300 px | JPEG |
| `festival-sceau.png` | 271 ko, 747 px | **16 ko**, 108 px | PNG |

**7 013 ko de sources pour 439 ko servis.** Les largeurs sont le double de l'affichage dans le
gabarit de 680 px.

⚠️ **Le sceau est en PNG, pas en JPEG** : son fond est **transparent**, et un JPEG l'aurait rempli
de blanc ou de noir selon le client. Vérifié après conversion : 108 × 110, RVB **+ alpha**, écart
de compression **0,00** — le PNG est sans perte.

**2. Les deux liens du pied sont des balises Brevo** — `{{ mirror }}` et `{{ unsubscribe }}`.
⚠️ **À confirmer dans Brevo avant l'envoi** : je n'ai pas pu vérifier cette syntaxe depuis ce
poste, l'application ne connaissant de Brevo que l'ajout de contacts. Si l'éditeur ne les
reconnaît pas, ce sont ses propres liens qu'il faut poser. **La désinscription doit rester celle
de Brevo**, jamais la nôtre : c'est elle que les clients de messagerie reconnaissent
(`List-Unsubscribe`).

**3. Les polices PZ ne sont pas embarquées** — les replis Georgia/Arial sont acceptés, comme le
prévoit le `NOTES.md` de la maquette.

## L'état mesuré de la chaîne, le 6 septembre 2026

**Les liens** — les deux seuls liens réels de la lettre :

| lien | mesuré |
|---|---|
| `https://pointzero2050.com/evenements/new-civilization-festival-2026` | **200**, titre juste |
| `https://www.youtube.com/watch?v=BQ1GkGUW6iQ` | ⚠️ voir ci-dessous |

⚠️ **Le film n'a pas été vérifié par un 200**, mais par quelque chose de plus utile : son
identifiant est **le même que celui de la page du Festival** (`data-play-video="BQ1GkGUW6iQ"`) — et
**pas** celui de la présentation de l'accueil (`97mNBv1zukw`). Un 200 de YouTube n'aurait pas dit
si c'était le bon film.

**La chaîne derrière le CTA**, mesurée en production :

- la page rend **250 €** ;
- **aucune jauge de places** — conforme au choix éditorial de la page ;
- le **vrai** formulaire est présent et poste vers la route d'inscription (donc vers Stripe).

**Le registre** — ⚠️ vérifié parce que le site vient de passer au tutoiement : la lettre **tutoie**
déjà (« Tu reçois cette lettre parce que tu suis l'aventure ») et ne contient **aucun**
vouvoiement. Aucune couture entre la lettre et la page qu'elle ouvre.

ⓘ Les six « vous » que compte un `grep` naïf sont tous des **« rendez-vous »**.

## Ce qui reste à faire, et par qui

**Portable — fait le 6 septembre au soir.** Les trois chantiers du §2 du protocole sont construits
et promus : le désabonnement prévient Brevo, le rapprochement corrige notre base dans l'autre sens,
et un banc fait l'aller-retour réel sur le compte.

**Boris — au moment du routage** :
- ⚠️ **les balises Brevo restent à confirmer.** Ni moi ni le portable n'avons de source qui fasse
  foi, et nous ne la devinerons pas dans un fichier qui part à plusieurs centaines de personnes.
  Recommandation commune : **laisser Brevo insérer lui-même son pied de désinscription** — c'est le
  lien que les clients de messagerie reconnaissent (`List-Unsubscribe`) ;
- **un envoi d'essai à soi-même d'abord**, lu sur téléphone et sur ordinateur ;
- segment et volume écrits **avant** d'envoyer.

⚠️ **Les images sont en ligne** depuis la promotion de `lot-ux-1`, et vérifiées en tête de ce
document. Avant elle, les quatre URL répondaient 404 : la lettre serait arrivée nue.
## Après l'envoi

À relever **48 h après** et à consigner ici même, selon le §5 du protocole : taux de plainte
(alerte > 0,1 %), bounces durs (> 2 %), désinscriptions (> 1 %), ouvertures et clics.
