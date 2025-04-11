# CSS Styling Crash Course

A comprehensive guide to modern CSS styling, including Flexbox, Grid, and utility-first frameworks like Tailwind CSS.

## Quick Reference

### Most Common Properties

```css
/* Layout */
display: flex | grid | block | inline-block;
position: static | relative | absolute | fixed | sticky;
float: left | right | none;

/* Box Model */
margin: value;
padding: value;
border: width style color;
box-sizing: border-box;

/* Flexbox */
display: flex;
flex-direction: row | column;
justify-content: flex-start | center | flex-end | space-between;
align-items: flex-start | center | flex-end | stretch;

/* Grid */
display: grid;
grid-template-columns: repeat(3, 1fr);
grid-template-rows: auto;
gap: 1rem;
```

### Common Patterns

```css
/* Centering with Flexbox */
.center-flex {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Centering with Grid */
.center-grid {
  display: grid;
  place-items: center;
}

/* Responsive Design */
@media (max-width: 768px) {
  .container {
    width: 100%;
  }
}

/* Hover Effects */
.button {
  transition: all 0.3s ease;
}

.button:hover {
  transform: scale(1.05);
}
```

### Quick Lookup

| Pattern        | CSS                              | Tailwind          |
| -------------- | -------------------------------- | ----------------- |
| Flex Container | `display: flex`                  | `flex`            |
| Grid Container | `display: grid`                  | `grid`            |
| Center Content | `justify-content: center`        | `justify-center`  |
| Space Between  | `justify-content: space-between` | `justify-between` |
| Gap            | `gap: 1rem`                      | `gap-4`           |
| Padding        | `padding: 1rem`                  | `p-4`             |
| Margin         | `margin: 1rem`                   | `m-4`             |

## 1. Flexbox vs Grid

### When to Use Flexbox

```css
/* ✅ Use Flexbox for:
 * - One-dimensional layouts (row OR column)
 * - Aligning items in a single direction
 * - Distributing space between items
 * - Navigation bars
 * - Card layouts with equal heights
 */

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card-container {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}
```

### When to Use Grid

```css
/* ✅ Use Grid for:
 * - Two-dimensional layouts (rows AND columns)
 * - Complex layouts with overlapping elements
 * - Creating responsive layouts with minimal media queries
 * - Page layouts
 * - Image galleries
 */

.page-layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}
```

## 2. Tailwind CSS

### Basic Usage

```html
<!-- Utility Classes -->
<div class="flex justify-between items-center p-4">
  <div class="w-1/2">Left</div>
  <div class="w-1/2">Right</div>
</div>

<!-- Responsive Design -->
<div class="w-full md:w-1/2 lg:w-1/3">
  <!-- Content -->
</div>

<!-- Hover/Focus States -->
<button class="bg-blue-500 hover:bg-blue-700 focus:ring-2">Click me</button>
```

### Common Patterns

```html
<!-- Card Component -->
<div class="max-w-sm rounded overflow-hidden shadow-lg">
  <img class="w-full" src="image.jpg" alt="Card image" />
  <div class="px-6 py-4">
    <div class="font-bold text-xl mb-2">Card Title</div>
    <p class="text-gray-700 text-base">Card description</p>
  </div>
</div>

<!-- Navigation -->
<nav class="bg-gray-800 text-white p-4">
  <div class="container mx-auto flex justify-between items-center">
    <div class="text-xl font-bold">Logo</div>
    <div class="space-x-4">
      <a href="#" class="hover:text-gray-300">Home</a>
      <a href="#" class="hover:text-gray-300">About</a>
      <a href="#" class="hover:text-gray-300">Contact</a>
    </div>
  </div>
</nav>
```

## 3. Best Practices

### Common Pitfalls to Avoid

```css
/* ❌ Avoid using !important */
.button {
  color: red !important; /* Bad */
}

/* ❌ Avoid overly specific selectors */
div.container > ul > li > a {
  /* Bad */
  color: blue;
}

/* ❌ Avoid fixed heights when possible */
.container {
  height: 500px; /* Bad - use min-height instead */
}

/* ✅ Better alternatives */
.button.primary {
  color: red; /* Good */
}

.nav-link {
  color: blue; /* Good */
}

.container {
  min-height: 500px; /* Good */
}
```

### Performance Considerations

```css
/* ✅ Use CSS variables for theming */
:root {
  --primary-color: #007bff;
  --spacing-unit: 1rem;
}

/* ✅ Use transform instead of position for animations */
.animate {
  transform: translateX(100px); /* Better performance */
}

/* ✅ Use will-change for elements that will animate */
.animated-element {
  will-change: transform;
}

/* ✅ Use contain for isolated components */
.isolated-component {
  contain: content;
}
```

### Code Style Guidelines

```css
/* ✅ Use meaningful class names */
.user-profile-card {
  /* Good */
  /* styles */
}

.card {
  /* Too generic */
  /* styles */
}

/* ✅ Group related properties */
.selector {
  /* Layout */
  display: flex;
  position: relative;

  /* Box Model */
  margin: 0;
  padding: 1rem;

  /* Typography */
  font-size: 1rem;
  line-height: 1.5;

  /* Colors */
  color: #333;
  background-color: #fff;
}

/* ✅ Use CSS custom properties for theming */
:root {
  --primary-color: #007bff;
  --spacing-unit: 1rem;
}

.theme-dark {
  --primary-color: #0056b3;
}
```

## 4. Responsive Design

### Media Queries

```css
/* Mobile First Approach */
.container {
  width: 100%;
  padding: 1rem;
}

@media (min-width: 768px) {
  .container {
    width: 750px;
    margin: 0 auto;
  }
}

@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}

/* Common Breakpoints */
/* Small devices (phones) */
@media (max-width: 576px) {
  /* styles */
}

/* Medium devices (tablets) */
@media (min-width: 577px) and (max-width: 768px) {
  /* styles */
}

/* Large devices (desktops) */
@media (min-width: 769px) and (max-width: 992px) {
  /* styles */
}

/* Extra large devices */
@media (min-width: 993px) {
  /* styles */
}
```

### Responsive Units

```css
/* ✅ Use relative units */
.container {
  width: 100%; /* Percentage */
  padding: 1rem; /* Root em */
  font-size: 1.2em; /* Relative to parent */
  line-height: 1.5; /* Unitless */
}

/* ✅ Use viewport units for full-height layouts */
.hero-section {
  height: 100vh; /* Full viewport height */
  width: 100vw; /* Full viewport width */
}

/* ✅ Use min/max for responsive typography */
h1 {
  font-size: clamp(2rem, 5vw, 3.5rem);
}
```
