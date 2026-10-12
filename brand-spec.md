# ZetaAI — Brand & Visual Spec

Derived from the reference screenshot `e1693d303b3d7370b798752dc9e9f973.jpg`
(Crypko homepage, crypko.ai — domain no longer resolves, screenshot is the source).
Colors are **sampled pixel values**, not invented. Applied 1:1 to a ZetaAI-branded
landing page.

## One-sentence system

An acid-yellow accent on a cream "plate" floating on warm gray, framed by heavy
black condensed display type and a white utility card — a poster-like hero that
reads as a physical print object.

## Color tokens (sampled → OKLch)

| Token       | Hex       | OKLch                        | Sample point / use                     |
|-------------|-----------|------------------------------|----------------------------------------|
| `--bg`      | `#C1C0BC` | `oklch(80.7% 0.006 95.1)`    | page gray (outer)                      |
| `--surface` | `#E6E4D5` | `oklch(91.6% 0.020 100.6)`   | cream plate                            |
| `--fg`      | `#0A0A0A` | `oklch(15% 0 0)`             | ink (sampled `#010101`, lifted for text)|
| `--muted`   | `#6B6960` | `oklch(52% 0.012 98)`        | secondary text on cream/white          |
| `--border`  | `#CFCDBE` | `oklch(84% 0.016 100)`       | hairlines on cream                     |
| `--accent`  | `#FAFE5F` | `oklch(96.6% 0.176 110.7)`   | acid yellow accent                     |
| `--paper`   | `#FFFFFF` | `oklch(100% 0 0)`            | card / button surface                  |

Sampled raw values: gray `rgb(193,192,188)`, cream `rgb(230,228,213)`,
black `rgb(1,1,1)`, yellow `rgb(250,254,95)`, white `rgb(255,255,255)`.

## Type

| Role    | Stack                                                              |
|---------|--------------------------------------------------------------------|
| Display | `'Anton', 'Arial Narrow', sans-serif` — heavy condensed grotesque  |
| Body/UI | `'Inter', system-ui, -apple-system, 'Segoe UI', sans-serif`        |
| Mono    | `'JetBrains Mono', ui-monospace, 'SFMono-Regular', monospace`      |

Both webfonts are **self-hosted** in `assets/fonts/` (`assets/fonts/fonts.css`),
never hotlinked from Google. The original site's display face could not be
identified because the site is offline; Anton is the closest free condensed
heavy grotesque (`SOURCE: visual match`, not a byte-exact recovery).

## Observed rules that define the language

1. **Plate-on-gray framing.** Content never touches the viewport edge; it sits on
   a rounded black plate (radius ≈34px, inset ~60px) floating on warm gray.
2. **The black header dips.** The header's bottom edge is a smooth downward arc
   (thin at the far left, deep through the centre-right) so the wordmark reads on
   cream while nav + CTA read on black.
3. **Heavy condensed caps, tight.** Headlines are Anton, all-caps, line-height
   ≈0.9, optically flush-left; they carry the composition.
4. **One accent, used as punctuation.** `#FAFE5F` marks only: the avatar rail, the
   floating action badge, the seal's inner type, and the download chip.
5. **Rounded white utility card** with a hairline border + a black `···` tab
   overlapping its top-right corner; store icons are overlapping black discs.
