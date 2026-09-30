# Tokyo Afterburn — Rusty Cleaner Theme

Synthwave neon night over Tokyo: magenta afterburn glow, electric blue
gridlines and deep indigo panels.

## Structure

```
theme.json          ← metadata (id, name, version, asset paths)
theme.css           ← THE THEME — CSS variables + custom rules
src/assets/images/background.png  ← main window background
src/assets/images/sidebar.png     ← sidebar background
src/assets/icons/brand.png        ← sidebar brand icon (png/jpg/webp only)
src/assets/fonts/                ← optional custom fonts (.ttf/.woff2)
```

## How it works

The `theme.css` is injected verbatim into the app's WebView as a
`<style>` element. It sets the app's CSS variables and can add any custom
CSS — border radii, glows, shadows, animations, anything the app's DOM
supports.

The app's built-in stylesheet uses CSS variables everywhere (no hardcoded
accent colors), so `:root { --cyan: #e71c64 }` repaints the entire UI.

## theme.json contract

Only `id`, `name` and `version` are mandatory:

```json
{
  "id": "tokyo-afterburn",
  "name": "Tokyo Afterburn",
  "version": "1.0.0",
  "author": "leandroruel",
  "description": "…",
  "background": "src/assets/images/background.png",
  "sidebar": "src/assets/images/sidebar.png",
  "brand": "src/assets/icons/brand.png",
  "fonts": []
}
```

- `background` / `sidebar` / `brand` — paths relative to the repo root,
  resolved to absolute and served through the asset protocol as `<img>`
  layers behind the UI.
- `fonts` — array of font file paths; each becomes an `@font-face`.
- `brand` must be a raster format (`.png`/`.jpg`/`.webp`); SVG is
  unreliable through the WebView asset protocol.

## theme.css

Everything visual. The only sanitization: `@import`, `expression()` and
`javascript:` URLs are stripped. Otherwise the CSS is injected as-is.

## Registering

Add the repository URL to `web/themes.json` in
[rusty-cleaner](https://github.com/leandroruel/rusty-cleaner).

## License

MIT
