# [Guiroy Subtheme](https://github.com/SU-SWS/guiroy_subtheme)
##### Version: 1.0.0

Changelog: [Changelog.txt](CHANGELOG.txt)

Description
---

Guiroy Subtheme is an experimental Stanford sub-theme that works with the Stanford Basic theme. It is largely vibe-coded based on other subthemes and should not be put into production without testing.



Features of this subtheme include:
- Banner with fixed aspect ratio
- Rounded buttons
- Source serif headers
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

Section color overrides
---

The following Stanford Sites section background colors are overridden in
`src/scss/theme/_sections.scss`. The selector class names are anchored to the
original palette hex (set by `stanford_layout_paragraphs`) and will not change
if the palette label changes.

| Palette label | Original hex | Override hex |
| --- | --- | --- |
| Lagunita Light | `#dcecef` | `#3C3846` ($guiroy-navy) |

When Lagunita Light is selected, WYSIWYG paragraph text (`.ptype-stanford-wysiwyg`), which otherwise inherits the default body text color (`#2e2d29`), is overridden to white (`#FFF`) for legibility against the dark background. Links and buttons keep their existing colors.

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
