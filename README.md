# Your Team — Homepage

A single-page marketing site for **Your Team**, a DMV-area home staging, styling,
cleaning, and junk-removal service. Implemented from the Claude Design mockup
`Your Team Homepage.dc.html`.

## Run it

No build step. Just open `index.html` in a browser:

```
start index.html      # Windows
```

Or serve the folder for clean relative paths:

```
python -m http.server 8000
# then visit http://localhost:8000
```

An internet connection is used only to load the Google Fonts
(Libre Caslon Display, Archivo, Instrument Sans).

## Structure

```
index.html      All markup, styles, and JS (self-contained)
assets/         Logo + optimized, orientation-corrected photos
README.md
```

Everything lives in `index.html`:
- **Styles** — an internal stylesheet using CSS custom properties for the
  palette (`--cream`, `--ink`, `--deep`, `--teal`, `--gold`) and fonts.
- **Interactions** (vanilla JS at the bottom):
  - Before/after comparison slider — click or drag anywhere to wipe between
    the empty and staged room (pointer events, works on touch).
  - Mobile hamburger menu.
- **Service-area map** — hand-built inline SVG (no external map dependency).

## Images

The photos in `assets/` were sourced from the originals in `~/Downloads`,
auto-rotated to correct orientation (several iPhone shots carried EXIF
rotation), resized for web, and re-encoded as progressive JPEG. Total ~3.7 MB.

| File | Source | Used for |
|------|--------|----------|
| `logo-mark.png` | logo1.png | Header + footer mark (transparent) |
| `logo-full.png` | Final 2-01.png | Full lockup, transparent (for light backgrounds; not placed on the dark site) |
| `hero.jpg` | IMG_2071 | Hero background |
| `service-staging.jpg` | IMG_1911 | Service 01 — Staging |
| `service-cleaning.jpg` | IMG_4498 | Service 02 — Cleaning |
| `service-junk.jpg` | IMG_1888 | Service 03 — Junk removal |
| `ba-before-v2.jpeg` | IMG_2058 | Before/after — empty room |
| `ba-after-v2.jpeg` | IMG_2074 | Before/after — same room, staged |
| `work-1.jpg … work-7.jpg` | IMG_1895, 4619, 4517, 4681, 4538, 4692, 2071 | Portfolio grid |

### Swapping an image
Drop a replacement into `assets/` with the same filename, or edit the
`src` on the relevant `<img>` in `index.html`. Every image slot has a
branded placeholder that shows automatically if a file is missing, so the
layout never breaks.

## Launch checklist (staging → production)

The site currently carries `<meta name="robots" content="noindex,nofollow">`
so the *preview* URL never becomes the version Google indexes. When the owner
approves and the site moves to its real domain:

1. **Remove the noindex meta tag** in `index.html` (marked with a
   `STAGING ONLY` comment).
2. Replace `REAL-DOMAIN.com` in `sitemap.xml` and `robots.txt`, and make
   `og:image` an absolute URL (`https://real-domain.com/assets/hero.jpg`).
3. Add the real phone/email to the page **and** to the JSON-LD block
   (`telephone`, `email` fields) — they're deliberately omitted while the
   numbers are placeholders.
4. Verify the domain in **Google Search Console** and submit the sitemap —
   this is what gets the site into Google within days instead of weeks.
5. Create/claim a **Google Business Profile** for "Your Team Inc" (owner
   action, needs a real address or service-area + phone). This is the single
   biggest lever for what Google and AI assistants say about the company —
   it will outrank the unaccredited-BBB result for name searches.
6. Put the website link in the Instagram bio (@yourstagingteam) — cross-links
   help Google connect the entity.
7. Optional: test the structured data at https://search.google.com/test/rich-results

Why this fixes the BBB problem: today the BBB listing is nearly the only
content Google has about "Your Team Inc," so searches and AI answers lean on
it. Once the site is live with the `LocalBusiness` JSON-LD (services, areas,
Instagram) plus a Business Profile, Google and AI assistants have a richer,
authoritative source to quote instead.

## Notes
- The design mockup's full-resolution photos could not be pulled through the
  Claude Design MCP (its file-fetch is capped at 256 KB and the originals are
  multi-megabyte iPhone photos), so the photos here were taken from the local
  `~/Downloads` copies instead. The logo mark came through the MCP intact.
- Contact details (`(555) 010-2400`, `hello@yourteam.com`) are placeholders
  from the mockup — replace with the real phone/email before going live.
  Instagram is real: [@yourstagingteam](https://www.instagram.com/yourstagingteam).
- The before/after slider supports keyboard control (Tab to focus, then
  arrow keys; Shift+arrow for bigger steps, Home/End to jump).
- Below-the-fold photos use `loading="lazy"`; favicon and Apple touch icon
  are generated from the logo mark.
