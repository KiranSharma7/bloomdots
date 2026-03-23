# Section 3 Redesign — Two-Tier Logo Showcase

**Date:** 2026-03-23
**Section:** 3 — "Built on Trust" Logo Wall

## Summary

Redesign Section 3 into a two-tier partner logo showcase:

- **Tier A (Card Pile):** 6 large placeholder logo cards with the existing scroll-pinned scattered pile animation
- **Tier B (Logo Grid):** 16 smaller placeholder logos in a grid with GSAP stagger entrance animation

## Overall Structure

```
┌─────────────────────────────────────────────────┐
│  TIER A: "Built on Trust" Card Pile             │
│  - 100vh, pinned during scroll scrub            │
│  - Heading: "The Brands We Move" / "Built on    │
│    Trust."                                      │
│  - 6 white cards fly in from offscreen,         │
│    land at scattered positions with rotation     │
│                                                 │
│  ── unpins, natural scroll continues ──         │
│  ── thin var(--line) divider ──                 │
│                                                 │
│  TIER B: Logo Grid (16 logos)                   │
│  - Label: "& Many More"                         │
│  - 8 per row (desktop), 4 (tablet), 3 (mobile) │
│  - 2 rows of 8 = 16 items                      │
│  - GSAP stagger entrance on scroll              │
│  - py-20 lg:py-28 padding                       │
└─────────────────────────────────────────────────┘
```

## Tier A — Card Pile (6 Big Logos)

### Cards
- Same white rounded card design as current implementation
- SVG logo + brand label underneath
- Responsive sizing: 140px → 158px → 176px wide
- Placeholder brands (any 6 from current set — will be swapped later)

### Animation (unchanged from current, adapted for 6)
- Scroll-pinned scrub: `start: '50% 50%'`, `end: '500% 50%'`
- Cards fly in pairs from offscreen directions (bottom, left, right, top, bottom-left, top-right)
- Land at scattered positions with rotation
- Wider spread than current 12-card version — more visual weight per logo
- `prefers-reduced-motion`: show all cards at final positions immediately

### Positions (re-spaced for 6)
```
Card 1: top-left area
Card 2: top-right area
Card 3: center-right
Card 4: center-left
Card 5: bottom-right
Card 6: bottom-left
```

## Tier B — Logo Grid (16 Logos)

### Layout
- Below card pile after unpin
- Thin `var(--line)` divider separating from Tier A
- Small uppercase label: "& Many More" (same style as section labels — `text-dim`, `tracking-[0.32em]`)
- Padding: `py-20 lg:py-28`

### Logo Items
- Dark surface tiles: `var(--surface)` background (`rgba(255,255,255,0.04)`)
- Subtle border: `1px solid var(--line)`
- Rounded: `rounded-lg` (8px)
- Square-ish boxes (~120px tall) with centered placeholder SVG/icon in `var(--text-dim)`
- No brand labels — just logo marks (minimal vs. the 6 big ones)
- Grid gap: `gap-3 lg:gap-4`

### Grid Responsive
- Desktop: 8 per row (2 rows)
- Tablet: 4 per row (4 rows)
- Mobile: 3 per row (~6 rows)

### Animation (GSAP ScrollTrigger Stagger)
- Initial state: `opacity: 0`, `y: 30`, `scale: 0.85`
- Final state: `opacity: 1`, `y: 0`, `scale: 1`
- Easing: `power3.out`
- Duration: `0.6s` per item
- Stagger: `0.06s` (wave effect left-to-right, row by row)
- ScrollTrigger: `start: 'top 80%'`, no pin, plays once
- `prefers-reduced-motion`: show all items immediately

## What Changes from Current Implementation

### HTML
- Remove cards 7–12 from `tca-scroll-card-wrapper`
- Keep cards 1–6 (any 6 placeholder brands)
- Add new `logo-grid` container after `#logo-stack-inner` with 16 placeholder logo tiles
- Add "& Many More" label above the grid

### CSS
- Keep all existing `#logo-stack`, `.tca-scroll-card`, `.stack-heading` styles
- Add new `.logo-grid` styles (grid layout, responsive columns)
- Add `.logo-grid-item` styles (dark surface tiles)

### JavaScript
- Update `finalPositions` array from 12 to 6 entries (wider spread)
- Update `entryDirections` array from 12 to 6 entries
- Update `startRotations` array from 12 to 6 entries
- Add new GSAP ScrollTrigger block for `.logo-grid-item` stagger entrance

## Design Decisions

- **GSAP over CSS keyframes** for the grid animation — keeps one animation system across the entire site
- **No filters/tabs** on the grid — static page, no Elementor, so MutationObserver pattern from reference code is unnecessary
- **Dark tiles** for grid logos (vs. white cards for big logos) — creates clear visual hierarchy between tiers
- **No brand labels on grid items** — keeps them minimal, lets the 6 big cards be the stars
