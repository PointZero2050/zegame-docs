# Mouvement M1 — correspondance éditoriale des états existants

> **Arbitrage Codex, 29 août 2026.** Cette note répond au point laissé ouvert par
> [`analyse-impact-mouvement-m1.md`](analyse-impact-mouvement-m1.md) : traduire les états
> techniques existants dans la grammaire unique du Mouvement, sans fusionner les tables ni
> inventer une transition qui n'a pas eu lieu.

## 1. Principe de lecture

Le Joueur voit quatre moments principaux :

`À éclaircir → À consentir → En mouvement → Accompli`

Trois issues restent explicites : `À poursuivre`, `À réviser` et `Abandonné`. Elles ne sont
pas de nouvelles étapes du parcours. `Empêché` est un signal temporaire attaché à `En
mouvement`.

La façade ne réécrit pas les modèles. Elle calcule un **état de lecture** et conserve dans le
détail l'objet source, son état technique, son historique et les droits réellement ouverts.
Un bouton n'apparaît que si la commande sous-jacente existe et si le Joueur peut l'exécuter.

## 2. Table de correspondance

| Objet et état existants | Lecture Mouvement | Libellé secondaire visible | Règle |
|---|---|---|---|
| Proposition · brouillon | À éclaircir | Brouillon | Visible par ses seuls éditeurs tant qu'elle n'est pas publiée. |
| Proposition · en exploration | À éclaircir | Contributions ouvertes | La carte accueille questions et reformulations. |
| Proposition · soumise | À consentir | Soumise au consentement | La version soumise est figée ; les personnes éligibles et le protocole doivent être visibles. |
| Proposition · adoptée | En mouvement | Passage consenti | Compatibilité avec le cycle historique ; ne signifie pas que l'exécution est accomplie. |
| Proposition · à retravailler | À réviser | Reformulation attendue | Une nouvelle version revient ensuite à `À éclaircir`. |
| Proposition · retirée | Abandonné | Retiré par son auteur | L'historique reste lisible ; aucun CTA de reprise implicite. |
| Décision · préparation | À éclaircir | Consentement à préparer | Le protocole, les personnes éligibles ou la version ne sont pas encore figés. |
| Décision · ouverte | À consentir | Consentement ouvert | Les consentements et tensions vivent dans la carte. |
| Décision · close + résultat adoptée | En mouvement | Consentement obtenu | La clôture ne vaut ni réalisation ni Oméga. |
| Décision · close + résultat à retravailler | À réviser | Nouvelle formulation attendue | La cause reste visible dans l'historique. |
| Décision · révisée | À réviser | Révision demandée | La version révisée revient à `À éclaircir` seulement après une action explicite. |
| Décision · annulée | Abandonné | Décision annulée | Le motif et l'auteur de l'annulation sont affichés lorsqu'ils existent. |
| Décision · close sans résultat | — | Issue à renseigner | État incohérent à signaler ; la façade ne choisit jamais une issue à la place du serveur. |
| Action · proposée | En mouvement | Porteur attendu | Le Mouvement existe, mais personne ne l'a encore accepté. |
| Action · acceptée | En mouvement | Prise en charge | Le porteur est nommé ; le premier geste peut commencer. |
| Action · en cours | En mouvement | En cours | Afficher porteur, appuis, échéance et prochain geste. |
| Action · bloquée | En mouvement | Empêché | Afficher l'obstacle et le geste permettant de le lever ; ne pas la classer comme abandonnée. |
| Action · accomplie | Accompli | Trace de résultat | L'accomplissement cible exige une Trace ; un ancien objet sans Trace reste signalé comme historique incomplet. |
| Action · abandonnée | Abandonné | Action abandonnée | Le motif reste visible et la reprise crée un nouveau passage explicite. |
| Objection · ouverte | À consentir | Tension ouverte | Indicateur enfant de la Décision, jamais carte Mouvement autonome. |
| Objection · répondue | À consentir | Réponse apportée | La réponse ne vaut pas résolution par l'auteur. |
| Objection · levée | À consentir | Tension résolue | N'empêche plus le passage selon le protocole annoncé. |
| Objection · maintenue | À consentir | Tension maintenue | Bloque, fait réviser ou ouvre un arbitrage selon le protocole ; la façade ne tranche pas. |

## 3. Les cinq états de rencontre et les deux états de sondage

Les cinq états de `PropositionDeRencontre` — `proposée`, `disponibilités recueillies`,
`confirmée`, `passée`, `annulée` — **ne sont pas convertis** en états du Mouvement. Une
rencontre demeure une rencontre. Elle peut être la source d'un Mouvement créé explicitement,
auquel cas la carte conserve un lien vers elle.

De même, un sondage reste `ouvert` ou `clos`. Son résultat peut nourrir ou déclencher un
Mouvement, mais `clos` ne signifie ni `consenti` ni `accompli`.

Cette séparation explique le compte relevé dans l'existant : les 26 états comprennent les
cinq états de rencontre ; seuls les états de Proposition, Décision, Action et Objection
participent à la lecture du Mouvement.

## 4. Priorité quand plusieurs objets décrivent le même passage

Pour éviter deux cartes successives à l'écran :

1. une Décision liée à une Proposition porte la lecture du passage dès qu'elle existe ;
2. la Proposition reste accessible dans l'historique et fournit ses versions ;
3. une Action autonome porte directement un Mouvement personnel ;
4. aucune Action n'est rattachée à une Décision par ressemblance de titre, de date ou de
   message : le lien doit être explicite ;
5. une Objection et un Consentement restent des éléments internes à la carte Décision.

Si le lien explicite manque, la façade montre deux objets honnêtes plutôt qu'un Mouvement
artificiellement recomposé.

## 5. Informations visibles sur la carte

La carte compacte montre seulement :

- le titre et l'état principal ;
- un libellé secondaire utile (`Porteur attendu`, `Empêché`, `Tension maintenue`…) ;
- le porteur, l'échéance et le prochain geste lorsqu'ils existent ;
- le nombre de tensions ouvertes ou maintenues ;
- un CTA principal réellement autorisé.

Le détail conserve le type et l'état sources, les versions, les consentements, les tensions,
les changements de porteur et les motifs de retrait, d'annulation ou d'abandon. Ce registre
est une garantie d'audit, pas le vocabulaire principal de navigation.

## 6. Garde-fous de portage

- Ne jamais déduire un consentement d'une absence de réponse.
- Ne pas afficher `Soumettre au consentement` avant l'éligibilité par personne et les
  notifications fiables identifiées par l'analyse d'impact.
- Ne jamais distribuer d'Oméga sur une transition de la façade.
- Ne pas présenter la projection en Mémoire comme disponible : le modèle n'existe pas.
- Ne pas marquer une Action historique `Accompli` comme conforme à la cible si aucune Trace de
  résultat ne peut être retrouvée.
- Tester séparément l'état technique, l'état de lecture, le libellé secondaire, les droits et
  le CTA : leur convergence éditoriale ne doit pas masquer leurs différences fonctionnelles.

