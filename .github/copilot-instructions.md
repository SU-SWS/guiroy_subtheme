# Copilot / AI agent instructions — Guiroy Subtheme

Purpose
- This repo is a Drupal sub-theme (machine name: `guiroy_subtheme`) built on the `stanford_basic` base theme. The repository contains front-end source (SCSS, minimal JS, assets) and Drupal theme metadata. AI agents should focus on the front-end build pipeline and Drupal library consumption patterns.

Quick start (developer commands)
- Install node deps: `yarn install`
- Build production assets: `yarn build`  (runs `NODE_ENV=production webpack`)
- Watch for changes (default script): `yarn watch` (note: the `watch` script currently sets `NODE_ENV=production`; see "Dev/HMR" below for how to run true dev/HMR)

Build outputs & how they are consumed
- Webpack entry points (see `webpack.config.js`):
  - `main` -> `src/scss/main.scss` -> outputs `dist/css/main.css`
  - `ckeditor5` -> `src/scss/ckeditor5.scss` -> outputs `dist/css/ckeditor5.css`
- `guiroy_subtheme.libraries.yml` references `dist/css/main.css` in the `allpages` library.
- `guiroy_subtheme.info.yml` sets `ckeditor5-stylesheets: [dist/css/ckeditor5.css]` for editor integration.
- Webpack's `FileManagerPlugin` deletes `dist/` at the start of each build; expect a clean `dist/` after every run.

Dev / HMR notes (important gotcha)
- The repo supports Hot Module Replacement (HMR) when `NODE_ENV !== 'production'` and `NO_HMR` is not set.
- The package `watch` script explicitly sets `NODE_ENV=production`, so to run with dev/HMR run webpack directly instead of `yarn watch`. Example:
  - `NODE_ENV=development npx webpack --watch`
- To force-disable HMR even when not production: set `NO_HMR=1`.

SCSS structure & conventions
- SCSS follows SMACSS-like categories. Main source: `src/scss/main.scss` which imports:
  - `src/scss/utilities/` (mixins, variables; e.g. `utilities/mixins/_buttons.scss`, `utilities/variables/_colors.scss`)
  - `src/scss/base/`, `components/`, `layout/`, `print/`, `state/`, `theme/`
- To add a component style: create `_mycomponent.scss` under `src/scss/components/` (or a subfolder like `components/cards/`) and import via `components/index.scss`.
- Theme-level visual tweaks go in `src/scss/theme/` (e.g. `_button.scss`, `_cta.scss`). Use mixins in `utilities/mixins/` to ensure consistent branding.
- Color and brand overrides: edit `src/scss/utilities/variables/_colors.scss` as the canonical place for theme color additions.

Assets & webpack aliases
- Webpack aliases (see `webpack.config.js`) you can use in SCSS/JS:
  - `decanter-assets` => `node_modules/decanter/core/src/img`
  - `decanter-src` => `node_modules/decanter/core/src`
  - `@fortawesome` and `fa-fonts` for Font Awesome assets
- SCSS variables reference these (example in `src/scss/main.scss`): `$su-image-path: '~decanter/core/src/img'` and `$fa-font-path`.

Drupal integration points
- Theme metadata: `guiroy_subtheme.info.yml` (regions, base theme, editor stylesheet)
- Libraries: `guiroy_subtheme.libraries.yml` controls which compiled CSS is loaded for pages.
- Typical dev checklist when opening PRs (see `.github/pull_request_template.md`): rebuild caches and import config: `drush cr ; drush ci`.

CI & release
- This repository has GitHub workflows for PR labeling and a `release` workflow that tags a release when PRs are merged/closed. There is no automated test suite (no unit/behat tests) discovered in the repo currently.

## Related repositories
- SU-SWS/stanford_profile — This repo includes the Base theme this repo extends. Contains shared styles, variables, and foundational patterns. This repo also includes configuration for Drupal profiles that use this theme.
- SU-SWS/stanford_profile_helper - This repo contains helper functions and utilities for the Stanford Profile theme, including some SCSS mixins and JS behaviors that may be relevant.
- decanter (https://github.com/SU-SWS/decanter or npm `decanter`) — Design system dependency used via SCSS imports (`decanter/core/src`).
Notes:
- Priority order when reading: `stanford_profile` → `stanford_profile_helper` → this repo.
- Please avoid using decanter components/styles directly unless necessary; prefer using or extending styles from `stanford_profile` first.

Conventions & patterns (explicit)
- Use `.is-` prefix for transient state classes (see comments in `guiroy_subtheme.libraries.yml`).
- Keep visual-only rules under `theme/`; functional/component styles should live under `components/`.
- Prefer mixins for reusable button/cta styles (`utilities/mixins/_buttons.scss`, `_cta.scss`).

Where to look for examples
- `src/scss/main.scss` — entry file showing how everything is composed
- `webpack.config.js` — build and asset behavior (aliases, plugins, HMR logic, output folders)
- `guiroy_subtheme.libraries.yml` / `guiroy_subtheme.info.yml` — how compiled assets are consumed by Drupal
- `.github/pull_request_template.md` — PR expectations and commands reviewers expect

Notable gotchas / checks for PRs
- Ensure `dist/` is present with the updated CSS after a `yarn build` (FileManagerPlugin deletes `dist/` at build start)
- `yarn watch` may not enable HMR due to `NODE_ENV=production` in the script; prefer direct webpack invocation for dev HMR as shown above.

