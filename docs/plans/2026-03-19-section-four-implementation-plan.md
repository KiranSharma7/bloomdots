# Section 4 — Services "Live Media Wall" Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build an asymmetrical mosaic grid of 5 service tiles with cursor-spotlight video reveals, GSAP diagonal cascade entrance, and mobile adaptation.

**Architecture:** A self-contained section inserted into `index.html` after Section 3 (Logo Card Stack). CSS goes in the existing `<style>` block (before `</style>` at line 545). HTML goes after the Section 3 closing `</section>` (line 993) and before the spacer section (line 996). GSAP script goes inside the existing `<script>` block as a new IIFE after the Section 3 IIFE.

**Tech Stack:** Tailwind CDN classes + custom CSS, GSAP 3.12 + ScrollTrigger, HTML5 `<video>`, CSS `mask-image` for spotlight effect.

---

### Task 1: Add Section 4 CSS Styles

**Files:**
- Modify: `index.html` — insert CSS before the `/* ── Selection ──` comment block (line 535)

**Step 1: Add the Services section CSS**

Insert this CSS block at line 535 (before `/* ── Selection ──`):

```css
    /* ── Services Section ──────────────────────────────────── */
    #services {
      position: relative;
      background: var(--bg);
      padding: 8rem 0;
      overflow: hidden;
    }

    .services-intro {
      position: relative;
      z-index: 2;
      padding: 0 1.25rem;
      margin-bottom: 3.5rem;
    }
    @media (min-width: 640px) { .services-intro { padding: 0 2rem; } }
    @media (min-width: 1024px) { .services-intro { padding: 0 3rem; margin-bottom: 4.5rem; } }
    @media (min-width: 1280px) { .services-intro { padding: 0 4rem; } }

    .services-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 0.75rem;
      padding: 0 1.25rem;
    }
    @media (min-width: 640px) { .services-grid { padding: 0 2rem; } }
    @media (min-width: 768px) {
      .services-grid {
        grid-template-columns: repeat(12, 1fr);
        grid-template-rows: auto auto auto;
        gap: 1rem;
        padding: 0 3rem;
      }
    }
    @media (min-width: 1280px) { .services-grid { padding: 0 4rem; } }

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

    /* Desktop grid spans */
    @media (min-width: 768px) {
      .svc-tile--social    { grid-column: span 7; grid-row: span 2; min-height: 420px; }
      .svc-tile--paid      { grid-column: span 5; min-height: 200px; }
      .svc-tile--content   { grid-column: span 5; min-height: 200px; }
      .svc-tile--podcast   { grid-column: span 5; min-height: 240px; }
      .svc-tile--influencer { grid-column: span 7; min-height: 240px; }
    }

    /* Video layer */
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
    .svc-tile__video-wrap video {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    /* Dark overlay on video */
    .svc-tile__overlay {
      position: absolute;
      inset: 0;
      background: rgba(0,0,0,0.45);
      z-index: 2;
    }

    /* Noise texture per tile */
    .svc-tile__noise {
      position: absolute;
      inset: 0;
      z-index: 3;
      pointer-events: none;
      opacity: 0.035;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
      background-repeat: repeat;
      background-size: 128px 128px;
    }

    /* Content layer */
    .svc-tile__content {
      position: relative;
      z-index: 4;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      height: 100%;
      padding: 1.5rem;
    }
    @media (min-width: 768px) {
      .svc-tile__content { padding: 2rem; }
    }

    /* Numbered label */
    .svc-tile__num {
      font-family: 'Satoshi', sans-serif;
      font-size: 10px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.3em;
    }

    /* Service name */
    .svc-tile__name {
      font-family: 'Canela', serif;
      font-size: 1.8rem;
      line-height: 1.05;
      color: var(--text);
      will-change: transform;
    }
    @media (min-width: 768px) {
      .svc-tile--social .svc-tile__name,
      .svc-tile--influencer .svc-tile__name {
        font-size: 2.5rem;
      }
    }

    /* Outcome line */
    .svc-tile__outcome {
      font-family: 'Satoshi', sans-serif;
      font-size: 13px;
      color: var(--text-soft);
      margin-top: 0.5rem;
      opacity: 0;
      transform: translateY(8px);
      transition: opacity 0.35s ease 0.3s, transform 0.35s ease 0.3s;
    }

    /* Explore arrow */
    .svc-tile__explore {
      font-family: 'Satoshi', sans-serif;
      font-size: 12px;
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      color: var(--text-soft);
      align-self: flex-end;
      opacity: 0;
      transform: translateX(-12px);
      transition: opacity 0.3s ease 0.35s, transform 0.3s ease 0.35s;
    }

    /* Accent line at bottom */
    .svc-tile__accent {
      position: absolute;
      bottom: 0;
      left: 0;
      height: 2px;
      width: 0;
      z-index: 5;
      transition: width 0.5s cubic-bezier(0.16, 1, 0.3, 1);
    }

    /* Hover states */
    .svc-tile:hover .svc-tile__outcome {
      opacity: 1;
      transform: translateY(0);
    }
    .svc-tile:hover .svc-tile__explore {
      opacity: 1;
      transform: translateX(0);
    }
    .svc-tile:hover .svc-tile__accent {
      width: 100%;
    }
    .svc-tile:hover {
      border-color: var(--line-strong);
    }

    /* Mobile: videos at low opacity always */
    @media (max-width: 767px) {
      .svc-tile__video-wrap {
        opacity: 0.15 !important;
        -webkit-mask-image: none !important;
        mask-image: none !important;
      }
      .svc-tile__outcome {
        opacity: 1;
        transform: none;
        transition: none;
      }
      .svc-tile__explore {
        opacity: 1;
        transform: none;
        transition: none;
      }
      .svc-tile__accent {
        width: 100% !important;
        transition: none;
      }
      .services-intro {
        margin-bottom: 2rem;
      }
      #services {
        padding: 5rem 0;
      }
    }

    /* Reduced motion */
    @media (prefers-reduced-motion: reduce) {
      .svc-tile {
        will-change: auto !important;
      }
      .svc-tile__video-wrap {
        transition: none !important;
      }
    }
```

**Step 2: Verify the CSS was inserted correctly**

Visually confirm the CSS block sits between the Logo Card Stack styles and the `::selection` rule.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat(s4): add Services Live Media Wall CSS styles"
```

---

### Task 2: Add Section 4 HTML Structure

**Files:**
- Modify: `index.html` — insert HTML after Section 3's closing `</section>` tag (line 993) and before the spacer `<section class="h-screen">` (line 996)

**Step 1: Add the section HTML**

Insert this block between line 993 and line 996:

```html
  <!-- ═══════════════════════════════════════════════════════
       SECTION 4 — SERVICES "LIVE MEDIA WALL"
       ═══════════════════════════════════════════════════════ -->
  <section id="services">
    <!-- Top divider -->
    <div class="absolute inset-x-0 top-0 h-px" style="background: var(--line);"></div>

    <!-- Section intro -->
    <div class="services-intro">
      <span class="svc-label block text-[10px] uppercase tracking-[0.35em] font-medium mb-3" style="color: var(--text-dim);">What We Do</span>
      <h2 class="svc-headline text-4xl md:text-5xl lg:text-[4rem] leading-[0.93] tracking-tight font-instrument-serif" style="clip-path: inset(100% 0 0 0);">
        Services That<br class="hidden sm:inline"> Move Culture
      </h2>
      <p class="svc-sub text-sm md:text-[0.92rem] leading-relaxed max-w-[36rem] mt-4" style="color: var(--text-soft); opacity: 0;">
        Strategy meets subculture. Execution meets outcomes.
      </p>
    </div>

    <!-- Mosaic Grid -->
    <div class="services-grid">

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

    </div>
  </section>
```

**Step 2: Create placeholder video directory**

```bash
mkdir -p videos
```

Note: Stock videos need to be sourced separately. The section will display the dark elevated panels without videos — the design degrades gracefully since tiles default to `--bg-elevated` with text visible.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat(s4): add Services Live Media Wall HTML structure"
```

---

### Task 3: Add GSAP Entrance Animation

**Files:**
- Modify: `index.html` — add GSAP code inside the `<script>` block, after the Section 3 IIFE (find the closing `})();` of the logo stack IIFE, insert after it)

**Step 1: Add the GSAP entrance animation IIFE**

Insert this script block after the Section 3 IIFE closing:

```javascript
    // ══════════════════════════════════════════════════════════
    // SECTION 4 — SERVICES "LIVE MEDIA WALL"
    // ══════════════════════════════════════════════════════════
    (function () {
      const section = document.getElementById('services');
      if (!section) return;

      const tiles = gsap.utils.toArray('.svc-tile');
      if (!tiles.length) return;

      const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
      const isDesktop = window.innerWidth > 767;

      // ── Reduced Motion: show everything immediately ──
      if (prefersReduced) {
        gsap.set('.svc-headline', { clipPath: 'inset(0% 0 0 0)' });
        gsap.set('.svc-sub', { opacity: 1 });
        gsap.set(tiles, { clipPath: 'inset(0% 0% 0% 0%)', opacity: 1, rotation: 0, scale: 1 });
        return;
      }

      // ── Header Reveal ──
      gsap.from('.svc-label', {
        opacity: 0, y: 12,
        duration: 0.4, ease: 'power3.out',
        scrollTrigger: { trigger: '#services', start: 'top 75%' }
      });

      gsap.to('.svc-headline', {
        clipPath: 'inset(0% 0 0 0)',
        duration: 0.7, ease: 'power4.out',
        scrollTrigger: { trigger: '#services', start: 'top 75%' }
      });

      gsap.to('.svc-sub', {
        opacity: 1,
        duration: 0.6, ease: 'power3.out',
        scrollTrigger: { trigger: '#services', start: 'top 68%' }
      });

      // ── Tile Cascade — diagonal stagger ──
      // Set initial states
      tiles.forEach((tile, i) => {
        const rot = i % 2 === 0 ? 1.5 : -1;
        gsap.set(tile, {
          clipPath: 'inset(8% 8% 8% 8%)',
          opacity: 0.3,
          rotation: rot,
          scale: 0.97,
        });
      });

      // Stagger delays: top-left to bottom-right
      const staggerDelays = [0, 0.15, 0.3, 0.45, 0.6];

      tiles.forEach((tile, i) => {
        gsap.to(tile, {
          clipPath: 'inset(0% 0% 0% 0%)',
          opacity: 1,
          rotation: 0,
          scale: 1,
          duration: 0.7,
          ease: 'power4.out',
          scrollTrigger: {
            trigger: '#services',
            start: 'top 65%',
            once: true,
          },
          delay: staggerDelays[i] || 0,
        });
      });

      // ── Phase 3: Accent line trace on entrance ──
      const accents = gsap.utils.toArray('.svc-tile__accent');
      accents.forEach((line, i) => {
        gsap.fromTo(line,
          { width: '0%' },
          {
            width: '30%',
            duration: 0.6,
            ease: 'power3.out',
            scrollTrigger: {
              trigger: '#services',
              start: 'top 55%',
              once: true,
            },
            delay: 0.8 + i * 0.12,
            onComplete: () => {
              // Reset to 0 so hover can take over
              gsap.to(line, { width: '0%', duration: 0.4, ease: 'power3.in' });
            }
          }
        );
      });

      // ── Cursor Spotlight Hover (desktop only) ──
      if (isDesktop) {
        tiles.forEach(tile => {
          const videoWrap = tile.querySelector('.svc-tile__video-wrap');
          const video = tile.querySelector('video');
          const nameEl = tile.querySelector('.svc-tile__name');

          if (!videoWrap || !video) return;

          // Spotlight size
          const spotSize = 280;

          tile.addEventListener('mouseenter', () => {
            // Play video
            video.play().catch(() => {});

            // Fade in video layer
            gsap.to(videoWrap, { opacity: 1, duration: 0.4, ease: 'power3.out' });

            // Shift title up
            gsap.to(nameEl, { y: -4, duration: 0.35, ease: 'power3.out' });
          });

          tile.addEventListener('mousemove', (e) => {
            const rect = tile.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;

            // Update radial mask position
            videoWrap.style.maskImage = `radial-gradient(circle ${spotSize}px at ${x}px ${y}px, rgba(0,0,0,1) 0%, rgba(0,0,0,0.6) 40%, rgba(0,0,0,0) 100%)`;
            videoWrap.style.webkitMaskImage = videoWrap.style.maskImage;
          });

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
        });
      }

      // ── Mobile: Tap Toggle ──
      if (!isDesktop) {
        // Autoplay videos at low opacity on mobile
        tiles.forEach(tile => {
          const video = tile.querySelector('video');
          if (video) {
            video.play().catch(() => {});
          }
        });

        // Simple fade-in entrance for mobile
        gsap.from(tiles, {
          opacity: 0, y: 30,
          duration: 0.5, stagger: 0.08, ease: 'power3.out',
          scrollTrigger: { trigger: '#services', start: 'top 80%' }
        });
      }

    })();
```

**Step 2: Verify the script is placed correctly**

Confirm it sits after the Section 3 IIFE and before the closing `</script>` tag.

**Step 3: Open in browser and test**

- Check that tiles appear on scroll with the diagonal cascade
- Verify hover spotlight works (will show dark panels without video files)
- Test mobile layout stacks correctly

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat(s4): add GSAP entrance animation and cursor spotlight"
```

---

### Task 4: Source and Add Placeholder Videos

**Files:**
- Create: `videos/` directory with 5 MP4 files

**Step 1: Create the videos directory if not already done**

```bash
mkdir -p videos
```

**Step 2: Source stock videos**

You need 5 short loop videos (5–10s, dark/moody, 720p, compressed MP4):

| File | Subject |
|------|---------|
| `videos/social-media.mp4` | Scrolling feeds, community content, phone screens |
| `videos/paid-media.mp4` | Data dashboards, analytics, performance metrics |
| `videos/content.mp4` | Filming/editing, cameras, creative production |
| `videos/podcast.mp4` | Microphones, studio, recording |
| `videos/influencer.mp4` | Creators filming, lifestyle content |

Sources: Pexels, Pixabay, Coverr (all free for commercial use).

**Note:** The section works without videos — tiles display as dark panels with text. Videos are an enhancement layer. This task can be done asynchronously.

**Step 3: After adding videos, commit**

```bash
git add videos/
git commit -m "feat(s4): add stock video assets for service tiles"
```

---

### Task 5: Visual Polish and Final Adjustments

**Files:**
- Modify: `index.html` — CSS and GSAP tweaks as needed

**Step 1: Test the full section in desktop Chrome**

Check for:
- Grid layout matches the mosaic diagram (7/5, 5/5, 5/7 spans)
- Tile heights feel balanced (anchor tiles taller than standard tiles)
- Entrance animation plays smoothly at scroll trigger point
- Hover spotlight reveals video correctly with the radial mask
- Outcome line and Explore arrow fade in on hover
- Accent line grows along bottom on hover
- Border transitions to `--line-strong` on hover

**Step 2: Test mobile layout (Chrome DevTools responsive mode)**

Check for:
- All tiles stack to single column at full width
- Videos play at low opacity (0.15) as ambient background
- Outcome line and Explore arrow are always visible
- Accent lines are always visible
- Font sizes are readable
- Spacing feels right (no cramped tiles)

**Step 3: Test scroll continuity**

Scroll through the full page to confirm:
- Section 3 → Section 4 transition feels natural
- No jarring jumps or layout shifts
- Section 4 → spacer/next section transition is clean

**Step 4: Adjust any values that feel off**

Common tweaks:
- Tile `min-height` values (if tiles feel too short/tall)
- Spotlight `spotSize` (if reveal circle feels too small/large)
- Entrance stagger timing (if animation feels too fast/slow)
- Mobile tile height (if content gets cramped)

**Step 5: Final commit**

```bash
git add index.html
git commit -m "feat(s4): polish Services Live Media Wall section"
```

---

## Implementation Notes

**Existing patterns to follow (from index.html):**
- Section comments use `═══` box style (see lines 899, 999)
- GSAP code is wrapped in IIFEs: `(function () { ... })();`
- ScrollTrigger patterns: `trigger`, `start`, `end`, `scrub`, `pin`, `once`
- CSS classes use BEM-like naming within sections (e.g., `.team-dot`, `.dot-circle`, `.dot-label`)
- Responsive breakpoints: 640px (sm), 768px (md), 1024px (lg), 1280px (xl)
- Section intros follow pattern: label → headline (clip-path) → sub (opacity)
- `will-change` is declared in CSS, not inline
- `prefers-reduced-motion` is checked at the top of each IIFE

**Video `preload="none"`:** Videos use `preload="none"` so they don't load until hover. On mobile where they autoplay, the browser will lazily load them.

**CSS class collision note:** The tile modifier class `.svc-tile--content` shares a word with the inner `.svc-tile__content` element class. They are distinct selectors (one is a modifier on the tile, one is a BEM element) and won't collide, but be aware during debugging.
