# Codex: GitHub Pages CV

## Intent
Publish a single-source CV website from Markdown (`cv.md`) and a BibTeX file (`publications.bib`), rendered to `docs/index.html` via Pandoc. GitHub Pages serves `/docs`.

## Success Criteria
- A valid `docs/index.html` is generated on every push to `main`.
- CV content comes from `cv.md` (Markdown) and publications from `publications.bib`.
- Citations render using a CSL style (default: `csl/ieee.csl`).
- No external build steps required by the human beyond pushing commits.

## Scope / Non-Goals
- In: Markdown CV, BibTeX publications, automatic HTML build via GitHub Actions.
- Out: Blog engine, theme frameworks, multi-page site, heavy templating.

## Interfaces (I/O)
- Inputs:
  - `cv.md` (Markdown with citation keys like `[@doe2024coolpaper]`)
  - `publications.bib` (BibTeX entries)
  - `csl/<style>.csl` (optional; defaults to `ieee.csl` if present)
- Outputs:
  - `docs/index.html` (standalone HTML for GitHub Pages)

## Constraints
- Keep build under ~2 minutes on GitHub-hosted runners.
- Avoid dependencies beyond `pandoc` and `pypandoc` (and `citeproc` built-in).
- Pages configured to serve from `/docs`. Ensure `docs/.nojekyll` exists.

## Local Build (optional)
- Install Pandoc: `brew install pandoc` (macOS) or `apt-get install pandoc`.
- Run:  
  ```bash
  pandoc cv.md \
    --from markdown \
    --to html5 \
    --standalone \
    --metadata title="Your Name – CV" \
    --citeproc \
    --bibliography=publications.bib \
    --csl=csl/ieee.csl \
    --output docs/index.html
