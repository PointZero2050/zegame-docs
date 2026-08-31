# Réponses de raccord — parcours linéaire du Monde 0

> **Codex — 31 août 2026.** Réponse consolidée aux analyses du portable et du poste fixe.
> La référence visuelle publiée est `zegame-prototypes/main@509fef9`, accessible sur
> <https://maquettes.167-233-210-57.sslip.io/pz-cible/parcours-lineaire-m0-cible/?view=journey>.

## 1. Les pages de Puissance restent des destinations durables

Le parcours linéaire remplace les sept cartes comme accueil ; il ne supprime aucune fonction.
Les pages de Puissance restent accessibles après leur éveil :

- par le menu `Puissances`, qui devient leur accès durable principal ;
- par les CTA contextuels d'une Expérience ou d'une autre page lorsque ce lien a un sens ;
- jamais avant leur éveil dans les menus ou les liens proposés au Joueur.

Une URL directe vers une fonction encore endormie montre seulement une explication courte et
`Reprendre mon passage`. Le menu n'est donc pas le chemin unique, mais il est la boussole stable.

## 2. Indicateurs : ne pas transformer des destinations en faux compteurs

Le tableau de bord proposé après le M0 traite chaque indicateur comme une **entrée vers une
page**, avec une icône, son libellé et `Voir`. Ce ne sont pas tous des mesures chiffrées.

| Puissance | Affichage V1 | Valeur chiffrée admise |
|---|---|---|
| Désir | Immateria · Quêtes | aucune tant qu'une source de quêtes n'est pas raccordée |
| Volonté | Parcours actif | `n/m Actions`, source existante |
| Imagination | Graines · Traces | aucune dans `Monde0Etats` ; liens seulement |
| Émotion | Mentor | aucune tant que le choix actif n'est pas exposé comme donnée de façade |
| Communication | Échanges · Profil | aucune ; liens seulement |
| Intuition | Guides · Ressources · Clés | `n/10 Clés`, en nommant exactement ce que le compteur mesure |
| Transcendance | Moteur · Accomplissements · Omégas | aucune mesure propre à la carte ; le total d'Omégas reste global |

Une fonction activée peut donc afficher `Accessible` ou son état textuel réel sans nombre. Un
compteur n'apparaît que lorsqu'une source et son sens sont tous deux établis.

## 3. Immateria fait partie du périmètre, sans bouton de rattrapage

L'événement idempotent de fin du tutoriel est nécessaire à l'Expérience 1 et appartient au
périmètre serveur. La cible ne garde pas un bouton manuel de validation en V1 : il créerait dès
le premier passage une exception à la règle de reconnaissance par l'action réelle.

Le retour porte le contexte du parcours. Si Immateria ne peut pas encore émettre cet événement,
l'intégration de l'Expérience 1 est bloquée honnêtement ; elle n'est pas simulée par un CTA.

## 4. Clôturer le M0 n'ouvre pas automatiquement le M1

`Ouvrir mon espace` est la dernière transition narrative du Monde 0. Elle transforme l'accueil
en tableau de bord et marque la clôture idempotente du parcours. Elle ne vaut pas validation du
Monde 1.

Le passage au Monde 1 reste une décision distincte, notamment liée à la participation reconnue
à l'Atelier. Le tableau de bord intermédiaire dit explicitement que le Joueur sera averti lorsque
ce passage sera validé.

## 5. L'Expérience 14 se reconnaît par une évaluation réelle

`Lire mon Moteur` emprunte temporairement la page encore verrouillée grâce au contexte
d'excursion. Le geste probant est une première évaluation de Puissance enregistrée. Observer la
circulation Ombre/Lumière et ouvrir la provenance des Omégas sont des gestes guidés de lecture ;
ils n'exigent pas trois listeners artificiels.

La reconnaissance de l'évaluation éveille Transcendance. Le Moteur et les Accomplissements
deviennent alors des destinations durables dans le menu.

## 6. Les chapitres deviennent des respirations, pas des tableaux de bord

La nouvelle page de chapitre remplace l'ancien chemin de médaillons :

- aucune liste de « Puissances dominantes » n'est ajoutée ; leur éveil se lit dans le parcours ;
- aucun champ `question:` générique n'est nécessaire ; le texte narratif porte l'entrée ;
- l'interface sépare `CHAPITRE X` et le titre court (`Je pressens`, `Je relie`, `Je contribue`) ;
- l'ancien `repeat(5, 1fr)` et sa colonne vide sont donc périmés par cette page mobile immersive.

## 7. Menu Actions M1 : libellé de la ressource

Le sous-titre canonique de `Partager une ressource` devient :

> Joindre un fichier ou partager un lien dans le fil.

L'aperçu éventuel du lien reste automatique et ne doit pas être promis comme un geste séparé.
`Partager un élément de Récit` reste distinct et n'apparaît que lorsque sa route est réellement
disponible.

## 8. Aides contextuelles

Le lot éditorial demandé est livré dans
[aides-contextuelles-pages-m0.md](../pedagogie/aides-contextuelles-pages-m0.md). Il couvre les
gabarits encore dépourvus d'aide et confirme : ouverture uniquement au clic sur `?`, jamais au
premier chargement, aucun effet sur progression ou Omégas.

## 9. Arbitrage confirmé par Boris

Le `Signe de reconnaissance` reste une Expérience facultative. Communication possède déjà un
geste obligatoire réel dans l'Expérience 9 ; imposer aussi le Signe alourdirait le chemin
principal. L'Expérience reste accessible, rapporte ses Omégas lorsqu'elle est accomplie et ne
bloque jamais la progression essentielle.
