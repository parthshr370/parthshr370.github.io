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
_includes/         # shared components (head, nav, frame, theme toggle, socials)
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
- On the homepage the name is the page `h1`. On every other page it is a plain bold `text-xl` brand line, and the page content owns its `h1` (Projects, Writing, or the post title).
- `.site-nav` links are muted; the current page gets `aria-current="page"` from `nav_active` and turns primary with an underline. Other links turn primary on hover/focus. Nav links and the theme button have a 40px minimum tap height.
- The theme button is `type="button"` and its `aria-label`/`title` name the destination theme (`head.html` updates it); its SVG icons are `aria-hidden`.
- Do not add global fixed navigation or reserve artificial top padding; it makes the narrow editorial layout feel sparse.
- `_includes/frame.html` draws a fixed, decorative 1px viewport border with corner ticks, inset by `--frame-inset` (20px, 8px under 640px). Content inside the border stays sharp; four `.frame__gutter` strips blur (8px, 55% background) whatever scrolls through the space outside it. Do not add blur or fades inside the border. The post `On this page` control sits inside the frame, tied to `--frame-inset`.
- The content column is `w-[90%] max-w-[42rem]` on `<body>` in both layouts.
- Both layouts start with a keyboard-visible `Skip to main content` link targeting `#main-content`. `default.html` wraps page content in `<main id="main-content" class="site-page">`; `post.html` wraps the article in `<main id="main-content">` with `<article class="post-article">`.
- The orange theme is shades of one orange (see COLORSCHEME.md), with one exception: off-site links on non-post pages use muted teal `--external-link` (`#7EC8BB`). Mark them with `class="external-link"`; the color only applies inside `.site-page`, so post bodies never turn teal. Mocha maps `--external-link` to `--link`.

### Homepage writing

`index.html` owns the manually curated Writing section:

- one featured post;
- three recent-post links;
- a link to the full blog index.

When publishing a newer post, update that section deliberately: promote the newest post to the feature, shift the prior feature into the short list, and keep exactly three recent entries. The related styles are `.featured-writing`, `.writing-list`, and `.writing-list__link` in `assets/css/style.css`. Series labels, dates, and read times use `--text-muted`; the featured title and "All posts" stay orange.

Homepage headings are `h2` for sections (Work Experience, Writing, Reading, Projects) and `h3` for the featured post and project titles, keeping their existing size classes.

### Homepage experience and reading

`index.html` also owns the concise Work Experience and Reading sections.

- Keep the current Lyzr-AI entry first and concise; role details belong only where explicitly requested.
- Keep prior roles as compact supporting context.
- The Reading section is a manually curated list of external articles and papers. Keep the “Interesting reads I found recently.” subtitle, use concise descriptions, open external sources in a new tab, and retain `rel="noopener noreferrer"` on every `target="_blank"` link.
- Every `target="_blank"` link keeps its visible `↗` inside `<span aria-hidden="true">` and adds `<span class="sr-only"> (opens in a new tab)</span>`.

### Blog index cards

`blogs/index.html` marks featured cards with `post-card` and a color variant:

- `post-card--primary`
- `post-card--secondary`
- `post-card--cyan`
- `post-card--gold`

Use a variant that matches the post’s existing accent; do not flatten every card to the same hover color. Card interaction is intentionally limited to border/surface/shadow refinement—no scale, glow, or large movement.

`blogs/index.html` uses a Writing `h1` intro, a Featured writing `h2` with an "All posts ↓" shortcut to `#all-posts`, and a neutral All Posts archive whose `h2` sits inside the native `<summary>`. Card and archive titles are `h3`; card descriptions use `leading-[1.65]`. Keep the archive free of accent side rails; use neutral dividers and a subtle full-row cyan tint on hover/focus instead. External archived posts must include `rel="noopener noreferrer"` with `target="_blank"`, the `external-link` class, and a visible `↗`.

### Projects

`projects/index.html` groups work into Featured, Built, and Contributions; the page title is the `h1`, each group label is an `h2`, and each project title link sits in an `h3.project-card__name`.

- Project cards share one accent: `--primary` on hover/focus, `--gold` for `project-card--featured`. Built/Contribution tags (`.project-tag`) are muted text. Do not reintroduce per-card color variants.
- Keep project cards content-led: neutral borders at rest, then a subtle full-card accent border/tint/shadow on hover or focus. Never add permanent side rails, scale, glow, or large movement.
- External project links must open in a new tab with `rel="noopener noreferrer"` and carry `project-card__title external-link`.

### Posts

`_layouts/post.html` provides two reading aids automatically:

1. A two-pixel theme-primary reading-progress track along the bottom edge of the floating `On this page` trigger. It updates during scrolling and appears with the control.
2. A contextual `On this page` control (a `<nav aria-label="On this page">`) for posts with at least two `h2[id]` or `h3[id]` headings. It stays hidden until the authored Table of Contents has passed above the viewport, lists headings in document order, indents `h3` entries, and marks the active section. Under 640px it is at most 16rem wide, anchored to the right, and its menu links are at least 40px tall.

The post control closes on item selection, outside click, and `Escape`; `Escape` restores trigger focus. New post headings need stable `id` values to appear in it. Keep the authored top Table of Contents for readers at the beginning of a post; the contextual control extends, rather than replaces, it.

Article typography and these controls are styled in `assets/css/style.css`; article rules are scoped to `.post-article`, not bare `article`, so project cards are unaffected. Preserve the quiet reading rhythm: modestly relaxed paragraphs, balanced headings, warm charcoal code surfaces, and no decorative page-wide effects beyond the frame. Group a diagram with its caption in `<figure>`/`<figcaption>`, describe artwork images in their `alt` (use `alt=""` only when purely decorative), and mark the TOC `>` chevron `aria-hidden="true"`.

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
