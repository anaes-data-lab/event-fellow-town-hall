# RCH Anaesthesia Fellowship Town Hall

Static site for the inaugural Royal Children's Hospital (Melbourne) Anaesthesia
Fellowship Town Hall — an online information evening for prospective paediatric
anaesthesia fellows.

- **Event:** Monday 25 May 2026, 19:30 – 20:30 AEST, online via Zoom
- **Live site:** https://events.rch-anaesthesia.org/

## Stack

- [Hugo](https://gohugo.io/) (extended) — static site generator
- Plain CSS via Hugo's asset pipeline (no theme; layouts live in `layouts/`)
- GitHub Actions → GitHub Pages (custom domain via `static/CNAME`)

## Local development

Requires Hugo extended (≥ 0.147). On macOS: `brew install hugo`.

```sh
hugo server -D     # live-reload server at http://localhost:1313
hugo               # one-off production build into ./public
```

## Editing content

- **Event details, registration link** — `hugo.toml` (`[params]`). Replace
  `registerUrl` with the Microsoft Forms URL when ready.
- **Landing page copy** — `layouts/index.html` (markup) plus the front matter in
  `content/_index.md` (page title / meta description).
- **FAQ page** — `content/faq.md`. Currently placeholders; expand questions as
  Nicole's collated FAQs come through.
- **Panel list** — `layouts/index.html`, the `#panel` section. Update names,
  remove `panel-card--tbc` / `panel-card__tbc` markers as people are confirmed.
- **Styles** — `assets/css/main.css`. Brand variables are at the top of the file
  under `:root` (RCH navy, teal, red).

## Deployment

Pushes to `main` build and deploy via `.github/workflows/deploy.yml`. To enable:

1. Create the GitHub repository and push this directory:
   ```sh
   git remote add origin git@github.com:<org>/<repo>.git
   git add . && git commit -m "Initial site"
   git push -u origin main
   ```
2. In the repo on GitHub: **Settings → Pages → Build and deployment → Source:
   GitHub Actions**.
3. Wait for the first workflow run to publish the site.

## Custom domain (`events.rch-anaesthesia.org`)

The `static/CNAME` file is published with each build, so GitHub Pages will pick
up the custom domain automatically. You also need a DNS record at the
`rch-anaesthesia.org` zone:

```
events   CNAME   <github-username>.github.io.
```

(Replace `<github-username>` with the user/org that owns the repo. For an
organisation, use `<org>.github.io.`.)

After DNS propagates, enable **Enforce HTTPS** in the repo's Pages settings.

## TODO before launch

- [ ] Add real Microsoft Forms registration URL to `hugo.toml` (`registerUrl`).
- [ ] Confirm full names and titles for Lizzie B and Nicole W in
      `layouts/index.html`.
- [ ] Confirm fourth panellist (Katherine Davies / Victoria S / other) and
      replace the TBC card.
- [ ] Replace placeholder FAQ answers in `content/faq.md` with the collated
      answers.
- [ ] Confirm whether the meeting agenda should be shown publicly or kept
      internal (currently shown).
