# CLAUDE.md — Averred Security Website

This file provides context and conventions for AI assistants (Claude and others) working in this repository.

## Project Overview

**averred.github.io** is the source for the [Averred Security](https://www.averred.net) website, hosted on GitHub Pages. Currently it serves an "under construction" landing page. The site is intentionally minimal with zero build dependencies.

- **Live URL:** https://www.averred.net (custom domain via CNAME)
- **Hosting:** GitHub Pages (served directly from the `main` branch)
- **License:** CC0 1.0 Universal (public domain)

## Repository Structure

```
averred.github.io/
├── index.html              # Single-page site (all HTML + CSS inline)
├── averred-sec-logo.png    # Main logo (1522×494 px)
├── site.webmanifest        # PWA manifest
├── browserconfig.xml       # Windows tile config (IE/Edge)
├── CNAME                   # GitHub Pages custom domain mapping
├── favicon.ico             # Multi-size Windows icon
├── favicon-16x16.png
├── favicon-32x32.png
├── apple-touch-icon.png    # 180×180 iOS icon
├── android-chrome-192x192.png
├── android-chrome-384x384.png
├── mstile-150x150.png      # Windows tile icon
├── safari-pinned-tab.svg   # Safari pinned tab icon
├── README.md
├── LICENSE
└── .gitignore
```

Everything is in the root — there are no subdirectories, no build output folders, and no framework scaffolding.

## Tech Stack

| Layer        | Technology                          |
|--------------|-------------------------------------|
| Markup       | Plain HTML5                         |
| Styling      | Inline CSS3 (inside `<style>` tag)  |
| Fonts        | Google Fonts — Roboto (300, 400)    |
| JavaScript   | None                                |
| Build system | None                                |
| Dependencies | None (no package.json)              |
| Deployment   | GitHub Pages (push-to-deploy)       |

## Development Workflow

Because there is no build system, the workflow is extremely simple:

1. Edit `index.html` (or other files) directly.
2. Commit and push to `origin/main`.
3. GitHub Pages automatically picks up the change — no build step required.

```bash
# Make changes, then:
git add <files>
git commit -m "descriptive message"
git push -u origin main
```

There are no tests, linters, or pre-commit hooks configured. Keep it that way unless explicitly asked to add them.

## Branching Convention

- `main` — production branch, served live by GitHub Pages. **Do not push breaking changes directly.**
- `claude/<description>-<SESSION_ID>` — AI-created feature branches. Always merge via PR.

## Key Conventions

### HTML
- All CSS lives **inside** a single `<style>` block in `<head>`. Do not introduce an external stylesheet unless specifically requested.
- No JavaScript. Do not add JS unless the user explicitly asks.
- Asset paths are **absolute** (e.g. `/averred-sec-logo.png`), not relative. This is intentional for GitHub Pages.
- The Google Fonts `<link>` is placed at the **end of `<body>`** (render-performance trick) — keep it there.

### CSS
- CSS IDs use **camelCase**: `#barpercent`, `#progress`, `#fill`.
- Section comments describe purpose: `/* Progress bar */`, `/* Fades in animation */`.
- Mobile breakpoint: `@media screen and (max-width: 600px)`.
- Brand colors:
  - Progress bar background: `#a8a8a8`
  - Progress fill (teal): `#00b98b`
  - Theme color: `#ffffff`
- Default font: Roboto (fallback: sans-serif).

### Assets / Images
- File names use **lowercase hyphenated** format: `averred-sec-logo.png`, `apple-touch-icon.png`.
- All favicon variants must be kept in sync when the brand changes.
- The `site.webmanifest` `name` and `short_name` fields are currently empty — fill them in when the full site launches.

### Git Commit Messages
- Use imperative present tense: `Add ...`, `Fix ...`, `Update ...`.
- Include the filename prefix for scoped changes: `index.html: Fix logo path`.

## What NOT to Do

- Do not introduce a package manager (npm/yarn/pnpm) or build tool unless explicitly requested.
- Do not split the CSS into a separate file unless asked.
- Do not add JavaScript frameworks or libraries.
- Do not rename or restructure files without being asked — the flat layout is intentional.
- Do not modify `CNAME` unless the domain is changing.
- Do not push directly to `main` from a Claude feature branch — always use a PR.

## Current Site State

The page shows an "under construction" placeholder:

- Logo centered on a vertically-middle-aligned flex cell.
- `<h1>Hello, World!</h1>` greeting.
- `<h2>This website is currently under construction.</h2>`
- An animated progress bar currently showing **65%** (`#fill { width: 65%; }`).

To update the progress percentage, change the `width` value in `#fill` **and** the text in `<h3>` inside `#barpercent`.

## Deployment Notes

- GitHub Pages serves whatever is on the `main` branch root.
- The `CNAME` file maps the custom domain (`www.averred.net` / `averred.net`).
- No server-side code, no backend, no database — purely static.
- PWA metadata (`site.webmanifest`, `browserconfig.xml`) is in place but `name`/`short_name` fields need completing before the site goes live.
