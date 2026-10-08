# Portfolio Color Scheme Reference

Two themes controlled by `data-theme` attribute on `<html>`. All colors use CSS variables — never hardcode hex values in HTML.

---

## Semantic Variables (both themes)

| Variable | Mocha | Orange | Purpose |
|----------|-------|--------|---------|
| `--bg` | `#1e1e2e` | `#0a0a0a` | Page background |
| `--text` | `#cdd6f4` | `#eeeeee` | Primary text |
| `--text-muted` | `#a6adc8` | `#808080` | Secondary/muted text |
| `--primary` | `#cba6f7` | `#EC5B2B` | Headings, current nav link |
| `--secondary` | `#fab387` | `#EE7948` | Hover states |
| `--accent` | `#f9e2af` | `#FFF7F1` | Badges, social links |
| `--link` | `#89b4fa` | `#F28A5B` (orange-mid) | Link color |
| `--link-hover` | `#74c7ec` | `#F2B48C` (orange-light) | Link hover |
| `--external-link` | `var(--link)` | `#7EC8BB` (muted teal) | Off-site links on non-post pages (`.site-page a.external-link`) |
| `--border` | `#313244` | `#1e1e1e` | Borders, separators |
| `--bold` | `#74c7ec` | `#EC5B2B` (orange-deep) | Bold text in articles |
| `--italic` | `#a6e3a1` | `#F2B48C` (orange-light) | Italic text, paren-notes |
| `--surface` | `#181825` | `#060606` | Card/elevated backgrounds |

## Extended Palette

| Variable | Mocha | Orange | Purpose |
|----------|-------|--------|---------|
| `--cyan` | `#94e2d5` | `#F28A5B` (orange-mid) | Series/tag labels |
| `--red` | `#f38ba8` | `#e06c75` | Error/red accents |
| `--gold` | `#f9e2af` | `#F2B48C` (orange-light) | Dates, warm accent |
| `--cream` | `#f5e0dc` | `#fff7f1` | Cream accent |
| `--peach` | `#fab387` | `#ee7948` | Properties fallback |
| `--muted-code` | `#6c7086` | `#8F8379` | Code comments (5.1:1 on the code surface) |

## Code Variables

| Variable | Mocha | Orange | Purpose |
|----------|-------|--------|---------|
| `--code-inline-text` | `#89b4fa` | `#F7CDB0` (orange-pale) | Inline code text |
| `--code-inline-bg` | `rgba(137,180,250,0.1)` | `rgba(236,91,43,0.08)` | Inline code background |
| `--code-inline-border` | `rgba(137,180,250,0.2)` | `rgba(236,91,43,0.22)` | Inline code border |
| `--code-block-bg` | `#181825` | `#14110f` | Code block background (warm charcoal) |
| `--code-block-border` | `#313244` | `#2a201a` | Code block border |
| `--code-keyword` | `#cba6f7` | `#EC5B2B` (orange-deep) | Keywords |
| `--code-property` | `#fab387` | `#e6dcd3` | Properties/tags |
| `--code-string` | `#a6e3a1` | `#F2B48C` (orange-light) | Strings |
| `--code-function` | `#89b4fa` | `#F28A5B` (orange-mid) | Functions/classes |
| `--code-number` | `#f9e2af` | `#e6dcd3` | Numbers/regex/variables |
| `--code-punctuation` | `#cdd6f4` | `#8f8379` | Punctuation and operators |

The orange theme uses one hue in four steps, defined once as `--orange-deep`, `--orange-mid`, `--orange-light`, `--orange-pale`: deep for emphasis and keywords, mid for links, tags, and functions, light for notes, dates, and strings, pale for inline code. Everything else is neutral grey or warm off-white. Do not add blue, cyan, green, or yellow to the orange theme. The mocha theme keeps its Catppuccin palette.

The single exception is `--external-link` (`#7EC8BB`, 10.2:1 on `#0a0a0a`), whose only job is marking links that leave the site: employers, project repositories, external reading, Medium archive posts, the notes repository, and social/contact links. Add `class="external-link"` to the anchor; `.site-page a.external-link` (and any `h2`–`h4` inside it) turns teal, with the same teal plus underline on hover/focus. `.site-page` is the `<main>` of `_layouts/default.html`, so post bodies never receive teal. Never use it for unlinked names, labels, dates, badges, headings, nav, frame, card borders, inline code, or syntax highlighting.

Roles that stay neutral: the inactive primary nav links, homepage series labels, dates and read times, the research note, and project Built/Contribution tags use `--text-muted`. The current nav link uses `--primary`.

---

## Usage Rules

- Always use `text-[var(--variable)]` or `bg-[var(--variable)]` in Tailwind classes
- Never use `--ctp-*` variables in HTML — those are internal to the CSS
- Card/elevated surfaces: `bg-[var(--surface)]`
- See [ORANGE_THEME.md](./ORANGE_THEME.md) for raw orange palette definitions

## Component Patterns

### Social Links (non-post pages)
```html
<a href="..." class="external-link">Twitter</a>
```

### External Links (non-post pages, new tab)
```html
<a href="..." target="_blank" rel="noopener noreferrer" class="external-link">Title <span aria-hidden="true">↗</span><span class="sr-only"> (opens in a new tab)</span></a>
```

### Headings
```html
<h2 class="text-2xl font-bold text-[var(--primary)] mb-4">Section Title</h2>
```

### Card / Elevated Surface
```html
<div class="p-4 rounded-xl border border-[var(--border)] bg-[var(--surface)]">...</div>
```

### Image Placeholder
```html
<img src="{{ '/blogs/post-slug/image.png' | relative_url }}" alt="[description]" class="w-full rounded-xl mb-6 border border-[var(--border)]" />
```

### Blockquote
```html
<blockquote class="border-l-2 border-[var(--primary)] pl-4 text-[var(--text-muted)] italic">
  Quote text here
</blockquote>
```

### Quick Tailwind Reference
```
text-[var(--text)]          text-[var(--text-muted)]
text-[var(--primary)]       text-[var(--secondary)]
text-[var(--link)]          text-[var(--link-hover)]
text-[var(--accent)]        text-[var(--bold)]
bg-[var(--bg)]              bg-[var(--surface)]
border-[var(--border)]
```
