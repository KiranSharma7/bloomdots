

# BloomDots — Practical Build Blueprint

## 1. Design system foundation

## 1.1 Brand feel

The build should feel like:

* dark
* editorial
* brutalist
* premium
* motion-led
* culturally sharp

The inspiration set supports that direction: WiredCo uses oversized statements, bold contrast, and project-led storytelling; Brandalism leans content-structured and editorial; Portal One brings premium restraint; We Are Social supports the culturally aware, socially fluent positioning.  ([WiredCo][1])

So the final build logic is:

**brutalist structure + premium finish + cinematic motion**

---

## 2. Color system

Use CSS variables so Tailwind and GSAP can both work cleanly with the same tokens.

## 2.1 Core palette

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

  --success-glow: rgba(79,124,255,0.16);
  --warm-glow: rgba(244,196,48,0.12);
}
```

## 2.2 Usage rules

* `--bg` for hero, logo wall, portfolio, CTA
* `--bg-soft` for section alternation
* `--bg-elevated` for overlays, menu panel, raised blocks
* `--text` for headings
* `--text-soft` for paragraph copy
* `--line` for subtle dividers
* accent colors only for:

  * active states
  * dot graphics
  * timeline markers
  * hover cues
  * numeric highlights
  * micro labels

## 2.3 Color behavior

Do not let the whole site become colorful. The copy deck already gives a strong brand anchor in the “Three Dots” logic, so color should become meaningful there instead of everywhere.  

---

## 3. Font system

Use **two fonts only**.

## 3.1 Pairing structure

### Display font

Use for:

* hero headline
* major section titles
* giant stat numbers
* case study titles
* final CTA headline

Recommended direction:

* editorial serif or sharp display sans
* high personality
* premium but not decorative

Good style references:

* Canela type mood
* PP Editorial / high-contrast serif mood
* or a brutalist grotesk if you want the whole site more aggressive

### Sans font

Use for:

* nav
* body
* labels
* buttons
* metadata
* service copy
* chips

Recommended direction:

* tight modern grotesk
* clean and slightly technical

Good style references:

* Inter Tight
* Satoshi
* General Sans
* Suisse/Neue Haas style mood

## 3.2 Font rules

* headlines: tight line-height
* labels: uppercase, tracked
* body: max readable width
* numerals: large and bold
* use display font sparingly, not everywhere

## 3.3 Suggested implementation

```js
fontFamily: {
  display: ['"Playfair Display"', 'serif'],
  sans: ['"Inter Tight"', 'sans-serif'],
}
```

If you want a more brutalist edge, swap the display font for a sharper grotesk and let size + composition do the premium work.

---

## 4. Spacing system

The site must breathe. Your current wireframe sections are good structurally, but the live build needs more pacing than the grayscale placeholders show. 

## 4.1 Section spacing

Recommended vertical rhythm:

* hero: `min-h-screen`
* major sections: `py-28 md:py-36`
* heavy visual sections: `py-32 md:py-40`
* compact supporting sections: `py-20 md:py-24`

## 4.2 Container system

```html
<div class="mx-auto w-full max-w-[1440px] px-5 sm:px-8 lg:px-12 xl:px-16">
```

## 4.3 Internal spacing

* label to heading: `mb-4`
* heading to paragraph: `mb-6` or `mb-8`
* paragraph to CTA: `mt-8`
* section intro to visual field: `mt-14 md:mt-20`

## 4.4 Grid system

Desktop:

* 12 columns

Tablet:

* 6 columns

Mobile:

* 1 column with strong spacing and clean stacking

---

## 5. Shared component rules

## 5.1 Section label

Use small uppercase micro-labels throughout:

```html
<p class="text-[11px] uppercase tracking-[0.22em] text-[var(--text-dim)]">
  Community-led / Culture-smart / Performance-backed
</p>
```

## 5.2 Heading

```html
<h2 class="font-display text-4xl leading-[0.95] sm:text-5xl lg:text-7xl text-[var(--text)]">
```

## 5.3 Body copy

```html
<p class="max-w-[42rem] text-base leading-7 text-[var(--text-soft)] md:text-lg">
```

## 5.4 Primary CTA

Harder-edged, premium, tactile:

```html
<a class="inline-flex items-center gap-3 border border-[var(--text)] bg-[var(--text)] px-6 py-3 text-sm uppercase tracking-[0.16em] text-black transition-all duration-300 hover:-translate-y-0.5">
```

## 5.5 Secondary CTA

```html
<a class="inline-flex items-center gap-3 border border-[var(--line-strong)] px-6 py-3 text-sm uppercase tracking-[0.16em] text-[var(--text)] transition-all duration-300 hover:border-[var(--text)]">
```

## 5.6 Dividers

Use hairlines, not heavy borders:

```html
<div class="h-px w-full bg-[var(--line)]"></div>
```

---

## 6. Texture and atmosphere

## 6.1 Grain layer

Add a subtle full-page or section-level grain overlay.
Use:

* low opacity
* fixed or absolute layer
* multiply/overlay feeling

## 6.2 Dot motif

The logo concept should show up as:

* subtle dot clusters
* orbit guides
* micro accent pulses
* diagrammatic circles in the Three Dots section

## 6.3 Border radius

Keep radius restrained:

* cards: `rounded-[20px]` max if needed
* premium brutalist option: `rounded-none` or `rounded-[6px]`
* buttons: slight radius only

For BloomDots, I’d stay between **6px and 16px**, not soft SaaS rounding.

---

# 7. Section behavior + GSAP animation map

The wireframe and dev notes already define the core behaviors for team dots, logo reveals, service hovers, and horizontal portfolio. This blueprint keeps those ideas but elevates them visually.   

---

## 7.1 Hero

### Purpose

Instantly establish BloomDots as a premium creative agency for cultural/community marketing.

### Content source

Use:

* “Make Your Brand Unskippable.”
* “Community-led. Culture-smart. Performance-backed.”
* proof strip with views / videos / brands 

### Layout

* fullscreen
* fixed/absolute background video
* nav overlay
* headline block center-left or centered
* proof strip below CTAs
* scroll cue at bottom

### Tailwind structure

* section: `relative min-h-screen overflow-hidden bg-[var(--bg)]`
* video layer: absolute inset
* content layer: relative z-10
* max width headline container around `max-w-[980px]`

### GSAP

#### Entrance

* nav: fade + y from `-24`
* micro-label: fade in
* headline lines: clip reveal with stagger
* paragraph: fade + y
* CTA row: fade + y
* proof chips: stagger in from below
* background video: scale from `1.08` to `1`

#### Scroll behavior

* headline slight parallax
* proof strip slight upward drift
* scroll cue loops gently

### Signature effect

Split the hero headline into lines and animate each line with a masked upward reveal.

---

## 7.2 Team — “Dots That Connect”

### Purpose

Express network intelligence and human cultural fluency.

### Content source

Wireframe/dev note explicitly says staff-photo dots scatter then converge on scroll. 

### Layout

* dark field
* one heading above or beside
* freeform constellation of circular portraits
* optional thin lines or SVG path network
* copy block anchored in one clean corner

### Tailwind structure

* outer: `relative overflow-hidden bg-[var(--bg-soft)]`
* portrait dots: absolutely positioned circle elements
* center cluster target zone
* SVG overlay for lines

### GSAP

#### Initial state

* dots placed around viewport in scattered positions
* some blurred, some sharp
* scale variation from `0.8` to `1.2`

#### ScrollTrigger

* scrubbed timeline
* dots move inward toward center cluster
* scale normalizes
* opacity equalizes
* lines draw in with SVG stroke animation
* select names/titles fade in near end

### Signature effect

As the user scrolls, the team literally becomes a connected network.

### Mobile fallback

* static circular grid
* staggered fade/scale reveal only
* no chaotic absolute field on small screens

---

## 7.3 Logo wall — “Local to Global”

### Purpose

Show credibility without a boring logo grid.

### Content source

Copy wants trust-building logos; dev notes say scattered logos appear on scroll in random positions.  

### Layout

* near-black section
* heading at top
* wide open canvas
* floating logos scattered in designed randomness

### Tailwind structure

* relative section with min height
* absolutely placed logo nodes on desktop
* clean marquee/grid fallback on mobile

### GSAP

* fade in logos one by one with stagger
* each enters from slightly different x/y offset
* blur to sharp
* optional depth parallax on scroll

### Signature effect

A constellation of client trust instead of a standard strip.

---

## 7.4 Services mosaic

### Purpose

Show BloomDots as strategic and commercially sharp.

### Content source

The copy deck recommends 2x2 visual tiles with bold titles, one-line outcomes, hover “Explore →”, and no heavy borders. The alternative service framing with Community/Cultural/Content/Digital is stronger for the homepage. 

### Layout

* asymmetrical 2x2 or 3-column broken grid
* one or two large anchor tiles
* visual background on each tile
* title + outcome + explore cue

### Tailwind structure

* grid: `grid-cols-1 md:grid-cols-12 gap-4 md:gap-6`
* tiles use mixed spans:

  * tile 1: `md:col-span-7 md:row-span-2`
  * tile 2: `md:col-span-5`
  * tile 3: `md:col-span-5`
  * tile 4: `md:col-span-7`

### Tile styling

* dark image/video overlay
* subtle gradient wash
* label pinned top
* title pinned bottom
* outcome line under title
* hover arrow slides in

### GSAP

#### On section enter

* each tile reveals with clip-path
* stagger timing from top-left to bottom-right
* slight rotation correction from `1.5deg` or `-1deg` to `0`

#### Hover

* background scale `1 -> 1.08`
* blur decreases
* title shifts up a few px
* arrow slides in
* accent line grows

### Signature effect

Tiles feel like live media panels, not simple cards.

---

## 7.5 Stats wall

### Purpose

Turn proof into a design feature.

### Content source

Stats exist in wireframes/dev notes and hero proof strip.  

### Layout

* broken grid of big numerals
* one oversized feature stat
* some stats boxed, some free-floating
* labels quieter than numbers

### Tailwind structure

* `grid-cols-1 md:grid-cols-12`
* hero stat: `md:col-span-6`
* smaller stats: `md:col-span-3`

### GSAP

* count up numbers when visible
* labels fade in after numbers begin
* small accent pulse on finish
* optional vertical line grows behind one hero stat

### Signature effect

Numbers feel like bold editorial typography, not dashboard cards.

---

## 7.6 Portfolio / case studies

### Purpose

This is the money section.

### Content source

Wireframe says horizontal scroll project cards with logo, what-we-did, bullets, visuals, and learn more. Copy deck says 3–4 hero case studies with metrics overlay.  

### Layout

Use **pinned horizontal scroll**.

Each panel:

* left: brand / challenge / services / result
* right: visual stack / thumbnails / campaign assets / metrics

### Tailwind structure

* wrapper: pinned section with overflow hidden
* inner track: `flex`
* each panel: `min-w-[100vw]`
* internal content: 12-col grid

### GSAP

* pin section
* scrub horizontal x transform
* nested content reveals per panel
* images parallax independently
* metrics chips float in stagger
* CTA arrow slides on hover

### Signature effect

The whole site pauses to let the work speak.

### Important

This section must feel slower and more cinematic than the rest.

---

## 7.7 Three Dots philosophy

### Purpose

Make the brand idea ownable.

### Content source

The copy deck clearly defines the three dots and says no card containers, with a central logo breakdown graphic and floating labels. 

### Layout

* centered large graphic
* three dots on a diagram
* labels floating around them
* microline below: Insight → Execution → Outcomes

### Tailwind structure

* centered section
* relative container
* dots absolutely positioned
* labels positioned with transform

### GSAP

* dots enter from off-screen arcs
* connecting lines draw
* labels fade/slide in
* each dot pulses subtly in idle loop
* microline wipes in last

### Signature effect

This becomes the most ownable BloomDots section after the hero.

---

## 7.8 Process section

### Purpose

Translate the methodology into a clear business process.

### Content source

Wireframe has 3 steps; copy deck has 4 strategic phases and suggests a horizontal timeline. For homepage, 3 simplified phases is cleaner.  

### Recommended homepage phases

* Insight
* Build
* Optimize

### Layout

* horizontal line
* large step numbers
* short text beneath
* active marker moves as user progresses

### Tailwind structure

* desktop row with 3 columns
* mobile stacked

### GSAP

* line draws left to right
* phase markers scale in
* text groups reveal sequentially
* active accent follows scroll progress

### Signature effect

Feels like a confident system, not a generic “how it works” block.

---

## 7.9 Founder note

### Purpose

Add intimacy and credibility.

### Content source

Wireframe includes photo, note, name, title, signature. 

### Layout

* editorial split layout
* image left
* statement right
* signature at end
* optional quote pullout

### Tailwind structure

* `grid-cols-1 md:grid-cols-12`
* image `md:col-span-5`
* text `md:col-span-7`

### GSAP

* image mask reveal
* text stagger
* signature fade or draw in
* subtle image scale settling

### Signature effect

One calm section after the more kinetic parts.

---

## 7.10 Final CTA — “Ready to Bloom?”

### Purpose

Close with force.

### Content source

Copy already gives the CTA language and intent. 

### Layout

* oversized heading
* short paragraph
* CTA row
* ambient dots or soft field in background

### Tailwind structure

* centered or offset text block
* strong whitespace
* dark background, maybe darkest on site

### GSAP

* headline reveal
* background dots drift
* CTA buttons lift on hover
* subtle final pulse or light sweep

### Signature effect

Feels like a poster ending, not a contact footer.

---

# 8. Navigation system

## 8.1 Desktop nav

* transparent on hero
* becomes solid/darker on scroll
* subtle height reduction after scroll
* active section indicator line or dot

## 8.2 Mobile nav

* fullscreen overlay
* oversized menu items
* staggered entrance
* dark background
* one accent dot or line motif
* CTA inside overlay

## 8.3 GSAP

* menu open: clip reveal or y-reveal
* nav items stagger
* background fade
* close feels fast and clean

---

# 9. Global animation rules

## 9.1 Animation categories

Use a consistent system:

### Reveal

* line reveal
* mask reveal
* fade + y

### Field motion

* dots
* logos
* particles
* labels

### Narrative scroll

* team convergence
* portfolio horizontal
* process line
* dot graphic assembly

### Hover motion

* tiles
* CTAs
* arrows
* images

### Ambient loops

* hero dots
* CTA background
* idle pulses

## 9.2 Easing

Use premium easing only.
Examples:

* `power3.out`
* `power4.out`
* `expo.out`
* custom ease for hero lines

Avoid bouncy/cartoon movement.

## 9.3 Duration rules

* micro hover: `0.25–0.45s`
* text reveals: `0.6–1s`
* hero statements: `0.9–1.4s`
* scroll scrubbed timelines: smooth, long-form

---

# 10. Build order for your demo

This is the smartest order for Claude Code:

## Phase 1 — foundation

* global color vars
* font setup
* container + spacing system
* nav
* buttons
* shared labels/headings
* grain layer

## Phase 2 — highest-impact sections

* hero
* team dots
* services mosaic
* portfolio horizontal
* Three Dots section
* final CTA

## Phase 3 — support sections

* logos
* stats
* process
* founder note
* footer

That order gives you the biggest visual payoff fastest.

---

# 11. Recommended Tailwind section classes

A clean class strategy helps Claude Code output better markup.

## Example utility conventions

* `bd-section`
* `bd-container`
* `bd-label`
* `bd-title`
* `bd-copy`
* `bd-cta-primary`
* `bd-cta-secondary`
* `bd-noise`
* `bd-grid-12`
* `bd-panel`
* `bd-dot`
* `bd-line`

Even with Tailwind, a few semantic helper classes will keep the code cleaner.

---

# 12. Final implementation stance

For BloomDots, the most important thing is this:

Do **not** build it like a normal agency template and then “add GSAP later.”

Instead, build it as:

* a motion-first editorial composition
* with dark premium surfaces
* brutalist type scale
* restrained brand color accents
* strong section identities

The copy already supports that direction:

* hero headline and positioning
* services with outcome-led framing
* visual-heavy portfolio
* Three Dots philosophy
* process methodology
* final CTA all clearly exist in the uploaded copy.    

The current wireframe already gives the right section structure and motion intentions too, especially for team convergence, logo reveal, services hover, and horizontal portfolio.   

Next best move: I’d turn this into a **Claude Code-ready master prompt** that tells it exactly how to build the full homepage in Tailwind + GSAP with this system.

[1]: https://www.wiredco.com.au/ "Multi-Award Winning Brandformance Marketing Agency | WiredCo."
