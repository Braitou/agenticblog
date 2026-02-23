# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Astro 5 static blog for **Agentic Flow** — an AI search optimization product for Shopify merchants. The blog covers AEO (Answer Engine Optimization), llms.txt, and getting Shopify products found by ChatGPT/Perplexity/Google AI Overviews.

## Commands

- `npm run dev` — Dev server at localhost:4321
- `npm run build` — Production build to `./dist/`
- `npm run preview` — Preview production build locally

No test runner or linter is configured.

## Architecture

**Static site generator**: Astro with MDX and sitemap integrations. No client-side framework (React/Vue/etc.) — pure Astro components with scoped CSS and a single global stylesheet (`src/styles/global.css`).

**Content system**: Blog posts live in `src/content/blog/` as Markdown files. The collection schema is defined in `src/content.config.ts` with Zod validation. Required frontmatter: `title`, `description`, `pubDate`. Optional: `updatedDate`, `heroImage`.

**Routing**: File-based. `src/pages/blog/[...slug].astro` generates individual post pages via `getStaticPaths()`. `src/pages/rss.xml.js` generates the RSS feed.

**Global constants**: `src/consts.ts` holds site title, description, URL, and Shopify app URL. These are imported throughout components for meta tags and links.

**Layouts**: Single layout `src/layouts/BlogPost.astro` wraps all blog post pages. `src/components/BaseHead.astro` handles all `<head>` meta/OG/Twitter tags.

## Deployment

GitHub Actions deploys to GitHub Pages on push to `main` branch (`.github/workflows/deploy.yml`). Uses Node 20, `npm ci`, then Astro build. Custom domain: `agentic-flow.app`.

## Adding a Blog Post

Create a new `.md` file in `src/content/blog/` with frontmatter:

```yaml
---
title: "Post Title"
description: "Short description"
pubDate: 2026-01-01
---
```

The post automatically appears on the homepage and blog index (sorted newest first), and is included in the RSS feed and sitemap.
