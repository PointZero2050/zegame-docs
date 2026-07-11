# Ze.game — Documentation Design & UI

<!-- Mis à jour par Claude, 2026-06-14 -->

Ce document décrit le système de design actuel de l'application : tokens de couleur, typographie, composants, patterns de mise en page, et structure de chaque écran principal. Il est destiné aux agents IA (Claude, Codex) pour comprendre et faire évoluer le design de façon cohérente.

---

## 1. Tokens de design

### Couleurs

| Variable / SCSS | Valeur | Usage |
|---|---|---|
| `$primary` / `--primary` | `#82246f` | Violet/magenta foncé — couleur de marque principale |
| `$secondary` / `--secondary` | `rgba(207, 82, 121)` | Rose — CTAs, badges de validation |
| `--bg-body` | `#f4f5f6` | Fond de page |
| `--bg-box` | `white` | Fond des cartes/panneaux |
| Gradient principal | `radial-gradient(circle at 50% -70%, rgba(194,100,175,1) 0%, rgba(98,4,79,1) 70%)` | Headers de pages (`.bg-primary-gradient`) |
| Fond sombre admin/devise | `rgba(34, 19, 37)` | Bas de la sidebar admin, zone devise |

**Usage des couleurs :**
- `bg-primary` : sidebar admin, éléments d'accentuation
- `bg-primary-gradient` : header de toutes les pages de contenu
- `bg-secondary` (rose) : boutons d'action principaux, badges de statut
- `text-success` (Bootstrap vert) : état validé/complété
- `text-muted` : informations secondaires

### Breakpoints (Bootstrap 4 customisé)

| Nom | Valeur | Note |
|---|---|---|
| `xs` | 0 | Mobile |
| `md` | 768px | Tablette / Desktop small |
| `lg` | 992px | Desktop |

> `sm` et `xl` sont désactivés. Le design est bimodal : mobile vs desktop (md+).

### Icônes

Police **Fontello** (custom), classes `icon-*` :

| Icône | Classe | Usage |
|---|---|---|
| Chevron | `icon-right-open` | Navigation, lien vers détail |
| Validé | `icon-ok` | Défi complété (vert) |
| En attente | `icon-hourglass-2` | Soumis, pas encore validé |
| En cours | `icon-cog` | Défi commencé |
| Ajout | `icon-plus` | Inscription, rejoindre |
| Info | `icon-info-circled` | Popover d'info compétence |
| Admin | `icon-cogs` | Accès espace admin |
| Jeu | `icon-gamepad` | Accès espace joueur |
| Menu | `icon-menu` | Burger mobile |
| Fermer | `icon-times` | Fermer la sidebar |
| Messagerie | `icon-chat` | Accès carnet de connexion |
| Compétences | `icon-medal` | Skills |
| Édition | `icon-pencil` | Modifier |
| Déconnexion | `icon-logout` | Sign out |

---

## 2. Composants UI

### Carte de contenu (pattern de base)

```haml
.bg-box.rounded-md-xl.border.overflow-hidden
  .bg-primary-gradient.mb-md-4.p-3.p-md-4
    / Header avec gradient violet-magenta
  .px-md-4
    / Contenu de la carte
```

- Fond blanc (`bg-box`), bordure fine, coins arrondis sur desktop (`rounded-md-xl`)
- Header toujours en gradient violet
- Padding horizontal `px-md-4` sur le contenu (0 sur mobile)

### Boutons

| Classe | Apparence | Usage |
|---|---|---|
| `btn btn-secondary rounded-xl px-5` | Rose, pill | Action principale (CTA) |
| `btn btn-outline-light rounded-xl` | Contour blanc | Action secondaire sur fond sombre |
| `btn btn-sm rounded-xl px-3` | Petit pill | Action compacte en liste |

### Badges de compétences

```haml
.badge.border.px-0.small.skill-badge
  .px-3
    .d-flex.justify-content-center
      %span.text-truncate= skill.name
      %i.icon-info-circled.c-pointer  / popover au focus
    .small.opacity-7.mt-1
      = "#{skill.framework} - #{skill.derived_framework}"
```

Badges blancs avec bordure fine, texte tronqué, popover Bootstrap sur icône info. Grille : 33% / 50% / 100% selon viewport.

### Anneau de progression

```haml
.progress-border.rounded-circle{style: "--progress: #{prct}%"}
  = circle_image src: journey.photo, size: 90
```

CSS : `background: conic-gradient(var(--secondary) var(--progress), #ddd 0%)` + padding 4px.
Anneau rose autour de la photo circulaire, représente le % de complétion du journey.

### Titres séparateurs (Striked)

```haml
!= title "Nom de section", tag: :h3, classes: "striked"
```

Titre centré avec lignes horizontales de part et d'autre (pseudo-éléments `::before`/`::after`). Sépare les sections dans les pages de détail.

### Ruban décoratif (Ribbon)

```haml
.ribbon.d-block.text-center.text-white
  %h3.h4= page.name
```

Forme ruban `clip-path` avec fond `bg-primary`. Utilisé pour les titres de pages de contenu dans un journey.

### Blocs de statistiques LEVEL / DURATION / POINT

```haml
.d-flex
  .flex-even.bg-black.text-white.font-weight-bolder.d-flex-center= "LEVEL".t
  .flex-even.bg-white.text-body.d-flex-center= preview_stars(resource.difficulty)
```

Blocs en deux colonnes : label fond noir / valeur fond blanc. Juxtaposés horizontalement (empilés sur mobile).

### Filtres toggle (tag-checkboxes)

```haml
.tag-checkbox
  / input caché + label stylé en pill
  / input:checked → label { background-color: var(--secondary) }
```

Checkboxes cachées, labels en `border rounded-xl px-3`. Actif = fond rose. Soumission auto (`oninput`).

### Dropdown menu utilisateur

```haml
.dropdown
  %a.dropdown-toggle= [avatar 35px, circle-border 3px]
  .dropdown-menu.border-0.shadow
    = dropitem(path, icon, title, subtitle)
```

Chaque `dropitem` : icône Fontello + titre bold + sous-titre `.small`.

---

## 3. Layouts

### Application (zone utilisateur)

```
┌────────────────────────────────────────────────────────┐
│ #top-bar (border-bottom shadow-sm bg-box)              │
│  [logo ou icône admin]                  [avatar 35px ▼]│
├────────────────────────────────────────────────────────┤
│  p-0 p-lg-5  d-flex justify-content-center            │
│  ┌──────────────────────────────────────────────────┐  │
│  │  #inner-main  width: min(1200px, 100vw)         │  │
│  │  = yield                                        │  │
│  └──────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────┘
```

Top bar masquée sur Hotwire Native pour les formulaires new/edit.

### Admin (back-office)

```
┌──────────────────┬────────────────────────────────────────┐
│ SIDEBAR col-lg-2 │ MAIN col-lg-10  #admin-main (scroll)   │
│                  │                                        │
│ #alm--top        │ #top-bar                               │
│  bg-primary      │  [burger] [gamepad Player space]   [▼] │
│  logo            │                                        │
│  nom + email     │ .p-3.p-lg-5 #inner-main               │
│  [avatar 70px]   │  = yield                              │
│                  │                                        │
│ #alm--bottom     │                                        │
│  bg-dark         │                                        │
│  Communities     │                                        │
│  Journeys        │                                        │
│  Challenges      │                                        │
│  Users           │                                        │
│  Skills          │                                        │
│  To validated    │                                        │
└──────────────────┴────────────────────────────────────────┘
```

**Mobile admin** : sidebar en `position: fixed`, glisse depuis la gauche (transition 0.4s) déclenchée par `<input#menu-cb type=checkbox>`. Overlay sombre semi-transparent sur le contenu quand ouverte.

---

## 4. Écrans principaux

### Connexion (Devise)

- Layout `devise`, fond sombre `rgba(34,19,37)`
- Formulaire centré : email + mot de passe
- OAuth : Google + Microsoft
- Liens secondaires : inscription, mot de passe oublié, confirmation

### Home — Logbook (`/`)

```
.bg-box.rounded-md-xl.border#homepage
  ┌─ GRADIENT ─────────────────────────────────────┐
  │  [CONNECTION NOTEBOOK] (bouton rose centré)    │
  │  [Rejoindre un parcours] [Rejoindre une comm.] │
  └────────────────────────────────────────────────┘

  "LOGBOOK" (h2, centré)
  Toggle : [Mes parcours en cours] / [Tous mes parcours]

  Par communauté (titre striked) :
    Notifications de feedback (liens texte centrés)
    Grille (col-md-6) :
    ┌──────────────────────────────────┐
    │ [anneau %][photo 90px]           │
    │  Nom du parcours (h4)            │
    │  [badge compétence principale]   │
    │  XX%                      [>]   │
    └──────────────────────────────────┘
```

### Liste des Journeys (`/journeys`)

```
.bg-box.rounded-md-xl.border
  ┌─ GRADIENT ─────────────────────────────────────┐
  │  [Barre de recherche]                          │
  │  [Filtres tag-checkbox]                        │
  └────────────────────────────────────────────────┘

  Par communauté (titre striked) :
  Grille (col-md-6) :
  ┌───────────────────────────────────────────────┐
  │ [photo 90px]  Nom (h4)                        │
  │               Description                     │
  │               X challenges - Y pts            │
  │               [badge skill] [badge skill]     │
  │               #tag1 #tag2                     │
  │               [Deja inscrit]  [Voir →]        │
  └───────────────────────────────────────────────┘
```

### Détail d'un Journey (`/journeys/:id`)

```
.bg-box.rounded-md-xl.border
  ┌─ GRADIENT ─────────────────────────────────────┐
  │ [anneau %][photo 90px]  Nom (h2)               │
  │                         [badge Auto/Pedagogiq] │
  │                         Description (italic)   │
  │                         #tags                  │
  │  [CTA : Inscrire / Commencer / Restart]        │
  └────────────────────────────────────────────────┘

  ┌─ bg-primary (rounded) ─────────────────────────┐
  │  [POINT | valeur totale]                       │
  │  Top 3 competences (badges rankes 1. 2. 3.)    │
  └────────────────────────────────────────────────┘

  Liste des elements (pages + challenges) :
  - Page  → .ribbon (ruban violet pleine largeur)
  - Challenge → carte horizontale :
    [photo 50px] Nom + infos + X pts + etat [>]
    Etats : ok vert | hourglass | cog
```

### Détail d'un Challenge (`/journeys/:id/challenges/:id`)

```
.bg-box.rounded-md-xl.border#challenge-page
  ┌─ GRADIENT (position:relative) ─────────────────┐
  │ [photo 130px]  Nom (h2)                        │ ← mobile : full-bleed
  │                [badge Auto/Pedagogiq]          │   gradient overlay
  │                #tags                           │
  │  ┌──────────┬──────────┬──────────┐           │
  │  │  LEVEL   │ DURATION │  POINT   │           │
  │  │  etoiles │  2h      │  30 pts  │           │
  │  └──────────┴──────────┴──────────┘           │
  │  [CTA selon etat]                             │
  └────────────────────────────────────────────────┘

  #cp--content (.px-3.px-md-5)
    Skills ——————
    [Grille badges competences]

    Description ——————
    [Contenu riche TinyMCE]

    Validation ——————
    ok Critere 1
    ok Critere 2

    Ressources ——————
    [icone] Titre / X min / Description / →
```

**États du CTA :**

| État | Affichage |
|---|---|
| Pas commence + inscrit | `[TAKE ON THIS CHALLENGE]` (rose) |
| Auto-valide + complete | ok Completed + `[Restart]` |
| Pedagog. + soumis | hourglass Pending review |
| Pedagog. + valide | ok Completed + `[Restart]` + `[FEEDBACKS]` |

### Messagerie — Thread

```
.bg-box.p-md-4.rounded-xl
  [<- Retour]
  [Titre du challenge/journey (centre)]
  [Messages]
  [Formulaire nouveau message]
```

### Profil utilisateur (`/users/me`)

```
.bg-box.border.rounded-xl
  [photo 100px]  Nom complet (h1)
                 Email
                 [badge communaute] x N
                 [badge DFF] [badge Admin]
                 [crayon Editer]
```

### Stats utilisateur (`/users/me/stats`)

```
.bg-box.border.rounded-xl
  "LOGBOOK" (centre)

  Par journey (titre striked) :
  Grille (col-6 col-md-4 col-lg-2) :
    [photo challenge 100px]
    Nom du challenge
    Date - X pts
    Competences (texte)
```

---

## 5. Patterns de navigation

| Pattern | Implementation |
|---|---|
| Retour arriere | Helper `back_to "texte", path` — lien en haut de page |
| Breadcrumb | Absent — navigation lineaire par `back_to` |
| Turbo Frames | `#list-journeys` sur la home (toggle ongoing/all) |
| Pagination | `pagy` — liens numerotes Bootstrap |
| Hotwire Native | Top bar masquee sur formulaires new/edit |
| Dropdown | Seul point d'acces : profil, messagerie, deconnexion |

---

## 6. Responsive — comportements mobiles

| Element | Desktop | Mobile (< 768px) |
|---|---|---|
| Grille journeys/challenges | col-md-6 | Pleine largeur |
| Challenge header | Photo + infos en ligne | Image full-bleed, titre absolu, overlay gradient |
| Blocs LEVEL/DURATION/POINT | Cote a cote | Empiles verticalement |
| Sidebar admin | Fixe col-lg-2 | Slide depuis gauche |
| Badges competences | 3 par ligne (33%) | 2 par ligne (50%), puis 1 (<500px) |
| Inner-main padding | `p-lg-5` | `p-0` |
| Photos `responsive-image` | 90-130px | 40px |
| Titres h2 | Variable | Force a 22px |

---

## 7. Bibliothèques front-end

| Lib | Version | Usage |
|---|---|---|
| Bootstrap | 4.6 | Grid, composants (partiellement importe) |
| Fontello | custom | Police d'icones (`icon-*`) |
| TinyMCE | 8 | Editeur WYSIWYG (challenges, pages) |
| Choices.js | latest | Select enrichi (tags, filtres) |
| Chart.js | 4 | Graphiques stats (code present, commente en prod) |
| Turbo | 2.0.23 | Navigation SPA, Turbo Frames, Turbo Streams |
| Stimulus | 3 | Controleurs JS legers |

**Bootstrap 4 modules desactives** (non importes) : cards, carousel, jumbotron, progress, media, list-group, spinners, print.

---

## 8. Points d'attention pour les évolutions design

- **Mode sombre** : aucun support actuellement
- **Tokens CSS partiels** : seules les couleurs primaires/secondaires et bg sont en variables CSS
- **Bootstrap 4.6 en fin de vie** : migration vers BS5 impacterait le grid et les utilitaires
- **Chart.js present mais non utilise** : code commente dans les vues stats — pret a activer
- **Icones exclusivement Fontello** : pas de SVG inline, pas de FontAwesome ni Heroicons
- **TinyMCE** : charge conditionnellement (`.tinymce-wrapper .tox-tinymce { display: none }` par defaut)
- **Photos** : via CarrierWave, helper `circle_image`, versions `:thumb` et `:medium`
