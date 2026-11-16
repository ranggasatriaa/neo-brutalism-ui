# ranggasatria-ui

Single source of truth for the `st-*` master CSS. Edit `stash.css` here only;
every site consumes it as a dependency. Docs: `docs/MASTER_CSS.md`, live demo: `styleguide/index.html`.

## Use in a site
- **Bundler sites** (Vite/Tailwind): `npm i github:ranggasatriaa/ranggasatria-ui` then `@import 'ranggasatria-ui/stash.css';`
- **Plain HTML sites**: `<link rel="stylesheet" href="/vendor/stash.css">` (copy from `node_modules/ranggasatria-ui/stash.css`).
- **Local dev (live edits)**: `npm i ../ui` links the folder, so changes show instantly.

## Roll out an update
1. Edit `stash.css`, bump version in `package.json`, commit, tag, push.
2. In each site: `npm update ranggasatria-ui` and rebuild.
