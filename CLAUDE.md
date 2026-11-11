# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based static site with a custom terminal UI theme built using WebTUI. The site uses Jekyll as a static site generator but has fully custom layouts that provide a terminal/command-line aesthetic.

## Development Commands

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

The categories are part of the post's URL (`/category1/category2/YYYY/MM/DD/slug.html`). The home page and the page description show the first paragraph of a post, unless the front matter has an `excerpt`.

Images go in `assets/images/`. For a picture with a caption, write a `<figure>` with an `<img>` and a `<figcaption>` (see the 2026-11-11 post). Markdown tables are styled too.

### Configuration
The `_config.yml` file contains site metadata (title, email, description, social usernames) and build settings. Changes require server restart to take effect.

### Custom Terminal Theme

The site uses a **fully custom theme** built from scratch with terminal UI aesthetics:

**CSS Framework**: WebTUI - A modular CSS library for terminal UI components (https://webtui.ironclad.sh/)
- Loaded via CDN: https://cdn.jsdelivr.net/npm/@webtui/css@latest/dist/full.css
- Pure CSS (no JavaScript required)
- Provides semantic HTML attributes like `is-="view"`, `is-="view-content"`, `marker-="tree"`, etc.

**Custom Layouts**:
- `_layouts/default.html`: Base layout with the bar on top, main content, and footer
- `_layouts/home.html`: Blog index page showing posts with `$ cat posts.log` aesthetic
- `_layouts/post.html`: Individual blog post layout with file-like metadata
- `_layouts/page.html`: Static page layout

**The bar** (`_includes/navigation.html`):
- A thin strip that stays at the top of the page, like the status bar on Patrick's desktop
- The site name on the left; the pages on the right, numbered like workspaces (`1 posts`, `2 about`, `3 github`)
- The page you are on gets the class `is-active` (Liquid, from `page.url` and `page.layout`; a single post counts as "posts")

**Look** (`assets/css/main.css`):
- The Hackerman theme of Patrick's desktop (his dotfiles, `themes/hackerman`): soft mint on deep blue-black
- CSS variables at the top of the file: `--bg-deep`, `--bg`, `--surface`, `--text`, `--fg`, `--mint`, `--cyan` and a few more
- Content sits in "windows": boxes with a rounded 2px border. The window with the focus (a post, a page, the post box under the mouse on the home page) has the accent colour `--cyan`; the others have `--surface`
- JetBrains Mono everywhere, loaded from Google Fonts with a real italic
- Code blocks get the editor's colours through the token classes of Rouge, Jekyll's highlighter (`.highlight [class^="k"]` for keywords and so on)
- `--muted` is for decoration only; it is too dim for text that has to be read. Meta lines and captions use `--subtle`

**WebTUI Attributes Used**:
- `<div is-="view">` and `<div is-="view-content">`: the boxes. WebTUI 0.1.10 has no styles of its own for these; `main.css` styles them
- `<div is-="typography-block">`: Typography styling wrapper
- `<ul marker-="tree">` on the home page: the attribute is still there, but `main.css` hides the markers (they landed above each post box)

**WebTUI Gotchas**:
- It is loaded as `@latest` from a CDN, so its rules can change without a commit here. Checked against 0.1.10 on 2026-11-11
- All its rules live in CSS layers. Any plain rule in `main.css` wins over them, whatever the selector; `!important` is never needed
- It sets `word-break: break-all` on `body` (words cut in half at the end of a line) and draws table lines with pseudo-elements. `main.css` undoes both; keep those rules

**Modifying the Theme**:
- Colors: Edit CSS variables in `assets/css/main.css`
- Layout structure: Edit files in `_layouts/`
- The bar: Edit `_includes/navigation.html`
- Head/meta tags: Edit `_includes/head.html`

### Plugins
- `jekyll-feed`: Generates an Atom feed at `/feed.xml`
