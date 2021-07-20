# Changelog

This file contains the detail of changelogs. For **release**, [check this](https://github.com/dinhanhthi/dinhanhthi.com/releases).

## Verion 4

### 4.5.1

1. Remove unnecessary image files from `/src/img/` and keep only the files (and directories) which are used in `sample_posts/`'s posts.
2. Change static images url (ones used by the theme, not the posts) to `img_src` (before is `img`). You can check this in `.eleventy.js`.
3. Create this changelog.
4. (For me only) Default built directory is back to `_site` and change output directory of `local:watch` to `_built`.
5. **Fix**: flash load if using animation => removing all transition for background!