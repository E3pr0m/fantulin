# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **WordPress 6.9.4** site running on Local by Flywheel. The WordPress installation lives entirely under `public/`. The active theme is **Twenty Twenty-Five** (`public/wp-content/themes/twentytwentyfive/`), a block-based Full Site Editing (FSE) theme.

No custom plugins are currently installed. Development work primarily involves the active theme and any future custom plugins under `public/wp-content/`.

## Commands

All theme build commands must be run from inside the theme directory:

```bash
cd public/wp-content/themes/twentytwentyfive

npm install          # Install dependencies (requires Node >= 20.10.0)
npm run build        # Compile style.css → style.min.css via PostCSS + cssnano
npm run watch        # Watch and rebuild on change
```

The same scripts are available in `twentytwentytwo/` if needed.

There is no root-level build, lint, or test runner. WordPress itself is a pre-built distribution.

## Architecture

### Entry Points

- `public/index.php` → `public/wp-blog-header.php` — bootstraps WordPress and dispatches the request
- `public/wp-admin/` — WordPress admin panel (separate request cycle)
- `public/wp-json/` — REST API (available but not currently used)

### Key Directories

| Path | Purpose |
|------|---------|
| `public/wp-config.php` | DB credentials, constants, environment flags |
| `public/wp-content/themes/` | Themes; only `twentytwentyfive` is active |
| `public/wp-content/plugins/` | Custom plugins go here |
| `public/wp-content/uploads/` | User-uploaded media |
| `conf/` | Local by Flywheel server config (Apache, MySQL, PHP) |

### Theme Architecture (Twenty Twenty-Five / FSE)

The active theme uses WordPress **Full Site Editing**: layout is defined in `theme.json` (global styles, typography, spacing, color palette) and block templates in `templates/` and `parts/`. There are no traditional PHP template files like `single.php` or `page.php` — everything is rendered via the block editor.

Custom styles are in `style.css` and compiled to `style.min.css` (the file WordPress actually enqueues).

### Environment

- `WP_ENVIRONMENT_TYPE` is set to `local` in `wp-config.php`
- `WP_DEBUG` is `false`; XDebug is available via Local's tooling
- Database: MySQL, host `localhost`, DB name `local`
- Italian locale (`it_IT`) is configured
