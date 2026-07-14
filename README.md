# parthshr370.github.io

Personal site. Built with Jekyll, Tailwind CSS (browser CDN), and a custom Catppuccin Mocha / Orange theme.

## Run locally

The current development environment uses Ruby 3.3 through `mise` and installs gems locally:

```bash
cd /path/to/parthshr370.github.io
mise install ruby@3.3
BUNDLE_PATH=vendor/bundle mise exec ruby@3.3 -- bundle install
BUNDLE_PATH=vendor/bundle mise exec ruby@3.3 -- bundle exec jekyll serve
```

Open `http://127.0.0.1:4000/`.

Build the published output without starting a server:

```bash
BUNDLE_PATH=vendor/bundle mise exec ruby@3.3 -- bundle exec jekyll build
```

## Structure

```
_layouts/          # page templates (default.html, post.html)
_includes/         # shared components (head, nav, theme toggle, socials)
assets/css/        # style.css with theme variables
assets/fonts/      # ZedMono Nerd Font
blogs/             # blog posts, each in its own folder
projects/          # projects page
_config.yml        # jekyll config
```

## Visual and interaction decisions

### Header

The shared header is intentionally **in flow**, not a fixed or floating global pill. It lives in `_includes/nav.html` and is used by `_layouts/default.html` and `_layouts/post.html`.

- Keep the compact title, primary links, divider, and theme button.
- Do not add global fixed navigation or reserve artificial top padding; it makes the narrow editorial layout feel sparse.
- The existing orange, blue, cyan, gold, muted, and syntax colors are part of the site identity. Create hierarchy with spacing, type, weight, and metadata contrast rather than removing colors.

### Homepage writing

`index.html` owns the manually curated Writing section:

- one featured post;
- three recent-post links;
- a link to the full blog index.

When publishing a newer post, update that section deliberately: promote the newest post to the feature, shift the prior feature into the short list, and keep exactly three recent entries. The related styles are `.featured-writing`, `.writing-list`, and `.writing-list__link` in `assets/css/style.css`.

### Homepage experience and reading

`index.html` also owns the concise Work Experience and Reading sections.

- Keep the current Lyzr-AI entry first and concise; role details belong only where explicitly requested.
- Keep prior roles as compact supporting context.
- The Reading section is a manually curated list of external articles and papers. Keep the “Interesting reads I found recently.” subtitle, use concise descriptions, open external sources in a new tab, and retain `rel="noopener noreferrer"` on every `target="_blank"` link.

### Blog index cards

`blogs/index.html` marks featured cards with `post-card` and a color variant:

- `post-card--primary`
- `post-card--secondary`
- `post-card--cyan`
- `post-card--gold`

Use a variant that matches the post’s existing accent; do not flatten every card to the same hover color. Card interaction is intentionally limited to border/surface/shadow refinement—no scale, glow, or large movement.

### Posts

`_layouts/post.html` provides two reading aids automatically:

1. A two-pixel theme-primary reading-progress line at the top. It updates during scrolling.
2. A contextual `On this page` control for posts with at least two `h2[id]` or `h3[id]` headings. It stays hidden until the authored Table of Contents has passed above the viewport, lists headings in document order, indents `h3` entries, and marks the active section.

The post control closes on item selection, outside click, and `Escape`; `Escape` restores trigger focus. New post headings need stable `id` values to appear in it. Keep the authored top Table of Contents for readers at the beginning of a post; the contextual control extends, rather than replaces, it.

Article typography and these controls are styled in `assets/css/style.css`. Preserve the quiet reading rhythm: modestly relaxed paragraphs, balanced headings, slate-like code surfaces, and no decorative page-wide effects.

## Adding a new blog post

Create `blogs/my-post/index.html`:

```html
---
layout: post
title: "My Post Title"
date_display: "March 6, 2026"
read_time: "5 min read"
permalink: /blogs/my-post/
prism:
  - python
---

<h2 id="first-section">First section</h2>
<p>Your content here. Use whatever HTML + Tailwind classes you want.</p>

<h3 id="useful-detail">Useful detail</h3>
<p>Give each navigable section a stable ID.</p>
```

The `prism` field is optional -- add language names to load syntax highlighting for code blocks.

Then add a link to it in `blogs/index.html`.
