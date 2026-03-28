# Plan — Step 6: Message (院長ご挨拶)

## Section
`#message` — doctor's greeting / from the director

---

## Design Tokens

| Token | Usage |
|---|---|
| `--cream` | Section bg |
| `--white` | Message card bg |
| `--primary-lighter` | Photo frame bg |
| `--text`, `--text-light`, `--text-muted` | Body, description, role label |
| `--border-light` | Card border |
| `--shadow` | Card elevation |
| `--fs-3xl` | Section title |
| `--fs-lg` | Doctor name |
| `--fs-md` | Lead paragraph |
| `--fs-base` | Body paragraphs |
| `--fs-xs` | Role label |
| `--radius-xl` | Photo frame |
| `--radius-lg` | Message card |
| Zen Maru Gothic | Doctor name, section title |
| Noto Sans JP | Body paragraphs |
| DM Sans | "Message" label, role label |

---

## HTML Structure

```html
<section id="message" aria-labelledby="message-title">
  <div class="container">

    <div class="message-header reveal">
      <div class="section-label">Message</div>
      <h2 id="message-title" class="section-title">院長ご挨拶</h2>
    </div>

    <div class="message-card reveal">

      <div class="message-photo">
        <div class="message-photo-frame" aria-label="院長写真（準備中）">
          <!-- placeholder SVG icon + label -->
        </div>
        <div class="message-signature">
          <span class="message-role">Director</span>
          <span class="message-name">皆川 ○○</span>
        </div>
      </div>

      <div class="message-body">
        <p class="message-lead">Lead sentence...</p>
        <p>Body paragraph...</p>
        <!-- more paragraphs -->
      </div>

    </div>
  </div>
</section>
```

---

## CSS

| Selector | Key rules |
|---|---|
| `#message` | `padding-block: var(--section-pad)`, bg `--cream` |
| `.message-card` | flex column → row at 769px, gap 2rem → 3rem, bg `--white`, border `--border-light`, `border-radius: var(--radius-lg)`, `box-shadow: var(--shadow)`, padding 2rem → 2.5rem, max-width 900px, centered |
| `.message-photo` | `flex-shrink: 0`, flex column centered, width 240px at desktop |
| `.message-photo-frame` | aspect-ratio 3/4, `border-radius: var(--radius-xl)`, bg `--primary-lighter`, flex column centered |
| `.message-role` | DM Sans, `--fs-xs`, `--text-muted`, uppercase, letter-spacing 0.1em |
| `.message-name` | Zen Maru Gothic, `--fs-lg`, weight 700, `--text` |
| `.message-body` | `flex: 1`, flex column, justify-content center |
| `.message-lead` | `--fs-md`, weight 500, `--text`, line-height 2 |
| `p` in `.message-body` | `--fs-base`, `--text-light`, line-height 2, margin-bottom 1rem |

---

## Responsive

- Mobile: card flex-direction column, photo centered above text
- ≥ 769px: card flex-direction row, photo 240px wide on left, text fills remaining space

---

## Animations

- `.message-header` — single `.reveal`
- `.message-card` — single `.reveal`

---

## Accessibility

- `<section>` with `aria-labelledby="message-title"`
- Photo frame has `aria-label="院長写真（準備中）"`
- Placeholder SVG has `aria-hidden="true"`
- Replace placeholder with `<img alt="院長 皆川○○">` when real photo provided
