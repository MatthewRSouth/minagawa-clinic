# Plan — Step 7: Services (診療案内)

## Section
`#services` — clinic service cards grid

---

## Design Tokens

| Token | Usage |
|---|---|
| `--warm-white` | Section bg |
| `--white` | Card bg |
| `--primary`, `--primary-light` | Top bar gradient, icon hover bg, arrow color |
| `--primary-lighter` | Icon container default bg |
| `--primary-dark` | Arrow label text |
| `--text`, `--text-light` | Card title, description |
| `--border-light` | Card border |
| `--shadow-lg` | Card hover elevation |
| `--radius-lg` | Card |
| `--radius` | Icon container |
| `--fs-3xl` | Section title |
| `--fs-md` | Service name |
| `--fs-sm` | Description |
| `--fs-xs` | Arrow label |
| Zen Maru Gothic | Service name |
| DM Sans | "Services" label |

---

## Services (6 cards)

| # | Title | Description |
|---|---|---|
| 1 | 内科 | 風邪・発熱・咳・倦怠感など |
| 2 | 消化器内科 | 胃もたれ・腹痛・逆流性食道炎など |
| 3 | 胃カメラ検査 | 上部消化管内視鏡 |
| 4 | 大腸カメラ検査 | 下部消化管内視鏡・ポリープ切除 |
| 5 | 生活習慣病 | 高血圧・糖尿病・脂質異常症 |
| 6 | 健診・予防接種 | 各種健診・ワクチン |

---

## HTML Structure

```html
<section id="services" aria-labelledby="services-title">
  <div class="container">
    <div class="services-header reveal">
      <div class="section-label">Services</div>
      <h2 id="services-title" class="section-title">診療案内</h2>
      <p class="section-subtitle">...</p>
    </div>
    <div class="services-grid stagger">
      <article class="service-card reveal">
        <div class="service-icon-wrap"><svg .../></div>
        <h3 class="service-name">...</h3>
        <p class="service-desc">...</p>
        <span class="service-arrow" aria-hidden="true">詳しく見る →</span>
      </article>
      <!-- × 6 -->
    </div>
  </div>
</section>
```

---

## CSS

| Selector | Key rules |
|---|---|
| `#services` | `padding-block: var(--section-pad)`, bg `--warm-white` |
| `.services-grid` | CSS grid, 1-col → 2-col at 640px → 3-col at 960px, gap `1.25rem` |
| `.service-card` | flex column, bg `--white`, border `--border-light`, `--radius-lg`, padding `1.75rem`, overflow hidden, `transition 0.35s cubic-bezier(0.22,1,0.36,1)` |
| `.service-card::before` | Top bar: absolute, 3px height, gradient `--primary`→`--primary-light`, `scaleX(0)` → `scaleX(1)` on hover |
| `.service-card:hover` | `translateY(-4px)`, `--shadow-lg`, `border-color: --primary-lighter` |
| `.service-icon-wrap` | 52×52px, `--radius`, bg `--primary-lighter` → `--primary` on hover |
| `.service-icon-wrap svg` | 26×26px, stroke `--primary` → white on hover |
| `.service-name` | Zen Maru Gothic, `--fs-md`, weight 700, `--text` |
| `.service-desc` | `--fs-sm`, `--text-light`, line-height 1.8, `flex: 1` |
| `.service-arrow` | `--fs-xs`, `--primary-dark`, weight 600, opacity 0 + `translateX(-4px)` → visible on hover |

---

## Responsive

- Mobile (default): 1 column
- ≥ 640px: 2 columns
- ≥ 960px: 3 columns

---

## Animations

- `.services-header` — single `.reveal`
- `.services-grid` — `.stagger` parent; each `.service-card` gets `.reveal`

---

## Accessibility

- `<section>` with `aria-labelledby="services-title"`
- `<article>` per card with `<h3>` heading
- All SVG icons have `aria-hidden="true"`
- `.service-arrow` has `aria-hidden="true"` (decorative)
