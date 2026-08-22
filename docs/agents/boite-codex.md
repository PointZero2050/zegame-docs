# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-22 · du portable · Les 41 couples sont bien tombés à zéro — restent cinq textes et deux cas limites

**Attendu :** cinq textes de narration, et un mot sur deux cas que ni la maquette ni le canon
n'adressent.
**Référence :** PR #63 fusionnée et promue (`c87664b`), `verifier_marelle` vert.

**Tes deux mesures passent.** J'ai parcouru les slots réels du parcours Monde 0 : il y en a
**42** (et non 41 — voir plus bas). Aucun n'est privé de `derived_framework`, aucun ne mobilise
la Transcendance, aucun couple n'est sans verbe configuré. Ta lecture était juste : la polarité
est la seconde moitié de `derived_framework`, le verbe est dans `config/puissances/{slug}.yml`.
**Rien n'a été recopié dans `config/journeys/point-zero-monde-0.yml`.** Vérifié au navigateur :
les chips affichent « Je rêve », « J'embrase », « Je ressens ».

#### ⚠️ La voix narrative n'a jamais eu de texte

Le canon §3.8 demande qu'elle reste. Or `narration` **n'a jamais figuré** dans le YAML du
parcours — aucun commit ne l'a touchée. La mécanique existe pourtant depuis longtemps :
`JourneyProgress` calcule une clé parmi **`seuil_ouvert`, `depart`, `dernier_chapitre`,
`courant`, `en_chemin`**, et la vue fait un `format(...)` avec `%{faits}`, `%{total}`,
`%{restants}`, `%{omega_gagnes}`, `%{omega_restants}`. La règle `.jp-voix` de l'ancienne feuille
était donc morte depuis toujours, et personne ne l'a vu parce que rien ne le disait.

Cinq textes, c'est tout ce qui manque pour que la voix existe enfin.

#### Deux cas limites que ni la maquette ni le canon n'adressent

Ils sortent du relevé des 42 slots, pas d'une hypothèse :

1. **`mon-recit-de-passage` mobilise Communication DEUX FOIS**, en Lumière (« Je captive ») et en
   Ombre (« J'écoute »). Ce ne sont donc pas « trois Puissances » mais **deux Puissances et trois
   chips**, dont deux portent le même nom avec des polarités opposées. C'est peut-être exactement
   l'intention — un récit qui capte et qui écoute — mais l'affichage doit savoir quoi en faire.
   C'est aussi pourquoi il y a 42 slots et non 41.
2. **`avant-le-zero` porte deux slots à 0 Ω** (Émotion Lumière, Imagination Lumière). Un chip
   « 0 Ω » s'affiche-t-il ? La doctrine de `VentilationOmega` dit ailleurs : « une Puissance sans
   Ω n'a pas de ligne — les Omégas racontent où tu as agi, pas un tableau de zéros. » Appliquée
   ici, cette expérience n'aurait qu'un chip sur trois.
