# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Jekyll-based academic personal website for Maximilian Voigt (Assistant Professor of Finance, HEC Montréal), built on the `academicpages` fork of the Minimal Mistakes theme. Deployed to GitHub Pages at https://maxvoigt.github.io.

## Commands

```bash
# Install dependencies
bundle install

# Serve locally with live reload at localhost:4000
bundle exec jekyll liveserve

# Use dev config (disables analytics, sets localhost baseurl)
bundle exec jekyll liveserve --config _config.yml,_config.dev.yml

# Build only
bundle exec jekyll build

# Minify JS
npm run uglify
```

## Architecture

**Collections** are the core content model. Each collection item is a Markdown file with YAML frontmatter:
- `_publications/` → `/publication/[slug]`
- `_talks/` → `/talks/[slug]`
- `_teaching/` → `/teaching/[slug]`
- `_pages/` → static pages (about, CV, etc.)

**Content generation**: `markdown_generator/` contains Python scripts and Jupyter notebooks that convert TSV spreadsheets (`publications.tsv`, `talks.tsv`) into collection Markdown files. Edit the TSV first, then regenerate rather than editing generated Markdown directly.

**Layouts**: `_layouts/` wraps content. Key layouts: `default.html` (base, masthead hidden), `single.html` (articles with sidebar), `talk.html` (adds venue/location metadata), `archive.html` (listing pages).

**Styling**: SCSS in `_sass/`. Main entry point is `assets/css/main.scss`. Component files are organized by concern (`_page.scss`, `_sidebar.scss`, `_navigation.scss`, etc.).

**Site config**: `_config.yml` is the primary config. `_config.dev.yml` overrides for local development (disables analytics, sets `url: http://localhost:4000`).

**Deployment**: GitHub Actions (`.github/workflows/jekyll.yml`) builds and deploys on push to `master`.

## Content Frontmatter

Publications use fields: `title`, `collection`, `permalink`, `excerpt`, `date`, `venue`, `paperurl`, `citation`.

Talks use: `title`, `collection`, `type` (Talk/Tutorial/etc.), `permalink`, `venue`, `date`, `location`.

## Files and Assets

- PDFs and downloadable files go in `files/`
- Images go in `images/`
- Navigation structure is defined in `_data/navigation.yml`
