# Plan de développement — de l'état actuel au Festival du 1er octobre 2026

> Rédigé par Claude (portable de Boris) le 2026-08-04, à sa demande. Croise deux sources :
> une **vérification directe de l'application en production** (base réelle, routes, code) et un
> **balayage de toutes les specs** de `zegame-docs`. Là où les deux divergent, le code fait foi
> et l'écart est signalé au §6.

## 1. Ce qui est livré

Trente-neuf commits depuis le 1er août. L'inventaire de portage est intégralement couvert.

| Domaine | État |
|---|---|
| Cœur du jeu (cat. A + B) | Parcours, expériences, progression, 8 évaluations, Profil, Ressourcerie |
| Cercles et communauté (cat. C) | Cercles, cycles, Pacte-Source, séances, annuaire, blocage/signalement, messagerie minimale, Graines |
| Billetterie (lots A→F) | Événements, inscriptions, émargement, CSV, gabarits récurrents, abonnés, invitations |
| Site public | 14 pages + 3 canoniques + 4 articles appliqués + 138 pages du corpus historique |
| Le Sas | 5 parcours publics, sans compte, progression locale |
| Espace pédagogique | Édition parcours / expériences / compétences (admins) |
| Données | Migration réelle : 31 joueurs, 927 Ω, Cercle et fils de conversation |

**Santé mesurée le 2026-08-04** : 27/27 pages publiques en 200, aucune erreur console.

## 2. Le trou de gouvernance — à combler en premier

`application-festival-2026.md` §8 exige un arbitrage qui **n'est écrit nulle part dans le
dépôt** : classer chaque fonction en *Indispensable le 1er octobre* / *Utile si stabilisé* /
*Après Festival*.

Conséquence concrète : le jalon « 15-31 août — fonctions Festival indispensables » suppose une
liste qui n'existe pas. **Tant que cet arbitrage n'est pas posé, aucun chantier n'est
officiellement dedans ou dehors.** Le présent document en propose une version ; Boris tranche.

Rappel du calendrier de référence : **gel fonctionnel le 15 septembre**, 16-30 septembre
corrections bloquantes et répétition générale, 1er octobre exploitation.

## 3. Les blocages mesurés dans l'application

Sans eux, ni la vente de fin août ni le Festival ne peuvent avoir lieu sur la nouvelle pile.

> **Relevé du 2026-08-05 (soir)** — B1, B3, B4 et B5 sont levés. B2 ne tient plus qu'à une
> décision de Boris : **plus aucun blocage technique n'empêche l'ouverture de la vente.**

### B1 — Stripe est en mode TEST · ~~bloquant~~ **LEVÉ le 2026-08-04**
La clé de production est en place (`rk_live_`, restreinte), le webhook est signé, et un achat
réel de bout en bout a été encaissé puis remboursé. C'était la seule preuve qui valait.

### B2 — Le Festival n'existe pas en base · **CRÉÉ, en brouillon**
`new-civilization-festival-2026` existe : 1er octobre 2026 9 h-22 h, Paris, 200 places, 250 €,
rattaché au parcours « Festival 2026 — la journée ». Son `statut` est `brouillon` : il ne
manque que la décision de Boris d'ouvrir la vente. **Ne pas publier avant B3 et B4** — un
acheteur n'obtiendrait aucun accès.

### B3 — Aucune inscription publique · **LEVÉ le 2026-08-05, par le billet**
Choix de conception (conforme au cadrage F9) : pas de `registerable` général — **on entre dans
le jeu par billet**, pas par formulaire libre. Le lien magique du courriel de confirmation crée
le compte (l'adresse du billet, non modifiable) ; cliquer le lien prouve le contrôle de la
boîte, ce qui rend `confirmable` superflu sur ce flux. L'inscription publique sans billet reste
un choix ouvert pour plus tard, mais elle ne bloque plus rien.

### B4 — Le billet ne donne pas accès au jeu (spec F9) · **LEVÉ le 2026-08-05**
Construit et vérifié (24 contrôles HTTP de bout en bout, préprod puis production, comptes
jetables) : `Registration#user_id`, lien magique signé sans expiration dans le courriel de
confirmation, création de compte ou rattachement au compte connecté — **le billet fait foi,
pas l'adresse**. Le rattachement ouvre le Monde 0 et le parcours du jour (l'onboarding suit
par le callback existant). Secours : page `/billet` (référence + adresse, réponse uniforme),
renvoi du lien et rattachement/détachement manuels dans la console gestion. Idempotent sous
verrou ; un billet déjà rattaché à un autre compte est refusé avec un chemin de recours.

### B5 — Le mode événement d'un parcours n'existe pas (spec F7) · **LEVÉ le 2026-08-04**
Construit en trois tranches : créneaux et salles avec capacité, composition de la journée,
programme du jour et réservation par le participant (verrou de capacité et détection des
chevauchements), compteurs d'inscrits, validation générique par trois questions avec traitement
anonymisé de la troisième. Voir `mode-evenement-specification.md`.

**Reste la tranche 4** — lien magique billet → compte : c'est exactement B4, elle attend de
vrais billets. Et le contenu : `Creneau.count == 0`, la journée n'est pas encore composée.

### B6 — Le parcours du jour J · **CRÉÉ, à remplir**
Le parcours « Festival 2026 — la journée » existe (id 18) et l'événement lui est rattaché. Les
six états frontoffice de `accueil-point-zero.md` §13-15 restent à intégrer, et la journée à
composer en créneaux.

## 4. Autres manques constatés

- **Notification par courriel des fils** (`GlobalSettings.send_mail_notif_for_thread`) : jamais
  implémentée — un candidat à un Cercle n'est pas prévenu qu'on lui a répondu.
- **Marqueur « 100 Ω » du Monde 0 inatteignable** avec le barème réel — visible du joueur.
- **Couvertures d'expériences** : 21 des 22 sans image de couverture, 6 sans médaillon.
- **Espace pédagogique incomplet** : pas de création (expérience, page, parcours), pas
  d'ajout/retrait d'étape, pas d'éditeur visuel, pas d'administration des ressources
  d'expérience (13 en base), des communautés ni des joueurs.
- **CTA sans dispositif** : les articles de Codex renvoient vers « l'autodiagnostic de ton
  organisation », qui n'est pas spécifié fonctionnellement — incohérence introduite par
  l'intégration, à corriger côté texte en attendant.
- **`Onboarding`** : modèle présent, jamais utilisé, table vide — à trancher.
- **OAuth Google** : absent ; arbitrage ouvert depuis le cadrage.
- **Critères de feu vert / repli** (`application-festival-2026.md` §7) : aucun n'est coché —
  installation propre, import rejouable, sauvegarde-restauration répétée, observabilité,
  responsables du jour J.

## 5. Le plan

### Vague 0 — Trancher (Boris, cette semaine)
Arbitrage de périmètre §8 : que contient exactement *Indispensable le 1er octobre* ?
Décisions attendues : prix et jauge du Festival, OAuth Google oui/non, date de bascule DNS,
ampleur du mode événement (F7 complet ou version réduite).

### Vague 1 — Ouvrir la vente (avant fin août) — BLOQUANTE
1. Créer et publier l'événement Festival.
2. Stripe en production : clés `live` restreintes, webhook, achat réel puis remboursement.
3. Inscription publique avec confirmation par courriel (colonnes `confirmable` déjà en base).
4. Chaîne billet → compte (F9 réécrite pour Stripe interne).
5. Bascule DNS `pointzero2050.com` → Hetzner + plan de 301. Bonne nouvelle mesurée : les 138
   pages historiques sont servies à leur URL d'origine et **aucune ne collisionne** avec un
   slug du nouveau site — les redirections ne porteront que sur les pages renommées.
6. Extinction WordPress, purge des secrets (`C:\Temp`), retrait des DKIM MailPoet.

### Vague 2 — Le jour J (avant le gel du 15 septembre)
7. **Mode événement F7** — le gros morceau : créneaux, salles, capacités, compteurs, présence.
8. Parcours du jour du Festival : parcours, expériences, six états frontoffice.
9. QR codes et usage mobile debout ; tenue de charge ; compteurs temps réel.
10. Répétition d'émargement à 50 participants simulés.
11. Critères de feu vert du §7 : chacun coché, avec un responsable nommé.
12. OAuth Google si retenu en vague 0.

### Vague 3 — Monde 0 impeccable (en parallèle, éditorial + backoffice)
Le Monde 0 est ce que feront les participants du Festival : il est sur le chemin critique.
13. Lot A du Monde 0 (réécritures, consignes, durées, accroches) — purement backoffice, faisable
    dans l'espace pédagogique.
14. Lot B (4 micro-expériences) et lot D (fils narratifs et Graines manquants).
15. Correction du marqueur 100 Ω ; couvertures et médaillons (DA — Codex).
16. Recommandations de fin des 5 parcours du Sas et trous éditoriaux (poste fixe).

### Vague 4 — Après le Festival
Cercles Lot 2 (Monde 2, cycle annuel, clôture et lignées), économie Oméga réelle (Fonds du
Commun — **revue juridique et prototype à budget fictif exigés avant tout argent réel**),
autodiagnostic organisationnel, catalogue Monde 1 (12-14 parcours), modèle `World` (F4/F10),
Graines de Récit et Résonances, badges, Ressourcerie V2, mini-jeux.

## 6. Écarts entre les specs et le code — à corriger dans la documentation

Le balayage des specs a signalé comme « à faire » plusieurs chantiers **réalisés depuis**. Les
documents concernés induiraient en erreur un agent qui les lirait aujourd'hui :

| Spec dit | Réalité vérifiée dans le code |
|---|---|
| P3 blocage/signalement : « aucun modèle Block/Report n'existe » | `Blocage` et `Signalement` existent, portés et testés |
| Faille `Messaging::Thread` sans restriction de participation | **Corrigée** : `Thread#visible_par?` transcrit la règle d'origine ; scénario vérifié — un tiers est exclu en lecture **et** en écriture |
| Cercles Lot 1 : « les 5 tables ne sont pas confirmées créées » | Les cinq existent (`circles`, `circle_cycles`, `circle_memberships`, `pact_source_versions`, `circle_sessions`) |
| P1 profil communautaire et annuaire : « à faire » | En ligne (`/profils`) |
| P2 fil candidat/référent : « à faire » | En ligne ; seule la **notification par courriel** manque réellement |
| Ressourcerie V1 : import à faire | Portée, 96 fiches servies |
| F17 : « pilote Désir seul, 6 puissances restantes » | Les six configurations de puissance sont en place et les fiches répondent |
| Lot C « WordPress » du Monde 0 | Caduc — WordPress s'éteint, billetterie interne |
| 14 formulaires WP à reconstruire | **Décision Boris 2026-08-03** : non récupérés, reconstruits avec le nouveau site |

## 7. Le risque principal

La vague 1 mêle quatre développements et une bascule d'infrastructure en trois semaines, et
**touche de l'argent réel et des comptes** : une erreur y est immédiatement publique.

Recommandations :
- traiter la vague 1 dans l'ordre, chaque étape vérifiée avant la suivante ;
- **ne pas basculer le DNS le jour de l'ouverture de la vente** — laisser au moins quarante-huit
  heures entre les deux, pour que deux incidents ne se superposent jamais ;
- décider tôt de l'ampleur de F7 : c'est le seul chantier de la vague 2 qui puisse déborder le
  gel du 15 septembre, et une version réduite (créneaux et présence, sans compteurs temps réel)
  reste jouable si le calendrier se tend.
