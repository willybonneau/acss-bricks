---
name: acss-bricks
description: Utiliser Automatic.css 4 (ACSS 4.x) par défaut pour tout travail WordPress + Bricks Builder (pages, sections, templates, composants, classes, custom CSS). Charger avant toute écriture de style Bricks. Ne jamais appliquer de syntaxe ACSS 3.x.
---

# ACSS 4 par défaut sur WordPress + Bricks

> Auteur : Willy Bonneau · Licence MIT · https://github.com/willybonneau/acss-bricks

ACSS est la source de vérité du design : réglages, variables, classes, recipes.
Ne jamais créer de design system parallèle. **ACSS 4 uniquement** : beaucoup de
noms 3.x n'existent plus (voir §6).

Sources : https://docs.automaticcss.com (v4) + l'état réel du site. Le site fait
foi : une option désactivée dans le dashboard ne génère pas sa classe ou sa
variable.

## 1. Lire le site AVANT d'écrire
- MCP : `bricks-get-design-context` (summary). ACSS synchronise dans Bricks une
  catégorie de variables « Automatic.css » (`acss_import_*`), une palette
  « ACSS Colors » et des classes globales en catégorie `acss`. Suivre
  `bricks:bricks-start-here` et `bricks:bricks-design-systems`.
- Toutes les variables ne sont pas synchronisées dans Bricks (ex.
  `--grid-gap`, `--content-gap`, `--container-gap`, `--h1…--h6`). La liste
  complète est dans le CSS généré `/wp-content/uploads/automatic-css/automatic.css`
  (lecture seule).
- WP-CLI si shell : `wp acss status --format=json`,
  `wp acss settings list --search=<motif>`, `wp acss settings get <clé>`.

## 2. Réglages
- **Tous les paramètres ACSS peuvent être modifiés, SAUF les points de rupture
  (breakpoints).** Ne jamais changer les breakpoints ACSS (réglages
  `breakpoint-*` / largeurs de breakpoints), ni les breakpoints Bricks qui en
  découlent (pas de `bricks/*breakpoint*` en écriture). Lecture seule.
- Couleurs, typo, espacements, largeurs, boutons, rayons, ombres, etc. : à régler
  dans le dashboard ACSS ou avec `wp acss settings set <clé> <valeur>`, puis
  `wp acss css regenerate`. Jamais en dur dans Bricks. Avant un `set`, vérifier
  que la clé n'est pas un breakpoint (`wp acss settings list --search=breakpoint`).
- Avant `import`/`reset` : `wp acss settings export --file=<backup>.json`
  (écrasement total, sans backup auto). Demander confirmation avant tout
  changement global.

## 3. Variables ACSS 4
- **Couleurs** (6 rôles) : `--primary`, `--secondary`, `--tertiary`, `--accent`,
  `--base`, `--neutral`, plus `--success`, `--danger`, `--warning`, `--info`,
  `--black`, `--white`.
  Nuances : `--{c}-ultra-dark`, `-dark`, `-semi-dark`, `-semi-light`, `-light`,
  `-ultra-light`, `-hover`.
  Pas de tokens de transparence en 4.x : utiliser
  `color-mix(in oklch, var(--primary) 50%, transparent)` ou la syntaxe relative
  `oklch(from var(--primary) l c h / 0.5)` (recipe `?primary-clr`).
- **Assignations contextuelles** (prioritaires sur les couleurs brutes) :
  `--bg-ultra-light`, `--bg-light`, `--bg-dark`, `--bg-ultra-dark`,
  `--body-bg-color`, `--text-dark`, `--text-dark-muted`, `--text-light`,
  `--text-light-muted`, `--heading-color`, `--text-color`, `--link-color`,
  `--link-color-hover`, `--focus-color`.
- **Typo** : `--h1…--h6`, `--text-xs…--text-xxl`, ponts fluides
  `--h2-to-h4`, `--text-l-to-m`, `--heading-line-height`, `--text-line-height`,
  `--heading-font-weight`. Les variables `--heading-font-family`,
  `--text-font-family` et `--h1-font-weight` n'existent que si elles sont
  réglées dans le dashboard.
- **Espacement** : `--space-xs…xxl`, `--section-space-xs…xxl`, ponts
  `--space-xl-to-m`, `--section-space-xl-to-s`, `--gutter`,
  `--section-padding-block`.
  Contextuel : `--container-gap`, `--content-gap`, `--grid-gap`.
  Smart spacing : `--paragraph-spacing`, `--heading-spacing`, `--list-spacing`,
  `--flow-spacing`, `--figure-spacing`, `--blockquote-spacing`, etc.
- **Layout** : `--content-width`, `--content-width-safe`, `--width-10…90`,
  `--width-full`, `--grid-1…12`, `--grid-1-2`, `--grid-1-3`, `--grid-2-1`,
  `--grid-2-3`, `--grid-3-1`, `--grid-3-2`, `--grid-auto-2…12`,
  `--header-height`, `--admin-bar-height`, `--scroll-margin`, `--offset`.
- **Effets** : `--radius`, `--radius-m`, `--radius-50`, `--radius-circle`,
  `--radius-none`, `--box-shadow-1…3`, `--drop-shadow-1…3`,
  `--text-shadow-1…3`, `--border`, `--border-light`, `--border-dark`,
  `--border-size`, `--divider*`, `--transition`, `--transition-duration`,
  `--ease-smooth`, `-snappy`, `-gentle`, `-bouncy`, `-elastic`.
- **Boutons et icônes** : `--btn-*` (padding-block, padding-inline, background,
  background-hover, text-color, border-*, radius…), `--icon-*`.
- **Variantes** : `calc(var(--grid-gap) * 1.25)` ou un pont `-to-`. Ne jamais
  inventer de taille.

## 4. Classes ACSS 4 (jeu volontairement réduit)
Seules celles-ci existent (synchronisées en classes globales Bricks `acss`) :
- Sections et header : `.section--{xs…xxl}`, `.section--{l}-to-{s}`,
  `.section--none`, `.header--{xs…xxl}`, `.sticky`
- Largeur : `.width--{10…90}`, `.width--full`, `.width--auto`,
  `.width--min-content`, `.width--max-content`, `.width--fit-content`,
  `.content-width`, `.content-width--safe`
- Content grid : `.content-grid`, `.content-grid--off`, `.content--feature`,
  `.content--feature-max`, `.content--full`, `.content--full-safe`
- Texte : `.text--{xs…xxl}`, `.text--dark`, `.text--dark-muted`,
  `.text--light`, `.text--light-muted`, `.h1…h6`
- Fonds : `.bg--ultra-light`, `.bg--light`, `.bg--dark`, `.bg--ultra-dark`.
  Ils règlent automatiquement le texte, les titres, les liens et les boutons :
  les préférer aux couleurs posées à la main.
- Thème : `.scheme--light`, `.scheme--dark`
- Boutons : `.btn--primary`, `.btn--primary-light`, `.btn--primary-dark`,
  `.btn--secondary`, `.btn--secondary-light`, `.btn--secondary-dark`,
  `.btn--outline`, `.btn--none`, `.btn--{xs…xxl}`
- Icônes : `.icon-list`, `.icon--boxed`, `.icon--plain`, `.icon--{xs…2xl}`
- Spacing : `.smart-spacing` (sur le parent direct), `.smart-spacing--off`,
  `.smart-spacing-normalize`
- Divers : `.overlay`, `.is-bg`, `.blockquote`, `.skip-link`,
  `.hidden-accessible`, `.unrelate`, `.on-enter--stagger`,
  `.on-exit--stagger`, `.on-visible--stagger`

Tout le reste se fait en **classe custom BEM** dans Bricks
(`.service-grid`, `.card__title`, `.card--featured`), stylée avec les variables :
```css
.service-grid {
  display: grid;
  grid-template-columns: var(--grid-3);
  gap: var(--grid-gap);
}
```
Pour le responsive, changer seulement la valeur aux breakpoints Bricks
(ex. `var(--grid-2)` en tablette). Réutiliser les classes existantes
(`bricks:bricks-naming-conventions`). Ne pas dupliquer, renommer ou surcharger
une classe ACSS.

## 5. Recipes (Custom CSS Bricks, syntaxe 4.x `?`, plus `@`)
- `?nom;` (Entrée dans un champ d'une ligne). `%root%` = l'élément.
- Déclaration courte, dans la règle : `%root% { ?center-all; }`, `?flex-row;`,
  `?grid-3;`
- Bloc avec son propre sélecteur, sur une ligne à part : `?auto-grid;`,
  `?flex-grid;`, `?variable-grid;`, `?columns;`, `?list-none;`,
  `?fade-top;`, `?fade-all;`, `?skip-link;`, `?is-bg;`, `?tooltip;`,
  `?footer-reveal;`, `?border-check;`, `?corner-ribbon;`,
  `?concentric-radius;`, `?concentric-radius-reverse;`, `?font-face;`
- Boutons custom : `?btn` sur une classe dédiée (ex. `.btn--custom`)
- Valeur : `background: ?linear-gradient;`, `?color-mix`, `?transparency`
- Pseudo : `?:hover,:focus-visible;`, `?::before,::after;`,
  `?hover-exclude-touch;`
- Couleur dans un champ : `?{couleur}-clr` →
  `oklch(from var(--primary) l c h / 1)`
- **Via MCP, la recipe n'est pas expansée** : écrire directement le CSS final
  qu'elle produirait, avec les variables ACSS.

## 6. Interdits (syntaxe ACSS 3.x ou hors framework)
- Modifier les points de rupture ACSS ou Bricks (voir §2).
- Classes 3.x supprimées : `.grid--3`, `.grid--auto-3`, `.grid--l-2`,
  `.padding--m`, `.margin-top--l`, `.gap--s`, `.flex--row`, `.owl--m`,
  `.pad--`, `.bg--primary`, `.text--primary`, `.text--700`, `.text--center`
  (sauf si le CSS du site les contient).
- Variables 3.x : `--action`, `--{c}-trans-*`, `--{c}-medium`,
  `--shadow-m`, `--font-primary`.
- Recipes `@nom` (3.x), à remplacer par `?nom`.
- Hex/rgb, px/rem en dur, media queries custom alors qu'une variable ou un
  breakpoint Bricks convient. Styles inline quand une classe convient.
  Variables ou palettes Bricks qui doublonnent ACSS.

## 7. Après écriture
- `wp acss css regenerate` si un réglage ACSS a changé, `wp acss doctor` en
  cas d'anomalie.
- `bricks:bricks-quality-gate`, puis `bricks:bricks-browser-verify`
  (responsive et contexte clair/sombre).
