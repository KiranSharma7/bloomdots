# Section 3 Two-Tier Logo Showcase — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Redesign Section 3 into a two-tier logo showcase — 6 big scattered card pile (pinned scroll) + 16-logo grid with GSAP stagger entrance.

**Architecture:** Replace the current 12-card pile with 6 cards (wider spacing), then add a new logo grid section below the pinned area. All changes in a single file (`index.html`) across three zones: CSS (~line 436), HTML (~line 3053), and JS (~line 4530).

**Tech Stack:** Tailwind CSS (CDN), GSAP + ScrollTrigger, inline SVG placeholders.

---

### Task 1: Remove Cards 7–12 from HTML

**Files:**
- Modify: `index.html:3109-3143` (delete these lines)

**Step 1: Delete cards 7–12**

Remove the 6 card blocks from Card 7 (Adobe) through Card 12 (Dropbox). The `tca-scroll-card-wrapper` div should end after Card 6 (Discord, line ~3107).

Delete from `<!-- Card 7 — Adobe -->` through the closing `</div>` of Card 12 (the `</div>` on line 3143).

After deletion, the wrapper should look like:

```html
      <div class="tca-scroll-card-wrapper">

        <!-- Card 1 — Spotify -->
        ...
        <!-- Card 6 — Discord -->
        <div class="tca-scroll-card" style="z-index: 15; margin-left: -79px; margin-top: -100px; --glow: #5865F2;">
          ...
        </div>

      </div>
    </div>
  </section>
```

**Step 2: Verify visually**

Open `index.html` in browser, scroll to Section 3. Should see 6 cards animating (JS will error on missing positions for cards 7–12 but that's expected — we fix that in Task 3).

---

### Task 2: Add Logo Grid HTML Below Section 3

**Files:**
- Modify: `index.html` — insert new HTML block between the closing `</section>` of `#logo-stack` (after old line 3147) and the `<!-- SECTION 4 -->` comment.

**Step 1: Insert the logo grid section**

After the `</section>` closing tag of `#logo-stack`, insert this block:

```html
  <!-- ── Logo Grid — "& Many More" ────────────────────────── -->
  <section id="logo-grid-section" class="relative" style="background: var(--bg);">
    <div class="absolute inset-x-0 top-0 h-px" style="background: var(--line);"></div>
    <div class="mx-auto w-full max-w-[1440px] px-5 sm:px-8 lg:px-12 xl:px-16 py-20 lg:py-28">
      <p class="text-[13px] sm:text-[15px] uppercase tracking-[0.32em] font-sans font-medium mb-10 text-center" style="color: var(--text-dim);">& Many More</p>
      <div class="logo-grid">
        <!-- Row 1 -->
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><rect x="8" y="8" width="24" height="24" rx="4" stroke="currentColor" stroke-width="1.5"/><circle cx="20" cy="20" r="6" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M10 30L20 10l10 20H10z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><circle cx="20" cy="20" r="12" stroke="currentColor" stroke-width="1.5"/><path d="M14 20h12M20 14v12" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><rect x="6" y="14" width="28" height="12" rx="3" stroke="currentColor" stroke-width="1.5"/><circle cx="14" cy="20" r="3" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M8 12h24v16H8z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/><path d="M8 12l12 10 12-10" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M20 8l4 8h8l-6 5 2 9-8-5-8 5 2-9-6-5h8z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><rect x="8" y="8" width="10" height="10" rx="2" stroke="currentColor" stroke-width="1.5"/><rect x="22" y="8" width="10" height="10" rx="2" stroke="currentColor" stroke-width="1.5"/><rect x="8" y="22" width="10" height="10" rx="2" stroke="currentColor" stroke-width="1.5"/><rect x="22" y="22" width="10" height="10" rx="2" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><circle cx="20" cy="16" r="6" stroke="currentColor" stroke-width="1.5"/><path d="M10 32c0-5.5 4.5-10 10-10s10 4.5 10 10" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <!-- Row 2 -->
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M12 28V12l16 16V12" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><circle cx="20" cy="20" r="12" stroke="currentColor" stroke-width="1.5"/><path d="M16 16l8 8M24 16l-8 8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M8 20h24M20 8v24" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/><circle cx="20" cy="20" r="4" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M10 14h20v14H10z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/><path d="M16 14V10h8v4" stroke="currentColor" stroke-width="1.5"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M20 8v24M12 16l8-8 8 8M12 24l8 8 8-8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><rect x="8" y="8" width="24" height="24" rx="12" stroke="currentColor" stroke-width="1.5"/><path d="M16 20l3 3 5-6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M8 20c0-6.6 5.4-12 12-12s12 5.4 12 12" stroke="currentColor" stroke-width="1.5"/><path d="M14 20c0-3.3 2.7-6 6-6s6 2.7 6 6" stroke="currentColor" stroke-width="1.5"/><circle cx="20" cy="20" r="2" fill="currentColor"/></svg></div>
        <div class="logo-grid-item"><svg width="40" height="40" viewBox="0 0 40 40" fill="none"><path d="M12 10l8 6-8 6V10z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/><path d="M22 10l8 6-8 6V10z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/></svg></div>
      </div>
    </div>
  </section>
```

---

### Task 3: Add Logo Grid CSS

**Files:**
- Modify: `index.html:535-536` — insert new CSS rules after the `.tca-scroll-card` responsive block (after line 535 `}`) and before the `/* ── Services Section */` comment (line 537).

**Step 1: Insert the logo grid styles**

Insert between line 535 and line 537:

```css
    /* ── Logo Grid — "& Many More" ─────────────────────────── */
    .logo-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 0.75rem;
    }
    .logo-grid-item {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100px;
      border-radius: 8px;
      background: var(--surface);
      border: 1px solid var(--line);
      color: var(--text-dim);
      transition: border-color 0.3s ease, color 0.3s ease;
    }
    .logo-grid-item:hover {
      border-color: var(--line-strong);
      color: var(--text-soft);
    }
    @media (min-width: 768px) {
      .logo-grid {
        grid-template-columns: repeat(4, 1fr);
      }
      .logo-grid-item {
        height: 110px;
      }
    }
    @media (min-width: 1024px) {
      .logo-grid {
        grid-template-columns: repeat(8, 1fr);
        gap: 1rem;
      }
      .logo-grid-item {
        height: 120px;
      }
    }
```

---

### Task 4: Update Card Pile GSAP — Trim to 6 Cards

**Files:**
- Modify: `index.html:4543-4603` — replace `finalPositions`, `startRotations`, and `entryDirections` arrays.

**Step 1: Replace `finalPositions` array (lines 4543–4556)**

Replace the entire `finalPositions` array with 6 entries, wider-spaced:

```javascript
      const finalPositions = [
        { x: -380, y: -180, rot: -8  },   // Card 1 (top-left)
        { x:  380, y: -180, rot:  6  },   // Card 2 (top-right)
        { x:  400, y:   40, rot: -7  },   // Card 3 (center-right)
        { x: -400, y:   40, rot:  10 },   // Card 4 (center-left)
        { x:  280, y:  200, rot:  5  },   // Card 5 (bottom-right)
        { x: -280, y:  200, rot: -6  },   // Card 6 (bottom-left)
      ];
```

**Step 2: Replace `startRotations` array (line 4559)**

Replace with 6 entries:

```javascript
      const startRotations = [35, -40, 30, -35, 42, -28];
```

**Step 3: Replace `entryDirections` array (lines 4590–4603)**

Replace with 6 entries:

```javascript
      const entryDirections = [
        { x: 0,      y: '120vh'  },   // bottom
        { x: '-120vw', y: 0      },   // left
        { x: '120vw',  y: 0      },   // right
        { x: 0,      y: '-120vh' },   // top
        { x: '-100vw', y: '80vh' },   // bottom-left
        { x: '100vw',  y: '-80vh'},   // top-right
      ];
```

**Step 4: Verify visually**

Open in browser, scroll to Section 3. 6 cards should fly in with wider spacing and no overlapping positions.

---

### Task 5: Add Logo Grid GSAP Stagger Animation

**Files:**
- Modify: `index.html` — insert new IIFE block after the closing `})();` of the Section 3 GSAP block (after line 4627) and before the `// SECTION 4` comment (line 4629).

**Step 1: Insert the logo grid animation**

Insert this IIFE between the Section 3 and Section 4 GSAP blocks:

```javascript
    // ══════════════════════════════════════════════════════════
    // SECTION 3B — LOGO GRID STAGGER ENTRANCE
    // ══════════════════════════════════════════════════════════
    (function () {
      const gridItems = gsap.utils.toArray('.logo-grid-item');
      if (!gridItems.length) return;

      const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

      if (prefersReduced) {
        gsap.set(gridItems, { opacity: 1, y: 0, scale: 1 });
        return;
      }

      gsap.set(gridItems, { opacity: 0, y: 30, scale: 0.85 });

      gsap.to(gridItems, {
        opacity: 1,
        y: 0,
        scale: 1,
        duration: 0.6,
        stagger: 0.06,
        ease: 'power3.out',
        scrollTrigger: {
          trigger: '#logo-grid-section',
          start: 'top 80%',
          once: true,
        }
      });
    })();
```

**Step 2: Verify visually**

Open in browser, scroll past the card pile. The 16 grid tiles should wave in left-to-right, row by row with a smooth stagger.

---

### Task 6: Final Polish and Commit

**Step 1: Full scroll-through test**

Open `index.html` in browser and verify:
- Section 3 card pile: 6 cards fly in during scroll scrub, land at scattered positions with good spacing
- Card pile unpins and page scrolls naturally
- Divider line appears between card pile and logo grid
- "& Many More" label centered above grid
- 16 logo tiles stagger in with wave animation
- Grid is 8 cols on desktop, 4 on tablet, 3 on mobile
- Hover on grid items shows subtle border/color change
- `prefers-reduced-motion` shows everything immediately (test in DevTools)
- Section 4 (Services) still works correctly after the new section

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat(logos): redesign Section 3 as two-tier logo showcase

Trim card pile from 12 to 6 cards with wider spacing.
Add 16-logo grid below with GSAP stagger entrance animation."
```
