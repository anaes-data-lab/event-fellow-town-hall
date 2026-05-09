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

All editable text and structured content lives outside the layout templates.
You should not normally need to touch any HTML to update copy.

| What you want to edit | Where |
|---|---|
| Event date / time / location / registration URL | `hugo.toml` → `[params]` |
| Hero, About, Program, Panel, CTA section copy | `content/_index.md` (front matter — TOML between the `+++` fences) |
| Agenda items (running order on the night) | `data/agenda.toml` — add/remove/reorder `[[items]]` blocks |
| Panel members | `data/panel.toml` — add/remove/reorder `[[members]]` blocks |
| FAQ questions and answers | `content/faq.md` (markdown body) |
| Page title, meta description, OG tags | `content/_index.md` (top of front matter) |
| Site-wide colours, type, spacing | `assets/css/main.css` (brand vars under `:root`) |

The front-matter strings in `content/_index.md` accept Markdown — use `**bold**`
for emphasis, blank lines between paragraphs for `aboutBody` etc.

**Panel card flags**

- `nameTbc = true` — adds an "— full name TBC" suffix next to the name
- `tbc = true` — applies the greyed-out placeholder treatment for an unfilled slot

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

- [ ] Confirm fourth panellist (Katherine Davies / Victoria S / other) — edit
      `data/panel.toml` and remove the `tbc = true` flag on the placeholder.
- [ ] Replace placeholder FAQ answers in `content/faq.md` with the collated
      answers.
- [ ] Confirm whether the meeting agenda should be shown publicly or kept
      internal (currently shown).
