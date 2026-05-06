# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **WordPress 6.9.4** site running on Local by Flywheel. The WordPress installation lives entirely under `public/`. The active theme is **Twenty Twenty-Five** (block-based Full Site Editing), but it is not tracked in git — only custom themes and plugins under `public/wp-content/` are versioned.

## Commands

There is no root-level build, lint, or test runner. WordPress itself is a pre-built distribution. If a custom theme with a build step is added, run its npm scripts from inside the theme directory.

## Architecture

### Entry Points

- `public/index.php` → `public/wp-blog-header.php` — bootstraps WordPress and dispatches the request
- `public/wp-admin/` — WordPress admin panel (separate request cycle)
- `public/wp-json/` — REST API (available but not currently used)

### Key Directories

| Path | Purpose |
|------|---------|
| `public/wp-config.php` | DB credentials, constants, environment flags |
| `public/wp-content/themes/` | Themes; `twentytwentyfive` is active (not tracked — add custom themes here) |
| `public/wp-content/plugins/` | Custom plugins go here |
| `public/wp-content/uploads/` | User-uploaded media |
| `conf/` | Local by Flywheel server config (Apache, MySQL, PHP) |

### Theme Architecture (FSE)

The active theme uses WordPress **Full Site Editing**: layout is defined in `theme.json` (global styles, typography, spacing, color palette) and block templates in `templates/` and `parts/`. There are no traditional PHP template files like `single.php` or `page.php` — everything is rendered via the block editor. Custom themes should follow the same FSE structure.

### Environment

- `WP_ENVIRONMENT_TYPE` is set to `local` in `wp-config.php`
- `WP_DEBUG` is `false`; XDebug is available via Local's tooling
- Database: MySQL, host `localhost`, DB name `local`
- Italian locale (`it_IT`) is configured
