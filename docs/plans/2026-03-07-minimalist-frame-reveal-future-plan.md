# BloomDots Minimalist Frame Reveal Future Plan

## Status
Future concept only. This does not replace the approved poster montage reveal plan.

## Purpose
Preserve a second intro direction for future exploration: a minimalist frame reveal that is cleaner, faster, and more performance-safe than the poster montage.

## Direction Summary
The intro uses a single dark full-screen overlay with:
- giant headline fragments
- thin editorial rules
- one controlled wipe or frame-clear motion
- restrained BloomDots accent signals

This approach should feel elegant, precise, and premium without becoming visually dense.

## Why Keep This Direction
- Safer for performance than a multi-card montage
- Faster to read on repeat visits
- Easier to keep clean across mobile breakpoints
- Strong fit if the final brand direction leans more restrained than campaign-like

## Trade-Off
The minimalist frame reveal may feel less memorable and less like a premium campaign launch than the poster montage or editorial curtain directions.

## Proposed Future Experience Flow
1. A near-black overlay appears with one oversized headline fragment and a small label.
2. Thin rules or frame edges define the composition.
3. One controlled wipe, split, or frame-lift clears the screen.
4. The hero timeline starts only after the frame reveal fully exits.

## Visual Guardrails
- Keep typography dominant
- Use one focal message only
- Limit accent colors to subtle signals
- Avoid image-heavy treatment
- Avoid layered-card clutter
- Keep motion planar, sharp, and deliberate

## Motion Guardrails
- Favor `transform` and `opacity`
- Use minimal `clip-path`
- Keep total intro time short, around 1.4 to 2.0 seconds
- Use `power3.out`, `power4.out`, or `expo.out`
- Avoid bounce, spin, or decorative motion

## Suggested Future Build Scope
- Separate `intro-overlay` variant for minimalist mode
- One large type block
- One label block
- One or two thin frame/rule elements
- One wipe or panel-clear animation
- Shared hero handoff logic with the main intro system

## When To Choose This Later
Choose this direction if:
- the poster montage feels too visually busy
- mobile readability becomes a bigger concern
- repeat-load elegance matters more than spectacle
- performance simplification becomes a priority

## Relationship To Existing Plans
This file is an additive future option.

The current approved implementation path remains:
- [2026-03-07-landing-page-reveal-animation-design.md](C:\Users\black\OneDrive\Desktop\Code\Bloom Dots\Bloomdots\docs\plans\2026-03-07-landing-page-reveal-animation-design.md)
- [2026-03-07-landing-page-reveal-animation-implementation-plan.md](C:\Users\black\OneDrive\Desktop\Code\Bloom Dots\Bloomdots\docs\plans\2026-03-07-landing-page-reveal-animation-implementation-plan.md)
