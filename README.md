# Portfolio

My personal portfolio website — plain HTML, CSS, and images (no build tools, no frameworks).

- **Repo:** `HeidiCode/Portfolio` on GitHub (public)
- **Hosting:** Azure Static Web Apps
- **Live updates:** automatic — every push to `main` redeploys the site (see below)

> **This repo is public**, so anyone can read the code and commit history. That's fine — the
> deployment token is *not* in the code. It lives only in GitHub's encrypted **Secrets**
> (`AZURE_STATIC_WEB_APPS_API_TOKEN`), which are never exposed in a public repo, so the site stays
> secure. Just don't paste real tokens, passwords, or private info into the files themselves.

## Files

| File / folder | What it is |
| --- | --- |
| `index.html` | Home page |
| `about_me.html` | About page |
| `case_study_*.html` | Individual case study pages |
| `case_template.html` | Blank template for a new case study |
| `styles.css` | All styling |
| `images/` | Photos, screenshots, and SVG icons |
| `.github/workflows/` | The auto-deploy setup (don't need to touch this) |

## How to update the live site

The whole flow is: **edit → save → 3 commands → it's live.** After editing files, run these in the
terminal from inside this folder:

```bash
git add -A
git commit -m "Describe what I changed"
git push
```

That's it. Pushing to GitHub automatically triggers Azure to redeploy — usually live within about a
minute. **No more `swa deploy` command needed.**

- `git add -A` = "include all my changes"
- `git commit -m "..."` = "save a labelled snapshot" (write a short note so future-me remembers what changed)
- `git push` = "send it to GitHub" → this kicks off the automatic deploy

## Checking that a deploy worked

- On GitHub: open the repo → **Actions** tab. A green ✓ means the deploy succeeded.
- Or in the terminal: `gh run list` (shows recent deploys and their status).

## Good to know

- **Commit identity** for this repo is set locally to my personal name/email — separate from my work
  git identity, which is untouched.
- **The deployment token** lives safely in GitHub as a repository secret named
  `AZURE_STATIC_WEB_APPS_API_TOKEN` (under Settings → Secrets and variables → Actions). The auto-deploy
  uses it automatically. Keep it secret — it's like a password for the site.
- **Manual deploy (fallback only):** the old way still works if ever needed —
  `swa deploy --deployment-token=<token> --env=production ./nettisivut`
- **Undo / history:** because everything is in git, I can always look back at or restore an earlier
  version. Nothing is ever truly lost once it's committed.
