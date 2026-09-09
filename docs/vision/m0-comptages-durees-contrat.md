# M0 — Contrat d'affichage des compteurs et des durées

Note Codex — réponse à la remontée M0-13/M0-14 du poste fixe dans `46f0bc7`, après la demande de Boris « Récupère et continue ». Précisions d'intégration du [rapport d'audit](https://github.com/PointZero2050/zegame-docs/blob/main/docs/vision/audit-parcours-lineaire-m0-preprod-2026-09-09.md). Les mesures ci-dessous sont celles rapportées par Claude, sans nouvelle mesure de la base dans cette réponse.

## Comptage : 19 expériences, puis un épilogue

Le numéro éditorial suit les 19 expériences dans leur ordre, facultatives comprises. L'épilogue conserve son objet technique et ses conditions actuelles, mais n'entre dans aucun compteur d'expériences. Aucun changement de statut obligatoire en base n'est demandé.

| Surface | Texte et règle |
|---|---|
| Présentation du parcours | « 19 expériences : 16 essentielles et 3 facultatives, puis un épilogue. » |
| Position courante, carte et fiche | « Expérience {rang} sur {total} » ; aujourd'hui total = 19, même rang sur les deux surfaces. |
| Nature de l'expérience | Mention séparée « Essentielle » ou « Facultative ». |
| Progression | « Expériences essentielles accomplies : {accomplies} / {total_essentielles} ». Compter des accomplissements réels, pas le rang courant. |
| Facultatives | « Expériences facultatives accomplies : {accomplies} / {total_facultatives} », si ce compteur est montré. |
| Lien vers la carte complète | « Voir les 19 expériences et l'épilogue » ; nombre dérivé des données. |
| Chapitres | 7 / 7 / 5 expériences, avec la répartition essentielles/facultatives si utile. |
| Épilogue | Bloc distinct au pied du troisième chapitre, titré « Épilogue — Ton espace est prêt », sans « Expérience 20 sur 20 ». CTA existant « Ouvrir mon espace ». |

Le bloc épilogue reste soumis à son dévoilement et à son accès actuels ; pas de quatrième chapitre. Ne pas montrer l'ensemble des détails futurs pour faire fonctionner le lien de carte. Les nombres ci-dessus décrivent le contenu actuel : implémenter des populations explicites, pas des constantes dispersées ni une soustraction aveugle de 1. Une expérience sautée en recette n'est pas accomplie. La clôture et l'accès au Monde 1 gardent leurs règles séparées.

## Durées : une estimation publiée par expérience

**Source de lecture retenue pour la carte, la fiche et les totaux : `challenge.duration`.** C'est le contrat d'affichage, pas une certification des valeurs actuelles. La somme des chaînes `sequence[].duree` n'est pas une source fiable à calculer automatiquement : elle peut mêler gestes successifs, temps inclus, alternatives et attentes.

**Convention retenue : « + ».** Afficher « Temps estimé des expériences essentielles : {durée} », puis « + {durée} pour les expériences facultatives ». L'épilogue est hors de ces deux sommes ; sa propre estimation peut figurer dans son bloc si elle est renseignée et vérifiée. Ne pas reprendre les 6 h 30 ou 1 h 30 de démonstration, ni republier les anciens totaux sans recalcul de ces populations.

Une estimation conflictuelle n'est pas résolue en choisissant arbitrairement l'une des deux valeurs. Pour E1, le conflit 5 min / 10 min reste à réconcilier avec le module réel ; aucun des deux chiffres n'est validé ici. Même exigence pour l'Atelier : durée d'activité actuelle, hors attente d'un rendez-vous ou d'une validation. Les durées des lectures autonomes restent indicatives.

**Pendant la réconciliation :** sur une expérience dont l'estimation est contradictoire ou inconnue, afficher « Durée à préciser » à la place d'un chiffre. Si une population contient une telle expérience, son total affiche « Temps total à préciser » ; ne jamais traiter une valeur manquante comme zéro. Les expériences non litigieuses peuvent conserver leur estimation. Le mécanisme permettant d'identifier ces cas doit être explicite et revu par le portable, sans état parallèle caché dans une vue.

Les minutages de gestes vérifiés peuvent rester visibles comme repères ; ceux qui contredisent l'estimation globale attendent réconciliation. Ne pas les rééchelonner artificiellement pour obtenir un total imposé.

## Livraison et recette

**Portable :** inventaire E1–E19 + épilogue avec durée en base, durées des gestes, source éditoriale ou mesure disponible, contradiction éventuelle ; analyse d'impact des sélections et de la représentation des durées inconnues. Proposer les corrections chiffrées documentées ; les valeurs non établies restent ouvertes. Ne pas modifier progression, validation ou Ω pour corriger des compteurs.

**Poste fixe :** porter les libellés et le bloc épilogue dans les vues, une fois les sélections partagées avec le portable. Reprendre les corrections déjà livrées dans #168/#169, sans chantier concurrent sur les mêmes fichiers.

**Critères de recette :** E1 affiche 1/19 et zéro essentielle accomplie sur un compte neuf ; E11 est facultative et conserve son rang 11/19 ; E19 affiche 19/19 ; l'épilogue n'a pas de numéro d'expérience. Carte et fiche donnent la même position. Un saut de recette laisse le compteur d'accomplissements inchangé. Un rejeu ne l'incrémente pas. Les deux sous-totaux de durée excluent l'épilogue, distinguent essentielles et facultatives et signalent une estimation incomplète. Vérifier zéro/une/plusieurs expériences et une durée absente dans les helpers, puis les rendus desktop/mobile sur le contenu actuel.

M0-13 est spécifié, pas déclaré livré. M0-14 a sa convention d'affichage, mais reste ouvert tant que l'inventaire et les estimations conflictuelles ne sont pas réconciliés. Aucun montant de durée métier n'est modifié par ce document.
