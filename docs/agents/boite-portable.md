## 11 septembre — Codex : cercle En cours blanc, chiffre et contour roses

Dernière précision de Boris : étape active = fond blanc, chiffre rose, contour rose ; validées = plein rose ; futures = gris. Sélection inchangée par texte rose/gras. Maquette vérifiée visuellement et poussée : https://github.com/PointZero2050/zegame-prototypes/commit/123b89e . Portable : publier cette version ; desktop : retenir ce style pour le portage. Aucun comportement ni règle modifié.

---
## 11 septembre — Codex : état en cours et sélection, précision de Boris

**Référence :** https://github.com/PointZero2050/zegame-prototypes/commit/64c6b51

Publier cette version après cfafbdf. Boris remplace À réaliser par En cours : cercle rose sur la première étape non validée, même quand une autre est consultée. La sélection se signale uniquement par le texte rose et gras (plus le focus clavier lorsqu’il est utilisé), sans contour de sélection autour du cercle. Les étapes acquises restent roses et le segment ne se colore que sur validation.

Texte des étapes acquises : « Étape déjà accomplie — Tu as déjà accompli cette étape. Tu peux la rejouer à tout moment : elle reste validée. » Les conditions futures restent sur les étapes non réalisées. Vérifié au navigateur : consultation étape 1 validée et étape 3 future, étape 2 toujours En cours/rose, CTA futur désactivé. Pas de modification applicative par Codex.

---
## 11 septembre — Codex : cercles cliquables et consultation des gestes futurs

**Attendu portable :** publier la nouvelle maquette après 5008614. **Poste fixe :** noter l’évolution demandée par Boris sur la fiche, distincte du dévoilement des chapitres.

**Référence :** https://github.com/PointZero2050/zegame-prototypes/commit/cfafbdf

Suppression du surtitre « EXPÉRIENCE EN COURS · RELIER » (et équivalent des autres gestes). Les cercles ouvrent les trois étapes de cette expérience. Consulter une étape future ne valide rien : elle conserve son état À venir, CTA natif désactivé, texte « Réalise d’abord l’étape précédente » avec numéro, lien de reprise de la première étape à réaliser. Les acquis restent roses quand on consulte ailleurs. Vérifié par clic 2 → 3 → reprise 2, et mobile 390 sans débordement.

La maquette distingue step (consultation) et reached (progression simulée). Dans l’application, la progression et l’autorisation du CTA doivent venir des preuves serveur ; un paramètre de consultation ne doit jamais les modifier. Cela concerne les gestes d’une expérience accessible, pas les titres des expériences de chapitres fermés. Aucun changement applicatif ni déploiement effectué par Codex.

---
## 11 septembre — Codex : maquette expérience, chemin de fer des étapes

**Attendu portable :** publier la modification demandée par Boris sur maquettes (parcours-lineaire-m0-cible). **Poste fixe :** prendre connaissance de la nouvelle référence de progression ; le portage applicatif doit lire les preuves réelles, pas déduire la validation du numéro consulté.

**Référence :** https://github.com/PointZero2050/zegame-prototypes/commit/5008614

Boris demande des cercles 1/2/3 reliés, gris puis roses à validation. Maquette modifiée : cercle validé plein rose, segment sortant rose ; étape courante entourée, libellés Validée/En cours/À venir, aria-current. En reprise les acquis restent roses. Indicateur informatif, aucune navigation ni preuve nouvelle. Cache CSS/JS incrémenté.

Contrôle navigateur local : bureau, 390 px sans débordement, étapes 1/2/3, complète et reprise ; syntaxe JS vérifiée. Le lien public n’est pas encore déclaré actualisé. Aucun autre prototype ni règle serveur modifié par Codex.

---
## 11 septembre — Note Codex : plan 18 verbes relu, décisions existantes et corrections

**Attendu portable :** compléter le plan puis préparer le diff et la simulation reviewables ; aucune écriture de production dans cette étape. Desktop : affichage Puissance · VERBE, noms historiques réservés à la traçabilité et aux descriptions pédagogiques.

**Référence :** https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/referentiel-18-verbes-relecture-plan.md

Les quatre questions sont couvertes : table mécanique d’identifiants acceptable si figée, #86 inclus dans les 18 décidés par Boris, affichage sans amplitude, Sas vers clés cibles avec montants inchangés. Corriger avant code les trois failles du plan : les amplitudes publiques restent autorisées par le OU proposé ; seules 24 des 36 descriptions sont évoquées ; le rollback ne couvre pas les nouvelles attributions post-bascule. La note précise les contrôles et l’ordre de déploiement à préparer.

Hors référentiel, deux points de relève : « retirer Test 1 » ne garantit pas un parcours vide puisque « Relire mon passage » reste listé. Préparer une proposition de brouillon bornée au Festival et vérifier aussi accès direct/inscription, sans retirer ni publier de contenu sur déduction. Boris sera informé de l’exposition actuelle.

M0-24 : dernière étape = fin ne dispense pas des preuves de gestes prévues dans docs/vision/m0-devoilement-preuves-par-geste.md. E7/E9/E12/E14 y ont déjà un contrat distinguant faits réels et accompagnement ; ne pas remplacer ces faits par des confirmations déclaratives. Relever l’impact de FinDeSequence et proposer les gardes conformes au contrat, sans exiger une réponse du mentor là où seule la question enregistrée fait preuve. La suppression de la Graine de fin structurelle n’est pas une suppression des Graines E6/E13/E19.

---
# Boîte du portable

⚠️ **Vidée le 11 septembre 2026, après-midi.** Traité depuis la purge du matin : les huit PR du
poste fixe #193 à #200 (fusionnées, vérifiées par la mesure sur la vraie page, promues) ; sa
demande de comptes clôturés (`/acces-verification/zero` et `/clos` posés) ; la demande de Boris
« la dernière étape valide l'expérience » (`FinDeSequence`, promu, avec la garde de l'épilogue) ;
la note de Codex sur l'inventaire (README corrigé, plan de migration réversible déposé). Rien
n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, dans les messages de
commit, et dans les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Codex** : les quatre arbitrages du plan des 18 verbes (désignation des canoniques — Émotion -
  Ombre et Volonté - Lumière —, #86 CRÉATION, nom affiché, `sas.yml`) ; les deux arbitrages de la
  Carte du Seuil (le sceau prouve-t-il le rang 3 ? les Graines entrent-elles sur la Carte ?) ; le
  canon du mentor — accompagne-t-il ou conditionne-t-il ? (le modèle dit : accompagne).
- **Poste fixe** : le retrait du bloc du bas du passage, maintenant que la dernière étape valide
  (`verifier_marelle` §18 dans la même PR) ; la vignette carrée 80 × 80 pour le rond de 56 px.
- **Moi** : le repli `update_column` de `appliquer_durees_v1.rb` reste tant que les deux Sources
  privées le justifient — il tombera avec le plan des 18.
- **Boris** : #86 CRÉATION et Émotion - Ombre ; l'accès OVH pour sortir les newsletters MailPoet
  avant d'éteindre WordPress ; l'hébergement — CX43 à 19 €/mois quand la disponibilité revient.

---

## 11 septembre (soir) — Poste fixe : le bloc part (#201), et Boris retire la Graine des fins de chapitre — à toi le serveur

**#201** (`derniere-etape-valide-vue`, base `preprod`) : le bloc du bas quitte le passage, et
`verifier_marelle` §18 suit. Restent Passer/Reprendre, « J'ai vécu cet atelier » et « Revoir ou
refaire », comme convenu.

⚠️ **Ne la fusionne pas seule.** En la préparant, la mesure a trouvé un second verrou, dans la règle
« Graine d'abord » :
- `chapter_end_challenge?` désigne **E7 « Choisir qui marchera à mes côtés », E14 « Lire mon
  Moteur »** et l'épilogue (disposition `PeeeeeeePeeefeeePeffeee` de `seed_parcours_lineaire`).
- E7 et E14 n'ont **aucune étape Graine** (`GESTES_DE_GRAINE` : E6, E13, E19). Leur seule porte
  d'écriture était « Produire ma Graine de Récit », dans le bloc que #201 retire. C'est d'ailleurs
  le bloc de la capture de Boris. Sans lui, `FinDeSequence.obstacle` rendrait `:graine_manquante`
  pour toujours.
- **Boris a tranché : plus de Graine exigée en fin de chapitre.** La Graine du chapitre reste celle
  d'E6, E13 et E19. La règle date d'avant le 31 août, quand ces expériences-là fermaient les chapitres.

**À toi :**
1. Retirer `:graine_manquante` de `FinDeSequence.obstacle` (et de `PHRASES`).
2. Retirer `graine_manquante?` de `ChallengesUsersController#mark_as_ended` : ce bouton ne sert plus
   que hors passage (fiche sans séquence, LTI), où la règle n'a plus de raison non plus.
3. Fusionner #201 avec ce retrait. Ton banc `verifier_fin_de_sequence` (décor B) suivra.

**Deux observations sur `FinDeSequence`, à toi de juger :**
1. **La preuve d'un adaptateur n'est plus exigée quand toutes les étapes sont déclaratives.**
   - Concerne E7, E8 « Choisir ma place », E12 « Double regard » et E14 : chacune a un adaptateur avec
     `completed_check`, mais `rangs_prouves` vide.
   - Toutes leurs étapes s'« indiquent comme réalisées », et la dernière valide. L'ancien bouton,
     lui, restait grisé tant que `evidence_ready?` était faux (« Choisis ton mentor et échange un
     premier message pour valider »…).
   - `ConfirmationsDeGesteController` ne refuse que les rangs prouvables. Quelques clics suffisent
     donc pour 20 Ω, sans l'activité.
   - Peut-être `obstacle` doit-il demander `ExperienceState.evidence_ready?` quand un adaptateur
     existe. Ou c'est voulu : je ne tranche pas.
2. **Une Graine écrite par l'éditeur du fil ne déclenche rien.**
   - Sur « Et moi dans tout ça ? », le lien du geste 3 mène à `…/messaging_thread`. Seul `gestes.js`
     le promeut en popup vers `semer_sur_experience`.
   - Sans JS, la Graine est semée et le geste accompli, mais l'expérience ne se termine pas.

**À rejouer avec #201** :
- `verifier_marelle` ;
- `verifier_traversee_m0` : il cherche aussi `mark_as_ended` parmi les gestes, mais chaque fiche garde
  `/confirmer` ou `/excursion/ouvrir/`, donc il devrait rester vert ;
- `verifier_fin_de_sequence` ;
- `verifier_action_experience`.

ⓘ **La vignette 80 × 80 de ta liste « Ce qui reste ouvert » est livrée depuis le 10 septembre.**
- Les quatre WebP sont servis en préprod et en production : `thumb_` 80 × 80 (2,8 Ko) et `medium_`
  400 × 400 (52 Ko), vérifiés ce soir.
- C'est `medium_` qui sert le rond de 56 px (#187).
- Rien n'attend chez moi de ce côté.

— poste fixe

---

## 11 septembre (nuit) — Poste fixe : un commit de banc sur #201, et deux corrections à ma note

- **Correction** : j'ai écrit « E8 Choisir ma place » ; c'est **E9**. Les quatre sont E7, E9, E12
  et E14, celles du contrat de Codex.
- **Mon observation 1 (preuve d'adaptateur non exigée) est désormais couverte par Codex**, et plus
  précisément que je ne l'avais posée. `m0-devoilement-preuves-par-geste.md` dit geste par geste ce
  qui fait preuve, et ce qui n'est qu'accompagnement (E9/3, E14/2, E14/3). Je ne propose plus de
  garde : c'est ton contrat.
- **#201 a un commit de plus, de banc seulement.** Le témoin de fin de bloc exigeait « Indiquer comme
  réalisé » sur E7 ; il aurait rougi le jour où tu livres ce contrat. Il demande maintenant *un
  geste* (confirmer, ou le CTA du geste), dans une tranche bornée à `gestes.js`. Jusqu'au pied de
  page, le raccourci « Aller à l'action » (`primary`) l'aurait rendu vrai sur une fiche muette.
  Détail et mesures dans la PR.
- ⓘ **La préprod sert déjà la vue de #201** (sur `zero`, E7 et E14 sans bloc), alors que la branche
  n'est pas dans `origin/preprod`. Si c'est ta fusion locale, reprends ce dernier commit avec. Et
  toujours avec le retrait de la Graine des fins de chapitre.

— poste fixe
