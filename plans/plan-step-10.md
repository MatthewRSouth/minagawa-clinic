# Plan — Step 10: Access (アクセス)

## Section
`#access` — clinic location, phone CTA, info table, map placeholder

---

## Design Tokens

| Token | Usage |
|---|---|
| `--warm-white` | Section bg |
| `--white` | Info table bg |
| `--accent` | Phone number, phone icon stroke |
| `--accent-light` (`#F5E6DC`) | Phone button bg |
| `--primary`, `--primary-lighter` | Map placeholder bg/icon, section label |
| `--text`, `--text-light`, `--text-muted` | Table content, dt labels |
| `--border`, `--border-light` | Table card border, row dividers |
| `--shadow-sm` | Phone button, table card |
| `--radius-lg` | Phone button, table card |
| `--radius-xl` | Map area |
| `--fs-xl` | Phone number |
| `--fs-xs` | Labels, dt text, map link |
| `--fs-sm` | Table dd content |
| DM Sans | Phone number, postal code |

---

## HTML Structure

```html
<section id="access" aria-labelledby="access-title">
  <div class="container">
    <div class="access-header reveal">...</div>
    <div class="access-grid reveal">

      <div class="access-info">
        <a href="tel:..." class="access-phone">
          <svg phone aria-hidden/>
          <div class="access-phone-text">
            <span class="access-phone-label">...</span>
            <span class="access-phone-number">072-XXX-XXXX</span>
          </div>
        </a>
        <dl class="access-table">
          <div class="access-row"><dt>住所</dt><dd>...</dd></div>
          <div class="access-row"><dt>最寄駅</dt><dd>...</dd></div>
          <div class="access-row"><dt>駐車場</dt><dd>...</dd></div>
          <div class="access-row"><dt>休診日</dt><dd>...</dd></div>
        </dl>
      </div>

      <div class="access-map-wrap">
        <div class="access-map" aria-label="..."><!-- iframe here --></div>
        <a href="#" class="access-map-link" target="_blank" rel="noopener noreferrer">
          <svg external-link/> Google Mapsで見る
        </a>
      </div>

    </div>
  </div>
</section>
```

---

## CSS

| Selector | Key rules |
|---|---|
| `#access` | `padding-block: var(--section-pad)`, bg `--warm-white` |
| `.access-grid` | flex column → row at 769px, gap `2.5rem`, `align-items: flex-start` |
| `.access-info` | flex column, gap `1.5rem`, `flex: 1` |
| `.access-phone` | flex row, bg `--accent-light`, `--radius-lg`, padding `1.25rem 1.5rem`, `--shadow-sm`; hover: slightly deeper |
| `.access-phone-number` | DM Sans, `--fs-xl`, weight 700, `--accent`, letter-spacing `-0.02em` |
| `.access-table` | bg `--white`, border `--border`, `--radius-lg`, `--shadow-sm`, overflow hidden |
| `.access-row` | flex, padding `0.875rem 1.25rem`, border-bottom `--border-light` |
| `.access-row dt` | `--fs-xs`, weight 600, `--text-muted`, min-width 72px |
| `.access-row dd` | `--fs-sm`, `--text`, line-height 1.7 |
| `.access-map` | `--radius-xl`, `aspect-ratio: 4/3`, bg `--primary-lighter`, flex center column |
| `.access-map-link` | inline-flex, `--fs-xs`, `--primary`, weight 500; hover: underline |

---

## Responsive

- Mobile: single column, info above map
- ≥ 769px: 2-column row (equal flex: 1)

---

## Animations

- `.access-header` — single `.reveal`
- `.access-grid` — single `.reveal`

---

## Placeholders to replace

- `072-XXX-XXXX` → real phone number (also update `href="tel:..."`)
- `〒000-0000` / `大阪府 ○○市 ○○町 0-0-0` → real address
- `○○線「○○」駅 徒歩○分` → real nearest station
- `駐車場○台あり` → real parking count
- `.access-map` placeholder → `<iframe>` Google Maps embed
- Google Maps link `href="#"` → real Google Maps URL

---

## Accessibility

- `<section>` with `aria-labelledby="access-title"`
- Phone link has descriptive `aria-label`
- Map placeholder has `aria-label`
- Map link has `aria-label`, `target="_blank"`, `rel="noopener noreferrer"`
- `<dl>` / `<dt>` / `<dd>` semantics for info table
