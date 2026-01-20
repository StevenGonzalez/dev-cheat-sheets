# HTML Cheat Sheet

Quick reference for HTML5 markup, semantic elements, and modern web standards. HTML (HyperText Markup Language) is the foundation of web pages and web applications.

## Table of Contents

- [Document Structure](#document-structure)
- [Basic Elements](#basic-elements)
- [Text Formatting](#text-formatting)
- [Lists](#lists)
- [Links and Navigation](#links-and-navigation)
- [Images and Media](#images-and-media)
- [Tables](#tables)
- [Forms](#forms)
- [Semantic Elements](#semantic-elements)
- [Meta Tags](#meta-tags)
- [Accessibility](#accessibility)
- [Modern HTML Features](#modern-html-features)
- [Web Components](#web-components)
- [Performance Optimization](#performance-optimization)
- [Best Practices](#best-practices)
- [Validation and Standards](#validation-and-standards)
- [Tools & References](#tools--references)

## Document Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Page description">
    <title>Page Title</title>
    <link rel="stylesheet" href="styles.css">
    <link rel="icon" href="favicon.ico">
</head>
<body>
    <header>
        <h1>Main Heading</h1>
        <nav>
            <ul>
                <li><a href="#section1">Section 1</a></li>
                <li><a href="#section2">Section 2</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <article>
            <h2>Article Title</h2>
            <p>Article content...</p>
        </article>
        
        <aside>
            <h3>Sidebar</h3>
            <p>Related content...</p>
        </aside>
    </main>
    
    <footer>
        <p>&copy; 2026 Website Name</p>
    </footer>
    
    <script src="script.js"></script>
</body>
</html>
```

## Basic Elements

```html
<!-- Headings (h1 is most important, h6 least) -->
<h1>Main Title</h1>
<h2>Section Title</h2>
<h3>Subsection Title</h3>
<h4>Sub-subsection Title</h4>
<h5>Minor Heading</h5>
<h6>Smallest Heading</h6>

<!-- Paragraphs and line breaks -->
<p>This is a paragraph of text.</p>
<p>Another paragraph.<br>With a line break.</p>

<!-- Horizontal rule -->
<hr>

<!-- Comments (not displayed) -->
<!-- This is a comment -->

<!-- Generic containers -->
<div class="container">Block-level container</div>
<span class="highlight">Inline container</span>
```

## Text Formatting

```html
<!-- Emphasis and importance -->
<em>Emphasized text (usually italic)</em>
<strong>Important text (usually bold)</strong>
<mark>Highlighted text</mark>
<small>Fine print</small>

<!-- Visual formatting (use CSS instead when possible) -->
<b>Bold text</b>
<i>Italic text</i>
<u>Underlined text</u>
<s>Strikethrough text</s>

<!-- Technical and semantic formatting -->
<code>inline code</code>
<pre><code>
// Preformatted code block
function hello() {
    console.log("Hello, World!");
}
</code></pre>

<kbd>Ctrl+C</kbd> <!-- Keyboard input -->
<samp>Sample output</samp> <!-- Program output -->
<var>variable</var> <!-- Mathematical variable -->

<!-- Quotations -->
<q>Short inline quote</q>
<blockquote cite="https://example.com">
    <p>Longer quoted text that stands alone.</p>
    <footer>— <cite>Author Name</cite></footer>
</blockquote>

<!-- Abbreviations and definitions -->
<abbr title="HyperText Markup Language">HTML</abbr>
<dfn>Definition term</dfn>

<!-- Subscript and superscript -->
H<sub>2</sub>O (water)
E=mc<sup>2</sup> (Einstein's equation)

<!-- Insertions and deletions -->
<ins datetime="2026-01-20">Added text</ins>
<del datetime="2026-01-19">Removed text</del>
```

## Lists

```html
<!-- Unordered list -->
<ul>
    <li>First item</li>
    <li>Second item
        <ul>
            <li>Nested item</li>
            <li>Another nested item</li>
        </ul>
    </li>
    <li>Third item</li>
</ul>

<!-- Ordered list -->
<ol>
    <li>First step</li>
    <li>Second step</li>
    <li>Third step</li>
</ol>

<!-- Ordered list with custom start -->
<ol start="5" type="a">
    <li>Fifth item (e)</li>
    <li>Sixth item (f)</li>
</ol>

<!-- Description list -->
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language</dd>
    
    <dt>CSS</dt>
    <dd>Cascading Style Sheets</dd>
    <dd>Used for styling web pages</dd>
</dl>
```

## Links and Navigation

```html
<!-- Basic links -->
<a href="https://example.com">External link</a>
<a href="/page.html">Internal link</a>
<a href="#section1">Link to section on same page</a>
<a href="mailto:user@example.com">Email link</a>
<a href="tel:+1234567890">Phone link</a>

<!-- Links with additional attributes -->
<a href="https://example.com" 
   target="_blank" 
   rel="noopener noreferrer">
   Open in new tab (secure)
</a>

<a href="document.pdf" 
   download="filename.pdf">
   Download file
</a>

<!-- Navigation with accessibility -->
<nav aria-label="Main navigation">
    <ul>
        <li><a href="/" aria-current="page">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>

<!-- Breadcrumb navigation -->
<nav aria-label="Breadcrumb">
    <ol>
        <li><a href="/">Home</a></li>
        <li><a href="/category">Category</a></li>
        <li aria-current="page">Current Page</li>
    </ol>
</nav>
```

## Images and Media

```html
<!-- Basic image -->
<img src="image.jpg" alt="Descriptive text" width="300" height="200">

<!-- Responsive image -->
<img src="image.jpg" 
     alt="Descriptive text"
     loading="lazy"
     decoding="async">

<!-- Picture element for responsive images -->
<picture>
    <source media="(min-width: 800px)" srcset="large.jpg">
    <source media="(min-width: 400px)" srcset="medium.jpg">
    <img src="small.jpg" alt="Responsive image">
</picture>

<!-- Image with different formats -->
<picture>
    <source srcset="image.avif" type="image/avif">
    <source srcset="image.webp" type="image/webp">
    <img src="image.jpg" alt="Modern format image">
</picture>

<!-- Figure with caption -->
<figure>
    <img src="chart.png" alt="Sales data chart">
    <figcaption>Q4 2025 Sales Performance</figcaption>
</figure>

<!-- Audio -->
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    Your browser does not support audio playback.
</audio>

<!-- Video -->
<video controls width="640" height="480" poster="preview.jpg">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    <track kind="subtitles" src="subtitles.vtt" srclang="en" label="English">
    Your browser does not support video playback.
</video>

<!-- Embedded content -->
<iframe src="https://example.com" 
        width="800" 
        height="600"
        title="Embedded content"
        loading="lazy">
</iframe>
```

## Tables

```html
<!-- Basic table -->
<table>
    <thead>
        <tr>
            <th>Product</th>
            <th>Price</th>
            <th>Stock</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Laptop</td>
            <td>$999</td>
            <td>15</td>
        </tr>
        <tr>
            <td>Phone</td>
            <td>$599</td>
            <td>32</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Total</td>
            <td>$1598</td>
            <td>47</td>
        </tr>
    </tfoot>
</table>

<!-- Table with accessibility -->
<table role="table" aria-label="Product inventory">
    <caption>Current Product Inventory - January 2026</caption>
    <thead>
        <tr>
            <th scope="col">Product Name</th>
            <th scope="col">Unit Price</th>
            <th scope="col">Units in Stock</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Gaming Laptop</th>
            <td>$1,299.99</td>
            <td>8</td>
        </tr>
    </tbody>
</table>

<!-- Complex table with spanning -->
<table>
    <tr>
        <th rowspan="2">Product</th>
        <th colspan="2">Sales</th>
    </tr>
    <tr>
        <th>Q3</th>
        <th>Q4</th>
    </tr>
    <tr>
        <td>Laptops</td>
        <td>150</td>
        <td>200</td>
    </tr>
</table>
```

## Forms

```html
<!-- Complete form example -->
<form action="/submit" method="post" enctype="multipart/form-data">
    <!-- Text inputs -->
    <div>
        <label for="name">Full Name*</label>
        <input type="text" 
               id="name" 
               name="name" 
               required 
               autocomplete="name"
               placeholder="Enter your full name">
    </div>
    
    <!-- Email input -->
    <div>
        <label for="email">Email Address*</label>
        <input type="email" 
               id="email" 
               name="email" 
               required 
               autocomplete="email">
    </div>
    
    <!-- Password input -->
    <div>
        <label for="password">Password*</label>
        <input type="password" 
               id="password" 
               name="password" 
               required 
               minlength="8"
               autocomplete="new-password">
    </div>
    
    <!-- Number input -->
    <div>
        <label for="age">Age</label>
        <input type="number" 
               id="age" 
               name="age" 
               min="13" 
               max="120" 
               step="1">
    </div>
    
    <!-- Date input -->
    <div>
        <label for="birthdate">Birth Date</label>
        <input type="date" id="birthdate" name="birthdate">
    </div>
    
    <!-- Select dropdown -->
    <div>
        <label for="country">Country</label>
        <select id="country" name="country" required>
            <option value="">Choose a country</option>
            <option value="us">United States</option>
            <option value="ca">Canada</option>
            <option value="uk">United Kingdom</option>
        </select>
    </div>
    
    <!-- Radio buttons -->
    <fieldset>
        <legend>Preferred Contact Method</legend>
        <div>
            <input type="radio" id="contact-email" name="contact" value="email">
            <label for="contact-email">Email</label>
        </div>
        <div>
            <input type="radio" id="contact-phone" name="contact" value="phone">
            <label for="contact-phone">Phone</label>
        </div>
    </fieldset>
    
    <!-- Checkboxes -->
    <fieldset>
        <legend>Interests</legend>
        <div>
            <input type="checkbox" id="tech" name="interests" value="technology">
            <label for="tech">Technology</label>
        </div>
        <div>
            <input type="checkbox" id="sports" name="interests" value="sports">
            <label for="sports">Sports</label>
        </div>
    </fieldset>
    
    <!-- Textarea -->
    <div>
        <label for="message">Message</label>
        <textarea id="message" 
                  name="message" 
                  rows="4" 
                  cols="50"
                  placeholder="Enter your message here..."></textarea>
    </div>
    
    <!-- File upload -->
    <div>
        <label for="resume">Resume</label>
        <input type="file" 
               id="resume" 
               name="resume" 
               accept=".pdf,.doc,.docx">
    </div>
    
    <!-- Hidden input -->
    <input type="hidden" name="form_id" value="contact_form_v2">
    
    <!-- Submit and reset buttons -->
    <div>
        <button type="submit">Submit Form</button>
        <button type="reset">Clear Form</button>
        <button type="button" onclick="goBack()">Cancel</button>
    </div>
</form>

<!-- Modern input types -->
<input type="color" name="theme-color">
<input type="range" name="volume" min="0" max="100" value="50">
<input type="search" name="query" placeholder="Search...">
<input type="tel" name="phone" autocomplete="tel">
<input type="url" name="website" placeholder="https://example.com">
<input type="time" name="appointment">
<input type="datetime-local" name="event-time">
<input type="month" name="birth-month">
<input type="week" name="vacation-week">
```

## Semantic Elements

```html
<!-- Page structure -->
<header>
    <h1>Site Title</h1>
    <nav aria-label="Main navigation">
        <!-- Navigation links -->
    </nav>
</header>

<main>
    <!-- Primary content -->
    <article>
        <header>
            <h2>Article Title</h2>
            <p>Published on <time datetime="2026-01-20">January 20, 2026</time></p>
            <p>By <address>John Doe</address></p>
        </header>
        
        <section>
            <h3>Introduction</h3>
            <p>Article content...</p>
        </section>
        
        <section>
            <h3>Main Content</h3>
            <p>More article content...</p>
        </section>
        
        <footer>
            <p>Tags: <span>HTML</span>, <span>Web Development</span></p>
        </footer>
    </article>
    
    <aside>
        <h3>Related Articles</h3>
        <ul>
            <li><a href="/article1">Related Article 1</a></li>
            <li><a href="/article2">Related Article 2</a></li>
        </ul>
    </aside>
</main>

<footer>
    <div>
        <h4>Contact Information</h4>
        <address>
            <p>123 Web Street<br>
            Internet City, IC 12345<br>
            <a href="mailto:contact@example.com">contact@example.com</a></p>
        </address>
    </div>
    
    <div>
        <p>&copy; 2026 Company Name. All rights reserved.</p>
    </div>
</footer>

<!-- Additional semantic elements -->
<details>
    <summary>Click to expand</summary>
    <p>Hidden content that can be toggled.</p>
</details>

<dialog id="modal">
    <h3>Modal Dialog</h3>
    <p>Modal content goes here.</p>
    <button onclick="closeModal()">Close</button>
</dialog>
```

## Meta Tags

```html
<head>
    <!-- Character encoding (must be first) -->
    <meta charset="UTF-8">
    
    <!-- Viewport for responsive design -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- Page description for search engines -->
    <meta name="description" content="Learn HTML with this comprehensive cheat sheet">
    
    <!-- Keywords (less important now) -->
    <meta name="keywords" content="HTML, web development, markup">
    
    <!-- Author information -->
    <meta name="author" content="Developer Name">
    
    <!-- Refresh/redirect -->
    <meta http-equiv="refresh" content="30">
    
    <!-- Security headers -->
    <meta http-equiv="X-Content-Type-Options" content="nosniff">
    <meta http-equiv="X-Frame-Options" content="DENY">
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'">
    
    <!-- Open Graph (social media) -->
    <meta property="og:title" content="Page Title">
    <meta property="og:description" content="Page description">
    <meta property="og:image" content="https://example.com/image.jpg">
    <meta property="og:url" content="https://example.com/page">
    <meta property="og:type" content="website">
    <meta property="og:site_name" content="Site Name">
    
    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="Page Title">
    <meta name="twitter:description" content="Page description">
    <meta name="twitter:image" content="https://example.com/image.jpg">
    <meta name="twitter:creator" content="@username">
    
    <!-- Favicon -->
    <link rel="icon" href="/favicon.ico" sizes="any">
    <link rel="icon" href="/favicon.svg" type="image/svg+xml">
    <link rel="apple-touch-icon" href="/apple-touch-icon.png">
    <link rel="manifest" href="/manifest.json">
    
    <!-- Preconnect for performance -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="dns-prefetch" href="https://cdn.example.com">
    
    <!-- Canonical URL -->
    <link rel="canonical" href="https://example.com/page">
</head>
```

## Accessibility

```html
<!-- ARIA landmarks -->
<nav role="navigation" aria-label="Main navigation">
    <ul>
        <li><a href="/" aria-current="page">Home</a></li>
        <li><a href="/about">About</a></li>
    </ul>
</nav>

<!-- ARIA labels and descriptions -->
<button aria-label="Close dialog">×</button>
<input type="text" aria-describedby="password-help">
<div id="password-help">Password must be at least 8 characters</div>

<!-- Skip links -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Accessible forms -->
<form>
    <fieldset>
        <legend>Personal Information</legend>
        <label for="first-name">First Name *</label>
        <input type="text" id="first-name" required aria-required="true">
        <span role="alert" id="name-error">Please enter your first name</span>
    </fieldset>
</form>

<!-- Accessible tables -->
<table role="table" aria-labelledby="table-title">
    <caption id="table-title">Sales Data for Q4 2025</caption>
    <thead>
        <tr>
            <th scope="col" id="product">Product</th>
            <th scope="col" id="sales">Sales</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row" id="laptops">Laptops</th>
            <td headers="laptops sales">$50,000</td>
        </tr>
    </tbody>
</table>

<!-- Focus management -->
<div tabindex="0" role="button" aria-pressed="false">Custom button</div>

<!-- Live regions -->
<div aria-live="polite" id="status"></div>
<div aria-live="assertive" id="errors"></div>

<!-- Hidden content -->
<span aria-hidden="true">👍</span> <!-- Decorative emoji -->
<div class="visually-hidden">Content for screen readers only</div>
```

## Modern HTML Features

```html
<!-- Web Components -->
<template id="user-card-template">
    <div class="user-card">
        <img class="avatar" alt="User avatar">
        <h3 class="name"></h3>
        <p class="email"></p>
    </div>
</template>

<!-- Custom elements -->
<user-profile data-user-id="123"></user-profile>

<!-- Shadow DOM example -->
<div id="shadow-host"></div>
<script>
    const host = document.getElementById('shadow-host');
    const shadow = host.attachShadow({mode: 'closed'});
    shadow.innerHTML = '<p>Shadow DOM content</p>';
</script>

<!-- Progressive Web App features -->
<link rel="manifest" href="/manifest.json">
<meta name="theme-color" content="#000000">
<meta name="apple-mobile-web-app-capable" content="yes">

<!-- Modern input attributes -->
<input type="email" 
       list="email-suggestions"
       pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"
       autocomplete="email"
       spellcheck="false">
<datalist id="email-suggestions">
    <option value="user@gmail.com">
    <option value="user@yahoo.com">
</datalist>

<!-- Content Security Policy -->
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; script-src 'self' 'unsafe-inline'">

<!-- Lazy loading -->
<img src="image.jpg" alt="Description" loading="lazy">
<iframe src="embed.html" loading="lazy"></iframe>

<!-- Preloading resources -->
<link rel="preload" href="critical.css" as="style">
<link rel="preload" href="hero-image.jpg" as="image">
<link rel="prefetch" href="next-page.html">

<!-- Module scripts -->
<script type="module" src="main.js"></script>
<script type="module">
    import { component } from './component.js';
</script>
```

## Performance Optimization

```html
<!-- Critical resource hints -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="dns-prefetch" href="https://cdn.example.com">
<link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>

<!-- Optimize images -->
<picture>
    <source srcset="hero-small.avif" media="(max-width: 600px)" type="image/avif">
    <source srcset="hero-large.avif" media="(min-width: 601px)" type="image/avif">
    <source srcset="hero-small.webp" media="(max-width: 600px)" type="image/webp">
    <source srcset="hero-large.webp" media="(min-width: 601px)" type="image/webp">
    <img src="hero-fallback.jpg" alt="Hero image" loading="lazy" decoding="async">
</picture>

<!-- Async and defer scripts -->
<script src="analytics.js" async></script>
<script src="main.js" defer></script>

<!-- Resource prioritization -->
<link rel="stylesheet" href="critical.css">
<link rel="preload" href="non-critical.css" as="style" onload="this.onload=null;this.rel='stylesheet'">

<!-- Service Worker registration -->
<script>
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
}
</script>
```

## Best Practices

```html
<!-- 1. Use semantic HTML -->
<!-- Good: -->
<article>
    <h2>Article Title</h2>
    <p>Article content...</p>
</article>

<!-- Avoid: -->
<div class="article">
    <div class="title">Article Title</div>
    <div class="content">Article content...</div>
</div>

<!-- 2. Always include alt text for images -->
<img src="chart.png" alt="Sales increased 25% from Q3 to Q4 2025">

<!-- 3. Use proper form labels -->
<label for="email">Email Address</label>
<input type="email" id="email" name="email">

<!-- 4. Include viewport meta tag -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- 5. Use HTTPS for all external resources -->
<link rel="stylesheet" href="https://cdn.example.com/styles.css">

<!-- 6. Validate forms on both client and server -->
<input type="email" required pattern="[^@]+@[^@]+\.[^@]+">

<!-- 7. Use descriptive link text -->
<a href="/report.pdf">Download Q4 2025 Sales Report (PDF, 2MB)</a>

<!-- 8. Progressive enhancement -->
<button onclick="submitForm()" type="submit">Submit</button>

<!-- 9. Minimize HTTP requests -->
<link rel="stylesheet" href="combined-styles.css">

<!-- 10. Use consistent indentation and formatting -->
<article>
    <header>
        <h2>Title</h2>
    </header>
    <section>
        <p>Content</p>
    </section>
</article>
```

## Validation and Standards

```html
<!-- HTML5 DOCTYPE (required) -->
<!DOCTYPE html>

<!-- Valid HTML structure -->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Valid Document</title>
</head>
<body>
    <!-- Content -->
</body>
</html>

<!-- Validation tools -->
<!-- Use W3C Markup Validator: https://validator.w3.org/ -->
<!-- Use WAVE Web Accessibility Evaluator: https://wave.webaim.org/ -->
<!-- Use Lighthouse in Chrome DevTools -->

<!-- HTML standards compliance -->
<!-- Follow HTML Living Standard: https://html.spec.whatwg.org/ -->
<!-- Use semantic elements appropriately -->
<!-- Ensure proper nesting of elements -->
<!-- Close all tags properly -->
<!-- Use lowercase for element names and attributes -->
```

## Tools & References

### Development Tools
- **VS Code** with HTML extensions
- **Chrome DevTools** for debugging and performance
- **Firefox Developer Tools** for accessibility testing
- **Lighthouse** for performance and accessibility audits
- **WAVE** for accessibility evaluation

### Validation and Testing
- **W3C Markup Validator**: https://validator.w3.org/
- **HTML5 Validator**: https://html5.validator.nu/
- **aXe DevTools**: Accessibility testing
- **Pa11y**: Command-line accessibility testing

### Documentation and Learning
- [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [HTML Living Standard](https://html.spec.whatwg.org/)
- [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/WCAG21/quickref/)
- [Can I Use](https://caniuse.com/) - Browser compatibility tables

### Performance Tools
- **PageSpeed Insights**: Google's performance analyzer
- **WebPageTest**: Detailed performance testing
- **GTmetrix**: Performance monitoring

### HTML Preprocessors and Frameworks
- **Pug**: Clean, whitespace-sensitive syntax
- **Handlebars**: Logic-less templates
- **Mustache**: Logic-less templates

---

*This HTML cheat sheet covers modern web standards and best practices as of 2026. Always validate your HTML and test for accessibility across different browsers and devices.*
```
```