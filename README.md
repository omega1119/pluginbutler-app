# PluginButler

Website for [pluginbutler.app](https://pluginbutler.app)

PluginButler is a native macOS app for discovering, inspecting, organising and safely
uninstalling audio plug-ins. The app itself lives in a separate repository; this repo is
the marketing site. It is a Coming Soon page today.

## Structure

```
pluginbutler-app/
├── CNAME                    # Domain configuration
├── README.md
├── _config.yml              # GitHub Pages metadata
├── favicon.svg
├── index.html               # Redirect shell (language detection) into en/
├── privacy.html             # Redirect shell into en/privacy.html
├── assets/
│   ├── css/styles.css       # Shared stylesheet (light and dark theme)
│   ├── fonts/               # Self-hosted Inter
│   ├── images/              # App icon exports
│   └── js/
│       ├── main.js          # Nav, footer, theme toggle, hreflang, JSON-LD
│       └── redirect.js      # Language redirect logic
└── en/                      # English locale
    ├── index.html           # Landing page
    └── privacy.html         # Privacy policy
```

## Local Development

No build step. From the repository root:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080/en/`. Hard refresh if assets look stale: CSS and JS are
referenced with a `?v=N` query string.

## Checks

```bash
python3 .github/scripts/check-site.py .
```

The same check runs on every pull request (`.github/workflows/site-check.yml`).

## Deployment

The site is deployed via GitHub Pages from the root of the `main` branch. A push to
`main` publishes live, so open a pull request for changes.
