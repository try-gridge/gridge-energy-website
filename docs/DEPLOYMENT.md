# Deployment

The site is static: HTML, JS, images, JSON. No build, no server code, no environment variables.
Any static host works. Every option below serves the repository root.

## GitHub Pages

1. Push the repository to GitHub.
2. **Settings → Pages → Build and deployment**, source **Deploy from a branch**, branch `main`,
   folder `/ (root)`.
3. Save. The site publishes at `https://<org>.github.io/<repo>/` in a minute or two.

`.nojekyll` is already present, which stops Jekyll from stripping files. For a custom domain, add
a `CNAME` file at the root containing the bare domain, then point a DNS `CNAME` (or the four
Pages `A` records for an apex domain) at GitHub.

## Netlify

- **Build command:** leave empty
- **Publish directory:** `.`

Or drag the repository folder onto the Netlify dashboard for a one-off deploy.

## Vercel

Import the repository, framework preset **Other**, build command empty, output directory `.`.

## Cloudflare Pages

Framework preset **None**, build command empty, build output directory `/`.

## Any web server

Copy the repository contents into the document root. Two things to configure:

```nginx
# long cache for images, short for the HTML so copy changes go live immediately
location ~* \.(png|jpe?g|svg)$ { expires 30d; add_header Cache-Control "public"; }
location = /index.html      { expires 5m;  add_header Cache-Control "public"; }
```

## Pre-flight checks

- Serve over HTTPS. The page loads fonts from Google Fonts over HTTPS; mixed content will block them.
- Confirm `data/siddique_series.json` and `data/alarms.json` return 200 — if they 404 the live
  sections fall back to empty values.
- Open the deployed URL on a real phone and page through all nine sections.

## Single-file alternative

If you need to hand the site to someone without a server — email, USB, an offline demo — export the
self-contained build (every image and script inlined into one ~17 MB HTML file). It opens by
double-click, no HTTP needed. Ask the design tool for the standalone export rather than committing
that file here; it bloats the repository history.
