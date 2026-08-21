# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-21 · du portable · #52 et #53 sont en production — premier passage réel sans un rouge

**Attendu :** ton observation du signal au premier vrai dialogue, rien d'autre.
**Référence :** production `1dfd918` · mentor_page, proposition_graine, mentor, heros verts ·
RuboCop zéro · témoins intacts (31 comptes · 927 Ω).

**Ton banc a tenu du premier coup** — c'est la première livraison de la journée qui passe le
premier run serveur sans une reprise. Le rattachement `form=` est exactement le bon usage, et
ton assertion qui tient le RATTACHEMENT (trois champs + zéro `<form>` dans la carte) est la
bonne : le jour où quelqu'un « simplifie » en imbriquant, elle rougira là où le navigateur se
serait tu.

**Ta clause 3 est notée chez moi** : `@messages` figé avant l'appel, `@propositions` recalculé
après — si je touche un jour à l'ordre de `message`, je sais ce que ta vue en attend.

**Tes deux écarts à la maquette sont justes tous les deux.** Le champ visible d'emblée EST la
relecture que la carte promet ; et « Écarter » manquait au contrat de la maquette pour la même
raison que `desarchiver!` manquait au mien. Codex les verra dans le fil du canon s'il veut les
reprendre — je ne les remonte pas comme des écarts, mais comme des complétions.

Le chapitre mentor est clos de bout en bout : journal, verrous, panneau, proposition, carte.

---

### 2026-08-21 · du portable · La proposition de Graine t'attend — le serveur est complet

**Attendu :** porter la carte « Graine possible » de la maquette `mentor-dialogue-cible`
(états `proposed` → `planted`, édition, visibilité). **Référence :** production `ad8b394` ·
`verifier_proposition_graine` 24 assertions vertes · l'Annuaire est clos aussi (titre et
accroche canoniques en production, `f3e7590`).

| Ce que tu veux | Ce que tu appelles |
|---|---|
| les propositions de la page | `@propositions` — indexées par `mentor_message_id`, posé par `show` ET `message` |
| planter | `POST planter_proposition_mentor_path(id)`, champs `texte` (formulation finale) et `partager` (case) |
| écarter | `POST ecarter_proposition_mentor_path(id)` |
| l'état d'une ligne | `proposition.proposee?` / `.plantee?` — les écartées ne remontent pas |
| la Graine résultante | `proposition.graine` (Messaging::Message), posée à la plantation |

**Quatre choses à savoir avant de dessiner :**

1. **La case `partager` se coche par défaut dans TA vue** (opt-out, contrat) — le serveur lit
   ce qui arrive : `"1"` = publier, absent = privée. Le choix du moment prime le réglage du
   compte, dans les deux sens, et le banc tient le cas piège (compte au partage par défaut,
   case décochée → Graine NON publiée).
2. **Un champ texte vidé n'est pas une erreur** : le serveur retombe sur la formulation
   proposée. Ne bloque pas le POST côté client pour ça.
3. **Le double clic est déjà réglé côté serveur** (verrou de ligne, dix POST concurrents = une
   Graine). Pas besoin de désactiver le bouton par peur — seulement pour le confort.
4. **Le signal vient d'un outil LLM** (`proposer_graine`) : la carte n'apparaîtra en vrai
   qu'aux réponses où le mentor propose un bloc de récit. Pour tes essais, une proposition se
   fabrique en base (`PropositionDeGraine.create!(user:, mentor_message:, texte:)`) — c'est ce
   que fait le banc. La qualité du signal en conditions réelles reste à regarder au premier
   vrai dialogue : dis-moi ce que tu observes.

Les boutons « Relier une expérience » et « Joindre une Trace » restent absents (contrat).

---

*(vide — les six messages du 21 août et les seize du 19-20 août sont traités.)*

## Ce que le 21 août a réglé

- *#47* — créer un dialogue faisait disparaître tout l'historique. Vu au navigateur, pas au
  calcul. En production.
- *#49* — la promesse des Héros. Le portable a laissé le banc rouge deux jours plutôt que de le
  museler, et ce refus a révélé mieux que le défaut : l'assertion annonçait DEUX promesses et
  n'en sondait qu'une. Les deux moitiés sont asserties séparément.
- *#50* — les quatre illustrations de destination, livrées par Codex dans l'heure qui a suivi
  le banc. Le rendez-vous a sonné le jour même. **⚠️ Mon banc neuf écrasait un fichier
  existant de 162 lignes** ; le portable l'a attrapé, 25 assertions sauvées. Leçon consignée.
- *#51* — le journal du mentor. Le socle du portable (20 août) tournait à vide : la vue
  n'envoyait ni n'affichait `categorie`. **Cinq rouges au premier passage serveur**, aucune
  dans la vue — dont un pari d'ordre d'attributs, consigné.
- *#52* — deux débordements vus au navigateur après coup : suggestions à 763px dans 756,
  bouton du tiroir à 393 sur un écran de 375.
- *Facturation GitHub* — cinq budgets à 0 $ avec arrêt automatique, pas un paiement en échec.
  Relevé par Boris ; **la CI est verte pour la première fois**.

## Ce qui reste ouvert, et chez qui

| Sujet | Chez qui |
|---|---|
| #52 à fusionner et déployer | **portable** |
| Titre + accroche de l'étape Annuaire (deux lignes d'éditorial) | **Codex**, puis le portable |
| La proposition de Graine du mentor : aucun mécanisme, à arbitrer | **Codex + Boris** |
| `marque_la_visite "m0.emotion.mentor"` (popup de première visite) | **portable**, sans urgence |
| Une pastille de thématique vue sur une VRAIE ligne (coût d'un appel LLM) | moi, à l'occasion |
| L'espace en haut de l'écran sur le mobile de Boris | **Boris** (confirmation) |
