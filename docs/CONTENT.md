# Editing content

All copy, images and numbers live in `index.html` (and its authoring twin
`src/Gridge Energy Homepage v4.dc.html` — **keep the two in sync**; `index.html` is a straight
copy).

## Copy

Section text is plain markup in the template. Search for a phrase and edit it in place. Two places
hold copy in the logic class instead, as arrays near the top:

- `APP_SHOTS` — the three tabs in section 05 (`src`, `alt`, `title`, `body`).
- The AI tab blocks in section 06 — copy sits in the template, one `<sc-if>` per tab.

Keep body copy under about 55 characters per line's worth of `max-width` (the existing
`max-width:46ch`–`56ch` values); longer lines break the one-screen-per-section fit.

## Images

Referenced images, all in `assets/`:

| File | Used in |
| --- | --- |
| `w_hero_phone_panel.webp` | 01 Home — hero photo |
| `w_bg_grid_transmission.jpg` | 02 Why Now — background |
| `w_panel_closed.webp`, `w_panel_open.webp` | 03 Product |
| `w_app_live_consumption.webp`, `w_app_device_control.webp`, `w_app_costs_safety.webp` | 05 The App tabs |
| `w_app_ai_savings_schedule.webp`, `w_app_costs_safety.webp` | 06 The AI tabs |
| `w_bg_city_skyline.jpg` | 08 Ecosystem — background |
| `gridge_nav_logo.svg`, `gridge_icon_256x256.png` | logo / favicon |

Rules when replacing them:

- **Phone screenshots** must be PNG with a transparent background. They are sized by height
  (`height:min(58svh,600px)`) and sit on a green radial glow, so an opaque rectangle will show as
  a visible box. Keep the same aspect ratio or the height cap will need adjusting.
- **Photography** should be JPEG, roughly 1600–2400px on the long edge, quality ~80. Background
  photos are rendered at reduced opacity under a gradient, so contrast matters more than detail.
- Keep filenames stable, or update every reference (search the filename — some appear in both the
  template and `APP_SHOTS`).
- Always write real `alt` text, except on the two decorative background photos, which correctly
  use `alt=""`.

## Numbers and claims

Every figure on the page traces to the pitch deck or to the meter export in `data/`. Four claims
were corrected against the deck during build (EV charger load impact, builder LOI status, and two
startup-status claims), and two unverifiable figures were removed from section 03 — do not
reintroduce numbers without a source. The ₹/hr estimates assume a **₹8/kWh** tariff; that constant
lives in the logic class.

## Adding a section

1. Copy an existing `<section>` as a template — it must carry `data-pageshell`, a sequential
   `data-page-idx`, a unique `id`, and a `data-screen-label`.
2. Renumber the `data-page-idx` of every later section, and the visible page badge inside each.
3. Add the nav entry if it should appear in the header, and set `data-nav` to the nav key it
   should highlight.
4. Re-check the scroll controller: it counts `[data-page-idx]` elements, so it picks up the new
   section automatically once numbering is sequential.

## Style guardrails

- Inline styles only. Do not introduce CSS classes or a stylesheet — the page is authored so that
  markup and styling arrive together.
- The only legal global CSS is what is already in `<helmet>`: font links, `@keyframes`, body
  resets, and the responsive `@media` blocks.
- Two background colors maximum (`#0E100D` page, `#181A16` cards). Accent green `#22C55E` is for
  CTAs, live indicators and highlights — not for body text.
