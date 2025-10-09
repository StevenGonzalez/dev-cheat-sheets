# CSS Cheat Sheet

## Table of Contents
- [CSS Basics](#css-basics)
- [Selectors](#selectors)
- [Box Model](#box-model)
- [Typography](#typography)
- [Colors & Backgrounds](#colors--backgrounds)
- [Layout - Flexbox](#layout---flexbox)
- [Layout - Grid](#layout---grid)
- [Positioning](#positioning)
- [Responsive Design](#responsive-design)
- [Animations & Transitions](#animations--transitions)
- [Transforms](#transforms)
- [CSS Variables](#css-variables)
- [Pseudo-classes & Pseudo-elements](#pseudo-classes--pseudo-elements)
- [Modern CSS Features](#modern-css-features)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## CSS Basics

### Adding CSS to HTML
```html
<!-- Inline CSS -->
<div style="color: red; font-size: 16px;">Content</div>

<!-- Internal CSS -->
<head>
  <style>
    .my-class { color: blue; }
  </style>
</head>

<!-- External CSS (recommended) -->
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```

### CSS Syntax
```css
/* CSS Rule Structure */
selector {
  property: value;
  property: value;
}

/* Comments */
/* Single line comment */

/*
Multi-line comment
Can span multiple lines
*/

/* CSS Rule Examples */
h1 {
  color: #333;
  font-size: 2rem;
  margin-bottom: 1rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}
```

## Selectors

### Basic Selectors
```css
/* Element selector */
h1 { color: blue; }
p { margin: 1rem 0; }

/* Class selector */
.header { background: #f0f0f0; }
.btn { padding: 10px 15px; }

/* ID selector */
#main-nav { position: fixed; }
#footer { background: #333; }

/* Universal selector */
* { box-sizing: border-box; }

/* Multiple selectors */
h1, h2, h3 { font-family: 'Arial', sans-serif; }
```

### Attribute Selectors
```css
/* Has attribute */
[data-theme] { transition: all 0.3s; }

/* Attribute equals value */
[type="text"] { border: 1px solid #ccc; }
[class="button"] { cursor: pointer; }

/* Attribute contains value */
[class*="btn"] { display: inline-block; }
[href*="mailto"] { color: green; }

/* Attribute starts with value */
[class^="icon-"] { font-size: 1.2em; }
[href^="https"] { color: blue; }

/* Attribute ends with value */
[href$=".pdf"] { color: red; }
[src$=".jpg"] { border-radius: 4px; }
```

### Combinators
```css
/* Descendant selector */
.nav a { text-decoration: none; }
.card p { color: #666; }

/* Direct child selector */
.menu > li { list-style: none; }
.container > .row { margin: 0 -15px; }

/* Adjacent sibling selector */
h1 + p { font-weight: bold; }
.alert + .form-group { margin-top: 20px; }

/* General sibling selector */
h1 ~ p { color: #888; }
.checkbox:checked ~ label { color: green; }
```

### Specificity
```css
/* Specificity calculation: inline(1000) > IDs(100) > classes(10) > elements(1) */

/* Specificity: 1 */
p { color: black; }

/* Specificity: 10 */
.text { color: blue; }

/* Specificity: 100 */
#heading { color: red; }

/* Specificity: 111 */
#heading.large p { color: green; }

/* !important overrides specificity (use sparingly) */
.text { color: purple !important; }
```

## Box Model

### Box Model Properties
```css
.box {
  /* Content dimensions */
  width: 200px;
  height: 150px;
  
  /* Padding (inside the element) */
  padding: 20px;                    /* All sides */
  padding: 10px 20px;               /* Vertical | Horizontal */
  padding: 10px 20px 15px 25px;     /* Top | Right | Bottom | Left */
  
  /* Border */
  border: 1px solid #ccc;
  border-width: 2px;
  border-style: solid;
  border-color: #333;
  
  /* Margin (outside the element) */
  margin: 20px;
  margin: 10px auto;                /* Vertical | Horizontal (auto centers) */
  margin: 10px 20px 15px 25px;      /* Top | Right | Bottom | Left */
}
```

### Box Sizing
```css
/* Default box-sizing */
.default-box {
  box-sizing: content-box;  /* width = content only */
  width: 200px;
  padding: 20px;
  border: 5px solid #ccc;
  /* Total width = 200 + 40 + 10 = 250px */
}

/* Border-box (recommended) */
.border-box {
  box-sizing: border-box;   /* width = content + padding + border */
  width: 200px;
  padding: 20px;
  border: 5px solid #ccc;
  /* Total width = 200px */
}

/* Global border-box reset */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

### Display Property
```css
/* Block elements */
.block {
  display: block;           /* Takes full width, stacks vertically */
  width: 100%;
  margin: 10px 0;
}

/* Inline elements */
.inline {
  display: inline;          /* Takes only needed width, flows horizontally */
  /* Cannot set width/height */
}

/* Inline-block elements */
.inline-block {
  display: inline-block;    /* Flows horizontally but can have dimensions */
  width: 200px;
  height: 100px;
}

/* Hide elements */
.hidden {
  display: none;           /* Removes from layout completely */
}

.invisible {
  visibility: hidden;      /* Hides but maintains space */
}
```

## Typography

### Font Properties
```css
.text {
  /* Font family with fallbacks */
  font-family: 'Helvetica Neue', Arial, sans-serif;
  font-family: 'Georgia', 'Times New Roman', serif;
  font-family: 'Courier New', monospace;
  
  /* Font size */
  font-size: 16px;         /* Absolute units */
  font-size: 1rem;         /* Relative to root font size */
  font-size: 1.2em;        /* Relative to parent font size */
  font-size: 100%;         /* Percentage of parent */
  
  /* Font weight */
  font-weight: normal;     /* 400 */
  font-weight: bold;       /* 700 */
  font-weight: 300;        /* Light */
  font-weight: 600;        /* Semi-bold */
  font-weight: 900;        /* Black */
  
  /* Font style */
  font-style: normal;
  font-style: italic;
  font-style: oblique;
}
```

### Text Properties
```css
.text-styling {
  /* Text alignment */
  text-align: left;
  text-align: center;
  text-align: right;
  text-align: justify;
  
  /* Text decoration */
  text-decoration: none;
  text-decoration: underline;
  text-decoration: line-through;
  text-decoration: overline;
  
  /* Text transform */
  text-transform: none;
  text-transform: uppercase;
  text-transform: lowercase;
  text-transform: capitalize;
  
  /* Line height */
  line-height: 1.5;        /* Multiplier of font size */
  line-height: 24px;       /* Absolute value */
  line-height: 150%;       /* Percentage */
  
  /* Letter and word spacing */
  letter-spacing: 1px;
  letter-spacing: 0.1em;
  word-spacing: 2px;
  
  /* Text overflow */
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

### Web Fonts
```css
/* Google Fonts import */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;700&display=swap');

/* Font face declaration */
@font-face {
  font-family: 'CustomFont';
  src: url('fonts/custom-font.woff2') format('woff2'),
       url('fonts/custom-font.woff') format('woff');
  font-weight: 400;
  font-style: normal;
  font-display: swap;      /* Improves loading performance */
}

/* Usage */
.custom-text {
  font-family: 'Inter', 'CustomFont', system-ui, sans-serif;
}
```

## Colors & Backgrounds

### Color Values
```css
.colors {
  /* Named colors */
  color: red;
  color: blue;
  color: transparent;
  
  /* Hexadecimal */
  color: #ff0000;          /* Red */
  color: #0000ff;          /* Blue */
  color: #333;             /* Short form for #333333 */
  
  /* RGB */
  color: rgb(255, 0, 0);   /* Red */
  color: rgba(255, 0, 0, 0.5);  /* Red with 50% opacity */
  
  /* HSL (Hue, Saturation, Lightness) */
  color: hsl(0, 100%, 50%);     /* Red */
  color: hsla(0, 100%, 50%, 0.5); /* Red with 50% opacity */
  
  /* Modern color functions */
  color: hwb(0 0% 0%);          /* Red using HWB */
  color: lab(50% 20 -20);       /* LAB color space */
}
```

### Background Properties
```css
.background {
  /* Background color */
  background-color: #f0f0f0;
  background-color: rgba(0, 0, 0, 0.1);
  
  /* Background image */
  background-image: url('image.jpg');
  background-image: linear-gradient(45deg, #ff6b6b, #4ecdc4);
  
  /* Background repeat */
  background-repeat: no-repeat;
  background-repeat: repeat-x;
  background-repeat: repeat-y;
  
  /* Background position */
  background-position: center;
  background-position: top left;
  background-position: 50% 50%;
  background-position: 10px 20px;
  
  /* Background size */
  background-size: cover;      /* Scale to cover entire element */
  background-size: contain;    /* Scale to fit within element */
  background-size: 100% 100%;  /* Stretch to fill */
  background-size: 200px 150px; /* Specific dimensions */
  
  /* Background attachment */
  background-attachment: scroll;  /* Default */
  background-attachment: fixed;   /* Fixed during scroll */
  
  /* Shorthand */
  background: #fff url('bg.jpg') no-repeat center/cover;
}
```

### Gradients
```css
/* Linear gradients */
.linear-gradient {
  background: linear-gradient(to right, #ff6b6b, #4ecdc4);
  background: linear-gradient(45deg, red, blue);
  background: linear-gradient(to bottom, #fff 0%, #000 100%);
  
  /* Multiple color stops */
  background: linear-gradient(
    90deg,
    #ff6b6b 0%,
    #4ecdc4 50%,
    #45b7d1 100%
  );
}

/* Radial gradients */
.radial-gradient {
  background: radial-gradient(circle, #ff6b6b, #4ecdc4);
  background: radial-gradient(ellipse at center, red, blue);
  background: radial-gradient(circle at 20% 50%, #fff, #000);
}

/* Conic gradients */
.conic-gradient {
  background: conic-gradient(from 0deg, red, yellow, green, blue, red);
  background: conic-gradient(at 50% 50%, #ff6b6b, #4ecdc4);
}
```

## Layout - Flexbox

### Flex Container
```css
.flex-container {
  display: flex;
  
  /* Main axis direction */
  flex-direction: row;         /* Default: left to right */
  flex-direction: row-reverse; /* Right to left */
  flex-direction: column;      /* Top to bottom */
  flex-direction: column-reverse; /* Bottom to top */
  
  /* Line wrapping */
  flex-wrap: nowrap;          /* Default: single line */
  flex-wrap: wrap;            /* Multi-line */
  flex-wrap: wrap-reverse;    /* Multi-line, reverse order */
  
  /* Shorthand for direction and wrap */
  flex-flow: row wrap;
  
  /* Main axis alignment */
  justify-content: flex-start;   /* Default: start of container */
  justify-content: flex-end;     /* End of container */
  justify-content: center;       /* Center of container */
  justify-content: space-between; /* Even spacing, no edge gaps */
  justify-content: space-around;  /* Even spacing, half edge gaps */
  justify-content: space-evenly;  /* Even spacing, full edge gaps */
  
  /* Cross axis alignment */
  align-items: stretch;       /* Default: full height */
  align-items: flex-start;    /* Top alignment */
  align-items: flex-end;      /* Bottom alignment */
  align-items: center;        /* Center alignment */
  align-items: baseline;      /* Text baseline alignment */
  
  /* Multi-line cross axis alignment */
  align-content: stretch;     /* Default */
  align-content: flex-start;
  align-content: center;
  align-content: space-between;
  
  /* Gap between items */
  gap: 1rem;                  /* Both row and column gap */
  row-gap: 1rem;              /* Gap between rows */
  column-gap: 2rem;           /* Gap between columns */
}
```

### Flex Items
```css
.flex-item {
  /* Flex grow: ability to grow */
  flex-grow: 0;               /* Default: don't grow */
  flex-grow: 1;               /* Grow equally with other items */
  flex-grow: 2;               /* Grow twice as much as items with flex-grow: 1 */
  
  /* Flex shrink: ability to shrink */
  flex-shrink: 1;             /* Default: can shrink */
  flex-shrink: 0;             /* Don't shrink */
  
  /* Flex basis: initial size before free space is distributed */
  flex-basis: auto;           /* Default: content size */
  flex-basis: 200px;          /* Specific size */
  flex-basis: 25%;            /* Percentage of container */
  
  /* Shorthand */
  flex: 1;                    /* flex-grow: 1, flex-shrink: 1, flex-basis: 0 */
  flex: 0 1 auto;             /* Default values */
  flex: 2 1 200px;            /* Custom values */
  
  /* Individual alignment */
  align-self: auto;           /* Default: inherit from container */
  align-self: flex-start;
  align-self: flex-end;
  align-self: center;
  align-self: stretch;
  
  /* Order */
  order: 0;                   /* Default: source order */
  order: 1;                   /* Move later in visual order */
  order: -1;                  /* Move earlier in visual order */
}
```

### Common Flexbox Patterns
```css
/* Centering content */
.center-content {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

/* Navigation bar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
}

/* Card layout */
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
}

.card {
  flex: 1 1 300px;            /* Grow, shrink, min 300px wide */
}

/* Sidebar layout */
.sidebar-layout {
  display: flex;
  gap: 2rem;
}

.sidebar {
  flex: 0 0 250px;            /* Fixed 250px width */
}

.main-content {
  flex: 1;                    /* Take remaining space */
}
```

## Layout - Grid

### Grid Container
```css
.grid-container {
  display: grid;
  
  /* Define columns */
  grid-template-columns: 200px 1fr 100px;        /* Fixed, flexible, fixed */
  grid-template-columns: repeat(3, 1fr);          /* 3 equal columns */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); /* Responsive */
  
  /* Define rows */
  grid-template-rows: 100px 1fr 50px;           /* Header, content, footer */
  grid-template-rows: repeat(4, 100px);          /* 4 rows of 100px */
  
  /* Grid gaps */
  gap: 20px;                  /* Both row and column gap */
  row-gap: 10px;              /* Gap between rows */
  column-gap: 20px;           /* Gap between columns */
  
  /* Grid areas (named template) */
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
    
  /* Alignment */
  justify-items: start;       /* Horizontal alignment of items */
  justify-items: end;
  justify-items: center;
  justify-items: stretch;     /* Default */
  
  align-items: start;         /* Vertical alignment of items */
  align-items: end;
  align-items: center;
  align-items: stretch;       /* Default */
  
  /* Grid content alignment */
  justify-content: start;     /* Horizontal alignment of grid */
  justify-content: center;
  justify-content: end;
  justify-content: space-between;
  justify-content: space-around;
  justify-content: space-evenly;
  
  align-content: start;       /* Vertical alignment of grid */
  align-content: center;
  align-content: end;
}
```

### Grid Items
```css
.grid-item {
  /* Column placement */
  grid-column-start: 1;
  grid-column-end: 3;
  grid-column: 1 / 3;         /* Shorthand */
  grid-column: 1 / -1;        /* From first to last column */
  grid-column: span 2;        /* Span 2 columns */
  
  /* Row placement */
  grid-row-start: 2;
  grid-row-end: 4;
  grid-row: 2 / 4;            /* Shorthand */
  grid-row: span 3;           /* Span 3 rows */
  
  /* Area placement */
  grid-area: header;          /* Use named area */
  grid-area: 1 / 1 / 2 / 4;   /* row-start / col-start / row-end / col-end */
  
  /* Individual alignment */
  justify-self: start;        /* Horizontal alignment */
  justify-self: center;
  justify-self: end;
  justify-self: stretch;
  
  align-self: start;          /* Vertical alignment */
  align-self: center;
  align-self: end;
  align-self: stretch;
}
```

### Grid Functions & Units
```css
.grid-advanced {
  /* fr unit (fraction of remaining space) */
  grid-template-columns: 1fr 2fr 1fr;  /* 25% 50% 25% */
  
  /* minmax() function */
  grid-template-columns: minmax(200px, 1fr) 300px;
  
  /* repeat() function */
  grid-template-columns: repeat(12, 1fr);              /* 12 equal columns */
  grid-template-columns: repeat(auto-fit, 200px);      /* Auto columns, 200px each */
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  
  /* fit-content() function */
  grid-template-columns: fit-content(200px) 1fr;
  
  /* Auto sizing */
  grid-template-rows: auto 1fr auto;   /* Content-sized header/footer */
}
```

### Common Grid Patterns
```css
/* Holy Grail Layout */
.holy-grail {
  display: grid;
  grid-template-areas:
    "header header header"
    "nav main aside"
    "footer footer footer";
  grid-template-rows: auto 1fr auto;
  grid-template-columns: 200px 1fr 200px;
  min-height: 100vh;
}

/* Card Grid */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

/* Masonry-style Layout */
.masonry {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-auto-rows: 10px; /* Small row height for masonry effect */
  gap: 1rem;
}

.masonry-item {
  grid-row-end: span var(--rows); /* CSS custom property for height */
}
```

## Positioning

### Position Property
```css
/* Static positioning (default) */
.static {
  position: static;         /* Normal document flow */
  /* top, right, bottom, left have no effect */
}

/* Relative positioning */
.relative {
  position: relative;
  top: 10px;               /* Move 10px down from normal position */
  left: 20px;              /* Move 20px right from normal position */
  z-index: 1;              /* Stacking order */
}

/* Absolute positioning */
.absolute {
  position: absolute;       /* Positioned relative to nearest positioned ancestor */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* Center the element */
  z-index: 10;
}

/* Fixed positioning */
.fixed {
  position: fixed;          /* Positioned relative to viewport */
  top: 0;
  right: 0;
  width: 100%;
  z-index: 1000;           /* Above other content */
}

/* Sticky positioning */
.sticky {
  position: sticky;         /* Switches between relative and fixed */
  top: 0;                  /* Becomes fixed when 0px from top */
  z-index: 100;
}
```

### Z-Index and Stacking Context
```css
/* Z-index controls stacking order */
.layer-1 { z-index: 1; }
.layer-2 { z-index: 2; }    /* Appears above layer-1 */
.layer-3 { z-index: -1; }   /* Appears below default layer (0) */

/* Elements that create new stacking contexts */
.stacking-context {
  position: relative;       /* Any position except static */
  opacity: 0.99;           /* Any opacity < 1 */
  transform: translateX(0); /* Any transform */
  filter: blur(0);         /* Any filter */
  z-index: 1;              /* With positioned element */
}

/* Common positioning patterns */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 1000;
}

.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1001;           /* Above overlay */
}
```

## Responsive Design

### Media Queries
```css
/* Basic media query syntax */
@media screen and (max-width: 768px) {
  .container {
    padding: 10px;
  }
}

/* Common breakpoints */
/* Mobile first approach */
.responsive-element {
  font-size: 14px;          /* Base (mobile) styles */
}

@media (min-width: 576px) {  /* Small tablets */
  .responsive-element {
    font-size: 16px;
  }
}

@media (min-width: 768px) {  /* Tablets */
  .responsive-element {
    font-size: 18px;
  }
}

@media (min-width: 992px) {  /* Small desktops */
  .responsive-element {
    font-size: 20px;
  }
}

@media (min-width: 1200px) { /* Large desktops */
  .responsive-element {
    font-size: 22px;
  }
}

/* Advanced media queries */
@media (orientation: landscape) {
  .landscape-only { display: block; }
}

@media (orientation: portrait) {
  .portrait-only { display: block; }
}

@media (prefers-color-scheme: dark) {
  .dark-mode { background: #333; color: #fff; }
}

@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; }
}

@media (hover: hover) {
  .hover-effect:hover { background: #f0f0f0; }
}
```

### Responsive Units
```css
.responsive-units {
  /* Viewport units */
  width: 100vw;            /* 100% of viewport width */
  height: 100vh;           /* 100% of viewport height */
  font-size: 4vw;          /* 4% of viewport width */
  
  /* Relative units */
  font-size: 1rem;         /* Relative to root font size */
  padding: 2em;            /* Relative to element font size */
  width: 50%;              /* Relative to parent width */
  
  /* Container query units (modern) */
  width: 50cqw;            /* 50% of container width */
  font-size: 4cqh;         /* 4% of container height */
}

/* Fluid typography */
.fluid-text {
  font-size: clamp(1rem, 4vw, 3rem); /* Min 1rem, ideal 4vw, max 3rem */
}

/* Responsive images */
.responsive-image {
  max-width: 100%;
  height: auto;
}

/* Responsive containers */
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 clamp(1rem, 5vw, 3rem);
}
```

### Container Queries (Modern CSS)
```css
/* Container query setup */
.card-container {
  container-type: inline-size;  /* Enable container queries */
  container-name: card;         /* Optional name */
}

/* Container query */
@container card (min-width: 300px) {
  .card {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
}

@container (max-width: 250px) {
  .card .image {
    display: none;           /* Hide image in small containers */
  }
}
```

## Animations & Transitions

### CSS Transitions
```css
.transition-element {
  background: blue;
  transform: scale(1);
  
  /* Single property transition */
  transition: background 0.3s ease;
  
  /* Multiple property transitions */
  transition: background 0.3s ease, transform 0.2s ease-out;
  
  /* All properties transition */
  transition: all 0.3s ease-in-out;
  
  /* Detailed transition syntax */
  transition-property: background, transform;
  transition-duration: 0.3s, 0.2s;
  transition-timing-function: ease, ease-out;
  transition-delay: 0s, 0.1s;
}

.transition-element:hover {
  background: red;
  transform: scale(1.1);
}

/* Common timing functions */
.timing-functions {
  transition-timing-function: linear;      /* Constant speed */
  transition-timing-function: ease;        /* Slow start, fast, slow end */
  transition-timing-function: ease-in;     /* Slow start */
  transition-timing-function: ease-out;    /* Slow end */
  transition-timing-function: ease-in-out; /* Slow start and end */
  
  /* Custom cubic-bezier */
  transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1);
}
```

### CSS Animations
```css
/* Keyframe definition */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes bounce {
  0%, 20%, 53%, 80%, 100% {
    transform: translate3d(0, 0, 0);
  }
  40%, 43% {
    transform: translate3d(0, -30px, 0);
  }
  70% {
    transform: translate3d(0, -15px, 0);
  }
  90% {
    transform: translate3d(0, -4px, 0);
  }
}

/* Animation properties */
.animated-element {
  animation-name: fadeIn;
  animation-duration: 1s;
  animation-timing-function: ease-out;
  animation-delay: 0.5s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  animation-fill-mode: both;
  animation-play-state: running;
  
  /* Shorthand */
  animation: fadeIn 1s ease-out 0.5s infinite alternate both;
}

/* Multiple animations */
.multi-animated {
  animation: 
    fadeIn 1s ease-out,
    bounce 2s infinite;
}

/* Animation control */
.paused { animation-play-state: paused; }
.reversed { animation-direction: reverse; }
```

### Common Animation Patterns
```css
/* Loading spinner */
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.spinner {
  animation: spin 1s linear infinite;
}

/* Pulse effect */
@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}

.pulse {
  animation: pulse 2s ease-in-out infinite;
}

/* Shake effect */
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  10%, 30%, 50%, 70%, 90% { transform: translateX(-10px); }
  20%, 40%, 60%, 80% { transform: translateX(10px); }
}

.shake {
  animation: shake 0.82s cubic-bezier(.36, .07, .19, .97) both;
}

/* Slide in animations */
@keyframes slideInLeft {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.slide-in {
  animation: slideInLeft 0.5s ease-out;
}
```

## Transforms

### 2D Transforms
```css
.transform-2d {
  /* Translate (move) */
  transform: translateX(50px);        /* Move 50px right */
  transform: translateY(-20px);       /* Move 20px up */
  transform: translate(50px, -20px);  /* Move right and up */
  
  /* Scale (resize) */
  transform: scaleX(1.5);            /* 150% width */
  transform: scaleY(0.8);            /* 80% height */
  transform: scale(1.2);             /* 120% both dimensions */
  transform: scale(1.5, 0.8);        /* Different X and Y scaling */
  
  /* Rotate */
  transform: rotate(45deg);          /* 45 degrees clockwise */
  transform: rotate(-90deg);         /* 90 degrees counterclockwise */
  
  /* Skew */
  transform: skewX(15deg);           /* Skew horizontally */
  transform: skewY(10deg);           /* Skew vertically */
  transform: skew(15deg, 10deg);     /* Skew both axes */
  
  /* Multiple transforms */
  transform: translate(50px, 20px) rotate(45deg) scale(1.2);
  
  /* Transform origin */
  transform-origin: center;          /* Default */
  transform-origin: top left;
  transform-origin: 25% 75%;
  transform-origin: 50px 100px;
}
```

### 3D Transforms
```css
.transform-3d {
  /* 3D translations */
  transform: translateZ(50px);       /* Move towards viewer */
  transform: translate3d(50px, 20px, -30px);
  
  /* 3D rotations */
  transform: rotateX(45deg);         /* Rotate around X-axis */
  transform: rotateY(60deg);         /* Rotate around Y-axis */
  transform: rotateZ(30deg);         /* Rotate around Z-axis (same as rotate) */
  transform: rotate3d(1, 1, 0, 45deg); /* Rotate around custom axis */
  
  /* 3D scaling */
  transform: scaleZ(2);              /* Scale depth */
  transform: scale3d(1.5, 1.2, 0.8);
  
  /* Perspective */
  perspective: 1000px;               /* On parent element */
  transform-style: preserve-3d;      /* Preserve 3D space for children */
  
  /* Backface visibility */
  backface-visibility: hidden;       /* Hide back face */
  backface-visibility: visible;      /* Show back face (default) */
}

/* 3D card flip example */
.flip-card {
  perspective: 1000px;
  width: 300px;
  height: 200px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.flip-card-back {
  transform: rotateY(180deg);
}
```

## CSS Variables

### Custom Properties (CSS Variables)
```css
/* Global variables (on :root) */
:root {
  --primary-color: #007bff;
  --secondary-color: #6c757d;
  --font-size-base: 16px;
  --font-family-sans: 'Helvetica Neue', Arial, sans-serif;
  --border-radius: 4px;
  --spacing-unit: 8px;
  --box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Using variables */
.button {
  background-color: var(--primary-color);
  color: white;
  font-family: var(--font-family-sans);
  font-size: var(--font-size-base);
  border-radius: var(--border-radius);
  padding: calc(var(--spacing-unit) * 2) calc(var(--spacing-unit) * 3);
  box-shadow: var(--box-shadow);
}

/* Variables with fallbacks */
.element {
  color: var(--text-color, #333);     /* Use #333 if --text-color undefined */
  margin: var(--margin, 1rem);
}

/* Local variables (scoped to selector) */
.card {
  --card-padding: 2rem;
  --card-background: #fff;
  
  padding: var(--card-padding);
  background: var(--card-background);
}

.card.dark {
  --card-background: #333;           /* Override for dark theme */
  color: white;
}
```

### Dynamic Variables with JavaScript
```css
/* CSS variables can be manipulated with JavaScript */
.dynamic-element {
  background: var(--dynamic-color, blue);
  transform: translateX(var(--x-position, 0));
}
```

```javascript
// JavaScript to update CSS variables
const element = document.querySelector('.dynamic-element');

// Set variable on specific element
element.style.setProperty('--dynamic-color', 'red');
element.style.setProperty('--x-position', '100px');

// Set global variable
document.documentElement.style.setProperty('--primary-color', '#ff6b6b');

// Get variable value
const primaryColor = getComputedStyle(document.documentElement)
  .getPropertyValue('--primary-color');
```

### Theming with CSS Variables
```css
/* Light theme (default) */
:root {
  --bg-color: #ffffff;
  --text-color: #333333;
  --border-color: #e0e0e0;
  --shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Dark theme */
[data-theme="dark"] {
  --bg-color: #1a1a1a;
  --text-color: #ffffff;
  --border-color: #404040;
  --shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

/* Components using theme variables */
.card {
  background: var(--bg-color);
  color: var(--text-color);
  border: 1px solid var(--border-color);
  box-shadow: var(--shadow);
}

/* Responsive variables */
:root {
  --container-width: 1200px;
  --gutter: 2rem;
}

@media (max-width: 768px) {
  :root {
    --container-width: 100%;
    --gutter: 1rem;
  }
}
```

## Pseudo-classes & Pseudo-elements

### Common Pseudo-classes
```css
/* Link states */
a:link { color: blue; }           /* Unvisited link */
a:visited { color: purple; }      /* Visited link */
a:hover { color: red; }           /* Mouse over */
a:active { color: orange; }       /* Being clicked */
a:focus { outline: 2px solid blue; } /* Keyboard focus */

/* Form states */
input:focus { border-color: blue; }
input:invalid { border-color: red; }
input:valid { border-color: green; }
input:required { border-left: 3px solid red; }
input:disabled { opacity: 0.5; cursor: not-allowed; }
input:checked { background: blue; } /* For checkboxes/radio buttons */

/* Structural pseudo-classes */
li:first-child { margin-top: 0; }
li:last-child { margin-bottom: 0; }
li:nth-child(odd) { background: #f0f0f0; }    /* Odd rows */
li:nth-child(even) { background: white; }     /* Even rows */
li:nth-child(3n) { color: red; }              /* Every 3rd item */
li:nth-child(3n+1) { color: blue; }           /* 1st, 4th, 7th... */

p:first-of-type { font-weight: bold; }
p:last-of-type { margin-bottom: 0; }
h2:nth-of-type(2) { color: red; }             /* 2nd h2 element */

/* Other useful pseudo-classes */
div:empty { display: none; }                  /* Empty elements */
input:not([type="submit"]) { width: 100%; }   /* Not matching selector */
.item:target { background: yellow; }          /* Target of URL fragment */
```

### Pseudo-elements
```css
/* ::before and ::after */
.quote::before {
  content: '"';
  font-size: 1.2em;
  color: #666;
}

.quote::after {
  content: '"';
  font-size: 1.2em;
  color: #666;
}

/* Creating decorative elements */
.button::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1));
  opacity: 0;
  transition: opacity 0.3s;
}

.button:hover::before {
  opacity: 1;
}

/* Text selection styling */
::selection {
  background: #007bff;
  color: white;
}

::-moz-selection { /* Firefox */
  background: #007bff;
  color: white;
}

/* First line and first letter */
p::first-line {
  font-weight: bold;
  font-size: 1.1em;
}

p::first-letter {
  font-size: 3em;
  float: left;
  line-height: 1;
  margin-right: 0.1em;
}

/* Form input placeholders */
input::placeholder {
  color: #999;
  opacity: 1; /* Firefox */
}

input::-webkit-input-placeholder { color: #999; } /* Chrome/Safari */
input::-moz-placeholder { color: #999; } /* Firefox 19+ */
input:-ms-input-placeholder { color: #999; } /* IE 10+ */
```

### Advanced Pseudo-selectors
```css
/* Negation */
:not(.special) { color: black; }
:not(p):not(div) { margin: 0; }

/* Multiple conditions */
input:not([type="submit"]):not([type="button"]) {
  border: 1px solid #ccc;
}

/* Language pseudo-class */
:lang(en) { font-family: 'English Font', serif; }
:lang(fr) { font-family: 'French Font', serif; }

/* Root element */
:root { font-size: 16px; }

/* Any link (internal or external) */
:any-link { color: blue; }

/* Form validation */
:valid { border-color: green; }
:invalid { border-color: red; }
:in-range { border-color: green; }
:out-of-range { border-color: red; }
```

## Modern CSS Features

### CSS Grid Areas & Subgrid
```css
/* Subgrid (limited browser support) */
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}

.grid-item {
  display: grid;
  grid-column: span 2;
  grid-template-columns: subgrid; /* Inherit parent's column tracks */
}

/* Container queries */
@container (min-width: 400px) {
  .card {
    display: flex;
    flex-direction: row;
  }
}

/* CSS nesting (future feature) */
.card {
  padding: 1rem;
  
  & .title {
    font-size: 1.5rem;
    margin-bottom: 0.5rem;
  }
  
  & .content {
    line-height: 1.6;
  }
  
  &:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
}
```

### CSS Functions
```css
/* Mathematical functions */
.calc-example {
  width: calc(100% - 40px);
  height: calc(100vh - 60px);
  margin: calc(2rem + 10px);
}

/* Min, max, clamp */
.responsive-sizing {
  width: min(90%, 600px);           /* Smaller of 90% or 600px */
  height: max(200px, 20vh);         /* Larger of 200px or 20vh */
  font-size: clamp(1rem, 4vw, 2rem); /* Between 1rem and 2rem, ideal 4vw */
}

/* Color functions */
.color-functions {
  background: hsl(200, 50%, 50%);
  color: color-mix(in srgb, blue 30%, red); /* Mix colors */
  border-color: color-contrast(white vs black, blue, red); /* Best contrast */
}

/* CSS comparison functions */
.comparison {
  padding: max(1rem, 2vw);         /* Larger value */
  margin: min(5%, 2rem);           /* Smaller value */
}
```

### CSS Logical Properties
```css
/* Traditional physical properties */
.physical {
  margin-top: 1rem;
  margin-right: 2rem;
  margin-bottom: 1rem;
  margin-left: 2rem;
  border-left: 2px solid blue;
}

/* Logical properties (writing-mode aware) */
.logical {
  margin-block-start: 1rem;        /* Top in horizontal writing */
  margin-inline-end: 2rem;         /* Right in LTR, left in RTL */
  margin-block-end: 1rem;          /* Bottom in horizontal writing */
  margin-inline-start: 2rem;       /* Left in LTR, right in RTL */
  border-inline-start: 2px solid blue; /* Left border in LTR */
}

/* Shorthand logical properties */
.logical-shorthand {
  margin-block: 1rem 2rem;         /* Block start and end */
  margin-inline: 1rem;             /* Inline start and end */
  padding-block: 0.5rem;
  padding-inline: 1rem;
  border-block: 1px solid #ccc;
  border-inline-start: 3px solid blue;
}
```

## Best Practices

### CSS Architecture
```css
/* BEM (Block Element Modifier) methodology */
.card { }                    /* Block */
.card__title { }             /* Element */
.card__content { }           /* Element */
.card--featured { }          /* Modifier */
.card__title--large { }      /* Element with modifier */

/* OOCSS (Object-Oriented CSS) */
/* Structure */
.media { display: flex; }
.media__object { flex-shrink: 0; }
.media__body { flex: 1; }

/* Skin */
.media--article { padding: 1rem; }
.media--comment { border-left: 3px solid blue; }

/* Utility classes */
.text-center { text-align: center; }
.mb-1 { margin-bottom: 0.25rem; }
.mb-2 { margin-bottom: 0.5rem; }
.d-none { display: none; }
.d-block { display: block; }
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
```

### Performance Best Practices
```css
/* Use efficient selectors */
/* Good */
.navigation-item { color: blue; }
#header .logo { width: 200px; }

/* Avoid */
div > ul > li > a { } /* Too specific */
* { } /* Universal selector can be slow */

/* Minimize reflows and repaints */
.animated-element {
  /* Prefer transforms and opacity for animations */
  transform: translateX(100px); /* Better than changing left */
  opacity: 0.5;                 /* Better than changing visibility */
}

/* Use will-change for animations */
.will-animate {
  will-change: transform, opacity;
}

/* Remove will-change after animation */
.animation-complete {
  will-change: auto;
}

/* Optimize critical CSS */
/* Inline critical above-the-fold CSS */
/* Load non-critical CSS asynchronously */

/* Use CSS containment */
.isolated-component {
  contain: layout style paint; /* Isolate for performance */
}
```

### Accessibility Best Practices
```css
/* Focus management */
:focus {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}

/* High contrast support */
@media (prefers-contrast: high) {
  .button {
    border: 2px solid currentColor;
  }
}

/* Reduced motion support */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

/* Screen reader friendly hiding */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Skip links */
.skip-link {
  position: absolute;
  top: -40px;
  left: 6px;
  background: #000;
  color: #fff;
  padding: 8px;
  text-decoration: none;
  z-index: 1000;
}

.skip-link:focus {
  top: 6px;
}
```

### Maintainable CSS
```css
/* Use consistent naming conventions */
/* kebab-case for classes */
.main-navigation { }
.user-profile-card { }

/* Group related properties */
.well-organized {
  /* Positioning */
  position: relative;
  top: 0;
  left: 0;
  
  /* Display & Box Model */
  display: block;
  width: 100%;
  height: 200px;
  margin: 1rem 0;
  padding: 1rem;
  
  /* Background & Border */
  background: #fff;
  border: 1px solid #ccc;
  border-radius: 4px;
  
  /* Typography */
  font-family: Arial, sans-serif;
  font-size: 1rem;
  line-height: 1.5;
  color: #333;
  
  /* Others */
  opacity: 1;
  z-index: 1;
}

/* Document with comments */
/**
 * Card component
 * Used for displaying content in a contained format
 */
.card {
  /* Base styles */
}

/* Modular CSS with custom properties */
.button {
  /* Use custom properties for theming */
  background: var(--button-bg, #007bff);
  color: var(--button-color, white);
  border-radius: var(--button-radius, 4px);
  padding: var(--button-padding, 0.5rem 1rem);
}
```

## Troubleshooting

### Common Issues

#### Specificity Problems
```css
/* Problem: Style not applying due to specificity */
.button { background: blue; }           /* Specificity: 10 */
#header .nav .button { background: red; } /* Specificity: 120 - wins */

/* Solutions */
/* 1. Increase specificity */
.main-content .button { background: blue; } /* Specificity: 20 */

/* 2. Use !important (last resort) */
.button { background: blue !important; }

/* 3. Restructure selectors */
.button--primary { background: blue; }   /* New class with higher specificity */
```

#### Box Model Issues
```css
/* Problem: Element larger than expected */
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid #ccc;
  /* Total width = 200 + 40 + 10 = 250px */
}

/* Solution: Use border-box */
.box {
  box-sizing: border-box;
  width: 200px;                    /* Total width = 200px */
  padding: 20px;
  border: 5px solid #ccc;
}
```

#### Margin Collapsing
```css
/* Problem: Margins collapse between adjacent elements */
.element1 { margin-bottom: 20px; }
.element2 { margin-top: 30px; }
/* Actual gap = 30px (not 50px) */

/* Solutions */
/* 1. Use padding instead */
.element1 { padding-bottom: 20px; }

/* 2. Use flexbox */
.container {
  display: flex;
  flex-direction: column;
  gap: 20px;                       /* Consistent spacing */
}

/* 3. Add border or padding to prevent collapse */
.container {
  padding: 1px 0;                  /* Prevents margin collapse */
}
```

#### Float Clearing Issues
```css
/* Problem: Parent doesn't contain floated children */
.parent {
  border: 1px solid #ccc;
}

.child {
  float: left;
  width: 50%;
}

/* Solutions */
/* 1. Clearfix */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

/* 2. Use flexbox or grid instead */
.parent {
  display: flex;
}

.child {
  flex: 1;                         /* No need for floats */
}
```

### Debugging Techniques
```css
/* Visual debugging borders */
* {
  border: 1px solid red;           /* See all element boundaries */
}

/* Debug specific elements */
.debug {
  border: 2px solid lime !important;
  background: rgba(255, 0, 0, 0.1) !important;
}

/* CSS debugging properties */
.debug-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  
  /* Visual grid debugging */
  background-image: 
    linear-gradient(rgba(255, 0, 0, 0.1) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 0, 0, 0.1) 1px, transparent 1px);
  background-size: 20px 20px;
}

/* Console debugging */
.element {
  /* Use CSS counters to debug */
  counter-increment: debug-counter;
}

.element::before {
  content: "Element #" counter(debug-counter);
  position: absolute;
  background: yellow;
  font-size: 12px;
  z-index: 9999;
}
```

### Browser DevTools Tips
```css
/* CSS that helps with debugging */

/* Highlight focus for keyboard navigation */
*:focus {
  outline: 3px solid orange !important;
  outline-offset: 2px;
}

/* Show empty elements */
*:empty {
  background: rgba(255, 255, 0, 0.1);
  border: 1px dashed red;
}

/* Highlight elements with no alt text */
img:not([alt]) {
  border: 3px solid red;
}

/* Show broken images */
img {
  position: relative;
}

img::after {
  content: "🖼 " attr(alt);
  position: absolute;
  top: 0;
  left: 0;
  background: #f0f0f0;
  border: 1px solid #ccc;
  padding: 10px;
  display: block;
  width: 100%;
  color: #666;
  font-size: 14px;
}
```

### Performance Debugging
```css
/* Identify expensive operations */
* {
  /* Highlight elements that trigger repaints */
  box-shadow: inset 0 0 0 1px red;
}

/* Monitor transform performance */
.animated {
  /* Use transform3d to force GPU acceleration */
  transform: translate3d(0, 0, 0);
  /* Or use will-change */
  will-change: transform, opacity;
}

/* Identify layout thrashing */
.layout-trigger {
  /* These properties cause layout recalculation */
  /* width, height, padding, margin, border, left, top, etc. */
  
  /* Prefer these for animations */
  transform: translateX(100px);     /* Compositing layer */
  opacity: 0.5;                    /* Compositing layer */
}

/* CSS containment for performance */
.independent-component {
  contain: layout style paint;      /* Isolate from rest of page */
}
```