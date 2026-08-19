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

## Conventions

- **New case study:** copy `case_template.html`, don't build one from scratch.
- **Styling:** add to `styles.css`; pages share it. No per-page CSS files.
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
  one-liner — perl mangled `ö` into `Ã¶`. Verify with `grep -c "Ã"`.
