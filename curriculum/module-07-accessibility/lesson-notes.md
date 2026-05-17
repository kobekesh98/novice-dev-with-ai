# Module 7 — Web Accessibility: Lesson Notes

**Prerequisites:** Module 6 milestone complete
**Read before:** Opening VS Code today

---

## Concept 1 — What is Web Accessibility?

Web accessibility means building websites that **everyone can use** — including people who:
- Cannot see (use screen readers like NVDA, JAWS, VoiceOver)
- Have low vision (use zoom or high contrast)
- Cannot use a mouse (use keyboard only or switch devices)
- Have cognitive differences (benefit from clear structure and language)
- Have motor difficulties (need large tap targets, no time limits)

**The key insight:** If you have done Modules 1–6 correctly — semantic HTML, proper headings, alt text, form labels, responsive design — you are already ahead of most websites.

Accessibility is not a layer you add at the end. It is the result of writing correct HTML from the start.

---

## Concept 2 — The Four WCAG Principles (POUR)

WCAG = Web Content Accessibility Guidelines (the international standard)

| Principle | Meaning | Example |
|---|---|---|
| **P**erceivable | Content can be seen or heard | Alt text on images |
| **O**perable | Users can navigate and interact | Keyboard-accessible menus |
| **U**nderstandable | Content is clear and predictable | Descriptive labels on forms |
| **R**obust | Works with current and future assistive tech | Valid, semantic HTML |

---

## Concept 3 — Screen Readers and Landmarks

Screen readers navigate pages using landmark regions. This is why semantic HTML is critical:

```
When a screen reader user presses the landmark shortcut, they hear:
"Navigation"        → <nav>
"Main"              → <main>
"Banner"            → <header>
"Complementary"     → <aside>
"Content info"      → <footer>
```

If you used `<div class="nav">` instead of `<nav>`, the screen reader announces: nothing.

They also navigate by **headings** — your h1→h2→h3 hierarchy is a navigation menu
for screen reader users. If headings are skipped or out of order, they get lost.

---

## Concept 4 — Color Contrast

Text must have sufficient contrast against its background so people with low vision can read it.

**Minimum ratios (WCAG AA):**
- Normal text (below 18px): **4.5:1** contrast ratio
- Large text (18px+ or 14px+ bold): **3:1** contrast ratio
- UI components (buttons, inputs): **3:1**

**Check your colors:**
- WAVE: https://wave.webaim.org
- Contrast checker: https://webaim.org/resources/contrastchecker/
- Browser DevTools: DevTools → Inspect → click the color swatch → ratio shows

**Common failures:**
```css
/* FAIL — light grey text on white */
color: #cccccc;  /* contrast ratio ≈ 1.6:1 */

/* PASS — dark text on white */
color: #374151;  /* contrast ratio ≈ 10.7:1 */

/* FAIL — white text on light blue */
color: white; background: #93c5fd; /* ≈ 2.5:1 */

/* PASS — white text on dark blue */
color: white; background: #1d4ed8; /* ≈ 7.2:1 */
```

---

## Concept 5 — Keyboard Navigation

Every interactive element must be reachable and usable with a keyboard.

**Test it right now:**
1. Close your mouse (or unplug it)
2. Press `Tab` — you should be able to move through all links, buttons, and inputs
3. Press `Enter` or `Space` on a button — it should activate
4. Press `Shift+Tab` to go backwards

**Focus styles — NEVER remove without replacing:**
```css
/* WRONG — breaks keyboard navigation for all users */
:focus { outline: none; }

/* CORRECT — visible custom focus style */
:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 3px;
  border-radius: 2px;
}
```

The blue outline is not ugly — removing it is a disability for keyboard users.

---

## Concept 6 — Skip Navigation Link

Users who navigate by keyboard have to Tab through every nav link on every page load.
A skip link lets them jump straight to the main content:

```html
<!-- First element inside <body> -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<header>...</header>
<main id="main-content">...</main>
```

```css
.skip-link {
  position: absolute;
  top: -40px;          /* hidden above the viewport by default */
  left: 0;
  background: #2563eb;
  color: white;
  padding: 0.5rem 1rem;
  text-decoration: none;
  z-index: 100;
}

.skip-link:focus {
  top: 0;              /* slides into view when focused by keyboard */
}
```

---

## Concept 7 — Images and Alt Text (Review)

```html
<!-- Informative image — describe what it shows -->
<img src="chart.png" alt="Bar chart showing a 40% increase in student enrollment from 2024 to 2026">

<!-- Decorative image — empty alt -->
<img src="divider.svg" alt="">

<!-- Image that IS a link — describe the destination, not the image -->
<a href="/home">
  <img src="logo.png" alt="Return to homepage">
</a>

<!-- Complex image — link to a description -->
<figure>
  <img src="infographic.png" alt="Infographic showing the 3 layers of a webpage" aria-describedby="infographic-desc">
  <figcaption id="infographic-desc">
    HTML provides structure, CSS controls appearance, and JavaScript adds behaviour.
  </figcaption>
</figure>
```

---

## Concept 8 — Form Accessibility (Review)

```html
<form>
  <!-- Method 1: label with for/id -->
  <label for="name">Full name <span aria-hidden="true">*</span></label>
  <input type="text" id="name" name="name" required aria-required="true">

  <!-- Group related inputs -->
  <fieldset>
    <legend>Contact preference</legend>
    <label><input type="radio" name="contact" value="email"> Email</label>
    <label><input type="radio" name="contact" value="phone"> Phone</label>
  </fieldset>

  <!-- Error message linked to input -->
  <label for="email">Email address</label>
  <input type="email" id="email" name="email" aria-describedby="email-error">
  <span id="email-error" class="error" role="alert">
    Please enter a valid email address.
  </span>
</form>
```

---

## Concept 9 — ARIA (Use Rarely)

ARIA (Accessible Rich Internet Applications) attributes add semantic information that HTML alone can't express. But:

> **First rule of ARIA: Don't use ARIA.**
> Use native HTML elements instead.

```html
<!-- WRONG — adds ARIA to a div to make a button -->
<div role="button" tabindex="0" onclick="submit()">Submit</div>

<!-- CORRECT — just use a button -->
<button type="submit">Submit</button>
```

Only use ARIA when native HTML cannot do the job (complex custom widgets).

---

## Audit Checklist

Run through this for your project before submitting:

**Structure:**
- [ ] One `<h1>` only
- [ ] Heading levels not skipped
- [ ] Landmark regions: header, nav, main, footer

**Images:**
- [ ] All meaningful images have descriptive `alt`
- [ ] All decorative images have `alt=""`
- [ ] No `alt="image"` or `alt="photo"`

**Links:**
- [ ] No "click here" or "read more" link text
- [ ] External links have `rel="noopener noreferrer"`
- [ ] Every link makes sense when read in isolation

**Forms:**
- [ ] Every input has a linked `<label>`
- [ ] Required fields use `required` attribute
- [ ] Error messages are associated with inputs

**Color and Contrast:**
- [ ] Text contrast passes 4.5:1 (checked with WAVE)
- [ ] No information conveyed by color alone

**Keyboard:**
- [ ] Tab through entire page — everything reachable
- [ ] Focus styles visible on all interactive elements
- [ ] Skip link present if navigation is long

---

## Exercises

### Exercise 7-A — WAVE Audit (Guided)
Run your project through WAVE (https://wave.webaim.org).
List every error and alert found. Fix ALL errors before the next step.

### Exercise 7-B — Keyboard-Only Test
Unplug or ignore your mouse for 10 minutes.
Navigate your page using only Tab, Shift+Tab, Enter, and Space.
Write down every problem you encounter.

### Exercise 7-C — Contrast Check
Use the WAVE contrast checker on all your text.
Fix any that fail 4.5:1. Document the before/after colors in a comment.

### Exercise 7-D — Skip Link
Add a skip navigation link to your page.
Test it with keyboard only — press Tab once after page loads.

---

## Milestone Assessment

Submit a Pull Request with:
- WAVE audit: zero errors (include a screenshot)
- Keyboard test: document that you tested with keyboard only
- Skip link present and working
- All 5 items in audit checklist confirmed in PR description
