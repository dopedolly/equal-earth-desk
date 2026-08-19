# Equal Earth Desk

[Visit the live desk](https://dopedolly.github.io/equal-earth-desk/)

![Equal Earth Desk preview](preview.png)

Equal Earth Desk is a global news publication built around an interactive Equal Earth map. Each issue presents a concise selection of news, policy changes, and unusually revealing stories from across the world's continents while preserving countries' true relative areas.

The publication is intentionally lightweight. It has no backend, database, framework, build step, paid API, or package manager. A single `index.html` provides the complete interface, while small dated JSON files preserve past issues. GitHub Pages hosts both.

## Editorial model

The reader is American; America is not the center. Stories are selected for their importance where they happened, with room for events that are unusually significant for a country relative to its own recent baseline.

The selection and writing rules are documented in [`EDITORIAL_CHARTER.md`](EDITORIAL_CHARTER.md).

## Updating an issue

The scheduled Codex workflow researches and verifies a new issue, validates its story data, saves the dated issue under `issues/`, updates `issues/index.json`, and then updates the latest issue embedded in `index.html`. GitHub Pages publishes the committed files automatically.

The built-in editor at `#edit` remains available for manual previews and emergency updates. A manual download updates the latest `index.html`; a complete manual publication should also add the matching dated archive JSON and manifest entry.

## Critical map rule

Never rewrite, reformat, regenerate, or prettify `const MAP` inside `index.html`. The generated geometry must remain intact. Routine issue updates should change only the marked `ISSUE_DATE`, `ISSUE`, and `STORIES` block, plus the dated archive JSON and `issues/index.json`.

## Public files

- `index.html`: the publication interface, interactive map, latest issue data, archive browser, and editor.
- `issues/index.json`: the archive manifest.
- `issues/YYYY-MM-DD.json`: one immutable snapshot per published issue.
- `preview.png`: the 1200 by 630 social link-preview image.
- `EDITORIAL_CHARTER.md`: the public editorial charter.
- `README.md`: this project overview.

A KDY Project.
