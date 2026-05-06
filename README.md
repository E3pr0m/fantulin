# Fantulin

WordPress site running on [Local by Flywheel](https://localwp.com/).

## Stack

- **CMS**: WordPress 6.9.x
- **Theme**: Twenty Twenty-Five (block-based / Full Site Editing)
- **Language**: Italian (`it_IT`)

## Setup

1. Import the site in Local by Flywheel.
2. Restore the database from a dump (not tracked in this repo).
3. Copy `public/wp-config.php` from a team member or create one from `public/wp-config-sample.php`.

## What is tracked

Only custom, non-core WordPress content is versioned:

- `public/wp-content/themes/<custom-theme>/` – custom themes (default themes are ignored)
- `public/wp-content/plugins/` – custom plugins
- `public/wp-content/mu-plugins/` – must-use plugins (if added)
- `CLAUDE.md` – AI assistant context
