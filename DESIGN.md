# DESIGN.md — the Field Report system, as applied here

This page uses Energy Plus's live design system (the one running at
slashyourenergycost.com), not the separate navy/champagne "Energy+" token set from
yourenergyplus.com. The stylesheet and script are the production files (`assets/site.css`,
`assets/site.js`, `assets/fonts/report-fonts.css`, plus the two font files they call for),
copied in unmodified except for two changes described below.

## Tokens (from site.css, used as-is)
- Document ground: `--paper` (#f3f5f6, cool white), `--card` (#ffffff), `--rule` (#d3d9dd)
- Ink: `--ink` (#101416), `--body-c`, `--faint`
- The instrument moments (hero, close, dark beats): `--graphite` (#174e58, petrol), with
  `--panel-ink` / `--panel-body` / `--panel-faint` for text on it
- The one signal color: `--amber` (#e0a21c), used only on a verified or metered value
  (the `.readout` and `.floor` components, the three tallest bars in the spread chart)

## Type
- Body and headings: Archivo (variable, width axis 62% to 125%), display weight uses the
  wide/bold stretch the system reserves for h1/h2/h3
- Figures, footnote markers, and metered values: Geist Mono
- No second typeface or palette was introduced anywhere on this page.

## What's reused directly from the live system
- `.beat` / `.beat--rule` / `.beat--dark` for section rhythm
- `.hero`, `.hero__media`, `.hero__scrim`, `.hero__lede` for the top banner
- `.creds` (hairline-tiled card grid) reused for both the "real problem" three columns and
  the stakes stat tiles
- `.steps` (the numbered, border-topped list) reused for both the five fix levers and the
  three pilot steps
- `.floor` (amber-wash callout) for the combined-recovery note, the pricing box, and the
  guarantee
- `.dossier` / `.plate__frame--portrait` for the engineer profile
- `.ledger` + `.sheet` dialog for the scrolling case record and the full-record modal —
  this markup, and the entire ledger/dialog behavior, is driven by the RECORD array already
  baked into `site.js`; no page-specific JavaScript was needed for it
- `.film-inline` for the Wistia facade
- `details.gate` for the three-audience chain section
- `.plate` for the rooftop-unit image band
- `.close` for the closing CTA band

## What was added, and why
A small inline `<style>` block adds only structural rules that don't exist yet in the shared
system (a static top bar, the stat-tile grid, slider styling, the calculator panel and output
tiles, the bar-chart wrapper, a plain footer bar). Every value in that block is one of
site.css's own custom properties — no new colors, no second palette, no new font.

## Deliberate simplifications from the live root's "bold version"
- No `.hero-scrolly` pinned scroll-scrub: that pattern exists to draw pen marks onto a
  specimen bill exhibit as you scroll, which is Sedano's-specific artwork this page doesn't
  have. Wrapping our hero in `.hero-scrolly` without that content would force an empty
  230vh scroll-jack with nothing to reveal, so the hero here is the system's static resting
  frame instead (graphite ground, dimmed photo, white bold Archivo H1).
- No fixed, hero-clearing header: the live root's `.head` goes transparent over the hero and
  fades its nav back in on scroll. This page's header carries two plain lines of info, not
  navigation, so it is a plain static bar instead, avoiding a contrast bug where header text
  would sit low-contrast over the hero photo during the "is-clear" state.
- No numbered footnote/disclosures apparatus: the live root's footer carries FMI-specific
  legal notes tied to Sedano's copy. This page's footer is the single paragraph the build
  spec calls for.

## The no-dash rule
Enforced throughout the new copy: ranges are written "20 to 55 percent," never with an en
dash or em dash. `site.js`'s own baked-in case-ledger data already uses "to" for its ranges;
the two vendor-name mentions it did carry ("HVAC Optimizer," "Tri-S ECM") were edited out of
the local copy of `site.js` before deploying, since the case ledger renders live on this page.
