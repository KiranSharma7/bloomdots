# Section 4 — Services Redesign: Rebalanced Grid + Reference Card Styling + Spotlight Hover

## Summary

Section 4 redesign addresses two problems: tiles feel empty/short, and video backgrounds aren't visible due to insufficient tile height. The solution combines a rebalanced grid with taller tiles, card styling from a reference design (glow blobs, icon boxes, structured content, rounded-2xl borders), and retains the original cursor-tracking spotlight hover that reveals video on mouseover.

---

## Decisions

| Decision | Choice |
|----------|--------|
| Grid rebalance | Bottom row from 5/7 → 6/6 even split |
| Tile heights | All increased: 200→280, 240→300, 420→480 |
| Card styling | Adopted from reference: glow blob, icon box, rounded-2xl, structured content stack |
| Video treatment | Always-visible at 12% opacity + original spotlight hover on top |
| Spotlight hover | Kept from original design — cursor-tracking radial mask |
| Description visibility | Always visible (was hover-only before) |

---

## Grid Layout

### Desktop (md+)

```
┌──────────────────────────┬──────────────────────────┐
│  SOCIAL MEDIA            │  PAID MEDIA              │
│  col-span-7, row-span-2 │  col-span-5              │
│  min-height: 480px       │  min-height: 280px       │
│                          ├──────────────────────────┤
│                          │  CONTENT                 │
│                          │  col-span-5              │
│                          │  min-height: 280px       │
├─────────────────────────┬┴──────────────────────────┤
│  PODCAST                │  INFLUENCER               │
│  col-span-6             │  col-span-6               │
│  min-height: 300px      │  min-height: 300px        │
└─────────────────────────┴───────────────────────────┘
```

### Changes from current

| Tile | Old Span | New Span | Old Height | New Height |
|------|----------|----------|------------|------------|
| Social Media | col-span-7, row-span-2 | col-span-7, row-span-2 | 420px | 480px |
| Paid Media | col-span-5 | col-span-5 | 200px | 280px |
| Content | col-span-5 | col-span-5 | 200px | 280px |
| Podcast | col-span-5 | **col-span-6** | 240px | 300px |
| Influencer | col-span-7 | **col-span-6** | 240px | 300px |

### Mobile

- Single column, all tiles `min-height: 220px` (up from 200px)
- No spotlight (no hover on touch)
- Videos autoplay at 12% opacity with no mask
- All content visible by default

---

## Tile Card Design

### Structure per tile

```
┌──────────────────────────────────────────┐
│  ◈ glow blob (accent, top-right, blur)  │
│                                          │
│  [icon]  ← accent-tinted icon box       │
│                                          │
│  01                                      │
│  Social Media                            │
│  Turn followers into brand advocates     │
│                                          │
│ ═══ VIDEO (full-tile background) ═══════ │
│ ═══ spotlight mask on hover ════════════ │
│                           Explore →      │
└──────────────────────────────────────────┘
```

### Z-index stacking (bottom to top)

1. `#0E0F11` background
2. Glow blob (absolute positioned, CSS blur, no z-index conflict)
3. Video layer + dark overlay + spotlight mask
4. Noise grain texture (3.5% opacity)
5. Content layer (icon, number, name, description, explore arrow)
6. Accent line (bottom edge)

---

## Styling Details

### Card base (new)

- Background: `#0E0F11`
- Border: `1px solid rgba(255,255,255,0.08)`
- Border-radius: `16px` (rounded-2xl, up from 8px)
- Padding: `2rem` (p-8)
- Hover border: `rgba(255,255,255,0.20)`
- Transition: `border-color 0.5s`

### Glow blob (new)

- Absolute positioned, top-right corner (`-top-24 -right-24`)
- Size: `w-48 h-48`
- Color: tile's accent color at 10% opacity
- Blur: `blur-[80px]`
- Hover: accent color at 20% opacity
- Transition: `all 0.5s`

### Icon box (new)

- Size: `w-10 h-10`
- Background: accent color at 10% opacity
- Border: accent color at 20% opacity
- Border-radius: `rounded-lg` (8px)
- Icon: 20x20 SVG stroke icon in accent color
- Margin-bottom: `1.5rem`

### Per-tile icon mapping

| Service | Accent | Icon |
|---------|--------|------|
| Social Media | `--blue` (#4f7cff) | Share/network icon |
| Paid Media | `--yellow` (#f4c430) | Target/crosshair icon |
| Content | `--orange` (#ff7a1a) | Pen/edit icon |
| Podcast | `--blue` (#4f7cff) | Microphone icon |
| Influencer | `--yellow` (#f4c430) | Star/people icon |

---

## Video Treatment

### Default state

- Videos autoplay muted looped at `opacity: 0.12`
- No mask applied — full tile coverage
- Dark overlay: `rgba(0,0,0,0.45)` on top of video
- Gives subtle living texture to every tile

### Hover state (spotlight — retained from original)

- Cursor-tracking `radial-gradient` mask: ~280px soft circle centered on cursor
- Video opacity jumps to `1` within spotlight radius
- Mask position updates via `mousemove` event
- Dark overlay remains for text readability

### Mouse leave

- Spotlight mask shrinks to 0 over 0.3s
- Video fades back to `opacity: 0.12`
- All transitions use `power3.out`

---

## Content Layout

### Default state (visible)

- Icon box (top)
- Number label: `01–05`, 10px uppercase, `tracking-[0.3em]`, accent colored
- Service name: Canela, 1.8rem (2.5rem on anchor tiles), `--text`
- Description: Satoshi, 13px, `--text-soft` — **always visible** (was hover-only)

### Hover-only

- "Explore →": slides in from left, 12px uppercase, `--text-soft`
- Accent line: 2px, accent color, grows L→R along bottom

---

## GSAP Entrance Animation

Unchanged from original design doc. Diagonal cascade with clip-path + rotation.

### Trigger

Section top hits 75% of viewport. `once: true`.

### Phase 1 — Header (0s–0.8s)

- Label: `y: 12 → 0`, `opacity: 0→1`, 0.4s
- Headline: `clip-path: inset(100% 0 0 0) → inset(0% 0 0 0)`, 0.7s, `power4.out`
- Sub: fades in 0.2s after headline

### Phase 2 — Tile Cascade (0.4s–1.6s)

Diagonal stagger: Social (0.4s) → Paid (0.55s) → Content (0.7s) → Podcast (0.85s) → Influencer (1.0s)

Per tile (0.7s, `power4.out`):
- `clip-path: inset(8% 8% 8% 8%) → inset(0% 0% 0% 0%)`
- `rotation: 1.5deg → 0deg` (odd) / `-1deg → 0deg` (even)
- `opacity: 0.3 → 1`
- `scale: 0.97 → 1`

### Phase 3 — Accent Lines (1.2s–1.8s)

Thin `1px` line traces along bottom of each tile L→R, staggered.

---

## Performance

- `will-change: clip-path, transform, opacity` on entrance (removed after animation)
- Videos always playing but small filesize (720p max, compressed MP4)
- Spotlight uses CSS `mask-image` (GPU-composited)
- Glow blobs are pure CSS blur — no JS overhead
- `ScrollTrigger` fires once

---

## Mobile Adaptation

- Single column, all tiles `min-height: 220px`
- No cursor spotlight (no hover on touch)
- Videos autoplay muted at `opacity: 0.12` with dark overlay, no mask
- All content visible (icon, number, name, description, explore arrow)
- Accent lines at full width by default
- Entrance: `y: 30` fade-in stagger, no rotation/clip-path
- Glow blobs still present but at reduced size
