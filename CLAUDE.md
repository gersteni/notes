# notes.idoh.com

This is the source for **notes.idoh.com**, a collection of interlinked notes hosted on GitHub Pages via Jekyll.

## How it works

- The repo lives at `github.com/gersteni/notes` and is deployed automatically by GitHub Pages.
- The custom domain `notes.idoh.com` is configured via the `CNAME` file.
- Jekyll converts the `.md` files to `.html` at build time. There is no theme gem; all styling is custom.

## Directory structure

```
├── _config.yml          # Jekyll config (kramdown, layout defaults)
├── _layouts/
│   ├── default.html     # Base HTML shell, loads style.css
│   ├── home.html        # Index page: site header + alphabetical page list
│   └── page.html        # Content pages: breadcrumb nav + article
├── style.css            # All styling (Georgia serif, 650px max-width, minimal)
├── index.md             # Home page (uses `home` layout)
├── CNAME                # Custom domain: notes.idoh.com
├── *.md                 # Content notes (each uses `page` layout by default)
└── README.md            # GitHub repo readme (not rendered by Jekyll)
```

## Adding a new note

1. Create a file like `My New Note.md` in the root directory.
2. Add Jekyll front matter at the top with a `permalink` that is the lowercase, hyphenated version of the title:
   ```
   ---
   title: My New Note
   permalink: /my-new-note.html
   ---
   ```
3. Write content below the front matter. Do NOT include a `# Title` heading — the `page` layout renders the title from front matter automatically.
4. The note will automatically appear in the index page list (sorted alphabetically).

## Linking between notes

Use standard markdown links with the target page's `permalink` value:

```markdown
[link text](/my-other-note.html)
```

**Important:**
- Links must use the permalink path (lowercase, hyphens, `.html`), not the source filename.
- Every content file has a `permalink` in its front matter — always link to that value.
- Use absolute paths starting with `/` (e.g., `/mece.html`, not `MECE.html` or `./MECE.html`).

## Layouts

- **`default.html`** — bare HTML wrapper. Loads `style.css`. All other layouts inherit from this.
- **`home.html`** — the index page. Shows "idoh.com" / "Notes and posts." header, then lists all pages with a `title` in their front matter (sorted alphabetically, excluding the index itself).
- **`page.html`** — content pages. Shows a breadcrumb (`notes > Page Title`), then an `<h1>` with the title, then the article body.

Layout assignment is handled in `_config.yml` defaults: all files get `page` layout, except `index.md` which gets `home`.

## Styling

`style.css` controls all visual design. Key properties:
- Georgia serif font, 18px base, 1.6 line-height
- 650px max-width, centered
- Links: blue (`#07c`), visited: dark red (`#941352`)
- Breadcrumb: small gray text with `>` separator
- No nav bar, no sidebar, no footer — content only

## Things to watch out for

- **Front matter is required.** Jekyll will not process a `.md` file without `---` front matter at the top. Files without it (like `README.md`) are ignored.
- **Title in front matter, not in body.** The layout renders `<h1>{{ page.title }}</h1>`, so a `# Title` in the markdown body would create a duplicate heading.
- **Link format.** Always use the permalink path (`/lowercase-hyphens.html`), not the source filename.
- **The `.gitignore` excludes `.png` files.** Screenshots and images are local-only and not committed.
- **This is also an Obsidian vault.** The `.obsidian/` directory is gitignored. The notes can be edited in Obsidian, but Obsidian's `[[wikilink]]` syntax is not used — standard markdown links are used instead so Jekyll can process them.
