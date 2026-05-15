# BloomDots Landing Page Reveal Animation Design

## Scope
Design a premium full-page opening reveal animation for the BloomDots landing page using GSAP. This is a branded intro system that plays before the hero animation on every page load. It is not a hero-only reveal and it is not a fake loader showing the live hero underneath.

## Context
- The current project is a single-page dark editorial marketing site in `index.html`.
- The existing design direction is premium, brutalist, editorial, and motion-led.
- The current page already uses GSAP, ScrollTrigger, Canela, Satoshi, dark surfaces, and restrained accent colors.
- The new reveal must fit that system instead of introducing a different visual language.

## Goals
- Create a memorable premium first impression.
- Make the intro feel theatrical, bold, and art directed.
- Keep typography as the primary visual driver.
- Preserve a clear separation between the branded intro and the hero entrance.
- Ensure the reveal is repeatable on every load without becoming visually noisy.

## Non-Goals
- Do not build a progress-bar style preloader.
- Do not reveal the live hero underneath the intro.
- Do not let images dominate the intro.
- Do not add cartoonish or overly decorative motion.
- Do not turn the montage into a cluttered collage.

## Selected Direction
Recommended and approved direction: poster montage reveal.

This approach uses a fixed full-screen branded overlay composed of several editorial poster cards. Oversized typography, micro-labels, thin rules, proof-like cues, and restrained BloomDots accents enter as a layered composition, then collapse away before the hero begins.

## Experience Flow
The intro plays on every page load.

The reveal is a self-contained full-screen poster montage that fully owns the screen for roughly 2.2 to 2.8 seconds. During this phase, the hero content does not animate underneath it.

After the montage sequence completes, the intro exits in a decisive final move. Only then does the hero begin its own animation sequence:
- hero background media entrance
- nav and logo entrance
- headline reveal
- subcopy and CTA reveal
- scroll cue entrance

This creates a theatrical two-act sequence:
1. Brand montage
2. Page reveal

The handoff must be immediate, with no dead pause between the intro exit and the first hero motion.

## Visual Composition
The intro should feel like a family of premium editorial campaign posters assembling live on a dark stage.

### Core elements
- Near-black full-screen background
- Subtle grain texture
- One dominant oversized Canela-led statement card
- Small uppercase Satoshi label card
- One or two thin divider rules
- Restrained BloomDots accents using yellow, blue, and orange as signals only
- One optional supporting proof or metric card
- One optional image card only if needed later, never as the main background

### Poster system
Use 3 to 5 total cards.

Recommended card roles:
1. Hero statement card
2. Signal label card
3. Numeric or proof card
4. Dot or accent card
5. Optional image card

The cards should vary in size and aspect ratio. One should be clearly dominant. The composition can feel layered and slightly offset, but it must still obey a disciplined underlying grid.

### Motion language
- Lateral slides
- Vertical drops
- Clip reveals
- Stack compression
- Restrained opacity transitions

Avoid:
- bounce
- dramatic spin
- particle-like effects
- scrapbook randomness
- too many equal-weight moving objects

The feel should be rigid, graphic, cinematic, and premium.

## Animation Architecture
The reveal must be implemented as a separate intro system, not folded into the hero timeline.

### Structure
Create a fixed full-viewport `intro-overlay` above the page content containing:
- grain layer
- poster stage wrapper
- 3 to 5 poster cards
- type blocks
- label elements
- accent dots and rules

### Timelines
Use two GSAP timelines:

1. `introTl`
Controls the poster montage sequence from first frame through exit.

2. `heroTl`
Starts only after `introTl` completes.

### `introTl` responsibilities
- stage fade-in
- dominant card entrance
- secondary card stagger
- label and rule snap-in
- brief montage hold
- card alignment/compression
- full overlay exit

### `heroTl` responsibilities
- hero background media entrance
- nav and logo arrival
- headline line reveal
- subcopy and CTA stagger
- scroll indicator entrance

This separation keeps the motion system maintainable and allows future tuning of the intro without breaking the hero.

## Behavior and Performance
Because the intro plays on every load, it needs strong implementation guardrails.

### Interaction behavior
- The overlay is fixed and full-screen while active
- Pointer interaction is blocked during the intro
- The intro begins only after the DOM is ready
- After exit, the overlay is removed or left inert and hidden

### Performance constraints
- Prefer `transform` and `opacity`
- Use `clip-path` sparingly and only on a few large elements
- Avoid layout-triggering animation properties
- Keep the grain effect static or extremely subtle
- Limit the poster count to 3 to 5 cards
- Keep rotation minimal or eliminate it entirely
- Avoid heavy blur and shadow effects that muddy the montage

## Fallbacks
- If GSAP fails, the intro overlay must fail open so the page becomes visible quickly
- If hero media loads slowly, the hero should still animate into a controlled placeholder state
- If reduced-motion handling is implemented later, it should switch to a near-instant staged fade rather than running the full montage

## Testing and Success Criteria
The reveal is successful if it:
- fully covers the viewport on desktop and mobile
- exits cleanly every time
- always triggers the hero sequence after completion
- keeps one clear visual focal point throughout the montage
- avoids flicker, overlap bugs, and frozen-looking states
- feels premium rather than chaotic

### Testing checklist
- desktop viewport load behavior
- tablet and mobile viewport load behavior
- repeated refresh behavior
- intro-to-hero timing handoff
- readability of card hierarchy and overlap across breakpoints
- slow hero media behavior
- GSAP failure fallback
- reduced-motion behavior if added

## Main Risk
The biggest risk is overdesign. Too many cards, labels, numbers, and signals arriving at once will make the intro feel cluttered instead of premium. The implementation should bias toward subtraction.

## Recommendation
Implement the intro as a dedicated full-screen poster montage system with 3 to 5 editorial cards, then trigger the hero timeline only after the montage fully exits.
