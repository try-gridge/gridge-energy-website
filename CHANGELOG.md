# Changelog

## v4 — September 2026

Current version. Nine sections, one idea per screen.

### Structure
- Reorganized from fourteen pages to nine: Problem, Rising Load and Electrification merged into
  **Why Now**; Live Energy Flow and Circuit Monitor merged into **Live Control**; the two AI
  sections merged into **The AI**.
- Removed the fit-scaling system — sections now grow with their content instead of shrinking it.

### Navigation
- Replaced CSS scroll-snap with a JS page-to-page controller: one gesture advances exactly one
  section and centers it, with a momentum lock so a single trackpad swipe cannot skip pages.
- Sections taller than the window scroll natively until their edge, then page on.

### Content and accuracy
- Fact-checked against the August 2026 pitch deck; four claims corrected (EV charger load impact,
  builder LOI status, two startup-status claims).
- Removed two unverifiable figures from Product ("50,000+ hours of load data", "94% NILM accuracy").
- Removed the data-disclosure footnote from the footer.
- Live Control now links through to The AI: "See how the AI works →".

### Visual
- Hero photo moved to a portrait frame on the right of the home section.
- Section 06 restructured: copy and savings figures inside the card, phone screenshot on the page
  background with a green glow, matching section 05's treatment.
- Animated Gridge Energy logo added to Contact, above the closing line; divider above it removed.
- Seven approved photographs and app screenshots swapped in.

### Mobile
- Fixed phone screenshots overflowing their sections.
- Explicit section dividers and full-screen section heights so page breaks read clearly.
- Tab rows wrap and go full width; corner arrows meet 44px hit targets; page badges move inline.

### Performance (added when the v4 folder was merged into the repository)
- Animations now run only in sections within half a screen of the viewport; `prefers-reduced-motion`
  turns them off entirely. Scrolling through all nine sections went from 85 dropped frames to 7
  (headless Chrome, software rendering).
- The nav-highlight loop that ran `getBoundingClientRect` on every animation frame was replaced with
  two IntersectionObservers, and the duplicate `componentWillUnmount` was merged.
- Photography and app screenshots re-encoded to WebP: `assets/` went from 13 MB to 1.1 MB. Images
  below the first screen are lazy-loaded and carry explicit dimensions so paging targets stay put.
- `support.js` caches parsed inline-style objects (`cssToObj`). Re-parsing every style string on
  every render was the single largest cost of a tab or circuit click; median click work dropped by
  about a third at 6x CPU throttling. **This edits the generated runtime — re-exporting `support.js`
  from the design tool will drop it.**

### Waitlist
- The waitlist modal posted nowhere: it showed the success state and discarded the address. It now
  submits to the Netlify form named `waitlist`, matching the static form in `index.html`, and shows
  an error if the request fails.

## v3 and earlier

Fourteen-section layout with fit-scaling, placeholder imagery, and pre-audit copy. Preserved as
`Gridge Energy Homepage.dc.html` in the design project, not in this repository.
