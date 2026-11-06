# Artificial Studios website

AI-native filmmaking company, Brighton · London.

- **Live site:** https://artificialstudios.co.uk
- **GitHub Pages copy:** https://greyent.github.io/artificial-studios-site/
- **Contact:** hello@artificialstudios.co.uk

Static one-page site: one `index.html`, no build step, no framework.

_Last updated 5 November 2026._

## Page sections

| Section | Video |
|---|---|
| Hero showreel | Loops `environments-loop-061126`, `elgar-crowd-test`, `originals-sizzle-061126`, `generate-reel` and `werewolf` (every video on the page except Mr James and the Academy background), in full and shuffled, after the `as-logo` bumper |
| About / How we work | `how-we-work-reel` |
| Originals | `originals-sizzle-061126` |
| Selected work 01 / Micro-drama: Mr James Ep.2 "Ecstasy of Gold" | `mr-james-ep2-half` |
| Selected work 02 / Generated environments | `environments-loop-061126` |
| Selected work 03 / Generated people and crowds | `elgar-crowd-test` |
| Capabilities: Generate | `generate-reel` |
| Capabilities: Augment | `werewolf` |
| Academy | `ambient/contact-hero` |
| Contact | Email only |

Videos are in `assets/video/work/` (720p H.264, faststart). Poster frames with the same names are in `assets/img/work/`. Every video box plays on hover and opens a lightbox with sound on click. Each box has its own sound toggle and play bar.

Older clips still in `assets/video/` are no longer used by the page.

## Two versions of the page

- **`index.html`** loads assets with relative paths. GitHub Pages serves this one.
- **`webhost/index.html`** is the same page, but it loads every video and image from `greyent.github.io`. This is the file for **artificialstudios.co.uk**: upload it to the host's `/httpdocs` folder as `index.html`. Only that one small file has to go up, because the videos stay on GitHub.

Keep both files in sync on every change.

## Updating

1. Edit `index.html` and make the same change in `webhost/index.html`.
2. Commit and push to `main`. GitHub Pages redeploys in about a minute.
3. Upload `webhost/index.html` to the real domain as `index.html`.
