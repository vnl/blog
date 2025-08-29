# Viv's Thoughts — Jekyll Blog

A simple blog powered by Jekyll and the Minima theme, built with the GitHub Pages stack. The site is published under the path `/blog` at https://vivianlobo.com/blog.

## Quick start

- macOS prerequisites
  - Ruby (3.4+ works here)
  - Bundler
  - Command Line Tools for Xcode may be required for native gems
- Install deps

```bash
bundle install
```

- Serve locally

```bash
bundle exec jekyll serve
```

Then open http://localhost:4000/blog/ (note the `/blog` baseurl).

- Build static site

```bash
bundle exec jekyll build
```

Outputs to `_site/`.

## Project layout

- `_posts/` — Blog posts (YYYY-MM-DD-title.md)
- `_includes/` — Theme includes (custom `google-analytics.html`)
- `index.html` — Home page (uses `layout: home`, supports pagination)
- `about.md` — About page
- `favicon.ico` — Site icon served from the root
- `_config.yml` — Site configuration

## Writing posts

Create a new file in `_posts/` with this naming convention: `YYYY-MM-DD-your-title.markdown`.

Minimal front matter example:

```yaml
---
layout: post
title: "Post title"
date: 2025-08-29 12:00:00 +0000
categories: [life]
tags: [note]
excerpt: "One‑sentence summary for feeds and previews."
# published: false     # uncomment to hide a draft post
# image: /assets/images/cover.jpg
---
```

Drafts (optional): place files in `_drafts/` and run:

```bash
bundle exec jekyll serve --drafts
```

## Pagination

Pagination is enabled via `_config.yml`:

```yaml
paginate: 5
paginate_path: "/page:num/"
```

The homepage must be an HTML template (this repo uses `index.html` with `layout: home`). Jekyll will paginate your posts there.

## SEO, feed, and sitemap

Enabled plugins:
- `jekyll-seo-tag` — metadata
- `jekyll-feed` — RSS/Atom feed
- `jekyll-sitemap` — XML sitemap

These are GitHub Pages–compatible and work automatically.

## Google Analytics (GA4)

Configured via `_config.yml`:

```yaml
google_analytics: G-TSKPPBVCB6
```

The custom include at `_includes/google-analytics.html` injects GA4 only in production builds. You don’t need to paste the script in pages.

## Favicon

Replace `favicon.ico` in the project root with your own icon. Browsers request `/favicon.ico` by default; keeping it at the root avoids 404s.

## Base URL and site URL

From `_config.yml`:

```yaml
baseurl: "/blog"
url: "https://vivianlobo.com/"
```

- Local serve → http://localhost:4000/blog/
- Production → https://vivianlobo.com/blog/

If you change the publication path (e.g., move the blog to `/`), update `baseurl` accordingly and test.

## Deploying to GitHub Pages

This project uses the `github-pages` gem so local builds match GitHub’s environment.

Typical steps:
- Push your changes to the repository branch configured for Pages in GitHub settings (commonly `gh-pages` or `main`).
- If using a custom domain, configure it in the repository Pages settings and DNS.
- Ensure `_config.yml` `url` and `baseurl` are correct for the final domain/path.

## Troubleshooting

- Pagination warning: “Pagination is enabled, but I couldn't find an index.html …”
  - Ensure `index.html` exists and uses `layout: home` (not Markdown).
- Favicon 404
  - Keep a `favicon.ico` at the project root.
- Faraday v2 retry message: “To use retry middleware with Faraday v2.0+, install faraday-retry gem”
  - This is harmless for most local builds. You can ignore it.
- Recursive include / `stack level too deep`
  - Avoid overriding `_includes/head.html` to include itself. Use `_includes/google-analytics.html` and set `google_analytics` in config instead.

## Useful commands

```bash
# Serve locally (auto-regenerate)
bundle exec jekyll serve

# Serve with drafts
bundle exec jekyll serve --drafts

# Build the site (no server)
bundle exec jekyll build

# Clean and rebuild
rm -rf _site && bundle exec jekyll build
```

## Tech stack

- Jekyll 3.x via `github-pages` gem
- Theme: `minima`
- Plugins: `jekyll-feed`, `jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-paginate`, `jekyll-redirect-from`, `jekyll-mentions`, `jekyll-include-cache`

If you want more customization (custom layouts, SCSS, or components), I can scaffold those next.