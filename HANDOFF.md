# Green Book Hymn Finder: handoff notes

Written at the end of a cloud session on 21 Nov 2026, to carry on in a local Claude Code session on the PC "Editor".

## Start here: what's left to do

The app is finished and pushed. Only these GitHub settings remain, and the cloud session couldn't reach them. Use Chrome:

1. **Rename the repository:** https://github.com/joshdswa/Code/settings → change the name from `Code` to `green-book` → **Rename**.
2. **Turn on GitHub Pages:** https://github.com/joshdswa/green-book/settings/pages →
   - Source: **Deploy from a branch**
   - Branch: **`ccr-563b9e14-f7hugw`**, folder **/ (root)** → **Save**
3. **Check the live site** after a minute or two:
   - App: https://joshdswa.github.io/green-book/
   - Install and share page (QR code): https://joshdswa.github.io/green-book/install.html
   - Choose the Green Book PDF, search "shepherd", open a hymn, then check zoom, swipe and favourites.
4. **Optional tidy-up:**
   - Make `main` the default branch: create `main` from `ccr-563b9e14-f7hugw`, set it as default in Settings → Branches, and point Pages at `main`.
   - Delete the cloud-only environment "Green Book hymn work (Drive downloads)" in Claude Code environment settings if you won't use it again.

To get the code locally:

```
git clone https://github.com/joshdswa/Code.git green-book    # or .../green-book.git after the rename
cd green-book
git checkout ccr-563b9e14-f7hugw
python -m http.server 8000      # then open http://localhost:8000
```

## Where everything lives

| What | Where |
|---|---|
| The app's code (current version) | GitHub `joshdswa/Code`, soon `joshdswa/green-book`, branch `ccr-563b9e14-f7hugw` |
| Older copy on claude.ai (private) | https://claude.ai/artifact/2BCWM8pvZqrGAkyowZu4ex (version 5). Same app, without the install/share page, install button and offline file. |
| Green Book PDF (original scan, 665 pages, 20 MB) | Google Drive → folder "Green book" → `green_ book.pdf`. Private, never shared. |
| Each user's PDF copy, favourites, recent hymns, settings | On their own phone, in the browser's storage (IndexedDB and localStorage). Never uploaded. |

**The PDF is deliberately not in the repository or on the website.** It's a scan of a copyrighted book. Each person picks their own copy the first time they open the app.

## What the app does

- Look up a hymn by number. The first line shows under the number as you type.
- Search by any words: first lines, verses, titles, tune names, Bible references and book sections. Accents are ignored ("blessed" finds "blessèd").
- The viewer trims white margins. Zoom with a pinch or the − / Fit / + buttons; **Fit** shows the whole hymn, music and words together. The ⇅/⇆ button switches between stacking pages and placing them side by side. Your zoom choice is remembered.
- Swipe left or right for the next or previous hymn. A star (★) adds favourites, and the last 12 hymns opened are listed as recent.
- Light, dark or automatic theme. In dark mode the pages are inverted.
- Installs as an app: Android shows an Install button, and on iPhone use Share → Add to Home Screen. Works offline via `sw.js`.
- The **Share** button opens `install.html`, which has a QR code, a share-link button, and steps for Android, iPhone and the PDF.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app |
| `hymns.json` | Search index, one entry per hymn: `n` number, `f` first line, `t` tune, `s` section, `x` searchable words, `c` = 1 if the words are copyrighted |
| `install.html` | Install and share page with QR code |
| `sw.js` | Offline cache. **Bump `CACHE` (e.g. `greenbook-v2`) whenever you change any file**, or installed phones keep the old version. |
| `pdf.min.js`, `pdf.worker.min.js` | PDF.js, which renders the pages |
| `qrcode.js` | QR generator (qrcode-generator 1.4.4, MIT licence) |
| `manifest.json`, `icon-*.png` | Home-screen name and icons |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |

### How hymns map to PDF pages

- `MAP` in `index.html` gives the first PDF page of each hymn (hymn 1 = page 4), and `END = 633`.
- `START = {35:51, 326:475}` covers the two hymns that begin partway down the previous page.
- There are 438 hymns.

## How the search words were made

1. Machine OCR (Tesseract) of every page, used only as a helper.
2. **Every hymn was transcribed by Claude from the page images.** This included zooming in on the words under the music in anthems.
3. **11 hymns have words still under copyright**: 1, 88, 110, 123, 143, 155, 181, 348, 356, 387, plus one more flagged during transcription. For these the index holds only the first line and a word list, not the lyrics in order. They're still searchable by any word, but results show no preview line.
   - Judgement calls on copyright status: 143 and 155 were flagged; 41, 100, 212, 270, 325 and 343 were left as public domain, because no words copyright is printed.

### Things worth checking against the printed book

- **Anthems where voice parts overlap** (10, 18, 28, 30, 248, 308): the order of the overlapping phrases is a best reading.
- **Misprints kept as printed:** 336 ("We thank, Thee Lord"), 340 ("our's"), 342 v5, 359 ("aweful"). One was silently corrected: 433 ("heen" → "been").
- **Hymns with two tunes** record only the first tune name.

## Housekeeping done during the session

- To read the 20 MB PDF, a **temporary copy** was shared by link, downloaded, then moved to the Drive bin. The original was never shared. Empty the Drive bin if you like.
- The cloud environment "Green Book hymn work (Drive downloads)" was created to allow downloads from Google Drive.

## Ideas not yet done

- A custom web address (e.g. greenbookhymns.com) pointed at GitHub Pages.
- Hymn titles shown in the viewer's top bar.
- A "service list": queue several hymns for a meeting and step through them.
