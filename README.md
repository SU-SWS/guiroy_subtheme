# [Guiroy Subtheme](https://github.com/SU-SWS/guiroy_subtheme)
##### Version: 1.0.0

Changelog: [Changelog.txt](CHANGELOG.txt)

Description
---

Guiroy Subtheme is an experimental Stanford sub-theme that works with the Stanford Basic theme. It is largely vibe-coded based on other subthemes and should not be put into production without testing.



Features of this subtheme include:
- Banner with fixed aspect ratio
- Rounded buttons
- It is also based on the Minimally Branded subtheme, as this theme is meant to have very little branding.

Documentation
---
See subtheming guides and best practices here: 
https://devguide.sites.stanford.edu/front-end/drupal/sub-themes 

Installation
---
Install on a site that uses Stanford Basic as an enabled theme.

Configuration
---

Nothing special needed. Install, enable, and set as the default active theme.

Developer
---

If you wish to develop on this theme you will most likely need to compile some new css. Please use the sass structure provided and compile with the sass compiler packaged in this theme. To install:

```
nvm install 18
nvm use
```
After you've made a change you want to see processed, you can run:
```
npm run build
```
This will process scss, js, and asset files, preparing them from the src directory to the dist directory.


Contribution / Collaboration
---

You are welcome to contribute functionality, bug fixes, or documentation to this theme. If you would like to suggest a fix or new functionality you may add a new issue to the GitHub issue queue or you may fork this repository and submit a pull request. For more help please see [GitHub's article on fork, branch, and pull requests](https://help.github.com/articles/using-pull-requests)
