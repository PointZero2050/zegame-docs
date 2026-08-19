# Boîte du poste fixe

Le portable et Codex déposent ici. Le poste fixe est le seul à retirer.
Protocole : [README.md](README.md).

---

### 2026-08-19 · du portable · La carte Communication progresse — à regarder sur la préprod

**Attendu :** vérifier le rendu de la carte aux trois étapes, puis verdict ici. Je promeus
sur ton feu vert.
**Référence :** préprod `57c56b5` · banc `verifier_accueil_m0.rb` vert (dont 7 assertions
neuves sur cette progression).

Constat de Boris : après un dialogue avec un guide, la carte de l'accueil restait sur
« Rencontre les deux guides ». Elle progresse désormais : guides → profil communautaire →
Espace d'échange. Même mécanique que la carte Imagination (destinations incrémentales).

Le parcours de vérification, avec les comptes du décor :

1. `/acces-verification/sacha?vers=/jeu` — Sacha n'a jamais dialogué : carte de base,
   « Dialoguer avec les guides » ;
2. pose une question à un guide avec lui, reviens sur `/jeu` : la carte doit inviter
   « Créer ton profil communautaire » (surbrillance, image de repli = celle de la Puissance,
   les webp dédiées n'existent pas encore) ;
3. visite `/profils/apercu`, écris une présentation, reviens : « Entrer dans l'Espace
   d'échange » ;
4. visite `/echanges` : la carte s'apaise, et reste une porte vers l'Espace d'échange —
   c'est la règle de la matrice (l'image du dernier territoire révélé reste), pas un oubli.

Nino et Lou ont déjà dialogué et un profil selon l'état du décor — Sacha est le seul
propre pour l'étape 1. Rien n'a changé dans tes vues : la carte est rendue par le même
partial, seules la config et deux `marque_la_visite` (profils#apercu, echanges#index) ont
bougé côté serveur.

---
