# Portfolio Color Scheme Reference

This portfolio supports multiple themes. The default is **Catppuccin Mocha**, and an alternative **Orange Theme** is available via the theme toggle.

---

## Catppuccin Mocha (Default)

Based on **Catppuccin Mocha** palette. 

| Element | Color | Hex | CSS Variable |
|---------|-------|-----|--------------|
| Background | Base | `#1e1e2e` | `var(--bg)` |
| Text | Text | `#cdd6f4` | `var(--text)` |
| Muted Text | Subtext0 | `#a6adc8` | `var(--text-muted)` |
| Primary | Mauve | `#cba6f7` | `var(--primary)` |
| Secondary | Peach | `#fab387` | `var(--secondary)` |
| Accent | Yellow | `#f9e2af` | `var(--accent)` |
| Links | Blue | `#89b4fa` | `var(--link)` |
| Border | Surface0 | `#313244` | `var(--border)` |

---

## Orange Theme

A high-contrast theme with orange accents. See [ORANGE_THEME.md](./ORANGE_THEME.md) for full details.

| Element | Hex | CSS Variable |
|---------|-----|--------------|
| Background | `#1a0f0c` | `var(--bg)` |
| Text | `#eeeeee` | `var(--text)` |
| Muted Text | `#808080` | `var(--text-muted)` |
| Primary | `#EC5B2B` | `var(--primary)` |
| Secondary | `#EE7948` | `var(--secondary)` |
| Accent | `#FFF7F1` | `var(--accent)` |
| Links | `#EC5B2B` | `var(--link)` |
| Border | `#EC5B2B` | `var(--border)` |

---

## Usage in Code

The site uses CSS variables defined in `assets/css/style.css`. Themes are toggled by setting the `data-theme` attribute on the `<html>` element.

- `mocha` (Default)
- `orange`


---

## Component Examples

### Social Links
```html
<div class="flex gap-4 text-base">
  <a href="..." class="text-[#a6e3a1] hover:text-[#94e2d5] font-medium">Twitter</a>
  <span class="text-[#585b70]">/</span>
  <a href="..." class="text-[#a6e3a1] hover:text-[#94e2d5] font-medium">Github</a>
</div>
```

### Section Header
```html
<h2 class="text-2xl font-bold text-[#cba6f7] mb-4">Section Title</h2>
```

### Project Item
```html
<span class="text-[#fab387] font-bold">Project Name</span>
<span class="text-[#bac2de]">Description text</span>
```

### Code Block
```html
<pre class="bg-[#181825] p-4 rounded-lg border border-[#313244]">
  <code class="text-[#cdd6f4]">...</code>
</pre>
```

### Inline Code
```html
<code class="bg-[#313244] px-1.5 py-0.5 rounded text-[#f5c2e7]">code</code>
```

### Tags/Labels
```html
<span class="text-sm text-[#6c7086]">Category / Tag</span>
```

### Blockquote
```html
<blockquote class="border-l-2 border-[#cba6f7] pl-4 text-[#a6adc8] italic">
  Quote text here
</blockquote>
```

---

## Quick Reference (Tailwind Classes)

```
Primary Text:     text-[#cdd6f4]
Muted Text:       text-[#a6adc8]
Faint Text:       text-[#6c7086]
Links:            text-[#89b4fa] hover:text-[#74c7ec]
Social Links:     text-[#f9e2af] hover:text-[#fab387]
Headings:         text-[#cba6f7]
Project Names:    text-[#fab387]
Highlights:       text-[#f9e2af]
Borders:          border-[#313244]
Separators:       text-[#585b70]
Code BG:          bg-[#181825]

Bold (strong):    text-[#74c7ec] (Sapphire)
Italic (em):      text-[#a6e3a1] (Green)
Strikethrough:    text-[#eba0ac] (Maroon)
```
