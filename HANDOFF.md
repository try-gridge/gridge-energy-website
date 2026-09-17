# Handoff — pushing this to the repository

These files are the **v4 website** for `try-gridge/gridge-energy-website`, delivered as a plain
folder. Nothing here needs a build step.

## What you are receiving

```
index.html          the website (static, no build)
support.js          runtime the page requires — do not edit
assets/             the 9 photos/screenshots + logo files the page loads
data/               anonymized meter series + alarm log for the live sections
src/                authoring copy of index.html (design-tool version, same markup)
docs/               DEPLOYMENT, CONTENT, DATA, DESIGN-SYSTEM
README.md           architecture, page map, interactive behavior, editing checklist
CHANGELOG.md        what changed in v4
.gitignore, .nojekyll
```

## Putting it on a branch

```bash
git clone https://github.com/try-gridge/gridge-energy-website.git
cd gridge-energy-website
git checkout -b website-v4-docs

# copy the unzipped folder's contents over the working tree
cp -R /path/to/unzipped-repo/. .

git add -A
git commit -m "Website v4: nine-section layout, page-to-page scrolling, full docs"
git push -u origin website-v4-docs
```

Then open a pull request against `main`.

## Before merging, please check

- Serve over HTTP (`python3 -m http.server 8080`) rather than opening `index.html` directly —
  from `file://` the JSON fetches are blocked and the live sections render empty.
- `data/siddique_series.json` and `data/alarms.json` return 200.
- Arrow keys and the bottom-right arrows advance exactly one section and center it.
- Tapping a circuit in **Live Control** updates Total Active and the insight line.
- Check at 1440px, 820px and 390px — no horizontal scrollbar, no phone screenshot spilling out.

## Notes for review

- **Styling is inline by design.** There is no stylesheet and no CSS classes. The only global CSS
  is in the `<helmet>` block at the top of the file: font links, `@keyframes`, body resets, and the
  responsive `@media` rules that key off `data-*` attributes.
- **Scroll-snap is deliberately absent.** Paging is owned by JS (`setupPaging` / `gotoPage` in the
  logic class at the bottom of the file); CSS snap fought it and caused double-jumps.
- **`index.html` and `src/…dc.html` are the same markup.** If you edit one, mirror the other, or
  drop `src/` if the team does not use the design tool.
- **Data and imagery are company material** — anonymized meter export and product photography.
  Keep the repository private unless that has been cleared.

Full detail on each of these is in `README.md` and `docs/`.
