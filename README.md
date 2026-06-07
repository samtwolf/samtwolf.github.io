# Personal website — Samuel Wolf

A hand-coded static site. No build tools, no frameworks, nothing to install. Layout is a sticky
**left sidebar** (name, photo, bio, contact links) plus a **main column** of "Working Papers" and
"Other Writing" entries.

Files:

| File | What it is |
|---|---|
| `index.html` | The whole page (sidebar + Working Papers + Other Writing). |
| `style.css` | All styling. Colours/spacing live in the `:root` block at the top. |
| `assets/` | `headshot.jpg`, `favicon.svg`, and (when ready) `cv.pdf`, `governor.pdf`. |

To edit: open the folder in **VS Code** (`code "…/website"`), change the file, save, refresh the browser.

---

## Editing the page (`index.html`)

**Sidebar** (top of `<body>`):
- **Name** — the `<h1 class="name">`.
- **Photo** — `assets/headshot.jpg`. Replace that file to change it.
- **Bio** — the `<p class="bio">` paragraph.
- **Contact links** — email (shown as `swolf [at] mit [dot] edu`), CV (→ `assets/cv.pdf`), GitHub,
  LinkedIn. Edit the `href`s to change them.

**Main column** — each item is one `<article class="entry">` block:

```html
<article class="entry">
  <p class="entry-title"><a href="…">Title</a> (Year)</p>
  <p class="entry-meta">Date or venue</p>
  <details class="abstract">
    <summary>Abstract</summary>
    <p>Abstract text…</p>
  </details>
</article>
```

- To add an item, copy one `<article class="entry">…</article>` block.
- The **"+ Abstract"** toggle is a native HTML `<details>` element — no JavaScript.
- The CV link and the governor-paper link point to `assets/cv.pdf` and `assets/governor.pdf`; they
  start as 404s and work once those PDFs are added to `assets/`.

---

## Unlisted (not indexed)

`index.html` includes `<meta name="robots" content="noindex, nofollow">`, so search engines won't list
the site — it's reachable only by people you give the link to. To make it publicly discoverable later,
delete that one line.

## Preview locally

```sh
python3 -m http.server 8000
```

then open <http://localhost:8000>. Ctrl-C to stop.

## Hosting (GitHub Pages, free)

Lives on the **personal** github.com account (`samtwolf`), repo `samtwolf.github.io`, served at
`https://samtwolf.github.io/`. To redeploy after edits: `git add . && git commit -m "Update" && git push`.

### Custom domain — samueltwolf.com (when ready)

`og:url` is already set to `https://samueltwolf.com/`. To switch the live site to the domain:

1. Register **samueltwolf.com**.
2. Add a file named `CNAME` here containing one line: `samueltwolf.com`.
3. In the registrar's DNS, add:
   - Four **A** records, host `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - One **CNAME** record: `www` → `samtwolf.github.io`
4. Repo **Settings → Pages → Custom domain** → `samueltwolf.com` → Save; then tick **Enforce HTTPS**.

The free `samtwolf.github.io` URL keeps working alongside the custom domain.
