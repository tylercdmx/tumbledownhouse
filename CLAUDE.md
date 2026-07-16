# Tumbledown House — Website Migration

## Project overview

Rebuilding tumbledownhouse.com as a static site to replace an expensive Squarespace subscription ($360/yr). Target cost: ~$12/yr (domain only, free static hosting). Tumbledown House is a San Francisco Bay Area band (modern speakeasy / saloon jazz / parlor pop) led by Gillian Wolfe and Tyler Ryan Miller. Tyler is the site owner.

The goal is a near-exact visual replica of the current Squarespace site (template family with index sections, dark theme). A complete first-pass `index.html` already exists in this repo — it was built from design tokens extracted from the live site's compiled CSS, so treat its palette/typography as ground truth.

## Status

- [x] First-pass single-file `index.html` (all sections, working audio player, video embeds, gallery slideshow)
- [x] Download all assets from Squarespace CDN before the subscription is cancelled (see Asset Manifest below) and switch `index.html` to local paths — done July 16, 2026. All 20 images (`assets/img/`, true JPEGs at max 2500w — the CDN serves WebP unless you send `Accept: image/jpeg`) and all 9 MP3s (`assets/audio/`, 256kbps) downloaded and verified (decode + duration checks in a local browser). `index.html` is the canonical file with local paths; `tumbledownhouse-rebuild_1.html` is the pre-localization original, safe to delete once Tyler confirms.
- [ ] Side-by-side visual comparison against live site; tighten spacing/header/hero crop
- [ ] Wire mailing list form (currently a placeholder alert) — likely Mailchimp embedded form
- [ ] Wire contact form (currently a placeholder alert) — Formspree free tier or similar
- [ ] Decide fate of old news posts (2018–2019): rebuild as static pages or drop; links currently point to old tumbledownhouse.com URLs which will die
- [ ] Deploy: GitHub Pages or Cloudflare Pages from this repo
- [ ] Transfer domain away from Squarespace (Cloudflare Registrar or Porkbun, ~$11–12/yr) and point DNS at the new host
- [ ] Only after everything above is verified live: cancel Squarespace

## Decisions made

- **No merch / no commerce.** The band is not currently selling merch. All cart and merch functionality was intentionally removed. Physical/digital sales point to Bandcamp only. Do not re-add commerce.
- **Twitter feed section dropped** (dead embeds). Twitter icon links kept for now; fine to remove if Tyler agrees.
- **Static site, no framework.** Plain HTML/CSS/JS is deliberate: zero build step, zero hosting cost, trivially portable. Don't introduce React/SSGs unless Tyler asks.
- **Content is intentionally frozen** (~2019–2020 era band content). Faithful replication first; pruning/updating is Tyler's call, not an assumption.
- **Instagram feed is static** (grid of images linking to posts) rather than an auto-updating API feed, to avoid tokens/paid widgets.

## Design tokens (extracted from live Squarespace CSS — do not eyeball-change)

Colors:
- Page background: `#100806`
- Site wrapper background: `#181616`
- Body text: `#ffffff`
- Links: `#fdf8a1` (pale yellow)
- Buttons/accent: `#e7d0ba` (tan) with dark text `#1c1c1c`

Typography (Google Fonts):
- Site title: Source Code Pro, 23px, uppercase, letter-spacing 1.87px
- Nav: Roboto Slab, ~15–17px, uppercase, letter-spacing 2px
- Headings (h1/section): Abel, uppercase, letter-spacing 7px (large sizes)
- Body: Sanchez, 16px, line-height 1.75em, letter-spacing 0.4px
- Buttons: Source Code Pro, uppercase, letter-spacing 2px

Page structure (one-page scroll, anchors): Home (full-bleed hero + social icons + mailing list) → Video → Music → Tour → Bio → News & Updates → Galleries → Contact → Footer.

## Asset manifest — download these BEFORE cancelling Squarespace

Create `assets/img/` and `assets/audio/`, download everything below, then update `index.html` to local paths. URLs are live as of July 2026. Append `?format=2500w` to image URLs for full-size versions.

### Images (images.squarespace-cdn.com/content/v1/5d9373f018c280789b578cae/...)
- Hero: `1571146998852-9IBK1AZ059WIW47QAHRX/TDH_Standing2_PhotoCredit_Kala_Minko_LOWRes_LandscapeColor.jpg`
- Album cover: `1571254233822-UJORJE9BH5K8R6DKNP88/CD_Cover_FINALCover_12.jpg`
- Bio/contact photo: `1570900319924-6OMV31XYCNRP1UD49F0S/TDH_Expoloratorium1_Credit_KalaMinko_%40kminkophoto.jpg`
- News thumbs: `1571262947054-YWFPR470M3DL0CE2XYZJ/IMG_7572-e1565195205372.jpg`, `1571262946151-6VC4YPFHM330QM2VUU3Q/TDH_Alaska_2019-Ad_Square_V5_Homer.jpg`, `1571262944850-RF9LUT43AT0415LSSHO7/IMG_3817-e1545165078648.jpg`
- Gallery: `1571243730482-CUZVER2M1UGH3ZR8PTRR/TDH_Seated1_PhotoCredit_Kala_Minko_Highres_LandscapeColor.jpg`, `1571244158688-S66FLMI3OE4NT79APUG5/TDH_Standing1_PhotoCredit_Kala_Minko_HighRes_LandscapeBW.jpg`, `1571243783950-YEIKU1VVE9CX9ISP1B67/TDH_Credit_KalaMinko_%40kminkophoto.jpg`, `1571243791997-LA6T5EXB1XVT8XI5EJ3S/IMG_5450-Edit-2.jpg`, `1571243798788-L3T3O8ZT3QRN8VV1SITG/IMG_5589-Edit-2.jpg`, `1571244380455-E09SA40C1SEYZGV3ZUB1/P1090750.jpg`
- Instagram grid images: the eight `image-asset.jpeg` URLs currently in `index.html` (grep for `ig-grid`)
- Note: original full-res photos are by Kala Minko (@kminkophoto); Tyler may have originals that beat the CDN versions.

### Audio — "Sum and Substance" album (static1.squarespace.com/static/5d9373f018c280789b578cae/5da5d5f0c84add337ca9a9d1/...)
All nine track MP3 URLs are in `index.html` in the `#tracklist` list (`data-src` attributes). Track order: Shaky Little Thing, Clever Crocodile, The Buttons In Me, Ode to Josephine, The Devil's Design, Pure Medicine, Sullied Acres, Set You Down, Midnight in The Barrio.

### Also grab before cancelling
- Full text + images of the six news posts (URLs in the News section of `index.html`) if Tyler decides to keep them
- Any pages not on the homepage index (check Squarespace admin for hidden/unlinked pages)

## Embeds and third-party pieces

- YouTube: `6aLytXPxZsU`, `XlFjdjG73RA` (live at Reno Artown), `YLhzKh2xrQs` (Ode to Josephine). Channel: `UC19p9XJqHFJW20utUo2guiQ`
- Tour: ReverbNation widget, artist_458069 (iframe already in `index.html`). Alternative if it dies: Bandsintown free widget.
- Bandcamp: https://tumbledownhouse.bandcamp.com/
- Spotify artist: `7Cr5P87IxJxAdoGiPnH8UG`
- Booking contact: Barbara Collin, 323-556-1046, collinartists@gmail.com; Bay Area booking via info@tumbledownhouse.com

## Deployment plan

1. Repo on Tyler's existing GitHub account (e.g. `tumbledownhouse`)
2. GitHub Pages (Settings → Pages → deploy from main) or Cloudflare Pages connected to the repo
3. Custom domain `tumbledownhouse.com` + `www`, HTTPS enforced
4. Domain transfer: unlock at Squarespace, get auth code, transfer to Cloudflare Registrar or Porkbun; expect up to a week; do this before cancelling the Squarespace site but note domain and site are separate cancellations
5. Keep Squarespace live until the new site is verified at the real domain

## Working preferences

- Tyler prefers natural, human-sounding copy; avoid AI-sounding language in any site text or drafts
- Keep changes cheap and simple; the whole point of this migration is cost and independence
- Verify against the live site (while it's still up) rather than guessing at design details
