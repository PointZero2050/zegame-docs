# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · Pour voir le rituel NEUF, c'est `sacha` — pas Nino, pas Lou

**Attendu :** utiliser `sacha` pour vérifier la première bifurcation, `nino` pour le reste.
**Référence :** préprod `0b851e6`, état relevé à l'instant sur les trois comptes du décor.

```
https://preprod.167-233-210-57.sslip.io/acces-verification/sacha?vers=/fresque
```

Le détail qui coûte une demi-heure quand il n'est pas dit : **Nino et Lou ont déjà une Graine
de Fresque** — je les ai semées hier pour débloquer ton contrôle de partage. Sur leurs
comptes, le rituel affiche donc « POSÉE » et un envoi te renverra vers la page d'édition, pas
vers la Fresque. Ce n'est pas un défaut, c'est le comportement voulu — mais tu ne verrais
jamais l'état neuf.

Relevé à l'instant, pour que tu n'aies pas à le deviner :

| compte | rituel fait | Graine de Fresque | Trace héritée |
|---|---|---|---|
| `nino` | oui | oui | non |
| `lou` | oui | oui | non |
| **`sacha`** | **non** | **non** | **non** |

Sacha est membre du canal M0 **et** du Cercle comme les deux autres : tu ne perds aucun
décor en passant par lui.

**Ce qu'il reste à voir sur un compte neuf**, dans cet ordre : le formulaire vierge (pas de
bannière « POSÉE »), l'envoi des quatre réponses, puis le retour sur `/fresque` — la Graine
doit y apparaître avec chaque réponse **sous sa question**, et la bannière « POSÉE » doit
s'allumer. Un second envoi doit t'emmener sur la page d'édition.

**Aucun compte ne teste le cas hérité** (Trace seule, sans Graine) : c'est le banc qui le
couvre, section 3 bis de `verifier_v4_imagination.rb`. Si tu veux le voir à l'œil, demande-le
ici — je pose une Trace sur un quatrième compte, je ne l'ai pas fait d'office.

---
