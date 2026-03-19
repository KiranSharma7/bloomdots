# Section 4 — Services "Live Media Wall" Design

## Summary

Section 4 is an asymmetrical mosaic grid of 5 service tiles built on a 12-column layout. Tiles default to dark typographic panels. On hover, a cursor-tracking radial spotlight reveals a stock video background behind each tile — creating a "live media wall" effect. GSAP handles diagonal clip-path entrance animations and all hover transitions.

---

## Decisions

| Decision | Choice |
|----------|--------|
| Service grouping | Tactical 5: Social Media, Paid Media, Content, Podcast, Influencer |
| Hover imagery | Stock video snippets (one per tile) |
| Layout | True mosaic — 12-col grid with alternating 7/5 col anchor tiles |
| Tile content | Medium — numbered label, service name, one-line outcome, hover arrow |
| Entrance animation | Diagonal cascade with clip-path + rotation correction |
| Overall approach | "Live Media Wall" — dark panels with cursor-spotlight video reveal |

---

## Section Header

- Label: `WHAT WE DO` — 10–11px uppercase, tracking-[0.35em], `--text-dim`
- Headline: `Services That Move Culture` — Canela, ~4rem–5rem, clip-path reveal
- Sub: `Strategy meets subculture. Execution meets outcomes.` — Satoshi, `--text-soft`

---

## Grid Layout

```
┌─────────────────────────────┬───────────────────┐
│                             │                   │
│   SOCIAL MEDIA              │   PAID MEDIA      │
│   col-span-7, row-span-2   │   col-span-5      │
│   ~420px tall               │   ~200px tall     │
│                             ├───────────────────┤
│                             │                   │
│                             │   CONTENT         │
│                             │   col-span-5      │
│                             │   ~200px tall     │
├───────────────┬─────────────┴───────────────────┤
│               │                                 │
│   PODCAST     │   INFLUENCER                    │
│   col-span-5  │   col-span-7                    │
│   ~240px tall │   ~240px tall                   │
│               │                                 │
└───────────────┴─────────────────────────────────┘
```

- Gap: `gap-3 md:gap-4`
- Border-radius: `rounded-[8px]`
- Each tile: `1px` border in `var(--line)`

---

## Tile Content Layout

```
┌──────────────────────────────────────┐
│  01                        ← numbered label, top-left
│                               10px uppercase, --text-dim
│                               tracking-[0.3em]
│                               colored with tile's accent
│
│
│  Social Media              ← service name, bottom-left
│  Turn followers into          Canela, ~1.8rem–2.5rem
│  brand advocates.             Outcome: Satoshi 13px, --text-soft
│                    Explore → ← bottom-right, hover-only
└──────────────────────────────────────┘
```

### Tile Content (5 tiles)

| # | Service | Outcome Line | Accent Color |
|---|---------|-------------|-------------|
| 01 | Social Media | Turn followers into brand advocates | `--blue` |
| 02 | Paid Media | Precision targeting, measurable ROI | `--yellow` |
| 03 | Content | Stories that stop the scroll | `--orange` |
| 04 | Podcast | Voices that build authority | `--blue` |
| 05 | Influencer | Reach the right people, authentically | `--yellow` |

---

## Visual Treatment

### Default State (No Hover)

- Background: `var(--bg-elevated)` (#17191f)
- Video in DOM but paused, `opacity: 0`
- Noise/grain overlay at 3–4% opacity
- Visible: numbered label + service name only
- Outcome line: `opacity: 0`, `translateY(8px)`
- "Explore →": `opacity: 0`, `translateX(-12px)`
- Border: `1px solid var(--line)`

### Hover State — Cursor Spotlight

1. Video activates — plays, fades to `opacity: 1` over 0.4s
2. Radial mask — CSS `radial-gradient` mask centered on cursor, ~280px soft circle. Video only visible within spotlight. Follows cursor via `mousemove`.
3. Dark overlay — `rgba(0,0,0,0.45)` over video for text readability
4. Title shifts up 4px, `power3.out`
5. Outcome line fades in, translates to position, 0.3s delay
6. "Explore →" arrow slides in from left, 0.35s delay
7. Border transitions to `var(--line-strong)`
8. Accent line — 2px line in tile's accent color grows along bottom edge L→R

### Mouse Leave

- Spotlight mask shrinks to 0 over 0.3s
- Video pauses + fades to `opacity: 0`
- Title returns to original position
- Outcome line + arrow fade out
- Accent line retracts
- All use `power3.out`

---

## GSAP Entrance Animation

### Trigger
Section top hits 75% of viewport. `once: true`.

### Phase 1 — Header (0s–0.8s)
- Label: `y: 12 → 0`, `opacity: 0→1`, 0.4s
- Headline: `clip-path: inset(100% 0 0 0) → inset(0% 0 0 0)`, 0.7s, `power4.out`
- Sub: fades in 0.2s after headline

### Phase 2 — Tile Cascade (0.4s–1.6s)

Diagonal stagger order:
1. Social Media — delay 0.4s
2. Paid Media — delay 0.55s
3. Content — delay 0.7s
4. Podcast — delay 0.85s
5. Influencer — delay 1.0s

Per tile (0.7s, `power4.out`):
- `clip-path: inset(8% 8% 8% 8%) → inset(0% 0% 0% 0%)`
- `rotation: 1.5deg → 0deg` (odd) / `-1deg → 0deg` (even)
- `opacity: 0.3 → 1`
- `scale: 0.97 → 1`

### Phase 3 — Accent Lines (1.2s–1.8s)
Thin `1px` line traces along bottom of each tile L→R, staggered.

---

## Performance

- `will-change: clip-path, transform, opacity` on entrance
- Videos paused until hover — no idle playback
- Spotlight uses CSS `mask-image` (GPU-composited)
- `ScrollTrigger` fires once

---

## Mobile Adaptation

- Single column, all tiles full-width, ~200px height
- No cursor spotlight (no hover on touch)
- Videos autoplay muted at `opacity: 0.15` with dark overlay
- Tap toggles outcome line + explore arrow
- Entrance: `y: 30` fade-in stagger, no rotation/clip-path

---

## Video Assets Needed

5 stock video clips (one per service), short loops (5–10s), dark/moody tone:
- Social Media — scrolling feeds, community content, phone screens
- Paid Media — data dashboards, analytics, performance metrics
- Content — filming/editing, cameras, creative production
- Podcast — microphones, studio, recording
- Influencer — creators filming, lifestyle content, collaboration

Videos should be compressed MP4, ~720p max, muted, looping.

---

## Insertion Point

After Section 3 (Logo Card Stack), before the spacer `<section class="h-screen">` at line 996 in `index.html`.
