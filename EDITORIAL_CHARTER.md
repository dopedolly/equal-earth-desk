# Editorial Charter

This document is the source of truth for the Equal Earth Desk curation pipeline.
Change this file to change the product.

## Audience

Young Americans, roughly 18–30. Assume curiosity, not expertise. Explain necessary
context clearly, without talking down to the reader.

## Core principle

**American as the reader, not American as the center.**

The reader's nationality determines what needs explaining. It never determines what is
important.

## What the daily desk is

Equal Earth Desk is a ranked briefing of the most important recent developments across
the six inhabited continents: North America, South America, Europe, Africa, Asia, and
Oceania.

Start with developments reported or materially updated during the previous 24 hours. If
a continent does not have enough genuinely important developments, extend the window to
72 hours and retain major continuing stories only when they received a substantive new
development.

Aim for ten dispatches per continent. If ten defensible stories do not exist, publish
fewer. Never fill a slot with weak, stale, celebrity, lifestyle, travel, viral, or novelty
content merely to make the count reach ten.

## Selection and ranking

A story earns a slot through consequence, not color.

Rank candidates within each continent using:

1. Number of people materially affected.
2. Significance for law, government, rights, elections, security, public health, climate,
   economics, business, technology, migration, or everyday life.
3. Scale and durability of the change.
4. Urgency and the degree to which the development changes an ongoing major story.
5. Strength and independence of the available evidence.

Build a broad candidate pool before choosing. Do not select the first ten searchable
headlines.

A story must matter where it happened. A United States connection may appear as context,
but it must not be the reason the story was selected.

Geographic diversity is useful, but it is not a quota. Never demote a more consequential
story merely to add another country to the map.

Do not publish two dispatches about the same development. Assign a cross-border story to
its principal geography unless separate regional consequences genuinely warrant separate
coverage.

The three modes are `news`, `policy`, and `fun`. Hard news and policy should dominate
the daily ranking. A fun story qualifies only when it is independently newsworthy and
widely reported, not because the desk needs a lighter item.

## Source hierarchy

Every dispatch must be based on a source page that was actually opened and read.
A search-result snippet, remembered fact, AI summary, or headline alone is never a source.

### Preferred reporting

Ordinarily use reporting from a major independent international newsroom, including:

- Reuters
- Associated Press
- AFP
- BBC
- CNN
- Financial Times
- The Wall Street Journal
- The New York Times
- The Washington Post
- Bloomberg
- The Guardian
- The Economist
- Al Jazeera
- France 24
- Deutsche Welle

A comparably established major national or regional general-news organization may be
used when it provides stronger local reporting than the international outlets. It must
have a real newsroom, named reporting, a record of corrections or editorial
accountability, and a direct article page. The daily run report must identify every time
this exception is used.

### Primary-source verification

For laws, regulation, courts, elections, economic statistics, public health, climate,
company disclosures, and government decisions, verify the central claim against a
primary source whenever one is available. Examples include legislation, court decisions,
government ministries, central banks, election authorities, regulators, official
statistics, company filings, UN agencies, WHO, World Bank, IMF, OECD, and EU institutions.

The displayed link should normally be the strongest major-news report because it gives
readers context. A primary document may be displayed instead when it is the clearest
authoritative account.

### Prohibited sources

Do not use:

- Entertainment, celebrity, lifestyle, or travel outlets.
- SEO content farms, anonymous blogs, or sites without transparent editorial standards.
- News aggregators or syndication pages such as MSN, Yahoo, or copied wire pages.
- Press-release aggregators or company marketing presented as reporting.
- Search-results pages, social posts, or an article that could not be opened.
- A small outlet merely because it is the only result that supports an attractive
  headline.

For disputed, fast-moving, or high-stakes claims, cross-check at least two independent
reliable sources. If the central claim cannot be verified, drop the story.

## Framing

State what changed, when it changed, who made the decision, and who is affected.

State stakes in local terms. Countries and people are protagonists, not objects.

Do not exoticize. Avoid words such as "bizarre," "strange," "little-known," and "you
won't believe."

Do not use "what America can learn from X" framing or make American consumer culture the
unit of comparison.

Distinguish confirmed facts from allegations, forecasts, estimates, and analysis.

Use plain, concise English. Be lively but not cute. Specific numbers, dates, institutions,
and affected populations are more useful than jokes or vague claims.

## Output contract

Return a JSON array and nothing else. Use exactly these keys:

```json
[
  {
    "c": "Africa",
    "k": "Nigeria",
    "m": "policy",
    "a": 1,
    "h": "Headline in plain English",
    "w": "What changed and why it matters locally",
    "s": "Reuters",
    "u": "https://www.reuters.com/..."
  }
]
```

| Key | Meaning |
|---|---|
| `c` | Exactly one of: `North America`, `South America`, `Europe`, `Africa`, `Asia`, `Oceania`. |
| `k` | Country name matching a key in `MAP.countries` exactly. |
| `m` | `news`, `policy`, or `fun`. |
| `a` | `1` when the story is unusually significant for that country, otherwise `0`. |
| `h` | Concise English headline. |
| `w` | Concise context and local stakes. |
| `s` | Displayed source name. |
| `u` | Direct working `https://` article or primary-source URL. |

`k` uses Natural Earth spellings, not ISO codes. Examples include `United States of
America`, `Dem. Rep. Congo`, `Bosnia and Herz.`, `Dominican Rep.`, `Central African
Rep.`, `S. Sudan`, `Eq. Guinea`, `Solomon Is.`, `Timor-Leste`, `eSwatini`,
`Côte d'Ivoire`, `W. Sahara`, and `N. Cyprus`.

## Publishing constraints

Before publishing:

- Validate every country, continent, mode, and direct URL.
- Reject duplicate stories and continent mismatches.
- Confirm every source page opens and supports the written claim.
- Preserve the generated `const MAP` block byte-for-byte.
- Do not publish if sourcing or hard validation fails.
- Report story counts by continent, displayed-source breakdown, regional-source
  exceptions, primary-source checks, validation results, commit identifier, and live URL.
