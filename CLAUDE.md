# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

# Minagawa Clinic — Design System & Implementation Guide

Use this file as context when working on the 皆川クリニック (Minagawa Clinic) website. It documents every design decision, token, and pattern so changes stay consistent.

---

## Project Overview

- **Client:** 皆川クリニック (Minagawa Clinic)
- **Type:** Internal medicine / gastroenterology clinic (内科・消化器内科)
- **Location:** Osaka, Japan
- **Current site:** http://minagawaclinic.main.jp/ — HTML frames from ~2000. This redesign is a complete replacement.
- **Stack:** Single-file HTML, vanilla CSS (custom properties), vanilla JS. No frameworks. Google Fonts CDN only.
- **Source file:** `minagawa-clinic.html`

---

## Development Workflow

There is no build system. Open the file directly in a browser:

```bash
open minagawa-clinic.html        # macOS
# or serve locally to avoid CORS issues with fonts:
npx serve .                       # then open http://localhost:3000
python3 -m http.server 3000       # alternative
```

There are no linting, testing, or compilation steps. All CSS and JS live inside `<style>` and `<script>` tags in `minagawa-clinic.html`. The Google Fonts CDN link requires an internet connection — offline, fonts fall back to system sans-serif.

---

## Code Organization Inside `minagawa-clinic.html`

The single file is structured in this order:
1. `<head>` — charset, viewport, Google Fonts (`Zen Maru Gothic`, `Noto Sans JP`, `DM Sans`), inline `<style>`
2. `<style>` block — `:root` custom properties → reset → base → component classes → section-specific styles → responsive breakpoints → animations
3. `<body>` — sections in page order: `<header>` → `#hero` → `#hours` → `#news` → `#message` → `#services` → `.cta-banner` → `#features` → `#access` → `<footer>` → `.sticky-bar`
4. `<script>` block at end of body — IntersectionObserver (scroll reveal + stagger), mobile menu toggle, header scroll shadow

---

## Color Palette

All colors are defined as CSS custom properties on `:root`. Always use the variable names — never hardcode hex values.

### Primary — Calming Teal

| Token | Hex | Usage |
|---|---|---|
| `--primary` | `#3B8EA5` | Links, icons, active states, section accents |
| `--primary-light` | `#5AABBF` | Gradients (end stop), lighter icon states |
| `--primary-lighter` | `#E8F4F8` | Card backgrounds on hover, service icon bg, tag bg |
| `--primary-dark` | `#2D7A90` | Hover states on primary elements, secondary button text |
| `--primary-deep` | `#1B5E73` | CTA banner gradient start, darkest teal |

### Accent — Warm Terracotta

| Token | Hex | Usage |
|---|---|---|
| `--accent` | `#D4845A` | **CTA buttons only.** This is the conversion color. |
| `--accent-hover` | `#C07248` | CTA hover state |
| `--accent-light` | `#F5E6DC` | Accent backgrounds (phone button in access section) |

**Rule:** Accent is reserved exclusively for booking/call-to-action buttons. Never use it for decorative elements, borders, or text. This keeps the CTA color psychologically "hot" — patients' eyes are trained to associate it with action.

### Neutrals

| Token | Hex | Usage |
|---|---|---|
| `--white` | `#FFFFFF` | Card backgrounds, header bg |
| `--warm-white` | `#FAFBF9` | Page background (has slight warmth) |
| `--cream` | `#F6F5F0` | Alternating section backgrounds (message, features) |
| `--sand` | `#EDE9E0` | Unused reserve — available for future hover states |
| `--text` | `#2C3E40` | Primary body text, headings |
| `--text-light` | `#5A6E72` | Secondary text, descriptions, subtitles |
| `--text-muted` | `#8FA3A8` | Tertiary text, captions, dates, placeholders |
| `--border` | `#E2E8E4` | Card borders, dividers |
| `--border-light` | `#EFF2EE` | Subtle internal borders (table rows, news items) |

### Semantic

| Token | Hex | Usage |
|---|---|---|
| `--open` | `#3B8EA5` | Hours table "open" dot (same as primary) |
| `--closed` | `#C7A08A` | Hours table "closed" dash |
| `--afternoon` | `#7BB5A3` | Reserved for afternoon session indicator if needed |
| `--danger` | `#C4756E` | "Important" news tag, Sunday/holiday column headers |

---

## Typography

### Font Stack

```css
/* Display/Headings — warm, rounded, trustworthy */
font-family: 'Zen Maru Gothic', 'Noto Sans JP', sans-serif;

/* Body — clean, highly legible Japanese */
font-family: 'Noto Sans JP', 'Hiragino Kaku Gothic ProN', sans-serif;

/* English labels/numbers — geometric, modern */
font-family: 'DM Sans', sans-serif;
```

**Why these fonts:**
- **Zen Maru Gothic** — Rounded terminals feel warm and approachable. Medical sites that use sharp geometric fonts feel clinical/cold. This font says "welcoming doctor's office" not "hospital corridor."
- **Noto Sans JP** — Gold standard for Japanese body text. Excellent legibility at small sizes, full character coverage, well-optimized weights.
- **DM Sans** — Used only for English labels ("POINT 01", "News", section labels), numbers in phone/dates. Geometric but not sterile.

### Type Scale

All sizes use CSS custom properties. The scale is designed for mobile-first with clamp() for responsive headings.

| Token | Value | Usage |
|---|---|---|
| `--fs-xs` | `0.75rem` (12px) | Badges, legends, fine print, section labels |
| `--fs-sm` | `0.8125rem` (13px) | Card descriptions, news titles, table text |
| `--fs-base` | `0.9375rem` (15px) | Body text, form labels, general content |
| `--fs-md` | `1.0625rem` (17px) | Service card names, hero subtitle |
| `--fs-lg` | `1.25rem` (20px) | Feature titles, hours header, doctor name |
| `--fs-xl` | `1.5rem` (24px) | Phone number display |
| `--fs-2xl` | `clamp(1.5rem, 3.5vw, 2rem)` | Section titles, message heading, CTA banner |
| `--fs-3xl` | `clamp(1.75rem, 4.5vw, 2.625rem)` | Main section titles |
| `--fs-hero` | `clamp(1.875rem, 5.5vw, 3.25rem)` | Hero headline only |

### Line Heights

- Headings: `1.35–1.45` (tight but readable for Japanese)
- Body text: `1.8–2.0` (generous — Japanese text needs more line-height than English)
- UI elements (buttons, labels): `1.2`

### Font Weights

- `300` — Not currently used. Reserve for light body text variations.
- `400` — Body text, descriptions
- `500` — Navigation links, subtle emphasis, table cells
- `600` — Buttons, section labels, strong emphasis
- `700` — Headings (Zen Maru Gothic), clinic name, key numbers

---

## Spacing System

### Section Padding

```css
--section-pad: clamp(3.5rem, 8vw, 7rem);
```

All major sections use this for top/bottom padding. It scales from 56px (mobile) to 112px (desktop).

### Container

```css
--container: min(90%, 1120px);
```

Content never exceeds 1120px. On mobile, 5% padding on each side.

### Component Spacing Conventions

- **Between section label → title:** `0.5rem`
- **Between title → subtitle:** `0.75rem`
- **Between title block → content grid:** `2–2.5rem`
- **Card internal padding:** `24–28px`
- **Grid gaps:** `16–20px` (cards), `2–3rem` (major grid layouts)

---

## Border Radius Tokens

| Token | Value | Usage |
|---|---|---|
| `--radius-sm` | `6px` | Small buttons, tags, input fields |
| `--radius` | `10px` | Default cards, navigation items, service icons |
| `--radius-lg` | `16px` | Feature cards, service cards |
| `--radius-xl` | `24px` | Hours card, news list, map placeholder, hero image |
| `--radius-full` | `999px` | Pill buttons (CTAs), badges, dots |

---

## Shadow Tokens

| Token | Value | Usage |
|---|---|---|
| `--shadow-sm` | `0 1px 3px rgba(44,62,64,0.06)` | Subtle elevation — scrolled header, news list |
| `--shadow` | `0 4px 20px rgba(44,62,64,0.08)` | Default card elevation — hours card, feature cards on hover |
| `--shadow-lg` | `0 12px 40px rgba(44,62,64,0.12)` | Service cards on hover, prominent elements |
| `--shadow-accent` | `0 8px 30px rgba(212,132,90,0.25)` | CTA buttons — colored shadow for depth |

---

## Component Patterns

### Buttons

**Primary (CTA):**
```
.btn-primary
- Background: var(--accent)
- Text: white
- Border-radius: var(--radius-full) (pill shape)
- Shadow: var(--shadow-accent)
- Hover: darker bg, slight translateY(-1px), deeper shadow
- Always includes a right arrow SVG icon
- Used for: "WEB予約はこちら" ONLY
```

**Secondary:**
```
.btn-secondary
- Background: white
- Text: var(--primary-dark)
- Border: 1.5px solid var(--border)
- Border-radius: var(--radius-full)
- Hover: primary-lighter bg, primary border
- Used for: phone links, secondary actions
```

### Cards

All cards follow this pattern:
- `background: white`
- `border: 1px solid var(--border-light)`
- `border-radius: var(--radius-lg)`
- Hover: `translateY(-4px)` + `box-shadow: var(--shadow-lg)` + `border-color: var(--primary-lighter)`
- Transition: `0.35s cubic-bezier(0.22, 1, 0.36, 1)`

**Service cards** additionally have:
- A top border bar (`::before` pseudo-element) that scales in from left on hover
- An icon container that transitions from `--primary-lighter` bg to `--primary` bg on hover
- A "詳しく見る →" arrow that fades in on hover

### Section Headers

Every section uses this pattern:
```html
<div class="section-label">English Label</div>
<h2 class="section-title">日本語タイトル</h2>
<p class="section-subtitle">Optional description text.</p>
```

The `.section-label` has a left decorative dash via `::before`.

### Hours Table

- Uses colored dots: `.dot-open` (teal circle) and `.dot-closed` (muted horizontal dash)
- Saturday headers get `.sat` class (teal color)
- Sunday/Holiday headers get `.sun` class (danger/red color)
- Wrap in `.hours-card` for the outer container with header containing phone number

---

## Animation System

### Scroll Reveal

All animated elements use the `.reveal` class:

```css
.reveal {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.7s cubic-bezier(0.22, 1, 0.36, 1),
              transform 0.7s cubic-bezier(0.22, 1, 0.36, 1);
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

Triggered by IntersectionObserver with `threshold: 0.1` and `rootMargin: '0px 0px -30px 0px'`.

### Stagger Pattern

Wrap children in a `.stagger` parent. Children automatically get staggered `transition-delay` (0s, 0.08s, 0.16s, etc up to 6 children).

For individual control, use inline `style="transition-delay: 0.12s"`.

### Easing

- **Movement:** `cubic-bezier(0.22, 1, 0.36, 1)` — smooth overshoot for cards, reveals
- **Color/opacity:** `ease` or `0.2s–0.3s` linear

### Specific Animations

- **Hero badge dot:** `pulse-dot` keyframe (scale + opacity, 2s infinite)
- **Service card top bar:** `transform: scaleX(0)` → `scaleX(1)` from left on hover
- **Service arrow:** Fades in + slides right on card hover
- **Button arrow SVG:** `translateX(3px)` on hover
- **Hamburger:** Three spans rotate/fade to form an X

---

## Layout Architecture

### Section Background Alternation

Sections alternate backgrounds to create visual rhythm:

1. Hero — gradient (primary-lighter tones)
2. Hours — `--warm-white`
3. News — `--warm-white` (continuation)
4. Message — `--cream`
5. Services — `--warm-white`
6. CTA Banner — primary gradient (dark teal)
7. Features — `--cream`
8. Access — `--warm-white`
9. Footer — `--text` (dark)

### Responsive Breakpoints

- **Mobile:** Default (< 640px)
- **Tablet:** `640px` — service cards go 2-column
- **Desktop nav:** `769px` — hamburger → desktop nav, grid layouts activate
- **Full desktop:** `960px` — hero gets 2-column with image, services go 3-column

### Mobile-Specific Considerations

- Sticky bottom bar appears below 769px with `env(safe-area-inset-bottom)` padding for notched iPhones
- Footer has extra `padding-bottom: 5rem` on mobile to clear the sticky bar
- Hero badges, phone numbers are tap-targets with `tel:` links
- Hours table scrolls horizontally if needed (min-width: 480px)
- `.hidden-sp` class hides `<br>` tags on mobile for better text flow

---

## CTA Placement Strategy

CTAs appear at these intervals to ensure no patient scrolls more than ~2 screens without a booking opportunity:

1. **Hero** — Primary CTA button + phone button (visible immediately)
2. **Hours card** — Phone number as tappable link (within first scroll)
3. **Mid-page CTA banner** — After services section, full-width teal banner
4. **Access section** — Phone + map buttons
5. **Sticky bottom bar** — Phone + WEB予約, always visible on mobile

---

## Placeholder Content to Replace

When working with real client data, replace these placeholders:

| Placeholder | Location | Notes |
|---|---|---|
| `072-XXX-XXXX` | Header, hero, hours, CTA banner, access, footer, sticky bar | Real clinic phone number |
| `大阪府 ○○市 ○○町 0-0-0` | Header, access table, footer | Real address |
| `〒000-0000` | Access table, footer | Real postal code |
| Hero image frame | `.hero-image-frame` | Replace with `<img>` of clinic exterior |
| Doctor photo frame | `.message-photo-frame` | Replace with `<img>` of doctor/院長 |
| Feature image areas | `.feature-img` | Replace with relevant photos |
| Map placeholder | `.access-map` | Replace with Google Maps `<iframe>` embed |
| `皆川 ○○` | Message section signature | Doctor's full name |
| `○○線「○○」駅` | Access table | Nearest station info |
| `駐車場○台` | Access table | Parking count |
| Hours table data | `#hours` table | Confirm actual hours with client |
| News items | `#news` section | Replace with real announcements |
| WEB予約 links | All `href="#"` on booking buttons | Real booking system URL |

---

## Accessibility Checklist

The current build includes:

- [x] Semantic HTML (`<header>`, `<nav>`, `<main>` implied, `<section>`, `<footer>`, `<article>`)
- [x] `aria-label` on navigation landmarks, logo link, mobile menu, sticky bar
- [x] `aria-expanded` on hamburger button (toggled by JS)
- [x] `aria-label` on status dots in hours table
- [x] `role="dialog"` on mobile menu
- [x] `role="table"` on hours table
- [x] Keyboard: Escape closes mobile menu + returns focus to hamburger
- [x] `focus-visible` outlines on all interactive elements (2px solid primary)
- [x] Color contrast: all text/bg combinations pass WCAG AA
- [x] Tap targets ≥ 44px on mobile

**Still needed for production:**
- [ ] Add `alt` text to all real images when placeholders are replaced
- [ ] Add `<main>` wrapper around content between header and footer
- [ ] Test with screen reader (VoiceOver / NVDA)
- [ ] Add skip-to-content link

---

## File Structure (if expanding beyond single file)

If the client wants a multi-page site later, extract to this structure:

```
/
├── index.html
├── css/
│   ├── variables.css      ← All :root custom properties
│   ├── base.css           ← Reset, typography, utilities
│   ├── components.css     ← Buttons, cards, tables
│   ├── layout.css         ← Header, footer, sticky bar, grids
│   └── pages/
│       └── home.css       ← Hero, section-specific styles
├── js/
│   ├── reveal.js          ← IntersectionObserver scroll animations
│   ├── menu.js            ← Mobile menu toggle
│   └── header.js          ← Scroll shadow behavior
└── assets/
    └── images/            ← Clinic photos, doctor photo
```

---

## Workflow Rules

### Plan Before Building
Before writing any code, output a short implementation plan:
1. Which section you're building
2. Which design tokens and component patterns from this file apply
3. Any responsive behavior needed
4. Expected HTML structure

Wait for approval before writing code.

### Build Section by Section
Do NOT build the entire page in one pass. Build one section at a time in page order:
1. Head + base styles + CSS custom properties
2. Header + navigation
3. Hero
4. Hours
5. News
6. Message
7. Services
8. CTA Banner
9. Features
10. Access
11. Footer + sticky bar
12. Script block (observers, menu, scroll)

After each section, stop and run checks before moving on.

### Checks After Each Section
After completing each section:
1. **Visual check** — Open the file in the browser and take a screenshot. Compare against the design intent described in this file.
2. **Accessibility** — Verify semantic HTML, aria attributes, color contrast, and tap target sizes per the Accessibility Checklist in this file.
3. Report what you found before proceeding to the next section.

### SEO Essentials
Include in the `<head>`:
- Descriptive `<title>` in Japanese with clinic name and specialty
- `<meta name="description">` — clinic summary in Japanese, under 160 chars
- `<meta name="viewport">` (already specified)
- `<link rel="canonical">`
- Open Graph tags (og:title, og:description, og:type, og:url, og:image)
- Structured data: JSON-LD `LocalBusiness` schema with address, phone, hours, medical specialty
- `lang="ja"` on the `<html>` tag

---

## Quick Reference — CSS Variable Cheat Sheet

```css
/* Copy-paste this block when you need to remember the system */

/* Colors */
--primary: #3B8EA5;        /* Teal — links, icons, accents */
--accent: #D4845A;         /* Terracotta — CTA buttons ONLY */
--text: #2C3E40;           /* Dark — headings, body */
--text-light: #5A6E72;     /* Medium — descriptions */
--text-muted: #8FA3A8;     /* Light — captions, dates */
--warm-white: #FAFBF9;     /* Page bg */
--cream: #F6F5F0;          /* Alternating section bg */
--border: #E2E8E4;         /* Card borders */

/* Type */
--fs-base: 0.9375rem;      /* 15px body */
--fs-sm: 0.8125rem;        /* 13px small */
--fs-lg: 1.25rem;          /* 20px subheadings */
--fs-3xl: clamp(…);        /* Section titles */
--fs-hero: clamp(…);       /* Hero only */

/* Space */
--section-pad: clamp(3.5rem, 8vw, 7rem);
--container: min(90%, 1120px);

/* Radius */
--radius: 10px;            /* Default */
--radius-lg: 16px;         /* Cards */
--radius-xl: 24px;         /* Large containers */
--radius-full: 999px;      /* Pills */
```
