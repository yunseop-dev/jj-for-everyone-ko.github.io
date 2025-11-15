# Repository Guidelines

## Project Structure & Module Organization
The project is an mdBook. `book.toml` defines titles, languages, extra CSS, and the `mdbook-admonish` preprocessor. All tutorial chapters, shell snippets, and embedded assets live in `src/`; Markdown files map one-to-one with the sidebar ordering given by `src/SUMMARY.md`, and supporting images or helper scripts (for example `src/reset.sh`) sit alongside the relevant chapter. Custom theming lives in `theme/` (Handlebars template, Catppuccin styles, fonts, and the custom `reset` icon). Tool pinning and task automation are captured in `mise.toml`, so run commands through `mise` whenever possible.

## Build, Test, and Development Commands
- `mise run serve` — starts `mdbook serve --port 3210` with live reload for local editing.
- `mdbook build --dest-dir docs` — produces the static site exactly as deployed to GitHub Pages (used by the deploy task).
- `mise run deploy` — rebuilds fresh content in a throwaway Jujutsu workspace and force-updates the `gh-pages` bookmark; only run when publishing.
- `mdbook test` — optional, but catches broken intra-book links and code fences that declare `rust`/`bash` test blocks.

## Coding Style & Naming Conventions
Write chapters in Markdown with concise, numbered headings that match the learning levels already present. Favor second-person, active voice instructions. Keep code blocks fenced with explicit languages (`bash`, `jj`, `text`) so mdBook renders syntax highlighting. Use `{{#note}}`/`{{#warning}}` directives from `mdbook-admonish`; include the custom `reset` block when referencing the `reset.sh` helper. File names remain kebab_case (for example `make_changes.md`) to mirror command topics, and images use lowercase snake_case endings.

## Testing Guidelines
Before pushing, ensure `mdbook build` completes without warnings and that chapters you touched still render via `mise run serve`. Use `mdbook test` when adding verified code listings so the harness runs shell snippets marked with `bash` and reports failures. When instructing readers to run commands, double-check them inside a clean jj repo, then update `src/reset.sh` if the reset flow needs adjustments.

## Commit & Pull Request Guidelines
Recent commits favor short, descriptive titles like “Update remote.md with 'revision' explanation.” Follow that style: keep the subject under ~60 characters, capitalize the first word, and mention the chapter being touched. Pull requests should explain the motivation, link to any issue the change satisfies, and include screenshots/gifs if the update impacts styling. Note any commands you executed (`mdbook build`, `mdbook test`) so reviewers can repeat them quickly.
