# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal GitHub Pages blog/portfolio for Paweł Walczak, built with **Jekyll** (Ruby static site generator) and served at `pawwal.com`. Uses the **Minima** theme with Google Analytics (G-JNP0PGXKYL) and the `jekyll-feed` plugin for RSS.

## Local Development Commands

```bash
bundle install                 # Install Ruby gem dependencies
bundle exec jekyll serve       # Serve locally at http://localhost:4000 with live reload
bundle exec jekyll build       # Build static site to _site/
```

There are no tests or linters configured.

## Deployment

Pushing to `master` triggers GitHub Pages' built-in Jekyll build and deploy automatically. No CI/CD configuration is needed. The `CNAME` file sets the custom domain.

## Architecture

Jekyll processes the source files into a static site in `_site/` (git-ignored):

- **`_config.yml`** — Central configuration: theme, plugins, Google Analytics ID, LinkedIn/GitHub usernames, and which pages appear in the header nav (`header_pages: [reading_list.md]`).
- **`_posts/`** — Blog posts in Markdown. Jekyll renders these automatically; they appear on the homepage via the `home` layout.
- **`_includes/`** — Reusable HTML snippets (currently only `google-analytics.html`, injected via Minima theme layouts).
- **Root `.md`/`.markdown` pages** — Become standalone pages. `index.markdown` uses `layout: home`; other pages use `layout: page`.

The Minima theme provides all layout templates (`home`, `page`, `post`, `default`). There are no custom `_layouts/` overrides.

## Conventions

**Blog posts** must be named `YYYY-MM-DD-slug.md` inside `_posts/`. Front matter must include at minimum:
```yaml
---
layout: post
title: "Post Title"
date: YYYY-MM-DD HH:MM:SS +TIMEZONE
categories: category-name
---
```

**New pages** at the root level with `layout: page` in front matter become standalone pages. To add one to the header navigation, add its filename to `header_pages` in `_config.yml`.

**Liquid templating** is available in any content file for dynamic values (e.g., `{{ site.author }}` resolves from `_config.yml`).
