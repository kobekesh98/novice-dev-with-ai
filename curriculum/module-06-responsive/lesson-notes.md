# Module 6 — Responsive Design: Lesson Notes

**Prerequisites:** Module 5 milestone complete
**Read before:** Opening VS Code today

---

## Concept 1 — What is Responsive Design?

A responsive website looks good and works correctly on **any screen size**.
Same HTML, same CSS file — the layout adjusts based on the device width.

**Why it matters:** Most website traffic is on mobile. If your site breaks on a phone,
most people will leave immediately.

---

## Concept 2 — The Viewport Meta Tag (Already In Your Boilerplate)

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Without this, mobile browsers zoom out and show a miniature desktop version.
With it, the browser uses the actual device width. You already have this in every page.

---

## Concept 3 — Mobile First (The Right Approach)

**Mobile first** = write base styles for the smallest screen first.
Then add media queries for larger screens.

```css
/* BASE — small mobile (no media query needed) */
.card-grid {
  display: grid;
  grid-template-columns: 1fr;  /* 1 column on mobile */
  gap: 1rem;
}

/* Tablet: 640px and wider */
@media (min-width: 640px) {
  .card-grid {
    grid-template-columns: 1fr 1fr;  /* 2 columns */
    gap: 1.5rem;
  }
}

/* Desktop: 1024px and wider */
@media (min-width: 1024px) {
  .card-grid {
    grid-template-columns: repeat(3, 1fr);  /* 3 columns */
  }
}
```

**Why mobile first instead of desktop first?**
- More users are on mobile
- It's easier to add complexity than strip it away
- Forces you to prioritize the most important content

---

## Concept 4 — Media Query Syntax

```css
/* Min-width: "from this size UP" */
@media (min-width: 768px) {
  /* styles for screens 768px wide and larger */
}

/* Max-width: "up to this size" (desktop-first — avoid this approach) */
@media (max-width: 767px) {
  /* styles for screens smaller than 768px */
}

/* Combining: a range */
@media (min-width: 640px) and (max-width: 1023px) {
  /* tablet only */
}

/* Dark mode preference */
@media (prefers-color-scheme: dark) {
  /* dark mode styles */
}

/* Reduced motion preference (accessibility) */
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !important; }
}
```

**Common breakpoints:**

| Name | Width | Target |
|---|---|---|
| Small mobile | 360px–479px | Small phones |
| Mobile | 480px–639px | Most phones |
| Large mobile | 640px | Large phones, small tablets |
| Tablet | 768px | iPads, tablets |
| Desktop | 1024px | Laptops, desktops |
| Wide | 1280px | Large monitors |

---

## Concept 5 — Responsive Typography

```css
/* Method 1: clamp() — scales between a min and max */
h1 {
  font-size: clamp(1.75rem, 5vw, 3rem);
  /* minimum | preferred (viewport-based) | maximum */
}

/* Method 2: Simple breakpoints */
h1 { font-size: 1.75rem; }

@media (min-width: 768px) {
  h1 { font-size: 2.5rem; }
}

@media (min-width: 1024px) {
  h1 { font-size: 3rem; }
}
```

---

## Concept 6 — Responsive Images

```css
/* Always do this — prevents images from overflowing their container */
img {
  max-width: 100%;
  height: auto;       /* maintains aspect ratio */
  display: block;     /* removes the inline bottom gap */
}

/* Modern: maintain aspect ratio */
.card__image {
  width: 100%;
  aspect-ratio: 16 / 9;
  object-fit: cover;   /* crops to fill the box */
}
```

---

## Concept 7 — Testing Responsive Layouts

**Chrome DevTools — Device Toolbar:**
1. Press `F12` to open DevTools
2. Press `Ctrl+Shift+M` (or click the phone/tablet icon)
3. Select a preset device OR type a custom width
4. Check: 375px (iPhone SE), 768px (iPad), 1280px (desktop)

**What to look for:**
- Text is readable (not too small)
- No horizontal scrollbar
- Buttons and links are large enough to tap (minimum 44x44px)
- Images scale correctly
- Layout doesn't break or overflow

---

## Full Responsive Page Example

```css
/* === Reset === */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

/* === Base (mobile) === */
body {
  font-family: system-ui, sans-serif;
  font-size: 1rem;
  line-height: 1.6;
}

.site-nav {
  display: flex;
  flex-direction: column;  /* stacked on mobile */
  gap: 1rem;
  padding: 1rem;
  background: #1e293b;
}

.nav-links {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  list-style: none;
}

.hero {
  padding: 3rem 1rem;
  text-align: center;
}

.hero h1 { font-size: clamp(1.75rem, 5vw, 3rem); }

.card-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
  padding: 1rem;
}

/* === Tablet (768px+) === */
@media (min-width: 768px) {
  .site-nav {
    flex-direction: row;           /* horizontal nav */
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
  }

  .card-grid {
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
    padding: 2rem;
  }
}

/* === Desktop (1024px+) === */
@media (min-width: 1024px) {
  .card-grid {
    grid-template-columns: repeat(3, 1fr);
  }

  .hero { padding: 6rem 2rem; }
}
```

---

## Exercises

### Exercise 6-A — Add Media Queries (Guided)
Take your bakery page from Module 2–4. Add:
- 1-column layout on mobile (base)
- 2-column card grid at 640px
- 3-column card grid at 1024px
- Nav: stacked on mobile, horizontal at 768px

### Exercise 6-B — Responsive Typography
Apply `clamp()` to all headings so they scale smoothly between sizes.
Test at 375px, 768px, and 1280px in DevTools.

### Exercise 6-C — Responsive Images
Find 3 images. Make them responsive. Use `aspect-ratio: 16/9` and `object-fit: cover`.
Test that they never overflow and always look correct at all sizes.

### Exercise 6-D — Full Responsive Audit (Milestone Prep)
Open your full project at these exact widths and screenshot each:
- 375px, 640px, 768px, 1024px, 1280px
Include all 5 screenshots in your PR description.

---

## Milestone Assessment

Submit a Pull Request with:
- Base (mobile-first) CSS with no media queries
- At least 2 breakpoints (640px and 1024px)
- Navigation collapses and expands correctly
- Card grid changes columns at breakpoints
- 5 DevTools screenshots in the PR description
