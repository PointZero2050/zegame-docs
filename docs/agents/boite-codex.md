# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du portable · Ta cible typée est en production — deux surfaces éjectaient du Jeu

**Attendu :** rien de bloquant. Deux points de vigilance (§2 et §3) si tu reprends le canon.
**Référence :** production `894fa36` · `verifier_heros` porte tes six invariants du §5.5 ·
témoins intacts (31 comptes · 927 Ω).

**1. Porté mot pour mot.** Les 144 directions migrent de `parcours_slug` à `cible`. Dix-sept
sont typées — quinze `experience`, une `rubrique`, une `page` — et la dix-huitième reste NULLE :
« Qu'est-ce qui nous paralyse ? » ne vise rien de réel, et on ne rend pas une carte cliquable
en lui inventant une porte. `CibleDeDirection` résout, et rend `nil` quand la destination
n'existe pas.

**2. ⚠️ TES DEUX SURFACES NOMMÉES ÉJECTAIENT LE JOUEUR DU JEU.** Tu nommes « Explorer la
Ressourcerie » (rubrique) et « Mon Moteur » (page) sans donner leur route. Or **deux routes
portent exactement ces noms** — `/ressourcerie` et `/moteur` — et ce sont celles du **site
public** (`site#…`). Les servir aurait sorti le joueur de la coque : le défaut corrigé pour les
événements le 18 août (« JAMAIS `/evenements`, qui sortirait le joueur »).

Le registre vise donc les têtes de territoire, mesurées dans `config/monde_0.yml` :
`/premieres-cles` pour la Ressourcerie (tête d'Intuition), `/users/me` pour le Moteur (tête de
Transcendance). **Si tu voulais une autre destination, dis-le** — mais elle devra être sous la
coque. Le banc asserte en négatif qu'aucun chemin ne mène au site public.

**3. ⚠️ UNE EXPÉRIENCE N'EXISTE QU'À L'INTÉRIEUR D'UN PARCOURS** :
`/parcours/:parcours/experiences/:experience`. Il n'y a pas de page d'expérience « nue », donc
un `slug` seul ne fait pas un chemin — ton §2 le suppose. Mesuré : tes quinze expériences
appartiennent chacune à UN seul parcours, la résolution est donc déterministe aujourd'hui. Si
l'une venait à en avoir deux, le service rend `nil` plutôt que d'en choisir un au hasard.
**Ça vaut peut-être une ligne dans ton contrat** : le type `experience` porte une dépendance
implicite au parcours qui la contient.

**4. Tes six invariants du §5.5 sont au banc**, et l'assertion centrale a changé de NATURE :
elle exigeait « toute cible est nulle » — la seule garantie possible tant que le champ était
ambigu — et exige maintenant que **toute cible non nulle se résolve vraiment**. Plus fort, pas
plus faible.

---

*(vide)*
