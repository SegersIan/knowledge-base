# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal knowledge base website built with Hugo static site generator. Content is written in Markdown and published to https://kb.segersian.com. The site uses the hugo-book theme (git submodule) to provide a book-like navigation structure.

## Key Commands

### Development
- Build the site: `hugo` (Hugo must be installed separately)
- Start development server: `hugo server` (enables live reload)
- Start server with drafts: `hugo server -D`
- PDF rendering: `npm run render` (uses mdpdf for A4 format)

### Git Submodules
- Initialize theme submodule: `git submodule update --init --recursive`
- Update theme: `git submodule update --remote themes/hugo-book`

## Architecture

### Content Structure

Content is organized in `content/` directory with hierarchical topics:
- Each directory represents a topic (e.g., `ai/`, `cybersecurity/`, `software-architecture/`)
- `_index.md` files define section landing pages with `bookCollapseSection: true` for collapsible menus
- Individual `.md` files contain article content
- Front matter includes `title`, `tags`, and optionally `draft: true`

### Theme Customization

The hugo-book theme is customized via layouts overrides (not direct theme modifications):

**Custom Layouts:**
- `layouts/partials/docs/inject/head.html` - Injects Plausible Analytics and Mermaid.js scripts
- `layouts/_default/_markup/render-codeblock.html` - Custom code block rendering with Mermaid support
- `layouts/shortcodes/mermaid.html` - Mermaid diagram shortcode

**Rendering Features:**
- Mermaid diagrams: Use ` ```mermaid ` code blocks or `{{</* mermaid */>}}` shortcode
- LaTeX math: Enabled via unsafe HTML rendering in hugo.yaml
- Syntax highlighting: Uses base16-snazzy style

### Configuration (hugo.yaml)

Key settings:
- `baseURL`: https://kb.segersian.com/
- `theme`: hugo-book
- `enableGitInfo`: true (shows last modified dates from git)
- `markup.goldmark.renderer.unsafe`: true (required for LaTeX/custom HTML)
- `params.BookEditLink`: Links to GitHub edit page for each article
- `params.BookLastChangeLink`: Links to commit history

## Content Authoring

### Creating New Content

Use the archetype for consistent formatting:
```bash
hugo new <section>/<title>.md
```

Default front matter from `archetypes/default.md`:
```yaml
---
date: '{{ .Date }}'
draft: true
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
---
```

### Markdown Extensions

- Standard GitHub-flavored Markdown
- Mermaid diagrams for flowcharts/graphs
- LaTeX for mathematical notation (rendered via KaTeX in browser)
- Table of contents starts at level 1 (`startLevel: 1`)

### Navigation Structure

- Menu defined in `hugo.yaml` (external links to GitHub, blog)
- Sections auto-generate from directory structure
- `BookMenuBundle: true` enables bundle-based navigation
- `BookCollapseSection: true` makes sections collapsible by default

## Publishing

The site is published to https://kb.segersian.com with GitHub Pages or similar hosting. Built files are generated in `public/` directory (git-ignored).

## Important Notes

- **Never modify theme files directly** - the theme is a git submodule. Use layout overrides in `layouts/` instead
- **Content is public** - all content on this repository is publicly accessible and indexed
- **Work in Progress** - Many articles are incomplete; this is expected and acceptable
- **No build tooling** - Pure Hugo with no additional build steps (npm scripts are minimal)
