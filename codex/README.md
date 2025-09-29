# Codex: GitHub Pages CV

## Intent
Provide an example single-source CV website from Markdown (`cv.md`) and a BibTeX file (`publications.bib`), plus a sample workflow (`.github/workflows/build.yaml`) that is easily forked from the `main` branch. Publish a personalized version of the CV by rendering to `/index.html` via Pandoc on the `gh-pages` branch (site files live at the branch root). GitHub Pages serves the personalized CV from `gh-pages`.

## Success Criteria
- A `main` branch is maintained that others can fork. 
- The `main` branch contains a generic CV and publications, and a detailed README explaining how to fork the repo and personalize.
- The `gh-pages` branch mirrors any changes to the `main` branch, except for the `cv.md` and `publications.bib` files.
- A valid `/index.html` is generated on every push to `gh-pages` (or whenever the workflow re-renders the personalized CV).
- CV content comes from `cv.md` (Markdown) and publications from `publications.bib`.
- Citations render using the Chicago Author-Date style (`csl/chicago-author-date-date-desc.csl`).
- Custom HTML template (`templates/cv.html`) and CSS (`css/cv.css`) shape the rendered page.
- No external build steps required by the human beyond pushing commits.
- CV is easily printed via a print button.

## Scope / Non-Goals
- In: Markdown CV, BibTeX publications, README, automatic HTML build and branch syncing via GitHub Actions
- Out: Blog engine, theme frameworks, multi-page site, heavy templating.

## Interfaces (I/O)
- Inputs:
  - `cv.md` (Markdown with publication list fenced as `## Publications:\n::: {#refs}\n:::` on `gh-pages`)
  - `publications.bib` (BibTeX entries stored on `gh-pages`)
  - `csl/chicago-author-date-date-desc.csl` (installed by default)
  - `templates/cv.html` (Pandoc HTML template; optional variables like `site_url`)
  - `css/cv.css` (stylesheet published alongside the output)
  - `filters/refs-list.lua` (Pandoc Lua filter that turns the bibliography into a semantic list)
- Outputs:
  - `/index.html` (standalone HTML for GitHub Pages)
  - `/cv.css` (copied stylesheet referenced by `index.html`)
  - `/.nojekyll` (ensures GitHub Pages serves files without Jekyll processing)

## Constraints
- Keep build under ~2 minutes on GitHub-hosted runners.
- Avoid dependencies beyond stock `pandoc` (with built-in citeproc).
- Pages configured to serve from the `gh-pages` branch root. Ensure `/.nojekyll` exists on that branch.
- Workflows MUST preserve `gh-pages` copies of `cv.md` and `publications.bib` while syncing everything else from `main`.
- If the sync detects merge conflicts, fail the workflow and surface an actionable alert.

## Local Build (optional)
- Install Pandoc: `brew install pandoc` (macOS) or `apt-get install pandoc`.
- Run:  
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
    --lua-filter=filters/refs-list.lua \
    --output index.html
  cp css/cv.css ./cv.css
  touch .nojekyll

## Customizing the Template
- Edit `templates/cv.html` to adjust layout or add new metadata-powered sections (e.g., `$if(site_url)$`).
- Update `css/cv.css` for typography and spacing; the workflow copies it to `cv.css` on every build.
- Define additional metadata in the `cv.md` front matter (such as `site_url`) and reference it inside the template.
- Adjust `filters/refs-list.lua` if you need a different bibliography structure (e.g., ordered list instead of bullets).

## Maintaining `/README.md`
- Ensure that `/README.md` contains everything needed to fork and personalize the CV (branch strategy, workflow overview, customization knobs).
- Include instructions for local builds, customization, deployment, and how the `main → gh-pages` sync behaves.
- Document the `codex/` files so AI agents (or humans) understand the automation contract.
