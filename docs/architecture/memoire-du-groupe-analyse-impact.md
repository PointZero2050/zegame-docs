# Mémoire du groupe — analyse d'impact (lot C du bandeau)

> Portable, 21 octobre 2026. Rapprochement des
> [règles V1 de Codex](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/memoire-du-groupe-v1-2026-10-21.md)
> avec les objets de `pointzero-app` (préprod à `c43fbf4` et suivants), comme Codex le demande avant tout choix de
> modèle ou de route. **Rien n'est construit** : ce document nomme les correspondances, les écarts, et les
> décisions qui reviennent à Codex (règles, textes) ou à Boris (périmètre).

## 1. Où vit la Mémoire

Une Mémoire par **espace** (`Espace`, quatre gabarits : `cercle`, `groupe`, `echange`, `canal`). Les autres fils
(retour d'expérience, de parcours, candidature à un Cercle) n'ont pas de groupe : pas de Mémoire.

**Le droit de lire la Mémoire est celui de lire le fil** (`ContexteDeFil::EspaceDeDiscussion#visible_par?` :
membre actif, ou mandat de modération). Quitter l'espace retire l'accès, comme au fil — rien à ajouter.

⚠️ **Écart 1 — le gabarit.** Les règles parlent du « groupe ». Faut-il une Mémoire dans un `echange` (deux
personnes) et dans un `canal` (le canal d'un Monde, ouvert à tous ses joueurs) ? Proposition : `groupe` et
`cercle` seulement en V1 ; le canal est trop large pour qu'une sélection y reste « ce que le groupe choisit ».
→ **Boris : `groupe` et `cercle` seulement (21 octobre).**

## 2. Les sources et ce qui existe

| Règle V1 | Objet existant | Ce qui est éligible | Écart |
| --- | --- | --- | --- |
| Son propre message humain | `Messaging::Message`, `author_type = "User"` | non supprimé (`supprime_le`), auteur = moi | — |
| Message d'un autre membre | idem | après accord de l'auteur (§ 3) | aucun mécanisme de demande privée : à créer |
| Proposition | `Proposition` (B3), six états | `en_exploration`, `soumise`, `adoptee`, `a_retravailler` | `brouillon` et `retiree` exclus — confirmé par Codex, § 7 |
| Action | `ActionDeFil`, six états | tous (aucune n'est un brouillon) | — |
| Décision | `Decision`, cinq états | tout sauf `preparation` | — |
| Sondage clos | `Sondage#clos?` | clos seulement | les votants masqués (lot 2) restent masqués : la carte lit `Carte::DeSondage` |
| Rencontre « publiée, confirmée ou passée » | `PropositionDeRencontre`, cinq statuts | `proposee`, `disponibilites`, `retenue` | **écart 2** : pas d'état « passée » (une rencontre `retenue` dont le créneau est passé) ; `declinee` et `retiree` exclues ? |
| Ressource partagée au groupe | `RessourceDeLien` (aperçu d'un lien), pièces jointes (`Message#pieces`) | — | **écart 3** : une ressource n'existe pas hors de son message |

⚠️ **Écart 2 — la rencontre.** « Passée » n'est pas un statut : c'est une rencontre `retenue` dont la date est
derrière nous. La carte (`Carte::Rencontre`) le sait déjà via ses créneaux. Les rencontres `declinee` et `retiree`
sont-elles éligibles ? Proposition : non (« ni brouillon » s'étend à ce qui n'a pas eu lieu). → **Réponse de Codex au § 7.**

⚠️ **Écart 3 — la ressource.** Dans le code, un lien partagé (`RessourceDeLien`) et une pièce jointe appartiennent
à un MESSAGE ; ils n'ont ni auteur propre ni existence séparée. Conserver « la ressource » d'un message d'autrui,
c'est conserver une partie de ce message. Deux lectures possibles :
- (a) la ressource suit la règle de son message : la conserver demande l'accord de l'auteur si ce n'est pas le mien ;
- (b) la ressource se conserve SANS le texte du message, sans accord (la carte montre le lien ou le fichier seul).
Proposition : (a) en V1 — une seule règle, pas de découpage d'un message. → **Confirmé par Codex au § 7.**

Les objets structurés sont **des liens vers leur état courant** : la carte de Mémoire relit l'objet (le modèle
`Carte` le fait déjà pour le fil), jamais une copie. Aucun extrait de texte personnel n'est aspiré d'un objet.

## 3. L'accord de l'auteur

Rien n'existe pour « une demande privée à un autre membre, qu'il accepte ou refuse ». Le plus proche :
`AccordDeRegard` (un choix par personne, versionné) et `Engagements` (ce qui attend un geste de moi).

Proposition :
- une table `demandes_de_conservation` (message, version, demandeur, statut : `en_attente`, `acceptee`,
  `refusee`, `annulee`, `caduque`) — **une seule demande active par message et par version** (index unique
  partiel) ;
- la demande apparaît chez l'auteur comme un **engagement** (`Engagements`, nouveau type `:conservation`) :
  l'accueil, l'attention et le Centre la montrent, sans compteur public ;
- **pas de courriel en V1** — « Essentiel » (lot A) ne couvre que mentions et réponses ; un courriel de demande
  serait une nouvelle catégorie de notification. → **Boris : pas de courriel en V1 (21 octobre).**

⚠️ **La version.** Un message se modifie (`Message#modifier_par!`, qui pose `edite_le`). La demande et l'entrée
retiennent l'**empreinte du texte accordé** (SHA-256), pas une date : une modification la change, l'entrée passe
**suspendue** et la demande **caduque** (« Le message a changé. Cette demande n'est plus valable. »).

**Compte fermé** (`FermetureDeCompte`) : les messages restent, l'auteur est neutralisé. Ses demandes en attente
deviennent caduques (« l'auteur ne peut plus être sollicité »). Ses entrées déjà accordées suivent le message :
elles restent, comme lui. Un compte purgé (bancs) emporte ses lignes.

## 4. Retrait, masquage, droits

**Retrait** : l'auteur de la source, la personne qui l'a conservée, et le **gardien** de l'espace
(`EspaceMembership` rôle `gardien`).

⚠️ **Écart 4 — « facilitateur, administrateur ayant réellement ce droit dans cet espace ».** Dans le code, le
mandat de modération **lit les espaces sans y agir** (`EspaceDeDiscussion` : « le mandat de modération lit sans
agir »), sauf pour masquer une réponse de regard. Aucun facilitateur ni administrateur n'a donc aujourd'hui de
« droit de gestion » dans un espace où il n'est pas gardien. Proposition : en V1, le retrait par la modération
passe par la SOURCE (son masquage ou sa suppression rend l'entrée indisponible), pas par un droit nouveau sur la
Mémoire. → **Boris : par la source en V1 (21 octobre).**

**Retirer** supprime la ligne de Mémoire, rien d'autre ; aucune copie du texte n'est gardée. Une source supprimée,
masquée ou devenue illisible rend l'entrée **indisponible** (« Cet élément n'est plus accessible. »), sans extrait
ni pièce — la carte relit la source, elle n'a rien en cache. Un rétablissement ne ressuscite pas une entrée retirée
(la ligne n'existe plus).

**Signaler** une entrée : le mécanisme existant (`Signalement`, qui vise un message) s'applique à la source.

## 5. Ce qui ne bouge pas

Ni Trace, ni Graine, ni Omégas, ni badge ; aucun contexte de regard (`RegardReponse` ne lit pas la Mémoire) ;
la recherche du fil (lot B) et l'export (`ExportDeFil`) ne lisent pas la Mémoire. Un regard IA ne conserve rien,
et ses messages ne sont pas éligibles.

## 6. Contrat proposé (après les réponses)

- **Tables** : `entrees_de_memoire` (espace, source polymorphe, conservee_par, empreinte, suspendue_le,
  timestamps ; unique sur espace + source) ; `demandes_de_conservation` (§ 3).
- **Routes** : conserver (son message, un objet), demander (le message d'autrui), accepter / refuser / annuler une
  demande, retirer une entrée ; la liste `GET /espaces/:id/memoire` (HTML pour la vue du poste fixe, « Afficher :
  Mémoire »).
- **Bancs** : les cas de la recette de Codex (§ « Analyse d'impact et recette »), un par section, dont l'unicité
  sous clics concurrents et la modification avant et après accord.

## 7. Arbitrages et questions

**Arbitrages de Boris (21 octobre 2026, au soir)** — les trois propositions retenues :
- **la Mémoire vit dans les espaces `groupe` et `cercle` seulement** ; ni `echange`, ni `canal` en V1 ;
- **le retrait par un facilitateur ou un administrateur passe par la SOURCE** (masquage, suppression) en V1 ;
  aucun droit nouveau sur la Mémoire hors du gardien ;
- **la demande à l'auteur est un engagement seulement** (accueil, attention, Centre) ; aucun courriel en V1.

**Réponses de Codex — 21 octobre 2026, nuit** :

| # | Question | Réponse |
| --- | --- | --- |
| 2 | Rencontres `declinee` / `retiree` : éligibles ? « Passée » = `retenue` au créneau passé ? | Non aux deux états exclus. Oui : « passée » = `retenue` dont le créneau retenu est passé ; aucun fait de présence ou d'accomplissement déduit. |
| 3 | Ressource d'un message d'autrui : accord de l'auteur (a) ou conservation seule (b) ? | **(a)** : accord de l'auteur du message, ressources comprises dans la version présentée ; une seule entrée liée au message, pas de conservation autonome pour contourner l'accord. |

### Précisions de conception — ajout Codex

Une rencontre déjà conservée devenue `declinee` ou `retiree` est indisponible
dans la Mémoire, sans ancien extrait en remplacement. Son histoire reste dans
le Fil selon les droits habituels. Les propositions `brouillon` / `retiree`
restent exclues à l'ajout, comme les décisions en `preparation`.

Le texte de la demande montre aussi les ressources du message concerné.
Si les pièces jointes peuvent être ajoutées, retirées ou remplacées après
l'accord, leur composition fait partie de la version à contrôler : l'empreinte
du seul texte ne suffit pas. Pas de fichier recopié ni de droit de téléchargement
élargi par la conservation. La règle, ses microtextes et les trois arbitrages
de Boris sont maintenant repris dans les règles V1 liées en introduction.

Ces réponses complètent l'analyse ; elles ne valent pas validation du plan
technique par Boris ni construction du lot C. Le portable garde la préparation
de ce plan, puis son implémentation après l'arbitrage prévu avec Boris.
