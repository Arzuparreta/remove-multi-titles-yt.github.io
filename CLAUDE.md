# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a GitHub Pages landing page for the "Remove Multi-Titles" browser extension. The extension addresses YouTube's A/B testing of video titles by showing the original title from page metadata instead of algorithm-selected variants.

The site is a single-page static site with no build process or dependencies.

## Architecture

- **Single-file architecture**: The entire site is contained in `index.html` with embedded CSS
- **No build system**: Direct HTML/CSS with no preprocessing, bundling, or build steps
- **GitHub Pages deployment**: Automated via GitHub Actions workflow in `.github/workflows/pages.yml`
- **No JavaScript**: The landing page is static HTML/CSS only (the extension itself is hosted separately on Chrome/Firefox stores)

## Development

### Local development

Open `index.html` directly in a browser or use a simple static file server:

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js (if available)
npx serve .
```

### Deployment

Deployment is automatic via GitHub Actions. The workflow in `.github/workflows/pages.yml`:
- Triggers on push to `main` branch
- Uses `actions/deploy-pages` action
- Requires `pages` and `id-token` permissions

To manually trigger a rebuild, make any commit to the `main` branch.

## Key Design Decisions

- **Store-style buttons**: Chrome button uses light background (Web Store pattern), Firefox button uses brand orange to avoid generic "social" blue appearance
- **Embedded CSS**: All styles are in `<style>` tags within `index.html` for simplicity and portability
- **No external CSS frameworks**: Custom CSS with CSS variables for theming
- **Responsive design**: Uses CSS Grid and Flexbox with mobile-first approach
- **Accessibility**: Semantic HTML, ARIA labels, and proper heading hierarchy

## File Structure

```
.
├── index.html              # Complete landing page with embedded CSS
├── README.md               # Minimal project description
└── .github/
    └── workflows/
        └── pages.yml       # GitHub Pages deployment workflow
```

## Common Tasks

### Update extension store links

Edit the `href` attributes in the store buttons (lines 438 and 451 in `index.html`):
- Chrome: `store-btn--chrome` link
- Firefox: `store-btn--firefox` link

### Modify styling

All CSS is in the `<style>` section (lines 11-411 in `index.html`). CSS variables are defined in `:root` (lines 12-33).

### Add new sections

Follow the existing pattern:
1. Add a `<section class="section">` with appropriate `aria-labelledby`
2. Use `.section-head` for section title and description
3. Use `.cards-grid` for card-based layouts
4. Add a `.divider` between sections

## Notes

- The extension source code is not in this repository—this is only the landing page
- Extension is distributed via Chrome Web Store and Firefox Add-ons
- No analytics or tracking is implemented on the landing page
- The site uses Google Fonts (Instrument Sans and Instrument Serif) via CDN
