# Bloomdots Design System

**Company:** Bloomdots — "Make Your Brand Unskippable"
**Type:** Creative Content Agency
**Tagline:** Make Your Brand Unskippable

## Overview

Bloomdots is a creative content agency that helps brands stand out through bold, memorable creative work. The brand identity is energetic, playful, and confident — built around a three-dot "B" logomark that signals vibrancy and creativity. The agency positions itself as a partner that transforms ordinary brands into unavoidable presences.

## Sources

- **Logo:** `uploads/logo.jpeg` (isolated mark; three teardrop dots forming a stylized B/D)
- No codebase or Figma links provided. Design system was inferred from logo + brand description.

---

## CONTENT FUNDAMENTALS

### Voice & Tone
- **Bold and direct.** Short, punchy statements. No hedging.
- **Confident without arrogance.** "We make brands unskippable" — active, assertive.
- **Action-oriented.** Verbs lead. "Make," "Create," "Build," "Transform."
- **You-first.** The copy speaks to "your brand," "your audience" — client-centric.
- **No jargon.** Creative work is explained in clear, accessible language.
- **Slightly playful.** A wit lives under the professionalism — a wink, not a joke.

### Casing
- Headlines: **Sentence case** (not Title Case, not ALL CAPS)
- CTAs: **All caps** for emphasis on buttons/labels: `GET STARTED`, `SEE WORK`
- Brand name: Always **Bloomdots** (capital B, lowercase rest, one word)

### Punctuation & Style
- Em dashes for drama: "We don't just create content — we create moments."
- Periods at end of standalone callouts. No trailing ellipsis.
- Avoid exclamation marks in body copy. Confidence doesn't need them.
- Numbers below 10 spelled out in copy; numerals for stats/metrics.

### Emoji & Special Characters
- **No emoji** in primary brand copy or headings.
- Dot "·" bullet separators used in nav or tag lists.
- The brand mark (three dots) is the icon system — lean into dot motifs.

### Specific Copy Examples
- "Make Your Brand Unskippable"
- "Creative content that commands attention"
- "We don't do forgettable"
- "Your story. Told boldly."
- "Content that moves people"

---

## VISUAL FOUNDATIONS

### Brand Colors
Three signature colors derived from the logomark:
- **Bloom Orange** `#E84E28` — Coral-red; heat, cultural sharpness, energy
- **Bloom Blue** `#29B9EA` — Sky blue; structure, trust, focus
- **Bloom Amber** `#FAB72B` — Warm yellow; spotlight, optimism, warmth

The three are co-equal brand primaries. None is the default; each section picks the one that fits its register.

### Color System
- **Light theme** (primary): White backgrounds, dark near-black text
- **Dark theme** (secondary): Near-black backgrounds, soft white text
- Backgrounds are clean and minimal — the brand colors do the work
- Pick one brand colour to lead each surface; rotate the lead across sections so the page travels through all three. Avoid mixing all three at equal weight inside a single surface (one section, one card, one hero).

### Typography
- **Display / Editorial Headlines:** Canela — a high-contrast serif. Used for hero h1, section h2s, and CTA headlines. Creates an editorial, premium feel.
  - Display: Canela Black (900)
  - h1: Canela Bold (700)
  - h2: Canela Bold (700)
- **Headings / UI / Body:** Satoshi — a geometric sans. Used for card titles, nav, buttons, body copy, captions, labels, stats.
  - Headings (h3, h4): Satoshi Bold (700)
  - Body / Lead: Satoshi Regular (400) / Medium (500)
  - Labels / Buttons: Satoshi Bold (700)
  - Display stats: Satoshi Black (900)
- **Mono / Code:** JetBrains Mono (Google Fonts CDN) — technical use only.
- All brand fonts loaded locally from `fonts/` via `@font-face` (no Google Fonts dependency for Canela or Satoshi).
- Type scale follows a major-third (1.25×) modular scale.
- Line heights: Display 1.05–1.1, Headings 1.2–1.3, Body 1.6–1.7.
- Letter spacing: Display −0.025em, Headings −0.015em, Body 0.

### Font Files
- `fonts/Satoshi-*.otf` — 300 Light · 400 Regular · 500 Medium · 700 Bold · 900 Black (+ italics)
- `fonts/Canela-*-Trial.otf` — 100 Thin · 300 Light · 400 Regular · 500 Medium · 700 Bold · 900 Black (+ italics)

### Spacing
- Base unit: **8px**
- Scale: 4, 8, 12, 16, 24, 32, 48, 64, 96, 128px
- Section padding: 96–128px vertical on desktop
- Card padding: 24–32px
- Component internal: 8–16px

### Backgrounds
- Primary: `#FFFFFF` (light) / `#111111` (dark)
- Surface: `#F7F7F7` (light) / `#1A1A1A` (dark)
- The three brand colors appear as full-bleed section backgrounds for hero/callout moments
- No gradients on primary surfaces. Gradients only allowed as subtle overlays on images.
- Dot/circle motifs can appear as large decorative shapes in the background (low opacity)

### Imagery
- **Warm, vivid, high-contrast** photography. Color-graded toward the brand palette.
- No cold/desaturated images. Brand energy is warm and alive.
- Full-bleed hero images with text protection overlays (gradient-to-transparent, dark)
- Campaign content: bold typography overlaid on strong visuals

### Animation
- **Easing:** ease-out for entrances, ease-in-out for state changes
- **Duration:** 200ms for micro-interactions, 400–600ms for layout transitions
- **Entrance:** Fade up (translateY 16px → 0, opacity 0 → 1)
- **Hover states:** Subtle scale (1.0 → 1.02), color darkens/lightens 10%
- **Press states:** Scale down slightly (0.97), instant
- **No bounces.** Clean, confident motion. No spring physics.

### Borders & Radius
- **Corner radius:** `8px` for cards/inputs, `12px` for large cards, `999px` for pills/chips, `50%` for circular avatars
- **Borders:** `1px solid` using border token colors (subtle, low contrast)
- No heavy border usage — whitespace and color do the separation work

### Cards
- Light theme: white bg, `0 2px 12px rgba(0,0,0,0.08)` shadow, 12px radius
- Dark theme: `#1E1E1E` bg, `0 2px 16px rgba(0,0,0,0.3)` shadow, 12px radius
- Hover: shadow lifts to `0 8px 32px rgba(0,0,0,0.14)`, slight translateY(-2px)

### Shadows
- `--shadow-sm: 0 1px 4px rgba(0,0,0,0.07)`
- `--shadow-md: 0 2px 12px rgba(0,0,0,0.09)`
- `--shadow-lg: 0 8px 32px rgba(0,0,0,0.13)`
- `--shadow-xl: 0 20px 60px rgba(0,0,0,0.18)`

### Icons
- No proprietary icon set identified. Lucide Icons (CDN) used as standard.
- Stroke weight: 1.5px. Style: outline.
- Icon sizes: 16px (inline), 20px (UI), 24px (feature), 40px (callout)
- See ICONOGRAPHY section below.

---

## ICONOGRAPHY

### Approach
Bloomdots' primary visual icon is the logomark itself (three dot shapes forming a B). Beyond the logo, a clean outline icon system is used for UI.

### Icon System
- **Primary:** Lucide Icons (https://unpkg.com/lucide@latest/dist/umd/lucide.js)
- Stroke-based, 24×24 viewBox, 1.5px stroke weight
- Style: minimal, geometric, outline — matches the brand's clean aesthetic
- **No emoji as icons.** No filled/solid icon style.

### Logo Assets
- `assets/logo.jpeg` — primary logo mark (square, white background)
- The mark is three teardrop dots: Blue (top), Amber (accent), Orange (large, bottom)

### Usage
- Logo mark minimum size: 32px
- Always maintain white/light background behind logo on light theme
- On dark backgrounds, use a version with inverted or white treatment

---

## FILE INDEX

```
/
├── README.md                     ← This file
├── SKILL.md                      ← Agent skill descriptor
├── colors_and_type.css           ← CSS custom properties: colors, type, spacing
├── assets/
│   └── logo.jpeg                 ← Primary logo mark
├── preview/
│   ├── colors-brand.html         ← Brand color swatches
│   ├── colors-light.html         ← Light theme semantic colors
│   ├── colors-dark.html          ← Dark theme semantic colors
│   ├── type-scale.html           ← Display/heading/body type scale
│   ├── type-weights.html         ← Font weight specimens
│   ├── type-body.html            ← Body text specimens
│   ├── spacing-tokens.html       ← Spacing scale
│   ├── spacing-radius.html       ← Border radius tokens
│   ├── spacing-shadows.html      ← Shadow system
│   ├── components-buttons.html   ← Button variants
│   ├── components-inputs.html    ← Input / form fields
│   ├── components-cards.html     ← Card components
│   ├── components-badges.html    ← Badges, chips, tags
│   └── brand-logo.html           ← Logo usage
└── ui_kits/
    └── website/
        ├── README.md             ← UI kit overview
        ├── index.html            ← Interactive agency website prototype
        ├── Header.jsx            ← Navigation header
        ├── Hero.jsx              ← Hero section
        ├── Services.jsx          ← Services / offerings grid
        ├── Work.jsx              ← Portfolio/case studies
        ├── CTA.jsx               ← Call-to-action section
        └── Footer.jsx            ← Footer component
```
