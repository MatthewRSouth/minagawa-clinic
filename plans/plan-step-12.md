# Plan — Step 12: JavaScript

Three functions implemented in the `<script>` block at end of body.

---

## 1. Stagger delays + Scroll Reveal

Applied before the IntersectionObserver is set up, so delays are baked in before observation starts.

```js
document.querySelectorAll('.stagger').forEach((parent) => {
    parent.querySelectorAll('.reveal').forEach((child, i) => {
        child.style.transitionDelay = `${i * 0.08}s`;
    });
});
```

IntersectionObserver: `threshold: 0.1`, `rootMargin: '0px 0px -30px 0px'`
Adds `.visible` class, then unobserves.

---

## 2. Header scroll shadow

```js
const header = document.getElementById('site-header');
window.addEventListener('scroll', () => {
    header.classList.toggle('scrolled', window.scrollY > 10);
}, { passive: true });
```

`.scrolled` CSS (`box-shadow: var(--shadow-sm)`) was already defined in step 1.

---

## 3. Mobile menu toggle

Wires `.hamburger`, `#mobile-menu`, `.mobile-menu-close`.

- `openMenu()`: adds `.open` to hamburger + menu, sets `aria-expanded="true"`, removes `hidden`, locks body scroll
- `closeMenu()`: reverses all above, returns focus to hamburger
- Triggers: hamburger click, close button click, Escape key, any nav link tap inside menu
- Guard: `if (!hamburger || !mobileMenu) return` — safe if elements missing
