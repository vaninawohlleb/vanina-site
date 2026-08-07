# vanina-tsoneva.com — static site

Plain HTML/CSS, no build step. Structure so far:

```
/
├── index.html        ← Home page (English)
├── style.css          ← Site-wide stylesheet (used by every page)
└── bg/
    └── index.html      ← Home page (Bulgarian)
```

As more pages get added (about, coaching, shibari cluster, book-me,
awaken-desire), they'll follow the same pattern:
`/about.html` + `/bg/about.html` (or `/about/index.html` + `/bg/about/index.html`
if you prefer clean URLs without `.html` — see note below).

## Deploying via GitHub + Cloudflare Pages

1. **Create a GitHub repo** (e.g. `vanina-site`) and push this folder to it:
   ```
   cd site
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/vanina-site.git
   git push -u origin main
   ```

2. **Connect it to Cloudflare Pages**:
   - Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git
   - Pick the repo
   - Build settings: **Framework preset: None**, **Build command: (leave empty)**,
     **Build output directory: `/`** (this is a static site — nothing to build)
   - Deploy

3. **Custom domain**: in the Pages project → Custom domains → add
   `vanina-tsoneva.com` and `www.vanina-tsoneva.com`, then update your DNS
   (if the domain isn't already on Cloudflare, it'll walk you through
   pointing nameservers or adding a CNAME).

4. From then on, every `git push` to `main` auto-deploys a new version.
   Cloudflare Pages also gives you preview URLs for other branches/PRs if
   you ever want to stage changes before going live.

## Clean URLs (optional)

Right now `/bg` needs `bg/index.html` to resolve automatically — Cloudflare
Pages does this by default (`/bg` → `/bg/index.html`), so no config needed.
If later you add pages like `/about`, just create `about/index.html`
(and `bg/about/index.html`) rather than `about.html`, and the URLs will
stay clean without a `.html` extension.

## Fonts

Pages currently load Playfair Display + Inter from Google Fonts via
`<link>` tags in each page's `<head>`. That's fine as-is; if you want zero
external requests later, the fonts can be self-hosted instead.
