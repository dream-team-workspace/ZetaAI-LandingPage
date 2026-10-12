# Crypko (reference) → ZetaAI · clone notes

## Source information

- **Original site URL:** `https://crypko.ai` / `https://www.crypko.ai` — **the site is retired and offline.** DNS does not resolve; the `crypko.com` variant returns a TLS error. There is no live site to crawl, no source repo, and no original HTML/CSS/JS that could be harvested.
- **Source of truth:** a single screenshot supplied by the user —
  `/home/dani/Downloads/e1693d303b3d7370b798752dc9e9f973.jpg` (1200×900 JPEG), the Crypko homepage.
- **Original author:** Crypko was a product by **Preferred Networks, Inc.**
- **Licence: NONE / undeclared ⇒ all rights reserved.** No licence was published with the site. Consequence: this rebuild is for **local learning and private use only**; the original design is **attributed** (see the colophon in `index.html`), and it must **not be redeployed publicly** in this form without permission.
- **Attribution requirement:** yes — satisfied by the colophon line at `index.html` (search for "design reference").

## Tech stack

- **Static, single-file site:** `index.html` — hand-written HTML plus one `<style>` block. **No JavaScript, no build step, no framework, no dependencies.**
- **Self-hosted fonts:** 13 woff2 files in `assets/fonts/`, declared by `assets/fonts/fonts.css`
  (Anton 400; Inter 400/500/600/700/800 — `latin` + `latin-ext` subsets only). **No runtime request leaves the machine.**
- Node v24.21.0 and the system Chrome (`/opt/google/chrome/chrome`) were used for **verification only**, through the web-clone skill's zero-dependency CDP adapter.
- The two images are crops the user supplied from their own screenshot.

## Pre-clone assessment

- **Complexity level: L1** — static HTML/CSS, no JS, a single view (`references/assessment.md`).
- **Mode: content re-skin onto the reference's layout** (a visual-clone rebuild plus a content swap). The user's brief was explicitly *"Keep the layout, use my ZetaAI content"*.
- **Can be high fidelity:** the plate-on-gray framing, the dipping black header band, the condensed all-caps headline, the full colour system, the circular seal, the portrait card with its yellow rail, the duo image, the white app card.
- **Approximated / substituted:** the display and body typefaces (see *Known gaps*), all copy, the wordmark, the nav, and the badge text.
- **Not cloned:** n/a — the reference site no longer exists, so this is a **rebuild from a screenshot**, not a copy of a live implementation.
- **Main risks:** font substitution that can no longer be verified (the site is offline); asset licensing (all rights reserved); the duo crop carries a baked-in badge from the original screenshot.

## Run it

```bash
cd <this project directory>
python3 -m http.server 8123
# then open http://127.0.0.1:8123/
```

## What changed vs the original

- **No tracking scripts were removed — because there were none to remove.** This is a from-scratch rebuild, not a mirror of captured HTML. The deliverable makes **zero third-party runtime requests**: every font is a local woff2, and the only external-looking references are placeholder `#` anchors.
- **All copy is new ZetaAI copy and is placeholder.** The user **skipped the content question**, so every string in the page is drafted copy and must be treated as such. The colophon says so in the page itself.
- The hero's layout, type scale, spacing and colour were measured from the screenshot; the header band and the seal were rebuilt as inline SVG (they cannot be reproduced with CSS curves alone).

## Original vs clone

| Module | Original (reference screenshot) | Clone | Difference / trade-off | Evidence |
|---|---|---|---|---|
| Page frame | Black plate inset on gray `#C1C0BC`, cream `#E6E4D5` inner panel | Same, `aspect-ratio:1052/713`, black plate padding `.85rem` | Measured from the screenshot's bounding box (`1080×741 at +60+79`) | `RECON/screenshots/clone-1440.png` |
| Header | Black band dipping into the cream panel; logo on cream far-left, nav on black centre, white pill on cream far-right | Inline SVG band, `viewBox="0 0 1000 41"` | Rebuilt as SVG — a CSS `border-radius` bulge cannot reproduce the asymmetric band | `index.html` `.band` |
| Headline | Two lines of heavy condensed all-caps | Anton `10cqw`, `line-height:.9` | Font substituted (source face unidentifiable) | see *Known gaps* |
| Seal | Circular stamp, ring text, black star burst, "START GENERATE" | Same, SVG (`viewBox 0 0 200 200`), text now "START CHAT" | Burst re-profiled to outer radius 55 / inner 47 | radial pixel profiling |
| Portrait card | Character art + yellow right rail with sparks and an up-arrow | Same, `grid-template-columns:81% 19%` | Art cropped from the user's screenshot (188×338) | `assets/avatar-portrait.jpg` |
| Duo image | Two characters, yellow stadium badge at the right edge | Same; badge overlaid as HTML | The crop has the original badge **baked in**, so an opaque overlay covers it | `assets/avatar-duo.jpg` |
| App card | White card, bold title, 2-line copy, Apple + Play discs, download pill | Same, with the black `···` tab on its top-right corner | Title is a normal-width bold grotesque (not condensed), per the reference | `index.html` `.app-card` |
| Below the fold | *(unknown — screenshot shows only the hero)* | Ticker, features, steps, download band, footer | **Extension, not a clone** — invented in the same visual language | `RECON/screenshots/clone-390.png` |
| Mobile | *(unknown)* | Single-column flow under 880px | Cannot be compared; verified only for correctness, not fidelity | `RECON/screenshots/clone-390.png` |

## Fidelity score

Scored only on what a screenshot and a browser run can support (`references/assessment.md`).

- **Source evidence: 2/5** — only a screenshot. No source, no live site, no asset harvest. Nothing could be checked against real markup.
- **Structure fidelity: 5/5** for the hero (every element of the reference hero is present, at measured positions). The rest of the page is an extension, so the score is hero-scoped.
- **Visual fidelity: 4/5** — colours are sampled exactly (see below); geometry is measured. Marked down because the typefaces are substitutes and the artwork is a JPEG crop rather than the original assets.
- **Motion / interaction: 3/5** — there was no scroll choreography or canvas to reproduce. Only hover/focus states and one CSS marquee are implemented.
- **Responsive: 5/5** — 10 viewport widths verified; no horizontal scroll, zero console errors, all tap targets ≥ 24px.
- **Feature completeness: 4/5** — all links resolve within the page; placeholder `#` anchors on community links are intentional.
- **Content replacement: 5/5** — fully ZetaAI; no original copy remains (the only "Crypko" mentions are the required attribution).
- **Legal / deployment risk: 2/5** — the reference is all-rights-reserved and the artwork is anime character art cropped from a screenshot. **Do not deploy publicly as-is.**
- **Overall:** a faithful, browser-verified rebuild of the *hero* of an offline reference site, safe for local study, **not** safe to publish without clearing the art and the design attribution.

## Colour system (sampled from the screenshot — exact)

| Token | Hex | OKLch | Role |
|---|---|---|---|
| `--bg` | `#C1C0BC` | `oklch(80.7% 0.006 95.1)` | page gray |
| `--surface` | `#E6E4D5` | `oklch(91.6% 0.020 100.6)` | cream plate |
| `--fg` | `#0A0A0A` | `oklch(15% 0 0)` | ink |
| `--muted` | `#6B6960` | `oklch(52% 0.012 98)` | secondary text |
| `--border` | `#CFCDBE` | `oklch(84% 0.016 100)` | hairlines on cream |
| `--accent` | `#FAFE5F` | `oklch(96.6% 0.176 110.7)` | accent yellow |
| `--paper` | `#FFFFFF` | `oklch(100% 0 0)` | cards |

## Replacement map (what to change, and where)

- **Text / copy** → all strings live inline in `index.html`. They are placeholder ZetaAI copy; rewrite them there.
- **Images** → `assets/avatar-portrait.jpg` (188×338) and `assets/avatar-duo.jpg` (452×300). Replace with your own art; keep the aspect ratios (`.portrait` is `232/340` including the yellow rail, `.duo` is `452/300`).
- **Colours** → the CSS custom properties in the `:root` block at the top of the `<style>` element.
- **Fonts** → `assets/fonts/` + `assets/fonts/fonts.css`. To swap the display face, change `--display` and add the woff2 + `@font-face` rule.
- **Logo** → the `.brand` element (text + an inline 4-point spark SVG).
- **The duo badge text** → `index.html`, the `.duo-badge` element (currently "Create avatar").
- **The seal ring text** → the `<textPath>` inside `.seal` (currently "★ Official release ★ On-device AI assistant ★ ZetaAI v1.0 ★").
- **Attribution** → the `p.colophon` in the footer. Keep it while the layout derives from the reference, or replace the layout and remove it.

## Known gaps

1. **Font substitution — `SOURCE: visual match`, not byte-exact.** The reference's display face could not be identified because the site is offline and its assets are unrecoverable. Substitutes: **Anton** (display), **Inter** (body/UI), JetBrains Mono (declared but unused). The headline in the reference is a heavy condensed grotesque; Anton is the closest free equivalent. The reference body face is a neutral grotesque; Inter is a reasonable match. **These are approximations and are not guaranteed to match the original.**
2. **The anime character art is cropped from a screenshot** (a lossy JPEG), not the original artwork. The portrait crop is 188×338 and the duo crop is 452×300; both are upscaled by CSS at large widths, so they will soften at high resolutions.
3. **The duo image has the original `CREATE ANIME` badge baked into the pixels.** It is covered by an opaque HTML badge positioned at image-fraction `left:94.9%; top:54.7%`. This works because the badge is opaque and covers it completely — but the underlying pixels are still the original artwork.
4. **Everything below the hero is an extension, not a clone.** The screenshot shows only the hero, so the ticker, features, steps, download band and footer were invented in the same visual language. They are not reproductions of anything.
5. **Mobile fidelity is unverifiable** for the same reason — there is no mobile reference to compare against. Mobile was verified for *correctness* (no overflow, no errors, sane stacking), not for fidelity.
6. **The seal's ring text is decorative SVG text** — it is not selectable or announced, which is intentional for a logo-like device, but it means its content is not available to assistive technology.
7. **Community links are placeholder `#` anchors** (Discord, GitHub, Changelog, Guide, FAQ, Docs).

## Verification

- [x] Runs locally, **console 0 errors** — verified at 1440/768/390 via `recon-site.mjs`, and at 10 widths via a custom probe.
- [x] Screenshots captured in `RECON/screenshots/` (`clone-1440.png`, `clone-768.png`, `clone-390.png`).
- [ ] `route-crawl.mjs` — **not applicable**, this is a single-page site.
- [ ] `interaction-probe.mjs` — **not applicable**, there is no JS. Hover/focus and the marquee were checked by eye and by computed styles.
- [ ] `visual-diff.mjs` — **not run.** It diffs against a recon of the original *site*; the original is offline, so there is no comparable render. Comparison was done manually, by cropping the same regions from the reference JPEG and from a fresh render and viewing them side by side.
- [x] `audit-clone.mjs` → `CLONE_AUDIT.md`. Fidelity hard-gate ("fonts / images / colours") reports **no findings**. The remaining findings are the intentional `Crypko` attribution in `brand-spec.md` and the colophon (required by the licence terms), plus hits inside `.od-skills/` — i.e. the skill's own files, not this deliverable.
- [x] No horizontal scroll at 360 / 390 / 430 / 600 / 768 / 820 / 1024 / 1366 / 1440 / 1920 px.
- [x] All interactive elements have a visible `:focus-visible` ring; every tap target is ≥ 24px (footer links were fixed from 19px to ~37px).
- [x] `od-preview-rewrite.mjs --project .` → **0 files updated** (asset references were already relative).
- [x] Responsiveness verified at 10 widths; `prefers-reduced-motion` disables the marquee and all transitions.

### Bugs found and fixed during verification

1. **`position:static` escape (mobile, ≤880px).** In the mobile breakpoint `.duo` and `.app-card` became grid items, so their absolutely-positioned children lost their containing block and resolved against `.plate-inner` instead: the `.duo-badge` drifted onto the portrait card (leaving the baked-in badge visible) and the `.app-tab` landed in the header. Fixed by keeping both parents `position:relative`.
2. **Relative-offset side-effect of fix 1.** Once those parents were `relative`, their inherited `left`/`top`/`bottom` values began acting as *relative* offsets (`.app-card` shifted to `x=187` in a 390px viewport). Fixed with `inset:auto` in the same rule.
3. **Footer links were 19px tall**, below the 24px minimum. Fixed with vertical padding.
4. **Duo badge geometry.** The reference badge is a **vertical stadium (~56×96)**, not a circle, centred at image-fraction **(94.9%, 54.7%)** — an earlier circular badge at (90.5%, 52%) left the original badge visible. Fixed and re-verified.
5. Assorted hero refinements matched to the reference: app-card title is a normal-width grotesque (not condensed); the `···` tab is a wide rounded rect overhanging the card's top edge by ~4px; store discs ≈40px; the download pill ≈127×34 with a full-height yellow circle; the seal burst outer radius ≈55% of the seal half-box.

## Pre-deploy replacement checklist

**Do not publish this page in its current form.** Before any public deployment:

1. **Clear the artwork.** Replace `assets/avatar-portrait.jpg` and `assets/avatar-duo.jpg` with art you own or that is properly licensed. The current crops are anime character art taken from a screenshot and are **all rights reserved by their owner**. This is the single biggest blocker.
2. **Clear the design.** The layout and art direction are derived from the Crypko homepage (Preferred Networks). Either obtain permission, or rework the layout far enough that it is no longer recognisable as a derivative.
3. **Replace the substituted fonts** if byte-exact type matters, or confirm you are happy with Anton + Inter (both SIL Open Font License).
4. **Resolve the attribution line** in the footer — either keep it (if the derivation stands) or remove it after step 2.
5. **Replace all placeholder copy** and the placeholder `#` community links.
6. **Confirm no third-party runtime requests** remain — currently there are none; keep it that way if "offline-first, private by default" is a claim the product makes.
7. Re-run `recon-site.mjs` and the responsive probe after any asset swap, since image aspect ratios are tied to the layout.

## How the hero was measured (for future edits)

All hero geometry is expressed relative to the cream panel (`1052 × 713`), which the original occupies as `1080×741 at +60+79` inside the 1200×900 screenshot. Panel-local positions converted by subtracting `x=75, y=93`. The hero uses `container-type:inline-size` on `.plate-inner` and **`cqw` units throughout**, so every element scales with the plate and the measurements stay valid at any width. If you change the plate's `aspect-ratio`, the `cqw` values continue to work; the `%` positions are relative to the panel and are unaffected.

Reference measurements used: headline at 3.8% / 17.1%; seal centre at 59.4% / 55.0%, diameter ≈200px; portrait card at 75.4% / 17.5%, 22.1% × 47.7%; duo at 3.1% / 53.7%, 43.0% × 42.1%; app card at 49.7% / bottom 4.8%, 47.4% wide; header band depth ≈39px below the panel top, spanning ≈60% of the width.
