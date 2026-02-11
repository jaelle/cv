# Active Context: GitHub Pages CV Starter

## Current Work Focus
- Initializing memory bank for the project
- Documenting project structure, patterns, and context
- Establishing foundation for future development and maintenance

## Recent Changes
- Created `.clinerules/memory_bank/` directory structure
- Documented project brief, product context, system patterns, and technical context
- Next: Create active context and progress tracking files

## Next Steps
1. Complete memory bank initialization with `activeContext.md` and `progress.md`
2. Document current project state and known issues
3. Establish baseline for tracking future changes

## Active Decisions and Considerations
- **Branch Strategy**: Maintaining two-branch model (main for templates, gh-pages for published content)
- **File Protection**: `cv.md` and `publications.bib` are protected from automation overwrites
- **Automation**: GitHub Actions workflow handles sync and rendering
- **Local Testing**: Pandoc command available for local build verification

## Important Patterns and Preferences
- **Template Customization**: Users can modify `templates/cv.html` for layout changes
- **Styling**: CSS customization through `css/cv.css`
- **Citations**: BibTeX with CSL styling for academic publications
- **Conflict Resolution**: Manual merge required when conflicts arise

## Learnings and Project Insights
- The two-branch model effectively separates template code from personalized content
- Automated workflow reduces manual rendering errors
- Protected files pattern prevents accidental data loss
- Clear documentation is essential for user adoption