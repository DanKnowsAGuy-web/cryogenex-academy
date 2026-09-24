# DESIGN.md — the placeholder skin

Version 2 drops the Field Report design system entirely (`site.css`, `site.js`, the
Archivo/Geist Mono fonts, `hvac-dusk.jpg`) per Dan's rejection of that design. The real
Energy Plus brand is not resolved yet, so this version ships on a deliberately isolated
placeholder skin: one file, `assets/brand.css`, holds every color, font, spacing, and
radius token the page uses.

## The rule: all tokens live in brand.css
`index.html` contains no color literal, no `font-family` declaration, and no radius value
of its own. Every visual property it sets comes from a `var(--...)` defined in
`assets/brand.css`, or from a class (`.btn`, `.card`, `.ledger-table`, etc.) whose rules
live entirely in that file. To reskin this page for the real brand, replace
`assets/brand.css` and nothing else. Nothing in `index.html`'s markup or inline `<script>`
needs to change.

## Tokens (assets/brand.css)
- Color: `--bg` (#ffffff), `--bg-2` (#f6f7f8, the alternate band), `--ink` (#0b0f12),
  `--ink-2` (#48525b), `--hair` (#e3e7ea), `--money` (#0e6b52, used only for recovered
  dollar figures), `--accent` (#0b0f12, buttons), `--warn` (#b45309, used only on the word
  "Claim" in the ledger's confidence column).
- Type: `--font-display` (Inter Tight 600/700/800), `--font-body` (Inter 400/500/600),
  `--font-mono` (JetBrains Mono 400/600), loaded from Google Fonts. Numerals in the ledger
  and callouts render in mono with tabular figures.
- Scale: display `clamp(2.4rem, 1.6rem + 3.5vw, 4.5rem)` at weight 800; h2
  `clamp(1.7rem, 1.3rem + 1.6vw, 2.6rem)` at weight 700; body 1.15rem/1.6; labels 0.78rem
  uppercase, letter-spacing 0.12em, mono.
- Spacing: `--wrap` (1080px), `--narrow` (44rem, used for the hero and the three bill
  sections), section padding `clamp(4rem, 3rem + 4vw, 7rem)`, 20px minimum gutter.
- Shape: `--radius` (8px) on cards, buttons, and the toggle; 1px hairlines everywhere; no
  shadow anywhere except the soft two-layer shadow on the ledger `.card`.

## Page is light, no hero image
No hero photo. The hero is text only, on `--bg`. The only photography on the page is Cliff
Suljak (rendered in grayscale via a CSS filter, not a pre-processed image) and the film
cover still.

## What's in brand.css
Structural page components (header/footer bars, the wordmark, the ledger card and table,
the range slider and scope toggle, the two button variants, the numbered steps list, the
callout cards, the film facade) are all defined once in `brand.css` as classes, so
`index.html`'s markup stays plain and semantic. This is different from the old system,
where a page-specific inline `<style>` block layered structural CSS on top of a shared
production stylesheet; here there is exactly one stylesheet and it is the whole design.

## Motion
`prefers-reduced-motion: reduce` disables every transition on the page via a single rule.
The only motion otherwise is a 200ms color transition on the ledger's numeric cells and
buttons when their values change or their state toggles; nothing scrolls, animates in, or
autoplays.

## What was removed from version 1
`assets/site.css`, `assets/site.js`, `assets/fonts/` (Archivo variable, Geist Mono, and
their loader stylesheet), and `assets/img/hvac-dusk.jpg` are deleted. `assets/img/cliff-lab.jpg`
and `assets/img/film-cover.jpg` are kept; they are the only two photos version 2 uses.

## The no-dash rule
Unchanged: ranges are written "20 to 24 percent," never with an en dash or em dash.
