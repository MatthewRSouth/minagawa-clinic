# Plan — Step 11: Footer + Sticky Bar

## Footer (`#site-footer`)

### Design Tokens

| Token | Usage |
|---|---|
| `--text` | Footer bg |
| `--white` | Clinic name, nav links |
| `rgba(255,255,255,0.55)` | Specialty, address, labels |
| `rgba(255,255,255,0.12)` | Divider |
| `--primary-light` | Clinic name hover |
| `--accent` | Phone number |
| `--accent-hover` | Phone hover |
| `--fs-lg` | Clinic name |
| `--fs-xl` | Phone number |
| `--fs-sm` | Nav links |
| `--fs-xs` | Labels, address, copyright |
| DM Sans | Phone number |
| Zen Maru Gothic | Clinic name |

### Layout
- Mobile: 1-col grid, `padding-bottom: 7rem` (clear sticky bar)
- ≥ 769px: 3-col grid (`1.4fr 1fr 1.4fr`), `padding-bottom: 2.5rem`

### Columns
1. **Brand** — logo (name + specialty), address
2. **Nav** — 6 anchor links to all sections
3. **Contact** — phone label, tel link, hours note, WEB予約 btn

### CSS
- `#site-footer` — bg `--text`, `padding-block: 3.5rem 2.5rem`
- `.footer-inner` — grid, `padding-bottom: 2.5rem`, border-bottom `rgba(white,0.12)`
- `.footer-logo-name` — Zen Maru Gothic, `--fs-lg`, weight 700, white
- `.footer-address` — `--fs-xs`, `rgba(white,0.55)`, `font-style: normal`
- `.footer-nav a` — `rgba(white,0.75)`; hover: white
- `.footer-tel` — DM Sans, `--fs-xl`, weight 700, `--accent`
- `.footer-bottom small` — `--fs-xs`, `rgba(white,0.4)`

---

## Sticky Bar (`.sticky-bar`)

- `position: fixed`, bottom 0, full width, z-index 900
- bg `--white`, border-top `--border`, shadow above
- `padding-bottom: calc(0.75rem + env(safe-area-inset-bottom))` for notch
- Two items: phone (`.sticky-phone`, teal pill) + book (`.btn-primary`, accent)
- Hidden at ≥ 769px via `display: none`

---

## Accessibility
- `<footer aria-label="サイトフッター">`
- `<nav aria-label="フッターナビゲーション">`
- `<address>` for address (font-style: normal override)
- Phone links have descriptive `aria-label`
- Sticky bar has `role="navigation"` + `aria-label`
