# Mathematics Course Materials — site source

This repository is the entire website. It is a **plain static site** — just
HTML, CSS, and JavaScript, no build step — so Cloudflare Pages can deploy it
directly with zero configuration. Every time you push changes to this repo
(or upload files through the GitHub website), Cloudflare automatically
rebuilds and republishes the live site within about a minute.

## Folder structure

```
index.html                      ← homepage
assets/css/style.css            ← one shared stylesheet used by every page
calculus/index.html             ← Calculus section landing page
calculus/pdfs/                  ← put Calculus PDFs here
calculus/interactive/           ← put Calculus interactive .html pages here
linear-algebra/  ...            ← same pattern
statistics/       ...           ← same pattern
resources/         ...          ← same pattern (general / cross-topic material)
```

Each topic section works the same way, so once you've added one PDF and one
interactive page, you know how to add all of them.

## Adding a new PDF

1. Put the PDF file in the right `pdfs/` folder, e.g. `calculus/pdfs/03-related-rates.pdf`.
   Keep the file name simple — letters, numbers, and hyphens, no spaces or accents.
2. Open that section's `index.html` (e.g. `calculus/index.html`) in a text editor.
3. Find the `<ul class="resource-list">` under **"Downloadable Notes (PDF)"**.
4. Add a new `<li>` following this pattern (copy, paste, edit the two bold-ish parts):

   ```html
   <li>
     <a class="resource-link" href="pdfs/03-related-rates.pdf">
       <span class="resource-icon pdf">PDF</span>
       <span class="resource-text">
         <span class="title">Related Rates — Notes</span>
         <span class="desc">Worked examples and practice problems.</span>
       </span>
     </a>
   </li>
   ```

   Change `href` to your file's path, and the `title`/`desc` text to describe it.
   If the section still shows the empty-note `<li>` (the italic "No PDFs
   posted yet…" line), you can delete that `<li>` once you've added a real one.
5. Save, then upload/commit the changed files to GitHub (see the main
   setup guide for exact steps). The live site updates automatically.

## Adding a new interactive page

1. Duplicate `calculus/interactive/surface-explorer.html` into the right
   `interactive/` folder and rename it, e.g. `linear-algebra/interactive/eigenvectors.html`.
2. Edit the file:
   - Update the `<title>` and the breadcrumb text.
   - Update the explanation text and LaTeX between `$...$` (inline) or
     `$$...$$` (display) — KaTeX renders it automatically.
   - Update the JavaScript at the bottom to plot your own function/data with
     Plotly (`type: "surface"` for 3D surfaces, `type: "scatter3d"` for
     points/curves, `type: "scatter"` for 2D plots). Rotation and zoom are
     built into every Plotly 3D plot automatically — you don't need to add
     that yourself.
   - Keep the relative links at the top (`../../assets/css/style.css`,
     `../../index.html`, etc.) — they're what make the shared header/footer
     and styling work from inside an `interactive/` subfolder.
3. Open that section's `index.html` and add a matching `<li>` under
   **"Interactive Pages"**, same pattern as the PDF one above but pointing to
   your new file, e.g. `href="interactive/eigenvectors.html"`.
4. Upload/commit to GitHub. The live site updates automatically.

## Adding a whole new topic section (beyond the initial four)

1. Duplicate an existing topic folder (e.g. `statistics/`) and rename it,
   e.g. `differential-equations/`.
2. Inside the new folder's `index.html`, update the `<title>`, `<h1>`, and
   breadcrumb text, and clear out the example list items.
3. Add a link to the new section in the navigation menu — it appears near
   the top of every page inside `<nav>...</nav>`. Add one line like:

   ```html
   <a href="../differential-equations/index.html">Differential Equations</a>
   ```

   (Adjust the number of `../` to match how deep the current page is — the
   homepage `index.html` uses no `../`, section pages use one, interactive
   pages use two.)
4. Add a matching topic card on the homepage (`index.html`) inside
   `<div class="topic-grid">`, copying one of the existing `<a class="topic-card">` blocks.

## Local preview (optional)

You don't need this to publish — Cloudflare handles that — but if you want
to preview changes on your own computer before uploading, open a terminal in
this folder and run:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000` in your browser.
