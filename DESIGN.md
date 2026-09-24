# DESIGN.md — the live site skin

## Version 5 (September 2026): the real Energy Plus skin, pulled live
Version 2 through 4 shipped on a deliberately isolated placeholder skin
(`assets/brand.css`) because the real brand wasn't resolved yet. It is now. This version
deletes `assets/brand.css` and pulls the live root's own production assets straight from
slashyourenergycost.com, so this page shares the exact same colors, type, and spacing as
the site it lives under.

### Assets pulled, and when the live copies were last modified
All four requests returned the same `Last-Modified` header, `Thu, 17 Sep 2026 17:06:26
GMT` — the root site's most recent deploy — confirming these are the current live files,
not stale cached copies:

| Live URL | Saved to | Last-Modified |
|---|---|---|
| `https://slashyourenergycost.com/assets/site.css` | `assets/site.css` | Thu, 17 Sep 2026 17:06:26 GMT |
| `https://slashyourenergycost.com/assets/fonts/report-fonts.css` | `assets/fonts/report-fonts.css` | Thu, 17 Sep 2026 17:06:26 GMT |
| `https://slashyourenergycost.com/assets/fonts/archivo-var.woff2` | `assets/fonts/archivo-var.woff2` | Thu, 17 Sep 2026 17:06:26 GMT |
| `https://slashyourenergycost.com/assets/fonts/GeistMono-400.woff2` | `assets/fonts/GeistMono-400.woff2` | Thu, 17 Sep 2026 17:06:26 GMT |
| `https://slashyourenergycost.com/assets/img/energy-plus-logo.png` | `assets/img/energy-plus-logo.png` | Thu, 17 Sep 2026 17:06:26 GMT |

`report-fonts.css` names two font files (`archivo-var.woff2`, `GeistMono-400.woff2`);
both were resolved against `https://slashyourenergycost.com/assets/fonts/` and pulled
alongside it. `index.html` links `assets/fonts/report-fonts.css` and
`assets/site.css?v=20260924d`.

### The rule: all tokens live in site.css
`index.html` contains no color literal and no `font-family` declaration outside the one
inline `<style>` block, and every rule in that block reaches for a `var(--...)` defined
in `assets/site.css`: `--paper`/`--paper-2`/`--card` (grounds), `--ink`/`--body-c`/
`--faint` (text), `--rule`/`--rule-soft` (hairlines), `--graphite`/`--graphite-2` (the
petrol instrument color, used on the hero and the ledger's toggle/thumb/buttons),
`--amber`/`--amber-ink` (reserved for verified or metered values — the ledger's
recovered-dollar figures use `--amber-ink`, matching the root's own convention of amber
marking a measured number), `--font-sans` (Archivo), `--font-mono` (Geist Mono), and the
`--step-*` type scale. Nothing on the page is styled from a value that doesn't trace back
to one of these.

### What the inline `<style>` block adds
Two kinds of rules live in the `<style>` block in `<head>`:
1. **The ledger and its sliders.** This page's roof ledger — the card, the three range
   inputs, the min/max mono footers, the store/fleet toggle, the before/after table — is
   a widget the root site doesn't have a design-system class for, so it's built here,
   entirely from `var(--...)` tokens.
2. **Page furniture the root's marketing-site classes (`.beat`, `.steps`, `.record`,
   `.dossier`, etc.) don't map onto**, because those are built for the root's specific
   sections, not a generic component library. The bill/why/pilot sections on this page
   keep their existing structure and copy from version 4, so `.band`, `.card`, `.grid`,
   `.plain-card`, `.film`, `.steps`, `.callout`, and `.toggle` are defined once here,
   again entirely from site.css variables.

The header and the hero are the one place this page borrows the root's own classes
directly rather than writing new ones: `.head`/`.head__mark`, and `.hero`/`.hero__media`/
`.hero__scrim`/`.hero__in`/`.hero__lede`/`.btn`/`.textlink`, all copied verbatim from the
markup at slashyourenergycost.com (nav links and the book button dropped, since this
page isn't the marketing site).

### The hero photo
`assets/img/hero-store.jpg` and `assets/img/hero-store-mobile.jpg` come from a single
source photograph: *Academy Sports + Outdoors in Brenham, TX on opening weekend*,
Wikimedia Commons, uploaded by Ted Eytan and released under CC0 1.0 (public domain
dedication) —
`https://upload.wikimedia.org/wikipedia/commons/6/6c/Academy_Sports_%2B_Outdoors_in_Brenham%2C_TX_on_opening_weekend.jpg`,
original 4032×3024, 2.7 MB.

Processed with PowerShell's `System.Drawing` (no ImageMagick or Pillow available in this
environment):
- `hero-store.jpg`: cropped to a 16:9 frame (4032×2268, offset to keep the storefront
  centered with some parking lot foreground and sky above), resized to 1920×1080, JPEG
  quality 70. **1920×1080, 293,420 bytes** (under the 350 KB budget).
- `hero-store-mobile.jpg`: cropped to a 4:5 frame (1814×2268, centered on the storefront
  facade), resized to 900×1125, JPEG quality 60. **900×1125, 123,124 bytes** (under the
  150 KB budget).

The mobile crop swaps in via a `<picture><source media="(max-width: 719px)">` in the
hero, not a CSS background-image media query, so the browser only downloads the crop it
needs.

Both crops sit inside `.hero__media`, which site.css already renders with
`filter: grayscale(1) contrast(1.06) brightness(0.9)` on the image and a graphite
gradient `.hero__scrim` over it (0.92 opacity at the strong side fading to 0.4/transparent)
— the exact same classes and values the hotels page (`slashyourenergycost.com/hotels/`)
uses for its building-photo hero, so the "teal panel with the storefront showing through
at roughly 25 to 30 percent" treatment the brief asked for is the root's own effect,
inherited for free rather than re-implemented.

### A grid min-width fix
`.hero` is `display: grid` with no explicit `grid-template-columns`; the root always
wraps its hero content in `.hero__grid`, whose children get `min-width: 0` so they can
shrink below their own content width in a narrow track. This page's hero has no second
column (no bill-graphic exhibit), so it doesn't use `.hero__grid`, and needed the same
`min-width: 0` rule applied directly to `.hero__in` — without it, the grid item's default
`min-width: auto` lets a long paragraph refuse to wrap to the viewport on narrow screens.

### The no-dash rule
Unchanged: ranges are written "20 to 24 percent," never with an en dash or em dash.

## Version 2 through 4: the placeholder skin (superseded)
Versions 2 through 4 shipped on `assets/brand.css`, a deliberately isolated placeholder
stylesheet built before the real Energy Plus brand was resolved. It defined every color,
font, spacing, and radius token the page used, plus structural classes for the header,
footer, ledger card, buttons, steps, and callouts. `assets/brand.css` is deleted as of
version 5; its job is now done by `assets/site.css` (shared with the live root) plus the
inline `<style>` block described above.
