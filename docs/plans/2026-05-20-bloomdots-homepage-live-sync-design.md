# BloomDots Homepage Live Sync Design

## Goal

Update the live BloomDots homepage on `staging4.bloomdots.com.au` so it matches the local `index.html` as closely as possible, visually and interactively, while preserving the existing header, footer, and contact form.

## Current State

- Local source of truth: `index.html`.
- Live WordPress homepage: page `32`, title `Home`, slug `home`.
- Live builder surface: Elementor v3 containers and widgets.
- Elementor v4 atomic widgets are not available on the site because the `e_atomic_elements` experiment is off.
- Existing Novamira sandbox files already split the homepage into global, nav, footer, and section-specific behavior.
- Existing Elementor v3 global styles contain the BloomDots palette and typography foundation:
  - Canela display typography.
  - Satoshi body/UI typography.
  - Dark background and surface colors.
  - Bloom orange `#E84E28`, Bloom blue `#29B9EA`, Bloom amber `#FAB72B`.

## Non-Goals

- Do not redesign the header.
- Do not redesign the footer.
- Do not redesign or replace the contact form section.
- Do not enable or migrate to Elementor v4 atomic widgets for this update.
- Do not replace the Elementor page with a single static HTML dump.

## Recommended Approach

Keep the live homepage as an Elementor v3 document, and use Novamira to update the Elementor structure and sandbox files section by section.

Elementor v3 global styles should carry reusable colors and typography. The Novamira sandbox should carry high-fidelity section CSS and JavaScript needed for parity with `index.html`: GSAP, ScrollTrigger, Lenis, pinned scroll, counters, hover panels, marquee motion, responsive overrides, and section-specific layout.

This approach gives the closest match to `index.html` without sacrificing the live page's existing WordPress/Elementor composition.

## Sandbox Responsibilities

- `bloomdots-global.php`: global variables, base styles, font assumptions, GSAP/ScrollTrigger/Lenis enqueue, reduced-motion safety.
- `bloomdots-nav.php`: existing header and mobile menu behavior. Preserve unless a global compatibility fix is required.
- `bloomdots-footer.php`: existing footer behavior. Preserve unless a global compatibility fix is required.
- `bloomdots-section-hero.php`: hero visuals and hero animation hooks, excluding nav/header changes.
- `bloomdots-section-team.php`: connected/team dot animation.
- `bloomdots-section-logos.php`: logo stack and logo grid animation.
- `bloomdots-section-services.php`: live media wall, hover/tap expansion behavior, service tile visual states.
- `bloomdots-section-stats.php`: receipts layout, marquee, counter animation.
- `bloomdots-section-portfolio.php`: selected work intro, pinned/stacked portfolio panels, CTA behavior.
- `bloomdots-section-process.php`: process timeline and reveal choreography.
- `bloomdots-section-founder.php`: founder note layout and reveal choreography.

## Section Scope

Update, in order:

1. Global style foundation.
2. Hero section, preserving the existing header/nav.
3. Team and logo sections.
4. Services section.
5. Stats section.
6. Portfolio/work section.
7. Process section.
8. Founder section.

Leave contact and footer untouched.

## Elementor Structure

The live Elementor page should expose the IDs and classes expected by the sandbox scripts and styles. Elementor content should remain semantically sectioned with v3 containers/widgets rather than hidden in a single HTML widget.

Use native Elementor v3 settings and global styles where they express the intent cleanly. Use sandbox CSS/JS for behavior that Elementor controls cannot represent, especially ScrollTrigger timelines, pseudo-elements, hover media behavior, pinned panels, and animated counters.

## Verification

After each major section update:

- Read the Elementor tree back through Novamira.
- Confirm expected section IDs/classes are present.
- Confirm header, footer, and contact form remain intact.
- Visually inspect desktop and mobile behavior.
- Verify GSAP/ScrollTrigger behavior does not hide content when scripts fail or reduced motion is active.

## Risks

- The local `index.html` uses custom Tailwind-era markup and scripts that cannot be copied directly into Elementor v3 controls.
- Pinned scroll and hover media behavior depends on correct DOM hooks and script timing.
- Global CSS changes can accidentally affect preserved nav/footer/contact sections, so selectors must stay scoped where possible.
- The live page already has a large Elementor tree; surgical updates should avoid deleting unrelated existing content until replacements are verified.
