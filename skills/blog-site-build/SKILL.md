# Skill: blog-site-build

Turn Parth's final markdown blog into a polished post for `parthshr370.github.io`.

This skill is not for writing the blog. The writing is already done.

The job here is to:
- preserve the article's wording and rhythm
- preserve emphasis already present in markdown
- convert the article into the site's HTML format
- place images/diagrams well
- keep the site theme intact while using the available palette with taste
- update blog index / series labels / references if needed

## Non-goals

Do not:
- rewrite the article in a new voice
- flatten bold/italics into plain text
- replace the site theme with a different theme system
- over-polish the article into generic blog prose

## Primary workflow

1. Read the final markdown draft.
2. Preserve all meaningful bold / italic emphasis.
3. Convert the markdown into site HTML using the repo's post conventions.
4. Copy banner and post-local diagrams into the post folder.
5. Add TOC, section anchors, code blocks, diagrams, and footer references.
6. Update `blogs/index.html` if the post should appear there.
7. Run local Jekyll validation if possible.

## Core rule

Treat the markdown draft as source of truth.

Do not silently change:
- sentence wording
- pacing
- emphasis rhythm
- code comments inside examples

Only adapt when HTML/site rendering requires it.

## Site structure

- Each post lives in `blogs/<slug>/index.html`
- Images for a post live in the same folder as the post
- Use `layout: post`
- Use `{{ '/path/' | relative_url }}` for internal links and images

## Frontmatter template

```yaml
---
layout: post
title: "Post Title"
date_display: "Month Day, Year"
read_time: "8 min read"
permalink: /blogs/post-slug/
prism:
  - go
  - json
---
```

## HTML conversion rules

- Headings:
  - `<h2 id="slug" class="text-2xl font-bold mt-12 mb-6 text-[var(--primary)]">`
- Paragraphs:
  - `<p class="mb-6 leading-relaxed">`
- Unordered lists:
  - `<ul class="list-disc pl-6 mb-6 space-y-2">`
- Ordered lists:
  - `<ol class="list-decimal pl-6 mb-6 space-y-2">`
- Images:
  - `<img src="{{ '/blogs/slug/image.png' | relative_url }}" alt="..." class="w-full rounded-xl mb-6 border border-[var(--border)]" />`
- Code blocks:
  - `<pre><code class="language-go">...</code></pre>`
- Horizontal rule:
  - `<hr class="border-[var(--border)] my-8" />`

## Table of contents

- Add a TOC near the top of the post
- Use a `<details>` wrapper
- Link to major `h2` sections only unless the article clearly needs more

## Emphasis preservation rules

This is the most important part.

- Preserve existing `**bold**` and `*italics*` from markdown unless it becomes invalid HTML
- If the markdown uses emphasis rhythm to guide the eye, keep it
- Do not remove emphasis just to make the page look "cleaner"
- If a paragraph feels flat after conversion, restore the original emphasis from markdown before inventing new emphasis

### Inline code conversion

Convert raw technical mentions into `<code>` when they are clearly one of:
- Go types
- function names
- struct names
- fields
- methods
- literals / slices / JSON-ish snippets

Examples:
- `ToolDefinition`
- `RegisterTool`
- `GenerateSchema`
- `GetAllTools`
- `Execute`
- `ChatRequest.Tools`
- `tool_call_id`
- `[]llm.Tool`

Do not overdo this for ordinary prose words.

### Parenthesis treatment

When parentheses carry meaningful side-context, keep them visually distinct.

Use:

```html
<span class="paren-note">(...)</span>
```

This is especially useful for:
- clarifying asides
- structural groupings
- subtle technical context

Examples:
- `(ToolDefinition)`
- `(JSON)`
- `(validate, extract type, generate schema)`
- `(a single JSON object with its properties)`

## Code block rules

- Preserve comments inside code blocks if they help comprehension
- Do not strip inline comments added for explanation
- If comments are part of the teaching rhythm, keep them
- Choose the correct Prism language in the code block class

### Syntax / color intent

Use the site's current theme, but preserve this visual separation:
- comments: muted grey
- keywords: orange
- properties/identifiers: blue
- functions/classes: teal
- strings: green or warm readable accent depending on context
- numbers/secondary literals: gold
- code background: dark slate, not dead black

Inline code should not look dull. It should feel distinct from body text.

## Current palette reference (orange theme)

These are the palette anchors. Use CSS variables, not raw hex in HTML.

| Name | Hex | CSS Variable |
|------|-----|-------------|
| orange | `#EC5B2B` | `--primary` |
| peach | `#EE7948` | `--secondary` |
| gold | `#E5C07B` | `--gold` |
| teal | `#56B6C2` | `--cyan` |
| blue | `#6BA1E6` | `--link` |
| green | `#78D278` | `--code-string` |
| cream | `#FFF7F1` | `--accent` |
| muted grey | `#6C6C6C` | `--muted-code` |
| dark bg | `#0A0A0A` | `--bg` |
| surface | `#060606` | `--surface` |
| code block bg | `#161B22` | `--code-block-bg` |

Use these as reference, not as a license to repaint the site.
Full variable table: see COLORSCHEME.md.

## Theme / visual rules

- Keep the existing website theme system intact
- Do not replace the theme with Obsidian or terminal styling
- Borrow only useful visual ideas:
  - inline code should pop
  - syntax lanes should be clearly separated
  - comments should recede
  - diagrams should help readability

## Diagram rules

- Only include diagrams that reduce load
- Skip diagrams that are visually weak, cramped, or redundant
- Place diagrams close to the section they explain
- Typical good placements:
  - overview diagram near intro
  - execution diagram near execution section
- If a diagram is unfinished, leave it out rather than force it in

## Image placeholders

When an image or diagram is not ready yet, use this placeholder pattern instead of leaving a broken reference:

```html
<!-- TODO: add image — [what goes here] -->
<div class="w-full h-48 rounded-xl mb-6 border border-[var(--border)] bg-[var(--surface)] flex items-center justify-center">
  <span class="text-[var(--text-muted)] text-sm">[placeholder: description]</span>
</div>
```

Replace with the real image when available:
```html
<img src="{{ '/blogs/slug/image.png' | relative_url }}" alt="[description]" class="w-full rounded-xl mb-6 border border-[var(--border)]" />
```

Banner images and Excalidraw diagram exports live in the post folder alongside `index.html`.

## Footer / references

End posts with references that actually connect to the article.

Good footer references include:
- repo link
- previous blog in a series
- related internal blogs
- official docs for the key Go packages used

Examples for tool-calling posts:
- SDK repo
- Agent SDK Blog 1
- `JSON, Marshals and Go`
- `reflect` docs
- `encoding/json` docs

## Blog index rules

When adding a new post to `blogs/index.html`:
- update featured/latest post if appropriate
- add the post to the all-posts list
- preserve title tint behavior
- series labels are allowed when meaningful

For series labels, use small uppercase text with a subtle accent tone.
Example:
- `Agent SDK Blog 1`
- `Agent SDK Blog 2`

## Verification checklist

Before considering the conversion done, check:

1. Title, slug, permalink, and frontmatter are correct
2. Bold / italics from markdown survived conversion
3. Raw technical names that should be code are code
4. Parenthetical side-notes are visually distinct where useful
5. Inline code is readable and not dull
6. Syntax highlighting has separation between comments / strings / functions / keywords
7. Diagrams are placed well and not bloating the post
8. Footer references are relevant
9. `blogs/index.html` is updated if needed
10. `bundle exec jekyll build` or `serve` works if local tooling is available

## Notes from the tool-calling post build

These came up during a real post conversion and should be remembered:

- Do not flatten emphasis from the markdown draft
- `ToolDefinition`-style names should be inline code in prose
- Parenthetical technical context looks better when tinted
- Inline code pills should not be flat grey on dark background
- Code comments must not share the same emphasis lane as real code
- The site should stay the site, but code styling can borrow good contrast ideas from Obsidian
- When in doubt, preserve the article's teaching rhythm over generic prettification
