# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

*(vide — le courrier des 21 et 22 août est traité, réponses de Codex sur le parcours comprises.)*

## Le parcours M0 : le canon est écrit, le portage peut commencer

Codex a répondu aux six écarts et les a inscrits dans
[`page-parcours-carte-du-voyage.md`](../vision/page-parcours-carte-du-voyage.md) §3.8,
« Arbitrages de migration de la page fusionnée ». **C'est la référence du portage**, pas les
notes des maquettes. Deux de ses réponses infirment ce que j'avais supposé : la **voix narrative
reste** (les compteurs l'accompagnent), et **l'Atelier garde un traitement de rite** au lieu de
redevenir une ligne ordinaire.

L'inventaire d'écart qui a servi à poser les questions :
[`inventaire-ecart-parcours-m0-2026-08-22.md`](../vision/inventaire-ecart-parcours-m0-2026-08-22.md).

**⚠️ Les deux pages forment un seul lot.** Intensité `/5`, échelle d'effet `/5`, séquence et
reconnaissance n'existent que dans `journeys/_show.html.haml` : porter la page parcours seule les
supprimerait de l'application, CI verte et bancs verts, chaque page étant conforme à sa maquette
prise isolément.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| Le rite dans son chapitre : `journey_progress.rb:109-113` à retourner, Ω comptés une fois (§3.8) | **portable** |
| L'étape courante de la séquence demande un état réel — besoin de modèle | **portable** |
| Les deux cas limites de dérivation (aucun skill sans `derived_framework` ; aucune Transcendance non configurée) | **portable** |
| Un parcours sans YAML (Festival 2026) : la dégradation actuelle survit-elle ? | **Codex** — à défaut je la conserve |
| Un chip dont le verbe manque : que montre-t-il ? | **Codex** — à défaut Puissance + polarité, sans verbe |
| Les 18 illustrations pèsent 57 Mo (~3,3 Mo pièce) : hors dépôt + conversion, comme les médaillons | **Boris / portable** |
| `?stage=m1entry` et `?stage=m1circle` à porter — `_classique.html.haml` disparaîtra ce jour-là | **poste fixe**, après le parcours |
| `marque_la_visite "m0.emotion.mentor"` (popup de première visite du mentor) | **portable**, sans urgence |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) |

## Les quatre leçons, toutes payées une fois

1. **Un banc supprimé ne casse rien — il se tait.** `ls scripts/ | grep <thème>` avant d'écrire.
2. **Une assertion décrit le RENDU, jamais la source.**
3. **Une purge d'entrée n'est pas un filet, c'est un masque.**
4. **⚠️ Une assertion qui ne peut pas échouer ne borne rien.** Produite deux fois le jour même où
   je la consignais — et le portable a produit le même motif de son côté, à quelques heures
   d'écart. Ce n'est pas une étourderie, c'est un angle mort de la méthode.

## Et la méthode qui a tout trouvé

**Le navigateur voit ce qu'aucun banc ne peut voir.** Cinq défauts en deux jours, dont un panneau
entièrement INERTE en production avec CI verte et bancs verts. Aucun n'a été trouvé au calcul.
