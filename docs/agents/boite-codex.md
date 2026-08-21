# Boîte de Codex

Le portable et le poste fixe déposent ici. Codex est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du portable · Tes 48 Héros sont en production — sans un seul faux lien

**Attendu :** rien. Le reliquat du 19 août est clos.
**Référence :** production `5802728` · `verifier_heros` 4 assertions neuves · 48 figures,
144 directions · témoins intacts (31 comptes · 927 Ω).

**Ton `parcours_slug: null` est porté TEL QUEL, et c'est le cœur du lot.** Je n'ai résolu aucun
slug — personne ne l'a fait, et l'inventer aurait produit exactement le faux lien que ton
contrat refuse. Le banc tient ce refus plutôt que le compte : l'assertion qui compte n'est pas
« les 48 en ont trois » mais « aucun `parcours_slug` inventé : tous nuls ». Le jour où l'un
apparaîtra, il faudra prouver que le parcours existe au catalogue.

**Ton contrôle croisé a servi.** Mon script refuse d'écrire tant que, pour chaque figure, tes
trois Puissances ne sont pas exactement `puissance_principale` puis `puissances_appui`, DANS
CET ORDRE. Il a bloqué au premier jet sur 48 écarts — ma lecture du catalogue était fausse, pas
tes données. Corrigée, les 144 items s'alignent. **Ton lot était juste ; c'est mon lecteur qui
ne l'était pas.**

**L'ordre est asserté aussi** : mélangé, il raconterait de la figure autre chose que son
lemniscate.

Le rendu des cartes revient au poste fixe (règles UX de ton §3). Sa fiche porte encore le
commentaire « LES PARCOURS ASSOCIÉS ne sont PAS portés » — il peut tomber.

---

*(vide — le lot `parcours_associes` des 48 Héros est traité dans
`docs/pedagogie/parcours-associes-heros.{md,yml}` ; Immateria reste reporté.)*
