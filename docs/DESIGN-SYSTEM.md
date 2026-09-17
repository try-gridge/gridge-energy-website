# Design system

## Color

| Token | Value | Use |
| --- | --- | --- |
| Page background | `#0E100D` | Every section. Deeper `#0B0C0A` for the footer band. |
| Card / panel | `#181A16` | Content cards, tab rows, stat blocks. |
| Card border | `rgba(255,255,255,.08)` | 1px, all cards and dividers. |
| Accent | `#22C55E` | CTAs, live pulses, highlights, links, logo mark. |
| Accent light | `#4ADE80` | Secondary accent, gradient ends. |
| Heading text | `#F4F4F2` | |
| Body text | `#c7c7bf`, `#a8a89f` | |
| Muted text | `#8f8f86`, `#6f6f68` | Labels, captions, eyebrow text. |

Two background colors maximum. Accent green never carries body copy — full-opacity off-white on
the dark ground keeps text above 4.5:1 contrast.

## Type

- **Inter** (400–900) for everything: headings, body, UI, numerals.
- **DM Serif Display** (regular + italic) for the "Gridge Energy" wordmark only — "Gridge" upright
  in off-white, "Energy" italic in accent green.
- Headings: `clamp(26px, 2.6vw, 36px)` for section headings, larger for the hero, weight 700–800,
  `letter-spacing:-.02em`.
- Body: 15–16px, `line-height:1.6`, `text-wrap:pretty`.
- Eyebrow labels: 11–12px, weight 600, `letter-spacing:.16em–.2em`, uppercase, muted or accent.

## Layout

- Desktop page padding 64px (`[data-pad]`), collapsing to 32px then 20px on smaller screens.
- Two-column splits use `[data-split]` so one media rule collapses them all.
- Card radius 12–20px; 16px is the default.
- Sections are `min-height:100svh` and vertically centered, one idea per screen.
- Gaps, not margins: sibling groups are flex or grid with `gap`.

## Motion

Subtle and continuous, never attention-seeking. Keyframes defined in `<helmet>`:

| Animation | Use |
| --- | --- |
| `gridgePulse` | Live-data dots, logo satellite node. |
| `gridgeCorePulse` | Logo core node. |
| `gridgeSegPulse` | Hexagon spokes, staggered per spoke. |
| `gridgeHexPulse` | Hexagon outline breathing. |
| `gridgeFlowDash` | Dashed energy-flow lines in the Live Control diagram. |
| `gridgePing` | Expanding ring on live indicators. |

## Imagery

- Photography sits under a directional gradient at 50–55% opacity, so the ground reads as
  near-black with detail rather than as a photo background.
- Phone screenshots are transparent PNGs on a green radial glow with two-layer drop shadows —
  they blend into the page rather than sitting in a frame.
- Product photography is framed: rounded corners, hairline border, `object-fit:cover`.

## Components

**Card.** `#181A16`, 1px hairline border, 16px radius, 24–28px padding.

**Tab row.** Card-colored pill container, 4–5px padding, active tab in accent-tinted fill with
off-white text, inactive muted. Wraps on narrow screens; full-width and evenly split below 480px.

**Stat callout.** Large accent-green figure, muted caption beneath.

**Corner page arrows.** Fixed bottom-right, card background, hairline border; 44px minimum hit
target on phones.

**Page badge.** Accent-green two-digit number plus a muted uppercase label, top-right on desktop,
inline above the content on mobile.
