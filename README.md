# atonal440.net

The personal site of Vee Loring. Static HTML on GitHub Pages. No build step,
no dependencies — edit a file, commit, done.

Index pages are lists of links, and `style.css` is ~45 lines and the whole
template for them. Pieces don't use it.

    index.html          the list
    style.css
    404.html
    favicon.svg
    work/               résumé
    photographs/        drop files in photographs/plates/
    writing/            list of collections
      invisible_networks/2026/algossamer/
      invisible_networks/2026/bug_1729/
      dollposting/      index, then one page per piece

## The one rule

A piece is a self-contained artifact. All of its CSS is inline or beside it, it
does not load `style.css`, it gets whatever palette, typeface and layout the
writing asks for, and **it carries no navigation of any kind** — no header, no
exit link, nothing pointing back. Anyone curious can walk up the tree.

To add one: write the page, add one `<li>` to its collection index.

## The two collections

*Invisible Networks* pieces are found documents — each wears the skin of the
system that produced it.

*Dollposting* pieces are one-off treatments built to fit the writing, each
signed and dated at the foot.

## Conventions for a new piece

- Body text and small metadata clear 4.5:1 against whatever is behind them.
  Display type of 24px and up can go down to 3:1.
- Decorative marks, figures and ornaments get `aria-hidden="true"`. Anything
  that carries meaning gets an `aria-label` describing it.
- Uppercase is `text-transform`, never typed into the markup, so copied text
  keeps the real casing.
- Every page: `lang`, `charset`, `viewport`, `title`, favicon link.
- Prose text is verbatim. Straighten quotes to curly, nothing else — and never
  let CSS stand in for a real character (padding may widen a space, not
  replace it).
- Sizes are clamps and `em`, not breakpoints. Scale on `vmin` so a short
  landscape window shrinks too. Hold the measure with
  `calc(<n>ch + 2 * var(--pad))`. Centre with auto block margins, never
  `align-items: center`, which strands the top of tall content off-screen.
- No animation anywhere on the site, so nothing needs a reduced-motion
  fallback. If you add some, it will.
