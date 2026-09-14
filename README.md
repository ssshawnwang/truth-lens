# TruthLens

Help people explore different perspectives on topics they care about, understand the sources behind them, and form their own informed judgments.

Team 2 · 95-874 Agile Methods · CMU · Fall 2026

## What's here

| Path | What it is |
|---|---|
| `app/` | The living prototype. Always the latest sprint's work. Open `app/index.html` in a browser. |
| `releases/` | Frozen copies of each release, never edited after tagging. |
| `docs/` | Class artifacts: feature decomposition, feature board, sprint notes. |

## Releases

| Release | Tag | Scope | Open |
|---|---|---|---|
| Version 1, Core Exploration | `v1.0` | Search a topic, read viewpoint summaries with citations, browse the sources behind each, see uncertainty notices | `releases/v1/index.html` |

Version 2 (Deeper Analysis and Personal Use) is next. The feature board in `docs/` lists its stories.

## Running it

No build step and no dependencies. Double-click any `index.html`, or use the live site: <https://ssshawnwang.github.io/truth-lens/>. The root of the site opens the current prototype in `app/`; frozen releases are at `/releases/v1/` and so on.

## Sample data

Every topic, viewpoint, summary, and source in the current prototype is sample data written for the prototype. Publishers are fictional and links go to a placeholder page. Nothing calls a model or fetches live sources yet. See "What is mocked" in `app/README.md`.

## Working agreement

- One branch per user story or sprint, merged by pull request.
- Commit messages name the story, for example `Search: show no-results state`.
- At the end of a release: copy `app/` to `releases/vN/`, tag `vN.0`, and create a GitHub Release with notes.
