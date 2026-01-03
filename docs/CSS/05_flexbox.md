# Flexbox

Learn Flexbox - a powerful, modern CSS layout system that makes it easy to create flexible, responsive layouts.

## What is Flexbox?

Flexbox (Flexible Box Layout) is a one-dimensional layout method for arranging items in rows or columns. It makes it easy to align, distribute space, and resize elements.

### Why Use Flexbox?

- **Easy Alignment:** Center items vertically and horizontally with ease
- **Flexible Sizing:** Items can grow or shrink to fill available space
- **Responsive:** Adapts to different screen sizes automatically
- **Simple Syntax:** Less code than older layout methods
- **Modern:** Supported by all modern browsers

## Flex Container

To use Flexbox, make an element a flex container:

```css
.container {
    display: flex;
}
```

This makes all direct children flex items.

## Flex Direction

Controls the direction of flex items:

```css
.container {
    display: flex;
    flex-direction: row; /* Default - left to right */
}
```

**Values:**
- `row` - Left to right (default)
- `row-reverse` - Right to left
- `column` - Top to bottom
- `column-reverse` - Bottom to top

### Example

```css
.container {
    display: flex;
    flex-direction: row;
}

/* Items arranged horizontally */
```

```html
<div class="container">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</div>
```

## Justify Content

Aligns items along the main axis (horizontal by default):

```css
.container {
    display: flex;
    justify-content: flex-start; /* Default */
}
```

**Values:**
- `flex-start` - Start of container
- `flex-end` - End of container
- `center` - Center of container
- `space-between` - Space between items
- `space-around` - Space around items
- `space-evenly` - Equal space everywhere

### Examples

```css
/* Center items */
.container {
    display: flex;
    justify-content: center;
}

/* Space between */
.container {
    display: flex;
    justify-content: space-between;
}

/* Even spacing */
.container {
    display: flex;
    justify-content: space-evenly;
}
```

## Align Items

Aligns items along the cross axis (vertical by default):

```css
.container {
    display: flex;
    align-items: stretch; /* Default */
}
```

**Values:**
- `stretch` - Stretch to fill container
- `flex-start` - Start of cross axis
- `flex-end` - End of cross axis
- `center` - Center of cross axis
- `baseline` - Align to baseline

### Centering Example

```css
.container {
    display: flex;
    justify-content: center; /* Horizontal center */
    align-items: center;     /* Vertical center */
    height: 300px;
}
```

This perfectly centers content both horizontally and vertically!

## Flex Wrap

Controls whether items wrap to new lines:

```css
.container {
    display: flex;
    flex-wrap: nowrap; /* Default - no wrapping */
}
```

**Values:**
- `nowrap` - All items on one line
- `wrap` - Wrap to new lines
- `wrap-reverse` - Wrap in reverse order

```css
.container {
    display: flex;
    flex-wrap: wrap;
}
```

## Flex Shorthand

Combine `flex-direction` and `flex-wrap`:

```css
.container {
    display: flex;
    flex-flow: row wrap;
}
```

## Align Content

Aligns wrapped lines (only works with `flex-wrap: wrap`):

```css
.container {
    display: flex;
    flex-wrap: wrap;
    align-content: flex-start;
}
```

**Values:** Same as `justify-content` but for cross axis.

## Gap

Space between flex items:

```css
.container {
    display: flex;
    gap: 20px; /* Space between all items */
}

.container {
    display: flex;
    row-gap: 10px;    /* Vertical gap */
    column-gap: 20px; /* Horizontal gap */
}
```

## Flex Items

Properties that apply to flex items (children):

### Flex Grow

How much an item should grow relative to others:

```css
.item {
    flex-grow: 0; /* Default - don't grow */
}

.item-large {
    flex-grow: 2; /* Grow twice as much */
}
```

### Flex Shrink

How much an item should shrink:

```css
.item {
    flex-shrink: 1; /* Default - can shrink */
}

.item-fixed {
    flex-shrink: 0; /* Don't shrink */
}
```

### Flex Basis

Initial size before growing/shrinking:

```css
.item {
    flex-basis: 200px; /* Start at 200px */
}
```

### Flex Shorthand

Combine `grow`, `shrink`, and `basis`:

```css
.item {
    flex: 1; /* flex: 1 1 0 */
}

.item {
    flex: 0 1 auto; /* Default */
}

.item {
    flex: 2 1 200px; /* grow: 2, shrink: 1, basis: 200px */
}
```

### Align Self

Override `align-items` for individual items:

```css
.item {
    align-self: center;
}
```

### Order

Change visual order without changing HTML:

```css
.item-first {
    order: -1; /* Appears first */
}

.item-last {
    order: 1; /* Appears last */
}
```

## Common Flexbox Patterns

### Navigation Bar

```css
.nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
}

.nav-links {
    display: flex;
    gap: 20px;
    list-style: none;
}
```

### Card Grid

```css
.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.card {
    flex: 1 1 300px; /* Grow, shrink, min 300px */
    max-width: 400px;
}
```

### Centered Content

```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
```

### Sidebar Layout

```css
.layout {
    display: flex;
    height: 100vh;
}

.sidebar {
    flex: 0 0 250px; /* Don't grow/shrink, 250px wide */
}

.main-content {
    flex: 1; /* Take remaining space */
}
```

### Equal Height Columns

```css
.columns {
    display: flex;
    gap: 20px;
}

.column {
    flex: 1; /* Equal width */
}
```

## Complete Example

```css
/* Navigation */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 30px;
    background-color: #333;
    color: white;
}

.nav-links {
    display: flex;
    gap: 20px;
    list-style: none;
}

/* Card Grid */
.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 30px;
    padding: 20px;
}

.card {
    flex: 1 1 300px;
    background: white;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Centered Hero Section */
.hero {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 400px;
    text-align: center;
}

/* Button Group */
.button-group {
    display: flex;
    gap: 10px;
    justify-content: center;
}

.button {
    flex: 0 1 auto;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
```

## Best Practices

1. **Use for One-Dimensional Layouts:** Flexbox is perfect for rows or columns
2. **Combine with Media Queries:** Make layouts responsive
3. **Use Gap Instead of Margins:** Cleaner spacing between items
4. **Flex Shorthand:** Use `flex: 1` instead of separate properties
5. **Don't Overuse:** Sometimes simple block/inline is better

## Common Mistakes

### 1. Forgetting display: flex

```css
/* ❌ Wrong */
.container {
    justify-content: center; /* Won't work! */
}

/* ✅ Correct */
.container {
    display: flex;
    justify-content: center;
}
```

### 2. Using Flexbox for Everything

```css
/* ❌ Wrong - simple paragraph doesn't need flexbox */
p {
    display: flex;
}

/* ✅ Correct */
p {
    /* Normal block element */
}
```

### 3. Not Understanding Flex Shorthand

```css
/* ❌ Confusing */
.item {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 0;
}

/* ✅ Clearer */
.item {
    flex: 1;
}
```

## Practice Exercise

Create layouts using Flexbox:

1. A navigation bar with logo on left, links on right
2. A card grid that wraps on smaller screens
3. A centered hero section with text and button
4. A sidebar layout with fixed sidebar and flexible main content
5. A button group with equal spacing
6. A footer with multiple columns of equal width

## What's Next?

Now that you understand Flexbox, learn:

- **CSS Grid** - Two-dimensional layouts
- **Responsive Design** - Media queries and mobile-first
- **Advanced Layouts** - Combining Flexbox and Grid
- **CSS Animations** - Add motion to your designs

---

**Previous Tutorial:** [Box Model and Layout](04_box_model_layout.md)  
**Next Tutorial:** [Responsive Design](06_responsive_design.md)


