# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal blog of Joseph R. Jones using Jekyll with the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) theme. Primarily an archive of old posts with occasional new content.

## Common Commands

```bash
# Install dependencies
bundle install

# Run local development server (with live reload)
./tools/run.sh
# Or directly:
bundle exec jekyll s -H 0.0.0.0 -l

# Build for production
JEKYLL_ENV=production bundle exec jekyll b

# Test HTML output
bundle exec htmlproofer --disable-external --check-html --allow_hash_href _site
```

The site runs at http://localhost:4000 when using the dev server.

## Architecture

- **Theme:** jekyll-theme-chirpy (installed via gemspec)
- **Posts:** `_posts/` - Markdown files with YYYY-MM-DD-title.md naming
- **Tabs:** `_tabs/` - Navigation pages (About, Archives)
- **Layouts:** `_layouts/` - Custom home.html shows welcome message and 3 recent posts (overrides theme default)
- **Includes:** `_includes/` - Theme partials (sidebar, comments, etc.)
- **Archived:** `_archived/` - Unused theme tutorial posts

## Content Conventions

- **Categories:** One per post, capitalized
- **Tags:** Multiple allowed, lowercase (except proper nouns like `iPhone`)
- **Permalink format:** `:year/:month/:day/:title/`

## Configuration

Main settings in `_config.yml`:
- Dark theme by default (`theme_mode: dark`)
- Timezone: America/Phoenix
- Avatar: `/assets/img/jrjtoon-square-300.png`
- Paginate: 5 posts per page
