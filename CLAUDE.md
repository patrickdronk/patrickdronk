# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based static site with a custom terminal UI theme built using WebTUI. The site uses Jekyll as a static site generator but has fully custom layouts that provide a terminal/command-line aesthetic.

th## Development Commands

### Local Development Server
```bash
bundle exec jekyll serve
```
Starts the development server at http://localhost:4000 (default). The server auto-regenerates pages when files change, but does NOT reload `_config.yml` automatically - restart the server after config changes.

### Build Site
```bash
bundle exec jekyll build
```
Generates the static site in the `_site/` directory.

### Install Dependencies
```bash
bundle install
```
Run this after cloning the repository or when Gemfile changes.

## Architecture

### Directory Structure
- `_posts/`: Blog post content in Markdown format with YYYY-MM-DD-title.markdown naming convention
- `_layouts/`: Custom layout templates (default.html, home.html, post.html, page.html)
- `_includes/`: Reusable template partials (head.html, navigation.html)
- `assets/css/`: Custom CSS files including main.css with terminal color scheme
- `_site/`: Generated static HTML files (excluded from git, regenerated on build)
- `_config.yml`: Site-wide configuration including title, description, theme, and plugins
- `_jekyll-cache/`: Build cache (excluded from git)

### Content Creation
Blog posts must:
- Be placed in `_posts/` directory
- Follow naming pattern: `YYYY-MM-DD-title-with-hyphens.markdown`
- Include YAML front matter with at minimum: `layout`, `title`, `date`, and `categories`

### Configuration
The `_config.yml` file contains site metadata (title, email, description, social usernames) and build settings. Changes require server restart to take effect.

### Custom Terminal Theme

The site uses a **fully custom theme** built from scratch with terminal UI aesthetics:

**CSS Framework**: WebTUI - A modular CSS library for terminal UI components (https://webtui.ironclad.sh/)
- Loaded via CDN: https://cdn.jsdelivr.net/npm/@webtui/css@latest/dist/full.css
- Pure CSS (no JavaScript required)
- Provides semantic HTML attributes like `is-="view"`, `is-="view-content"`, `marker-="tree"`, etc.

**Custom Layouts**:
- `_layouts/default.html`: Base layout with header, navigation, main content, and footer
- `_layouts/home.html`: Blog index page showing posts with `$ cat posts.log` aesthetic
- `_layouts/post.html`: Individual blog post layout with file-like metadata
- `_layouts/page.html`: Static page layout

**Custom Navigation** (`_includes/navigation.html`):
- Terminal command-style navigation (`$ ls posts`, `$ cd about`)
- Uses WebTUI list markers for visual consistency

**Color Scheme** (`assets/css/main.css`):
- Catppuccin-inspired dark terminal colors
- CSS variables: `--terminal-bg`, `--terminal-fg`, `--terminal-accent`, `--terminal-green`, etc.
- Monospace font family (Courier New)
- Custom styling for links, headings, code blocks, and WebTUI components

**WebTUI Components Used**:
- `<div is-="view">` and `<div is-="view-content">`: Terminal-style boxes with rounded dimensions
- `<div is-="typography-block">`: Typography styling wrapper
- `<ul marker-="tree">`: Tree-style list markers for blog post listings
- `<ul marker-="bullet">`: Bullet-style markers for navigation

**Modifying the Theme**:
- Colors: Edit CSS variables in `assets/css/main.css`
- Layout structure: Edit files in `_layouts/`
- Navigation: Edit `_includes/navigation.html`
- Head/meta tags: Edit `_includes/head.html`

### Plugins
- `jekyll-feed`: Generates an Atom feed at `/feed.xml`
