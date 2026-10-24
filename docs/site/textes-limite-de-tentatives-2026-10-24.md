# Texte de la page après trop de tentatives

> Note Codex — 24 octobre 2026. Réponse au portable et au poste fixe sur
> [#486](https://github.com/PointZero2050/pointzero-app/pull/486).

## Texte proposé pour le rendu commun

**Surtitre** : Une pause

**Titre** : Réessaie un peu plus tard.

**Corps** : Plusieurs tentatives se sont enchaînées. Attends un peu avant de reprendre cette action.

**Lien** : Revenir à l’accueil → `root_path`.

Le titre de page peut rester « Trop de tentatives ». La mise en forme est confiée
au poste fixe. Ce texte n’altère ni le statut 429 ni les compteurs.

## Cas particuliers

« Revenir à la connexion » convient à une variante propre à la connexion,
pas au rendu générique des billets, de la lettre ou d’un compte déjà connecté.
Ne pas promettre « quelques minutes » : la fenêtre du mot de passe oublié est
une heure dans #486. Sans durée restante fournie par le serveur, ne pas inventer
un compte à rebours ou une heure de déblocage. Ne pas déduire de la limite que
le mot de passe est faux ou que le compte est verrouillé.

## Source et portée

Vue `app/views/comptes/trop_de_tentatives.html.erb` et concern
`LimiteDeTentatives` lus à `3a677dffa37137d4b732008ebdcd5273461d29ae`.
[Commentaire dans la PR](https://github.com/PointZero2050/pointzero-app/pull/486#issuecomment-6383741218).
Relecture éditoriale uniquement, aucun test de charge, de sécurité ou rendu de
cette page en préproduction par Codex. Les clients qui reçoivent un statut seul
restent à vérifier pour qu’un 429 ne se traduise pas par une action silencieuse.
