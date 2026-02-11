# Product Context: GitHub Pages CV Starter

## Why This Project Exists

This project solves the common problem of maintaining an up-to-date, professional CV/resume that is:
- **Easy to update**: Markdown-based editing with version control
- **Professionally formatted**: Consistent styling and layout
- **Web-hosted**: Accessible from anywhere
- **Print-ready**: Works both online and as a PDF
- **Citation-aware**: Supports academic publications with BibTeX

## Problems Solved

1. **Version Control**: Traditional CVs are static documents that get outdated. This system uses Git for version control, allowing users to track changes over time.

2. **Separation of Concerns**: The two-branch model separates template code (main) from personalized content (gh-pages), preventing accidental overwrites of personal data.

3. **Automation**: Manual rendering is error-prone and time-consuming. The GitHub Actions workflow automates the conversion from Markdown to HTML, ensuring consistent output.

4. **Citation Management**: Academic CVs require proper citation formatting. The system integrates BibTeX and CSL styles to handle citations automatically.

5. **Conflict Resolution**: When template updates conflict with personalized content, the system provides clear error messages and manual resolution paths.

## How It Should Work

### User Journey

1. **Initial Setup**
   - User forks the repository
   - Creates a `gh-pages` branch
   - Personalizes `cv.md` and `publications.bib`
   - Configures GitHub Pages to serve from `gh-pages` branch

2. **Ongoing Maintenance**
   - User updates `cv.md` and `publications.bib` on `gh-pages` branch
   - Changes automatically render to `index.html`
   - User can test locally before pushing

3. **Template Updates**
   - User updates template files on `main` branch
   - GitHub Actions syncs changes to `gh-pages`
   - Personalized files are preserved during sync

4. **Conflict Handling**
   - If conflicts arise, workflow fails with clear error
   - User manually resolves conflicts on `gh-pages`
   - Workflow resumes after conflict resolution

## User Experience Goals

- **Simplicity**: Users should be able to update their CV without understanding the underlying technology
- **Reliability**: The system should handle edge cases gracefully
- **Flexibility**: Users can customize templates, styles, and citation formats
- **Transparency**: Clear documentation and error messages
- **Portability**: Easy to fork, clone, and deploy

## Key Interactions

1. **Content Editing**: Users edit `cv.md` in Markdown format
2. **Citation Management**: Users add/remove entries in `publications.bib`
3. **Template Customization**: Users modify `templates/cv.html` for layout changes
4. **Styling**: Users edit `css/cv.css` for visual customization
5. **Workflow Interaction**: Users trigger workflows via Git pushes or manual dispatch

## Success Metrics

- Number of active forks using the template
- Frequency of template updates from maintainers
- User-reported issues and bug reports
- Adoption of the two-branch model
- Success rate of automated workflows