# Agent Guide - parthshr370.github.io

## Overview
Personal portfolio and blog site built with Jekyll 4.4, Tailwind CSS (browser CDN v4), and custom theme support. Focuses on AI/agents, Golang, and personal projects with two themed color schemes.

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
│   ├── json-marshals-and-go/index.html  # Local blog post
│   ├── anatomy-of-subagents/index.html  # Local blog post
│   └── pairing-agents-with-mcp/index.html  # Local blog post
├── projects/
│   └── index.html         # Projects page (open source + personal projects)
├── _layouts/
│   ├── default.html       # Base layout (nav + content container)
│   └── post.html          # Blog post layout (back button + article + socials)
├── _includes/
│   ├── head.html          # Meta tags, Tailwind CDN, theme JS, Prism.js loading
│   ├── nav.html           # Navigation bar (logo + Home/Blogs/Projects links)
│   ├── theme-toggle.html  # Theme switcher button (moon/sun icons)
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
- Use pattern: `<a href="...">title</a>` with `<p class="text-[var(--text-muted)]">description</p>`
- External links: include `↗` symbol in title and `target="_blank"`
- Featured projects on homepage get `⭐ Featured` badge

## Code Style Guidelines

### HTML/Tailwind Classes
- Always use CSS variables for colors: `text-[var(--text)]`, `bg-[var(--bg)]`, `border-[var(--border)]`
- Available variables: `--bg`, `--text`, `--text-muted`, `--primary`, `--secondary`, `--accent`, `--link`, `--link-hover` (see COLORSCHEME.md)
- Spacing: Use Tailwind scale (`mt-8` `mb-6` `p-4`)
- Borders: `border border-[var(--border)]`
- Links: `text-[var(--link)] hover:text-[var(--link-hover)]`
- Bold text in `<article>`: Use CSS variable `--bold` (automatically colored per theme)
- Italic text in `<article>`: Use CSS variable `--italic`

### Jekyll/Liquid
- Always use `{{ '/path/' | relative_url }}` for internal links (not absolute paths)
- Front matter is YAML, ensure proper indentation (2 spaces)
- Use `site.title`, `page.title`, `page.nav_title`, `page.nav_active`, `page.date_display`, `page.read_time`

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

### Naming Conventions
- Folders: kebab-case (`json-marshals-and-go`, `anatomy-of-subagents`)
- Files: kebab-case (`index.html`, `style.css`)
- Page slugs: kebab-case in `permalink` front matter
- Social links: lowercase (`parthshr370`, `parthshar370@gmail.com`)

### Navigation Active States
Set in front matter:
```yaml
nav_title: "Page Title"        # Shown in nav (default: site.title)
nav_active:                    # Highlights nav link (home|blogs|projects, or omit)
```

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
- `:root` defaults to mocha
- `[data-theme="orange"]` overrides variables
- Prism.js syntax highlighting uses theme variables

## Important Patterns

### Blog Pages
- Use `layout: post` for individual blog pages
- Include `permalink: /blogs/slug/` (trailing slash required)
- Add table of contents with `<details>` wrapper
- Use `<hr class="border-[var(--border)] my-8">` for section breaks
- End with socials via `{% include socials.html %}`

### Content Pages (Home, Blogs, Projects)
- Use `layout: default` for main pages
- Content wrapped in `<section class="mt-8">` or similar
- Use consistent spacing: `space-y-4`, `space-y-6`, `space-y-8`

### Lists
- Ordered: `<ol class="list-decimal pl-6 mb-6 space-y-2">`
- Unordered: `<ul class="list-disc pl-6 mb-6 space-y-2">`
- Clean lists: `<ul class="list-none space-y-4">`

### Externally Hosted Content
Some blogs link to Medium (https://medium.com/@parthshr370/...). These are listed in `blogs/index.html` "All Posts" collapsible section with `target="_blank"`.

## Build Exclusions
From `_config.yml` exclude: `Gemfile`, `Gemfile.lock`, `README.md`, `COLORSCHEME.md`, `ORANGE_THEME.md`, `excalidraw.log`, `node_modules`, `vendor` (not deployed to GitHub Pages)

## Responsive Design
- Mobile: `w-full max-w-[90%]` (90% width)
- Desktop: `md:w-[43%]` (43% width, ~660px)
- Use Tailwind responsive prefixes: `md:`, `lg:` for breakpoints
- Navigation uses `flex-wrap` for small screens

## Accessibility
- Add `alt` attributes to all images
- Use semantic HTML (`<article>`, `<section>`, `<nav>`, `<h1>`-`<h3>`)
- Links have hover states and underlines
- Color contrast meets WCAG standards in both themes