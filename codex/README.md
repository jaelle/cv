# Codex: GitHub Pages CV

## Intent
Provide an example single-source CV website from Markdown (`cv.md`) and a BibTeX file (`publications.bib`), and a sammple workflow (`.github/workflows/build.yaml`) that is easily forked from the main branch. Publish a personalized version of the CV, rendered to `/index.html` via Pandoc. Personalized CV is stored on the `gh-pages` branch in the `/` directory. GitHub Pages serves the personalized CV.

## Success Criteria
- A `main` branch is maintained that others can fork. 
- The `main` branch contains a generic CV and publications, and a detailed README explaining how to fork the repo and personalize.
- The `gh-pages` branch mirros any changes to the `main` branch, except for the `cv.md` and `publications.bib` files.
- A valid `/index.html` is generated on every push to `gh-pages`.
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
  - `cv.md` (Markdown with publication list as `## Publications:\n::: {#refs}\n:::`)
  - `publications.bib` (BibTeX entries)
  - `csl/chicago-author-date-date-desc.csl` (installed by default)
  - `templates/cv.html` (Pandoc HTML template; optional variables like `site_url`)
  - `css/cv.css` (stylesheet copied alongside the output)
- Outputs:
  - `/index.html` (standalone HTML for GitHub Pages)

## Constraints
- Keep build under ~2 minutes on GitHub-hosted runners.
- Avoid dependencies beyond stock `pandoc` (with built-in citeproc).
- Treat custom Lua filters as out of scope for this project.
- Pages configured to serve from a gh-pages branch in the `/` directory. Ensure `/.nojekyll` exists.

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
    --output index.html
  cp css/cv.css ./cv.css
  touch .nojekyll

## Customizing the Template
- Edit `templates/cv.html` to adjust layout or add new metadata-powered sections (e.g., `$if(site_url)$`).
- Update `css/cv.css` for typography and spacing; the workflow copies it to `docs/cv.css` on every build.
- Define additional metadata in the `cv.md` front matter (such as `site_url`) and reference it inside the template.

## Maintaining /README.md
- Ensure that `/README.md` contains all the information someone would need to fork and customize the CV.
- Include instructions for local builds, customization, and deployment.
- Add a section about the `codex/` files for the purpose of integrating with AI agents.