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
| `_tabs/` | Sidebar navigation pages (About, Categories, Tags, Archives, Daily Tasks Log) |
| `_data/` | YAML for authors, contact links, share buttons |
| `_plugins/posts-lastmod-hook.rb` | Jekyll hook that auto-sets `last_modified_at` on posts from `git log` |
| `Daily_Tasks.md` | Password-protected custom page that parses and renders `daily_tasks_log.md` as a dashboard |
| `daily_tasks_log.md` | Markdown data source consumed by the Daily Tasks page |
| `assets/img/` | Images referenced in posts and config |

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
- Images must include dimensions: `![alt](/path/img.png){: w="700" h="400" }`
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
