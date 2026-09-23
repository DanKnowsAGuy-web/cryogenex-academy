# DESIGN.md — Energy+ system, as applied here

## Tokens
Dark navy surfaces with a champagne accent, carried over from `energyplus/tokens.css`:
- Surfaces: `--navy` (page bg), `--navy-mid` (alt section bg), `--navy-card` (tiles, cards),
  `--navy-hero` (hero gradient), `--navy-deep` (header, CTA, footer)
- Accent: `--amber` / `--amber-light` (champagne, not gold-yellow)
- Text: `--white` (headlines), `--cream` (body), `--mid` (leads), `--muted` (supporting)
- Borders: `--border` (amber at low opacity), `--border-sub` (hairline white)

## Type
- Display / headings: Spectral (300, 400, 500, 600, plus italics for `em`)
- Body and UI: Barlow (400, 500, 600, 700)
- Labels, buttons, chips, eyebrows: Barlow Condensed (400, 500, 600, 700), always uppercase
  and letter-spaced
- Body copy is set at 1.15rem minimum (`--t-body`), because this is read by a VP on a phone.
  Nothing on the page drops below 0.9rem, and that only applies to fine-print footnotes.

## No em dash / en dash rule
Enforced throughout: ranges are written "20 to 55 percent," not "20-55%," except inside the
scrolling case ledger, which quotes vendor-reported figures verbatim (a hyphen-minus is used
there for ranges like "20-35%" instead of an en dash, to stay ASCII-clean).

## Big type for phone reading
- The calculator and equation widgets render their headline numbers in `--font-display` at
  `clamp(1.9rem, 4.5vw, 2.9rem)` or larger, in champagne, so the one number a VP needs is
  legible at arm's length on a phone.
- Section headings never drop below `--t-h1` (`clamp(1.8rem, ..., 2.8rem)`).
- Buttons have a 44px minimum tap target.

## Structural patterns reused from the Redstone/Landry's reference
- The `.triple` three-column pattern for the "real problem" section
- The `.lever` numbered list for the fix
- The proof block layout: engineer feature, protocol statement, scrolling case ledger with a
  `<dialog>` "full record" sheet, the money statement, and the Wistia film facade
- The `.steps` numbered pilot plan and the `.guarantee` callout
- The 80-frame canvas hero film and ember canvas from the reference were dropped entirely;
  this page uses a single static hero with a dimmed background image instead.
