# Module 5 — CSS Grid: Lesson Notes

**Prerequisites:** Module 4 milestone complete
**Read before:** Opening VS Code today

---

## Concept 1 — Flexbox vs Grid: When to Use Each

```
Flexbox = one direction          Grid = two directions
────────────────────────         ───────────────────────────
[nav item] [nav item]            [header][header][header]
                                 [sidebar][main  ][main  ]
OR                               [footer][footer][footer]

[card]
[card]
[card]
```

- Use **Flexbox** when you have a single row or column of items
- Use **Grid** when you need rows AND columns at the same time
- You can (and should) use both on the same page — they solve different problems

---

## Concept 2 — Defining a Grid

```css
.grid {
  display: grid;

  /* Define columns */
  grid-template-columns: 200px 1fr;           /* fixed + flexible */
  grid-template-columns: 1fr 1fr 1fr;         /* 3 equal columns */
  grid-template-columns: repeat(3, 1fr);       /* shorthand for above */
  grid-template-columns: repeat(4, minmax(200px, 1fr)); /* responsive */

  /* Define rows (optional — grid auto-creates them) */
  grid-template-rows: auto 1fr auto; /* header, content, footer */

  /* Gap */
  gap: 1.5rem;
  column-gap: 2rem;
  row-gap: 1rem;
}
```

**The `fr` unit — fraction of available space:**
```
grid-template-columns: 1fr 2fr 1fr

Total = 4fr
┌──────┬────────────┬──────┐
│  1fr │    2fr     │  1fr │
│  25% │    50%     │  25% │
└──────┴────────────┴──────┘
```

---

## Concept 3 — Template Areas (Most Readable Method)

Name your grid zones, then assign elements to them:

```css
.page {
  display: grid;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  grid-template-columns: 240px 1fr;
  grid-template-rows: auto 1fr auto;
  min-height: 100dvh;
  gap: 0;
}

/* Assign each element to a named area */
.site-header  { grid-area: header;  }
.site-sidebar { grid-area: sidebar; }
.site-main    { grid-area: main;    }
.site-footer  { grid-area: footer;  }
```

HTML:
```html
<div class="page">
  <header class="site-header">Header</header>
  <aside class="site-sidebar">Sidebar</aside>
  <main class="site-main">Main content</main>
  <footer class="site-footer">Footer</footer>
</div>
```

---

## Concept 4 — Spanning Columns and Rows

```css
.featured-card {
  grid-column: 1 / 3;   /* span from column line 1 to line 3 */
  grid-row: 1 / 2;      /* span row line 1 to line 2 */
}

/* Shorthand with span keyword */
.wide-item {
  grid-column: span 2;  /* span 2 columns from current position */
}
```

---

## Concept 5 — Responsive Grid Without Media Queries

```css
.auto-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}
```

This creates as many columns as will fit, each at least 250px wide.
On a wide screen: 4 columns. On a phone: 1 column. No media query needed.

`auto-fill` vs `auto-fit`:
- `auto-fill` — creates empty columns if there's space
- `auto-fit` — stretches existing items to fill the space ← use this for cards

---

## Full Example — Blog Layout

```css
.blog-layout {
  display: grid;
  grid-template-areas:
    "header"
    "content"
    "sidebar"
    "footer";
  gap: 1.5rem;
  padding: 1rem;
}

/* Tablet and up: sidebar moves alongside content */
@media (min-width: 768px) {
  .blog-layout {
    grid-template-areas:
      "header  header"
      "content sidebar"
      "footer  footer";
    grid-template-columns: 1fr 300px;
  }
}

.blog-header  { grid-area: header; }
.blog-content { grid-area: content; }
.blog-sidebar { grid-area: sidebar; }
.blog-footer  { grid-area: footer; }
```

---

## Exercises

### Exercise 5-A — Basic Grid (Guided)
Create a photo gallery with 4 images:
- 2 columns on mobile, 4 columns on desktop
- 1rem gap between images
- Each image: `width: 100%`, `aspect-ratio: 1`

### Exercise 5-B — Named Areas (Semi-guided)
Build a page layout with named template areas:
- Header full width
- Sidebar (200px) + Main content (rest)
- Footer full width
- Add a media query: stack to single column on mobile

### Exercise 5-C — Auto-fit Card Grid (Challenge)
A card grid where:
- Cards are minimum 250px wide
- Fills the full width with `auto-fit`
- Adds a `grid-column: span 2` "featured" card in position 1
- All without any media queries

---

## Milestone Assessment

Submit a Pull Request with:
- A page using CSS Grid for the overall layout (header/sidebar/main/footer)
- A card section using `auto-fit` that collapses to 1 column on mobile
- HTML and CSS validators: zero errors
