# Plan — Step 9: Features (当院の特徴)

## Section
`#features` — 3 "POINT" cards showcasing clinic differentiators

---

## Design Tokens

| Token | Usage |
|---|---|
| `--cream` | Section bg |
| `--white` | Card bg |
| `--primary-lighter` | Image area gradient start |
| `--primary` | POINT number, image icon stroke |
| `--text`, `--text-light`, `--text-muted` | Title, description, POINT label |
| `--border-light` | Card border |
| `--shadow` | Card hover elevation |
| `--radius-lg` | Card |
| `--fs-lg` | Feature title |
| `--fs-sm` | Description |
| `--fs-xs` | "POINT 0X" label |
| DM Sans | "POINT" label |
| Zen Maru Gothic | Feature title |

---

## Features (3 cards)

| POINT | Title | Theme |
|---|---|---|
| 01 | 専門性の高い消化器内科 | Endoscopy camera icon |
| 02 | 丁寧な説明と相談しやすい環境 | Chat bubble icon |
| 03 | 地域医療との連携 | Community/people icon |

---

## HTML Structure

```html
<section id="features" aria-labelledby="features-title">
  <div class="container">
    <div class="features-header reveal">
      <div class="section-label">Features</div>
      <h2 id="features-title" class="section-title">当院の特徴</h2>
      <p class="section-subtitle">...</p>
    </div>
    <div class="features-grid stagger">
      <article class="feature-card reveal">
        <div class="feature-img" aria-hidden="true"><svg .../></div>
        <div class="feature-body">
          <div class="feature-point">POINT <span>01</span></div>
          <h3 class="feature-title">...</h3>
          <p class="feature-desc">...</p>
        </div>
      </article>
      <!-- × 3 -->
    </div>
  </div>
</section>
```

---

## CSS

| Selector | Key rules |
|---|---|
| `#features` | `padding-block: var(--section-pad)`, bg `--cream` |
| `.features-grid` | CSS grid, 1-col → `repeat(3,1fr)` at 769px, gap `1.5rem` |
| `.feature-card` | flex column, bg `--white`, `--border-light`, `--radius-lg`, overflow hidden; hover: `translateY(-4px)`, `--shadow`, `border-color: --primary-lighter` |
| `.feature-img` | `aspect-ratio: 16/10`, gradient `--primary-lighter` → `rgba(90,171,191,0.15)`, flex center |
| `.feature-img svg` | 48×48px, stroke `--primary`, opacity 0.5 |
| `.feature-body` | padding `1.5rem`, flex column, `flex: 1` |
| `.feature-point` | DM Sans, `--fs-xs`, `--text-muted`, uppercase, letter-spacing 0.1em |
| `.feature-point span` | 0.875rem, weight 700, `--primary` |
| `.feature-title` | Zen Maru Gothic, `--fs-lg`, weight 700, `--text`, line-height 1.4 |
| `.feature-desc` | `--fs-sm`, `--text-light`, line-height 1.9 |

---

## Responsive

- Mobile: 1 column
- ≥ 769px: 3 columns

---

## Animations

- `.features-header` — single `.reveal`
- `.features-grid` — `.stagger` parent; each `.feature-card` gets `.reveal`

---

## Accessibility

- `<section>` with `aria-labelledby="features-title"`
- `<article>` + `<h3>` per card
- `.feature-img` has `aria-hidden="true"` (decorative)
- Replace `.feature-img` placeholder with `<img alt="...">` when real photos provided
