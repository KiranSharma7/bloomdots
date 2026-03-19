# Section 4 Services Redesign — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Redesign the Services section tiles with rebalanced grid, taller heights, reference card styling (glow blobs, icon boxes, rounded-2xl), always-visible video at 12% opacity, while keeping the cursor spotlight hover.

**Architecture:** All changes are in `index.html` — CSS block (lines ~535–745), HTML block (lines ~1221–1340), and JS block (lines ~1896–2056). Three tasks: CSS first, then HTML, then JS adjustments.

**Tech Stack:** Tailwind CDN classes, custom CSS, GSAP + ScrollTrigger, inline SVG icons

---

### Task 1: Update CSS — Grid, Tile Base, and New Elements

**Files:**
- Modify: `index.html:570-589` (tile base + grid spans)
- Modify: `index.html:536-541` (section background)
- Modify: `index.html:592-601` (video layer — always-visible default)
- Modify: `index.html:667-676` (outcome line — always visible)
- Modify: `index.html:720-739` (mobile overrides)
- Add new CSS rules after line 701 (glow blob, icon box)

**Step 1: Update tile base styles**

Change `index.html:570-580` from:
```css
/* Tile base */
.svc-tile {
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  border: 1px solid var(--line);
  background: var(--bg-elevated);
  cursor: pointer;
  min-height: 200px;
  will-change: clip-path, transform, opacity;
}
```
To:
```css
/* Tile base */
.svc-tile {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
  border: 1px solid rgba(255,255,255,0.08);
  background: #0E0F11;
  cursor: pointer;
  min-height: 220px;
  will-change: clip-path, transform, opacity;
  transition: border-color 0.5s;
}
```

**Step 2: Update desktop grid spans with new heights and bottom-row rebalance**

Change `index.html:582-589` from:
```css
/* Desktop grid spans */
@media (min-width: 768px) {
  .svc-tile--social    { grid-column: span 7; grid-row: span 2; min-height: 420px; }
  .svc-tile--paid      { grid-column: span 5; min-height: 200px; }
  .svc-tile--content   { grid-column: span 5; min-height: 200px; }
  .svc-tile--podcast   { grid-column: span 5; min-height: 240px; }
  .svc-tile--influencer { grid-column: span 7; min-height: 240px; }
}
```
To:
```css
/* Desktop grid spans */
@media (min-width: 768px) {
  .svc-tile--social    { grid-column: span 7; grid-row: span 2; min-height: 480px; }
  .svc-tile--paid      { grid-column: span 5; min-height: 280px; }
  .svc-tile--content   { grid-column: span 5; min-height: 280px; }
  .svc-tile--podcast   { grid-column: span 6; min-height: 300px; }
  .svc-tile--influencer { grid-column: span 6; min-height: 300px; }
}
```

**Step 3: Make video always visible at 12% opacity (remove mask by default)**

Change `index.html:592-601` from:
```css
.svc-tile__video-wrap {
  position: absolute;
  inset: 0;
  z-index: 1;
  opacity: 0;
  transition: opacity 0.4s ease;
  /* Spotlight mask — centered offscreen by default */
  -webkit-mask-image: radial-gradient(circle 0px at 50% 50%, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 100%);
  mask-image: radial-gradient(circle 0px at 50% 50%, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 100%);
}
```
To:
```css
.svc-tile__video-wrap {
  position: absolute;
  inset: 0;
  z-index: 1;
  opacity: 0.12;
  transition: opacity 0.4s ease;
  /* No mask by default — spotlight mask applied on hover via JS */
}
```

**Step 4: Make outcome line always visible on desktop**

Change `index.html:667-676` from:
```css
.svc-tile__outcome {
  font-family: 'Satoshi', sans-serif;
  font-size: 13px;
  color: var(--text-soft);
  margin-top: 0.5rem;
  opacity: 0;
  transform: translateY(8px);
  transition: opacity 0.35s ease 0.3s, transform 0.35s ease 0.3s;
}
```
To:
```css
.svc-tile__outcome {
  font-family: 'Satoshi', sans-serif;
  font-size: 13px;
  color: var(--text-soft);
  margin-top: 0.5rem;
  opacity: 1;
  transform: none;
}
```

**Step 5: Remove the hover rule for outcome (no longer needed)**

Delete `index.html:703-707`:
```css
/* Hover states */
.svc-tile:hover .svc-tile__outcome {
  opacity: 1;
  transform: translateY(0);
}
```
Replace with:
```css
/* Hover states */
```

**Step 6: Update hover border to match reference**

Change `index.html:715-717` from:
```css
.svc-tile:hover {
  border-color: var(--line-strong);
}
```
To:
```css
.svc-tile:hover {
  border-color: rgba(255,255,255,0.20);
}
```

**Step 7: Add new CSS rules for glow blob and icon box**

Insert after the accent line CSS (after line 701) and before the hover states block:

```css
/* Glow blob */
.svc-tile__glow {
  position: absolute;
  top: -6rem;
  right: -6rem;
  width: 12rem;
  height: 12rem;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.10;
  pointer-events: none;
  z-index: 0;
  transition: opacity 0.5s;
}
.svc-tile:hover .svc-tile__glow {
  opacity: 0.20;
}

/* Icon box */
.svc-tile__icon {
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.25rem;
}
.svc-tile__icon svg {
  width: 20px;
  height: 20px;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
  fill: none;
}
```

**Step 8: Update mobile video override (12% is now default, keep same)**

Change `index.html:720-725` from:
```css
@media (max-width: 767px) {
  .svc-tile__video-wrap {
    opacity: 0.15 !important;
    -webkit-mask-image: none !important;
    mask-image: none !important;
  }
```
To:
```css
@media (max-width: 767px) {
  .svc-tile__video-wrap {
    opacity: 0.12 !important;
    -webkit-mask-image: none !important;
    mask-image: none !important;
  }
```

**Step 9: Verify CSS changes in browser**

Open `index.html` in browser. At this point tiles will have wrong heights/radius but HTML not yet updated. Confirm no CSS errors in console.

**Step 10: Commit**

```bash
git add index.html
git commit -m "refactor(s4): update CSS — taller tiles, rebalanced grid, card styling, always-visible video"
```

---

### Task 2: Update HTML — Add Glow Blobs, Icon Boxes, Restructure Content

**Files:**
- Modify: `index.html:1239-1337` (all 5 tile HTML blocks)

**Step 1: Replace Tile 1 (Social Media) HTML**

Change `index.html:1239-1257` from:
```html
<!-- Tile 1: Social Media — anchor tile (col-span-7, row-span-2) -->
<div class="svc-tile svc-tile--social" data-accent="var(--blue)">
  <div class="svc-tile__video-wrap">
    <video src="videos/social-media.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <span class="svc-tile__num" style="color: var(--blue);">01</span>
    </div>
    <div>
      <h3 class="svc-tile__name">Social Media</h3>
      <p class="svc-tile__outcome">Turn followers into brand advocates</p>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--blue);"></div>
</div>
```
To:
```html
<!-- Tile 1: Social Media — anchor tile (col-span-7, row-span-2) -->
<div class="svc-tile svc-tile--social" data-accent="var(--blue)">
  <div class="svc-tile__glow" style="background: #4f7cff;"></div>
  <div class="svc-tile__video-wrap">
    <video src="videos/social-media.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <div class="svc-tile__icon" style="background: rgba(79,124,255,0.10); border: 1px solid rgba(79,124,255,0.20);">
        <svg viewBox="0 0 24 24" style="stroke: #4f7cff;"><path d="M4 12v8a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-8"/><polyline points="16 6 12 2 8 6"/><line x1="12" y1="2" x2="12" y2="15"/></svg>
      </div>
      <span class="svc-tile__num" style="color: var(--blue);">01</span>
      <h3 class="svc-tile__name">Social Media</h3>
      <p class="svc-tile__outcome">Turn followers into brand advocates</p>
    </div>
    <div>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--blue);"></div>
</div>
```

**Step 2: Replace Tile 2 (Paid Media) HTML**

Change `index.html:1259-1277` from:
```html
<!-- Tile 2: Paid Media (col-span-5) -->
<div class="svc-tile svc-tile--paid" data-accent="var(--yellow)">
  <div class="svc-tile__video-wrap">
    <video src="videos/paid-media.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <span class="svc-tile__num" style="color: var(--yellow);">02</span>
    </div>
    <div>
      <h3 class="svc-tile__name">Paid Media</h3>
      <p class="svc-tile__outcome">Precision targeting, measurable ROI</p>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--yellow);"></div>
</div>
```
To:
```html
<!-- Tile 2: Paid Media (col-span-5) -->
<div class="svc-tile svc-tile--paid" data-accent="var(--yellow)">
  <div class="svc-tile__glow" style="background: #f4c430;"></div>
  <div class="svc-tile__video-wrap">
    <video src="videos/paid-media.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <div class="svc-tile__icon" style="background: rgba(244,196,48,0.10); border: 1px solid rgba(244,196,48,0.20);">
        <svg viewBox="0 0 24 24" style="stroke: #f4c430;"><circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="6"/><circle cx="12" cy="12" r="2"/></svg>
      </div>
      <span class="svc-tile__num" style="color: var(--yellow);">02</span>
      <h3 class="svc-tile__name">Paid Media</h3>
      <p class="svc-tile__outcome">Precision targeting, measurable ROI</p>
    </div>
    <div>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--yellow);"></div>
</div>
```

**Step 3: Replace Tile 3 (Content) HTML**

Change `index.html:1279-1297` from:
```html
<!-- Tile 3: Content (col-span-5) -->
<div class="svc-tile svc-tile--content" data-accent="var(--orange)">
  <div class="svc-tile__video-wrap">
    <video src="videos/content.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <span class="svc-tile__num" style="color: var(--orange);">03</span>
    </div>
    <div>
      <h3 class="svc-tile__name">Content</h3>
      <p class="svc-tile__outcome">Stories that stop the scroll</p>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--orange);"></div>
</div>
```
To:
```html
<!-- Tile 3: Content (col-span-5) -->
<div class="svc-tile svc-tile--content" data-accent="var(--orange)">
  <div class="svc-tile__glow" style="background: #ff7a1a;"></div>
  <div class="svc-tile__video-wrap">
    <video src="videos/content.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <div class="svc-tile__icon" style="background: rgba(255,122,26,0.10); border: 1px solid rgba(255,122,26,0.20);">
        <svg viewBox="0 0 24 24" style="stroke: #ff7a1a;"><path d="M12 20h9"/><path d="M16.5 3.5a2.12 2.12 0 0 1 3 3L7 19l-4 1 1-4Z"/></svg>
      </div>
      <span class="svc-tile__num" style="color: var(--orange);">03</span>
      <h3 class="svc-tile__name">Content</h3>
      <p class="svc-tile__outcome">Stories that stop the scroll</p>
    </div>
    <div>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--orange);"></div>
</div>
```

**Step 4: Replace Tile 4 (Podcast) HTML**

Change `index.html:1299-1317` from:
```html
<!-- Tile 4: Podcast (col-span-5) -->
<div class="svc-tile svc-tile--podcast" data-accent="var(--blue)">
  <div class="svc-tile__video-wrap">
    <video src="videos/podcast.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <span class="svc-tile__num" style="color: var(--blue);">04</span>
    </div>
    <div>
      <h3 class="svc-tile__name">Podcast</h3>
      <p class="svc-tile__outcome">Voices that build authority</p>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--blue);"></div>
</div>
```
To:
```html
<!-- Tile 4: Podcast (col-span-6) -->
<div class="svc-tile svc-tile--podcast" data-accent="var(--blue)">
  <div class="svc-tile__glow" style="background: #4f7cff;"></div>
  <div class="svc-tile__video-wrap">
    <video src="videos/podcast.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <div class="svc-tile__icon" style="background: rgba(79,124,255,0.10); border: 1px solid rgba(79,124,255,0.20);">
        <svg viewBox="0 0 24 24" style="stroke: #4f7cff;"><path d="M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3Z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/><line x1="12" y1="19" x2="12" y2="22"/></svg>
      </div>
      <span class="svc-tile__num" style="color: var(--blue);">04</span>
      <h3 class="svc-tile__name">Podcast</h3>
      <p class="svc-tile__outcome">Voices that build authority</p>
    </div>
    <div>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--blue);"></div>
</div>
```

**Step 5: Replace Tile 5 (Influencer) HTML**

Change `index.html:1319-1337` from:
```html
<!-- Tile 5: Influencer — anchor tile (col-span-7) -->
<div class="svc-tile svc-tile--influencer" data-accent="var(--yellow)">
  <div class="svc-tile__video-wrap">
    <video src="videos/influencer.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <span class="svc-tile__num" style="color: var(--yellow);">05</span>
    </div>
    <div>
      <h3 class="svc-tile__name">Influencer</h3>
      <p class="svc-tile__outcome">Reach the right people, authentically</p>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--yellow);"></div>
</div>
```
To:
```html
<!-- Tile 5: Influencer (col-span-6) -->
<div class="svc-tile svc-tile--influencer" data-accent="var(--yellow)">
  <div class="svc-tile__glow" style="background: #f4c430;"></div>
  <div class="svc-tile__video-wrap">
    <video src="videos/influencer.mp4" muted loop playsinline preload="none"></video>
    <div class="svc-tile__overlay"></div>
  </div>
  <div class="svc-tile__noise"></div>
  <div class="svc-tile__content">
    <div>
      <div class="svc-tile__icon" style="background: rgba(244,196,48,0.10); border: 1px solid rgba(244,196,48,0.20);">
        <svg viewBox="0 0 24 24" style="stroke: #f4c430;"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M22 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
      </div>
      <span class="svc-tile__num" style="color: var(--yellow);">05</span>
      <h3 class="svc-tile__name">Influencer</h3>
      <p class="svc-tile__outcome">Reach the right people, authentically</p>
    </div>
    <div>
      <span class="svc-tile__explore">Explore →</span>
    </div>
  </div>
  <div class="svc-tile__accent" style="background: var(--yellow);"></div>
</div>
```

**Step 6: Verify HTML changes in browser**

Open `index.html` — confirm:
- All 5 tiles render with glow blobs visible in top-right
- Icon boxes appear with correct accent colors
- Descriptions are visible by default
- Bottom row (Podcast + Influencer) appears evenly split
- Videos show faintly at 12% opacity

**Step 7: Commit**

```bash
git add index.html
git commit -m "feat(s4): add glow blobs, icon boxes, restructure tile content HTML"
```

---

### Task 3: Update JavaScript — Video Autoplay + Spotlight Adjustments

**Files:**
- Modify: `index.html:1988-2036` (cursor spotlight hover logic)
- Modify: `index.html:2038-2054` (mobile section)

**Step 1: Update the desktop spotlight hover to work with always-visible video**

The video is now always at `opacity: 0.12`. On hover, we need to:
1. Apply the spotlight mask (video is already visible, mask reveals full opacity within radius)
2. NOT change overall video-wrap opacity to 1 (that would blast the full video visible everywhere)

Change the `mouseenter` handler in `index.html:2000-2008` from:
```js
tile.addEventListener('mouseenter', () => {
  // Play video
  video.play().catch(() => {});

  // Fade in video layer
  gsap.to(videoWrap, { opacity: 1, duration: 0.4, ease: 'power3.out' });

  // Shift title up
  gsap.to(nameEl, { y: -4, duration: 0.35, ease: 'power3.out' });
});
```
To:
```js
tile.addEventListener('mouseenter', () => {
  // Shift title up
  gsap.to(nameEl, { y: -4, duration: 0.35, ease: 'power3.out' });
});
```

The `mousemove` handler stays the same — it sets the radial mask which now controls the spotlight reveal over the always-visible video.

Change the `mouseleave` handler in `index.html:2021-2034` from:
```js
tile.addEventListener('mouseleave', () => {
  // Shrink spotlight and fade out
  gsap.to(videoWrap, { opacity: 0, duration: 0.3, ease: 'power3.out' });

  // Reset mask
  videoWrap.style.maskImage = 'radial-gradient(circle 0px at 50% 50%, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 100%)';
  videoWrap.style.webkitMaskImage = videoWrap.style.maskImage;

  // Pause video
  video.pause();

  // Reset title position
  gsap.to(nameEl, { y: 0, duration: 0.3, ease: 'power3.out' });
});
```
To:
```js
tile.addEventListener('mouseleave', () => {
  // Reset mask — removes spotlight, video returns to base 12% opacity appearance
  videoWrap.style.maskImage = '';
  videoWrap.style.webkitMaskImage = '';

  // Reset title position
  gsap.to(nameEl, { y: 0, duration: 0.3, ease: 'power3.out' });
});
```

**Step 2: Update desktop video autoplay — videos must always play now**

Insert after the `const isDesktop = window.innerWidth > 767;` line (after line 1904), before the reduced-motion check:

```js
// Autoplay all videos (always visible at 12% opacity)
tiles.forEach(tile => {
  const video = tile.querySelector('video');
  if (video) video.play().catch(() => {});
});
```

**Step 3: Remove the mobile-only autoplay block (now handled globally)**

The mobile block at `index.html:2039-2046` starts all videos. Since we now autoplay globally (Step 2), remove the duplicate:

```js
// Autoplay videos at low opacity on mobile
tiles.forEach(tile => {
  const video = tile.querySelector('video');
  if (video) {
    video.play().catch(() => {});
  }
});
```

Keep the mobile entrance animation (`gsap.from(tiles, ...)`) that follows it.

**Step 4: Verify in browser**

Open `index.html` and confirm:
- Videos play at low opacity on all tiles by default
- Hovering a tile shows the cursor spotlight revealing video at full intensity
- Moving cursor away removes spotlight cleanly, video returns to faint 12%
- Title shifts up on hover, back on leave
- Explore arrow still slides in on hover
- Accent line grows on hover
- Glow blobs intensify on hover
- Mobile: videos visible at 12%, no spotlight, fade-in entrance works

**Step 5: Commit**

```bash
git add index.html
git commit -m "fix(s4): adjust JS for always-visible video + spotlight hover compatibility"
```

---

### Visual Verification Checklist

After all 3 tasks, open `index.html` and verify:

- [ ] Grid: top row is 7/5, bottom row is 6/6 (even)
- [ ] Heights: Social ~480px, Paid/Content ~280px, Podcast/Influencer ~300px
- [ ] Border radius: all tiles have 16px rounded corners
- [ ] Glow blobs: visible in top-right of each tile, correct accent color
- [ ] Glow hover: intensifies on hover
- [ ] Icon boxes: visible in each tile, correct color + icon
- [ ] Descriptions: visible by default (not hover-only)
- [ ] Video: faintly visible at 12% across all tiles
- [ ] Spotlight: cursor spotlight reveals video on hover (desktop)
- [ ] Accent line: grows on hover, correct color
- [ ] Explore arrow: slides in on hover
- [ ] GSAP entrance: tiles cascade in diagonally on scroll
- [ ] Mobile: single column, no spotlight, videos at 12%, all content visible
- [ ] No console errors
