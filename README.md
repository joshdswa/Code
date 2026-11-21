# Green Book Hymn Finder

A phone app for finding hymns in the Christadelphian Hymn Book (the "Green Book") by number or by words.

**Open it:** https://joshdswa.github.io/green-book/
**Install & share (QR code and steps):** https://joshdswa.github.io/green-book/install.html

## Features

- Type a hymn number, or search any words from the hymn
- Zoom in and out (pinch or buttons); "Fit" shows music and words together
- Swipe left or right for the next or previous hymn
- Favourites and recently opened hymns
- Light and dark mode
- Works offline once installed

## How it works

It is a web app (a plain web page with no build step), hosted free on GitHub Pages.
Each person chooses their own PDF of the Green Book the first time they open it.
The PDF stays on their phone and is never uploaded. **The PDF is not part of this repository.**

| File | What it is |
|---|---|
| `index.html` | The app |
| `hymns.json` | Search index: each hymn's number, first line, section and searchable words |
| `install.html` | Install and share page with a QR code |
| `sw.js` | Offline support |
| `pdf.min.js`, `pdf.worker.min.js` | PDF.js, which shows the PDF pages |
| `qrcode.js` | QR code generator (MIT licence) |
| `manifest.json`, `icon-*.png` | App name and icons for the home screen |

After changing any file, bump `CACHE` in `sw.js` (e.g. `greenbook-v2`) so installed phones pick up the update.
