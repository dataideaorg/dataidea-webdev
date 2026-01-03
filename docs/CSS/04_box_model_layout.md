# Box Model and Layout

Understand the CSS box model - the foundation of how elements are sized and spaced. Learn to control layout and positioning.

## The Box Model

Every HTML element is a rectangular box with four areas:

```
┌─────────────────────────────────┐
│         Margin (outside)         │
│  ┌───────────────────────────┐  │
│  │      Border               │  │
│  │  ┌─────────────────────┐  │  │
│  │  │    Padding          │  │  │
│  │  │  ┌───────────────┐  │  │  │
│  │  │  │   Content     │  │  │  │
│  │  │  └───────────────┘  │  │  │
│  │  └─────────────────────┘  │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

### Box Model Components

1. **Content:** The actual content (text, images)
2. **Padding:** Space inside the element, around the content
3. **Border:** Line around the padding
4. **Margin:** Space outside the element, between elements

## Width and Height

Control element size:

```css
div {
    width: 300px;
    height: 200px;
}
```

### Box-Sizing

Controls how width/height are calculated:

```css
/* Default: content-box */
div {
    box-sizing: content-box;
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    /* Total width = 300 + 40 + 10 = 350px */
}

/* Better: border-box */
div {
    box-sizing: border-box;
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    /* Total width = 300px (includes padding and border) */
}
```

!!! tip "Use border-box"
    Set `box-sizing: border-box` globally for easier sizing:
    ```css
    * {
        box-sizing: border-box;
    }
    ```

## Padding

Space inside the element, around content:

```css
div {
    padding: 20px; /* All sides */
}

p {
    padding-top: 10px;
    padding-right: 15px;
    padding-bottom: 10px;
    padding-left: 15px;
}
```

### Shorthand

```css
/* One value - all sides */
padding: 20px;

/* Two values - vertical, horizontal */
padding: 10px 20px;

/* Three values - top, horizontal, bottom */
padding: 10px 20px 15px;

/* Four values - top, right, bottom, left */
padding: 10px 15px 20px 25px;
```

## Border

Line around the element:

```css
div {
    border: 2px solid black;
}
```

### Border Properties

```css
div {
    border-width: 2px;
    border-style: solid;
    border-color: black;
}

/* Individual sides */
div {
    border-top: 1px solid red;
    border-right: 2px dashed blue;
    border-bottom: 3px dotted green;
    border-left: 4px double orange;
}
```

### Border Styles

- `solid` - Solid line
- `dashed` - Dashed line
- `dotted` - Dotted line
- `double` - Double line
- `none` - No border
- `hidden` - Hidden border

### Border Radius

Rounded corners:

```css
div {
    border-radius: 10px; /* All corners */
}

button {
    border-radius: 50%; /* Circle */
}

.card {
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}
```

## Margin

Space outside the element, between elements:

```css
h1 {
    margin: 20px; /* All sides */
}

p {
    margin-top: 10px;
    margin-bottom: 20px;
}
```

### Shorthand

Same as padding:

```css
margin: 20px;              /* All sides */
margin: 10px 20px;         /* Vertical, horizontal */
margin: 10px 20px 15px;    /* Top, horizontal, bottom */
margin: 10px 15px 20px 25px; /* Top, right, bottom, left */
```

### Auto Margin

Center elements horizontally:

```css
.container {
    width: 800px;
    margin: 0 auto; /* Top/bottom: 0, Left/right: auto */
}
```

### Negative Margin

Can overlap elements:

```css
.overlap {
    margin-top: -20px;
}
```

## Display Property

Controls how elements are displayed:

### Block

Takes full width, starts on new line:

```css
div {
    display: block;
}
```

**Block elements:** `<div>`, `<p>`, `<h1>-<h6>`, `<section>`, `<article>`

### Inline

Takes only needed width, stays on same line:

```css
span {
    display: inline;
}
```

**Inline elements:** `<span>`, `<a>`, `<strong>`, `<em>`

### Inline-Block

Combines both: inline flow, but can have width/height:

```css
.button {
    display: inline-block;
    width: 100px;
    height: 40px;
}
```

### None

Hides element completely:

```css
.hidden {
    display: none;
}
```

## Positioning

Control where elements appear:

### Static (Default)

Normal document flow:

```css
div {
    position: static;
}
```

### Relative

Positioned relative to normal position:

```css
div {
    position: relative;
    top: 20px;
    left: 10px;
}
```

### Absolute

Positioned relative to nearest positioned ancestor:

```css
div {
    position: absolute;
    top: 0;
    right: 0;
}
```

### Fixed

Positioned relative to viewport (stays on screen when scrolling):

```css
.header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
}
```

### Sticky

Sticks when scrolling reaches threshold:

```css
.navbar {
    position: sticky;
    top: 0;
}
```

## Float

Float elements left or right (legacy, use Flexbox/Grid instead):

```css
img {
    float: left;
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}
```

## Z-Index

Control stacking order of positioned elements:

```css
.overlay {
    position: absolute;
    z-index: 10;
}

.modal {
    position: fixed;
    z-index: 1000;
}
```

Higher z-index appears on top.

## Complete Layout Example

```css
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
}

.container {
    width: 1200px;
    max-width: 100%;
    margin: 0 auto;
    padding: 0 20px;
}

.header {
    background-color: #333;
    color: white;
    padding: 20px;
    position: sticky;
    top: 0;
    z-index: 100;
}

.main-content {
    padding: 40px 0;
}

.card {
    background-color: white;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.button {
    display: inline-block;
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    text-decoration: none;
}

.button:hover {
    background-color: #0056b3;
}
```

## Common Layout Patterns

### Centered Container

```css
.container {
    width: 1200px;
    max-width: 100%;
    margin: 0 auto;
    padding: 0 20px;
}
```

### Card Layout

```css
.card {
    background: white;
    border-radius: 8px;
    padding: 20px;
    margin: 20px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}
```

### Fixed Header

```css
.header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background: white;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

body {
    padding-top: 60px; /* Space for fixed header */
}
```

## Best Practices

1. **Use border-box:** Makes sizing predictable
2. **Reset margins/padding:** Start with consistent defaults
3. **Use max-width:** Prevent content from being too wide
4. **Margin for spacing:** Use margin between elements
5. **Padding for internal space:** Use padding inside elements
6. **Avoid fixed widths:** Use percentages or max-width for responsiveness

## Common Mistakes

### 1. Not Using border-box

```css
/* ❌ Wrong */
div {
    width: 300px;
    padding: 20px;
    /* Total width = 340px (unexpected!) */
}

/* ✅ Correct */
* {
    box-sizing: border-box;
}

div {
    width: 300px;
    padding: 20px;
    /* Total width = 300px */
}
```

### 2. Using Padding for Element Spacing

```css
/* ❌ Wrong */
.card {
    padding-bottom: 20px; /* Creates space inside */
}

/* ✅ Correct */
.card {
    margin-bottom: 20px; /* Creates space outside */
}
```

### 3. Forgetting to Clear Floats

```css
/* ❌ Wrong */
.container::after {
    /* Missing clearfix */
}

/* ✅ Correct */
.container::after {
    content: "";
    display: table;
    clear: both;
}
```

## Practice Exercise

Create CSS for:

1. A centered container (max-width 1200px)
2. Cards with padding, border-radius, and shadow
3. A fixed header at the top
4. Buttons with padding and border-radius
5. Proper spacing between sections using margin
6. A layout using display: inline-block for side-by-side elements

## What's Next?

Now that you understand the box model, learn:

- **Flexbox** - Modern, flexible layout system
- **CSS Grid** - Two-dimensional layout
- **Responsive Design** - Make sites work on all devices
- **Advanced Layouts** - Complex page structures

---

**Previous Tutorial:** [Colors, Text, and Fonts](03_colors_text_fonts.md)  
**Next Tutorial:** [Flexbox](05_flexbox.md)


