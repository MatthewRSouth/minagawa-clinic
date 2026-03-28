# Plan — Step 5: News (お知らせ)

## Section
`#news` — news announcements list

---

## Design Tokens

| Token | Usage |
|---|---|
| `--warm-white` | Section bg (continues from Hours — `padding-top: 0`) |
| `--white` | News list card bg |
| `--primary`, `--primary-lighter` | Default tag text + bg, news title hover color |
| `--danger`, `#fdf0ef` | 重要 tag text + bg |
| `--text` | News title text |
| `--text-muted` | Date text |
| `--border` | Card outer border |
| `--border-light` | Row dividers |
| `--shadow-sm` | News list card shadow |
| `--fs-xs` | Section label, tags, dates |
| `--fs-sm` | News titles |
| `--fs-3xl` | Section title |
| DM Sans | Date digits |
| `--radius-xl` | News list card outer |
| `--radius-sm` | Tags |

---

## HTML Structure

```html
<section id="news" aria-labelledby="news-title">
  <div class="container">

    <div class="news-header reveal">
      <div class="section-label">News</div>
      <h2 id="news-title" class="section-title">お知らせ</h2>
    </div>

    <div class="news-list stagger" role="feed" aria-label="お知らせ一覧">

      <article class="news-item reveal">
        <div class="news-meta">
          <time class="news-date" datetime="2026-03-28">2026.03.28</time>
          <span class="news-tag news-tag--important">重要</span>
        </div>
        <a href="#" class="news-title-link">年末年始の休診についてのご案内</a>
      </article>

      <article class="news-item reveal">
        <div class="news-meta">
          <time class="news-date" datetime="2026-03-10">2026.03.10</time>
          <span class="news-tag">お知らせ</span>
        </div>
        <a href="#" class="news-title-link">インフルエンザ予防接種のご予約を受け付けています</a>
      </article>

      <!-- 2 more items -->

    </div>
  </div>
</section>
```

---

## CSS Additions

| Selector | Key rules |
|---|---|
| `#news` | `padding-block: var(--section-pad)`, `padding-top: 0`, bg `--warm-white` |
| `.news-list` | bg `--white`, border `--border`, `border-radius: var(--radius-xl)`, `box-shadow: var(--shadow-sm)`, overflow hidden, `max-width: 700px`, centered |
| `.news-item` | flex row, `align-items: baseline`, padding `1rem 1.5rem`, border-bottom `--border-light`; last-child no border; hover bg `--primary-lighter` |
| `.news-meta` | flex row, `align-items: center`, gap `0.625rem`, `flex-shrink: 0`, `min-width: 160px` |
| `.news-date` | DM Sans, `--fs-xs`, `--text-muted`, letter-spacing `0.04em` |
| `.news-tag` | `--fs-xs`, weight 500, `border-radius: var(--radius-sm)`, padding `0.2rem 0.6rem`; default: `--primary` on `--primary-lighter` |
| `.news-tag--important` | `--danger` text on `#fdf0ef` bg |
| `.news-title-link` | `--fs-sm`, `--text`, `line-height: 1.6`; hover: color `--primary`, underline via `text-decoration-color` |

---

## Tag Variants

| Class | Text | Background | Usage |
|---|---|---|---|
| `.news-tag` | `--primary` | `--primary-lighter` | General notices |
| `.news-tag--important` | `--danger` | `#fdf0ef` | Closures, urgent notices |

---

## Responsive
No breakpoint changes needed — single column at all widths. Card max-width 700px, centered.

---

## Animations
- `.news-header` — single `.reveal`
- `.news-list` — `.stagger` parent; each `.news-item` gets `.reveal` with auto stagger delay

---

## Accessibility
- `<section>` with `aria-labelledby="news-title"`
- `role="feed"` + `aria-label` on news list container
- `<article>` per item
- `<time datetime="YYYY-MM-DD">` for machine-readable dates
- News title links need descriptive text (not generic "詳しくはこちら")
