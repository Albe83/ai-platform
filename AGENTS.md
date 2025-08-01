# Guidelines for AI Agents

This document provides guidance for AI agents working in this repository.

## Development workflow
- Do not modify `AGENTS.md` unless explicitly requested.
- Use `rg` for searching; avoid commands like `grep -R` or `ls -R`.
- After modifying files, run all available tests with `pytest`. If other test suites are introduced, run them as well.
- Keep commits focused and descriptive, using the present tense (e.g., "Add feature" rather than "Added feature").

## Code style
- Maintain consistent formatting with any tools configured in the repository. If formatting tools (such as `black` or `pre-commit`) are available, run them before committing.
## Documentation
- Use English for all documentation, comments, and notes.
- Update documentation or comments when behavior changes or new features are introduced.
- Prefer Markdown as the format for documentation artifacts.
- Create diagrams as code using Mermaid embedded in Markdown files.
- Validate Mermaid diagrams with `mmdc` (Mermaid CLI) to ensure syntax is correct and diagrams render successfully.
  - Install Mermaid CLI if it is not already available:
    ```bash
    npm install -g @mermaid-js/mermaid-cli
    ```
  - Render a diagram to check for syntax errors:
    ```bash
    mmdc -i diagram.mmd -o /tmp/diagram.svg
    ```
    The command fails when the diagram contains invalid syntax.
- Use the C4 model for architecture diagrams.
- Use sequence diagrams for component interactions.

