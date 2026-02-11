# System Patterns: GitHub Pages CV Starter

## Architecture Overview

The system follows a **two-branch architecture** with clear separation of concerns:

```
main branch (template)
│
├── templates/          # HTML templates for rendering
├── css/                # CSS stylesheets
├── csl/                # Citation style files
├── .github/workflows/  # GitHub Actions workflows
└── README.md           # Documentation

gh-pages branch (published)
│
├── cv.md               # Personalized CV content (protected)
├── publications.bib    # Personalized citations (protected)
├── index.html          # Rendered output (auto-generated)
├── cv.css              # CSS copy (auto-generated)
└── .nojekyll           # GitHub Pages configuration
```

## Key Design Patterns

### 1. Two-Branch Model Pattern
- **Purpose**: Separate template code from personalized content
- **Implementation**:
  - `main` branch contains reusable templates and tooling
  - `gh-pages` branch contains personalized content and rendered output
  - Automated sync preserves personalized files during updates

### 2. Protected Files Pattern
- **Purpose**: Prevent accidental overwrites of user data
- **Implementation**:
  - `cv.md` and `publications.bib` are marked as protected
  - Workflow skips these files during merge operations
  - Users maintain full control over these files

### 3. Automated Rendering Pattern
- **Purpose**: Ensure consistent output across all deployments
- **Implementation**:
  - GitHub Actions workflow triggers on push events
  - Pandoc converts Markdown to HTML with templates
  - CSS and CSL files are copied to output directory
  - All operations are deterministic and reproducible

### 4. Conflict Resolution Pattern
- **Purpose**: Handle merge conflicts gracefully
- **Implementation**:
  - Workflow detects conflicts before merging
  - Fails with clear error messages
  - Provides manual resolution path
  - Resumes after conflict is resolved

## Component Relationships

### Workflow Orchestration
```
Git Push → GitHub Actions → Merge (with exclusions) → Render → Deploy
```

### Rendering Pipeline
```
cv.md + publications.bib + template.html + cv.css + csl → Pandoc → index.html
```

### File Protection Mechanism
```
Merge Operation
├── Include: All files except cv.md and publications.bib
└── Exclude: cv.md and publications.bib (preserved from gh-pages)
```

## Critical Implementation Paths

### 1. Template Update Path
1. User modifies template on `main` branch
2. Push triggers workflow
3. Workflow merges changes to `gh-pages`
4. Workflow renders new `index.html`
5. Changes deployed to GitHub Pages

### 2. Content Update Path
1. User modifies `cv.md` or `publications.bib` on `gh-pages`
2. Push triggers workflow
3. Workflow re-renders `index.html` with updated content
4. Changes deployed to GitHub Pages

### 3. Conflict Resolution Path
1. Workflow detects merge conflict
2. Workflow fails with error
3. User manually resolves conflict on `gh-pages`
4. User pushes resolved changes
5. Workflow resumes and completes render

## Data Flow

### Input Data
- `cv.md`: Markdown content with YAML front matter
- `publications.bib`: BibTeX citation database
- `templates/cv.html`: HTML template with Pandoc variables
- `css/cv.css`: CSS stylesheet
- `csl/chicago-author-date-date-desc.csl`: Citation style

### Processing
- Pandoc parses Markdown and front matter
- Pandoc processes citations using BibTeX and CSL
- Pandoc applies template with variable substitution
- Pandoc outputs standalone HTML

### Output Data
- `index.html`: Rendered CV in HTML format
- `cv.css`: CSS file in branch root
- `.nojekyll`: GitHub Pages configuration file

## Error Handling

### Merge Conflicts
- Detected during merge operation
- Workflow fails with descriptive error
- User notified via GitHub Actions UI

### Rendering Errors
- Detected during Pandoc execution
- Workflow fails with error details
- User can debug locally using provided command

### Missing Files
- Detected during workflow execution
- Workflow fails with file not found error
- User can verify file existence on branch

## Maintenance Patterns

### Template Updates
- Update files on `main` branch
- Test changes locally before pushing
- Monitor workflow execution
- Verify rendered output

### Style Updates
- Modify `css/cv.css`
- Test locally with Pandoc
- Push to `main` for propagation
- Verify on GitHub Pages

### Citation Style Updates
- Replace or modify CSL file
- Test with sample BibTeX entries
- Push to `main` for propagation
- Verify citation formatting