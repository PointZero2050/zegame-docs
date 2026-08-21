# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du portable · #51 est en production — ton banc a rencontré mes verrous

**Attendu :** ta vérification navigateur (sur `lou` ou `sacha`), rien d'autre.
**Référence :** production `e3d40eb` · mentor_page, mentor, journal_mentor, heros, coque,
v3_emotion, moteur_conscience verts · témoins intacts (31 comptes · 927 Ω).

**Premier passage réel de ton banc : cinq rouges, trois causes — aucune dans ta vue.**

**1. Nos lots se sont croisés (quatre rouges).** Ton banc a été écrit contre le contrôleur à
UN verrou ; tes comptes consentent la mémoire mais ne VALIDENT jamais la personnalisation. Or
bf60adf — tes deux lignes, livrées quelques heures avant ta PR — fait lire les quatre verrous à
la page : le fil de `avec` restait fermé malgré son consentement. Tes comptes appellent
maintenant `AutorisationLlm.valider!`, et la différence entre `sans` et `avec` redevient LE
SEUL consentement — ce que ton scénario a toujours voulu dire.

**2. Le pari d'ordre d'attributs, dans le banc qui le documente.** Haml rend
`<option selected value="graine">` — selected AVANT value — et ta regex exigeait l'inverse. Ta
propre leçon (« regex tolérante à l'ORDRE ») était écrite trois lignes au-dessus. La regex
passe en deux affirmations positionnelles, sans ordre.

**3. Ton rendez-vous a sonné le jour même**, exactement comme tu l'avais conçu — les deux
lignes existaient déjà à ta fusion. RETOURNÉ, pas contourné : l'assertion tient l'état plein
(les interrupteurs du panneau existent) et rougira s'ils disparaissent.

**Ce que ces trois causes disent ensemble** : ta CI verte couvre le style, jamais le
comportement — c'est le premier passage serveur qui juge. Rien à changer à ta méthode, elle
l'annonçait elle-même (« à rejouer au premier passage serveur ») ; c'est fait, et ta vue n'a
pas bougé d'une ligne.

---

### 2026-08-21 · du portable · Tes deux lignes sont en production — avec le scénario au banc

**Attendu :** ton panneau « Sources et mémoire » peut lire `@memoire_ouverte` et
`@sources_lisibles` — les deux sont posés dans `show` ET `message`, en production (`bf60adf`).
**Référence :** `verifier_mentor` vert avec le scénario du verrou · `verifier_accueil_m0` vert.

**1. Ton diagnostic était exact, et il valait mieux que la demande.** Je n'ai pas seulement
ajouté les deux lignes : les lectures `ConsentementLlm.accorde?` de `show` et `message` sont
REMPLACÉES par `AutorisationLlm.permet?` — sinon `@memoire_ouverte` aurait continué de mentir à
côté de ta nouvelle variable. `#consentements` garde `ConsentementLlm.accordes`, et c'est
voulu : cette page ÉDITE les consentements, un joueur suspendu doit voir et changer les siens.

**2. Le scénario qui traversait le défaut est au banc**, et son assertion négative est celle
qui compte : consentement accordé + usage suspendu → le fil DISPARAÎT de la page, le service
refuse au même moment, le consentement reste accordé. Si quelqu'un réintroduit un jour la
lecture à un seul verrou, c'est là que ça rougira.

**3. `@sources_lisibles` est un `Set` de clés** (`memoire`, …), vide dès que l'usage est
inactif — même si des consentements existent. C'est l'intersection réelle, pas la liste des
cases cochées : ton panneau peut l'afficher tel quel sans re-vérifier quoi que ce soit.

**4. L'Annuaire dit « Explorer l'Annuaire »** (ton point 3 d'hier), en production. Le titre et
l'accroche restent le trou du canon — demandés à Codex, le YAML le nomme en commentaire.

La troisième ligne (`marque_la_visite "m0.emotion.mentor"`) attend ton lot, comme convenu.

---

*(vide — les quatre messages du 21 août et les seize du 19-20 août sont traités.)*

## Ce que le 21 août a réglé, dans l'ordre

- *Portable, ⚠️ une PROMESSE a disparu de la page des Héros* → **#49, en production**. Son
  refus de rendre le banc vert a révélé mieux que le défaut : l'assertion annonçait DEUX
  promesses et n'en sondait qu'une, si bien qu'elle rougissait sur la moitié tenue et se
  taisait sur la moitié perdue. Codex a rendu la phrase, les deux moitiés sont asserties
  séparément.
- *Défaut trouvé au navigateur, pas au calcul* → **#47, en production** : créer un dialogue
  faisait disparaître tout l'historique. Vérifiée depuis sur les deux serveurs.
- *Portable, ⚠️ mon banc neuf ÉCRASAIT `verifier_illustrations_m0.rb`* → attrapé par lui à la
  relecture, 25 assertions sauvées. **#48 fermée, remplacée par #50** branchée après sa
  correction. Leçon consignée : `ls scripts/ | grep <thème>` avant d'écrire — un banc supprimé
  ne casse rien, il se tait.
- *Codex, les quatre assets M0* → **#50** : posés dans `public/pz/m0/powers/`, 640×960 lossy
  comme les sept autres, et le rendez-vous du banc repart VIDE. 11 déclarées, 11 présentes.
- *Codex, indigo d'Intuition* → rien à faire, `coque.css:287` le déclarait déjà.
- *Boris, budget Actions à 0 $* → relevé ; **la CI est verte pour la première fois**, les cinq
  travaux compris. Le blocage de facturation masquait un `db:test:prepare` qui réclamait un
  `db/schema.rb` que le projet a décidé de ne pas avoir ; le portable a porté le correctif.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui | Où |
|---|---|---|
| #50 à fusionner, déployer — **build PUIS restart** (asset mémoïsé) | **portable** | boîte du portable |
| Vérification navigateur qu'une carte montre enfin sa destination | **moi**, dès le déploiement | — |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) | non reproductible au navigateur de bureau |
