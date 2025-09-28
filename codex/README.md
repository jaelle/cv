# Codex: GitHub Pages CV

## Intent
Publish a single-source CV website from Markdown (`cv.md`) and a BibTeX file (`publications.bib`), rendered to `docs/index.html` via Pandoc. GitHub Pages serves `/docs`.

## Success Criteria
- A valid `docs/index.html` is generated on every push to `main`.
- CV content comes from `cv.md` (Markdown) and publications from `publications.bib`.
- Citations render using the Chicago Author-Date style (`csl/chicago-author-date-date-desc.csl`).
- Custom HTML template (`templates/cv.html`) and CSS (`css/cv.css`) shape the rendered page.
- No external build steps required by the human beyond pushing commits.

## Scope / Non-Goals
- In: Markdown CV, BibTeX publications, automatic HTML build via GitHub Actions.
- Out: Blog engine, theme frameworks, multi-page site, heavy templating.

## Interfaces (I/O)
- Inputs:
  - `cv.md` (Markdown with citation keys like `[@doe2024coolpaper]`)
  - `publications.bib` (BibTeX entries)
  - `csl/chicago-author-date-date-desc.csl` (installed by default)
  - `templates/cv.html` (Pandoc HTML template; optional variables like `site_url`)
  - `css/cv.css` (stylesheet copied alongside the output)
- Outputs:
  - `docs/index.html` (standalone HTML for GitHub Pages)

## Constraints
- Keep build under ~2 minutes on GitHub-hosted runners.
- Avoid dependencies beyond stock `pandoc` (with built-in citeproc).
- Pages configured to serve from `/docs`. Ensure `docs/.nojekyll` exists.

## Local Build (optional)
- Install Pandoc: `brew install pandoc` (macOS) or `apt-get install pandoc`.
- Run:  
  ```bash
  pandoc cv.md \
    --from markdown \
    --to html5 \
    --standalone \
    --citeproc \
    --bibliography=publications.bib \
    --csl=csl/chicago-author-date-date-desc.csl \
    --template=templates/cv.html \
    --css=cv.css \
    --output docs/index.html
  cp css/cv.css docs/

## Customizing the Template
- Edit `templates/cv.html` to adjust layout or add new metadata-powered sections (e.g., `$if(site_url)$`).
- Update `css/cv.css` for typography and spacing; the workflow copies it to `docs/cv.css` on every build.
- Define additional metadata in the `cv.md` front matter (such as `site_url`) and reference it inside the template.
