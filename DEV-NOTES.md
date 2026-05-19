# BloomDots — Dev Notes (from Wireframes)

Notes extracted from the hand-drawn wireframes (Wireframes/1–9.jpeg).

---

## Section 1 — Hero / Landing (wireframe 1)
- Logo left, nav links right: Home, Team, Services, Projects
- Title text centered with 2 CTA buttons (Btn1, Btn2)
- **Background video** behind hero content
- Scroll arrow pointing to next section

---

## Section 2 — "Dots That Connected" Team (wireframe 2)
- Each dot = a **staff photo**
- **Scroll effect (vertical):** while scrolling down, they all come together
- Dots start scattered and converge on scroll

---

## Section 3 — "Local to Global" Logo Wall (wireframe 3)
- Dark/blank black screen
- **Scroll-down effect:** while scrolling down, fade-in logos one by one in random places on the screen
- Logos appear scattered at varying positions

---

## Section 4 — "Our Services" Mosaic Grid (wireframe 4)
- Services listed: SM (Social Media), Paid Media, Content, Podcast, Influencer
- **Not all containers are the same size** — irregular mosaic layout
- **Mouse-over effect:** show blurry image in background on hover
- Note: "Aditi & Maria → figure out what to put here"

---

## Section 5 — Stats / Numbers (wireframe 5)
- 29 Projects
- 55 Clients
- 2345 Content/Campaigns Delivered
- 343M Engagement/Views
- 20+ Brands
- 6th card: **(empty/placeholder)** — to be considered

---

## Section 6 — Portfolio / Case Studies (wireframe 6)
- Each card = one project
- Card layout: Work logo (top), text "What we did" + bullet points (left), images to show (right, 4–5 thumbnails)
- "Learn more" button at bottom
- **Scroll-to-side effect** — horizontal scroll between project cards
- Another portfolio card follows in same structure
- Note: "add 4–5 sections" (meaning 4–5 project cards)

---

## Section 7 — "How We Do It" Process (wireframe 7)
- 3 steps in circles connected by arrows: **Ideas → Strategy → Execution**
- Text/bullets below each step

---

## Section 8 — Founder Note (wireframe 8)
- Left: **Photo** (portrait)
- Right: "A word from Aditi" heading + paragraph text
- Bottom right: **Aditi** name + **signature**

---

## Section 9 — "Ready to Bloom?" Contact (wireframe 9)
- Heading: "Ready to Bloom?"
- **Contact Form** block below

---

## Interaction & Animation Notes (across wireframes)
| Section | Effect |
|---------|--------|
| S2 — Team | Vertical scroll: dots converge together |
| S3 — Logos | Scroll-triggered fade-in, logos appear one-by-one at random positions |
| S4 — Services | Mouse-over: blurry background image on tile hover |
| S6 — Portfolio | Horizontal scroll-to-side between project cards |


---

## Sandbox change log

- 2026-05-19 — bloomdots-global.php: replaced :root palette with tri-primary (--bloom-orange #E84E28, --bloom-blue #29B9EA, --bloom-amber #FAB72B) + 10 surface/text vars; kept --orange/--blue/--yellow as aliases pending phase 3 sweep.
- 2026-05-19 — sandbox hex-literal sweep complete: 19 JS hex literals (#f4c430/#4f7cff/#ff7a1a) → tri-primary across logos/process/services; 31 CSS var(--yellow|blue|orange) → var(--bloom-amber|blue|orange) across 8 files; legacy --yellow/--blue/--orange aliases removed from bloomdots-global.php.
- 2026-05-19 — v3 kit colors: bd_orange→#E84E28 (in place); created bd_blue #29B9EA (id cc9c8043) and bd_amber #FAB72B (id 11c6e253). System colors (secondary yellow, accent blue) left unchanged — out of plan scope, no postmeta refs.
