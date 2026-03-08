# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

BloomDots is a creative agency website — currently in the planning/design phase. The repo contains planning documents and a structural wireframe HTML file, but no production build system yet. The site must be built as a single HTML page (or framework of choice) using **Tailwind CSS** and **GSAP**.

## Current Repo Contents

- `wireframe.html` — structural wireframe built with Tailwind CDN; the source of truth for section order and layout skeleton
- `DEV-NOTES.md` — interaction and animation notes extracted from hand-drawn wireframes (Wireframes/1–9.jpeg)
- `Practical Build Blueprint.md` — detailed technical spec: color system, font system, spacing, component classes, GSAP animation map per section, build order
- `Visual Direction Brief - Chatgpt.md` — art direction brief: brand personality, visual philosophy, section-by-section direction
- `BloomDots Website Copy.pdf` — final website copy (headlines, body, CTAs, stats)
- `Wireframes/1–9.jpeg` — hand-drawn wireframes, one per section

## Design System

### Tech Stack
- **Tailwind CSS** (CDN for prototype; proper config for production)
- **GSAP + ScrollTrigger** for all animations
- Two fonts only: `"Canela"` (display/headings) + `"Satoshi"` (sans/body/UI)
- Fonts are loaded locally via `@font-face` — no Google Fonts import needed
  - Canela: `Canela_Collection/Canela Family/Canela-*-Trial.otf` (weights 100–900)
  - Satoshi: `Satoshi_Complete/Satoshi_Complete/Fonts/WEB/fonts/Satoshi-*.woff2` (weights 300–900)

### CSS Variables (must be defined at `:root`)
```css
:root {
  --bg: #0b0b0d;
  --bg-soft: #121317;
  --bg-elevated: #17191f;
  --surface: rgba(255,255,255,0.04);
  --surface-2: rgba(255,255,255,0.07);
  --text: #f5f1e8;
  --text-soft: rgba(245,241,232,0.72);
  --text-dim: rgba(245,241,232,0.48);
  --line: rgba(245,241,232,0.12);
  --line-strong: rgba(245,241,232,0.22);
  --yellow: #f4c430;
  --blue: #4f7cff;
  --orange: #ff7a1a;
}
```

### Utility Class Conventions
Use these semantic helper classes alongside Tailwind utilities:
`bd-section`, `bd-container`, `bd-label`, `bd-title`, `bd-copy`, `bd-cta-primary`, `bd-cta-secondary`, `bd-noise`, `bd-grid-12`, `bd-panel`, `bd-dot`, `bd-line`

### Container
```html
<div class="mx-auto w-full max-w-[1440px] px-5 sm:px-8 lg:px-12 xl:px-16">
```

## Site Section Order & Signature Effects

| # | Section | Signature GSAP behavior |
|---|---------|------------------------|
| 1 | Hero | Line-by-line headline clip reveal; background video scales from 1.08→1 |
| 2 | Team "Dots That Connect" | ScrollTrigger scrub: portrait circles scatter→converge; SVG connecting lines draw in |
| 3 | Logo Wall "Local to Global" | Logos fade in one-by-one at scattered positions with blur→sharp |
| 4 | Services Mosaic | Asymmetrical 12-col grid tiles; clip-path reveal on enter; background scale + blur decrease on hover |
| 5 | Stats Wall | Count-up numbers on scroll reveal; broken editorial grid (not uniform cards) |
| 6 | Portfolio (Horizontal) | GSAP pin + horizontal scrub; each panel = `min-w-[100vw]`; content and images parallax independently |
| 7 | Three Dots Philosophy | Dots drift in from arcs; SVG lines draw; idle pulse loop |
| 8 | Process (3 phases) | Horizontal line draws L→R; phase markers scale in sequentially |
| 9 | Founder Note | Portrait mask/wipe reveal; text stagger; signature fade-in |
| 10 | CTA "Ready to Bloom?" | Oversized headline reveal; ambient dot drift; tactile CTA hover |

## Key Design Rules

- **Dark first**: `--bg` (#0b0b0d) is the base. Never use white backgrounds.
- **Accent colors** (yellow/blue/orange) are signals, not decoration — use only for: active states, dot graphics, timeline markers, hover cues, numeric highlights, micro labels, Three Dots section.
- **Border radius**: 6–16px max. No soft SaaS rounding. Brutalist option: `rounded-none`.
- **Motion easing**: `power3.out`, `power4.out`, `expo.out` only. No bounce/cartoon easing.
- **Animation durations**: hover 0.25–0.45s, text reveals 0.6–1s, hero 0.9–1.4s.
- **Every section has one signature behavior** — do not animate everything uniformly.
- **Grain/noise overlay**: subtle full-page or per-section texture layer at low opacity.
- **Nav**: transparent over hero, solid after scroll threshold, fullscreen overlay on mobile.

## Build Order (highest ROI first)

1. Global CSS vars + font setup + container + nav + buttons + grain layer
2. Hero → Team dots → Services mosaic → Portfolio horizontal → Three Dots → Final CTA
3. Logo wall → Stats → Process → Founder note → Footer

## Content Reference

- Hero headline: "Make Your Brand Unskippable."
- Sub: "Community-led. Culture-smart. Performance-backed."
- Stats: 29 Projects / 55 Clients / 2,345 Content pieces / 343M Engagement / 20+ Brands
- Services (homepage): Community Marketing / Cultural Marketing / Content Marketing / Digital Marketing
- Process phases: Insight → Build → Optimize (or Strategy → Execution → Growth)
- Three Dots: Yellow = Ideas, Blue = Execution, Orange = Accountability
- Full copy is in `BloomDots Website Copy.pdf`


Requirements:
- full-width big finish
- oversized type
- dark poster-like composition
- ambient dot field or subtle motion background
- strong CTA row
- premium ending, not a plain form section

NAVIGATION
Build a clean premium nav:
- logo left
- nav right
- CTA on desktop if it fits
- mobile menu should open as a fullscreen overlay
- transparent over hero, then darkens on scroll
- subtle shrink or backdrop effect on scroll
This still respects the original nav structure from the wireframe notes. :contentReference[oaicite:18]{index=18}

GLOBAL GSAP SYSTEM
Use GSAP heavily but tastefully.

You MUST include:
- gsap.registerPlugin(ScrollTrigger)
- reusable reveal utilities
- line/word/element stagger logic
- scroll-triggered section entrances
- hover motion where helpful
- pinned horizontal portfolio
- scrubbed team convergence animation
- timeline draw animation
- ambient motion loops for hero and CTA
- performance-minded code

MOTION PHILOSOPHY
Every section should have one distinct motion identity.
Motion must feel:
- smooth
- cinematic
- premium
- deliberate
- slightly weighty
- never cartoonish

Use easing like:
- power3.out
- power4.out
- expo.out

Avoid bouncy gimmicks.

VISUAL DETAILS TO INCLUDE
- subtle grain/noise overlay
- thin divider lines where needed
- strong section labels in small uppercase
- layered depth
- muted gradients only when useful
- minimal but beautiful hover states
- poster-like composition in major sections

DO NOT
- do not make it look like a template
- do not use soft generic startup cards everywhere
- do not over-round every element
- do not overuse bright colors
- do not fill every section with equal-width boxes
- do not leave it looking like a wireframe
- do not produce a bland corporate layout
- do not skip GSAP
- do not make motion noisy for no reason

RESPONSIVENESS
- desktop first
- tablet adapted
- mobile clean and simplified
- preserve visual hierarchy on small screens
- simplify absolute/scattered motion sections on mobile when necessary

IMPLEMENTATION QUALITY
- deliver polished, cohesive code
- maintain consistent naming
- keep styles intentional
- ensure the page feels like one unified premium system
- write code as if it will be shown directly to a client

FINAL OUTPUT
Return only the final complete HTML document.
No explanation.
No markdown fences.
No notes outside the code.