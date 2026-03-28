# Plan — Step 8: CTA Banner

## Section
`.cta-banner` — mid-page full-width conversion banner between Services and Features

---

## Design Tokens

| Token | Usage |
|---|---|
| `--primary-deep` | Gradient start (135deg) |
| `--primary-dark` | Gradient end |
| `--white` | All text |
| `--accent` | Primary CTA button bg |
| `--accent-hover` | Primary CTA hover |
| `--shadow-accent` | Primary CTA shadow |
| `--fs-2xl` | Banner headline |
| `--fs-base` | Subtitle, button text |
| `--fs-xs` | Section label |
| `--radius-full` | Both buttons |
| Zen Maru Gothic | Headline |
| DM Sans | Section label |

---

## HTML Structure

```html
<section class="cta-banner" aria-labelledby="cta-banner-title">
  <div class="container">
    <div class="cta-content reveal">
      <div class="section-label">Web Reservation</div>
      <h2 id="cta-banner-title" class="cta-title">...</h2>
      <p class="cta-subtitle">...</p>
      <div class="cta-actions">
        <a href="#" class="btn-primary">WEB予約はこちら <svg arrow/></a>
        <a href="tel:..." class="btn-on-dark"><svg phone/> 072-XXX-XXXX</a>
      </div>
    </div>
  </div>
</section>
```

---

## CSS

| Selector | Key rules |
|---|---|
| `.cta-banner` | `padding-block: var(--section-pad)`, `background: linear-gradient(135deg, --primary-deep, --primary-dark)`, `text-align: center` |
| `.cta-content` | `max-width: 640px`, centered |
| `.cta-banner .section-label` | `color: rgba(255,255,255,0.65)` |
| `.cta-banner .section-label::before` | `background: rgba(255,255,255,0.45)` |
| `.cta-title` | Zen Maru Gothic, `--fs-2xl`, weight 700, white, line-height 1.45 |
| `.cta-subtitle` | `--fs-base`, `rgba(255,255,255,0.8)`, line-height 1.9 |
| `.cta-actions` | flex wrap, justify-content center, gap `1rem` |
| `.btn-primary` | inline-flex, bg `--accent`, white, `--radius-full`, padding `0.875rem 2rem`, `--shadow-accent`; hover: `--accent-hover`, `translateY(-1px)` |
| `.btn-primary svg` | 18×18px; hover: `translateX(3px)` |
| `.btn-on-dark` | inline-flex, bg `rgba(255,255,255,0.12)`, white text, border `1.5px solid rgba(255,255,255,0.3)`, `--radius-full`; hover: bg `rgba(255,255,255,0.22)` |

Note: `.btn-on-dark` is banner-specific. Standard `.btn-secondary` (white bg) is used elsewhere.

---

## Responsive

- Mobile: buttons wrap and go full-width via flex-wrap
- ≥ 640px: buttons sit side-by-side

---

## Animations

- `.cta-content` — single `.reveal`

---

## Accessibility

- `<section>` with `aria-labelledby="cta-banner-title"`
- Both SVG icons have `aria-hidden="true"`
- Phone link uses `href="tel:..."` for native dialing
