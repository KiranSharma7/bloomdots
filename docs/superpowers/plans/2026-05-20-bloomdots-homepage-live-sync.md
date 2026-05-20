# BloomDots Homepage Live Sync Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the live BloomDots homepage so page `32` matches local `index.html` as closely as possible while preserving the live header, footer, and contact form.

**Architecture:** Keep the WordPress page as an Elementor v3 document and use Novamira abilities for all live implementation writes. Elementor v3 global styles provide reusable colors and typography; `wp-content/novamira-sandbox/*.php` provides high-fidelity CSS/JS for animation-heavy sections.

**Tech Stack:** WordPress 6.9.4, Elementor v3 containers/widgets under Elementor 4, Elementor Pro, Novamira MCP, GSAP 3.12.5, ScrollTrigger, Lenis, PHP sandbox files, local `index.html`.

---

## File Structure

- Source reference: `C:/Users/black/OneDrive/Desktop/Code/Testing/index.html`
- Design reference: `C:/Users/black/OneDrive/Desktop/Code/Testing/docs/plans/2026-05-20-bloomdots-homepage-live-sync-design.md`
- Plan tracker: `C:/Users/black/OneDrive/Desktop/Code/Testing/docs/superpowers/plans/2026-05-20-bloomdots-homepage-live-sync.md`
- Live Elementor page: WordPress page `32`, homepage.
- Live sandbox files:
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-global.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-hero.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-team.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-logos.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-services.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-stats.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-portfolio.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-process.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-founder.php`
- Preserve unless fixing selector compatibility:
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-nav.php`
  - `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-footer.php`

## Task 1: Baseline Backup And Section Map

**Files:**
- Read: `C:/Users/black/OneDrive/Desktop/Code/Testing/index.html`
- Read: live Elementor page `32`
- Create: `C:/Users/black/OneDrive/Desktop/Code/Testing/docs/superpowers/specs/2026-05-20-post32-pre-homepage-sync.json`

- [ ] **Step 1: Export the current Elementor document**

Run Novamira ability `novamira/elementor-get-content` with:

```json
{
  "post_id": 32,
  "full_dump": true
}
```

Save the returned content JSON to `docs/superpowers/specs/2026-05-20-post32-pre-homepage-sync.json`.

- [ ] **Step 2: Confirm live page identity**

Run Novamira ability `novamira/execute-php` with:

```php
$id = (int) get_option('page_on_front');
return [
  'page_on_front' => $id,
  'title' => get_the_title($id),
  'permalink' => get_permalink($id),
  'modified' => get_post_modified_time('c', false, $id),
  'template' => get_post_meta($id, '_wp_page_template', true),
  'elementor_edit_mode' => get_post_meta($id, '_elementor_edit_mode', true),
];
```

Expected: `page_on_front` is `32`, title is `Home`, permalink is `https://staging4.bloomdots.com.au/`, and `elementor_edit_mode` is `builder`.

- [ ] **Step 3: Map source sections from local HTML**

Run:

```powershell
Select-String -Path "C:\Users\black\OneDrive\Desktop\Code\Testing\index.html" -Pattern '<header id="hero"','<section id="logo-stack"','<section id="logo-grid-section"','<section id="services"','<section id="stats"','<section id="work"','<section class="port-panel','<section id="process"','<section id="founder"','<section id="contact"','<footer id="site-footer"' | ForEach-Object { "{0}:{1}" -f $_.LineNumber,$_.Line.Trim() }
```

Expected: line references for hero, logo stack, logo grid, services, stats, work/portfolio panels, process, founder, contact, and footer.

- [ ] **Step 4: Commit the backup artifact**

Run:

```powershell
git add docs/superpowers/specs/2026-05-20-post32-pre-homepage-sync.json
git commit -m "docs(bloomdots): backup homepage before live sync"
```

Expected: commit succeeds and does not stage unrelated `.playwright-cli` deletions or `index.html`.

## Task 2: Global Style Foundation

**Files:**
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-global.php`
- Read: Elementor v3 global styles
- Preserve: nav/footer/contact selectors

- [ ] **Step 1: Read current global sandbox file**

Run Novamira ability `novamira/read-file` with:

```json
{
  "path": "wp-content/novamira-sandbox/bloomdots-global.php"
}
```

Expected: file contains GSAP, ScrollTrigger, Lenis enqueue, and `:root` BloomDots variables.

- [ ] **Step 2: Confirm global Elementor v3 styles**

Run Novamira ability `novamira/elementor-list-v3-styles` with `{}`.

Expected custom colors include `bd_bg`, `bd_bg_soft`, `bd_bg_elevated`, `bd_orange`, `bd_blue`, and `bd_amber`; typography includes Canela and Satoshi presets.

- [ ] **Step 3: Update global PHP/CSS only for parity gaps**

Use Novamira ability `novamira/edit-file` for surgical replacements in `bloomdots-global.php`.

Required global values:

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
  --bloom-orange: #E84E28;
  --bloom-orange-hover: #D1401C;
  --bloom-blue: #29B9EA;
  --bloom-blue-hover: #1AA3D4;
  --bloom-amber: #FAB72B;
  --yellow: var(--bloom-amber);
  --blue: var(--bloom-blue);
  --orange: var(--bloom-orange);
}
```

Expected: legacy aliases remain because local `index.html` still uses `--yellow`, `--blue`, and `--orange` in several section scripts/styles.

- [ ] **Step 4: Verify scripts are enqueued once**

Run Novamira ability `novamira/execute-php` with:

```php
return [
  'gsap_registered' => wp_script_is('gsap', 'registered'),
  'scrolltrigger_registered' => wp_script_is('gsap-st', 'registered'),
  'lenis_registered' => wp_script_is('lenis', 'registered'),
];
```

Expected: all three values are `true` after `wp_enqueue_scripts` has run on the frontend. If this PHP context returns `false`, verify by reading `bloomdots-global.php` rather than adding duplicate enqueues.

## Task 3: Hero Section Parity

**Files:**
- Modify: live Elementor page `32`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-hero.php`
- Preserve: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-nav.php`

- [ ] **Step 1: Read live hero subtree**

Run Novamira ability `novamira/elementor-get-content` with:

```json
{
  "post_id": 32,
  "element_id": "a32b95e"
}
```

Expected: subtree contains the top hero area and does not include contact/footer.

- [ ] **Step 2: Align hero DOM hooks**

Use `novamira/elementor-edit-element` or `novamira/elementor-set-content` to ensure the hero section exposes these hooks through v3 containers/widgets:

```text
#hero
#hero-video
#hero-content
#hero-eyebrow
#headline-1
#hero-phrase-wrap
#hero-phrase-0
#hero-phrase-1
#hero-sub
#hero-ctas
#hero-trust
```

Expected: header/nav remains controlled by existing `#main-nav` from `bloomdots-nav.php`.

- [ ] **Step 3: Update hero sandbox behavior**

Patch `bloomdots-section-hero.php` so its CSS/JS matches the local `index.html` hero behavior:

```text
hero video scale/parallax
hero phrase swap animation
hero CTA styling
hero trust bar
reduced-motion fallback
content-visible fallback when GSAP fails
```

Expected: no edits to `bloomdots-nav.php`.

- [ ] **Step 4: Verify hero**

Open `https://staging4.bloomdots.com.au/`.

Expected desktop: fullscreen hero, video visible, centered headline `Content`, rotating phrase, CTA pair, trust bar, nav preserved.

Expected mobile: headline and CTAs fit without overlap, trust bar collapses as in `index.html`, nav preserved.

## Task 4: Team And Logo Sections

**Files:**
- Modify: live Elementor page `32`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-team.php`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-logos.php`

- [ ] **Step 1: Read team and logo subtrees**

Run Novamira ability `novamira/elementor-get-content` for elements:

```json
{ "post_id": 32, "element_id": "0cc5dee" }
```

```json
{ "post_id": 32, "element_id": "6f26c59" }
```

Expected: `0cc5dee` maps to `team`; `6f26c59` maps to `logos`.

- [ ] **Step 2: Align section hooks**

Ensure Elementor exposes:

```text
#logo-stack
#logo-stack-inner
.tca-scroll-card
#logo-grid-section
.logo-grid-item
.many-more-heading
```

For the team section, preserve or add the hooks already expected by `bloomdots-section-team.php`, including:

```text
#team
.bd-team-dot
.bd-team-connection
.bd-team-mobile
```

- [ ] **Step 3: Update sandbox CSS/JS from local HTML**

Patch section files so behavior matches `index.html`:

```text
Team: vertical scroll dot convergence, mobile fallback list.
Logos: pinned card stack, scattered logo/grid reveal, light nav theme triggers.
```

Expected: section backgrounds and nav theme transitions match local `index.html`.

- [ ] **Step 4: Verify team/logos**

Scroll through the live page.

Expected: team dots converge on scroll; logo stack cards animate; logo grid items stagger in; content remains visible if ScrollTrigger fails.

## Task 5: Services Live Media Wall

**Files:**
- Modify: live Elementor page `32`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-services.php`

- [ ] **Step 1: Read current services subtree**

Run Novamira ability `novamira/elementor-get-content` with the current services root discovered from the skeleton. If the services root is not obvious, run:

```php
$data = json_decode(get_post_meta(32, '_elementor_data', true), true);
$out = [];
$walk = function($els) use (&$walk, &$out) {
  foreach ($els as $el) {
    $s = $el['settings'] ?? [];
    $text = wp_strip_all_tags(($s['title'] ?? '') . ' ' . ($s['editor'] ?? '') . ' ' . ($s['_element_id'] ?? '') . ' ' . ($s['css_classes'] ?? ''));
    if (preg_match('/services|svc-|outcomes/i', $text)) {
      $out[] = ['id' => $el['id'], 'elType' => $el['elType'] ?? '', 'widgetType' => $el['widgetType'] ?? '', 'text' => mb_substr($text, 0, 120)];
    }
    if (!empty($el['elements'])) $walk($el['elements']);
  }
};
$walk($data);
return $out;
```

Expected: identify the services section root and child tile elements.

- [ ] **Step 2: Align services content and hooks**

Ensure the live section has:

```text
#services
.svc-label
.svc-headline
.svc-sub
.svc-tile
.svc-tile--website
.svc-tile--content
.svc-tile--paid
.svc-tile--cultural
.svc-tile__thumb
.svc-tile__video-wrap
.svc-tile__content
.svc-tile__accent
#svc-expand
.svc-expand__inner
```

Expected user-facing tile content:

```text
Brand & Identity
Content & Social
Performance & Ads
Cultural Marketing
```

- [ ] **Step 3: Update service sandbox behavior**

Patch `bloomdots-section-services.php` so it matches `index.html`:

```text
live media wall layout
hover/tap media reveal
tile accent lines
expand panel open/close
reduced-motion fallbacks
video playing/waiting class behavior
```

- [ ] **Step 4: Verify services**

Expected desktop: irregular media wall, hover video/image movement, tile accent lines animate, expansion panel opens without layout collision.

Expected mobile: tiles stack cleanly, tap opens details, text remains readable.

## Task 6: Stats Receipts Section

**Files:**
- Modify: live Elementor page `32`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-stats.php`

- [ ] **Step 1: Read stats subtree**

Run Novamira ability `novamira/elementor-get-content` with:

```json
{
  "post_id": 32,
  "element_id": "e7c7445"
}
```

Expected: root has `_element_id` `stats` and class `bd-section bd-section-stats`.

- [ ] **Step 2: Align stats hooks and values**

Ensure the section exposes:

```text
#stats
.stats-marquee
.stats-marquee__track
.stats-body
.stats-hero__ghost
.stats-gridlines
.stats-label
.stats-hero
.stats-hero__number [data-count-to="343"]
.stats-block--projects [data-count-to="29"]
.stats-block--clients [data-count-to="55"]
.stats-block--content [data-count-to="2345"]
.stats-bottom [data-count-to="20"]
```

- [ ] **Step 3: Update stats CSS/JS**

Patch `bloomdots-section-stats.php` to match the local receipts design, marquee, gridlines, counters, and reduced-motion final-state behavior.

- [ ] **Step 4: Verify stats**

Expected: marquee loops smoothly, counters count once on entry, `343M+` is visually dominant, stats layout matches `index.html` on desktop and mobile.

## Task 7: Portfolio / Selected Work

**Files:**
- Modify: live Elementor page `32`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-portfolio.php`

- [ ] **Step 1: Read portfolio subtrees**

Run Novamira ability `novamira/execute-php`:

```php
$data = json_decode(get_post_meta(32, '_elementor_data', true), true);
$out = [];
$walk = function($els) use (&$walk, &$out) {
  foreach ($els as $el) {
    $s = $el['settings'] ?? [];
    $text = wp_strip_all_tags(($s['title'] ?? '') . ' ' . ($s['editor'] ?? '') . ' ' . ($s['_element_id'] ?? '') . ' ' . ($s['css_classes'] ?? ''));
    if (preg_match('/selected work|portfolio|port-|pinned|services/i', $text)) {
      $out[] = ['id' => $el['id'], 'elType' => $el['elType'] ?? '', 'widgetType' => $el['widgetType'] ?? '', 'text' => mb_substr($text, 0, 140)];
    }
    if (!empty($el['elements'])) $walk($el['elements']);
  }
};
$walk($data);
return $out;
```

Expected: identify intro section and four portfolio panel roots.

- [ ] **Step 2: Align portfolio hooks**

Ensure Elementor exposes:

```text
#work
#portfolio
.portfolio-intro
.port-panel
.pinned
.last-pinned
.port-panel--1
.port-panel--2
.port-panel--3
.port-panel--4
.port-panel__effect
.port-panel__inner
.port-panel__text
.port-panel__visuals
.port-img-grid
.port-img
```

- [ ] **Step 3: Update portfolio sandbox**

Patch `bloomdots-section-portfolio.php` to match `index.html` pinned panel behavior:

```text
intro reveal
panel scale/rotate/shrink effect
last panel dark anchor
mobile non-pinned fallback
image hover scale
CTA hover state
```

- [ ] **Step 4: Verify portfolio**

Expected desktop: selected work intro transitions into stacked/pinned panels with smooth scroll progress.

Expected mobile: portfolio panels stack naturally without pinning glitches or excessive blank space.

## Task 8: Process Timeline

**Files:**
- Modify: live Elementor page `32`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-process.php`

- [ ] **Step 1: Read process subtree**

Run Novamira ability `novamira/elementor-get-content` with:

```json
{
  "post_id": 32,
  "element_id": "bcf65bb"
}
```

Expected: root has `_element_id` `process` and classes `bd-section bd-section-process`.

- [ ] **Step 2: Align process hooks**

Ensure Elementor exposes:

```text
#process
.process-intro
.process-label
.process-headline
.process-sub
.process-timeline
.process-line-wrap
.process-line
.process-line__track
.process-line__progress
.process-dot-indicator
.process-phases
.process-phase
.process-phase__marker
.process-phase__num
.process-phase__dot
.process-phase__content
.process-phase__title
.process-phase__desc
.process-phase__list
```

- [ ] **Step 3: Update process sandbox**

Patch `bloomdots-section-process.php` to match the local three-phase animation:

```text
desktop pinned timeline progress
active phase transitions
mobile staggered phase reveals
reduced-motion visible state
```

- [ ] **Step 4: Verify process**

Expected: labels/headline reveal, three process phases activate in order, list items animate without overlap.

## Task 9: Founder Section

**Files:**
- Modify: live Elementor page `32`
- Modify: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-section-founder.php`

- [ ] **Step 1: Read founder subtree**

Run Novamira ability `novamira/execute-php`:

```php
$data = json_decode(get_post_meta(32, '_elementor_data', true), true);
$out = [];
$walk = function($els) use (&$walk, &$out) {
  foreach ($els as $el) {
    $s = $el['settings'] ?? [];
    $text = wp_strip_all_tags(($s['title'] ?? '') . ' ' . ($s['editor'] ?? '') . ' ' . ($s['_element_id'] ?? '') . ' ' . ($s['css_classes'] ?? ''));
    if (preg_match('/founder|aditi|creative director|word from/i', $text)) {
      $out[] = ['id' => $el['id'], 'elType' => $el['elType'] ?? '', 'widgetType' => $el['widgetType'] ?? '', 'text' => mb_substr($text, 0, 140)];
    }
    if (!empty($el['elements'])) $walk($el['elements']);
  }
};
$walk($data);
return $out;
```

Expected: identify founder section root and portrait/content elements.

- [ ] **Step 2: Align founder hooks**

Ensure Elementor exposes:

```text
#founder
.founder-portrait
.founder-portrait__img
.founder-portrait__mask
.founder-content
.founder-label
.founder-pullquote
.founder-body
.founder-divider
.founder-name
.founder-role
.founder-dots
.founder-dots__dot
```

- [ ] **Step 3: Update founder sandbox**

Patch `bloomdots-section-founder.php` to match the local section:

```text
light section theme
portrait mask wipe
content stagger reveal
signature/name treatment
decorative dots reveal
mobile stacking
```

- [ ] **Step 4: Verify founder**

Expected: portrait and copy match `index.html`; mask and content reveal fire once; section does not collide with contact below.

## Task 10: Preserve Contact, Footer, And Header

**Files:**
- Read: live Elementor page `32`
- Read: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-nav.php`
- Read: `/home/customer/www/staging4.bloomdots.com.au/public_html/wp-content/novamira-sandbox/bloomdots-footer.php`

- [ ] **Step 1: Confirm contact subtree still exists**

Run Novamira ability `novamira/execute-php`:

```php
$data = json_decode(get_post_meta(32, '_elementor_data', true), true);
$found = [];
$walk = function($els) use (&$walk, &$found) {
  foreach ($els as $el) {
    $s = $el['settings'] ?? [];
    $text = wp_strip_all_tags(($s['title'] ?? '') . ' ' . ($s['editor'] ?? '') . ' ' . ($s['_element_id'] ?? '') . ' ' . ($s['css_classes'] ?? ''));
    if (preg_match('/contact|ready to bloom|send message|cf-name|contact-form/i', $text)) {
      $found[] = ['id' => $el['id'], 'elType' => $el['elType'] ?? '', 'widgetType' => $el['widgetType'] ?? '', 'text' => mb_substr($text, 0, 140)];
    }
    if (!empty($el['elements'])) $walk($el['elements']);
  }
};
$walk($data);
return $found;
```

Expected: contact-related elements are still present and were not rebuilt.

- [ ] **Step 2: Confirm nav/footer files were not replaced**

Run Novamira ability `novamira/list-directory` with:

```json
{
  "path": "wp-content/novamira-sandbox",
  "recursive": false
}
```

Expected: `bloomdots-nav.php` and `bloomdots-footer.php` remain present. Modified timestamps should not change during section work unless a selector compatibility fix was intentionally made and recorded.

- [ ] **Step 3: Manual behavior check**

Expected:

```text
Header: nav opens/closes on mobile, scroll hide/show still works.
Contact: form fields render and submit feedback still works.
Footer: footer links and animations still render.
```

## Task 11: Final Full-Page Verification

**Files:**
- Read: live page frontend
- Read: live Elementor page `32`
- Modify: `C:/Users/black/OneDrive/Desktop/Code/Testing/DEV-NOTES.md` only if recording completion notes

- [ ] **Step 1: Read final Elementor skeleton**

Run Novamira ability `novamira/elementor-get-content` with:

```json
{
  "post_id": 32
}
```

Expected: page reads successfully, element count is reasonable, and section roots for hero/team/logos/services/stats/portfolio/process/founder/contact remain present.

- [ ] **Step 2: Frontend smoke check**

Open `https://staging4.bloomdots.com.au/` on desktop and mobile widths.

Expected:

```text
No blank first viewport.
No JavaScript console errors from duplicated GSAP registration.
No text overlap in hero, services, stats, portfolio, process, founder.
Pinned sections release correctly.
Reduced-motion users get visible content.
Header, footer, contact are intact.
```

- [ ] **Step 3: Cache/style refresh check**

If frontend does not reflect Elementor changes, run Novamira ability `novamira/elementor-set-content` only with the final validated tree, or make a no-op `novamira/update-post` on page `32` to trigger cache invalidation.

Expected: frontend updates without manual WordPress admin work.

- [ ] **Step 4: Record completion note**

Append a short dated note to `DEV-NOTES.md`:

```markdown
- 2026-05-20 - Live homepage sync completed via Novamira/Elementor v3. Updated global foundation and hero/team/logos/services/stats/portfolio/process/founder to match `index.html`; preserved header, footer, and contact form.
```

- [ ] **Step 5: Commit local documentation updates**

Run:

```powershell
git add DEV-NOTES.md docs/superpowers/specs/2026-05-20-post32-pre-homepage-sync.json
git commit -m "docs(bloomdots): record homepage live sync"
```

Expected: commit includes only documentation/backup artifacts created during this work.

## Self-Review

Spec coverage:
- Close visual/interactive parity with `index.html`: Tasks 2-9.
- Use Novamira MCP for implementation: every live write is a Novamira ability.
- Elementor v3: plan keeps v3 and does not enable v4 atomic.
- Use global styles as much as possible: Task 2 confirms v3 global style foundation before section work.
- Inspect sandbox files: file responsibilities are mapped above.
- Preserve header/footer/contact: Tasks 3 and 10 explicitly protect them.

Placeholder scan:
- No task depends on an unspecified file.
- Every live write names the Novamira ability or target file.
- Verification expectations are explicit.

Type and identifier consistency:
- WordPress page ID is `32` throughout.
- Sandbox paths consistently use `wp-content/novamira-sandbox`.
- Section hooks are copied from the approved local `index.html` and current live skeleton.
