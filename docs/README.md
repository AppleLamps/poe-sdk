# Documentation (`docs/`)

This folder contains the source files for the project documentation site.

The documentation is built with **MkDocs** using the configuration in the repository root at `mkdocs.yml`.

## Structure

- `index.md`
  - The documentation homepage.
- `getting-started/`
  - Installation, authentication, and core concepts.
- `guides/`
  - Task-oriented guides (chat completions, tool calling, models, usage).
- `reference/`
  - API reference pages (client, chat, models, usage, errors).
- `advanced/`
  - Advanced topics (rate limits, OpenAI compatibility).

## Local preview

From the repository root:

```bash
pip install mkdocs
mkdocs serve
```

Then open the local site (MkDocs prints the URL; by default it is `http://127.0.0.1:8000/`).

## Editing guidelines

- Keep new pages inside `docs/` and add them to the navigation in `mkdocs.yml`.
- Use fenced code blocks with a language tag (e.g. `python`, `bash`, `powershell`) for consistent rendering.
