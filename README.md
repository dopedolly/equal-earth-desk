# Equal Earth Desk

Equal Earth Desk is a single-file global news publication. It places up to ten curated dispatches from each continent on an Equal Earth map, preserving countries' true relative areas.

The publication is intentionally static: no backend, database, framework, build step, package manager, or news API is required. The live product is `index.html`, with `preview.png` providing its social link preview.

## Editorial model

The reader is American; America is not the center. Stories are selected for their importance where they happened, with space reserved for events that are unusually significant for a country relative to its own recent baseline.

Read `EDITORIAL_CHARTER.md` before selecting or writing stories.

## Updating an issue

1. Open the hosted site with `#edit` appended to its URL.
2. Copy the built-in prompt and use it with any web-enabled model.
3. Paste the returned JSON into the editor.
4. Run **Check & preview**.
5. Publish only when the validator reports no hard errors and the sources have been opened and checked.

Detailed instructions are in `HANDOFF.md`. Coding agents must also read `AGENTS.md`.

## Critical map rule

Never rewrite, reformat, regenerate, or prettify `const MAP` inside `index.html`. The generated geometry is deliberately kept intact. Routine updates should change only the marked `ISSUE` and `STORIES` block.

## Files

- `index.html`: the complete publication and issue editor.
- `preview.png`: the 1200 by 630 link-preview image.
- `EDITORIAL_CHARTER.md`: the editorial system prompt.
- `HANDOFF.md`: the human publishing workflow.
- `AGENTS.md`: constraints for coding agents.
- `prototype.html`: an earlier preview build, not the hosted page.

A KDY Project.
