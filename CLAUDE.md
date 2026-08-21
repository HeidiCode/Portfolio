# Portfolio — project guide

Heidi's personal portfolio site. Plain HTML + CSS + images, **no build tools and
no framework**. See `README.md` for the human-facing update/deploy walkthrough;
this file is the working brief.

- **Repo:** https://github.com/HeidiCode/Portfolio (public)
- **Hosting:** Azure Static Web Apps

## Layout

| File / folder | What it is |
|---|---|
| `index.html` | Home page |
| `about_me.html` | About page |
| `case_study_*.html` | One file per case study |
| `case_template.html` | Blank starting point for a **new** case study |
| `styles.css` | All styling lives here (shared across every page) |
| `images/` | Photos, screenshots, SVG icons |
| `.github/workflows/azure-static-web-apps.yml` | Auto-deploy config — normally don't touch |
| `DoNotPush/` | Local working files — **gitignored, never commit** (see below) |
| `.claude/launch.json` | Local preview server config — **gitignored**, not part of the site |

## Conventions

- **New case study:** copy `case_template.html`, don't build one from scratch.
  A case study is **two edits**: the new `case_study_*.html` page, plus a summary
  card added to `index.html` (challenge → role → image → results → highlight → link).
- **Page structure** (follow `case_study_TransparentLiving.html`): `col-md-4` holds
  `.caption` + `<h2>` + `p.hashs`; `col-md-8` holds the intro, `<h4>` Team and
  My contribution, then `<h3 class="highlight pt-5">` per section. First paragraph
  after a section heading gets `class="tp"`. Images are wrapped in a link to the
  full-size file on `heidimanninen.net`, followed by `div.image-caption`.
- **Tags** (`p.hashs`): 2–3 per case study, PascalCase — more than that stacks
  too tall in the narrow left column.
- **Styling:** add to `styles.css`; pages share it. No per-page CSS files.
- **Screenshots stay PNG.** They're flat UI with text, which PNG compresses better —
  converting them to JPEG made three of five *larger* and blurred the type.
  JPEG is for photos, 3D renders and infographics.
- **Portrait images:** add `img-portrait` alongside `img-fluid` to cap them at 500px.
  Without it a tall screenshot renders ~950px high and swamps the page.
- **No build step** — edit HTML/CSS directly; what's in the repo is what ships.

## Deploy

GitHub Actions deploys to Azure on **every push to `main`** (workflow uses
`app_location: "/"`, `skip_app_build: true` — it just uploads the files as-is;
usually live within ~1 min). The deploy token is **not** in the code — it's the
GitHub Actions secret `AZURE_STATIC_WEB_APPS_API_TOKEN`. Never paste tokens,
passwords, or private info into files (the repo is public).

Check a deploy: GitHub → **Actions** tab (green ✓), or `gh run list`.

## `DoNotPush/` — local-only working files

Drafts and explorations that must **not** go into the public repo (case-study
drafts, design mockups, source of the separate Mökin vedet app). It's in
`.gitignore`; keep it that way. Don't commit its contents or reference private
details from it in tracked files.

## Related project

The **Mökin vedet** app is a separate repo (`HeidiCode/Mokin-vedet`, hosted on
GitHub Pages), intended to be linked from a case-study page here later. Its
pre-refactor source is archived at `DoNotPush/mokin_vedet.html`.

## Working notes / gotchas

- **Commit identity** for this repo is set locally to the personal name/email
  (`Heidi Manninen` / `heidi.manninen@proton.me`), separate from any work git
  identity — plain `git commit` uses the right one.
- This repo lives in **iCloud Drive**. Renaming/moving a synced folder can
  briefly revoke the terminal's file access ("Operation not permitted") until
  iCloud settles or the terminal app is restarted — not data loss.
- When find/replacing non-ASCII text (e.g. `ö`), use Python, not a `perl`
  one-liner — perl mangled `ö` into `Ã¶`. Verify with `grep -c "Ã"`
  (this file itself contains one deliberate instance, in the line above).
- **`styles.css` is linked *before* Bootstrap** on every page, so Bootstrap wins any
  equal-specificity tie: a plain `.my-class { max-width: … }` loses to `.img-fluid`'s
  `max-width: 100%`. Give custom rules extra specificity — `main img.img-portrait` —
  rather than reaching for `!important`.
- **`h3.highlight::before` sits at a fixed `top: 4rem`,** so the pale blue band does
  not adapt to heading height. A section heading that wraps to two lines gets the band
  cut straight through its second line. Keep section headings to roughly **32
  characters** so they stay on one line down to 375px. (Fixing it properly would mean
  `top: calc(100% - 18px); height: 73px`, which changes shared CSS and so affects
  every existing page.)
- **Previewing locally:** `.claude/launch.json` runs `python3 -m http.server 4310`.
  Opening pages as `file://` silently drops the stylesheet and images. When iterating
  on `styles.css` the browser caches it — force a refetch by setting the `<link>` href
  to `styles.css?v=<timestamp>`, or the change appears not to work.
