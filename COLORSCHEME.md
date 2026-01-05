# Portfolio Color Scheme Reference

Based on **Catppuccin Mocha** palette. Use this as a reference when creating new pages or components.

---

## Base Colors

| Element | Color | Hex | CSS Variable |
|---------|-------|-----|--------------|
| Background | Base | `#1e1e2e` | `var(--ctp-base)` |
| Background Alt | Mantle | `#181825` | `var(--ctp-mantle)` |
| Background Dark | Crust | `#11111b` | `var(--ctp-crust)` |

---

## Text Colors

| Element | Color | Hex | CSS Variable | Usage |
|---------|-------|-----|--------------|-------|
| Primary Text | Text | `#cdd6f4` | `var(--ctp-text)` | Body text, paragraphs |
| Secondary Text | Subtext1 | `#bac2de` | `var(--ctp-subtext1)` | Less important text |
| Muted Text | Subtext0 | `#a6adc8` | `var(--ctp-subtext0)` | Descriptions, metadata |
| Disabled/Faint | Overlay0 | `#6c7086` | `var(--ctp-overlay0)` | Timestamps, tags |

---

## Headings

| Element | Color | Hex | CSS Variable |
|---------|-------|-----|--------------|
| H1 (Page Title) | Mauve | `#cba6f7` | `var(--ctp-mauve)` |
| H2 (Section) | Mauve | `#cba6f7` | `var(--ctp-mauve)` |
| H3 (Subsection) | Lavender | `#b4befe` | `var(--ctp-lavender)` |
| H4+ | Text | `#cdd6f4` | `var(--ctp-text)` |

---

## Links & Interactive

| Element | Color | Hex | CSS Variable | Usage |
|---------|-------|-----|--------------|-------|
| Primary Links | Blue | `#89b4fa` | `var(--ctp-blue)` | Standard links |
| Link Hover | Sapphire | `#74c7ec` | `var(--ctp-sapphire)` | Hover state |
| Project Titles | Peach | `#fab387` | `var(--ctp-peach)` | Project names, highlights |
| Social Links | Green | `#a6e3a1` | `var(--ctp-green)` | Twitter, GitHub, etc. |
| CTA/Important | Yellow | `#f9e2af` | `var(--ctp-yellow)` | Call-to-action, names |

---

## Text Formatting (Bold/Italic)

Inspired by Obsidian Catppuccin theme - bold and italic get their own colors.

| Element | Color | Hex | CSS Variable | Usage |
|---------|-------|-----|--------------|-------|
| **Bold** | Sapphire | `#74c7ec` | `var(--ctp-sapphire)` | `<strong>`, `<b>` |
| *Italic* | Green | `#a6e3a1` | `var(--ctp-green)` | `<em>`, `<i>` |
| ***Bold+Italic*** | Teal | `#94e2d5` | `var(--ctp-teal)` | Combined formatting |
| ~~Strikethrough~~ | Maroon | `#eba0ac` | `var(--ctp-maroon)` | `<del>`, `<s>` |

---

## Accent Colors

| Element | Color | Hex | CSS Variable | Usage |
|---------|-------|-----|--------------|-------|
| Name Highlight | Yellow | `#f9e2af` | `var(--ctp-yellow)` | "I'm Parth" |
| Project Names | Peach | `#fab387` | `var(--ctp-peach)` | Project titles |
| Section Headers | Mauve | `#cba6f7` | `var(--ctp-mauve)` | "Open Source", "Projects" |
| Success/Positive | Green | `#a6e3a1` | `var(--ctp-green)` | Achievements |
| Warning | Yellow | `#f9e2af` | `var(--ctp-yellow)` | Notices |
| Error | Red | `#f38ba8` | `var(--ctp-red)` | Errors, warnings |

---

## Borders & Surfaces

| Element | Color | Hex | CSS Variable | Usage |
|---------|-------|-----|--------------|-------|
| Border Light | Surface0 | `#313244` | `var(--ctp-surface0)` | Dividers, hr |
| Border Medium | Surface1 | `#45475a` | `var(--ctp-surface1)` | Card borders |
| Border Dark | Surface2 | `#585b70` | `var(--ctp-surface2)` | Separators (slashes) |
| Code Block BG | Mantle | `#181825` | `var(--ctp-mantle)` | Code backgrounds |

---

## Code Blocks (Syntax Highlighting)

| Element | Color | Hex | CSS Variable |
|---------|-------|-----|--------------|
| Background | Mantle | `#181825` | `var(--ctp-mantle)` |
| Text | Text | `#cdd6f4` | `var(--ctp-text)` |
| Keywords | Mauve | `#cba6f7` | `var(--ctp-mauve)` |
| Strings | Green | `#a6e3a1` | `var(--ctp-green)` |
| Numbers | Peach | `#fab387` | `var(--ctp-peach)` |
| Functions | Blue | `#89b4fa` | `var(--ctp-blue)` |
| Comments | Overlay0 | `#6c7086` | `var(--ctp-overlay0)` |
| Variables | Text | `#cdd6f4` | `var(--ctp-text)` |
| Types/Classes | Yellow | `#f9e2af` | `var(--ctp-yellow)` |
| Operators | Sky | `#89dceb` | `var(--ctp-sky)` |

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
