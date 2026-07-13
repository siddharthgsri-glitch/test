# Handoff: askappu.in — Siddharth ("Appu") Personal Site

## Overview

A personal portfolio + projects site for **Siddharth** (known to family as "Appu") — a 12-year-old from Bangalore whose interests include aircraft, flying, chess, badminton, Harry Potter, and teaching. His mission is **AI for Bharat** — small AI tools for real, everyday problems Indians face.

The site is a two-tier structure:

1. **Landing page** (`askappu-blueprint.html`) — five-section vertical scroll:
   - **01 Hero** — Introduction with animated paper airplane
   - **02 About** — Illustrated compass-badge avatar with initial "A" + short bio + quick facts
   - **03 Interests** — 5 cards (Flying, Chess, Badminton, Harry Potter, Teaching)
   - **04 Projects** — 6 project cards linking to sub-pages
   - **05 Mission + Contact** — AI-for-Bharat mission statement + mailto-based contact form

2. **Six project sub-pages** (`projects/<slug>/index.html`) — one detailed page per project:
   - **FormSaathi** — AI assistant for Indian government forms in native languages
   - **KrishiScan** — Crop disease diagnosis from a phone photo
   - **BusBuddy** — Simplified real-time BMTC bus tracker for elders
   - **PathshalaAI** — Textbook translation into a kid's stronger language
   - **DoctorSetu** — Prescription decoder + medication reminders
   - **ShopSmart** — WhatsApp-based kirana inventory for small shopkeepers

An **alternate visual direction** is also included (`askappu-opensky.html` — bright, cloud-and-sun aesthetic with Fraunces serif display type). The user selected the Blueprint Cockpit direction as the primary; Open Sky is preserved for reference or A/B use.

## About the Design Files

The HTML/CSS files in this bundle are **design references** — self-contained prototypes that demonstrate intended look, layout, motion, and copy. They are **not intended to be shipped as-is into a framework codebase without review**.

The task for the developer is to **recreate these designs in the target environment** using its established patterns and libraries. Since Siddharth wants to host this directly on askappu.in (a static site), the simplest path is to **ship these HTML files as-is** — they are already self-contained (aside from the shared `projects/_shared/project.css` that sub-pages reference) and production-viable for a static host such as Netlify, Cloudflare Pages, GitHub Pages, or Vercel.

If integrating into an existing framework (React, Vue, Astro, Next.js, etc.), port the markup to components and move the CSS into the target styling solution. The `projects.json` file (`projects/_shared/projects.json`) is the single source of truth for all project copy — it drives the sub-page template.

Only one address change is required before deploy: update the `to` variable in the `sendMessage()` function inside `askappu-blueprint.html` to Siddharth's real email address (currently `hello@askappu.in`).

## Fidelity

**High-fidelity (hifi).** Every file in this bundle is a pixel-precise mockup with final colors, typography, spacing, layout rhythm, iconography, motion, and copy. All values below are the exact tokens used in the code.

## File Structure

```
askappu-blueprint.html               # PRIMARY landing page (Blueprint Cockpit direction)
askappu-opensky.html                 # Alternate direction (Open Sky) — reference only
projects/
  _shared/
    project.css                      # Shared styles for all sub-pages
    projects.json                    # Single source of truth for project copy
  formsaathi/
    index.html                       # FormSaathi sub-page
    hero.jpg                         # AI-generated blueprint-style hero (1152x768)
  krishiscan/
    index.html
    hero.jpg
  busbuddy/
    index.html
    hero.jpg
  pathshala/
    index.html
    hero.jpg
  doctorsetu/
    index.html
    hero.jpg
  shopsmart/
    index.html
    hero.jpg
```

## Screens / Views

### LANDING PAGE — `askappu-blueprint.html`

All five sections share:

- Fixed **blueprint-grid background** (`<div class="grid-bg">`): stacked `linear-gradient` grids at 40px (soft) and 200px (harder) intervals, plus subtle radial glows in the corners.
- Fixed **top HUD bar** — brand mark + section links (numbered `01 · Home` etc.) + `Cleared for takeoff` status with pulsing green dot. Collapses to hamburger menu below 768px (JS toggle on `nav.open`).
- Fixed **animated paper airplane** — SVG at 60px wide, 22s linear infinite `fly` keyframe that sweeps left→right across the viewport with vertical dips at 25/50/75% and opacity fade at both ends.
- Section padding: `90–100px top / 80–100px bottom / 6vw side` on desktop; `70px top / 60px bottom / 5vw side` on mobile. **Only the Hero uses `min-height: 100vh`** — every other section sizes to content. This was tightened at user's request after initial build; keep it that way.

#### 01 · Hero

**Purpose:** Introduce Siddharth in one line — age, city, personality.

**Layout:** Single column of centered content inside a 1200px max container. Two decorative circular **cockpit gauges** absolutely positioned on the right (hidden below 900px).

**Components:**

| Element | Details |
|---|---|
| Callsign | `CALLSIGN · SIDDHARTH-001 · BLR` — JetBrains Mono 12px, letter-spacing 0.25em, `#ffb454` (amber), uppercase |
| Headline | `Hi, I'm Siddharth. I'm 12, and I'm building things.` — Space Grotesk 700, `clamp(36px, 9vw, 108px)`, `#ffffff`, letter-spacing -0.03em, line-height 1.02, `overflow-wrap: break-word` + `hyphens: auto` (for narrow phones). "Siddharth" is wrapped in `<span class="accent">` styled `#7fd7ff` (cyan). |
| Sub | *"A kid from Bangalore who loves aircraft, chess, badminton and Harry Potter — and who thinks AI can quietly fix a lot of everyday problems in Bharat."* — max-width 600px, `clamp(16px, 1.4vw, 20px)`, `#cfe2f5` |
| Meta strip | 4 mono key/value stats in a flex-wrap row: `AGE · 12 years` / `BASE · Bangalore, IN` / `CURRENT MISSION · AI for Bharat` / `ALTITUDE · Climbing ↗`. Label is `--muted` #6d8ca8 mono 12px; value is `#7fd7ff` (cyan) 15px, block-level below the label. |
| Cockpit gauges | Two 120×120 SVG-composed circular gauges (border 1.5px `#1e4a75`), with animated needles: gauge "slow" runs `spin1` (18s, 20° → 120° ease-in-out alternate infinite), gauge "fast" runs `spin2` (8s, -45° → 85°). Labels: `CURIOSITY 082`, `FUEL: IDEAS 100`. Amber needle with linear-gradient fade at the tip. Tick marks at 12 and 6 o'clock. |
| Scroll cue | Bottom-left `SCROLL` mono label above a 1px×30px cyan gradient line. `bob` animation 2.4s translateY infinite. Hidden on mobile. |

#### 02 · About

**Layout:** Two-column grid `320px | 1fr`, gap 60px, collapses to single column below 900px.

**Left — Avatar (compass badge):** A 1:1 SVG (`viewBox 0 0 300 300`) with:
- Concentric rings at r=120 (`#1e4a75` 1.5px), r=105 (`#1e4a75` dashed 3 4), r=88 (`#7fd7ff` 1.5px opacity 0.6).
- Two symmetric wing paths (Q-curves) in `#7fd7ff` (2px) and `#52b6e6` (1.2px + 1px opacity 0.7).
- N/S/E/W compass labels at top/bottom/left/right in JetBrains Mono 9px `#52b6e6`.
- Large centered initial `A` in Space Grotesk 96/700 `#7fd7ff` with text-shadow glow `0 0 20px rgba(127,215,255,0.4)`.

**Right — Bio:**
- Eyebrow: `02 · About the pilot` (section-label style: 40px cyan line + mono 11px `#52b6e6`)
- Title: `Curious kid, blueprint brain.` — Space Grotesk 600, `clamp(36px, 5vw, 64px)`, `#ffffff`
- Body: `"I'm Siddharth — friends call me Appu — twelve years old, from Bangalore. I love figuring out how things work, especially aircraft (why does lift even happen?), chess openings, and the small, quiet magic of a good Harry Potter chapter. I teach whenever I can, because explaining something is the best way to actually understand it."`
- Facts grid: 4 cards, auto-fit min-140px, gap 20px. Each: `--k` mono 10/uppercase muted label, `--v` white 18/500 value. Cards: 1px `#1e4a75` border, `rgba(23,50,79,0.35)` bg, cyan L-shape corner brackets via `::before` (top-left) and `::after` (bottom-right).
  - Age — **12**
  - Based in — **Bangalore**
  - Superpower — **Curiosity**
  - Dream job — **Aeronaut / builder**

#### 03 · Interests

**Layout:** Eyebrow (`03 · Flight log`), title `Things I nerd out about.`, one-line sub, then a grid `repeat(auto-fit, minmax(220px, 1fr))` gap 20px.

**5 cards** with same shape: 1px `#1e4a75` border, `linear-gradient(180deg, rgba(23,50,79,0.5), rgba(10,26,46,0.5))` bg, 28/24 padding, min-height 220px, mono `data-num` counter (`01/05`) in top-right corner. Hover: `translateY(-4px)` + border becomes `#7fd7ff` + brighter bg gradient. 300ms transition.

Each card has a 44×44 cyan stroke SVG icon (custom, no icon library), a Space Grotesk 22/600 title, and 14/muted body copy:

| # | Title | Copy |
|---|---|---|
| 01 | Flying & Aircraft | *How lift, drag and thrust actually work. Paper planes, model kits, cockpit videos on repeat.* |
| 02 | Chess | *Openings, middlegame tactics, endgame studies. Currently obsessed with the London and the Caro-Kann.* |
| 03 | Badminton | *Weekend smashes and drop shots. Working on my backhand clear so it stops embarrassing me.* |
| 04 | Harry Potter | *Ravenclaw energy. Re-reading the series for the nth time — Prisoner of Azkaban still wins.* |
| 05 | Teaching | *Explaining aerodynamics, chess ideas and small science tricks to whoever will listen — mostly cousins.* |

#### 04 · Projects

**Layout:**
- Split header: left has eyebrow `04 · Hangar · Live projects` + title `Things I'm building.`; right has one-line sub *"Small AI tools for real problems in India. Each one starts with something I saw at home or in my neighbourhood."*
- Grid `repeat(auto-fit, minmax(280px, 1fr))` gap 20px.

**Project card (`.p-card`)** — an entire `<a>` linking to `projects/<slug>/index.html`:
- Thumbnail (3:2 aspect ratio) filling the top with `object-fit: cover`, `border-bottom: 1px solid #1e4a75`.
- Overlay status pill (`.p-card-status`) top-left of thumbnail: `In dev` (amber), `Beta` (cyan), `Live` (green). 9px mono, uppercase, `rgba(6,17,31,0.85)` bg, 1px `#12324f` border, with a pulsing 5px dot.
- Body block below thumbnail, padding 22/22/24:
  - Codename mono 10px muted uppercase (e.g. `FORM-ASSIST-01`)
  - `<h3>` Space Grotesk 22/600 white
  - Description mono 14/1.5 muted
  - Footer row: dashed top border, mono 10px muted category on left + cyan arrow `→` on right.
- Hover: `translateY(-6px)`, border becomes cyan, thumbnail scales 1.03x, cyan mix-blend-overlay tint at 0.15 opacity, arrow slides 4px right and turns cyan.

**6 cards** (order matters):
| # | Codename | Title | Desc | Status | Category |
|---|---|---|---|---|---|
| 1 | FORM-ASSIST-01 | FormSaathi | Fill any Indian government form — in your own language, with a friend. | In dev | Civic tools |
| 2 | AGRI-MOD-02 | KrishiScan | Photograph a sick leaf. Get a diagnosis and a plan — before the crop is gone. | Beta | Agriculture |
| 3 | BMTC-API-03 | BusBuddy | Bangalore buses, live and readable — for people who don't want to squint at an app. | Live | Civic tools |
| 4 | EDU-TRANS-04 | PathshalaAI | Any textbook, any language, any kid. Learning shouldn't need translation homework. | In dev | Education |
| 5 | RX-DECODE-05 | DoctorSetu | That prescription your doctor scribbled? Here's what it actually says. | In dev | Healthcare |
| 6 | KIRANA-OS-06 | ShopSmart | Kirana inventory over WhatsApp — no app to install, no touchscreen to fight. | Prototype | SMB / commerce |

#### 05 · Mission + Contact

**Layout:** Two-column grid `1.1fr | 1fr`, gap 60px, stacks below 900px.

**Left — Mission:**
- Eyebrow `05 · Mission brief`
- Title `AI for Bharat.` (line break) `Small tools, real problems.`
- Body: *"I want to use AI to help with the ordinary stuff — the messy, everyday problems that Indians run into but nobody makes an app for. Not big flashy things. Small, useful, kind tools that actually work in Hindi, Kannada, Tamil, and the way people really talk."*
- **Mission callout** (`.mission-box`): 1px dashed cyan border, `rgba(23,50,79,0.25)` bg. Amber `CURRENT MISSION` tag mono 10/0.2em, white quote Space Grotesk 20/500: *"Build tools that make daily life in India 1% easier — starting with the things my own family struggles with."*
- **Problem list** — 4 bulleted lines, arrow-prefixed:
  1. Helping grandparents navigate government forms and services
  2. Translating school material into a kid's own language
  3. Turning long PDFs and notices into simple, one-page answers
  4. Small tools for local shops, tutors, and neighbourhood problems
- **See-all-projects button** (`.see-all-btn`): `See all 6 projects →` — bordered pill, mono 11/uppercase, links to `#projects`.

**Right — Contact card** (`.contact-card`):
- `border: 1px solid #1e4a75` with cyan L-shape brackets in opposite corners (`::before` top-left, `::after` bottom-right).
- Heading `Say hello ✈` — 22/600 white
- Desc *"Got an idea, a problem worth solving, or just want to talk about aircraft or chess? Drop me a note."*
- Three fields: `Your name` (required, text), `Email (optional)` (email), `Message` (required, textarea min-height 100px). Labels are mono 10/0.2em uppercase cyan-2.
- Inputs: `rgba(6,17,31,0.6)` bg, 1px `#1e4a75` border, 12/14 padding, focus border cyan.
- Submit button `Transmit message →`: cyan bg, navy text, mono 12/0.2em uppercase 700. Hover → white bg.
- On submit → assembles a `mailto:` URL with encoded subject/body and opens the visitor's default email client. Success message `✓ Opening your email app…` appears in `#form-msg`.

### PROJECT SUB-PAGES — `projects/<slug>/index.html`

All six sub-pages share the exact same template, driven by data from `projects/_shared/projects.json`. Styles live in `projects/_shared/project.css`.

**Top HUD** — identical structure to the landing page but with breadcrumbs instead of nav:
`[A] askappu.in` (link to home) — `Home / Projects / <ProjectName>` — `<CODENAME>` with pulsing green dot.

On mobile (<768px), brand text and status collapse; only breadcrumb remains readable.

#### Section: Hero (`.p-hero`)

Two-column grid `1fr | 1.15fr`, gap 60px, stacks below 900px.

**Left column:**
- Status pill (`.p-status`) — bordered rounded 100px pill with pulsing colored dot. Variants: amber (In development), green `.live` (Live), cyan `.beta` (Beta / Prototype).
- Title (`.p-title`) — `clamp(40px, 6vw, 76px)`, Space Grotesk 700, `#ffffff`, letter-spacing -0.03em. Suffix (`AI`, `Setu`, `Buddy`, `Saathi`, `Scan`, `Smart`) is wrapped in `.accent` styled cyan.
- Tagline — one-liner, `clamp(17px, 1.6vw, 22px)` `--text`, max-width 540px.
- Meta strip — 3 mono key/value blocks (`CODENAME` / `CATEGORY` / `STATUS`).
- CTA row — two buttons:
  - `.btn-primary` — cyan bg, navy text — `Try the app →` links to demo URL (currently `#` placeholder)
  - `.btn-ghost` — bordered transparent, cyan text — `Watch demo` links to video URL (currently `#`)

**Right column:**
- Framed hero image container (`.p-hero-image`) — 3:2 aspect ratio, 1px `#1e4a75` border, cyan L-brackets in opposite corners, `hero.jpg` filling with `object-fit: cover`.
- Bottom-left caption pill: `FIG.01 · <CODENAME> · SYSTEM VIEW` in mono 10px cyan on semi-transparent navy chip.

#### Section: 01 · The problem (`.p-section`)

- Section label `01 · The problem`
- Title `What <ProjectName> is trying to fix.`
- Two-column layout: left is `.p-problem-body` (2 paragraphs, `clamp(16px, 1.15vw, 18px)`, text-wrap: pretty); right is `.p-problem-callout` — dashed border card with amber `Design principle` tag and a white quote (Space Grotesk 20/500).

Every project has a distinct problem lead / body / quote — see `projects.json` for exact copy.

#### Section: 02 · How it works (`.p-section`)

- Section label `02 · How it works`
- Title `Three steps, no learning curve.`
- Grid `repeat(3, 1fr)` on desktop, single column on mobile.

Each step (`.p-step`): 1px `#1e4a75` border, gradient bg, 28/26 padding, min-height 220px.
- Auto-numbered `STEP 01/02/03` (via CSS counter) in top-right mono 10px muted.
- Big cyan mono number (`01`, `02`, `03`) at top — 40px 700.
- H3 title Space Grotesk 20/600 white.
- Body 14.5px muted.

#### Section: 03 · Built with (`.p-section`)

- Section label `03 · Built with`
- Title `The stack.`
- Chip row (`.p-tech`) — each chip: 1px `#1e4a75` border, `rgba(23,50,79,0.35)` bg, 10/16 padding, mono 12px, cyan glow-dot on left.

Sample chips (varies by project): `Gemini 2.5`, `Whisper (voice)`, `Bharat Fonts`, `Next.js`, `Tailwind`, `Supabase`, `TensorFlow Lite`, `Gemini Vision`, `Flutter`, `Firebase`, `BMTC Open API`, `PWA`, `WhatsApp Cloud API`, etc.

#### Section: 04 · Try it & connect (`.p-section`)

Three-column grid (min 220px) of CTA cards (`.p-cta-card`):

1. **Try the app** — arrow icon, links to demo. Copy: *"Open the live demo and take it for a spin."*
2. **Watch the walkthrough** — play-triangle icon, links to video. Copy: *"3-minute video of how <Project> works, end to end."*
3. **Talk to Siddharth** — mail-envelope icon, links to `../../askappu-blueprint.html#problems` (jumps back to the contact form on the landing page).

Each card: 1px border, `rgba(10,26,46,0.6)` bg. Hover: `translateY(-2px)` + border cyan + brighter bg. Cyan 32px SVG icon top-left, white 17/600 h4, muted 13px body, cyan mono `LAUNCH →` / `PLAY →` / `CONTACT →` arrow at bottom.

Below the grid: `← Back to all projects` mono link jumping to `../../askappu-blueprint.html#projects`.

#### Footer

Blueprint-style footer identical to landing page, but with the sub-page trail: `askappu.in / projects / <slug> · © 2026 Siddharth` on left, `<CODENAME> · Bangalore, India` on right.

## Interactions & Behavior

### Paper airplane (landing page)
- Fixed-positioned SVG, 60px wide, `top: 22%`, `left: -80px`.
- `fly` keyframe: 22s linear infinite. Sweeps left→right with keyframe waypoints at 0/5/25/50/75/95/100%. Vertical dips at 4vh, -6vh, 8vh, -4vh. Opacity 0→1→1→0 fade at both ends. `filter: drop-shadow(0 4px 12px rgba(127,215,255,0.25))`.

### Cockpit gauges (landing hero)
- Two SVG-composed circles right of hero content.
- Needle rotates via `spin1` (18s, 20°→120° ease-in-out alternate infinite) and `spin2` (8s, -45°→85°).
- Hidden below 900px width.

### Section reveal
- IntersectionObserver on `.reveal` and every `section`. When 12% visible, adds `.in` class → opacity 0→1, translateY 20px→0 over 800ms ease.

### Hover states
- Landing cards: `translateY(-4px)` + border cyan. 300ms transition.
- Project cards (`.p-card`): `translateY(-6px)` + border cyan + thumbnail scale 1.03 + cyan tint 0.15 mix-blend overlay + arrow slides 4px right and turns cyan.
- Sub-page CTA cards: `translateY(-2px)` + border cyan + brighter bg.
- Buttons: cyan → white on hover (primary), border cyan on hover (ghost).

### Smooth scroll
- `html { scroll-behavior: smooth; }` — all in-page nav links use `#section-id` anchors.

### Mobile nav (landing page)
- Below 768px viewport, the 5-link HUD nav is hidden; a `MENU` button appears in its place. Clicking toggles `.open` class on `<nav id="mainnav">` which drops the nav open as a full-width vertical stack under the HUD, with 1px dashed dividers between links.

### Contact form
- All-vanilla JS. On submit:
  - `preventDefault()`
  - Reads `name`, `email`, `message` from the DOM.
  - Constructs `mailto:hello@askappu.in?subject=Hello from <name>...&body=...` (URL-encoded).
  - Sets `window.location.href` → opens visitor's default email client.
  - Writes `✓ Opening your email app…` to `#form-msg`.
- **Before deploy:** change `const to = 'hello@askappu.in';` to Siddharth's actual address.
- If a real backend is desired later: replace `sendMessage()` with a POST to Formspree / Basin / a serverless function. Keep the field names (`name`, `email`, `message`) identical.

### Responsive behavior
- **Landing page** breakpoints:
  - `< 900px`: About and Mission grids collapse to single column; cockpit gauges hide.
  - `< 768px`: Nav collapses to hamburger, sections tighten to 70px/60px vertical padding, hero centered, facts grid becomes 2-column, interests + projects grids become single column, scroll cue hidden, contact card padding reduced.
  - `< 420px`: Hero title further reduced to 32px, titles cap at 28–32px, hero meta labels tighten.
- **Sub-pages** breakpoints:
  - `< 900px`: Hero grid + How-it-works grid stack.
  - `< 768px`: HUD brand text + status hide, breadcrumb shrinks, section padding 44px vertical, CTA buttons full-width, CTA row becomes single column.
  - `< 420px`: Title 32px, section title 24px.

## State Management

Minimal — static site.

- Contact form: field values held in DOM `input` values; ephemeral `#form-msg` status after submit.
- Landing mobile menu: `.open` class toggled on `<nav id="mainnav">` via inline `onclick`.
- IntersectionObserver `.in` class on sections + `.reveal` elements.

No routing, no persistent storage, no data fetching. Each project page is fully static.

## Design Tokens

### Colors (CSS custom properties on `:root`)

Landing page + all sub-pages share the same palette (defined at the top of `askappu-blueprint.html` and inside `projects/_shared/project.css`):

| Token | Hex | Use |
|---|---|---|
| `--navy-900` | `#06111f` | Page background |
| `--navy-800` | `#0a1a2e` | Card gradient bottom, hero image background |
| `--navy-700` | `#10253d` | Deeper surfaces |
| `--navy-600` | `#17324f` | Card gradient top |
| `--line` | `#1e4a75` | 200px grid lines, all card / input / chip borders |
| `--line-soft` | `#12324f` | 40px inner grid lines, dashed dividers |
| `--cyan` | `#7fd7ff` | Primary accent, headline highlight, hover borders, glow dots, primary CTA bg |
| `--cyan-2` | `#52b6e6` | Secondary cyan (section labels, wing detail lines) |
| `--amber` | `#ffb454` | Callsign, mission tag, `In dev` status, needle |
| `--paper` | `#e8f4ff` | Paper airplane body fill |
| `--text` | `#cfe2f5` | Body copy |
| `--muted` | `#6d8ca8` | De-emphasised text, muted labels |
| `--white` | `#ffffff` | Headings |
| `--ok` | `#4ade80` | `Live` status, `Cleared for takeoff` pulsing dot |

### Typography

- **Display + body**: `Space Grotesk` (400, 500, 600, 700) — Google Fonts
- **Technical labels + code / callsigns**: `JetBrains Mono` (400, 500, 700) — Google Fonts

Both loaded via `<link rel="preconnect">` warmup + a single Google Fonts URL.

**Fluid type scale** (all sizes use `clamp()`):

| Role | Size |
|---|---|
| Hero title (landing) | `clamp(36px, 9vw, 108px)` |
| Sub-page title | `clamp(40px, 6vw, 76px)` |
| Section title | `clamp(30–36px, 4–5vw, 48–64px)` |
| Card / project title | 22px |
| Sub-page step / CTA card title | 17–20px |
| Body | `clamp(16px, 1.15–1.4vw, 18–20px)` |
| Small / meta | 13–15px |
| Mono label | 10–12px, letter-spacing 0.15–0.25em, uppercase |

Line-height: 1.02 for oversized hero, 1.1 for section titles, 1.35 for lead paragraphs, 1.5–1.6 for body.

### Spacing scale

Consistent multiples of 4px: 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 36, 40, 44, 48, 56, 60, 70, 80, 90, 100.

Section padding (**tightened per user request**):
- Desktop landing: 80–100px top/bottom, 6vw side
- Desktop sub-pages: 56px top/bottom, 6vw side
- Mobile (<768px): 60–70px landing, 44px sub-pages
- Only Hero uses `min-height: 100vh`.

### Border radius

- 2px on buttons, inputs, form fields, status pills on cards (tight, technical)
- 50% on brand mark, gauge circles, status dots
- 100px on rounded status pill in sub-page hero

### Shadows / glows

Minimal — this is a blueprint aesthetic, not a soft-shadow one.
- Paper airplane: `drop-shadow(0 4px 12px rgba(127,215,255,0.25))`
- Status dots (`Live`, `Beta`, `In dev`, amber, cyan, green): `box-shadow: 0 0 4–8px <color>`
- Hero avatar initial: `text-shadow: 0 0 20px rgba(127,215,255,0.4)`
- Tech-chip dots: `box-shadow: 0 0 6px #7fd7ff`

### Breakpoints

- `900px` — column-grid collapse
- `768px` — nav collapse, tighter mobile spacing
- `700px` — HUD compaction on sub-pages
- `420px` — extra-narrow phone tuning

## Assets

**Six AI-generated blueprint-style hero images** — one per project — saved as `projects/<slug>/hero.jpg`. Generated via Gemini Nano Banana 2 at 1152×768. Style: dark navy background with cyan blueprint grid, a phone rendered in cyan line-art with screen mockup of the app, amber accent details, monospace annotations like `FORM.ASSIST v1`, technical drawing / engineering blueprint aesthetic.

**All other visuals are inline SVG** — icons (interests + step icons + CTA icons), the compass-badge avatar, the paper airplane, the cockpit gauges. No external icon library or image asset needed.

**Fonts:** loaded from Google Fonts CDN. Self-host if the target environment blocks Google CDN.

**No third-party JS libraries.** Everything is vanilla HTML/CSS/JS.

## Deploy Notes

1. Upload the entire folder structure to any static host (Netlify, Cloudflare Pages, GitHub Pages, Vercel, or the existing askappu.in host). Keep `projects/` alongside the root HTML files — relative paths depend on it.
2. In `askappu-blueprint.html`, find the line `const to = 'hello@askappu.in';` inside the `<script>` block near the bottom and replace with Siddharth's real email address.
3. In each `projects/<slug>/index.html`, replace the placeholder `#` demo/video URLs with real links as projects go live. All 6 sub-pages share the same template — search-and-replace by URL.
4. `projects/_shared/projects.json` mirrors the copy in the sub-pages. If moving to a data-driven build (Astro, Eleventy, Next.js), use it as the source of truth and regenerate the HTML from a single template.
5. No build step, no dependencies, no environment variables required.

## Files In This Bundle

- `README.md` — this document
- `askappu-blueprint.html` — primary landing page
- `askappu-opensky.html` — alternate direction (reference only)
- `projects/_shared/project.css` — shared styles for all sub-pages
- `projects/_shared/projects.json` — project copy (single source of truth)
- `projects/formsaathi/index.html` + `hero.jpg`
- `projects/krishiscan/index.html` + `hero.jpg`
- `projects/busbuddy/index.html` + `hero.jpg`
- `projects/pathshala/index.html` + `hero.jpg`
- `projects/doctorsetu/index.html` + `hero.jpg`
- `projects/shopsmart/index.html` + `hero.jpg`
