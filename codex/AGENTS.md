
---

## `/codex/AGENTS.md`

```markdown
# Agents

## Planner
- Mandate: Keep the CV site single-source and simple; ensure inputs/outputs remain stable while maintaining the `main → gh-pages` sync contract.
- Tools: none
- Inputs: /codex/README.md
- Outputs: Short task list for updates (e.g., "adjust sync workflow", "add new BibTeX entry; re-run build")
- Guardrails: No build complexity creep; avoid adding frameworks/themes; never break the branch isolation for `cv.md` and `publications.bib`.
- Escalates to: Builder

## Builder
- Mandate: Maintain the GitHub Action(s) that (1) sync `main` into `gh-pages` (excluding `cv.md`/`publications.bib`) and (2) render the personalized CV to the branch root (`index.html`, `cv.css`, `.nojekyll`).
- Tools: Git repo, GitHub Actions, Pandoc
- Inputs: Planner tasks, repo state on `main` and `gh-pages`
- Outputs: PRs modifying `.github/workflows/*.yml`, templates, filters, and other source files. Generated outputs are committed by CI on `gh-pages` only.
- Guardrails: Never overwrite `cv.md` or `publications.bib` when syncing from `main`; fail (and alert) if a merge conflict occurs; never commit generated HTML/CSS manually.
- Escalates to: Reviewer

## Reviewer
- Mandate: Verify rendered output and sync behaviour (e.g., `index.html`, `cv.css`, `.nojekyll` on `gh-pages`) and ensure citations resolve.
- Tools: Repo read, Action logs, HTML preview
- Inputs: PRs, CI artifacts, sync workflow logs
- Outputs: Review comments/approvals
- Guardrails: Block if `index.html` is missing/broken, citations unresolved, or the sync workflow replaces `cv.md`/`publications.bib`.
- Escalates to: Human

## Publisher (optional)
- Mandate: Confirm GitHub Pages is set to serve from the `gh-pages` branch root.
- Tools: GitHub Pages settings
- Inputs: Approved PRs and successful CI runs
- Outputs: Live site at GitHub Pages URL
- Guardrails: No custom domains without explicit approval; ensure `.nojekyll` remains present.
- Escalates to: Human
```
