# Module 4 — Layouts with Flexbox: Lesson Notes

**Prerequisites:** Module 3 milestone complete
**Read before:** Opening VS Code today

---

## Concept 1 — What is Flexbox?

Flexbox is a CSS layout system that arranges elements in **one direction** at a time — either a row or a column. Without Flexbox, elements stack vertically (block) or sit inline (inline). Flexbox gives you control.

**The key insight:** You apply Flexbox to the **container** (parent), and it affects the **items** (children).

```html
<div class="flex-container">   <!-- parent: gets display: flex -->
  <div class="item">1</div>    <!-- children: become flex items -->
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.flex-container {
  display: flex;   /* This one line turns on Flexbox */
}
```

That's it. The children immediately arrange in a row.

---

## Concept 2 — The Two Axes

Everything in Flexbox revolves around two axes:

```
flex-direction: row (default)
────────────────────────────────
→ → → → MAIN AXIS → → → →
[item 1] [item 2] [item 3]
↕ ↕ ↕ ↕ CROSS AXIS ↕ ↕ ↕ ↕

flex-direction: column
──────────────────────
↓ MAIN AXIS
[item 1]
[item 2]       → → CROSS AXIS
[item 3]
```

`justify-content` controls spacing along the **MAIN** axis.
`align-items` controls spacing along the **CROSS** axis.

---

## Concept 3 — Container Properties (Learn These First)

```css
.container {
  display: flex;

  /* Direction — which way items flow */
  flex-direction: row;         /* left → right (default) */
  flex-direction: column;      /* top → bottom */
  flex-direction: row-reverse; /* right → left */

  /* justify-content — spacing on the MAIN axis */
  justify-content: flex-start;    /* all items at start (default) */
  justify-content: flex-end;      /* all items at end */
  justify-content: center;        /* all items centered */
  justify-content: space-between; /* first + last at edges, equal space between */
  justify-content: space-around;  /* equal space around each item */
  justify-content: space-evenly;  /* equal space between AND at edges */

  /* align-items — alignment on the CROSS axis */
  align-items: stretch;     /* items fill the cross axis (default) */
  align-items: flex-start;  /* items at start of cross axis */
  align-items: flex-end;    /* items at end of cross axis */
  align-items: center;      /* items centered on cross axis */

  /* gap — space between items (no more margin hacks) */
  gap: 1rem;          /* same gap in all directions */
  gap: 1rem 2rem;     /* row-gap column-gap */

  /* flex-wrap — what happens when items don't fit */
  flex-wrap: nowrap;  /* items overflow (default) */
  flex-wrap: wrap;    /* items wrap to next line */
}
```

**Most common combinations:**

```css
/* Center anything horizontally + vertically */
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Navigation: logo left, links right */
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Card row that wraps on small screens */
.card-row {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
}
```

---

## Concept 4 — Item Properties (Learn After Container)

```css
.item {
  /* flex shorthand: grow shrink basis */
  flex: 1;          /* item grows to fill available space equally */
  flex: 0 0 200px;  /* fixed 200px, does not grow or shrink */
  flex: 1 0 300px;  /* starts at 300px, can grow, won't shrink */

  /* align-self — override container's align-items for ONE item */
  align-self: flex-end;  /* this item sits at the bottom */

  /* order — change visual position without changing HTML */
  order: 2;    /* default is 0; higher = appears later */
}
```

---

## Concept 5 — Flexbox Patterns You Will Use Every Day

### Pattern 1 — Navigation Bar
```html
<nav class="site-nav">
  <span class="nav-brand">My Site</span>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>
```

```css
.site-nav {
  display: flex;
  justify-content: space-between; /* brand left, links right */
  align-items: center;            /* vertically centered */
  padding: 1rem 2rem;
  background-color: #1e293b;
}

.nav-links {
  display: flex;      /* links in a row */
  list-style: none;
  gap: 1.5rem;
}

.nav-links a {
  color: #94a3b8;
  text-decoration: none;
}

.nav-links a:hover { color: #ffffff; }
```

### Pattern 2 — Card Row
```html
<section class="cards">
  <article class="card">Card 1</article>
  <article class="card">Card 2</article>
  <article class="card">Card 3</article>
</section>
```

```css
.cards {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap; /* cards wrap on small screens */
}

.card {
  flex: 1;           /* all cards grow equally */
  min-width: 250px;  /* card won't get smaller than this */
  padding: 1.5rem;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
}
```

### Pattern 3 — Centered Hero Section
```html
<section class="hero">
  <h1>Hello, I'm Amara</h1>
  <p>A web developer in training.</p>
  <a href="#projects" class="button">See my work</a>
</section>
```

```css
.hero {
  display: flex;
  flex-direction: column;   /* stack items vertically */
  justify-content: center;  /* center on main (vertical) axis */
  align-items: center;      /* center on cross (horizontal) axis */
  text-align: center;
  min-height: 60vh;
  gap: 1rem;
}
```

---

## Common Mistakes

| Mistake | Fix |
|---|---|
| `display: flex` on the wrong element | Put it on the PARENT, not the children |
| `justify-content` doesn't work | Check `flex-direction` — main axis may be vertical |
| Items don't wrap on small screens | Add `flex-wrap: wrap` to the container |
| Items squash instead of wrapping | Add `min-width` to each item |
| Using margins instead of `gap` | Use `gap` on the container — cleaner and easier |

---

## Exercises

### Exercise 4-A — Centering (Guided)
Create a `<section class="hero">` and center its content perfectly:
- Content must be centered both horizontally AND vertically
- Section must be at least 60vh tall
- Use Flexbox only — no positioning tricks

### Exercise 4-B — Navigation Bar (Semi-guided)
Build a navigation bar with:
- Your name/brand on the left
- 3–4 nav links on the right
- All items vertically centered
- A dark background color
- Hover effect on links
Hint: `justify-content: space-between`

### Exercise 4-C — Card Row (Challenge)
Build a row of 3 cards that:
- Are equal width
- Have a gap between them
- Wrap to 1 column when the screen is narrow (test in DevTools)
- Each card has a title, short paragraph, and a link

### Exercise 4-D — Full Page Layout (Milestone Prep)
Combine your bakery page with Flexbox:
- Flexbox navigation bar
- Flexbox hero section (centered)
- Flexbox card row for menu items
- No CSS Grid, no `float`, no `position: absolute` for layout

---

## Milestone Assessment

**Requirement to advance to Module 5:**

Live demo during Zoom session:
1. Center an element (any element) using Flexbox when asked by instructor
2. Demonstrate your navigation bar (brand left, links right)
3. Demonstrate your card row wrapping at a narrow width

Pull Request must include all three patterns working.
