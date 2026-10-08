# Agent Guide - parthshr370.github.io

## Overview
Personal portfolio and blog site built with Jekyll 4.4, Tailwind CSS (browser CDN v4), and custom theme support. Focuses on AI/agents, Golang, and personal projects with two themed color schemes.

## Repo Skill

Repo-local skill for site-building final markdown blogs:
- `skills/blog-site-build/SKILL.md`

Use this when the writing is already done and the task is to mould that final markdown into a website post while preserving emphasis, code treatment, diagrams, and the site's visual language.

## Development Commands

### Local Development
```bash
# Initial setup (one-time)
gem install bundler
bundle config set --local path 'vendor/bundle'
bundle install

# Run local server (auto-reloads on file changes)
bundle exec jekyll serve
# Site available at http://127.0.0.1:4000/

# Build for production
bundle exec jekyll build
# Output in _site/ directory
```

### No Testing Framework
This is a static site with no automated tests. Verify changes by:
1. Running `bundle exec jekyll serve` locally
2. Checking all pages (Home, Blogs, Projects, individual blog posts)
3. Testing theme toggle works correctly
4. Verifying responsive behavior (mobile/desktop)

## File Structure

```
/                          # Root
├── _config.yml            # Jekyll configuration (site title, baseurl, defaults)
├── index.html             # Homepage with intro, projects, socials
├── blogs/
│   ├── index.html         # Blog listing page (featured + all posts + notes section)
│   ├── how-i-built-tool-calling-engine-for-my-agent-sdk/  # Agent SDK Blog 2
│   ├── how-i-built-my-own-langchain-from-scratch-in-go/   # Agent SDK Blog 1
│   ├── anatomy-of-subagents/index.html
│   ├── json-marshals-and-go/index.html
│   └── pairing-agents-with-mcp/index.html
├── projects/
│   └── index.html         # Projects page (open source + personal projects)
├── _layouts/
│   ├── default.html       # Base layout (skip link, nav, <main id="main-content" class="site-page">)
│   └── post.html          # Blog post layout (skip link, nav, <main> > article.post-article + socials, On this page nav)
├── _includes/
│   ├── head.html          # Meta tags, Tailwind CDN, theme JS, Prism.js loading
│   ├── frame.html         # Fixed decorative viewport border with corner ticks
│   ├── nav.html           # Primary nav (aria-label="Primary"): home h1 or brand line + Home/Blogs/Projects links
│   ├── theme-toggle.html  # Theme switcher button (type="button", destination-theme aria-label, aria-hidden icons)
│   └── socials.html       # Footer social links for blog posts
└── assets/
    ├── css/style.css      # Theme variables + custom CSS + Prism colors
    ├── fonts/             # ZedMono Nerd Font (Regular + Bold)
    └── img/               # favicon, banner, blog images
```

## Adding New Content

### New Blog Post
1. Create folder: `blogs/my-slug/index.html`
2. Use front matter:
```yaml
---
layout: post
title: "Your Post Title"
date_display: "March 6, 2026"
read_time: "5 min read"
permalink: /blogs/my-slug/
prism:
  - python
  - go
---
```
3. Add HTML content (use `<p>`, `<h2>`, `<pre><code>`, `<img>`, etc.)
4. Add link in `blogs/index.html` in both "Featured Posts" and "All Posts" sections
5. Place images in `blogs/my-slug/` folder and reference with `{{ '/blogs/my-slug/image.png' | relative_url }}`
6. Use Tailwind classes for styling, color variables for theming

### New Project
Add entries in both `index.html` (Projects section) and `projects/index.html`:
- Homepage: `<a href="..." target="_blank" rel="noopener noreferrer" class="external-link group block"><h3 ...>Title <span aria-hidden="true">↗</span><span class="sr-only"> (opens in a new tab)</span></h3></a>` followed by one short, outcome-led `<p>` description; keep feature inventories in the repository README
- Projects page: `<h3 class="project-card__name"><a ... class="project-card__title external-link">` inside `.project-card__heading`, plus a plain `<span class="project-tag">Built|Contribution</span>`; no per-card color variants
- External links: `target="_blank"`, `rel="noopener noreferrer"`, visible `↗` in `aria-hidden` span, and an `sr-only` "(opens in a new tab)" cue
- Featured projects on homepage get `⭐ Featured` badge

## Code Style Guidelines

### HTML/Tailwind Classes
- Always use CSS variables for colors: `text-[var(--text)]`, `bg-[var(--bg)]`, `border-[var(--border)]`
- Core variables: `--bg`, `--text`, `--text-muted`, `--primary`, `--secondary`, `--accent`, `--link`, `--link-hover`, `--border`, `--bold`, `--italic`, `--surface`
- Extended palette: `--cyan`, `--red`, `--gold`, `--cream`, `--peach`, `--muted-code`
- Code variables: `--code-inline-text`, `--code-inline-bg`, `--code-inline-border`, `--code-block-bg`, `--code-block-border`, `--code-keyword`, `--code-property`, `--code-string`, `--code-function`, `--code-number`, `--code-punctuation`
- Never use `--ctp-*` variables in HTML — those are internal CSS definitions only
- Full reference: see COLORSCHEME.md
- Spacing: Use Tailwind scale (`mt-8` `mb-6` `p-4`)
- Borders: `border border-[var(--border)]`
- Links: `text-[var(--link)] hover:text-[var(--link-hover)]`
- Off-site links on non-post pages: add `class="external-link"` (muted teal `--external-link` in orange, scoped to `.site-page`). Never use it inside post bodies.
- Bold text in `.post-article`: Use CSS variable `--bold` (automatically colored per theme)
- Italic text in `.post-article`: Use CSS variable `--italic`
- Parenthetical side-notes can use `<span class="paren-note">(...)</span>` when they carry meaningful context
- Raw technical names in prose should usually be inline code when they are important types, functions, fields, or literals

### Jekyll/Liquid
- Always use `{{ '/path/' | relative_url }}` for internal links (not absolute paths)
- Front matter is YAML, ensure proper indentation (2 spaces)
- Use `site.title`, `page.title`, `page.nav_active`, `page.date_display`, `page.read_time`

### Code Blocks
- Wrap in `<pre><code class="language-python">` (add appropriate language class)
- Prism.js automatically highlights based on `language-` class
- Languages defined in front matter `prism:` array load corresponding scripts
- Supported: `python`, `go`, `json`, `javascript`, `bash`, `yaml`

### Images
- Place in same directory as HTML file (e.g., `blogs/my-post/image.png`)
- Reference: `<img src="{{ '/blogs/my-post/image.png' | relative_url }}">`
- Add `alt` attribute for accessibility
- Style: `w-full rounded-xl mb-6 border border-[var(--border)]`
- Banner images go in the post folder, referenced at the top of the article
- Diagrams (Excalidraw exports) go in the same post folder
- Placeholder when image is not ready yet:
  ```html
  <!-- TODO: add image — [description of what goes here] -->
  <div class="w-full h-48 rounded-xl mb-6 border border-[var(--border)] bg-[var(--surface)] flex items-center justify-center">
    <span class="text-[var(--text-muted)] text-sm">[placeholder: description]</span>
  </div>
  ```

### Naming Conventions
- Folders: kebab-case (`json-marshals-and-go`, `anatomy-of-subagents`)
- Files: kebab-case (`index.html`, `style.css`)
- Page slugs: kebab-case in `permalink` front matter
- Social links: lowercase (`parthshr370`, `parthshar370@gmail.com`)

### Navigation Active States
Set in front matter:
```yaml
nav_active:                    # home|blogs|projects, or omit
```
`nav_active` adds `aria-current="page"` to the matching link, which renders `--primary` with an underline; other nav links are `--text-muted`. `nav_active: home` also renders the site name as the page `h1`; every other page shows a plain brand line and must supply its own `h1` in content.

## Theme System

Two themes controlled by `data-theme` attribute on `<html>`:
- `mocha` (default): Catppuccin Mocha colors
- `orange`: High-contrast orange theme (set as default localStorage value)

Theme toggle logic in `head.html`:
1. Reads localStorage `theme` key (default: 'orange')
2. Sets `data-theme` attribute on `<html>` element
3. Toggles between 'mocha' and 'orange' via button click
4. CSS variables automatically update based on `[data-theme]` selector

Theme colors defined in `assets/css/style.css`:
- `:root` defines all semantic variables with mocha values
- `[data-theme="orange"]` overrides the same variables with orange values
- Both themes define the full variable set (core, extended palette, code highlighting)
- Prism.js syntax highlighting uses `--code-*` variables in both themes
- No `--ctp-*` variables should ever appear in HTML — internal CSS only

Visual intent:
- keep the current website theme intact
- inline code should not look dull
- comments in code should recede from real code
- syntax lanes should separate comments / strings / functions / keywords clearly
- code blocks should feel like a warm charcoal surface, not dead black; the orange theme uses only orange shades plus neutrals

## Important Patterns

### Blog Pages
- Use `layout: post` for individual blog pages
- Include `permalink: /blogs/slug/` (trailing slash required)
- Add table of contents with `<details>` wrapper
- Use `<hr class="border-[var(--border)] my-8">` for section breaks
- End with socials via `{% include socials.html %}`

### Content Pages (Home, Blogs, Projects)
- Use `layout: default` for main pages; it wraps content in `<main id="main-content" class="site-page">`
- Content wrapped in `<section class="mt-8">` or similar
- Heading order: one `h1` per page (homepage name in nav, otherwise the page title in content), `h2` for sections, `h3` for card/item titles; keep existing size classes when changing levels
- Metadata (series labels, dates, read times, tags) uses `--text-muted`
- Use consistent spacing: `space-y-4`, `space-y-6`, `space-y-8`

### Lists
- Ordered: `<ol class="list-decimal pl-6 mb-6 space-y-2">`
- Unordered: `<ul class="list-disc pl-6 mb-6 space-y-2">`
- Clean lists: `<ul class="list-none space-y-4">`

### Externally Hosted Content
Some blogs link to Medium (https://medium.com/@parthshr370/...). These are listed in `blogs/index.html` "All Posts" collapsible section with `target="_blank"`, `rel="noopener noreferrer"`, `class="external-link"`, and a visible `↗`. The "All posts ↓" link beside Featured writing jumps to `#all-posts`.

## Build Exclusions
From `_config.yml` exclude: `Gemfile`, `Gemfile.lock`, `README.md`, `COLORSCHEME.md`, `ORANGE_THEME.md`, `excalidraw.log`, `node_modules`, `vendor` (not deployed to GitHub Pages)

## Responsive Design
- Column: `w-[90%] max-w-[42rem]` on `<body>` in both layouts (~670px max)
- Viewport frame inset: `--frame-inset` (20px desktop, 8px under 640px)
- Use Tailwind responsive prefixes: `md:`, `lg:` for breakpoints
- Navigation uses `flex-wrap` for small screens

## Accessibility
- Add `alt` attributes to all images; describe artwork, use `alt=""` only for purely decorative images
- Use semantic HTML (`<main>`, `<article>`, `<section>`, `<nav>`, `<figure>`/`<figcaption>`, `<h1>`-`<h3>`)
- Both layouts start with a `.skip-link` to `#main-content`; nav is `aria-label="Primary"`, the post section control is `<nav aria-label="On this page">`
- Decorative glyphs (`↗`, TOC `>` chevrons, icons) get `aria-hidden="true"`
- Nav links, theme button, and mobile "On this page" menu links have a 40px minimum height
- Links have hover states and underlines
- Color contrast meets WCAG standards in both themes
