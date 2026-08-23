# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

*(vide — courrier des 21 au 23 août traité.)*

## PR en attente chez le portable

| PR | ce qu'elle fait |
|---|---|
| [#68](https://github.com/PointZero2050/pointzero-app/pull/68) | `g.porte` câblé (20 CTA), deux CTA distincts, un bloc de reconnaissance en moins, doublon CSS trouvé, « Commencer le parcours » corrigé, 5 liens `users/` arbitrés |

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| Vérifier au navigateur les 13 expériences non visitées (compte de recette limité à 2/14) | **portable**, après déploiement de #68 |
| Le panneau de Monde (`.world-panel`) et la carte d'apprentissage : contenu éditorial, rien en base ni en config | **Codex** — à défaut je porte en deux colonnes |
| Fil · Actions · Décisions · Mémoire : **onglets** dans la maquette, **pages** dans l'application | **Codex**, puis peut-être le portable |
| Les textes de narration du parcours (5 clés) — la voix ne peut pas être rendue sans eux | **Codex** |
| Les dérivés WebP des 18 illustrations — aucun outillage image sur ce poste | **portable** |
| `le-site-du-point-zero` vaut 9 Ω en préprod et 10 en production | **Boris** (arbitrage éditorial) |
| `?stage=m1entry` et `?stage=m1circle` — `_classique.html.haml` disparaîtra ce jour-là | **moi**, dès les réponses de Codex |
| `marque_la_visite "m0.emotion.mentor"` | **portable**, sans urgence |

## Les leçons de ces trois jours

1. **Un banc supprimé ne casse rien — il se tait.** `ls scripts/ | grep <thème>` avant d'écrire.
2. **Une assertion décrit le RENDU, jamais la source.**
3. **Une purge d'entrée n'est pas un filet, c'est un masque.**
4. **⚠️ Une assertion qui ne peut pas échouer ne borne rien** — et sa variante : une assertion
   peut mesurer une grandeur **voisine** de celle qui compte et rester verte pour toujours.
5. **⚠️ Une parité de CONTENU n'est pas un portage.** Un banc qui ne regarde que la présence de
   blocs ne voit pas une forme qui n'a pas suivi — d'où les assertions **négatives**.
6. **Les valeurs éditoriales divergent entre préprod et production.** Un banc compare deux
   mesures entre elles, jamais une constante.
7. **⚠️ Un doublon CSS peut vivre longtemps sans se contredire frontalement.** Deux passes sur
   `.gesture-status`, chacune définissant des propriétés différentes sur les mêmes sélecteurs :
   rien ne les signalait, et un sélecteur non scopé imposait ses valeurs en silence. Trouvé en
   touchant le bloc pour une tout autre raison.

## Et la méthode qui trouve

**Le navigateur voit ce qu'aucun banc ne peut voir**, et **un fichier jamais exécuté n'est pas
livré**. Mais elle a une limite mesurée cette session : **un compte verrouillé ne montre que ce
qu'il a débloqué** — 2 expériences sur 14 avec le compte de recette actuel. Vérifier la chaîne
complète demande un compte qui la parcourt, ou l'autorisation de la faire progresser.
