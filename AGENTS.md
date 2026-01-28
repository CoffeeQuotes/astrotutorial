# AGENTS.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

This is an Astro tutorial project - a minimal blog site that demonstrates Astro's core concepts including file-based routing, layouts, components, and Markdown content integration.

## Development Commands

All commands run from the project root:

- `npm run dev` - Start dev server at localhost:4321
- `npm run build` - Build production site to `./dist/`
- `npm run preview` - Preview production build locally
- `npm run astro ...` - Run Astro CLI commands (e.g., `npm run astro add`, `npm run astro check`)

## Architecture

### File-Based Routing
Pages are automatically routed based on file structure in `src/pages/`:
- `.astro` files become HTML pages
- `.md` files in `src/pages/posts/` become blog post routes
- Route paths match file paths (e.g., `src/pages/about.astro` → `/about`)

### Layout System
Two-tier layout architecture:
- `BaseLayout.astro` - Root layout with Header, Footer, and global styles. Accepts `pageTitle` prop. Includes menu.js script for navigation interactivity
- `MarkdownPostLayout.astro` - Wraps BaseLayout, designed for Markdown posts. Accesses frontmatter props (title, pubDate, description, author, image, tags)

### Component Organization
- `components/` - Reusable Astro components (Header, Footer, Navigation, Menu, Social)
- `layouts/` - Layout wrappers that structure pages
- `scripts/` - Client-side JavaScript (menu.js handles mobile menu toggle)
- `styles/` - Global CSS imported by BaseLayout

### Content Management
Blog posts are Markdown files in `src/pages/posts/` with YAML frontmatter:
- Required fields: layout, title, pubDate, description, author, image (url, alt), tags
- Posts are collected using `import.meta.glob("./posts/*.md", { eager: true })` on the blog page
- Each post automatically uses MarkdownPostLayout specified in frontmatter

## Key Patterns

### Adding New Pages
Create `.astro` files in `src/pages/` - they automatically become routes. Wrap content in BaseLayout for consistent structure.

### Adding Blog Posts
Create `.md` files in `src/pages/posts/` with proper frontmatter. The layout field must reference MarkdownPostLayout for proper rendering.

### Modifying Global Layout
Edit `BaseLayout.astro` to change site-wide structure. Changes affect all pages using this layout.

## TypeScript Configuration
Uses Astro's strict TypeScript config (`astro/tsconfigs/strict`). Type checking available via `npm run astro check`.
