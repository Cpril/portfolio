# Editing the portfolio

Each project, research entry, and experience has a folder under `src/content/` containing its text and pictures:

```text
src/content/projects/course-advisor/
  entry.json             Title, category, result, optional cover image
  description.md         The text you write
  course_advisor.png     Picture belonging to this project
```

Research lives in `src/content/research/`, experience in `src/content/experience/`, and earlier projects in `src/content/projects/archive/`. Keep each entry’s pictures in its own folder. Shared assets contain only the homepage stylesheet, portrait, and resume.

## Write descriptions in Markdown

For example, edit `description.md`:

```markdown
### Motivation
I wanted to help students find courses that fit their interests.

### My contribution
I built **tool calling** and a queryable catalog, with *multilingual* support.

- Explain an important technical choice.
- Describe the evaluation and its limitations.

### Results
Summarize what you measured or learned.

![An example conversation](course_advisor.png)

[View code](https://github.com/Cpril/course_advisor_bot_2)
```

Markdown supports headings, bold, italic, lists, quotes, links, images, code blocks, and tables. Raw HTML is also supported when needed. Image and file links are relative to the Markdown file’s folder; the compiler rewrites them for the generated homepage. Keep homepage descriptions brief, since all this text appears in its card.

If a project has no public link, simply omit it. Add only information and findings you are allowed to share. Images are optional; put new pictures beside `description.md` and reference them there. To display a cover image, set `image` and `imageAlt` in `entry.json`. Avoid referencing the same image in both places unless you want it displayed twice.

## Metadata and order

`entry.json` controls the card’s title, dates, type, and other short labels. Keep valid JSON: double quotes and no trailing commas. The optional `todo` field displays a visible “To add” reminder; remove it when complete.

Section layout and order remain in `src/sections/<section>/index.html`. An entry is included with:

```html
<!-- include: content/projects/course-advisor/entry.json -->
```

Move the include to reorder entries. Remove it to hide an entry without deleting its files. To add a new entry, copy a similar folder, edit its metadata and Markdown, then add its include. New folders are not included automatically.

## Build and check

Install the pinned Markdown compiler once after cloning:

```sh
npm ci
```

After editing:

```sh
npm run build
npm run check
```

On Windows, use `npm.cmd` if PowerShell blocks `npm.ps1`. After dependencies are installed, you can also run `node scripts/build.mjs` directly.

The generated root `index.html` continues to work with GitHub Pages. Commit it along with source changes and colocated pictures. Do not edit it directly; rebuilding overwrites it. The build checks missing cover images, missing includes, and circular includes. The check command verifies that output matches source.

## Other sections

| Location | Purpose |
| --- | --- |
| `src/index.html` | Page metadata and section order |
| `src/partials/` | Header, navigation, footer |
| `src/sections/hero/` | Introduction and portrait layout |
| `src/sections/about/` | Biography, education, awards |
| `src/sections/skills/` | Skills |
| `src/sections/contact/` | Contact links |
| `assets/css/portfolio.css` | Shared styling |
| `projects/` | Existing standalone project reports |

Other sections can also include Markdown files using `<!-- include: sections/about/description.md -->`. Include paths are always relative to `src/`; asset links inside Markdown are relative to that Markdown file.

Search `src/content/` for `todo` to find unfinished entry details. See PORTFOLIO_NOTES.md for content suggestions.
