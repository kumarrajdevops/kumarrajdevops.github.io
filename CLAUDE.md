# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Local dev server (live reload)
bundle exec jekyll serve

# Production build
bundle exec jekyll b

# HTML link/tag validation (run after build)
bundle exec htmlproofer _site \
  --disable-external \
  --ignore-urls "/^http:\/\/127.0.0.1/,/^http:\/\/0.0.0.0/,/^http:\/\/localhost/"
```

CI runs build + htmlproofer on every push to `main` and deploys to GitHub Pages automatically.

## Architecture

This is a **Jekyll + Chirpy theme** personal blog. The theme gem provides layouts, includes, and Sass — only the files listed below live in this repo.

| Path | Purpose |
|---|---|
| `_config.yml` | Site-wide config: title, timezone (`Asia/Kolkata`), social links, Kramdown/Rouge settings |
| `_posts/` | Blog posts — Jekyll builds these into `/posts/:title/` URLs |
| `_tabs/` | Sidebar navigation pages; each can be a real page or a JS redirect to a `pages/` page |
| `_data/` | YAML for authors, contact links, share buttons |
| `_plugins/posts-lastmod-hook.rb` | Jekyll hook that auto-sets `last_modified_at` on posts from `git log` |
| `pages/daily-tasks/Daily_Tasks.md` | Password-protected dashboard; permalink `/Daily_Tasks/` |
| `pages/daily-tasks/daily_tasks_log.md` | Raw markdown data — must live in same folder as `Daily_Tasks.md` for `include_relative` to work |
| `pages/roster-calendar/roster_to_calendar.md` | Roster → Google Calendar sync tool; permalink `/roster-calendar/` |
| `assets/img/posts/` | Hero images and post images |
| `assets/img/` | Avatar, favicons, other site images |

### `pages/` folder convention

Custom interactive pages (inline HTML/CSS/JS) live under `pages/` rather than the repo root. Jekyll processes them automatically — no collection config needed. Sidebar tabs in `_tabs/` use a JS `window.location.replace()` redirect to point at the real `pages/` URL.

## Inline JavaScript Pages — CRITICAL

Pages like `Daily_Tasks.md` and `roster_to_calendar.md` embed all HTML, CSS, and JS inline in one `.md` file.

**`// single-line comments are forbidden in inline JS.`**

`compress_html` is enabled in production (GitHub Pages) and collapses every `<script>` block to a **single line**. A `//` comment then comments out the entire rest of the script — killing all event listeners and making the page non-interactive. This bug only shows in production, not in local `jekyll serve`.

**Always use `/* block comments */` instead of `//` in any inline script.**

## Writing Blog Posts

**Before creating or editing any post**, read `.agents/rules/blog-markdown-style.md`. Key rules:

- Filename: `_posts/YYYY-MM-DD-title-slug.md`
- Required front matter:
  ```yaml
  ---
  title: "Title"
  date: YYYY-MM-DD HH:MM:SS +0530
  categories: [Primary, Secondary]   # max 2
  tags: [lowercase, tags]
  description: "SEO summary"
  ---
  ```
- Hero image (shows at top of post and in post cards):
  ```yaml
  image:
    path: /assets/img/posts/filename.png
    alt: Description of image
  ```
- Images in post body must include dimensions: `![alt](/path/img.png){: w="700" h="400" }`
- Code blocks must specify language; add `{: file="path" }` for filename headers
- Chirpy callouts: `{: .prompt-tip }` / `{: .prompt-info }` / `{: .prompt-warning }` / `{: .prompt-danger }`
- Enable mermaid diagrams with `mermaid: true` in front matter
- Enable math with `math: true` in front matter

## Daily Tasks System

`Daily_Tasks.md` is a custom Liquid/JS page (not a standard Jekyll post). It:
- Requires a password to unlock (JS-based overlay)
- Reads and parses `daily_tasks_log.md` at page load
- Renders task tables with Done/In-Progress/Total counters
- Has print buttons for current-day and full-report views

When updating the daily tasks workflow, edits go to `Daily_Tasks.md` (UI logic) and `daily_tasks_log.md` (data).
