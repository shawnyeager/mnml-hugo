# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## TODO for Next Session

- **Fix horizontal shift issue**: There is a remaining horizontal alignment shift between the home page and other pages. Need to investigate and fix the CSS causing this inconsistency.

## Project Overview

**mnml-hugo** is a minimalist Hugo theme ported from the [mnml Micro.blog theme](https://github.com/jimmitchell/mnml) by Jim Mitchell. This is a standalone Hugo theme that works with any Hugo installation, not a Micro.blog plugin.

Demo: https://mnml.micro.blog (original Micro.blog version)

**Version**: 1.0.0 - Released October 2025

## Architecture

### Hugo Theme Structure

This is a Hugo theme with the standard directory layout:

- `layouts/` - Template files
  - `_default/baseof.html` - Base template that all pages extend
  - `_default/list.html` - List page template (categories, archives)
  - `_default/single.html` - Single post template
  - `partials/` - Reusable template components (head, header, footer, pagination)
  - `post/single.html` - Post-specific single page layout
  - `section/` - Section-specific layouts
  - `shortcodes/` - Custom shortcodes (search.html)
- `static/` - Static assets served as-is
  - `css/` - Stylesheets (main.css, fonts.css, photos-grid.css, photos-masonry.css)
  - `js/` - JavaScript files (menu.js, scroll-to-top.js, search.js)
  - `fonts/` - GT-W font family (Regular, Bold, Oblique variants)
- `i18n/` - Localization files in JSON format (12 languages supported)

### Key Theme Features

**Home Page Categories**: Supports filtering home page posts by category via `home_category` param. Multiple categories can be comma-separated.

**Pinned Posts**: Theme supports pinning a post from a specific category to the top of the home page using `pinned_category` param.

**Photos Display**: Two photo layout modes controlled by `masonry_layout` param:
  - Grid layout (`photos-grid.html` + `photos-grid.css`) - uses IntersectionObserver for lazy loading
  - Masonry layout (`photos-masonry.html` + `photos-masonry.css`)

Photos can be filtered by category using `photos_category` param. The `all_formats` param controls whether to show all image formats or just photos. The `single_image` param shows only the first image from posts with multiple images.

**Pagination**: Controlled by `archive-paginate` param (defaults to 20 on home, 30 on list pages).

**Search**: Custom search shortcode (`{{< search >}}`) that uses client-side JavaScript. Results count controlled by `search_results` param (default 5).

**Date Formatting**: Toggle between short and long date formats using `use_short_date` param. Reading time can be shown with `show_read_time` param.

### CSS Architecture

**Design System**: Uses CSS custom properties in `main.css` with support for both light and dark color schemes via `prefers-color-scheme` media queries.

Key CSS variables:
- Layout: `--header-width` (94rem), `--site-width` (68rem), `--photos-wide` (120rem)
- Typography: `--sans-serif-font` (GTW with fallbacks), `--mono-space-font`
- Colors: Defined separately for light/dark modes (e.g., `--background`, `--text`, `--link`)

**Header Width**: Can be narrowed to match site width using `narrow_header` param (injects inline style).

**Cache Busting**: Stylesheets use `theme_seconds` param as query string for cache invalidation.

### Localization

Internationalization handled via Hugo's i18n system. Translation strings in `i18n/*.json` files include:
- Pagination ("Older", "Newer")
- Post actions ("Continue reading")
- Footer credits ("Hosted by", "Powered by")
- Search placeholder ("Type and hit return")

12 languages supported: English, German, Spanish, Finnish, French, Italian, Polish, Portuguese, Russian, Swedish, Ukrainian, Chinese (Traditional).

### JavaScript Components

**menu.js**: Handles mobile menu toggle functionality
**scroll-to-top.js**: Implements scroll-to-top button behavior
**search.js**: Client-side search functionality for the search shortcode

Scripts are loaded with `defer` attribute in `baseof.html`. Custom plugins can be added via `plugins_js` param.

### Micro.blog Plugin System

**Plugin Definition** (`plugin.json`):
- Version: 2.7.7
- Defines 22 configurable fields exposed in Micro.blog settings UI
- Field types include: string, boolean
- Fields use Hugo's param system (e.g., `params.masonry_layout`, `params.home_category`)
- Special fields: `defaultContentLanguage` (Hugo config level)

**Key Plugin Fields**:
- Language/Localization: `defaultContentLanguage`
- Display options: `use_short_date`, `narrow_header`, `hide_avatar`, `custom_avatar`
- Content filtering: `home_category`, `pinned_category`, `photos_category`
- Layout options: `show_full_post`, `category_full_post`, `masonry_layout`, `full_width_photos`
- Photo settings: `all_formats`, `single_image`
- Footer customization: `hide_copyright`, `footer_rss`, `hide_credit`
- Features: `show_read_time`, `show_categories`, `show_category_count`, `search_results`, `fediverse_creator`

**Micro.blog Platform Integration**:
- `partial "microblog_head.html"` in head.html for platform integration
- Archive JSON format (`list.archivejson.json`)
- Photos page format (`list.photoshtml.html`)
- Relies on Micro.blog injecting `theme_seconds` param for cache busting

## Development

### Plugin Development Workflow

Since this is a Micro.blog plugin, development follows the Micro.blog plugin system:

1. **Making Changes**: Edit templates, CSS, or JavaScript files locally
2. **Testing**: Install the plugin on a Micro.blog site (required for full integration testing)
   - Users can install via GitHub URL using "New Plug-in" button in Micro.blog
   - Use the "reload" button in Micro.blog to sync updates from the GitHub repository
3. **Version Management**: Update version number in `plugin.json` when releasing changes

**Important Notes**:
- This theme relies on Micro.blog-specific partials (e.g., `microblog_head.html`) and platform-injected params (e.g., `theme_seconds`)
- Parameters defined in `plugin.json` are set by users through Micro.blog's web UI, not in local config files
- Standard Hugo development may not work identically due to Micro.blog platform integration

### Adding New Plugin Fields

To add a new configurable option:

1. Add a field object to the `fields` array in `plugin.json`:
```json
{
  "field": "params.your_param_name",
  "label": "Display Name",
  "type": "boolean",  // or "string"
  "placeholder": "Optional help text"
}
```

2. Access the parameter in templates: `{{ .Site.Params.your_param_name }}`

3. Increment the version number in `plugin.json`

### Testing Theme Changes

**Recommended approach**: Install on a Micro.blog site
- Clone the GitHub repository through Micro.blog's plugin interface
- Make changes and push to GitHub
- Use the "reload" button in Micro.blog to pull updates

**Local Hugo testing** (limited):
- May not replicate Micro.blog's exact behavior
- Requires manually creating config files with parameters
- Missing platform-specific partials will cause errors

### Modifying Styles

When editing CSS:
1. Main styles are in `static/css/main.css`
2. Respect the existing CSS custom properties pattern
3. Maintain both light and dark mode color scheme support
4. Photo-specific styles in separate files (`photos-grid.css`, `photos-masonry.css`)

### Adding Localizations

To add a new language:
1. Create `i18n/[language-code].json` with translations for all existing keys
2. Use the structure from `i18n/en.json` as reference

### Template Modifications

When modifying layouts:
- `baseof.html` is the base template; changes affect all pages
- Use Hugo's `partial` function for reusable components
- Follow existing pattern of conditional rendering based on `.Site.Params`
- Maintain accessibility and semantic HTML
