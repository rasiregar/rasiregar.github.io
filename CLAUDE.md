# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build & Serve Commands

**Local development (Quarto — primary):**
```bash
quarto preview
```

**Local development (Jekyll — legacy):**
```bash
bundle exec jekyll serve
```

**Production build (Quarto):**
```bash
quarto render
```

Deployment is automated via GitHub Actions on push to `main`: `.github/workflows/quarto.yml` runs `quarto render`; `.github/workflows/jekyll.yml` runs the Jekyll build.

## Architecture

This is a **dual-stack personal website** — Quarto is the active system; Jekyll is legacy and kept for reference. Both output to `_site/`.

### Quarto (primary)
- **Config**: `_quarto.yml` — theme: Litera (Bootstrap), Google Analytics, navbar
- **Pages**: `index.qmd`, `about.qmd`, `thoughts.qmd`, `contact.qmd`
- **Posts**: `posts/*.qmd` — blog posts in Quarto markdown
- **Post metadata**: `posts/_metadata.yml` — configures Utterances comments (GitHub-backed, repo: rasiregar/rasiregar.github.io)
- **Styling**: `custom.scss` — overrides for Litera theme

### Jekyll (legacy)
- **Config**: `_config.yml` — theme: Minima, plugin: jekyll-feed
- **Posts**: `_posts/*.markdown` — original post source (36 posts, 2017–2026)
- **Layouts**: `_layouts/home.html`, `_layouts/post.html`
- **Includes**: `_includes/header.html`
- **Styling**: `assets/css/style.scss`

### Design tokens (consistent across both systems)
- Accent: `#2d6a4f` (forest green)
- Text: `#1a1a1a`, Muted: `#6e6e73`, Border: `#ebebeb`, BG: `#ffffff`
- Max content width: `680px`
- Font: system sans-serif stack (`-apple-system`, Helvetica Neue, Arial)

### Key integrations
- **Comments**: Utterances (GitHub Issues), configured in `posts/_metadata.yml`
- **Contact form**: Formspree, in `contact.qmd`
- **Analytics**: Google Analytics G-2BCRMN1T6G, in `_quarto.yml`

### Adding a new blog post
Create `posts/YYYY-MM-DD-slug.qmd` with this front matter:
```yaml
---
title: "Post title"
author: Risyad Abiyyu Siregar
date: YYYY-MM-DD
categories: [health, society, reflections]
---
```
Posts automatically appear on the Thoughts listing page (`thoughts.qmd`).

### About page
`about.qmd` renders a 2-column grid (sidebar: photo + links, main: bio). Collapsible `<details>` sections hold Education, Experience, and Publications — edit those directly in the file.
