# ranggasatria-ui

A **neo-brutalism UI template**: a single plain-CSS design system (`nb-*` classes and `--nb-*` tokens) with bold borders, hard offset shadows, flat high-contrast colors and chunky, playful components. No JavaScript, no build step required.

It is the single source of truth for the look of all ranggasatria sites. Edit `style.css` here only;
every site consumes it as a dependency. Docs: `docs/MASTER_CSS.md`, live demo: `styleguide/index.html`.

## Use in a site
- **Bundler sites** (Vite/Tailwind): `npm i github:ranggasatriaa/ranggasatria-ui` then `@import 'ranggasatria-ui/style.css';`
- **Plain HTML sites**: `<link rel="stylesheet" href="/vendor/style.css">` (copy from `node_modules/ranggasatria-ui/style.css`).
- **Local dev (live edits)**: `npm i ../ui` links the folder, so changes show instantly.

## Roll out an update
1. Edit `style.css`, bump version in `package.json`, commit, tag, push.
2. In each site: `npm update ranggasatria-ui` and rebuild.
