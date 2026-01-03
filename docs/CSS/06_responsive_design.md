# Responsive Design

Learn how to create websites that work beautifully on all devices - from mobile phones to desktop computers.

## What is Responsive Design?

Responsive design makes websites adapt to different screen sizes and devices. A responsive site looks good and functions well on:
- Mobile phones (320px - 768px)
- Tablets (768px - 1024px)
- Desktops (1024px+)

### Why Responsive Design Matters

- **Mobile Usage:** Over 50% of web traffic is mobile
- **User Experience:** Users expect sites to work on their device
- **SEO:** Google favors mobile-friendly sites
- **Future-Proof:** Works on devices that don't exist yet

## Viewport Meta Tag

Essential for responsive design. Add to your HTML `<head>`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

This tells mobile browsers to use the device width and set initial zoom to 1.0.

## Media Queries

Media queries allow you to apply CSS only when certain conditions are met (like screen size).

### Basic Syntax

```css
@media (condition) {
    /* CSS rules */
}
```

### Common Breakpoints

```css
/* Mobile First Approach */
/* Base styles for mobile */

/* Tablet */
@media (min-width: 768px) {
    /* Styles for tablets and up */
}

/* Desktop */
@media (min-width: 1024px) {
    /* Styles for desktops and up */
}

/* Large Desktop */
@media (min-width: 1200px) {
    /* Styles for large desktops */
}
```

### Example

```css
/* Mobile styles (default) */
.container {
    width: 100%;
    padding: 10px;
}

/* Tablet and up */
@media (min-width: 768px) {
    .container {
        width: 750px;
        margin: 0 auto;
        padding: 20px;
    }
}

/* Desktop and up */
@media (min-width: 1024px) {
    .container {
        width: 1200px;
    }
}
```

## Mobile-First Approach

Start with mobile styles, then add styles for larger screens:

```css
/* Mobile (default) */
.card {
    width: 100%;
    margin-bottom: 20px;
}

/* Tablet */
@media (min-width: 768px) {
    .card {
        width: 50%;
        display: inline-block;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .card {
        width: 33.333%;
    }
}
```

## Flexible Units

Use relative units instead of fixed pixels:

### Percentages

```css
.container {
    width: 100%; /* Full width */
}

.sidebar {
    width: 30%; /* 30% of parent */
}

.main-content {
    width: 70%; /* 70% of parent */
}
```

### Viewport Units

```css
.header {
    height: 100vh; /* Full viewport height */
    width: 100vw;  /* Full viewport width */
}

.section {
    padding: 5vh 5vw; /* 5% of viewport */
}
```

**Units:**
- `vw` - Viewport width (1vw = 1% of viewport width)
- `vh` - Viewport height (1vh = 1% of viewport height)
- `vmin` - Smaller of vw or vh
- `vmax` - Larger of vw or vh

### Rem and Em

```css
/* Root font size (usually 16px) */
html {
    font-size: 16px;
}

h1 {
    font-size: 2rem; /* 32px */
}

p {
    font-size: 1rem; /* 16px */
    padding: 1em;     /* 16px - relative to font-size */
}
```

## Flexible Images

Make images responsive:

```css
img {
    max-width: 100%;
    height: auto;
}
```

This ensures images never overflow their container.

### Responsive Images in HTML

```html
<picture>
    <source media="(min-width: 1024px)" srcset="large.jpg">
    <source media="(min-width: 768px)" srcset="medium.jpg">
    <img src="small.jpg" alt="Description">
</picture>
```

## Flexbox for Responsive Layouts

Flexbox makes responsive layouts easier:

```css
.container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.card {
    flex: 1 1 300px; /* Grow, shrink, min 300px */
}

/* Stack on mobile */
@media (max-width: 767px) {
    .container {
        flex-direction: column;
    }
}
```

## Common Responsive Patterns

### Responsive Navigation

```css
/* Mobile: Hamburger menu */
.nav {
    display: none;
}

.menu-toggle {
    display: block;
}

/* Desktop: Horizontal menu */
@media (min-width: 768px) {
    .nav {
        display: flex;
    }
    
    .menu-toggle {
        display: none;
    }
}
```

### Responsive Grid

```css
.grid {
    display: grid;
    grid-template-columns: 1fr; /* 1 column on mobile */
    gap: 20px;
}

/* 2 columns on tablet */
@media (min-width: 768px) {
    .grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

/* 3 columns on desktop */
@media (min-width: 1024px) {
    .grid {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

### Responsive Typography

```css
/* Mobile */
h1 {
    font-size: 1.5rem;
}

p {
    font-size: 0.9rem;
}

/* Desktop */
@media (min-width: 1024px) {
    h1 {
        font-size: 2.5rem;
    }
    
    p {
        font-size: 1rem;
    }
}
```

### Responsive Spacing

```css
.section {
    padding: 20px;
}

@media (min-width: 768px) {
    .section {
        padding: 40px;
    }
}

@media (min-width: 1024px) {
    .section {
        padding: 60px;
    }
}
```

## Complete Responsive Example

```css
/* Reset and Base */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
}

/* Mobile First - Header */
.header {
    background: #333;
    color: white;
    padding: 15px;
}

.nav {
    display: none; /* Hidden on mobile */
}

.menu-toggle {
    display: block;
    background: none;
    border: none;
    color: white;
    font-size: 24px;
    cursor: pointer;
}

/* Mobile - Container */
.container {
    width: 100%;
    padding: 15px;
}

/* Mobile - Cards */
.card {
    width: 100%;
    margin-bottom: 20px;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Tablet */
@media (min-width: 768px) {
    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    
    .nav {
        display: flex;
        gap: 20px;
        list-style: none;
    }
    
    .menu-toggle {
        display: none;
    }
    
    .container {
        max-width: 750px;
        margin: 0 auto;
        padding: 30px 20px;
    }
    
    .card-container {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
    }
    
    .card {
        flex: 1 1 calc(50% - 10px);
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .container {
        max-width: 1200px;
        padding: 40px 20px;
    }
    
    .card {
        flex: 1 1 calc(33.333% - 14px);
    }
    
    h1 {
        font-size: 2.5rem;
    }
}
```

## Testing Responsive Design

### Browser DevTools

1. Open Developer Tools (F12)
2. Click device toolbar icon
3. Select device or set custom dimensions
4. Test different screen sizes

### Common Breakpoints to Test

- 320px (Small mobile)
- 375px (iPhone)
- 768px (Tablet)
- 1024px (Desktop)
- 1440px (Large desktop)

## Best Practices

1. **Mobile-First:** Start with mobile, enhance for larger screens
2. **Use Relative Units:** Percentages, rem, em, vw, vh
3. **Flexible Images:** Always use `max-width: 100%`
4. **Test on Real Devices:** DevTools are great, but test real devices too
5. **Touch-Friendly:** Make buttons and links large enough (min 44x44px)
6. **Performance:** Optimize images and minimize CSS for mobile
7. **Content First:** Ensure content is readable on all sizes

## Common Mistakes

### 1. Fixed Widths

```css
/* ❌ Wrong */
.container {
    width: 1200px;
}

/* ✅ Correct */
.container {
    max-width: 1200px;
    width: 100%;
}
```

### 2. Forgetting Viewport Meta Tag

```html
<!-- ❌ Missing -->
<head>
    <title>My Site</title>
</head>

<!-- ✅ Correct -->
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Site</title>
</head>
```

### 3. Not Making Images Responsive

```css
/* ❌ Wrong */
img {
    width: 800px;
}

/* ✅ Correct */
img {
    max-width: 100%;
    height: auto;
}
```

## Practice Exercise

Create a responsive website with:

1. Mobile-first approach
2. Responsive navigation (hamburger on mobile, horizontal on desktop)
3. Flexible grid that adapts: 1 column (mobile), 2 columns (tablet), 3 columns (desktop)
4. Responsive typography (smaller on mobile, larger on desktop)
5. Responsive images
6. Proper viewport meta tag

## What's Next?

Congratulations! You've learned the fundamentals of CSS. Continue with:

- **CSS Grid** - Two-dimensional layout system
- **CSS Animations** - Add motion and transitions
- **CSS Variables** - Reusable values
- **Advanced Selectors** - More powerful targeting
- **CSS Preprocessors** - SASS, LESS for more powerful CSS

---

**Previous Tutorial:** [Flexbox](05_flexbox.md)  
**Next Steps:** Practice building responsive websites, or learn JavaScript to add interactivity!


