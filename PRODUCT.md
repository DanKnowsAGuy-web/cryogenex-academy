# PRODUCT.md — Academy Sports + Outdoors proposal page

## Version 2 (September 2026)
Rebuilt around one idea, per Dan's decision: every Academy store pays three bills for
cooling (energy, led by the demand charge; maintenance; the equipment replacement cycle),
and one treatment moves all three. The page is one interactive exhibit, the roof ledger,
plus three short bill sections, a mechanism section, and the pilot ask. Version 1's
five-lever list, sales equation, spread chart, standalone calculator, and three-audience
accordion are gone; their content folded into the ledger and the three bill sections.

## Purpose
A single-file, Energy Plus branded proposal landing page for Academy Sports + Outdoors. The
reader is an Academy VP who opens this on a phone, then forwards it to facilities and finance.
Cryogenex brought the introduction and is credited as the partner; Energy Plus leads the
engineering, the measurement, and the incentive filing.

## Hard rules this page follows
- No em dashes or en dashes anywhere in copy. Ranges use "to".
- No product or vendor names in body copy (no CryoGenX4, HVAC Optimizer, Airco, Tri-S,
  Frontier). "Cryogenex" appears only in the header partner line, the CTA copy, and the
  footer.
- No Texas, Houston, Katy, ERCOT, 4CP, or "113" anywhere. Savings are framed as cooling's
  share of the bill for an average store, then multiplied by the 322-store fleet.
- No stock photos of Academy stores, no Academy logo, no federal agency logos. The only
  photos on the page are Cliff Suljak (grayscale) and the film cover.
- `<meta name="robots" content="noindex, nofollow">` plus a matching robots.txt.
- No third-party scripts. The only external calls are the Google Fonts stylesheet link and,
  on click only, the Wistia iframe for the film. Everything else is same-origin
  (`assets/brand.css`, the inline script).
- Mobile first, no horizontal scroll at 375px. Respects `prefers-reduced-motion`.
- Numbers are not invented: the roof ledger uses the compute() engine given in the build
  spec verbatim, with LOSS, STORES, KWH_STORE, RATE, COOL_KWH_SHARE, PEAK_KW, DEMAND_RATE,
  COOL_PEAK_SHARE, DEMAND_MAX, MAINT_TODAY, MAINT_MAX, ROOF_COST, LIFE_YEARS, and EXT_MAX
  as the only inputs. All narrative figures (Simon Property Group case, the 94 percent
  purchased-electricity note, the twelve-units-a-roof estimate) cite the spec's own sourcing.

## The roof ledger and DEMAND_MAX
The ledger's JavaScript is the compute() function from the build spec, copied verbatim,
with `DEMAND_MAX = 0.125`: at full fouling, up to 12.5 percent of cooling's share of the
peak kW is recoverable, scaling down with the fouling fraction (10 to 15 percent of
cooling's peak share is the working range described in the spec). The constant stands at
0.125. An earlier draft of this note flagged a mismatch against the spec's narrative
"expected" figures; that narrative arithmetic was in error, not the code, so it has been
corrected rather than the constant. At age 12, one store: $13,785 energy recovered a year,
$5,364 maintenance recovered a year, $3,302 equipment life recovered a year, $22,450 total
recovered a year. At the 322-store fleet scope: about $7.2M total recovered a year, and
$77.3M of replacement capital deferred (at the 3.9 year extension the age-12 fouling
fraction implies).

## Open decisions
- **Brand.** The real Energy Plus visual identity is not resolved. This version ships on a
  placeholder skin (see DESIGN.md); reskinning is a single-file swap of `assets/brand.css`.
- **Product naming.** Still white-labeled; no product name appears anywhere on the page.
- **VP identity.** Unknown. The page is written to work for facilities, finance, or ESG,
  since each owns one of the three bills, rather than addressing a named title.
- Whose calendar the "Book the 15 minute fit call" button should point to once a specific
  Academy contact is engaged (currently Dan's own booking link).

## Fleet wide, not Texas specific
This page pitches Academy as a big box fleet story, not a Texas story: it covers all 322
stores, not a regional subset. There is no reference anywhere in the page to Texas, Houston,
Katy, ERCOT, "4CP," or "113"; the demand charge is described generically ("the highest
fifteen minutes of the month"), and the pilot is "five stores." The ledger's fleet toggle
covers all 322 stores by default off (one store is the default view).

## Customer-specific strings and where they live
All of the following are specific to Academy Sports + Outdoors and should be revisited if
this page is ever reused as a template for another retailer:
- Header: "Prepared for Academy Sports + Outdoors"
- Hero label, H1, and lead copy (store count, twelve rooftop units per store)
- The roof ledger: `STORES` (322), `KWH_STORE`, `PEAK_KW`, `MAINT_TODAY`, `ROOF_COST`, and
  the fine print citing "Academy's public filings and industry norms for a 70,000 square
  foot big box"
- Bill one's mono note citing Academy's 2021 GHG supplement (94 percent purchased
  electricity)
- Offer section: five-store pilot structure, bottom-quartile (about eighty stores) rollout,
  Academy's twenty to twenty five store a year build-and-remodel cadence
- CTA band: Daniel Gutierrez contact details, booking link with `?f=academy` query param
- Footer: "prepared for Academy Sports + Outdoors"
