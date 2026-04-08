# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A personal academic portfolio website for Mohammed Anas Ali, built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme. Deployed to `https://dcwire.github.io` via GitHub Actions (`gh-pages` branch).

## Local Development

**Docker (recommended):**
```bash
docker compose pull
docker compose up
# Visit http://localhost:8080
```

**Native Ruby (legacy):**
```bash
bundle install
pip install jupyter
bundle exec jekyll serve
# Visit http://localhost:4000
```

**Build only:**
```bash
bundle exec jekyll build  # outputs to _site/
```

## Deployment

Pushing to `main` automatically triggers `.github/workflows/deploy.yml`, which builds and pushes to the `gh-pages` branch. GitHub Pages serves from `gh-pages`. Do not manually edit or push to `gh-pages`.

## Architecture

| Path | Purpose |
|------|---------|
| `_config.yml` | All site settings — personal info, plugins, feature flags, third-party library versions |
| `_pages/about.md` | Homepage (landing page at `/`) |
| `_data/*.yml` | Structured content: `cv.yml`, `socials.yml`, `repositories.yml`, `coauthors.yml`, `venues.yml` |
| `_bibliography/papers.bib` | Publications (rendered by `jekyll-scholar`) |
| `_projects/` | Project cards |
| `_posts/` | Blog posts |
| `_includes/` | Liquid partials; `_includes/cv/` and `_includes/resume/` handle CV rendering |
| `_layouts/` | Page templates |
| `assets/json/resume.json` | JSON Resume format, pulled in via `jekyll-get-json` |

## Content Editing

- **Personal info**: Edit `_config.yml` fields (`first_name`, `last_name`, etc.) and `_pages/about.md`
- **CV**: Edit `_data/cv.yml` (structured sections) or `assets/json/resume.json` (JSON Resume)
- **Publications**: Edit `_bibliography/papers.bib` — jekyll-scholar renders these automatically
- **Social links**: Edit `_data/socials.yml`
- **GitHub repos on site**: Edit `_data/repositories.yml`

## Key Config Flags (in `_config.yml`)

- `enable_darkmode`, `enable_math`, `enable_masonry`, `enable_medium_zoom` — toggle UI features
- `scholar.last_name` / `scholar.first_name` — controls which author name is highlighted in publication lists
- `imagemagick.enabled` — requires `convert` (ImageMagick) on PATH; disable if not installed
- `external_sources` — for pulling in external blog posts (currently commented out)
