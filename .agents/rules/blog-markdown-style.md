# Blog Markdown Style Guide for AI Agents

This guide defines the mandatory formatting and structural rules for all blog posts in this repository, based on the reference files `2019-08-08-text-and-typography.md` and `2019-08-08-write-a-new-post.md`.

## 1. File Naming & Path
- **Path:** `_posts/`
- **Format:** `YYYY-MM-DD-TITLE.md` (e.g., `2024-03-12-my-new-post.md`)
- **Extension:** `.md` or `.markdown`

## 2. Front Matter (Mandatory)
Every post must have the following YAML front matter:
```yaml
---
title: "Clear and Concise Title"
date: YYYY-MM-DD HH:MM:SS +/-TTTT  # e.g., 2024-03-12 10:00:00 +0530
categories: [PrimaryCategory, SecondaryCategory] # Max 2
tags: [tag1, tag2] # Always lowercase
description: "A short summary of the post for SEO and previews."
# Optional Features:
# image: /path/to/image.png
# pin: true
# math: true
# mermaid: true
---
```

## 3. Typography & Spacing
- **Headings:** Use `#` to `####`. Add `{: .mt-4 .mb-0 }` to headings for consistent spacing if needed, but primary headings should follow Chirpy defaults.
- **Lists:**
  - Ordered: `1. `, `2. `
  - Unordered: `- `
  - Task List: `- [ ] ` or `- [x] `
- **Blockquotes:** Use `>` for standard quotes.
- **Prompts:** Special Chirpy callouts:
  - `{: .prompt-tip }`
  - `{: .prompt-info }`
  - `{: .prompt-warning }`
  - `{: .prompt-danger }`

## 4. Media & Assets
- **Images:**
  - Must include width and height: `![alt text](/path/to/img){: w="700" h="400" }`
  - For captions: Add italicized text on the next line: `_Image caption_`
  - Alignment: `{: .normal }`, `{: .left }`, `{: .right }`
  - Shadow: `{: .shadow }`
- **Embeds (Liquid):**
  - YouTube: `{% include embed/youtube.html id='VIDEO_ID' %}`
  - Video File: `{% include embed/video.html src='/path/to/video.mp4' %}`

## 5. Code Blocks
- **Syntax:** Always specify the language (e.g., ` ```bash `).
- **Filenames:** Use `{: file="path/to/file" }` to add a filename header.
- **No Line Numbers:** Use `{: .nolineno }` for logs or short snippets.
- **Filepaths:** Use `` `/path/to/file`{: .filepath} `` for inline paths.

## 6. Math & Diagrams
- **Math:** Enable `math: true` in front matter. Use `$$` for blocks/inline.
- **Mermaid:** Enable `mermaid: true` in front matter. Use ` ```mermaid ` blocks.
