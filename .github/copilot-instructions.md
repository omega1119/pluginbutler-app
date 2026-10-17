<!-- BEGIN GENERATED (web-common/agents/copilot-instructions.md -- edits here are overwritten by tools/sync-agent-config.sh) -->

# Agent instructions

This is a static site: hand-written HTML, CSS, and vanilla JS, deployed to GitHub
Pages from the `main` branch. There is no build step, no npm, no bundler, and no
framework (React, Vue, a static site generator's templating, etc.). Edit the HTML
files directly: do not introduce a build pipeline to "improve" this.

## Never change these without explicit approval

These are load-bearing. Changing them silently breaks live URLs, analytics history,
or JS that reads them by exact string:

- **URL slugs and file paths** (e.g. `en/products/metric.html`). Renaming or moving
  a page breaks bookmarks, search rankings, and inbound links from the App Store or
  other sites.
- **Anchor IDs** (`id="..."` targeted by in-page links or external deep links).
- **The Google Analytics measurement ID** (`G-XXXXXXXXXX` in the `gtag.js` snippet).
  Changing it silently orphans historical analytics data.
- **`data-*` attribute contracts** read by `assets/js/main.js` and
  `assets/js/redirect.js`, e.g. `data-languages`, `data-active-lang`,
  `data-footer-type`, `data-store` / `data-store-product`, `data-redirect-<lang>`,
  `data-theme` on `<source>` elements. These scripts parse specific attribute names
  and values; renaming or restructuring one without updating the JS (and every HTML
  file that uses it) breaks the feature with no error.

## General conventions

- No external `<script src>` beyond Google's `gtag.js`: do not add other
  third-party scripts without asking first.
- Fonts are self-hosted (`assets/fonts/*.woff2` + `@font-face` in `styles.css`), not
  loaded from Google Fonts or any other external stylesheet host. Every repo used to
  load its body font (usually Inter) from `fonts.googleapis.com`; all were migrated
  to self-hosted `@font-face` declarations in Sep 2026. Don't reintroduce an external
  font `<link>`: add a new self-hosted woff2 instead.
- When adding a page, copy an existing locale's page as the template rather than
  writing one from scratch, to keep markup structure consistent across locales.

<!-- END GENERATED -->

<!-- Per-repo notes go below this line. Never touched by the sync script. -->

## pluginbutler-app specifics

- Domain `pluginbutler.app`. Publisher Greenwood IT Consultancy Ltd. One product:
  PluginButler, a native macOS app for discovering, inspecting and safely uninstalling
  audio plug-ins. The app source is a separate repo (`PluginButler`); its `README.md`
  is the source of truth for feature claims. Do not invent features.
- Not launched: `en/index.html` is a Coming Soon page. There is no download button,
  no price and no App Store badge. The app has the App Sandbox disabled, so it is
  not intended for the Mac App Store: do not add a Mac App Store badge. `STORE_URLS`
  in `main.js` is deliberately empty.
- No analytics. No Google Analytics tag is wired into any page and the pages do not
  carry `data-cookie-consent`, so no cookie banner shows. The privacy policy says
  there is no analytics. If analytics is added, add a dedicated measurement ID (never
  reuse another site's), add `data-cookie-consent`, and update the privacy policy in
  the same PR.
- English only (`en`). Root `index.html` and `privacy.html` are redirect shells
  (`assets/js/redirect.js`, `data-redirect-en`). `HREFLANG_LANGS` in `main.js` is
  `['en']` and `SUPPORTED_LANGS` in `redirect.js` is empty. No terms page.
- Scaffolded from `plugscope-app`: `styles.css` is byte-identical to the one there and
  in `harmonic-tools`. The screenshot modal, device bezel and store-badge code in
  `main.js` and the CSS is carried over but unused until screenshots and a download
  link exist. Re-add a `#screenshots` nav item in `initNavItems()` when a screenshots
  section is added.
- App icon exports in `assets/images/` are 512x512 downscales of the app repo's
  1024px icons (`docs/icons/macOSAppIcon Exports/`). The favicon is a placeholder
  letter tile in the accent green.
- Cache-busting: CSS and JS are referenced with a `?v=N` query string. Bump it when
  you change `styles.css` or `main.js`.
