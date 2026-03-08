# BloomDots Nav + Hero Section Design

## Scope
Header/nav and hero section only. Two nav variations delivered in a single HTML file (toggle-able). Follows the exact structural pattern of `inspitation.html` (Spark Labs) with BloomDots design system, copy, and branding applied.

## Reference Sources
- `inspitation.html` — structural/layout source of truth
- `wireframe.html` — section order, nav links
- `Practical Build Blueprint.md` — GSAP map, component classes, spacing
- `Visual Direction Brief - Chatgpt.md` — art direction rules
- `CLAUDE.md` — design system (CSS vars, fonts, rules)

---

## 1. Global Foundation

### CSS Variables
Full `:root` palette from CLAUDE.md:
- `--bg: #0b0b0d` through `--orange: #ff7a1a`

### Fonts
- `@font-face` declarations for Canela (100-900) and Satoshi (300-900)
- Tailwind config: `font-instrument-serif` maps to Canela, `sans` maps to Satoshi

### Grain Overlay
- Fixed full-page noise texture layer
- Low opacity (~0.03-0.05), `pointer-events-none`
- Creates subtle film grain across entire viewport

---

## 2. Navigation

### Shared Structure (both variations)
- `position: fixed`, full-width, `z-50`
- `mix-blend-difference` with white text (inverts over light/dark content)
- `pointer-events-none` on wrapper, `pointer-events-auto` on interactive elements
- Padding: `px-6 py-6 md:px-12 md:py-8`
- Transparent over hero, no separate scroll state needed (mix-blend handles contrast)

### Logo (left side)
- "Bloom" text in Canela serif, `text-2xl md:text-3xl`
- Three dots after text: yellow (`--yellow`), blue (`--blue`), orange (`--orange`)
- Dots are small circles (~6-8px), spaced tight
- **Logo dot animation**:
  - On load: dots drift in from arc positions (scattered offscreen), settle into formation
  - Idle state: gentle floating pulse loop (subtle scale 0.9-1.1 + slight position drift)
  - Easing: `power3.out` for entrance, `sine.inOut` for idle loop

### Variation A — Site Sections + CTA
Desktop right side:
- Links: Home / Team / Services / Projects
- Style: `text-sm font-medium uppercase tracking-wide`
- Hover: `opacity-70` transition
- CTA: "Start a Project" pill button
  - `px-5 py-2 rounded-full border border-white/20`
  - Hover: `bg-white text-black` transition

### Variation B — Site Sections + Socials + CTA
Desktop right side:
- Links: Home / Team / Services / Projects
- Separator: thin vertical line `w-px h-4 bg-white/20`
- Socials: LinkedIn / Instagram (styled `text-white/60`, smaller)
- CTA: same "Start a Project" pill as Variation A

### Mobile (both variations)
- Logo left, hamburger icon right
- Hamburger: 2-line icon (not 3), animated to X on open
- **Fullscreen overlay menu**:
  - `fixed inset-0`, `bg-[var(--bg)]`, `z-[60]`
  - Large stacked nav links in Canela, `text-4xl`, centered
  - CTA button at bottom
  - Staggered fade-in entrance via GSAP

---

## 3. Hero Section

### Structure
- `<header>`, full `h-screen`, `overflow-hidden`, `bg-black`
- Three layers: video -> gradient -> content

### Video Layer
- `<video autoplay muted loop playsinline>`
- Source: Spark Labs video (placeholder, swap later)
- `absolute inset-0 w-full h-full object-cover`
- `opacity-60`, initial `scale-105` (GSAP animates to `scale-1`)

### Gradient Overlay
- `absolute inset-0`
- `bg-gradient-to-t from-[var(--bg)] via-[var(--bg)]/40 to-transparent`
- Creates dark base at bottom where content sits

### Content (bottom-left aligned)
Positioned: `absolute bottom-0 left-0 w-full px-6 py-12 md:px-12 md:py-20`

Layout: `flex flex-col md:flex-row justify-between items-end`

**Left block** (`max-w-3xl`):
1. Micro-label: `"CREATIVE AGENCY"` — `text-[11px] uppercase tracking-[0.22em]` in `--text-dim`
2. Headline (Canela):
   - Line 1: `"Make Your Brand"`
   - Line 2: `"Unskippable."` — in `--text-soft` for contrast split
   - Size: `text-5xl md:text-7xl lg:text-8xl`
   - Leading: `leading-[0.95]`, tight tracking
3. Sub-copy: `"Community-led. Culture-smart. Performance-backed."` — `--text-soft`, `text-base md:text-lg`, `max-w-md`
4. CTA row: `flex gap-4 md:gap-6`
   - Primary: filled button, `bg-[var(--text)] text-black`, uppercase, tracked
   - Secondary: border button, `border-[var(--line-strong)]`, `text-[var(--text)]`, uppercase

### Scroll Indicator (bottom-center)
- `absolute bottom-8 left-1/2 -translate-x-1/2`
- `"SCROLL"` label: `text-[10px] uppercase tracking-[0.3em]`, `--text-dim`
- Three dots below (yellow, blue, orange), ~6px each, stacked vertically with `gap-1.5`
- **Animation**: dots cascade downward sequentially (yellow -> blue -> orange), fade + translate down, reset and loop. ~2s cycle.
- Fades out on scroll via ScrollTrigger

---

## 4. GSAP Animation System

### Dependencies
- `gsap.min.js` + `ScrollTrigger.min.js` via CDN
- `gsap.registerPlugin(ScrollTrigger)`

### Hero Entrance Timeline (fires on page load)
| Element | Animation | Duration | Delay | Easing |
|---------|-----------|----------|-------|--------|
| Video | scale 1.08 -> 1 | 1.4s | 0 | power4.out |
| Nav | opacity 0->1, y -24->0 | 0.6s | 0.2s | power3.out |
| Logo dots | drift in from arcs | 0.8s | 0.3s | power3.out |
| Micro-label | opacity 0->1 | 0.4s | 0.5s | power3.out |
| Headline L1 | clip-path reveal (inset 100% 0 0 0 -> 0) | 0.9s | 0.6s | power4.out |
| Headline L2 | clip-path reveal | 0.9s | 0.75s | power4.out |
| Sub-copy | opacity 0->1, y 20->0 | 0.8s | 0.9s | power3.out |
| CTA primary | opacity 0->1, y 20->0 | 0.6s | 1.0s | power3.out |
| CTA secondary | opacity 0->1, y 20->0 | 0.6s | 1.1s | power3.out |
| Scroll indicator | opacity 0->1 | 0.5s | 1.4s | power3.out |

### Idle Loops (after entrance completes)
- Logo dots: gentle position drift + scale pulse, `sine.inOut`, infinite
- Scroll dots: cascade down loop, 2s cycle, infinite
- Scroll cue: subtle overall opacity pulse

### Scroll Behaviors (ScrollTrigger)
- Headline: slight parallax upward (`y: -40`) scrubbed to scroll
- Scroll indicator: fade out over first 100px of scroll
- Video: very slight additional zoom (`scale: 1` -> `1.02`) on scroll for depth

---

## 5. Responsive Behavior

### Desktop (1024px+)
- Full layout as described above
- Nav shows all links + CTA

### Tablet (768-1023px)
- Headline: `text-6xl`
- Nav may collapse to hamburger depending on variation
- CTAs remain side-by-side

### Mobile (<768px)
- Headline: `text-5xl`
- CTAs stack vertically, full width
- Nav: logo + hamburger only
- Fullscreen overlay menu
- Video still plays with `playsinline`
- Scroll indicator dots smaller (~5px)

---

## 6. File Output
Single `index.html` file containing:
- Both nav variations (one active, one commented or toggled via a class)
- Complete hero section
- All GSAP scripts inline at bottom
- No external dependencies beyond Tailwind CDN, GSAP CDN, Lucide icons CDN
