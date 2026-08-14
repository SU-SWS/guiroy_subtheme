# [Guiroy Subtheme](https://github.com/SU-SWS/guiroy_subtheme)
##### Version: 1.0.0

Changelog: [Changelog.txt](CHANGELOG.txt)

Description
---

Guiroy Subtheme is an experimental Stanford sub-theme that works with the Stanford Basic theme. It is largely vibe-coded based on other subthemes and should not be put into production without testing.



Features of this subtheme include:
- Banner with fixed aspect ratio
- Rounded buttons
- Space Grotesk headings and site name
- Some settings from Minimally Branded subtheme, as this theme is meant to have very little branding.

Documentation
---
See subtheming guides and best practices here: 
https://devguide.sites.stanford.edu/front-end/drupal/sub-themes 

Installation
---
Install on a site that uses Stanford Basic as an enabled theme.

Build requirements
---
The front-end build requires **Node.js 18** (see `.nvmrc` and `package.json` engines). Older Node versions (e.g. 11 or 12) cause build failures because a dependency (cosmiconfig via postcss-loader) uses optional chaining (`?.`), which needs Node 14+.

Before running the build:
```bash
nvm use      # use Node from .nvmrc (18)
# or, if Node 18 isn't installed:
nvm install 18
nvm use 18
npm install  # install dependencies (first time, or after pulling changes to package.json)
npm run build
```

This theme uses **npm** as its package manager (`package-lock.json`). Do not install with yarn or commit a `yarn.lock` file.

Configuration
---

Nothing special needed. Install, enable, and set as the default active theme.

Colors
---

Subtheme-specific color variables are defined in `src/scss/utilities/variables/_colors.scss`. Stanford/Decanter colors are not defined here.

Brand palette:

| Variable | Hex |
| --- | --- |
| `$guiroy-navy` | `#3C3846` |
| `$guiroy-blue` | `#4A4B7B` |
| `$guiroy-yellow` | `#FDE9CC` |
| `$guiroy-orange` | `#FDBE83` |
| `$guiroy-lavender` | `#C8A3B5` |
| `$guiroy-teal` | `#2F4E68` |

Fonts
---

**Space Grotesk** is self-hosted in `src/assets/fonts/space-grotesk/` (copied from the source files in the top-level `assets/Space_Grotesk/` folder), with `@font-face` declarations and the `$guiroy-font-sans` variable in `src/scss/theme/_typography.scss`. Only two static weights are loaded:

| Weight | File | Used for |
| --- | --- | --- |
| 500 (Medium) | `SpaceGrotesk-Medium.ttf` | Headings h1–h4, WYSIWYG headings, card/entity/list headlines |
| 700 (Bold) | `SpaceGrotesk-Bold.ttf` | Site name / lockup lines (`.su-lockup__line1`–`line5`) in the header |

Everything else (body text, nav, etc.) falls back to Stanford Basic / Decanter's default sans-serif stack.

Source Serif 4 was previously loaded from Google Fonts (`source-serif` library in `guiroy_subtheme.libraries.yml`) for headings and the site name, but is no longer used now that both were switched to Space Grotesk — the library dependency and the unused `$guiroy-font-serif` variable have been removed.

Section color overrides
---

The following Stanford Sites section background colors are overridden in
`src/scss/theme/_sections.scss`. The selector class names are anchored to the
original palette hex (set by `stanford_layout_paragraphs`) and will not change
if the palette label changes.

| Palette label | Original hex | Override hex |
| --- | --- | --- |
| Lagunita Light | `#dcecef` | `#3C3846` ($guiroy-navy) |

When Lagunita Light is selected, WYSIWYG paragraph text (`.ptype-stanford-wysiwyg`), which otherwise inherits the default body text color (`#2e2d29`), is overridden to white (`#FFF`) for legibility against the dark background. Secondary buttons (`.su-button--secondary`) in this section get a transparent background, a solid white border, and white text/arrow instead of their default white background and gradient border. Regular inline links (and their icons) in this section are white with a `$guiroy-yellow` hover state.

Link colors
---

Regular inline links in `.ptype-stanford-wysiwyg` (defined in `src/scss/theme/_links.scss`) use `$guiroy-teal` with a `$guiroy-navy` hover state, replacing the Decanter default (digital blue / black hover). This covers both link text and link icons (external, download, action, jump, video, internal). Button-styled links (`.su-button`, `.su-button--secondary`, `.su-button--big`) are excluded and keep their own colors. On the navy section background (see above), these same links switch to white with a `$guiroy-yellow` hover state instead.

Header (masthead)
---

The masthead background is `$guiroy-navy` (`src/scss/components/masthead/_masthead.scss`), with the lockup cell divider borders switched to white so they stay visible.

Nav and search text (`src/scss/components/main-nav/_main-nav.scss` and `src/scss/components/search/_search.scss`) are white by default with a `$guiroy-yellow` hover/focus/active state, matching the navy-section link scheme above. This covers the mobile hamburger toggle label, top-level menu links, and dropdown/flyout submenu links. Dropdown submenu panels get the same `$guiroy-navy` background as the masthead rather than the default white panel. The nav's accent/current-item indicator bars, previously `$guiroy-color-primary` (now equal to `$guiroy-navy` — see Colors above), were switched to `$guiroy-yellow` so they stay visible against the navy background instead of disappearing.

The search submit icon (`src/assets/svg/search-white.svg`) and dropdown caret icon (`src/assets/svg/caret-down-white.svg`) are white versions of the originals, since both only render on the navy masthead.

Brand gradient
---

`$guiroy-gradient-divider` (defined in `src/scss/utilities/variables/_colors.scss`) is a left-to-right gradient across the full brand palette (navy → teal → blue → lavender → orange → yellow), the same approach as vpue_undergrad_subtheme's `$vpue-gradient-footer-divider`. It's used in two places:

- The brand bar (`.su-brand-bar--dark`, `src/scss/components/brandbar/_brandbar.scss`) — 1rem tall, background is the gradient.
- The bottom of the local footer (`.su-local-footer`, `src/scss/components/local-footer/_local-footer.scss`) — a matching 1rem `border-bottom` using the same gradient via `border-image`.

Local footer
---

`.su-local-footer` (`src/scss/components/local-footer/_local-footer.scss`) has a `$guiroy-navy` background with white text. Links are white by default with a `$guiroy-yellow` hover/focus state, matching the scheme used elsewhere on navy backgrounds (section overrides, WYSIWYG links, nav) — this covers both link text and mask-based link icons (e.g. the action-links arrows). Social icons and the lockup cell divider borders in the footer header, which default to black, are switched to white for the same reason.

Developer
---

If you wish to develop on this theme you will most likely need to compile some new css. Please use the sass structure provided and compile with the sass compiler packaged in this theme. To install:

```
nvm install 18
nvm use
npm install
```
After you've made a change you want to see processed, you can run:
```
npm run build
```
This will process scss, js, and asset files, preparing them from the src directory to the dist directory.


Contribution / Collaboration
---

You are welcome to contribute functionality, bug fixes, or documentation to this theme. If you would like to suggest a fix or new functionality you may add a new issue to the GitHub issue queue or you may fork this repository and submit a pull request. For more help please see [GitHub's article on fork, branch, and pull requests](https://help.github.com/articles/using-pull-requests)
