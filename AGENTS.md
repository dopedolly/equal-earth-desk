# Equal Earth Desk — instructions for coding agents

A KDY Project. A single-file news site: ten dispatches per continent on an Equal Earth
map. Read this before touching anything.

## The one rule that matters

**Never rewrite, reformat, regenerate, or "clean up" `const MAP`.**

It is ~260KB of projected coordinates for 177 countries inside `index.html`. It is
generated output, not source. Reformatting it, re-indenting it, running a prettier pass
over the file, or echoing it back through a model will corrupt the map — and the failure
is silent: the page still loads, a country is just quietly the wrong shape.

If a task seems to require editing `MAP`, stop and say so instead.

## What you are normally being asked to change

Only this block, near the top of the `<script>` in `index.html`:

```js
const ISSUE = "Issue 01";
const STORIES = [ ... ];
```

Both are marked in the file:
`>>> STORIES - THIS IS THE ONLY BLOCK YOU EVER EDIT <<<` … `END OF STORIES BLOCK`

## The story object

```js
{
  c: "Africa",              // one of: North America, South America, Europe, Africa, Asia, Oceania
  k: "Nigeria",             // MUST be a key in MAP.countries, or the story gets no pin
  m: "policy",              // "news" | "policy" | "fun"
  a: 1,                     // 1 if unusually big FOR THAT COUNTRY, else 0
  h: "Headline, ~90 chars",
  w: "Why it matters, ~200 chars, stakes stated locally, ending on the takeaway",
  s: "The outlet's name",
  u: "https://direct-link-to-the-article"
}
```

Up to 10 per continent. At least 3 of every 10 must have `a: 1`. Return fewer rather than
padding a continent with weak items.

Country spellings come from Natural Earth. Check against `MAP.countries` before writing —
`United States of America`, `Dem. Rep. Congo`, `Bosnia and Herz.`, `Dominican Rep.`,
`Central African Rep.`, `S. Sudan`, `Eq. Guinea`, `Solomon Is.`, `Timor-Leste`,
`eSwatini`, `Côte d'Ivoire`, `W. Sahara`, `N. Cyprus`.

## Sourcing — non-negotiable

Every story needs a real `s` and `u`. **Search the web; do not answer from memory.** A
model working from recall produces stories that read as real and are not, with links
invented to match. If you cannot retrieve and open a source, drop the story.

Prefer local and regional outlets over US wire copy about the same place.

## Editorial rules

The full charter is an HTML comment at the top of `index.html`, and also in
`EDITORIAL_CHARTER.md`. Read it — it is the product. The short version:

- **American as the reader, not American as the center.** The reader's nationality decides
  what needs explaining, never what is important.
- No story whose real subject is the United States.
- Consequence is uncapped — big economies legitimately produce more consequential news —
  but three slots in ten go to what is unusually big *for that place*.
- No analogies drawn from US consumer culture. Never exoticize.
- Register: Morning Brew / The Best One Yet. Concrete, specific numbers, funny, never
  laughing at anyone.

## Also safe to change

Styles in `<style>`, the markup outside `<script>`, footer copy, and the `<head>` meta
tags. `og:url` should point at the live address; `og:image` expects `preview.png` beside
`index.html`.

## Do not add

No build step, no framework, no npm, no bundler, no backend, no external requests beyond
the Google Fonts link. This file has to stay openable and editable by anyone, with any
tool, years from now. That constraint is the design, not an oversight.

## Checking your work

`index.html` opened in a browser should show: 6 continent sections, one lead card each,
a country silhouette on every card, a pin on the map per story, working mode and anomaly
filters, and no console errors. Adding `#edit` to the URL opens a validator that reports
bad country names, missing sources, and per-continent counts.

## Files

| File | Role |
|---|---|
| `index.html` | The product. Everything is in here. |
| `preview.png` | 1200×630 link-preview card. Keep beside `index.html`. |
| `EDITORIAL_CHARTER.md` | The charter standalone. Mirrored inside `index.html`. |
| `HANDOFF.md` | Instructions for the human publishing an issue. |
| `prototype.html` | Preview build. Not the hosted file. |
