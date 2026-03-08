# BloomDots Section Three Local to Global Design

## Scope
Design Section 3 of the BloomDots homepage: the `LOCAL TO GLOBAL` client proof section. This section should turn the wireframe idea of a logo wall into a high-impact credibility moment that lives in normal page flow and resolves into a clean proof grid.

## Context
- `DEV-NOTES.md` defines section three as a dark logo wall where logos appear one by one while scrolling.
- The wider project direction is dark, editorial, premium, motion-led, and culturally sharp.
- There is no existing Section 3 implementation located in `index.html`, so this should be treated as a fresh section design rather than a visual revision of finished markup.
- The approved direction for this section is `credibility first`, with logos carrying the proof rather than supporting metrics or long copy.

## Goals
- Make the section feel like a signature motion moment without pinning the viewport.
- Use client logos as the sole proof device.
- Start with a dramatic, art-directed field and end in a trustworthy, organized grid.
- Preserve brand recognition while avoiding a noisy, fully saturated logo collage.
- Keep the section readable, premium, and screenshot-strong by the final state.

## Non-Goals
- Do not turn the section into a stat-heavy proof strip.
- Do not build a pinned or long scrub-only stage.
- Do not rely on hover or hidden details for meaning.
- Do not leave the final state loose, abstract, or chaotic.
- Do not keep all logos fully saturated from the first frame.

## Selected Direction
Recommended and approved direction: `Scatter to Proof Grid`.

The section opens as a dark field of scattered logos arranged on invisible arcs and depth layers. As the user scrolls through the section, the logos move inward in staggered waves, shifting from a muted, atmospheric state into a clean, multi-column proof grid. Brand color returns selectively during the transition and resolves fully enough that the ending reads as credible and polished.

This direction gives the section the dramatic entrance the user requested while still ending in a disciplined proof wall that supports trust.

## Architecture
Section 3 should be a full-width section in normal page flow rather than a pinned scene. It should contain two layers:

1. `Intro band`
- Small uppercase label: `LOCAL TO GLOBAL`
- One strong editorial headline focused on trust, scale, or brand proof
- Optional one-line support copy only if the section needs warmth or framing

2. `Logo field`
- Large relative container beneath the intro band
- Approximately 12 to 18 logos
- Initial composition arranged intentionally, not randomly
- Final state resolves into a clean, evenly spaced proof grid

The copy should remain visually subordinate. The logo field is the primary event and should hold most of the section's weight.

## Visual Composition
The opening composition should feel cinematic and controlled. Logos should be placed across invisible arcs and layered depth zones so the field looks designed, not algorithmically random.

Composition rules:
- Use a few larger anchor logos near the center third
- Place smaller logos toward outer edges to widen the field
- Vary scale enough to create hierarchy, but not enough to distort brand legibility
- Keep the background dark and restrained so the logos own the contrast
- Use muted or partially desaturated treatment on entry

The final composition should become a disciplined multi-column grid with consistent gaps and alignment. The last frame should read immediately as `proof`, not `art installation`.

## Motion Direction
The section should use a three-beat motion sequence tied to normal scroll progress.

### Beat 1: Scatter Arrival
- Logos enter in a muted, low-contrast state
- Initial positions are offset with slight scale variation
- A soft haze or blur keeps the first read atmospheric rather than instantly literal
- A few anchor logos arrive first to establish the visual structure

### Beat 2: Sweep In
- Logos move inward in staggered waves
- Paths vary by item so the section feels authored instead of mechanically synced
- Travel can be diagonal, horizontal, or vertical, but all movement trends clearly toward order
- Selected logos regain stronger brand color during this phase while others remain partially muted

### Beat 3: Proof Resolve
- Haze clears and spacing tightens
- Logos snap into a clean grid
- Color treatment sharpens selectively first, then the full system settles
- Motion should calm down almost completely in the final state so the credibility message lands cleanly

## Motion Feel
The motion should feel:
- cinematic
- controlled
- premium
- deliberate
- cumulative

Avoid:
- random bounce
- chaotic swarm behavior
- endless idle motion
- full-color overload at the start
- equal timing across every logo

## Color Strategy
Approved direction: `hybrid`.

The section should not start as a bright logo soup. Logos should begin muted, softened, or partially monochrome so the opening composition feels cohesive and premium. As the choreography resolves, selected brands can recover color first, followed by a cleaner and more recognizable final grid state.

This gives the section both art direction and brand recognition without sacrificing either.

## Content Rules
- Lead with logos only
- Keep text minimal and supportive
- Do not add stat chips, badges, or proof counters
- Do not use captions or hover-based reveals
- Let the final arranged grid serve as the section's main proof statement

## Responsive Behavior
### Desktop
- Full scattered-to-grid choreography
- Broad field with visible hierarchy and longer travel distances

### Tablet
- Reduce scatter radius and travel range
- Keep composition tighter so the section does not feel too loose
- Preserve the same three-beat motion logic with fewer extremes

### Mobile
- Skip the dramatic scattered field
- Use a simpler staggered reveal into a compact logo grid or stacked matrix
- Keep brand recognition clear and spacing clean
- Do not attempt the full desktop choreography on a narrow screen

### Reduced Motion
- Start close to the resolved state
- Use short-distance transforms or fade-only reveals
- Avoid haze, long travel, and aggressive sequencing

## Accessibility
- Logos must remain visible and understandable without hover
- Decorative motion must not block the final proof reading
- Contrast between logos and the dark field must remain sufficient
- Reduced-motion users should still receive a clear proof wall without the theatrical transition

## Testing and Success Criteria
The section is successful if it:
- feels visually distinct from surrounding sections while still matching the site's design system
- communicates client credibility immediately by the end state
- avoids looking random during the scattered phase
- resolves into a clean proof grid on common desktop widths
- degrades cleanly on tablet, mobile, and reduced-motion setups

### Testing checklist
- desktop scroll timing and pacing
- readability of the final proof grid at laptop widths
- spacing consistency in the resolved grid
- color transition quality from muted to restored logos
- tablet scatter-range reduction
- mobile simplified grid behavior
- reduced-motion fallback

## Main Risk
The largest risk is over-stylizing the opening state so much that the section stops reading as client proof. The build should bias toward intentional composition, restrained haze, and a decisive final resolve into order.

## Recommendation
Implement Section 3 as a dark editorial proof wall that begins as a scattered, muted logo field and resolves through staged scroll choreography into a clean multi-column client grid. This balances drama with trust and best matches the approved goals for the section.
