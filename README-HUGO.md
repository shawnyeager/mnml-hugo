# mnml for Hugo

This is a port of the **mnml** theme for use with Hugo (not as a Micro.blog plugin).

## Installation

### Option 1: Git Submodule

```bash
cd your-hugo-site
git submodule add https://github.com/jimmitchell/mnml.git themes/mnml-hugo
```

### Option 2: Clone

```bash
cd your-hugo-site/themes
git clone https://github.com/jimmitchell/mnml.git mnml-hugo
```

### Option 3: Hugo Modules (requires Go)

In your `hugo.toml`:

```toml
[module]
  [[module.imports]]
    path = "github.com/jimmitchell/mnml"
```

## Configuration

Copy the example configuration from `hugo.toml.example` to your site's `hugo.toml` file and customize as needed.

### Basic Configuration

```toml
baseURL = "https://example.com/"
languageCode = "en"
title = "My Blog"
theme = "mnml-hugo"

defaultContentLanguage = "en"

[pagination]
  pagerSize = 20

[taxonomies]
  category = "categories"
  tag = "tags"

[params]
  description = "A minimal, simple and clean blog."
  itunes_description = "A minimal, simple and clean blog."
  theme_seconds = "1"  # Cache busting version
```

### Theme Parameters

All parameters are optional with sensible defaults:

#### Date & Time
- `use_short_date` (boolean) - Use short date format (default: false)
- `show_read_time` (boolean) - Show reading time on posts (default: false)

#### Header & Avatar
- `narrow_header` (boolean) - Use narrow header width (default: false)
- `hide_avatar` (boolean) - Hide site avatar (default: false)
- `custom_avatar` (string) - URL to custom avatar image

#### Home Page
- `home_category` (string) - Filter by category (comma-separated)
- `pinned_category` (string) - Category for pinned post
- `show_full_post` (boolean) - Show full posts vs summaries (default: false)

#### Category/Archive Pages
- `category_full_post` (boolean) - Show full posts on category pages (default: false)
- `show_categories` (boolean) - Show category list on archives (default: false)
- `show_category_count` (boolean) - Show post counts (default: false)

#### Photos
- `photos_category` (string) - Filter photos by category
- `all_formats` (boolean) - Show all image formats (default: false)
- `masonry_layout` (boolean) - Use masonry layout (default: false = grid)
- `full_width_photos` (boolean) - Use wider photos layout (default: false)
- `single_image` (boolean) - Show only first image (default: false)

#### Search
- `search_results` (integer) - Number of search results (default: 5)

#### Footer
- `hide_copyright` (boolean) - Hide copyright notice (default: false)
- `footer_rss` (boolean) - Add RSS link (default: false)
- `hide_credit` (boolean) - Hide theme credits (default: false)

#### Advanced
- `fediverse_creator` (string) - Fediverse creator tag (e.g., @user@instance.social)
- `archive-paginate` (integer) - Archive page size (default: 30)
- `plugins_js` (array) - Additional JavaScript files to load

## Creating Content

### Regular Posts

Create posts in `content/posts/`:

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

### Search Page

Create a search page with the built-in shortcode:

```markdown
---
title: "Search"
---

{{< search >}}
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

## Development

To test the theme locally:

```bash
cd exampleSite
hugo server --themesDir ../..
```

Visit http://localhost:1313

## Differences from Micro.blog Version

This Hugo version differs from the Micro.blog plugin in these ways:

1. **Configuration**: Uses `hugo.toml` instead of Micro.blog's web UI
2. **Missing partials**: Includes stub files for `microblog_head.html` and `custom_footer.html`
3. **Platform features**: Some Micro.blog-specific features may not be available
4. **Layouts**: Includes Micro.blog-specific layouts (can be ignored)

## License

MIT License - see LICENSE file

## Credits

- Original theme by [Jim Mitchell](https://jimmitchell.org)
- Designed for [Micro.blog](https://micro.blog)
- Ported to Hugo
