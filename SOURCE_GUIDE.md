# Editing the portfolio

Edit `src/`, then compile it with:

```sh
npm run build
```

Only Node.js is required. There are no dependencies to install. On Windows, you can use `node scripts/build.mjs` directly if PowerShell blocks npm.

The build writes the root `index.html`. Do not edit that generated file directly: your changes would be overwritten. Commit it together with your source changes so GitHub Pages continues serving the repository without a custom deployment workflow.

## Where to edit

| File or folder | Content |
| --- | --- |
| `src/index.html` | Page shell, metadata, and section order |
| `src/partials/header.html` | Brand and navigation |
| `src/partials/footer.html` | Footer |
| `src/sections/hero/index.html` | Introduction and portrait |
| `src/sections/highlights.html` | Achievement summary |
| `src/sections/research/` | Section layout and one file per research entry |
| `src/sections/projects/` | Section layout, featured projects, and archive cards |
| `src/sections/experience/` | Section layout, individual roles, and earlier experience |
| `src/sections/about/index.html` | Biography, education, and awards |
| `src/sections/skills/index.html` | Skills |
| `src/sections/contact/index.html` | Contact links |
| `assets/css/portfolio.css` | Shared styles |
| `assets/Resume_JiaXinChen.pdf` | Downloadable resume |
| `projects/` | Existing standalone project reports |

Each section’s `index.html` controls its internal layout and entry order.

## Add or reorder an entry

1. Copy a similar entry into a new file, such as `src/sections/experience/new-role.html`.
2. Edit its text and links.
3. Add an include in `src/sections/experience/index.html` where it should appear:

```html
<!-- include: sections/experience/new-role.html -->
```

4. Run the build.

Includes are relative to `src/`, support nesting, and appear in exactly the order written. Files are included only when referenced. Move an include to reorder content, or remove the include to hide it.

Asset URLs are relative to the generated root homepage: use `assets/...` and `projects/...`, without extra `../` prefixes.

To add an entire section, create its file and include it from `src/index.html`; add its anchor to `src/partials/header.html` if it belongs in navigation.

## Check the output

```sh
npm run check
```

Or run `node scripts/build.mjs --check`. This verifies that the generated homepage matches the source. Missing files, circular includes, and includes outside `src/` fail the build. The output is written only after all includes resolve successfully.

Search `src/` for `To add` to find unfinished content. See [PORTFOLIO_NOTES.md](PORTFOLIO_NOTES.md) for content suggestions.
