# mnml for Hugo

![mnml](https://raw.githubusercontent.com/jimmitchell/mnml/main/icon.jpg)

A clean and simple minimalist theme for Hugo, ported from the [mnml Micro.blog theme](https://github.com/jimmitchell/mnml) by [Jim Mitchell](https://jimmitchell.org).

See the original theme in action at [mnml.micro.blog](https://mnml.micro.blog).

## Installation

### Option 1: Git Submodule

```bash
cd your-hugo-site
git submodule add https://github.com/shawnyeager/mnml-hugo.git themes/mnml-hugo
```

### Option 2: Clone

```bash
cd your-hugo-site/themes
git clone https://github.com/shawnyeager/mnml-hugo.git
```

### Option 3: Hugo Modules (requires Go)

In your `hugo.toml`:

```toml
[module]
  [[module.imports]]
    path = "github.com/shawnyeager/mnml-hugo"
```

## Quick Start

1. Copy the example configuration from `exampleSite/hugo.toml` to your site's `hugo.toml`
2. Customize the parameters
3. Create content in `content/post/`
4. Run `hugo server` to preview

## Key Features

- Localized for 12 languages
- System display mode aware (light and dark)
- Mobile responsive
- Featured post category setting
- Custom home page category setting
- Multiple, comma-separated home page categories
- Choose between wider or narrower site header
- Choose between long or short date formats
- Display full posts on category pages
- Custom photos page category setting
- Grid or Masonry photo layout options
- Show all image formats on photos page
- Wide or narrow photo page layout setting
- Use a custom site icon
- Hide the site avatar altogether if you choose
- Built-in search functionality
- Automatic video embedding from markdown links (MP4, MOV, WebM)
- Optional archive years feature for filtering posts by year
- [Fediverse Creator](https://blog.joinmastodon.org/2024/07/highlighting-journalism-on-mastodon/) tag support
- Pagination on all post-related pages

## Configuration

All parameters are optional with sensible defaults. See `exampleSite/hugo.toml` for a complete example.

### Basic Configuration

```toml
baseURL = "https://example.com/"
languageCode = "en"
title = "My Blog"
theme = "mnml-hugo"

defaultContentLanguage = "en"

[pagination]
  pagerSize = 20

[permalinks]
  post = "/:filename/"

[taxonomies]
  category = "categories"
  tag = "tags"

[outputs]
  home = ["HTML", "RSS", "archivejson"]
  section = ["HTML", "RSS"]
  archive = ["HTML", "archivehtml"]  # Required for archive_years feature

[outputFormats.RSS]
  mediaType = "application/rss+xml"
  baseName = "feed"

[outputFormats.archivejson]
  mediaType = "application/json"
  baseName = "archive/index"
  isPlainText = true
  notAlternative = true

[outputFormats.archivehtml]
  mediaType = "text/html"
  baseName = "index"

[params]
  description = "A minimal, simple and clean blog."
  itunes_description = "A minimal, simple and clean blog."
  theme_seconds = "1"  # Cache busting version
```

### Theme Parameters

#### Date & Time
- `use_short_date` (boolean) - Use short date format (default: false)
- `show_read_time` (boolean) - Show reading time on posts (default: true)

#### Header & Avatar
- `narrow_header` (boolean) - Use narrow header width (default: false)
- `hide_avatar` (boolean) - Hide site avatar (default: false)
- `custom_avatar` (string) - URL to custom avatar image

#### Home Page
- `home_category` (string) - Filter by category (comma-separated for multiple)
- `pinned_category` (string) - Category for pinned post (default: "Pinned")
- `show_full_post` (boolean) - Show full posts vs summaries (default: false)

#### Category/Archive Pages
- `category_full_post` (boolean) - Show full posts on category pages (default: false)
- `show_categories` (boolean) - Show category list on archives (default: true)
- `show_category_count` (boolean) - Show post counts on category tags (default: true)
- `archive_years` (boolean) - Enable year filtering on archive page (default: false)

**Archive Years Feature**: When enabled, adds a dropdown to filter archive posts by year. Based on the [Archive Years plugin](https://github.com/jimmitchell/plugin-mnml-archive-years) by Jim Mitchell. Requires `archivehtml` output format on the archive section (see configuration above).

#### Photos
- `photos_category` (string) - Filter photos by category (default: "Photos")
- `all_formats` (boolean) - Show all image formats (default: false)
- `masonry_layout` (boolean) - Use masonry layout (default: false = grid)
- `full_width_photos` (boolean) - Use wider photos layout (default: false)
- `single_image` (boolean) - Show only first image (default: false)

#### Search
- `search_results` (integer) - Number of search results to display (default: 5)

#### Footer
- `hide_copyright` (boolean) - Hide copyright notice (default: false)
- `footer_rss` (boolean) - Add RSS link to footer (default: true)
- `hide_credit` (boolean) - Hide theme credits (default: false)

#### Advanced
- `fediverse_creator` (string) - Fediverse creator tag (e.g., @user@mastodon.social)
- `archive-paginate` (integer) - Archive page size (default: 30)

## Creating Content

### Regular Posts

Create posts in `content/post/`:

```markdown
---
title: "My First Post"
date: 2025-10-06T10:00:00-00:00
categories: ["Blog"]
---

Your content here...
```

### Short Posts (Microblog Style)

Posts without titles work great for microblogging:

```markdown
---
date: 2025-10-06T10:00:00-00:00
categories: ["Micro"]
---

Just a quick thought...
```

### Photo Posts

Add photos using the `photos` parameter:

```markdown
---
title: "My Photo Collection"
date: 2025-10-06T10:00:00-00:00
categories: ["Photos"]
photos:
  - "/images/photo1.jpg"
  - "/images/photo2.jpg"
---

Optional description...
```

### Video Posts

Videos are automatically embedded when you link to .mp4, .mov, or .webm files:

**Simple video:**
```markdown
---
date: 2025-10-06T10:00:00-00:00
---

Check out this video:

[Video description](/uploads/video.mp4)
```

**Video with poster image:**
```markdown
[Video description](/uploads/video.mp4 "/uploads/poster.png")
```

The theme automatically converts these to HTML5 video players with controls.

### Adding a Search Page

Create `content/search.md`:

```markdown
---
title: "Search"
date: 2025-10-06T10:00:00-00:00
---

{{< search >}}
```

Then add it to your menu in `hugo.toml`:

```toml
[[menu.main]]
  name = "Search"
  url = "/search/"
  weight = 4
```

## Multi-language Support

The theme supports 12 languages:

- English (en)
- German (de)
- Spanish (es)
- Finnish (fi)
- French (fr)
- Italian (it)
- Polish (pl)
- Portuguese (pt)
- Russian (ru)
- Swedish (sv)
- Ukrainian (uk)
- Chinese Traditional (zh-TW)

Set your language in `hugo.toml`:

```toml
defaultContentLanguage = "de"
```

## Customization

### Custom CSS

You can override any theme styles by creating a `static/css/custom.css` file in your site. This file will be loaded after the theme's CSS, allowing you to customize colors, fonts, and other styles.

For example, to customize the color scheme:

```css
/* Light mode colors */
:root {
  --text-color: #333333;
  --link-color: #0d88d8;
  --background: #FFFFFF;
}

/* Dark mode colors */
@media (prefers-color-scheme: dark) {
  :root {
    --text-color: #FFFFFF;
    --link-color: #45c8f7;
    --background: #20232a;
  }
}
```

See the [Micro.blog customization guide](https://mnml.micro.blog/2025/01/23/modifying-the-color-scheme/) for more color variable examples.

## Development

To test the theme locally:

```bash
cd exampleSite
hugo server --themesDir ../..
```

Visit http://localhost:1313

## Differences from Micro.blog Version

This Hugo version differs from the [Micro.blog plugin](https://github.com/jimmitchell/mnml) in these ways:

1. **Configuration**: Uses `hugo.toml` instead of Micro.blog's web UI
2. **Content structure**: Posts go in `content/post/` directory
3. **Platform features**: Some Micro.blog-specific features may not be available
4. **Stub partials**: Includes empty stub files for `microblog_head.html` and `custom_footer.html`

## Special Thanks

Thank you to the following for their **mnml** localization contributions:

- Swedish: [@robertbirming](https://github.com/robertbirming)
- Ukrainian & Russian: [@luxury-format](https://github.com/luxury-format)
- Chinese (Traditional): [@bobbytung](https://github.com/bobbytung)
- Polish: [@bstn](https://micro.blog/bstn)

## License

MIT License - see LICENSE file

## Credits

- Original theme by [Jim Mitchell](https://jimmitchell.org)
- Designed for [Micro.blog](https://micro.blog)
- Original theme: [github.com/jimmitchell/mnml](https://github.com/jimmitchell/mnml)
- Hugo port: [github.com/shawnyeager/mnml-hugo](https://github.com/shawnyeager/mnml-hugo)

## Support the Original Theme

If you like **mnml**, consider supporting the original creator: [Buy Jim a Coffee](https://buymeacoffee.com/jim.mitchell).
