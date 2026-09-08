# Artificial Studios — new site, ready to deploy

Static site. No build step, no framework, no server-side code required. Any
web host can serve this folder as-is — just upload everything in `site/` to
the web root (or a subfolder first if you want to preview before going live).

**Easiest upload path:** one zip sits next to this folder —
`../artificial-studios-site.zip` (~345MB, everything below included). Most
hosts (cPanel's File Manager, Plesk, etc.) let you upload that single file
and extract it server-side, which is far faster than pushing 70+ individual
files — some 15–40MB each — over FTP/SFTP or a web upload form one at a
time. If your host doesn't support server-side extraction, fall back to
uploading `site/`'s contents directly (SFTP handles the total size fine,
it's just slower). Either way, unused dead weight has already been trimmed —
an orphaned 23MB reel file that nothing referenced any more is gone.

## What's in here

```
index.html           the whole site (one page, sections: hero, work, services,
                      process, studio, academy, contact)
assets/img/           real photos + the new brand mark, already wired in
assets/img/og-image.jpg  1200×630 link-preview crop (see "SEO" below)
assets/img/work/      poster frames for the self-hosted work-grid clips
assets/video/         as-logo.mp4 (animated logo bumper) and the hero-reel
                      source clips in hero/ and ambient/ — all already wired in
assets/video/work/    14 real clips, transcoded for the web (see below)
robots.txt            already correct for this site
sitemap.xml           one URL — it's a one-pager now
.htaccess             301s from every old page to the new page, for Apache/cPanel hosts
_redirects            same 301s, for Netlify — harmless if you're not on Netlify
site.webmanifest      favicon/home-screen icon config
```

## Work-grid videos are self-hosted, not YouTube embeds

14 of the work-grid tiles play your own clips directly — hover plays a muted
preview, click opens the full video with sound in an on-page lightbox. No
YouTube dependency for these. The files came from your Dropbox uploads
("WEBSITE VIDEOS 09 2026") and were transcoded down from ~700MB of source
footage to ~84MB total (H.264, capped at 1280px on the long edge, CRF 26) —
small enough to actually hand over and host. A few names got tightened up
from the raw filenames (e.g. "NAILED SCENE 1 CUT 1 APL 2026.mp4" → the title
card in the footage itself, "The Big Jeez") — check `assets/video/work/` and
the tile captions in `index.html` if anything should be relabelled before
launch. Two source clips were dropped as near-duplicates of ones already
in the grid (a second angle on the same VFX creature shot, a second near-
identical Mr James teaser) — the originals are still in your Dropbox if you
want the other angle in instead.

One thing I couldn't fully confirm from this end: the hover-preview/lightbox
JS is correct and standards-compliant (verified the right file resolves,
requests fire, no console/media errors), but the sandboxed browser I test
in here can't actually buffer *any* video — including an unrelated public
test file — so I could not visually confirm playback end-to-end. Load the
page in a normal browser once it's live (or just open `site/index.html`
through a real local server, not a file:// link) and check that hovering a
work tile plays a preview and clicking it opens the lightbox with sound.

## New: animated logo bumper on the hero

`assets/video/as-logo.mp4` (from your Dropbox, "AS LOGI 1.mp4", transcoded down
from 12.8MB to ~2.1MB) now plays over the reel on page load — the "ARTIFICIAL
STUDIOS / A FILM BY…" sting — and fades out on its own once it finishes,
revealing the reel underneath. It's muted (autoplay requires that), plays
once (not looped), and doesn't touch the "SOUND OFF" control, which still only
governs the reel. If you'd rather it loop, or sit somewhere other than over
the reel, say so.

## One thing that needs doing before this fully "just works"

**Contact form.** The form on the page tries to submit itself first; if
that fails (which it will, until one of these is wired up) it falls back to
opening a normal email draft — so it never dead-ends, it's just not silent
yet. Pick one:
- **Netlify** — if this is going on Netlify, the `data-netlify="true"` attribute
  already on the form is all it needs. Nothing else to do.
- **Anywhere else** — point the form at a form backend. Formspree
  (formspree.io) is the fastest zero-code option: sign up, drop their form
  endpoint into the `<form>` tag's `action`, done. Or wire it to a one-line
  PHP `mail()` script if the host runs PHP. Either way, the email address to
  send to is `info@artificialstudios.co.uk`.

## Things worth knowing, not blocking launch

- **Social links removed, not filled with placeholders.** The old site
  didn't expose real Instagram/YouTube/LinkedIn URLs anywhere I could
  verify, so rather than invent handles I left them out of the footer
  (only the real, confirmed `planetspectrum.tv` link is there). Add real
  ones when you have them — footer "Elsewhere" column.
- **"Privacy" in the footer legal line has no page yet** — either link it to
  a real privacy policy or drop it.
- **Work grid only has real, verifiable pieces** — 22 tiles total: 8 from
  what's actually credited on the current site (Coca-Cola, BMW, L'Oréal, the
  two trailers, the True Crime reel, the product showreel, PHENOMX/Planet
  Spectrum) plus 14 self-hosted from your Dropbox upload (see "Work-grid
  videos" above). No placeholder "Project title / Client name" tiles were
  left in — add more as real work ships. Several are explicitly captioned
  as tests/pitch material rather than finished client work, matching how
  they're actually described in the source footage/filenames — reword any
  that should read as finished deliverables instead.
- **Emmy category** is filled in as "The Ascent of Money", pulled from the
  team page bio. Flag if that's not the intended credit.
- **Client-login footer link** still points at
  `artificialstudios.co.uk/private/` on the current host — leave that
  domain/path alone when migrating, or update the link if it moves.

## SEO carried over

Title, meta description, canonical, Open Graph/Twitter card tags, and a
basic Organization/Person JSON-LD block (Emmy, founder, contact) are all in
`<head>`. `robots.txt` and `sitemap.xml` are set for the new one-page
structure; the old URLs 301 to the right section of the new page instead of
404ing, so any existing backlinks/search rankings carry across.

**Just added:** the link-preview image (what shows up when the URL is
shared on Slack, iMessage, LinkedIn, etc.) was pointing straight at
`dtfrontpage2.jpg` — a tall 1200×1402 portrait — so most platforms would
crop it awkwardly to their expected ~1.91:1 shape. Cropped a proper
1200×630 version (`assets/img/og-image.jpg`, face and shoulders framed
correctly, ~32KB) and pointed `og:image`/`twitter:image` at that instead,
plus added the `og:image:width`/`height`/`alt` tags that were missing. The
meta/OG/Twitter descriptions were also trimmed to ~150 characters each (the
old one ran to 187, past where Google/social previews start truncating
mid-sentence) and made consistent across all three tags, and the JSON-LD
block now carries a matching `description` field it was missing before.
`sitemap.xml` now also carries a `lastmod` date.

Not done, and worth a look when there's real usage data: title/description
are currently generic-studio copy — once you know what people are actually
searching to find you (own name, a specific past project, "AI VFX studio"),
tightening the title tag around that phrase would help more than any
markup change. Structured data is Organization-level only; adding
`VideoObject` markup for a couple of flagship work pieces is a further step
if video search traffic matters, not done here since it's speculative
without knowing which pieces you'd want surfaced that way.

## Local preview

From inside `site/`:
```
python3 -m http.server 8000
```
then open `http://localhost:8000`.
