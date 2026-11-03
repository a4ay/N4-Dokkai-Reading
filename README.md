# Dokkai (読解)

Japanese reading-comprehension practice pages. Each page has a reading passage with furigana you can show or hide, and a multiple-choice question that checks your answer and explains it.

The site is plain HTML, CSS and JavaScript with no build step, hosted on GitHub Pages.

## Project structure

```
Dokkai/
├── index.html    Landing page; renders a link for each page listed in pages.js
├── pages.js      The list of page file names (edit this when adding a page)
├── .nojekyll     Tells GitHub Pages to serve the files as-is
└── pages/        One HTML file per reading problem
    └── Problem-01_Jorge-DVD-Return.html
```

## Adding a new page

1. **Create the page in `pages/`.** The easiest way is to copy an existing page and replace the passage, question and options.

2. **Name the file** using this pattern:

   ```
   Problem-<number>_<Title-With-Dashes>.html
   ```

   For example, `Problem-02_Library-Notice.html`. Use two digits for the number (`01`, `02`, … `10`) so the files stay in order in the folder and on GitHub.

3. **Add the file name to `pages.js`:**

   ```js
   const PAGES = [
     "Problem-01_Jorge-DVD-Return.html",
     "Problem-02_Library-Notice.html",   // ← new page
   ];
   ```

   Links appear on the index in the order they are listed here. Each link's text comes from the file name: `Problem-02_Library-Notice.html` is shown as **02 もんだい 2** · Library Notice. A file name that doesn't follow the pattern still gets a link, labelled with the file name minus `.html`.

4. **Check it locally** by opening `index.html` in a browser and clicking the new link.

5. **Commit and push.** GitHub Pages updates the site within a minute or two.

> The index only shows pages listed in `pages.js`. A file in `pages/` that isn't in the list is still published, but nothing on the index links to it.

### Page conventions

When writing a new page, keep these parts from the existing pages so the furigana and quiz work:

- **Furigana:** wrap each kanji word as `<ruby class="furigana-word">漢字<rt>かんじ</rt></ruby>`. Readings are hidden until the word is tapped or clicked, or **Show All** is pressed. When a number changes the reading, put the number inside the ruby: `<ruby class="furigana-word">20日<rt>はつか</rt></ruby>`.
- **Furigana code:** keep the furigana `<style>` and `<script>` block in the page's `<head>` (it starts with `/* Furigana.`). Every page has its own identical copy so that pages don't depend on each other; copy it unchanged from any existing page, and when you change it, change it on every page.
- **Show All / Hide All:** the buttons need `id="showAllBtn"` and `id="hideAllBtn"`.
- **Quiz options:** each answer is an `<li class="option-item">` with `data-correct="true"` on the right answer and `data-correct="false"` on the others.
- **Explanation:** set `explanationText` in the page's script to the explanation shown after an answer is chosen.
- **Relative paths:** pages live in `pages/`, so a link back to the index or to a top-level file needs `../`, for example `<a href="../index.html">`.

## Running locally

Open `index.html` in a browser. No server or install is needed.

## Deploying to GitHub Pages

1. Push this folder to a GitHub repository.
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**, then choose `main` and `/ (root)`.
4. The site will be available at `https://<username>.github.io/<repository>/`.
