# KioskIQ Docs

Customer-facing product documentation for KioskIQ, published as a static site
on GitHub Pages.

## What is here

```
site/                      everything that gets published
  index.html               docs landing page
  assets/base.css          shared shell styles (landing page, future index pages)
  guides/till/index.html   Till Handbook
  .nojekyll                serve files verbatim, no Jekyll processing
.github/workflows/pages.yml  build and deploy on push to main
```

There is no build step and no dependencies. The site is plain HTML and CSS,
served exactly as it sits in `site/`.

Guide pages are deliberately **self-contained**: each one carries its own
styles and scripts inline so that a guide still works when it is saved to a
desktop, printed for a staff room wall, or emailed to a manager. Only the
landing page and future index pages use `assets/base.css`.

## Publishing

Pushing to `main` deploys automatically. To publish for the first time:

1. Create a **public** repository on GitHub named `kioskiq-docs`.
2. From this directory:

   ```bash
   git init -b main
   git add .
   git commit -m "Add KioskIQ docs site with Till Handbook"
   git remote add origin git@github.com:<org>/kioskiq-docs.git
   git push -u origin main
   ```

3. In the repository, go to **Settings > Pages** and set
   **Source** to **GitHub Actions**.
4. Re-run the **Publish Docs** workflow, or push again.

The site then lives at `https://<org>.github.io/kioskiq-docs/`.

### Custom domain

To serve it from `docs.kioskiq.com` instead:

1. Add a `CNAME` record at your DNS provider pointing `docs` to
   `<org>.github.io`.
2. Create `site/CNAME` containing the single line `docs.kioskiq.com`.
3. Set the custom domain under **Settings > Pages** and enable
   **Enforce HTTPS** once the certificate is issued.

## Editing a guide

Open the HTML file and edit it. Push to `main`. That is the whole loop.

Keep guides written for the person on shift, not for engineers: name things
the way they appear on screen, give one instruction per step, and say what to
do when something goes wrong rather than only what should happen.

## What must not go in this repo

This repository is **public**. Do not add:

- Anything describing a gap or weakness in a shipped control. Internal notes
  of that kind belong in the private monorepo, not here. The unredacted copy
  of the Till Handbook lives at `docs/till-handbook-internal.html` in the
  main repository.
- Real tenant names, API keys, terminal keys, PINs, or screenshots showing
  live customer data. The guides use `Your Restaurant` as a placeholder for
  exactly this reason.
