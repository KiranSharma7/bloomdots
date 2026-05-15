# BloomDots Section Two Pinned Constellation Theater Design

## Scope
Design section two of `2nd.html` only. This section is the team introduction and must turn the wireframe idea of "dots that connect" into a dramatic but controlled GSAP-driven scene within a hard `100vh` limit.

## Context
- `2nd.html` is currently a polished hero-only prototype with section two not yet implemented.
- The project direction is dark, editorial, brutalist, premium, and motion-led.
- The wireframe and notes define section two as staff photos represented as dots that scatter and converge on scroll.
- The approved emphasis is `team credibility` first, not abstract symbolism.
- The user wants a section that feels unique and dramatic while still restrained.

## Goals
- Make section two a memorable signature moment immediately after the hero.
- Present real people clearly enough to build trust.
- Push GSAP aggressively without making the section noisy or gimmicky.
- Keep the experience within a single-screen `100vh` stage.
- End on a screenshot-strong final composition with readable names and roles.

## Non-Goals
- Do not build a generic team grid.
- Do not turn the section into a dense tech-network graphic.
- Do not rely on hover for critical identity information.
- Do not force the full desktop choreography onto mobile.
- Do not exceed the single-screen `100vh` limit.

## Selected Direction
Recommended and approved direction: `Pinned Constellation Theater`.

The section behaves like a short scroll performance. Portraits begin as a scattered but intentional field across a dark stage. As the user scrolls through the section, the portraits move inward on curved paths, selected connection lines draw in, and the composition resolves into a readable team tableau.

The section should feel like a premium editorial stage, not a novelty interaction.

## Core Experience
The section is visually pinned to the viewport through its own `100vh` canvas, but it should not rely on a long `140-180vh` pin-spacer pattern. The choreography must complete inside one screen's worth of reading and scroll attention.

The motion plays in three beats:

1. `Drift`
Portraits start dispersed across the stage with different scales and slight softness differences. They move inward on authored curved paths rather than straight lines.

2. `Connect`
As portraits approach their final positions, a small number of thin SVG connection lines draw between selected people. The lines act as elegant signals, not a full web.

3. `Resolve`
Blur reduces, labels become fully legible, and the composition settles into a clean team formation that can hold briefly as a final visual payoff.

## Visual Composition
The section should read as a dark editorial spread with one structured intro band above a theatrical portrait field.

### Intro band
- Small uppercase label such as `THE DOTS THAT CONNECT`
- Large editorial headline split across two lines if needed
- One short supporting paragraph framing the team as collective intelligence
- Optional proof line if there is room, but not required

### Main stage
- One oversized relative-positioned canvas occupying most of the remaining viewport
- 8 to 10 circular portraits
- Portraits vary in diameter to create composition hierarchy
- Portraits are placed across invisible arcs so the initial state feels designed rather than random
- A restrained SVG line layer sits above or between portrait planes

### Identity layer
Names and roles should be visible enough to support credibility.

To avoid a repetitive roster look:
- 3 to 4 primary portraits can hold clearly visible labels from the start
- Remaining labels can become more explicit during the resolve phase
- Captions can be bottom-anchored or side-anchored depending on portrait placement

The final state should feel like a composed cast arrangement, not a loose cloud.

## Motion Direction
This section should be built around one master GSAP timeline tied to scroll progress.

### Primary motion layers
- Portrait wrapper translation on curved inward paths
- Slight scale adjustments during convergence
- Soft blur-to-sharp transitions
- Controlled opacity shifts
- SVG line draw animations
- Label opacity and vertical reveal

### Supporting motion layers
- Very subtle ambient drift before the main convergence begins
- Selective emphasis on 2 to 3 portraits during the resolve phase
- Light background depth shifts, if any, kept nearly invisible

### Motion feel
The motion should feel:
- magnetic
- weighted
- cinematic
- authored
- calm under pressure

Avoid:
- bounce
- busy orbital loops
- neon-glow network effects
- equal-timing animation across every portrait
- excessive rotation

## Technical Structure
Section two should be implemented as:
- `section#team` with `min-height: 100vh`
- an editorial top block for label, headline, and copy
- a `team-stage` relative container for the portrait field
- absolutely positioned portrait items on desktop
- an SVG overlay for connection paths
- an alternate simplified mobile layout

Each portrait item should support:
- image
- name
- role
- optional per-item motion offsets
- desktop label placement metadata if needed

## Scroll Strategy
Because the section is capped at `100vh`, the choreography must be compact.

Recommended approach:
- tie one GSAP timeline to section scroll progress using `ScrollTrigger`
- map early progress to portrait drift
- map middle progress to line drawing
- map late progress to label clarity and final settle

This should behave like a compressed cinematic sequence, not a long scrub chapter.

## Mobile Behavior
Mobile should preserve the concept but not attempt the full stage choreography.

Recommended mobile fallback:
- portraits arranged in a clean stacked or two-column circular roster
- staggered reveal on enter
- labels always readable
- little or no connection-line system
- no dense overlap

Mobile should communicate the same team credibility without fighting the screen size.

## Accessibility and Reduced Motion
- Identity information must remain available without hover.
- Portrait images should keep meaningful `alt` text.
- Reduced-motion mode should disable the heavy convergence choreography and present a simpler reveal or direct settled state.
- Text contrast must stay strong against the dark background and image edges.

## Testing and Success Criteria
The section is successful if it:
- feels visually distinct from the hero while still part of the same system
- completes its main choreography within the perceived `100vh` viewing window
- keeps names and roles legible by the resolve phase
- ends in a strong composed final arrangement
- avoids overlap bugs at common desktop widths
- degrades cleanly on mobile and reduced-motion settings

### Testing checklist
- desktop scroll timing through section
- final composition at common laptop widths
- label readability over portrait crops
- SVG line alignment during and after animation
- mobile stacked layout behavior
- reduced-motion fallback
- performance on lower-powered devices

## Main Risk
The biggest risk is overdesign. If too many lines, labels, blur states, or moving elements compete at once, the section will lose clarity and stop feeling premium. The build should bias toward fewer, more intentional signals.

## Recommendation
Implement section two as a single-screen editorial team stage with a scrubbed GSAP convergence timeline, selective line drawing, and a final readable team tableau.
