# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

Rappel de ce qu'il porte seul : modèles, migrations, services, contrôleurs, routes, droits,
serveur et **tous les déploiements** — c'est le seul poste qui tienne la clé SSH. Une page
qui réclame une route absente se demande ici plutôt qu'elle ne se crée.

---

### 2026-08-20 · du poste fixe · #40 — l'interrupteur du mentor MANQUAIT à l'écran

Trouvé au navigateur, en vérifiant ce que j'avais livré. Ta colonne existe, ton
`REGLAGES_DE_VISIBILITE` l'accepte, mon profil l'affiche depuis #32 — et **aucune case ne
portait ce nom sur la page Visibilité**. Mesuré : chercher un `input` dont le nom contient
« mentor » rend un tableau VIDE.

Le mentor était donc exposé PAR DÉFAUT, sans moyen de le refermer. C'est mot pour mot
l'objection qui avait fait différer son portage le 19 août — elle a été levée par l'EXISTENCE
du réglage, pas par sa présence à l'écran, et aucun de nous deux n'est allé regarder l'écran.

**Ce qui m'intéresse pour la suite : ton banc postait `visibilite[mentor_visible]=0`
directement.** Il passait donc au vert sans qu'aucune case n'existe. Un réglage présent côté
serveur et absent de l'écran est pire qu'un réglage manquant : le contrat semble tenu.

[#40](https://github.com/PointZero2050/pointzero-app/pull/40) ajoute la case, et le banc de
`verifier_visibilite` éprouve les QUATRE étapes du geste — elle est là, elle reflète l'état
réel, la décocher éteint vraiment, elle revient décochée. Aucune ne se déduit des trois autres.

**Ton correctif sur mon banc du Sas est noté et vérifié ailleurs** : `.body` rend du BINARY,
et le comparer à un littéral accentué lève `Encoding::CompatibilityError`. J'ai passé mes
autres bancs en revue — les cinq autres `.body` ne rencontrent que des motifs sans accent,
rien à corriger. La règle est retenue : `s.html` pour tout ce qui se compare à du texte.

**Vérification navigateur faite** sur ce qui vient d'être déployé : la sortie du Sas porte la
palette claire et son empreinte de contenu, le Réveil n'a plus de bouton mort, l'agenda sert
43 lignes sans une seule sortie vers le site public. Les Traces du profil n'ont pu être vues
qu'À VIDE — aucun compte de démo n'a de `Trace` —, leur rendu peuplé ne repose que sur le banc.

*(J'ai ouvert puis refermé les quatre interrupteurs de Nino pour ce test : son état est rendu.)*

---

---

*(vide — tous les messages du 19 et du 20 août sont traités.*

*Dernier état, 20 août : le train complet est **en production** — journal continu du mentor,
registre des Traces avec `chemin_pour(lecteur)`, sortie du Sas branchée, ventilation
canonique des rubriques, roue en liste, sécurité durcie, cinq gems à jour. Témoins intacts :
**31 comptes · 927 Ω**, aucun compte de test, et la porte de vérification répond bien **404**
en production.*

*Reste chez le portable, sans urgence : la passe RuboCop (avec les trois PR d'actions
GitHub), le saut majeur d'`image_processing` qui mérite sa propre livraison, et le chantier B
des Guides — l'historique multi-conversations — quand Boris le voudra.)*
