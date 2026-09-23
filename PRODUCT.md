# PRODUCT.md — Academy Sports + Outdoors proposal page

## Purpose
A single-file, Energy Plus branded proposal landing page for Academy Sports + Outdoors. The
reader is an Academy VP who opens this on a phone, then forwards it to facilities and finance.
Cryogenex brought the introduction and is credited as the partner; Energy Plus leads the
engineering, the measurement, and the incentive filing.

## Hard rules this page follows
- No em dashes or en dashes anywhere in copy. Ranges use "to".
- No product or vendor names in body copy (no CryoGenX4, HVAC Optimizer, Airco, Tri-S,
  Frontier). Levers are described by function. The case ledger keeps the customer names it
  already had (Simon Property Group, etc.). "Cryogenex" appears only in the header and footer
  partner line, plus the CTA copy.
- Savings are always framed as a share of the HVAC and cooling portion of the bill, never the
  whole bill.
- No stock photos of Academy stores, no Academy logo, no federal agency logos, no 179D
  reference.
- `<meta name="robots" content="noindex, nofollow">` plus a matching robots.txt.
- No external scripts. Google Fonts only. All CSS and JS inline. Works as a plain file open
  and on GitHub Pages.
- Mobile first, no horizontal scroll at 375px, 16px+ gutters. Respects
  `prefers-reduced-motion`.
- Numbers are not invented: the calculator and equation widgets use the engines given in the
  build spec verbatim; the stat tiles and stakes copy cite Academy's own public filings.

## Open decisions
- Whether to name the "product" (currently described only by function: restoration,
  runtime intelligence, demand staging, power conditioning, replacement) or introduce a
  branded name later in the sales process.
- Whether Cryogenex stays in the header long term, or moves to a footer-only credit once
  Energy Plus owns the relationship directly.
- Whose calendar the "Book the 15 minute fit call" button should point to once a specific
  Academy contact is engaged (currently Dan's own booking link).

## Customer-specific strings and where they live
All of the following are specific to Academy Sports + Outdoors and should be revisited if this
page is ever reused as a template for another retailer:
- Header: "Prepared for Academy Sports + Outdoors"
- Hero kicker, H1, and lead copy (store count, Texas cooling season framing)
- Stakes section: 322 stores / 113 Texas stores / 70,000 sq ft / 94% purchased electricity,
  and the 10-K / ESG Supplement footnote
- Equation section constants: `SALES_PER_STORE`, `TEXAS_STORES`, `FLEET_STORES`
- Calculator section constants: `TONS`, `SQFT`, store-count chips (5 / 113 / 322), and the
  124,514 tonne CO2e baseline referenced in the output tiles
- Offer section: Houston / Katy pilot geography, five-store pilot structure
- CTA band: Daniel Gutierrez contact details, booking link with `?f=academy` query param
- Footer: "prepared for Academy Sports + Outdoors"
