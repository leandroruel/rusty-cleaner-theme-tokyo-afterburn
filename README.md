# Tokyo Afterburn — Rusty Cleaner Theme

Synthwave neon night over Tokyo: magenta afterburn glow, electric blue
gridlines and deep indigo panels.

## Structure

```
theme.json                        ← the theme manifest (the contract)
src/assets/images/background.png  ← main window background
src/assets/images/sidebar.png     ← sidebar background
src/assets/images/preview.png     ← preview screenshot for the README
src/assets/icons/brand.svg        ← sidebar brand icon
src/assets/fonts/                 ← optional custom fonts (.ttf/.woff2)
```

## theme.json contract

| Field | Type | Maps to |
| ----- | ---- | ------- |
| `colors.background` | CSS color | `--bg` |
| `colors.panel` | CSS color | `--panel` |
| `colors.panel2` | CSS color | `--panel-2` |
| `colors.border` | CSS color | `--border` |
| `colors.text` | CSS color | `--text` |
| `colors.textDim` | CSS color | `--text-dim` |
| `colors.textFaint` | CSS color | `--text-faint` |
| `colors.accent` | CSS color | `--cyan` (primary accent) |
| `colors.accentSecondary` | CSS color | `--pink` |
| `colors.purple` | CSS color | `--purple` |
| `colors.green` | CSS color | `--green` |
| `colors.amber` | CSS color | `--amber` |
| `colors.red` | CSS color | `--red` |
| `colors.orange` | CSS color | `--orange` |
| `colors.blue` | CSS color | `--blue` |
| `background.image` | path | main window background (tinted by `background.tint`) |
| `background.tint` | CSS color | overlay on the background image for readability |
| `sidebar.image` | path | sidebar background |
| `sidebar.tint` | CSS color | overlay on the sidebar image |
| `fonts.text` | path (.ttf/.woff2) | replaces the interface font |
| `fonts.mono` | path (.ttf/.woff2) | replaces the monospace font |
| `icons.brand` | path (.png/.svg) | replaces the sidebar brand icon |

All asset paths are relative to the theme repository root. Only `id`,
`name` and `version` are mandatory — anything omitted keeps the built-in
value.

## Themable component IDs

Structural blocks carry stable IDs so themes or future tooling can target
them: `#app-shell`, `#sidebar`, `#brand-icon`, `#scan-visual`,
`#monitor-bar`, `#scan-button`, `#results-button`.

## Registering

Add the repository URL to `web/themes.json` in the
[rusty-cleaner](https://github.com/leandroruel/rusty-cleaner) repository:

```json
{
  "id": "tokyo-afterburn",
  "name": "Tokyo Afterburn",
  "author": "leandroruel",
  "description": "…",
  "repo": "https://github.com/leandroruel/rusty-cleaner-theme-tokyo-afterburn"
}
```

Users then see the theme under **Settings → Themes**, click
**Download & apply** and Rusty Cleaner clones the repository (public git
repositories only), reads `theme.json` and applies everything.

## License

MIT
