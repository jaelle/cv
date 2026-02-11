# Tech Context: GitHub Pages CV Starter

## Technologies Used

### Core Tools
- **Pandoc**: Universal document converter that transforms Markdown to HTML with templates
- **GitHub Actions**: CI/CD platform for automating workflows
- **GitHub Pages**: Static site hosting service
- **Markdown**: Lightweight markup language for content authoring
- **BibTeX**: Reference management system for academic citations
- **CSL (Citation Style Language)**: Standard for citation formatting

### Development Environment
- **Version Control**: Git with GitHub as the remote repository
- **Branch Strategy**: Two-branch model (main + gh-pages)
- **Local Development**: Standard command-line tools (bash, pandoc)
- **Text Editor**: Any Markdown-compatible editor

## Development Setup

### Prerequisites
- Git installed and configured
- Pandoc installed (for local testing)
- GitHub account with repository access
- Basic familiarity with Markdown syntax

### Local Build Command
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

## Technical Constraints

### GitHub Actions Limitations
- Workflow execution time limits (6 hours max)
- Storage limits for workflow artifacts
- Merge conflict detection requires manual resolution

### Pandoc Limitations
- Complex Markdown features may require specific extensions
- Citation processing requires proper BibTeX formatting
- Template variables must follow Pandoc syntax

### GitHub Pages Constraints
- Only serves from specific branches (gh-pages in this case)
- Requires `.nojekyll` file for non-Jekyll sites
- File size limits for static assets

## Dependencies

### Required Files
- `cv.md`: Main content file with YAML front matter
- `publications.bib`: BibTeX database for citations
- `templates/cv.html`: HTML template for rendering
- `css/cv.css`: Stylesheet for visual presentation
- `csl/chicago-author-date-date-desc.csl`: Citation style file

### Optional Files
- `.github/workflows/build.yaml`: GitHub Actions workflow
- `README.md`: Project documentation
- `.nojekyll`: GitHub Pages configuration

## Tool Usage Patterns

### Git Workflow
- `git checkout main`: Work on template updates
- `git checkout gh-pages`: Work on personalized content
- `git merge main`: Sync template changes to gh-pages
- `git push`: Trigger workflow execution

### Pandoc Usage
- Local testing before pushing changes
- Template variable substitution
- Citation processing with BibTeX and CSL
- CSS integration for styling

### GitHub Actions Usage
- Automated sync between branches
- Conditional execution based on branch
- Error handling and conflict detection
- Manual workflow dispatch for testing

## File Structure Conventions

### Branch-Specific Files
- **main branch**: Contains templates, CSS, CSL, and workflows
- **gh-pages branch**: Contains personalized content and rendered output

### Protected Files
- `cv.md`: Never overwritten by automation
- `publications.bib`: Never overwritten by automation

### Auto-Generated Files
- `index.html`: Generated from cv.md and template
- `cv.css`: Copied from css/cv.css
- `.nojekyll`: Created by workflow

## Error Handling Patterns

### Common Issues
- Merge conflicts between branches
- Missing or malformed BibTeX entries
- Invalid Markdown syntax
- Template variable errors
- CSS path issues

### Debugging Strategies
- Test locally with Pandoc before pushing
- Check workflow logs for error details
- Verify file permissions and paths
- Validate BibTeX formatting
- Inspect rendered HTML for issues

## Performance Considerations

### Rendering Performance
- Pandoc execution time depends on document size
- Large BibTeX files may slow down citation processing
- Complex templates increase rendering time

### GitHub Pages Performance
- Static site hosting is fast and scalable
- No server-side processing required
- CDN-backed for global distribution

## Security Considerations

### GitHub Pages Security
- Static sites have minimal attack surface
- No server-side code execution
- Content is publicly accessible by design

### GitHub Actions Security
- Workflow files should be reviewed for security
- No sensitive data should be stored in workflows
- Use GitHub's built-in security features

## Maintenance Patterns

### Template Updates
- Update on `main` branch first
- Test locally before pushing
- Monitor workflow execution
- Verify on GitHub Pages

### Content Updates
- Edit directly on `gh-pages` branch
- Test locally if needed
- Push to trigger rendering
- Verify changes on live site

### Workflow Updates
- Modify `.github/workflows/build.yaml`
- Test with manual dispatch
- Verify all scenarios work
- Document changes in README