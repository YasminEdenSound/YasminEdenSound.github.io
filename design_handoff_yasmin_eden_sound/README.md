# Handoff: Yasmin Eden Sound — landing page

## Overview
A single-page marketing site for an independent sound engineer offering mixing, mastering and
recording. Audience: musicians and bands looking to hire her. The page's job is one conversion:
get the visitor to send an enquiry (Formspree form) or reach out via email / WhatsApp / Instagram.

Requirement from the client: it must run as a **static site on GitHub Pages** — no build step,
no server. All copy marked with [square brackets] is a placeholder awaiting real content.

## About the Design Files
The files in this bundle are **design references created in HTML** — a prototype showing intended
look and behavior, not production code to copy verbatim. The task is to **recreate this design in
the target codebase's existing environment**, using its established patterns and libraries.

In this particular case the target may legitimately *be* plain static HTML/CSS/JS (that is the
client's deployment constraint), in which case the prototype can be followed very closely. If it
is being folded into an existing framework (React, Astro, Eleventy, etc.), rebuild the markup in
that framework's idiom and keep the visual spec below exact.

Note on the prototype's structure: it is authored as a component with a template plus a logic
class, and it manipulates the DOM directly for the animations (querySelector on data-attributes).
That is an artifact of the prototyping environment. In a real implementation, prefer the target
framework's own refs/effects — the animation *behavior* is what matters, not this wiring.

## Fidelity
**High-fidelity.** Final colors, typography, spacing and interactions. Recreate the UI closely.
The one low-fidelity companion file (`Concept Wireframes.dc.html`) is included for context only —
it shows three structural options that were explored; option **1a** is the one that was built.
Do not implement 1b or 1c.

## Layout foundation
- Page background `#12110E`, body text `#F2EDE1`.
- Every section is a full-width band; content is constrained by an inner container:
  `max-width: 1120px; margin: 0 auto; padding: clamp(64px, 9vw, 104px) 28px`.
- Section grids use `repeat(auto-fit, minmax(min(100%, Xpx), 1fr))` so they collapse on narrow
  viewports without media queries. X is 280px (work), 220px (process), 300px (about),
  260px (testimonials), 250px (rates), 290px (contact).
- Nothing is fixed-width; the page must reflow down to ~360px.
- Section dividers: a hairline rule `rgba(242,237,225,.1)` with a single jasmine petal centered,
  14px, rotated 20°, in accent yellow.

## The jasmine mark
The brand mark is a five-petal jasmine (the name Yasmin → jasmine). It is **geometric, not
illustrative**: five identical ellipses in a 100×100 viewBox (`viewBox="-50 -50 100 100"`),
each `rx="13" ry="38" cy="-26"`, rotated 0/72/144/216/288°, filled `#E9C846`. Nothing else.
It appears at 22px in the nav, 96px in the loading intro, 17px in the footer, one petal in the
dividers, and at `min(760px, 90vw)` at 8.5% opacity as a background bloom in the hero.

## Screens / Views
Single scrolling page. Sections in order:

### Sticky nav
- Purpose: persistent access to the Book CTA.
- Layout: sticky top, `z-index: 40`, background `rgba(18,17,14,.86)` with `backdrop-filter: blur(12px)`,
  bottom border `1px solid rgba(242,237,225,.09)`. Inner container padding `14px 28px`,
  flex, space-between, `flex-wrap: wrap`, `gap: 14px 20px`.
- Left: jasmine mark 22px + wordmark "Yasmin Eden" in Instrument Serif 20px.
- Right: four mono links (Work, Process, About, Rates) — Geist Mono 10px, letter-spacing .16em,
  uppercase, `#9A9384`; then the CTA pill "Book a session" — `padding: 9px 18px`,
  `border: 1px solid #E9C846`, `border-radius: 999px`, 13px/500, color `#E9C846`,
  `white-space: nowrap`. Hover: background fills `#E9C846`, text `#12110E`, 150ms.
- Anchors point at #work, #process, #about, #rates, #book. `html { scroll-behavior: smooth }`.

### Loading intro (first visit only)
- Purpose: brand moment. Fixed overlay, `inset: 0`, `z-index: 100`, background `#12110E`,
  centered column, `gap: 26px`.
- Content: the 96px jasmine, then "Yasmin Eden" (Instrument Serif 38px) with "SOUND" beneath
  (Geist Mono 10px, letter-spacing .34em, uppercase, `#9A9384`).
- See Interactions for timing. Shows once per browser session.

### Hero (#top)
- Purpose: say who she is and what the records sound like; drive to Book.
- Layout: container with `padding: clamp(72px,13vh,140px) 28px clamp(64px,11vh,112px)`,
  flex column, `gap: 30px`, left-aligned. Background bloom absolutely positioned
  `right: -14%; top: -26%`, `opacity: .085`, `pointer-events: none`; parent `overflow: hidden`.
- Eyebrow: "Mixing · Mastering · Recording" — Geist Mono 10px, letter-spacing .28em, uppercase, `#E9C846`.
- H1: "Records that sound like the room they were made in." — Instrument Serif 400,
  `clamp(46px, 8.2vw, 104px)`, line-height .96, letter-spacing -.015em, `max-width: 15ch`,
  `text-wrap: balance`.
- Body: `clamp(16px,1.5vw,19px)`/1.6, `#CFC9BC`, `max-width: 46ch`.
- Primary CTA: solid pill — `padding: 14px 26px`, background `#E9C846`, text `#12110E`, 15px/600,
  `border-radius: 999px`. Hover: `translateY(-2px)` + `box-shadow: 0 10px 26px rgba(233,200,70,.24)`.
- Secondary: "Hear the work ↓" mono link, `#9A9384`.

### 01 Selected work (#work)
- Purpose: prove the ear. Three SoundCloud embeds.
- Section heading pattern (used by every numbered section): a baseline-aligned flex row,
  `gap: 18px` — mono number (Geist Mono 10px, letter-spacing .24em, `#E9C846`) then H2
  (Instrument Serif 400, `clamp(30px,4vw,46px)`, line-height 1.05).
- Intro line: "Three records from the last year. Press play — the meter follows the track."
  16px/1.6, `#9A9384`, `max-width: 44ch`, 40px bottom margin.
- Three cards, grid `gap: 22px`. Card: `padding: 20px`, `border: 1px solid rgba(242,237,225,.11)`,
  `border-radius: 4px`, background `rgba(242,237,225,.02)`, flex column `gap: 14px`.
  - Header row: left column with track title (Instrument Serif 22px) and credit line
    (Geist Mono 10px, .16em, uppercase, `#9A9384`) e.g. "[Artist] · Mix & Master";
    right, a state label reading "Idle" / "Playing" (Geist Mono 9px, .14em, uppercase).
  - Meter: flex row, `align-items: flex-end`, `gap: 3px`, `height: 30px`, holding 22 bars —
    each `flex: 1; min-width: 2px; height: 100%`, background `#E9C846`,
    `transform-origin: bottom`, `border-radius: 1px`.
  - Player: bordered box `1px solid rgba(242,237,225,.09)`, `border-radius: 3px`,
    `overflow: hidden`, holding a 120px-tall SoundCloud iframe.
- **Open item:** the iframes currently point at placeholder URLs
  (`https://soundcloud.com/YOUR-PROFILE/TRACK-1..3`). Three real track URLs must be supplied.
  Player params used: `color=%23e9c846&visual=false&hide_related=true&show_comments=false&show_user=true&show_teaser=false`.

### 02 How it works (#process)
Four steps in a grid, `gap: 28px`, heading margin-bottom 44px. Each step: `padding-top: 18px`
with `border-top: 1px solid rgba(233,200,70,.4)`, then mono step number (11px, .2em, `#E9C846`),
H3 (Instrument Serif 400, 23px), body (15px/1.6, `#9A9384`, `text-wrap: pretty`).
Steps: Send the demos / Agree the plan / Work and revise / Delivery.

### 03 About Yasmin (#about)
- Band background `rgba(242,237,225,.03)` with hairline top and bottom borders.
- Two-column grid, `gap: clamp(32px,5vw,64px)`, `align-items: center`.
- Left: the **duotone photo**. Wrapper has background `#E9C846`, `border-radius: 3px`,
  `overflow: hidden`, `align-self: start`. The `<img>` is
  `filter: grayscale(1) contrast(1.12) brightness(1.04)` with `mix-blend-mode: multiply`,
  `width: 100%`, `height: auto`, `display: block`. That combination is what produces the
  black/yellow duotone — reproduce all three parts or the effect is lost.
- Right: section heading, two placeholder paragraphs (17px/1.68, `#CFC9BC`), then a
  `<dl>` of three stats in a `repeat(auto-fit, minmax(120px, 1fr))` grid: Based in / Working since /
  Records finished — mono label 9px .16em uppercase `#9A9384` over an Instrument Serif 20px value.

### 04 What artists say
Three `<blockquote>` cards in a grid, `gap: 22px`. Card: `padding: 26px`,
`border: 1px solid rgba(242,237,225,.11)`, `border-radius: 4px`, flex column `gap: 16px`.
Quote in Instrument Serif 20px/1.45; attribution in a `<footer>`, Geist Mono 10px, .14em,
uppercase, `#9A9384`.

### 05 Services & rates (#rates)
- **Deliberately placed late in the page.** The client did not want prices up front; they come
  after the work, the process, the about and the testimonials. Keep this order.
- Framing line above the cards (16px/1.6, `#9A9384`, `max-width: 52ch`): rates are starting
  points, final cost depends on track count / stem condition / revisions, fixed quote before work
  begins. This copy is load-bearing for the positioning — do not cut it.
- Three cards, grid `gap: 22px`, each `padding: 28px`, `border-radius: 4px`, flex column `gap: 18px`:
  H3 (Instrument Serif 400, 26px), then a price row, then a 4-item `<ul>` (list-style none,
  `gap: 10px`, 15px/1.5, `#CFC9BC`).
- Price row: baseline flex, `gap: 8px` — mono "from" (10px .14em uppercase `#9A9384`),
  the figure in Instrument Serif 38px `#E9C846`, then mono unit "/ song" or "/ day".
- Mixing `from $XXX / song`; Mastering `from $XX / song`; Recording `from $XXX / day`.
- Recording is the emphasized card: `border: 1px solid rgba(233,200,70,.34)`,
  background `rgba(233,200,70,.04)`.

### 06 Questions
Native `<details>`/`<summary>` accordion, `max-width: 760px`. Each row has
`border-top: 1px solid rgba(242,237,225,.12)` (last row also bottom). Summary:
`cursor: pointer`, `padding: 20px 0`, 17px, `list-style: none`, flex space-between with a
`+` in `#E9C846`. Answer: 15px/1.65, `#9A9384`, `max-width: 62ch`, `margin-bottom: 22px`.
Four questions: file delivery, mix turnaround, remote work, deposits and payment.

### 07 Book a session (#book)
- Band background `rgba(242,237,225,.03)`, hairline top border. Two-column grid,
  `gap: clamp(32px,5vw,72px)`.
- Left: heading, a 17px/1.65 line promising a reply within two working days, then three
  direct-contact rows. Each row is an `<a>`: flex space-between, `padding: 16px 0`,
  `border-top: 1px solid rgba(242,237,225,.12)` (last also bottom), a mono label on the left
  (`#9A9384`) and the value on the right at 16px `#F2EDE1`. Hover turns the row `#E9C846`.
  Rows: Email → `mailto:[hello@example.com]`; WhatsApp → `https://wa.me/[NUMBER]`;
  Instagram → `https://instagram.com/[handle]`.
- Right: the form — `padding: clamp(24px,3vw,34px)`, `border: 1px solid rgba(242,237,225,.13)`,
  `border-radius: 4px`, background `#12110E`, flex column `gap: 18px`.
  `<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">`.
  Fields (all required): `name` (text), `email` (email), `message` (textarea, rows 5).
  Each field is a `<label>` column, `gap: 9px`, with a mono caption (9px, .18em, uppercase,
  `#9A9384`) above the input. Input: `padding: 13px 14px`, background `rgba(242,237,225,.05)`,
  `border: 1px solid rgba(242,237,225,.14)`, `border-radius: 3px`, 16px, `outline: none`;
  on focus the border becomes `#E9C846`. Textarea adds `line-height: 1.5`, `resize: vertical`.
  Submit: full-width solid yellow pill, `padding: 15px 24px`, 15px/600, same hover lift as the hero CTA.
  A mono note under the button reminds the implementer to replace `YOUR_FORM_ID`; drop that note
  once the real endpoint is in.
- Note: 16px is the minimum input font-size that prevents iOS Safari from zooming on focus. Keep it.

### Footer
Hairline top border, `padding: 34px 28px`, flex wrap space-between. Left: 17px jasmine +
"Yasmin Eden Sound" in Instrument Serif 17px. Right: mono 10px, .16em, uppercase, `#9A9384` —
"© [Year] · [City]".

## Interactions & Behavior

All motion is disabled under `@media (prefers-reduced-motion: reduce)` — the prototype both
sets `animation-duration/transition-duration: .01ms` globally and branches on
`matchMedia('(prefers-reduced-motion: reduce)').matches` in JS to skip the intro, the reveals
and the meter loop. Preserve both.

1. **Loading intro.** Petals animate in one at a time via a `petalIn` keyframe:
   `transform: rotate(var(--r)) scaleY(.06)` + `opacity: 0` → `scaleY(1)`/`opacity: 1`,
   720ms `cubic-bezier(.2,.8,.2,1)`, delays 50 / 170 / 290 / 410 / 530ms. Each petal carries its
   own rotation as `--r` so the rotate survives the scale. The name block then uses a `riseIn`
   keyframe (14px up + fade), 800ms, delay 620ms. At 1900ms the overlay transitions to
   `opacity: 0; visibility: hidden` over 700ms and `pointer-events` go to none.
   `document.body.style.overflow = 'hidden'` while it plays; restored on hide.
   Gated by `sessionStorage['ye-loader-seen']` — once per session.
2. **Section reveals.** Elements marked `data-reveal` start at `opacity: 0`,
   `translateY(14px)`, transition `opacity .6s ease, transform .7s cubic-bezier(.2,.8,.2,1)`.
   An IntersectionObserver (`rootMargin: '0px 0px -8% 0px'`, `threshold: .08`) reveals them and
   `unobserve`s — **once only, no re-hide on scroll back**. Entries intersecting in the same
   callback are staggered 70ms apart. Two safety nets to keep, both important: if
   IntersectionObserver is unavailable everything is revealed immediately, and a 3500ms timeout
   reveals everything regardless, so content can never be stranded invisible.
3. **Nav mark as scroll indicator.** On scroll (passive listener), the nav jasmine rotates
   `scrollProgress × 90deg` — a quarter turn from top of page to bottom, `transition: transform .18s linear`.
   Progress = `scrollY / (scrollHeight - innerHeight)`.
4. **Play reaction** (the one place the page responds to audio). Via the SoundCloud Widget API
   (`https://w.soundcloud.com/player/api.js`), each iframe binds PLAY, PAUSE and FINISH.
   On PLAY of track *i*: that card's border goes `rgba(233,200,70,.45)` and background
   `rgba(233,200,70,.045)`; its state label reads "Playing" in `#E9C846`; the other two revert
   to idle styling. Its 22 meter bars animate on a 110ms interval — each bar eases toward a
   target `scaleY` of `max(.12, min(1, shape × (.45 + random × .75)))` where
   `shape = 1 - |i - 10.5| / 15` (a gentle center-weighted curve), lerp factor .75 rising /
   .25 falling; bar opacity 1 when live, .45 when idle. Idle rest position is `scaleY(.07)`.
   While anything plays, the hero bloom rotates +0.55° per tick and its opacity rises to .14;
   on stop it eases back to .085 over 800ms.
   **Be explicit with the client about this:** SoundCloud iframes do not expose audio data
   cross-origin, so the meter is driven by play state and a shaped random envelope, not by real
   levels. It reads as alive; it is not analysis. Do not attempt real FFT here — it cannot work.
5. **Hover states.** Nav pill fills yellow. Both solid CTAs lift 2px with a yellow-tinted shadow.
   Contact rows turn yellow. Inputs take a yellow focus border. All 120–150ms, no bounce.
6. **Responsive.** No media queries — `clamp()` for type and section padding, `auto-fit` grids,
   and `flex-wrap` on the nav and footer. Verify down to 360px: the nav wraps to two rows there
   and the Book pill must stay on one line.

## State Management
Minimal; all UI state, no data fetching.
- `playing`: index of the currently playing track, or null. Drives card styling, state labels,
  meter animation and the hero bloom. Set by SoundCloud PLAY, cleared by PAUSE/FINISH.
- `reduced`: cached reduced-motion preference; gates all motion.
- Per-meter `level[22]`: current bar scales, eased toward target each tick.
- `bloomAngle`: accumulating rotation for the hero bloom.
- Session flag `ye-loader-seen` in sessionStorage.
- One `setInterval` at 110ms for the meters, and one passive scroll listener — both must be
  torn down on unmount.
- Form submission is a native POST to Formspree; no client-side state, no fetch. Formspree
  handles validation feedback and the thank-you page. If a nicer inline success state is wanted
  later, switch to `fetch` with `Accept: application/json`.

## Design Tokens

Colors
- `#12110E` — page background (ink)
- `#F2EDE1` — primary text (cream)
- `#CFC9BC` — body copy on dark
- `#9A9384` — muted / mono labels (6.19:1 on ink — this is the floor; do not go dimmer)
- `#E9C846` — accent (signal yellow): CTAs, numbers, prices, the mark, meters
- `rgba(242,237,225,.02–.05)` — card and input fills
- `rgba(242,237,225,.09–.14)` — hairlines and borders
- `rgba(233,200,70,.04 / .34 / .45)` — emphasized card fill / border / active card border
- `rgba(18,17,14,.86)` — nav background under blur

Typography
- Display / headings: **Instrument Serif** 400 (and its italic, unused so far)
- Body / UI: **Instrument Sans** 400 / 500 / 600
- Technical: **Geist Mono** 400 / 500 — always uppercase with wide letter-spacing (.1em–.34em);
  used for section numbers, eyebrows, labels, units, credits, footer
- Scale: H1 `clamp(46px,8.2vw,104px)`/.96 · H2 `clamp(30px,4vw,46px)`/1.05 · H3 23–26px ·
  price figure 38px · lead `clamp(16px,1.5vw,19px)`/1.6 · body 15–17px/1.5–1.68 ·
  mono 9–11px. Nothing smaller than 9px, and 9px only for wide-tracked uppercase mono.
- `text-wrap: balance` on the H1, `text-wrap: pretty` on body paragraphs.
- Loaded from Google Fonts. If the target codebase self-hosts fonts, match the families exactly —
  the serif/mono pairing is the identity. Do not substitute Inter or Roboto.

Spacing
- Section vertical rhythm `clamp(64px,9vw,104px)`; horizontal gutter 28px; container 1120px.
- Grid gaps 22px (cards), 28px (process), `clamp(32px,5vw,64–72px)` (two-column bands).
- Card padding 20px (track), 26px (quote), 28px (rates); form padding `clamp(24px,3vw,34px)`.

Radii
- 3px inputs and the photo · 4px cards and the form · 999px pills.

Shadows
- Only one: `0 10px 26px rgba(233,200,70,.24)` (hero CTA hover) and `.22` (submit hover).
  No ambient shadows anywhere — depth comes from hairlines and fill tints.

## Assets
- `assets/yasmin-desk.png` — 608×404 photograph of Yasmin at the console, supplied by the client.
  Used once, in the About section, rendered duotone in CSS (see above). The source file is
  already black and white; the `grayscale(1)` filter is retained so a color replacement still works.
- No icon library, no illustrations. The jasmine mark is inline SVG, defined above.
- Fonts from Google Fonts. SoundCloud Widget API from `w.soundcloud.com`.

## Files
- `Yasmin Eden Sound.dc.html` — the high-fidelity design. Template first, then the logic class
  holding the loader, reveal, meter, scroll-knob and SoundCloud wiring.
- `Concept Wireframes.dc.html` — low-fidelity structural exploration, context only. Option 1a
  is what was built.
- `assets/yasmin-desk.png` — the About photo.

## Open items before launch
1. Three real SoundCloud track URLs (currently `YOUR-PROFILE/TRACK-1..3` placeholders).
2. The Formspree endpoint id, replacing `YOUR_FORM_ID`.
3. All `[bracketed]` copy: business name confirmation ("Yasmin Eden" vs "Yasmin Eden Sound" —
   the nav uses the former, the footer and intro the latter), track titles and artists, the two
   About paragraphs and three stats, three testimonials, four FAQ answers, prices, email,
   WhatsApp number, Instagram handle, city, year.
4. Deployment: static output to GitHub Pages. Needs a favicon (the jasmine mark works),
   `<title>`, meta description and an OG image — none of which the prototype includes.
