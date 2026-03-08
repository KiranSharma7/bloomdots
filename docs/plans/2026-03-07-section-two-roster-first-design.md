# BloomDots Section Two Roster First Design

## Scope
Design an alternate version of section two in `2nd.html` using the `Roster First` direction. This version keeps the section within a hard `100vh` limit and prioritizes a structured, visible team roster while preserving a creative-premium editorial feel.

## Context
- Section two is the team introduction immediately after the hero.
- The wireframe idea is still based on team members as dots, but this variant reduces the abstract scatter behavior in favor of a more legible roster.
- The approved stylistic target for this variant is `creative and premium`, not corporate-safe.
- This is an alternate concept alongside the more dramatic `Pinned Constellation Theater` direction.

## Goals
- Make the team immediately understandable at a glance.
- Keep names and roles clearly readable.
- Preserve visual tension and originality without relying on a dramatic convergence scene.
- Use GSAP to refine and tighten the roster rather than overpower it.
- Keep the section elegant, composed, and screenshot-strong.

## Non-Goals
- Do not build a generic equal-card team grid.
- Do not make the roster feel like a corporate About page.
- Do not use heavy blur choreography or long-travel animation.
- Do not let motion dominate readability.
- Do not exceed the `100vh` section limit.

## Selected Direction
Recommended and approved direction: `Editorial Split Roster`.

The section is built as a structured split layout. The left side carries the messaging and editorial voice. The right side presents a visible roster of circular team portraits arranged in a disciplined but art-directed composition. On scroll, the system becomes more precise: circles tighten, labels sharpen, and selective line accents appear.

This version should feel like a premium editorial casting board rather than a dramatic performance stage.

## Core Experience
The user should understand the section in a clean hierarchy:

1. What this team represents
2. Who the people are
3. How the motion reinforces that idea

The roster should never feel chaotic. The motion should act as refinement rather than transformation.

## Architecture
The section should live inside a single `100vh` composition with two main columns.

### Left column
- Small uppercase label
- Oversized headline in Canela
- Short supporting paragraph
- Optional micro-proof line or accent rule

### Right column
- 6 to 9 visible circular portraits
- Names and roles integrated directly into the roster composition
- A disciplined row structure with slight offsets and scale differences

This preserves roster clarity while leaving enough room for art direction.

## Visual Composition
The section should feel like a premium editorial page with controlled asymmetry.

### Left side treatment
- Strong negative space
- Tight paragraph width
- Large, confident type
- One subtle accent cue such as a thin line or dot marker

### Right side treatment
- Portraits arranged in a multi-row roster
- Alignment is intentional but not perfectly uniform
- Some circles slightly larger to create hierarchy
- A few portraits can sit a little higher or lower to avoid a template look
- One or two captions can break the base rhythm slightly for visual interest

### Caption system
- Names and roles should be visible without hover
- Captions should feel integrated, not boxed
- Use refined text blocks rather than UI cards

Optional supporting layer:
- a faint line system
- subtle guide arcs
- very restrained background structure behind the roster

The section should look designed, not decorative.

## Motion Direction
This version should use GSAP with more restraint than the constellation concept.

### Motion beats
1. `Reveal`
Left-side editorial copy enters first with a clean stagger. The roster appears already mostly formed.

2. `Tighten`
As the user scrolls, portrait circles shift slightly into a cleaner resolved alignment. Motion distances stay short.

3. `Signal`
Selective line accents or small connector cues activate. Labels sharpen, opacity settles, and the layout locks into a precise final state.

### Motion feel
The motion should feel:
- refined
- controlled
- premium
- deliberate
- exact

Avoid:
- large travel distances
- dramatic collapse effects
- heavy blur shifts
- excessive connectors
- animated clutter

## Technical Structure
The section should be implemented as:
- `section#team` constrained to `100vh`
- a left editorial content column
- a right roster field container
- portrait items with image, name, and role
- optional SVG accent lines behind or between portraits

Each portrait block should support:
- minor x/y offset behavior
- small scale variation
- label placement
- responsive reflow rules

## Scroll Strategy
Use one GSAP timeline connected to section scroll progress.

Recommended behavior:
- early progress reveals left-side text and roster presence
- mid progress performs subtle portrait tightening
- late progress resolves captions and accent lines

The user should feel that the layout is becoming sharper and more resolved, not being rebuilt.

## Mobile Behavior
Mobile should simplify the split into a stacked layout.

Recommended mobile fallback:
- headline and copy on top
- two-column or single-column circular roster beneath
- names and roles always readable
- simple staggered reveal only
- little or no line-accent system

The mobile version should keep the same identity while removing layout tension that would hurt readability.

## Accessibility and Reduced Motion
- All names and roles must remain visible without hover.
- Portraits should include meaningful `alt` text.
- Reduced-motion mode should skip the tightening choreography and show the roster in a settled layout with minimal fade/stagger only.
- Contrast must remain strong across text, captions, and portrait edges.

## Testing and Success Criteria
The section is successful if it:
- communicates the team clearly on first read
- feels more art-directed than a normal team grid
- keeps the roster readable at common desktop widths
- uses motion to refine the composition rather than distract
- adapts cleanly to mobile without feeling broken or cramped

### Testing checklist
- desktop split-layout balance
- roster readability at laptop widths
- caption placement consistency
- subtle scroll tightening behavior
- mobile roster stacking
- reduced-motion fallback
- visual rhythm between left text block and right roster field

## Main Risk
The main risk is drifting into a safe agency-team layout. If the roster becomes too regular or the captions become too UI-like, the section will lose the creative-premium edge. The build should protect asymmetry, hierarchy, and typographic confidence.

## Recommendation
Implement this alternate version as a `100vh` editorial split layout with a structured creative roster, always-readable identity details, and subtle tightening-on-scroll behavior.
