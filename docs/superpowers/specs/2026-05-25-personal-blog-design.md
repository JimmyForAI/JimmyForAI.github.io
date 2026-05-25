# Personal Blog Design Spec

## Overview

A comprehensive personal homepage built with Hexo static site generator, deployed to GitHub Pages via GitHub Actions.

## Tech Stack

- **Hexo** — static site generator (Node.js)
- **Butterfly** — Hexo theme
- **Markdown** — content authoring
- **GitHub Pages** — hosting
- **GitHub Actions** — CI/CD auto-deploy

## Site Structure

Three main pages:

- **Blog** (`/` — home page with post list, pagination)
- **About** (`/about/` — personal intro)
- **Projects** (`/projects/` — project showcase)

## Architecture

```
src/                    # Hexo project root
├── source/
│   ├── _posts/         # Markdown blog posts
│   ├── about/          # About page (index.md)
│   ├── projects/       # Projects page (index.md)
│   └── images/         # Image assets
├── themes/butterfly/   # Butterfly theme
├── _config.yml          # Hexo config
├── _config.butterfly.yml # Theme config
└── .github/workflows/  # GitHub Actions deploy workflow
```

Content authoring: write `.md` files under `source/_posts/` with YAML Front Matter (title, date, tags, categories).

## Publishing Flow

```
Create .md post → hexo g (generate static files) → git push → GitHub Actions builds and deploys to gh-pages
```

Local preview: `hexo s` starts a dev server at `http://localhost:4000`.

## Theme Features (Butterfly)

- Dark/light mode toggle
- Responsive design
- Code syntax highlighting
- Search
- Tag/category system
- Built-in About and Projects page layouts

## Deployment

GitHub Actions workflow:
1. Trigger on push to `main` branch
2. Install Node.js, install dependencies
3. Run `hexo generate`
4. Deploy `public/` to `gh-pages` branch
5. Site served at `<username>.github.io`

## Scope Boundaries

- No comment system initially (can add later via theme config)
- No analytics initially (can add later)
- No custom theme modifications — use Butterfly as-is with config
- Content is up to the user to write
