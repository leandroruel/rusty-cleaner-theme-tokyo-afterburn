# Tokyo Afterburn — Rusty Cleaner Theme

Synthwave neon night over Tokyo: magenta afterburn glow, electric blue
gridlines and deep indigo panels.

## Structure

```
theme.json          ← metadata: id, name, version, brand icon, fonts
theme.css           ← THE THEME — CSS variables + custom rules + backgrounds
src/assets/images/background.png
src/assets/images/sidebar.png
src/assets/icons/brand.png
src/assets/fonts/               ← optional custom fonts (.ttf/.woff2)
```

## How it works

The `theme.css` is injected verbatim into the app's WebView. It sets
CSS variables, custom rules and references images through the
`{{THEME_ROOT}}` placeholder — the app replaces it with the asset
protocol URL of the theme's installation directory, so any file in the
repo is referenceable.

The app's built-in stylesheet uses CSS variables everywhere (no hardcoded
accent colors), so `:root { --cyan: #e71c64 }` repaints the entire UI.

## theme.json contract

Only `id`, `name` and `version` are mandatory. `brand` and `fonts` are
optional — omit them if the theme doesn't need them:

```json
{
  "id": "tokyo-afterburn",
  "name": "Tokyo Afterburn",
  "version": "1.0.0",
  "author": "leandroruel",
  "description": "Synthwave neon night over Tokyo.",
  "brand": "src/assets/icons/brand.png",
  "fonts": []
}
```

| Field | Purpose |
| ----- | ------- |
| `id` | Unique identifier; also the installation directory name |
| `name` | Displayed in Settings → Themes |
| `version` | Displayed next to the name |
| `author` | Displayed in the theme card |
| `description` | Displayed in the theme card |
| `brand` | Path to a raster icon (`.png`/`.jpg`/`.webp`); swaps the sidebar brand icon. SVG is unreliable through the WebView asset protocol |
| `fonts` | Array of font file paths; each becomes an `@font-face` |

Background and sidebar images are **not** declared in `theme.json` — the
CSS references them directly via `{{THEME_ROOT}}`.

## theme.css

Everything visual. The only sanitization: `@import`, `expression()` and
`javascript:` URLs are stripped.

**Variables** (repaint the entire built-in UI):

```css
:root {
  --bg: #080818;
  --panel: rgba(21, 14, 39, 0.88);
  --panel-2: rgba(33, 24, 52, 0.85);
  --border: #2a1f4a;
  --text: #eee6f8;
  --text-dim: #a89fc4;
  --text-faint: #6f6790;
  --cyan: #e71c64;
  --pink: #2a67bb;
  --purple: #9e4e86;
  --green: #4ecfa8;
  --amber: #e8b849;
  --red: #ff3b5c;
  --orange: #e87a3e;
  --blue: #3a6fd8;
}
```

**Backgrounds** (any file in the repo, via the placeholder):

```css
body {
  background-image:
    linear-gradient(rgba(8,8,24,0.55), rgba(8,8,24,0.55)),
    url("{{THEME_ROOT}}/src/assets/images/background.png");
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

.sidebar {
  background-image:
    linear-gradient(rgba(15,10,30,0.60), rgba(15,10,30,0.60)),
    url("{{THEME_ROOT}}/src/assets/images/sidebar.png");
  background-size: cover;
}
```

**Custom rules** (borders, glows, radii, anything):

```css
.panel { border-radius: 6px; backdrop-filter: blur(2px); }
.scan-ring { filter: drop-shadow(0 0 18px var(--cyan)); }
.nav-item.is-active { box-shadow: inset 2px 0 0 var(--cyan); }
```

## Registering a theme

Add the repository URL to `web/themes.json` in
[rusty-cleaner](https://github.com/leandroruel/rusty-cleaner):

```json
[
  {
    "id": "tokyo-afterburn",
    "name": "Tokyo Afterburn",
    "author": "leandroruel",
    "description": "…",
    "repo": "https://github.com/leandroruel/rusty-cleaner-theme-tokyo-afterburn"
  }
]
```

Users then see the theme under **Settings → Themes**, click
**Download & apply** and Rusty Cleaner clones the repository, reads
`theme.json`, resolves `{{THEME_ROOT}}` in the CSS and injects it.

## License

MIT
