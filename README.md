# GitHub Pages CV Starter

A forkable template for publishing a résumé/CV with Markdown, BibTeX, and Pandoc. The repository keeps a generic example on `main` while GitHub Pages serves your personalized CV from the `gh-pages` branch root (`index.html`, `cv.css`).

## Branch Strategy
- **`main`** – holds the generic example plus reusable tooling (`templates/`, `css/`, `csl/`, workflows). Forks should update files here before syncing downstream.
- **`gh-pages`** – hosts the rendered site. Every push to `main` triggers a workflow that syncs all changes into `gh-pages`, except for `cv.md` and `publications.bib`. Those two files stay personalized on `gh-pages` and are never overwritten by automation.

## Workflow Overview
Workflow file: `.github/workflows/build.yaml`

1. **On `main` pushes**
   - Checkout both branches using a worktree.
   - Merge latest `main` files into `gh-pages`, skipping conflicts in `cv.md` and `publications.bib`.
   - If any other file conflicts, the workflow fails with an actionable error (requires manual resolution).
   - Render `cv.md` (from `gh-pages`) to `index.html` using Pandoc with the custom template, CSS, and CSL resources.
   - Copy `css/cv.css` to the branch root as `cv.css`, ensure `.nojekyll` exists, commit, and push to `gh-pages`.
2. **On `gh-pages` pushes**
   - Re-run the render step so direct edits to `cv.md`/`publications.bib` publish immediately.
3. **Manual trigger** – `workflow_dispatch` lets you re-run the sync/publish at any time.

## How to Personalize
1. Fork this repository.
2. On your fork, switch to `gh-pages` and edit:
   - `cv.md` (front matter + Markdown content; ensure publications block includes `::: {#refs}`).
   - `publications.bib` (add/update BibTeX entries).
3. Commit and push to `gh-pages`. The workflow renders fresh `index.html` and `cv.css` in the branch root. GitHub Pages should be configured to serve the `gh-pages` branch.
4. Update shared resources on `main` when you want to adjust styling or behavior (template, CSS, workflows, CSL, instructions). Push to `main` to propagate changes to `gh-pages` automatically.

## Local Build (Optional)
```bash
pandoc cv.md \
  --from markdown+fenced_divs \
  --to html5 \
  --standalone \
  --citeproc \
  --bibliography=publications.bib \
  --csl=csl/chicago-author-date-date-desc.csl \
  --template=templates/cv.html \
  --css=cv.css \
  --output index.html
cp css/cv.css ./cv.css
touch .nojekyll
```
Preview `index.html` locally before pushing.

## Customization Knobs
- **Template (`templates/cv.html`)** – Adjust layout, add metadata-powered sections, change header/footer structure.
- **Stylesheet (`css/cv.css`)** – Control typography, spacing, colors, print behavior (includes `[Print]` button styling).
- **Metadata** – Extend front matter in `cv.md` (e.g., `site_url`, custom section toggles) and reference via `$if(...)$` blocks in the template.
- **CSL (`csl/chicago-author-date-date-desc.csl`)** – Modify citation style.

## Sync Conflict Resolution
If the workflow fails with `Merge conflict syncing main→gh-pages`:
1. Checkout the `gh-pages` branch locally.
2. Merge `main` manually.
3. Resolve conflicts, commit, and push back to `gh-pages`.
4. Re-run the workflow (or push to `main`) to resume automated publishing.

## GitHub Pages Configuration
- Repository settings → **Pages** → Source: `Deploy from a branch`
- Branch: `gh-pages`
- Folder: `/` (root)
- Ensure `.nojekyll` stays in the branch root (workflow handles this).

## codex Directory
The `codex/` folder documents automation contracts for AI assistants and human maintainers:
- `codex/README.md` – canonical instructions for the project (inputs/outputs, constraints, maintenance).
- `codex/AGENTS.md` – role descriptions (Planner, Builder, Reviewer, Publisher) that articulate responsibilities under the `main ↔ gh-pages` model.

Keep these files in sync with any process changes so automated tooling stays aligned.

## Troubleshooting
- **Workflow failing on merge** – Resolve conflicts on `gh-pages`, re-run.
- **Output not updating** – Verify the workflow succeeded and GitHub Pages is pointed at `gh-pages` root.
- **Broken citations** – Confirm entries exist in `publications.bib`, run `pandoc` locally for verbose errors, inspect CSL style.
- **Styling issues** – Check `cv.css` is present alongside `index.html` and paths match the template link.

Happy publishing!
