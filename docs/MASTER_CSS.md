# Stash Master CSS

`resources/css/style.css` is the single source of truth for Stash's look. It is
plain CSS (custom properties + cascade layers) with **no Tailwind or build
dependency**, so you can drop it into any other website.

- Live reference: open [`docs/styleguide/index.html`](styleguide/index.html) in a
  browser (it links the CSS file directly).
- Design source: the "Stash / Foundations & Controls" and "Content & Feedback"
  reference sheets.

## Use it on another site

```html
<!-- 1. Font (any of these) -->
<link rel="stylesheet" href="/fonts/plus-jakarta-sans.css" />
<!-- self-hosted woff2 -->
<!-- or: npm i @fontsource-variable/plus-jakarta-sans && import '@fontsource-variable/plus-jakarta-sans' -->

<!-- 2. The master CSS -->
<link rel="stylesheet" href="/css/style.css" />

<body class="nb-body">
    <button class="nb-btn nb-btn--primary">+ Save</button>
</body>
```

With a bundler: `@import 'style.css';`. With Tailwind 4, declare the layer order
first so utilities can still refine components:

```css
@layer theme, base, nb-base, components, nb-components, utilities;
@import 'tailwindcss';
@import './style.css';
```

Everything is namespaced with `nb-` so it will not collide with existing CSS.
Base element styles only apply inside `.nb-body` (nothing global is reset).

## Tokens (CSS custom properties on `:root`)

| Group    | Tokens                                                                                                                                                                |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Palette  | `--nb-ivory #FFF8EF`, `--nb-white`, `--nb-ink #191A1D`, `--nb-orange #FF7417`, `--nb-yellow #FFD83D`, `--nb-muted #62656D`                                            |
| Derived  | `--nb-orange-hover`, `--nb-orange-text #C2410C` (text on light, AA), `--nb-yellow-soft`, `--nb-focus #E35D00`, `--nb-line-soft`, `--nb-surface-hover`, disabled tones |
| Semantic | `--nb-success/-soft/-line`, `--nb-info…`, `--nb-warning…`, `--nb-danger…`                                                                                             |
| Aliases  | `--nb-canvas`, `--nb-surface`, `--nb-text`, `--nb-text-muted`, `--nb-line`, `--nb-sidebar`                                                                            |
| Type     | `--nb-font-sans`, `--nb-text-heading 32`, `--nb-text-section 24`, `--nb-text-card 20`, `--nb-text-body 16`, `--nb-text-label 14`, `--nb-text-meta 12`                 |
| Shape    | `--nb-border 2px`, `--nb-radius 12px` (controls), `--nb-radius-card 20px`, `--nb-shadow 4px 4px 0 ink`, `--nb-shadow-hover 8px 8px` (+ `--nb-lift` -4px,-4px: box moves up-left, shadow stays put), `--nb-shadow-press 1px 1px`      |
| Space    | `--nb-space-1…7` = 4, 8, 12, 16, 24, 32, 48 px                                                                                                                        |
| Size     | `--nb-touch 44px`, `--nb-control-h 44px`, `--nb-sidebar-w`, `--nb-detail-w`                                                                                           |

Re-theme by overriding tokens, e.g. `:root { --nb-orange: #ff5f1f; --nb-orange-text: #b53c0c; }`
(re-check contrast when you change text/fill pairs).

## Components

| Block                                                 | Modifiers / elements                                                                                                                            | Reference    |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| `.nb-btn`                                             | `--primary --secondary --selected --danger --danger-solid --ghost --on-dark --sm --lg --icon --block`, `[disabled]`, `[aria-busy=true]` spinner | 01·05        |
| `.nb-link`                                            | `--plain`                                                                                                                                       | 01·06        |
| `.nb-field`                                           | `__label __hint __error`                                                                                                                        | 01·08        |
| `.nb-input` `.nb-textarea` `.nb-select`               | `[aria-invalid=true]`, `:disabled`, `.nb-input--sm`                                                                                             | 01·08        |
| `.nb-search`                                          | `__icon __clear`                                                                                                                                | 01·08        |
| `.nb-check` + `.nb-checkbox` `.nb-radio` `.nb-switch` | native inputs, `:checked`, `:indeterminate`                                                                                                     | 01·09        |
| `.nb-segmented`                                       | `__item[aria-pressed                                                                                                                            | aria-checked | aria-selected=true]` | 01·09 |
| `.nb-tag`                                             | `--orange --white --soft --selected`, `__remove`; `a/button.nb-tag` are interactive; `.nb-tags` wrapper                                         | 01·07        |
| `.nb-badge`                                           | `--unread --read --archived --trash --warning --type --outline`                                                                                 | 01·07        |
| `.nb-chip`                                            | `__label __remove` (active filters)                                                                                                             | —            |
| `.nb-panel`                                           | `--flat`, `__header __body`                                                                                                                     | —            |
| `.nb-card`                                            | `--interactive --selected --loading`, `__media __fallback __body __title __desc __host __meta __overlay(--tl/--tr) __select`                    | 02·01        |
| `.nb-skeleton`                                        | shimmer placeholder                                                                                                                             | 02·01        |
| `.nb-table-wrap` `.nb-table`                          | `tr[aria-selected=true]`                                                                                                                        | 02·02        |
| `.nb-pagination`                                      | `__page[aria-current=page]`                                                                                                                     | 02·02        |
| `.nb-alert`                                           | `--info --warning --error`, `__icon __content __title __body __action`                                                                          | 02·03        |
| `.nb-toast`                                           | `--info --warning --error`, `__icon __message __action __close`                                                                                 | 02·04        |
| `.nb-menu`                                            | `__item(--danger, [data-highlighted]) __label __separator`                                                                                      | 02·07        |
| `.nb-tooltip`                                         | —                                                                                                                                               | 02·07        |
| `.nb-overlay` `.nb-dialog`                            | `--sm --lg`, `__header __title __description __body __footer`                                                                                   | 02·05/09     |
| `.nb-sheet`                                           | `--right --left --bottom --full --dark`, `__header __body __footer`                                                                             | —            |
| `.nb-tabs` `.nb-tab`                                  | `--fill`, `[aria-selected=true]`                                                                                                                | 02·09        |
| `.nb-breadcrumb`                                      | `__sep`                                                                                                                                         | 02·09        |
| `.nb-dropzone`                                        | `--active --invalid`, `__title __hint`                                                                                                          | 02·09        |
| `.nb-progress`                                        | `__bar`                                                                                                                                         | 02·08        |
| `.nb-empty`                                           | `__icon __title __body`                                                                                                                         | 02·08        |
| `.nb-brand`                                           | `__mark __word __slogan`, `--sm`                                                                                                                | 01·02        |
| `.nb-sidebar` `.nb-nav`                               | `__item[aria-current=page] __label __count __dot __heading __separator`                                                                         | 01·02        |
| `.nb-nav-light__item`                                 | light nav states                                                                                                                                | 01·02        |
| `.nb-topbar` `.nb-bottomnav`                          | `__item[aria-current=page]`                                                                                                                     | 01·03        |
| Layout                                                | `.nb-toolbar .nb-section-title .nb-grid .nb-stack .nb-cluster`                                                                                  | —            |
| Content                                               | `.nb-markdown .nb-code .nb-kbd .nb-spinner .nb-icon-btn`                                                                                        | —            |
| Text                                                  | `.nb-h1 .nb-h2 .nb-h3 .nb-text .nb-label .nb-meta .nb-muted .nb-truncate .nb-clamp-2/3 .nb-break .nb-sr-only`                                   | 01·01        |

## Accessibility built in

- 44 px minimum targets for buttons, nav and inputs.
- Visible `:focus-visible` ring (`--nb-focus`, ≥ 3:1 on all surfaces).
- Status colours always paired with text/icons; alert/toast roles are up to the markup.
- `prefers-reduced-motion` removes lifts, presses and animations; `forced-colors`
  keeps borders visible.
- Inputs use 16 px text to prevent mobile zoom.
