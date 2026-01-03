# CSS Syntax and Selectors

Master the fundamentals of CSS syntax and learn how to target HTML elements with different types of selectors.

## CSS Syntax Basics

Every CSS rule follows this structure:

```css
selector {
    property: value;
    property: value;
}
```

### Breaking It Down

- **Selector:** Which HTML element(s) to style
- **Property:** What aspect to change (color, size, etc.)
- **Value:** The specific setting for that property
- **Declaration:** A property-value pair
- **Rule:** A selector with one or more declarations

### Example

```css
h1 {
    color: blue;
    font-size: 24px;
    text-align: center;
}
```

This rule:
- **Selects** all `<h1>` elements
- **Sets** color to blue
- **Sets** font size to 24 pixels
- **Sets** text alignment to center

## Types of Selectors

### Element Selector

Selects all elements of a specific type:

```css
p {
    color: red;
}

div {
    background-color: lightgray;
}

h1 {
    font-size: 32px;
}
```

**HTML:**
```html
<p>This paragraph is red.</p>
<div>This div has a light gray background.</div>
<h1>This heading is 32px.</h1>
```

### Class Selector

Selects elements with a specific class attribute. Starts with a dot (`.`):

```css
.highlight {
    background-color: yellow;
}

.error {
    color: red;
    font-weight: bold;
}
```

**HTML:**
```html
<p class="highlight">This text is highlighted.</p>
<p class="error">This is an error message.</p>
```

**Multiple Classes:**
```html
<p class="highlight error">This has both classes.</p>
```

### ID Selector

Selects an element with a specific ID attribute. Starts with a hash (`#`):

```css
#header {
    background-color: blue;
    color: white;
}

#footer {
    background-color: gray;
}
```

**HTML:**
```html
<div id="header">Header content</div>
<div id="footer">Footer content</div>
```

!!! warning "IDs Must Be Unique"
    Each ID should only appear once per page. Use classes for styling multiple elements.

### Universal Selector

Selects all elements (use sparingly):

```css
* {
    margin: 0;
    padding: 0;
}
```

This removes default margins and padding from all elements.

## Combining Selectors

### Multiple Selectors

Apply the same styles to multiple selectors:

```css
h1, h2, h3 {
    color: blue;
    font-family: Arial;
}
```

### Descendant Selector

Selects elements inside other elements:

```css
div p {
    color: red;
}
```

This selects all `<p>` elements inside `<div>` elements.

**HTML:**
```html
<div>
    <p>This paragraph is red.</p>
</div>
<p>This paragraph is NOT red.</p>
```

### Child Selector

Selects direct children only (not grandchildren):

```css
div > p {
    color: blue;
}
```

**HTML:**
```html
<div>
    <p>This is blue (direct child).</p>
    <section>
        <p>This is NOT blue (grandchild).</p>
    </section>
</div>
```

### Adjacent Sibling Selector

Selects the element immediately following another:

```css
h1 + p {
    font-weight: bold;
}
```

**HTML:**
```html
<h1>Heading</h1>
<p>This paragraph is bold.</p>
<p>This paragraph is NOT bold.</p>
```

### General Sibling Selector

Selects all siblings that follow:

```css
h1 ~ p {
    color: blue;
}
```

**HTML:**
```html
<h1>Heading</h1>
<p>This is blue.</p>
<p>This is also blue.</p>
```

## Attribute Selectors

Select elements based on their attributes:

### Has Attribute

```css
a[target] {
    color: red;
}
```

Selects all `<a>` elements with a `target` attribute.

### Exact Attribute Value

```css
input[type="text"] {
    border: 1px solid gray;
}
```

### Attribute Contains Value

```css
a[href*="example"] {
    color: blue;
}
```

Selects links where `href` contains "example".

### Attribute Starts With

```css
a[href^="https"] {
    color: green;
}
```

Selects links starting with "https".

### Attribute Ends With

```css
img[src$=".jpg"] {
    border: 2px solid black;
}
```

Selects images with `.jpg` extension.

## Pseudo-classes

Pseudo-classes select elements in a specific state:

### Link States

```css
a:link {
    color: blue;
}

a:visited {
    color: purple;
}

a:hover {
    color: red;
}

a:active {
    color: orange;
}
```

### Form States

```css
input:focus {
    border: 2px solid blue;
    outline: none;
}

input:disabled {
    background-color: lightgray;
}

input:checked {
    accent-color: blue;
}
```

### Structural Pseudo-classes

```css
/* First child */
p:first-child {
    font-weight: bold;
}

/* Last child */
p:last-child {
    margin-bottom: 0;
}

/* nth child */
li:nth-child(2) {
    color: blue;
}

/* Even/odd */
tr:nth-child(even) {
    background-color: lightgray;
}

tr:nth-child(odd) {
    background-color: white;
}
```

## Pseudo-elements

Pseudo-elements style specific parts of elements:

### ::before and ::after

Add content before or after an element:

```css
p::before {
    content: "Note: ";
    font-weight: bold;
}

p::after {
    content: " [End]";
    color: gray;
}
```

### ::first-line and ::first-letter

```css
p::first-line {
    font-weight: bold;
}

p::first-letter {
    font-size: 200%;
    color: blue;
}
```

## Specificity

When multiple rules target the same element, specificity determines which applies:

### Specificity Order (Highest to Lowest)

1. **Inline styles** (`style="..."`)
2. **IDs** (`#id`)
3. **Classes, attributes, pseudo-classes** (`.class`, `[attr]`, `:hover`)
4. **Elements, pseudo-elements** (`div`, `::before`)

### Calculating Specificity

```css
/* Specificity: 0,0,0,1 (1 element) */
p { color: black; }

/* Specificity: 0,0,1,0 (1 class) */
.text { color: blue; }

/* Specificity: 0,1,0,0 (1 ID) */
#header { color: red; }

/* Specificity: 0,0,1,1 (1 class + 1 element) */
div.text { color: green; }
```

The rule with higher specificity wins.

### !important Rule

Forces a style to apply (use sparingly):

```css
p {
    color: blue !important;
}
```

!!! warning "Avoid !important"
    Overusing `!important` makes CSS hard to maintain. Use specificity instead.

## Complete Examples

### Navigation Menu

```css
/* Style the navigation */
nav {
    background-color: #333;
    padding: 10px;
}

/* Style navigation links */
nav a {
    color: white;
    text-decoration: none;
    padding: 10px 15px;
    display: inline-block;
}

/* Hover effect */
nav a:hover {
    background-color: #555;
}

/* Active link */
nav a.active {
    background-color: #007bff;
}
```

### Form Styling

```css
/* All text inputs */
input[type="text"],
input[type="email"] {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

/* Focused input */
input:focus {
    border-color: #007bff;
    outline: none;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.3);
}

/* Error state */
input.error {
    border-color: red;
}
```

## Best Practices

1. **Use Classes for Styling:** More flexible than IDs
2. **Keep Selectors Simple:** Avoid overly complex selectors
3. **Use Semantic Names:** `.button-primary` not `.blue-box`
4. **Avoid Inline Styles:** Use external stylesheets
5. **Understand Specificity:** Know which styles will apply
6. **Group Related Styles:** Organize your CSS logically

## Common Mistakes

### 1. Overly Specific Selectors

```css
/* ❌ Too specific */
div.container div.row div.col-md-6 p.text-center {
    color: blue;
}

/* ✅ Better */
.text-center {
    color: blue;
}
```

### 2. Using IDs for Styling

```css
/* ❌ Wrong */
#button {
    background: blue;
}

/* ✅ Correct */
.button {
    background: blue;
}
```

### 3. Not Understanding Specificity

```css
/* If both apply, .text wins (higher specificity) */
p { color: black; }
.text { color: blue; }
```

## Practice Exercise

Create CSS that styles:

1. All paragraphs with blue text
2. Elements with class "highlight" with yellow background
3. Links that turn red on hover
4. First paragraph in each div with bold text
5. All inputs with type "text" with a gray border
6. Every other table row with a light gray background

## What's Next?

Now that you understand selectors, learn to:

- **Style Colors and Text** - Make your content visually appealing
- **Control Typography** - Fonts, sizes, spacing
- **Work with the Box Model** - Understand spacing and sizing
- **Create Layouts** - Position and arrange elements

---

**Previous Tutorial:** [Introduction to CSS](01_introduction.md)  
**Next Tutorial:** [Colors, Text, and Fonts](03_colors_text_fonts.md)


