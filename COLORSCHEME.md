# Portfolio Color Scheme Reference

Two themes controlled by `data-theme` attribute on `<html>`. All colors use CSS variables — never hardcode hex values in HTML.

---

## Semantic Variables (both themes)

| Variable | Mocha | Orange | Purpose |
|----------|-------|--------|---------|
| `--bg` | `#1e1e2e` | `#0a0a0a` | Page background |
| `--text` | `#cdd6f4` | `#eeeeee` | Primary text |
| `--text-muted` | `#a6adc8` | `#808080` | Secondary/muted text |
| `--primary` | `#cba6f7` | `#EC5B2B` | Headings, nav links |
| `--secondary` | `#fab387` | `#EE7948` | Hover states |
| `--accent` | `#f9e2af` | `#FFF7F1` | Badges, social links |
| `--link` | `#89b4fa` | `#6ba1e6` | Link color |
| `--link-hover` | `#74c7ec` | `#82aaff` | Link hover |
| `--border` | `#313244` | `#1e1e1e` | Borders, separators |
| `--bold` | `#74c7ec` | `#EC5B2B` | Bold text in articles |
| `--italic` | `#a6e3a1` | `#e5c07b` | Italic text in articles |
| `--surface` | `#181825` | `#060606` | Card/elevated backgrounds |

## Extended Palette

| Variable | Mocha | Orange | Purpose |
|----------|-------|--------|---------|
| `--cyan` | `#94e2d5` | `#56b6c2` | Code functions |
| `--red` | `#f38ba8` | `#e06c75` | Error/red accents |
| `--gold` | `#f9e2af` | `#e5c07b` | Numbers, warm accent |
| `--cream` | `#f5e0dc` | `#fff7f1` | Operators, URLs |
| `--peach` | `#fab387` | `#ee7948` | Properties fallback |
| `--muted-code` | `#6c7086` | `#6c6c6c` | Code comments |

## Code Variables

| Variable | Mocha | Orange | Purpose |
|----------|-------|--------|---------|
| `--code-inline-text` | `#89b4fa` | `#8cbeff` | Inline code text |
| `--code-inline-bg` | `rgba(137,180,250,0.1)` | `rgba(107,161,230,0.12)` | Inline code background |
| `--code-inline-border` | `rgba(137,180,250,0.2)` | `rgba(107,161,230,0.22)` | Inline code border |
| `--code-block-bg` | `#181825` | `#161b22` | Code block background |
| `--code-block-border` | `#313244` | `#243041` | Code block border |
| `--code-keyword` | `#cba6f7` | `#ec5b2b` | Keywords |
| `--code-property` | `#fab387` | `#6ba1e6` | Properties/tags |
| `--code-string` | `#a6e3a1` | `#78d278` | Strings |
| `--code-function` | `#89b4fa` | `#56b6c2` | Functions/classes |
| `--code-number` | `#f9e2af` | `#e5c07b` | Numbers/regex |
| `--code-punctuation` | `#cdd6f4` | `#d8dee9` | Punctuation |

---

## Usage Rules

- Always use `text-[var(--variable)]` or `bg-[var(--variable)]` in Tailwind classes
- Never use `--ctp-*` variables in HTML — those are internal to the CSS
- Card/elevated surfaces: `bg-[var(--surface)]`
- See [ORANGE_THEME.md](./ORANGE_THEME.md) for raw orange palette definitions

## Component Patterns

### Social Links
```html
<a href="..." class="text-[var(--accent)] hover:text-[var(--secondary)]">Twitter</a>
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
