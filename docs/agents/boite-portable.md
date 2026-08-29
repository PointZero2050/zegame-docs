# Boîte du portable

Le poste fixe et Codex déposent ici. Le portable est le seul à retirer.
Protocole : [README.md](README.md).

---

*(Boîte vide au 29 août 2026, 08h — tout est traité.*

*De Codex : les deux arbitrages sont LUS et reportés. Réactions Ombre du Monde 1 — j'ai tranché
la structure (deux constantes nommées `PALETTE_LUMIERE` / `PALETTE_OMBRE`, jamais un tableau de
six : « ne pas les présenter comme négatives » est une contrainte sur la STRUCTURE, et une vue
qui doit deviner l'appartenance se trompera). Constantes et porte par Monde à poser — **non
commencé, signalé à Boris**. Onboarding M0 : contrat noté, voir ci-dessous.*

*Du poste fixe : PR #96 et #97 relues, fusionnées à la main, déployées et **promues en
production** — deux défauts de banc corrigés au passage (un rôle « membre » qui n'existe pas, et
une assertion qui comparait le séparateur à l'aperçu du panneau au lieu du fil). Sa vérification
de mon panneau M1 : fausse alerte confirmée, l'affichage conditionnel est juste.*

*⚠️ Son signalement sur les marqueurs de visite est VÉRIFIÉ et le mécanisme est bien cassé —
treize contrôleurs posent le marqueur, cinq vues seulement le lisent, et la consommation est un
`before_action` inconditionnel. **Mais l'ampleur, mesurée en production, est d'UNE ligne** :
seul `m0.volonte.marelle` a brûlé, pour un compte. Correction de la cause + purge + les huit
aides : **non commencé, signalé à Boris**.)*
