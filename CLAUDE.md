# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an AI research project page built on the **Clarity** template — a static HTML/CSS/JS website template for presenting AI research papers. The main deliverable is a static site (`index.html` or customized from `clarity.html`/`minimal.html`) deployed via GitHub Pages or similar.

## Stylesheet Compilation

The CSS is compiled from SCSS. There are two stylesheet variants:

- **Free fonts** (default): compile `assets/stylesheets/main_free.scss` → `assets/stylesheets/main_free.css`
- **Licensed fonts**: compile `assets/stylesheets/main.scss` → `assets/stylesheets/main.css`
- The `clarity/clarity.scss` component imports `assets/stylesheets/master` (note: no underscore — resolves to `_master.scss`)

To compile SCSS (requires `sass` CLI):
```bash
sass assets/stylesheets/main_free.scss assets/stylesheets/main_free.css
sass clarity/clarity.scss clarity/clarity.css
```

For watch mode during development:
```bash
sass --watch assets/stylesheets/main_free.scss:assets/stylesheets/main_free.css
```

To preview the site locally:
```bash
python3 -m http.server 8000
# then open http://localhost:8000/clarity.html
```

## Architecture

### File Structure
- `clarity.html` — full-featured demo/reference template with all supported components
- `minimal.html` — minimal starter template for a new project page
- `assets/stylesheets/_master.scss` — shared SCSS variables (breakpoints, font sizes, colors)
- `assets/stylesheets/main_free.scss` — free-font variant (imports `main.scss`)
- `assets/stylesheets/main.scss` — licensed-font variant
- `clarity/clarity.scss` — Clarity grid and component styles (imports `_master.scss`)
- `clarity/clarity.js` — slideshow and interactive component logic
- `assets/scripts/navbar.js` — floating table-of-contents sidebar (injected via script tag)
- `assets/scripts/main.js` — base JS utilities

### CSS Architecture
`_master.scss` defines all shared variables (breakpoints, font sizes, color palette). Both `main_free.scss` and `main.scss` import it via `main.scss`. Component styles live in `clarity/clarity.scss`.

### HTML Structure Pattern
Every page section is wrapped in `<div class="container blog [modifier] [id]">`. Key layout classes:
- `.columns-N` (2–12) — CSS grid layouts
- `.blog-title` / `.blog-title white` / `.blog-title no-cover` — hero section variants
- `id="first-content"` on the hero div — used by `navbar.js` to anchor navigation

### Theme Variants
- **Light**: `background-color: #E0E4E6;` on hero + default `.blog-title`
- **Dark**: dark background + `.blog-title white`
- **No-cover**: `.blog-title no-cover` removes the project cover image layout
- **Gradient**: `background: linear-gradient(...)` on hero div

### Optional Features
- **Navbar/TOC**: enabled by including `<script src="assets/scripts/navbar.js"></script>` — remove the tag to disable
- **Image comparison slider**: via `img-comparison-slider` CDN library
- **Math**: MathJax 2.7 with `$...$` inline and `$$...$$` display delimiters
- **Syntax highlighting**: highlight.js via CDN
- **Slideshow**: handled by `clarity/clarity.js`

### Font Options
1. **Free** (default): Charter (local woff2 in `assets/fonts/`) + Poppins (Google Fonts)
2. **Licensed**: Tiempos Text + Athletics (place in `assets/fonts/`, update `_master.scss` font-size variables)

Switch between variants by changing the CSS `<link>` in the HTML `<head>` between `main_free.css` and `main.css`.
