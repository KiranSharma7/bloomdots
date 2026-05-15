---
name: Bloomdots Design System
description: Make Your Brand Unskippable — a creative content agency system built on warmth, energy, and conviction.
colors:
  bloom-orange: "#E84E28"
  bloom-orange-hover: "#D1401C"
  bloom-orange-press: "#B23516"
  bloom-blue: "#29B9EA"
  bloom-blue-hover: "#1AA3D4"
  bloom-amber: "#FAB72B"
  neutral-white: "#FFFFFF"
  neutral-surface: "#F7F7F7"
  neutral-raised: "#EFEFEF"
  neutral-border: "#E2E2E2"
  neutral-border-strong: "#CBCBCB"
  neutral-fg: "#1A1A1A"
  neutral-fg-2: "#444444"
  neutral-fg-3: "#888888"
  neutral-fg-disabled: "#ABABAB"
  status-success: "#1B9E5B"
  status-warning: "#E09F14"
  status-error: "#D0291C"
  status-info: "#1AA3D4"
  dark-bg: "#111111"
  dark-surface: "#1A1A1A"
  dark-raised: "#242424"
typography:
  display:
    fontFamily: "'Canela', serif"
    fontSize: "4.768rem"
    fontWeight: 900
    lineHeight: 1.1
    letterSpacing: "-0.02em"
  headline:
    fontFamily: "'Satoshi', sans-serif"
    fontSize: "3.815rem"
    fontWeight: 700
    lineHeight: 1.1
    letterSpacing: "-0.01em"
  title:
    fontFamily: "'Satoshi', sans-serif"
    fontSize: "2.441rem"
    fontWeight: 700
    lineHeight: 1.25
    letterSpacing: "-0.01em"
  body:
    fontFamily: "'Satoshi', sans-serif"
    fontSize: "1rem"
    fontWeight: 400
    lineHeight: 1.65
    letterSpacing: "0"
  label:
    fontFamily: "'Satoshi', sans-serif"
    fontSize: "0.8rem"
    fontWeight: 500
    lineHeight: "1"
    letterSpacing: "0.04em"
  overline:
    fontFamily: "'Satoshi', sans-serif"
    fontSize: "0.64rem"
    fontWeight: 700
    lineHeight: "1"
    letterSpacing: "0.12em"
rounded:
  sm: "4px"
  md: "8px"
  lg: "12px"
  xl: "16px"
  2xl: "24px"
  pill: "999px"
  full: "50%"
spacing:
  1: "4px"
  2: "8px"
  3: "12px"
  4: "16px"
  6: "24px"
  8: "32px"
  12: "48px"
  16: "64px"
  20: "80px"
  24: "96px"
  32: "128px"
components:
  button-primary:
    backgroundColor: "{colors.bloom-orange}"
    textColor: "{colors.neutral-white}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  button-primary-hover:
    backgroundColor: "{colors.bloom-orange-hover}"
    textColor: "{colors.neutral-white}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  button-secondary:
    backgroundColor: "{colors.bloom-blue}"
    textColor: "{colors.neutral-white}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  button-amber:
    backgroundColor: "{colors.bloom-amber}"
    textColor: "{colors.neutral-fg}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  button-outline:
    backgroundColor: "transparent"
    textColor: "{colors.bloom-orange}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  button-ghost:
    backgroundColor: "transparent"
    textColor: "{colors.neutral-fg}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  button-dark:
    backgroundColor: "{colors.neutral-fg}"
    textColor: "{colors.neutral-white}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  button-disabled:
    backgroundColor: "{colors.neutral-raised}"
    textColor: "{colors.neutral-fg-disabled}"
    rounded: "{rounded.md}"
    padding: "10px 20px"
  badge-orange:
    backgroundColor: "#FDF0EC"
    textColor: "{colors.bloom-orange-press}"
    rounded: "{rounded.pill}"
    padding: "3px 10px"
  badge-blue:
    backgroundColor: "#E8F7FD"
    textColor: "{colors.bloom-blue-hover}"
    rounded: "{rounded.pill}"
    padding: "3px 10px"
  badge-amber:
    backgroundColor: "#FEF9EC"
    textColor: "#966809"
    rounded: "{rounded.pill}"
    padding: "3px 10px"
  chip-default:
    backgroundColor: "{colors.neutral-white}"
    textColor: "{colors.neutral-fg}"
    rounded: "{rounded.md}"
    padding: "5px 12px"
  chip-selected:
    backgroundColor: "{colors.bloom-orange}"
    textColor: "{colors.neutral-white}"
    rounded: "{rounded.md}"
    padding: "5px 12px"
---

# Design System: Bloomdots

## 1. Overview

**Creative North Star: "The Vivid Collaborator"**

Bloomdots is not a broadcaster who shouts. It is the creative partner that stands next to the brand and helps it speak with a voice it did not know it had. Warmth and momentum are the twin poles: every surface should feel alive without feeling loud, confident without arrogance, kinetic without chaos. The system earns attention through colour conviction and typographic contrast, then holds it with honest, direct craft.

The palette is a tri-primary: Bloom Orange carries heat and cultural sharpness, Bloom Blue carries structure and trust, Bloom Amber carries optimism and spotlight. The three are co-equal; none is the default. Each section picks the brand colour that fits its job, and the page rotates through all three rather than leaning on one. Backgrounds stay clean so the brand colours carry all the weight. The Canela/Satoshi pairing creates editorial lift: high-contrast serif headlines feel like a magazine cover, while Satoshi's geometric legibility handles every UI need. Together they say "this agency has taste" before a single word is read.

This system explicitly refuses the following: gradient text decorations, glassmorphism panels, identical card grids where every tile carries the same icon-heading-body pattern, hero-metric templates (big number, small label, gradient accent), and the generic SaaS landing page vocabulary. Bloomdots work is visible, differentiated, and specific.

**Key Characteristics:**
- Three co-equal brand primaries: Orange, Blue, Amber. None is the default; each section picks the one that fits its job.
- Editorial serif (Canela) reserved for display-level moments. Satoshi handles everything else.
- Flat at rest, lifted on hover. Depth is earned through interaction, not decoration.
- Brand colours used as full-bleed surface backgrounds at hero scale, never as partial overlays or gradients.
- Motion is confident and clean. Fade up, ease out, no spring physics.

## 2. Colors: The Bloomdots Palette

Three co-equal brand primaries derived from the logomark; a clean neutral scale beneath them. No colour ranks above the others. Each owns a register, and the surface in question chooses which register to invoke.

### Bloom Orange — Heat
- **Bloom Orange** (`#E84E28`): The brand's heat. Used when a surface should feel kinetic, culturally sharp, urgent, or alive: campaign hero panels, marquee CTAs, content where energy is the point.
- **Bloom Orange Hover** (`#D1401C`): Hover state for orange interactive surfaces. 10% darker.
- **Bloom Orange Press** (`#B23516`): Active/press state. Immediate, no transition needed.

### Bloom Blue — Structure
- **Bloom Blue** (`#29B9EA`): The brand's structure. Used when a surface should feel grounded, considered, trustworthy, or focused: process sections, form fields and focus rings, structural CTAs, callouts where calm clarity is the point. Carries equal weight to Orange as a full-bleed surface choice.

### Bloom Amber — Spotlight
- **Bloom Amber** (`#FAB72B`): The brand's spotlight. Used when a surface should feel optimistic, headline-worthy, or punctuating: feature highlights, amber-button variants, full-bleed campaign moments where warmth without heat is the point. Carries equal weight to Orange and Blue as a full-bleed surface choice.

### Neutral
- **Near-White Canvas** (`#FFFFFF`): Primary page background, light theme.
- **Ash Surface** (`#F7F7F7`): Surface-level containers, light-theme card backgrounds.
- **Mist Raised** (`#EFEFEF`): Raised backgrounds, disabled button fills.
- **Stone Border** (`#E2E2E2`): Default borders. Inputs at rest.
- **Graphite Border** (`#CBCBCB`): Strong borders, dividers where Stone Border lacks contrast.
- **Rich Ink** (`#1A1A1A`): Primary foreground text, dark-button backgrounds, dark-card backgrounds.
- **Warm Slate** (`#444444`): Secondary foreground (fg-2 role). Subheadings, secondary labels.
- **Cool Pewter** (`#888888`): Tertiary foreground (fg-3 role). Supporting body on cards, meta text.
- **Stone Disabled** (`#ABABAB`): Disabled text and icons.

### Named Rules
**The Tri-Primary Rule.** One brand colour leads per surface, not per brand. The page should rotate through Orange, Blue, and Amber across its sections; any single screen should not lean on the same brand colour for every accent. Frequency is each colour's power: a section drenched in one of them earns conviction; a page that repeats one of them everywhere dilutes all three.

**The Single-Lead Rule.** Within one surface (a section, a card, a hero), one brand colour dominates and the other two appear at most as small accents (overline, icon, focus ring). Mixing all three at equal weight inside one element reads as noise.

**The No-Gradient Rule.** The three brand colours appear as solid fills, never as gradients. Gradient overlays on photographic images (for text protection) are permitted; gradient decorations on any UI surface are prohibited.

## 3. Typography: The Canela–Satoshi Pairing

**Display Font:** Canela (serif, with Georgia, serif fallback)
**Body + UI Font:** Satoshi (sans-serif, with system-ui, sans-serif fallback)
**Mono Font:** JetBrains Mono (technical use only, Google Fonts CDN)

**Character:** Canela brings the editorial authority of a well-designed magazine. Its high contrast stroke and slightly condensed proportions create immediate visual weight at display scale. Satoshi answers with geometric clarity and warmth — a modern sans that never feels cold. The contrast between them is deliberate: serif for impression, sans for function.

### Hierarchy

- **Display** (Canela Black 900, 4.768rem/~76px, lh 1.1, ls –0.02em): Hero-level text only. Page titles, campaign headlines. One per screen.
- **Headline / H1** (Satoshi Bold 700, 3.815rem/~61px, lh 1.1, ls –0.01em): Section-opening statements. Above the fold on interior pages.
- **Title / H2** (Satoshi Bold 700, 3.052rem/~49px, lh 1.25, ls –0.01em): Section headers, feature names.
- **Subhead / H3** (Satoshi Semibold 700, 2.441rem/~39px, lh 1.25, ls –0.01em): Card titles, sub-section headings.
- **Subtitle / H4** (Satoshi Semibold 700, 1.953rem/~31px, lh 1.5, ls 0): Tertiary headings, callout titles.
- **Lead** (Satoshi Regular 400, 1.25rem/20px, lh 1.65): Intro paragraphs. First paragraph under a hero heading.
- **Body** (Satoshi Regular 400, 1rem/16px, lh 1.65, max 70ch): All prose. Max line length 65–75ch.
- **Small / Caption** (Satoshi Regular 400, 0.8rem/~13px, lh 1.5): Supporting metadata, captions, timestamps.
- **Label** (Satoshi Medium 500, 0.8rem/~13px, lh 1, ls 0.04em, uppercase): UI element labels, button text, nav items.
- **Overline** (Satoshi Bold 700, 0.64rem/~10px, lh 1, ls 0.12em, uppercase): Category labels above card titles and section headings.

### Named Rules
**The Canela Ceiling Rule.** Canela is Display only. Never use it for body text, labels, or anything below H1. Diluting it across the hierarchy destroys its editorial impact.

**The Scale Ratio Rule.** The type scale runs on a major-third (1.25x) progression. Do not introduce off-scale sizes. Every size step should feel like a deliberate step up, not an inch.

## 4. Elevation

Bloomdots surfaces are flat by default. At rest, cards and panels sit on the canvas without shadow; depth is implied through background colour shifts (white → ash surface → mist raised). Shadows appear as interaction feedback, not structural decoration. A shadow means "this element has moved."

### Shadow Vocabulary

- **Shadow SM** (`0 1px 4px rgba(0,0,0,0.07)`): Subtle lift for small UI controls (dropdowns, tooltips).
- **Shadow MD** (`0 2px 12px rgba(0,0,0,0.09)`): Card hover state, modal surfaces, floating panels.
- **Shadow LG** (`0 8px 32px rgba(0,0,0,0.13)`): Lifted card (hover + translateY(−2px)), drawers, sticky headers with scroll.
- **Shadow XL** (`0 20px 60px rgba(0,0,0,0.18)`): Full-screen overlays, feature spotlight moments.

Dark-theme shadow values use higher opacity (0.25–0.55) at the same scale steps because ambient light absorption is different on near-black surfaces.

### Named Rules
**The Flat-by-Default Rule.** No shadow at rest. Shadow is a state indicator. If an element always has a shadow and never changes, the shadow is decoration. Remove it.

## 5. Components

### Buttons
Tactile and direct. Buttons have visible weight through colour and padding; they respond to touch with immediate colour deepening and a 0.97 scale press.

- **Shape:** Softly rounded (8px radius, `--radius-md`). Pill variant (999px) for marketing CTAs.
- **Orange variant:** Bloom Orange fill (`#E84E28`), white text. Padding 10px 20px (md), 13px 28px (lg), 6px 14px (sm). Font: Satoshi Bold 700 (Label style), uppercase text optional for hero CTAs. Hover: `#D1401C`, `transform: translateY(−1px)`. Press: `#B23516`, `scale(0.97)`.
- **Blue variant:** Bloom Blue fill (`#29B9EA`), white text. Same shape and size logic. Hover: `#1AA3D4`.
- **Amber variant:** Bloom Amber fill (`#FAB72B`), Rich Ink text (`#1A1A1A`). Same shape and size logic.
- The three variants are interchangeable as primary actions; the choice follows the section's register (Heat / Structure / Spotlight), not a fixed default.
- **Outline:** Transparent fill, 2px border in the section's brand colour, matching text. Hover: solid brand fill, contrasting text.
- **Ghost:** Transparent fill, 2px Stone Border (`#E2E2E2`), Rich Ink text. Secondary action on light surfaces.
- **Dark:** Rich Ink fill (`#1A1A1A`), white text. For use on light or coloured backgrounds.
- **Disabled:** Mist Raised fill (`#EFEFEF`), Stone Disabled text (`#ABABAB`). `cursor: not-allowed`.

### Badges and Chips
- **Status Badges:** Pill shape (999px). Tinted background from the brand palette with matching deep-hue text. Each badge carries a 6×6px dot indicator for status-oriented use (Active, Pending, Delivered). Variants: orange-tint, blue-tint, amber-tint, green-tint, neutral-tint, dark.
- **Outline Badges:** 1.5px solid border, matching text, transparent fill. For category/tag labeling without status weight.
- **Filter Chips:** 8px radius. White background, Stone Border, Rich Ink text at rest. Selected state flips to a brand colour fill (Orange, Blue, or Amber) matching the surrounding section's register. Interactive; `cursor: pointer`.

### Cards
- **Shape:** 12px radius (`--radius-lg`). Consistent across all card variants.
- **Default (Light):** White background (`#FFFFFF`), Shadow MD at rest. On hover: Shadow LG + `transform: translateY(−2px)`, `transition: 0.2s ease-out`.
- **Coloured Variants:** Full Bloom Orange, Bloom Blue, or Rich Ink fill. Text and CTA colours shift to maintain contrast (white text on Orange/Blue/Dark; Amber CTA text on Orange dark surfaces).
- **Overline:** any of the three brand colours, chosen to match the card's register (Orange on cards that should feel kinetic, Blue on structural/process cards, Amber on dark-card or spotlight contexts). Style: Satoshi Bold 700, 10px, 0.1em tracking, uppercase.
- **Internal Padding:** 20–24px (`--space-5` to `--space-6`).
- **Border:** None. Shadow and colour do the separation work.

**The Card Colour Rule.** Coloured card variants (orange, blue, dark) are used for emphasis, not repetition. A row of identical orange cards is the same visual noise as a row of identical white cards. Vary the surface; use colour to direct attention to one.

### Inputs and Form Fields
- **Style:** 1.5px Stone Border at rest, 8px radius, white background. Satoshi Regular 400, 13px.
- **Focus:** Border shifts to Bloom Blue (`#29B9EA`) + `box-shadow: 0 0 0 3px rgba(41,185,234,0.15)`. Clean focus glow derived from the secondary brand colour.
- **Error:** Border shifts to Status Error (`#D0291C`). Error message in same red, 10–11px, below the field.
- **Success:** Border shifts to Status Success (`#1B9E5B`).
- **Placeholder:** Stone Disabled colour (`#ABABAB`).
- **Select:** Custom chevron icon (stroke `#888`), `padding-right: 32px`, `appearance: none`.
- **Textarea:** No horizontal resize (`resize: none`). Height determined by context (min 64px).

### Navigation
- Font: Satoshi Label style (medium-weight, tracking, uppercase or sentence-case per implementation). Default colour: Rich Ink or fg-2. Hover and active: a brand colour (Orange, Blue, or Amber) chosen per surface; the choice is consistent within a single navigation context.
- Logo minimum size 32px; always on a white or light background in light theme; white/inverted treatment on dark or coloured backgrounds.
- Mobile: collapse to a drawer or stacked list. The three-dot brand mark functions as a natural menu indicator on mobile.

### Signature Component: The Brand Dot Motif
The Bloomdots logomark (three teardrop dots forming a stylized B) is the system's visual icon. Large decorative dot/circle shapes in brand colours can appear as background elements at low opacity (10–20%) to add energy to section breaks, hero backgrounds, and campaign moments. Use sparingly: one per section maximum. Never overlap readable text with a dot shape.

## 6. Do's and Don'ts

### Do:
- **Do** pick one brand colour per surface to lead its CTAs and accents, drawn from Orange, Blue, or Amber based on the section's register. Rotate the lead colour across sections so the page travels through all three.
- **Do** use Canela display type at full scale (76px+) for hero headlines. Its contrast is lost below 48px.
- **Do** apply full-bleed Bloom Orange, Bloom Blue, or Rich Ink backgrounds to hero and callout sections. Brand colour as architecture is the system's most distinctive move.
- **Do** keep body copy within 65–75ch. Bloomdots content is direct and readable; long lines undermine both.
- **Do** use Shadow MD/LG only on hover or interactive states. Flat at rest.
- **Do** use Bloom Amber as a full-bleed surface on equal footing with Orange and Blue. It is not reserved for accents; an entire section can lead with Amber when the register calls for spotlight or optimism.
- **Do** write CTAs in all caps for primary buttons (`GET STARTED`, `SEE WORK`). Satoshi's tracking at label weight makes uppercase readable and confident.
- **Do** use the dot motif (low-opacity circles/teardrops) as background decoration in hero sections. It ties back to the logomark and adds brand texture without competing with content.
- **Do** use sentence case for all display headlines. The brand voice is direct and conversational, not formal.

### Don't:
- **Don't** use gradient text (`background-clip: text`). Never intentional in this system.
- **Don't** use glassmorphism (backdrop-filter + translucent panels) as decoration. It is not part of the Bloomdots aesthetic.
- **Don't** use `border-left` greater than 1px as a coloured accent stripe on cards or callouts. Rewrite with full-border, background tint, or an overline label.
- **Don't** mix all three brand colours at equal weight inside a single surface (one section, one card, one hero). Pick one lead per surface; the other two appear only as small accents (overline, icon, focus ring).
- **Don't** treat any one brand colour as the default. Defaulting to a single colour across every section is the failure mode this system is designed to avoid.
- **Don't** use identical card grids where every card has the same layout, same icon, same text length. Vary the surface colour, content type, or card sizing before reaching for more cards.
- **Don't** use gradients on primary UI surfaces. Gradients are allowed only as transparent overlays on photographic images for text legibility protection.
- **Don't** use spring physics, bounce, or elastic easing. Bloomdots motion is ease-out, 200–600ms, confident and clean.
- **Don't** place the logo on a coloured or dark background without a white/light backing or inverted treatment. The three-dot mark reads poorly on Bloom Orange at its standard scale.
- **Don't** use exclamation marks in body copy. Confidence does not need them.
- **Don't** use Canela below H1 level. It loses its editorial authority at body size. Satoshi handles all UI text.
- **Don't** use the hero-metric template (big number, small label, supporting stats, gradient accent). It is a SaaS cliche and contrary to the Bloomdots brand register.
- **Don't** use cold or desaturated photography. Brand imagery is warm, vivid, high-contrast, and colour-graded toward the palette.
