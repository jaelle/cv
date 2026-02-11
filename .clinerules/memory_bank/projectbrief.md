# Project Brief: GitHub Pages CV Starter

## Core Requirements
- A forkable template for publishing a résumé/CV with Markdown, BibTeX, and Pandoc
- Maintains a generic example on `main` branch
- Publishes personalized CV from `gh-pages` branch root
- Automated workflow syncs changes from `main` to `gh-pages`
- Preserves personalized files (`cv.md` and `publications.bib`) on `gh-pages`
- Local build capability for testing before deployment

## Key Features
- **Branch Strategy**: Two-branch model (`main` for templates, `gh-pages` for published content)
- **Automated Workflow**: GitHub Actions automates sync and rendering
- **Customization**: Template-based rendering with Pandoc
- **Citation Support**: BibTeX with CSL styling
- **Print-Ready**: CSS with print-specific styling
- **Conflict Resolution**: Manual merge capability for conflicts

## Technical Stack
- **Markdown**: Content authoring
- **Pandoc**: Document conversion
- **BibTeX**: Citation management
- **CSL**: Citation styling
- **GitHub Actions**: Automation
- **GitHub Pages**: Hosting

## Target Audience
- Academics and professionals needing to publish CVs/resumes
- Users who want version-controlled, easily updatable CVs
- Technical users comfortable with Git and Markdown

## Project Goals
1. Maintain a clean separation between template code and personalized content
2. Ensure automated workflows handle most updates seamlessly
3. Provide clear documentation for customization
4. Support both automated and manual build processes
5. Handle merge conflicts gracefully when they occur