# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static personal portfolio and blog for thedomas.dev (Patryk Domasik). Hosted on GitHub Pages with custom domain. No build step, no framework — pure HTML/CSS/JS.

## Architecture

- **Static site** — each page is a standalone HTML file with inline `<style>` and `<script>` (no shared CSS/JS files)
- **Hosting**: GitHub Pages, domain configured via `CNAME` → `thedomas.dev`
- **SEO assets**: `robots.txt`, `sitemap.xml`, structured data (JSON-LD) in each page, Open Graph + Twitter Card meta tags

### Pages

| Route | File | Purpose |
|-------|------|---------|
| `/` | `index.html` | Portfolio homepage (hero, stack, projects, companies, about, certifications, contact) |
| `/blog/` | `blog/index.html` | Blog listing |
| `/blog/<slug>/` | `blog/<slug>/index.html` | Individual blog post |

### Assets structure

- `assets/` — images (project screenshots, profile photo in `.webp`)
- `assets/icons/` — tech stack SVG icons
- `assets/icons/companies/` — company logos (SVG/PNG/JPEG)
- `assets/blog/<slug>/` — blog post images

## Design system (inline in each page)

- **Fonts**: Space Grotesk (body), JetBrains Mono (code/tags) — loaded from Google Fonts
- **CSS variables** defined in `:root` — `--bg`, `--text`, `--accent`, `--border`, `--radius`, etc.
- **Scroll reveal**: `.reveal` class + IntersectionObserver JS pattern
- **Mobile nav**: hamburger toggle via `#hamburger` / `#navLinks`
- Responsive breakpoint: `768px`

## Google Analytics

gtag.js (`G-KLR02RFZ4K`) must be present in the `<head>` of **every** HTML page. This is a static site — there is no shared layout or SPA routing, so each page loads independently.

Current pages with gtag:
- `index.html`
- `blog/index.html`
- `blog/samsung-ac-monitoring-grafana-home-assistant/index.html`

## Adding a new blog post

1. Create `blog/<slug>/index.html` with full HTML document (copy structure from existing post)
2. Add post images to `assets/blog/<slug>/`
3. Add a `.post-card` link in `blog/index.html` pointing to the new post
4. Add a `<url>` entry in `sitemap.xml`
5. Include gtag snippet in the new page's `<head>`
6. Include structured data (JSON-LD), Open Graph, and Twitter Card meta tags

## Key conventions

- All styles are inline (`<style>` in `<head>`) — no external stylesheets
- All scripts are inline (`<script>` before `</body>`) — no external JS bundles
- Relative paths for internal links (e.g., `../` from blog to root, `../../` from post to root)
- `rel="noopener"` on all `target="_blank"` links
- Images use `.webp` format where possible
