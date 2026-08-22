# Recette du Monde 0 — août 2026

Passe de recette manuelle menée par Boris avant l'ouverture du Monde 1.
Le portable tient ce fichier : Boris rapporte, le portable transcrit, route et clôt.

## Où tester

**https://preprod.167-233-210-57.sslip.io** — et non la production.

Trois raisons, dont une mesurée : (1) les deux arbres sont **identiques** aujourd'hui
(`git diff origin/preprod main` est vide), donc tester la préprod teste exactement le code de
production ; (2) les comptes jetables n'y polluent pas les témoins de production (31 comptes,
927 Ω, qu'on surveille à chaque promotion) ; (3) elle est publique, aucune clé n'est requise.

**Le métaparcours du Monde 0 est à sens unique.** Franchir un seuil pose un marqueur qui ne se
retire pas d'un clic : le faire sur son compte réel consomme l'étape sans retour. Le portable
fournit donc des comptes jetables, et sait les **remettre à n'importe quelle étape** — y compris
« jamais entré », qui est l'état le plus difficile à retrouver et le plus important à tester.

## Comment rapporter

Un constat = un bloc. **Une ligne suffit quand c'est évident** ; les champs ci-dessous ne sont
là que pour ce qui ne l'est pas.

```
PAGE     /parcours/point-zero-monde-0
COMPTE   jetable A (Monde 0, n'a pas rejoint l'Espace)
GESTE    je clique « Entrer dans l'Espace d'échange »
VU       la page se recharge sur elle-même, rien ne change
ATTENDU  le fil s'ouvre dans le panneau de droite
HEURE    ~14 h 35
TYPE     bug
```

Ce qui fait gagner du temps, et pourquoi chaque ligne mérite sa place :

- **COMPTE, avec son Monde.** C'est le champ le plus rentable. Le 22 août, un défaut a vécu
  vingt-quatre heures en production parce que `/echanges` servait une page au Monde 0 et une
  autre au-delà : le même geste, sur deux comptes, donnait deux résultats. Sans ce champ, un
  rapport peut être irreproductible sans que personne comprenne pourquoi.
- **HEURE, même approximative.** Les journaux de production et de préprod sont lisibles et
  horodatés à la requête près. Avec un « vers 14 h 35 », le portable retrouve la requête exacte,
  son identifiant et sa trace — c'est la différence entre « je reproduis » et « je devine ».
- **ATTENDU.** Parfois le désaccord porte sur l'attendu, pas sur le code. L'écrire évite de
  corriger ce qui n'était pas cassé.
- **TYPE**, parce que trois agents se partagent le code et qu'un constat mal routé coûte une
  session entière :

| type | ce que c'est | pour qui |
|---|---|---|
| `bug` | ça ne marche pas, ça plante, ça n'enregistre pas | **portable** |
| `visuel` | ça marche mais c'est mal placé, illisible, cassé sous mobile | **poste fixe** |
| `éditorial` | les mots, un titre, un ordre, une promesse | **Codex** |
| `produit` | « est-ce qu'on veut ça ? » — ce n'est pas un défaut, c'est un arbitrage | **Boris** |

En cas de doute sur le type : ne pas trancher, écrire le constat. Le routage est le travail du
portable, pas celui du testeur.

## Le parcours à couvrir — les sept invitations du Monde 0

Une par Puissance. C'est la structure réelle de `config/monde_0.yml`, pas une liste inventée.

| # | Puissance | L'invitation | Destination |
|---|---|---|---|
| 1 | Désir | Crée ton jumeau dans Immateria | `/immateria` |
| 2 | Volonté | Commence le Monde 0 de la Marelle | `/parcours/point-zero-monde-0` |
| 3 | Imagination | Produis ta première Graine de Récit | `/fresque` |
| 4 | Émotion | Choisis un premier héros inspirant | `/heros` |
| 5 | Communication | Choisis ce que tu montres de toi | `/profils/apercu` |
| 6 | Intuition | Apprends à voir ce qui agit derrière ce que tu vois | `/premieres-cles` |
| 7 | Transcendance | Observe ton Moteur de Conscience | `/users/me` |

Communication a quatre étapes et c'est la plus longue : profil communautaire → Espace d'échange
(écran de seuil, puis le fil) → Annuaire. C'est aussi la zone la plus remuée ces jours-ci.

## Constats

*(vide — la passe n'a pas commencé)*

| # | Page | Compte | Constat | Type | Pour qui | État |
|---|---|---|---|---|---|---|
