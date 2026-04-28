# Frontend Mentor - QR code component solution

This is a solution to the [QR code component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/qr-code-component-iux_sIO_H). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- Mobile-first workflow

### What I learned

#### 1. CSS Custom Properties (Tokens)

Custom properties should live in `:root` so all elements can access them.

```css
:root {
    --slate-900-color: #1f314f;
    --space-md: 1rem;
    --font-primary: 'Outfit';
    --shadow-card: 0px 4px 16px 4px hsl(220, 15%, 55%);
}
```

#### 2. CSS Reset

Browser default styles add unexpected margins and padding to elements like `<figure>`, `<h1>`, `<p>`, and `<body>`. A reset strips these:

```css
*,
*::before,
*::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
```

- `box-sizing: border-box` makes padding and border included in element width — almost always wanted
- The `<figure>` element has a default browser margin of `1em 40px` — the reset fixes this
- Always include a reset at the top of the stylesheet
- 
#### 3. Responsive Units

**The unit types**

| Unit | Relative to | Best used for |
|---|---|---|
| `px` | Nothing (absolute) | Borders, fixed constraints |
| `rem` | Root font size | Font sizes, spacing, gaps |
| `em` | Parent font size | Avoid — use rem instead |
| `%` | Parent element width | Layout widths |
| `vw` / `vh` | Viewport width / height | Full-screen layouts |

**The key rule for rem**

`1rem` = browser base font size (usually 16px). To convert px to rem, divide by 16:

```
16px  → 1rem
24px  → 1.5rem
40px  → 2.5rem
288px → 18rem
320px → 20rem
```
#### 4. CSS Functions: min()

Picks the smaller value. Use for widths that should cap at a maximum:

```css
width: min(20rem, 90%);
/* On wide screen: 90% > 20rem, so uses 20rem (320px) */
/* On narrow screen: 90% < 20rem, so uses 90%          */
```

- Use **semantic token names** that describe purpose, not value (`--space-md` not `--16px`)
- Consolidate duplicate scales — one spacing scale is enough
- Tokens make site-wide changes easy: update one value, everything updates


#### 5. Images in CSS

```css
.qr-pic {
    width: 100%;      /* fill the container */
    height: auto;     /* maintain aspect ratio — never set a fixed height */
    display: block;   /* removes the default inline gap below images */
    border-radius: 0.625rem;
}
```

- `display: block` removes the small whitespace gap that appears below inline images
- Let the parent container control the image size — the image just fills it
- `height: auto` is essential to prevent distortion

#### 6.Typography

**line-height: use unitless values**

```css
/* Avoid — percentage line-height can cause inheritance bugs */
line-height: 120%;

/* Prefer — unitless is inherited correctly */
line-height: 1.2;
```

**Font fallback stack**

Always declare fallbacks in case the web font fails to load:

```css
font-family: 'Outfit', system-ui, -apple-system, sans-serif;
```

**Google Fonts best practices**

```html
<!-- Preconnect speeds up font loading -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- &display=swap shows fallback text while font loads -->
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@100..900&display=swap" rel="stylesheet">
```

#### 7. Box Shadow as a Token

```css
:root {
    --shadow-card: 0px 4px 16px 4px hsl(220, 15%, 55%);
}

.card {
    box-shadow: var(--shadow-card);
}
```

- Centralizing the shadow makes it easy to update sitewide
- HSL color format is easier to reason about than hex for shadows

#### 8. Semantic HTML

**Element choices**

| Element | Use when |
|---|---|
| `<main>` | Primary content of the page |
| `<article>` | Self-contained content that makes sense independently |
| `<figure>` | Image paired with a caption that describes it |
| `<figcaption>` | The caption for a `<figure>` — can contain headings and paragraphs |
| `<div>` | When no semantic element fits |
| `<section>` | A thematic grouping within a larger document |

**Class names should describe role, not appearance**

```html
<!-- Avoid — describes how it looks -->
<h1 class="horizontal-center-vert-top">

<!-- Prefer — describes what it is -->
<h1 class="card__title">
```