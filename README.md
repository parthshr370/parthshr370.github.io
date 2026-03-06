# parthshr370.github.io

Personal site. Built with Jekyll, Tailwind CSS (browser CDN), and a custom Catppuccin Mocha / Orange theme.

## Run locally

```
gem install bundler
bundle config set --local path 'vendor/bundle'
bundle install
bundle exec jekyll serve
```

Open `http://127.0.0.1:4000/`

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

<p>Your content here. Use whatever HTML + Tailwind classes you want.</p>
```

The `prism` field is optional -- add language names to load syntax highlighting for code blocks.

Then add a link to it in `blogs/index.html`.
