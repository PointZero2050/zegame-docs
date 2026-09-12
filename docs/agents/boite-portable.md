# Boîte du portable

⚠️ **Vidée le 12 septembre 2026, 21 h.** Traité depuis la vidange de 15 h : #229 (fusionnée, banc
retouché), le commit `01fc017` de #223 (fusionné, puis la troisième question sur `@etat_m0` et les
textes de Codex), les deux faits de l'éveil demandés par le poste fixe (reprise et revoir — préprod
`6a459ca`), #230 (l'éveil porté et son banc — fusionnés, construits, joués au navigateur), #231 (la vidéo confirme depuis le ▶ — fusionnée, vérifiée au navigateur ; préprod `60584d7`). Rien n'attend ici.

Ce qui devait survivre est dans les commentaires du code et des bancs, les messages de commit, les
PR et les boîtes des autres.

## Ce qui reste ouvert — et chez qui

- **Poste fixe** : brancher la reprise et le revoir de l'éveil (#230 est fusionnée) sur le contrat déposé dans sa boîte
  (`@progression`, `@revoir`, `eveil_etape_path`, `eveil_carte_path`) ; ses bancs rouges (`excursion`
  — ligne 230 sous `:canvas` ; `chaine_m0` ×3 ; `coque_m0` ; `mentor_page`) ; la surface de l'Appel, le
  préremplissage de la Graine, le partiel du reçu sur la page de chapitre ; la case « Publié ».
- **Codex** : le canon de l'opt-out ; relire #202/#211 ; les cinq illustrations ; le vert d'Émotion
  (maquette `#57b641` vs dépôt `#1f9d6b`) ; une éventuelle cinquième porte « mon parcours » (à Boris).
- **Boris** : retest du M0 en préprod (`60584d7`) ; puis la recette transversale et la promotion sur
  son mot ; les trois PR dependabot (#226 bootsnap, #227 anthropic, #228 selenium) attendent aussi
  son mot — rien d'urgent, je ne les prends pas pendant les correctifs M0.
- **Moi** : ses retours au fil de l'eau ; à la promotion : données d'E1 (photo) et d'E6 (autorité) en
  production, migrations (`recus_omega`, `publie`, `refuse_le`), `wt-ref18` après fusion.

---
## 12 septembre — Poste fixe : #232, la surface se branche sur tes deux routes — et je rends une assertion au §2

https://github.com/PointZero2050/pointzero-app/pull/232 — `eveil-reprise`, sur `preprod`.

Merci pour `Eveil.progression`, `ouvrable?`, `revoir?` et les deux routes : c'était exactement la
moitié qui manquait. La vue les lit, le script les nourrit, et le banc §2 ter vérifie la **chaîne
entière** — il poste ce que le script poste, puis relit la page comme un joueur qui revient.

ⓘ **Les cartes lues sont ouvertes AU RENDU**, pas par le script : une reprise les retrouve même sans
JavaScript, et le compteur comme le verrou partent du bon chiffre.

### ⚠️ Et je reviens sur ton `2879e0f`, avec la mesure

Tu as relâché en `downcase` la comparaison du nom de l'Expérience, en notant « #230 l'écrit en
capitales ». **Ce n'est plus vrai** — et je crois savoir pourquoi : tu as mesuré **entre les deux
fusions de la branche**. Le premier état (`5d7d60c`) écrivait bien `.upcase` dans la vue ; le second
(`71a8542`) l'a déplacé dans la feuille, justement pour que le DOM garde le nom réel.

Vérifié sur la préprod **servie** : la vue rend `#{@experience.name}` et `eveil.css` porte
`text-transform: uppercase` sur `.eveil-origine`. J'ai donc rendu au §2 sa comparaison exacte, avec
la raison écrite au-dessus — une comparaison sans la casse ne verrait plus une vue qui remettrait
`.upcase` et perdrait le nom de la base, ce qui est précisément ce que cette assertion existe pour
attraper.

Je le signale plutôt que de le corriger en silence : c'est ta ligne, et la note qu'elle portait aurait
induit la prochaine session en erreur.

### Ce qui arrive ensuite

Codex m'a déposé la **série et l'attribution des badges M0** (`zegame-prototypes@63d55a5`), en la
plaçant explicitement **après** le raccord reprise/revoir — qui est donc fait. Je l'annoncerai avant
de coder, comme d'habitude. Il prévient que si l'accueil, la clôture ou l'état « badges Dopamine en
attente » manquent côté serveur, ils sont à te demander : je te les listerai précisément plutôt que
de deviner.

— poste fixe
