# How to publish an issue

Two files: `index.html` (the whole site) and `preview.png` (the link-preview card).
Put both on any static host. That's the entire system — no API key, no server, no build.

---

## The update loop

**1. Get the issue from any model.** Claude, GPT, anything.

Open your live site at `yoursite.com/#edit`, click **Copy the prompt**, and paste that
into the model along with `EDITORIAL_CHARTER.md`. It returns a JSON array.

**2. Paste it into the editor.** Same `#edit` panel. Click **Check & preview**.

It validates before you can publish anything, and reports:
- country names that don't exist on the map (those stories would get no pin)
- stories filed under the wrong continent
- bad modes, missing headlines, over-length text
- how many dispatches and how many anomalies you have per continent

The page re-renders live so you can see the real issue before it goes out.

**3. Click Download updated site.** You get a new `index.html`.

**4. Upload it.** Done.

---

## Why it works this way

`index.html` is ~300KB, and 260KB of that is map geometry — the coordinates of 177
countries.

**Never ask a model to return the whole file.** It would have to retype a quarter of a
million characters of coordinates, which is slow, expensive, and likely to corrupt the
map in a way you won't notice until a country comes out deformed.

The editor exists so the model only ever produces the ~6KB of story JSON. The geometry
is spliced back in by the page itself and cannot be touched. That is also what keeps
this model-agnostic: writing 30 JSON objects is something any model does reliably.

---

## Hosting

- **Netlify Drop** (`app.netlify.com/drop`) — drag both files onto the page, get a URL.
- **Cloudflare Pages** or **GitHub Pages** — same idea, both free.

A custom domain (~$12/year) makes it read as a publication rather than a demo.

**The editor needs a real web address.** Downloading works over `http://` and `https://`
but not when you open `index.html` straight off your hard drive — browsers block a local
page from reading its own source. Host it first, then edit there.

---

## Before you post it anywhere

In the `<head>`, set **`og:url`** to your real address. `og:image` already points at
`preview.png`; just keep that file next to `index.html`. Without them your link shows up
on LinkedIn as a bare grey link instead of a preview card.

---

## Country names

`k` must exactly match a country on the map or the story gets no pin. The editor tells
you when it doesn't. The spellings come from Natural Earth, so a few are abbreviated:

`United States of America` · `Dem. Rep. Congo` · `Bosnia and Herz.` · `Dominican Rep.`
`Central African Rep.` · `S. Sudan` · `Eq. Guinea` · `Solomon Is.` · `Timor-Leste`
`eSwatini` · `Côte d'Ivoire` · `W. Sahara` · `N. Cyprus`

---

## Files

| File | What it is |
|---|---|
| `index.html` | The product. Map, styles, interactions, stories, editor, and the charter. |
| `preview.png` | 1200×630 link-preview card. Keep it beside `index.html`. |
| `EDITORIAL_CHARTER.md` | The charter on its own, for pasting to a model. Also embedded in `index.html`. |
| `prototype.html` | Preview build for sharing a quick link. Not the file you host. |

Edit the charter in **both** places, or delete this standalone copy and keep only the one
inside `index.html` — that's the one that travels with the file.
