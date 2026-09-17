# Gridge Energy — Website

Marketing website for **Gridge Energy**, a smart electrical distribution panel for Indian homes.
Single page, nine full-screen sections, dark theme, with two interactive sections driven by real
anonymized meter data from a Gridge-monitored home.

- **Live site:** _add URL after first deploy_
- **Source of truth:** `src/Gridge Energy Homepage v4.dc.html`
- **Deployable entry point:** `index.html` (identical markup, renamed for static hosting)

---

## Contents

| Path | What it is |
| --- | --- |
| `index.html` | The website. Static, no build step. |
| `src/Gridge Energy Homepage v4.dc.html` | Authoring copy of the same file (opens in the design tool). |
| `support.js` | Runtime that renders the page's template + logic class. Required, do not edit. |
| `assets/` | Photography, app screenshots, logo files actually referenced by the page. |
| `data/` | Anonymized meter series and alarm log powering the live sections. |
| `docs/DEPLOYMENT.md` | How to host it (GitHub Pages, Netlify, Vercel, any static host). |
| `docs/CONTENT.md` | How to change copy, images and numbers without breaking anything. |
| `docs/DATA.md` | Shape and provenance of the live data, and how to refresh it. |
| `docs/DESIGN-SYSTEM.md` | Colors, type, spacing, motion, component patterns. |
| `CHANGELOG.md` | Version history. |

---

## Running it locally

There is no build, no npm, no framework install. But it **must be served over HTTP** — opening
`index.html` from the filesystem will block the JSON data fetches.

```bash
# any one of these, from the repo root
python3 -m http.server 8080
npx serve .
php -S localhost:8080
```

Then open <http://localhost:8080>.

---

## How the page is built

The page is one **Design Component**: a single HTML file containing

1. a `<helmet>` block — font links and the only global CSS that cannot be inline
   (`@font-face`, `@keyframes`, body resets, and the responsive `@media` overrides);
2. a **template** — the nine `<section>` elements, styled entirely with inline styles;
3. a **logic class** (`class Component extends DCLogic`) at the bottom of the file — state,
   data selection, interaction handlers, and the page-to-page scroll controller.

`support.js` reads that structure and renders it. Values the template needs are exposed by name
from `renderVals()` and referenced as `{{ name }}` holes; `<sc-if>` and `<sc-for>` handle
conditionals and repetition.

**Styling rule:** all layout and color lives in inline `style="…"` attributes. There are no CSS
classes. Responsive behavior is handled by the attribute-selector media queries in `<helmet>`
(`[data-split]`, `[data-cols]`, `[data-pad]`, `[data-appshot]`, `[data-hero-photo]`,
`[data-tabrow]`, `[data-pagebadge]`, `[data-navdots]`).

---

## Page map

| # | Section id | Label | What it does |
| --- | --- | --- | --- |
| 01 | `home` | Home | Headline, dual CTA, three proof callouts, hero photo (app in hand + panel). |
| 02 | `p2` | Why Now | The case for change: the century-old distribution board, grid CAPEX, electrification and EV load. Grid photo background. |
| 03 | `product` | Product | What the panel is: closed/open panel photos plus the feature grid. |
| 04 | `live-data` | Live Control | **Interactive.** Energy-flow diagram (grid/solar/battery/generator → panel → circuits) and the Circuit Monitor. Tap a circuit to switch it off and watch totals and insight redraw. Links through to section 06. |
| 05 | `p5` | The App | Three tabbed app screens: live consumption, device control, appliance cost + safety. |
| 06 | `technology` | The AI | Three tabbed AI capabilities: cost savings, scheduling, fault prediction. Card holds the copy; the phone sits on the page background. |
| 07 | `p8` | Engineering | Hardware specification points and headline stat cards. |
| 08 | `ecosystem` | Ecosystem | Builders & developers, DISCOMs & utilities, homeowners. City skyline background. |
| 09 | `contact` | Contact | Animated Gridge Energy logo, closing line, waitlist CTA, footer. |

Each section carries `data-page-idx` (1–9), `data-pageshell`, and `data-screen-label`.
`data-page-idx` is what the scroll controller and the side rail read — keep it sequential if you
add or remove a section.

---

## Interactive behavior

**Page-to-page scrolling.** The logic class owns navigation (`setupPaging`, `gotoPage`,
`goToIndex`, `pageTop`). One wheel notch, one arrow key press, or a click on the corner
arrows advances exactly one section and centers it in the window. A ~900 ms lock absorbs trackpad
momentum so a single gesture cannot skip a page; sections taller than the window scroll natively
until you reach their edge, then the next gesture pages on. CSS scroll-snap is deliberately **not**
used — it fought the JS controller and caused double-jumps.

**Circuit Monitor.** `toggleCircuit(i)` flips a circuit off, and Total Active, the ₹/hr figures and
the insight line recompute from the remaining loads. Cost is estimated at ₹8/kWh.

**Live snapshot selection.** On load, and every 60 seconds after, the page picks the data snapshot
nearest to the visitor's current time of day, so the numbers track the real daily load curve.

**Tab groups.** Sections 05 and 06 each hold three tabs, driven by `appTab` / `aiTab` state and
rendered through `<sc-if>` blocks.

---

## Responsive rules

- **> 1080px** — desktop layout: two-column splits, 64px page padding, page-number badges in the
  top-right corner, JS page-to-page scrolling.
- **≤ 1080px** — splits collapse to one column, the side rail hides, sections become
  `min-height:100svh` blocks separated by a hairline divider, and page badges move inline above
  the content.
- **≤ 720px** — tighter padding and smaller tab pills.
- **≤ 480px** — tab rows go full width and split evenly, phone screenshots cap at 72vw, and the
  corner arrows grow to 44px hit targets.

---

## Editing checklist

Before you commit a change:

- [ ] Served over HTTP and checked at 1440px, 820px and 390px widths.
- [ ] No horizontal scrollbar at 390px; no phone screenshot spilling past its section.
- [ ] Arrow keys and the corner arrows still advance exactly one page.
- [ ] A circuit toggle still updates Total Active and the insight line.
- [ ] Any new section has a sequential `data-page-idx` and a `data-screen-label`.
- [ ] New images added to `assets/` and compressed (see `docs/CONTENT.md`).

---

## Licence and content rights

Code in this repository is Gridge Energy's. Photography, app screenshots and the meter data are
company material and **not** for redistribution. Add a `LICENSE` file before making the
repository public.
